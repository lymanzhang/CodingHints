## JAVA programming hints

### java出现Resource leak: 'input' is never closed 解决方案

如下一段代码，input对象上出现这样的提示：
```java
Resource leak: 'input' is never closed
```

```java
package javaProgrammingTutorials.chapter01;

import java.util.Scanner;

public class Tuto_05 {
	public static void main(String[] args) {
  
		Scanner input = new Scanner(System.in);
    
			System.out.println("请输入学生人数: ");

			int nums = input.nextInt();
			int count = 0;

			for (int i = 0; i < nums; i++) {
				System.out.println("请输入第" + (i + 1) + "位学生的成绩: ");
				int score = input.nextInt();
				if (score >= 80) {
					count++;
				}
			}

			System.out.println("超过80分的学生人数为：" + count);
			double result = Double.parseDouble(count + "") / nums;
			System.out.println("80分以上的学生人数占比为：" + result * 100 + "%");
	}
}

```

而且程序运行时确实会出现问题。检索网站上提供的解决办法后，对程序作了如下改动（try()和finally()的调用）
```java
try {
.......
} finally {
			// TODO: handle finally clause
		}
```

```java
package javaProgrammingTutorials.chapter01;

import java.util.Scanner;

public class Tuto_05 {
	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);

		try {
			System.out.println("请输入学生人数: ");

			int nums = input.nextInt();
			int count = 0;

			for (int i = 0; i < nums; i++) {
				System.out.println("请输入第" + (i + 1) + "位学生的成绩: ");
				int score = input.nextInt();
				if (score >= 80) {
					count++;
				}
			}

			System.out.println("超过80分的学生人数为：" + count);

			double result = Double.parseDouble(count + "") / nums;
			System.out.println("80分以上的学生人数占比为：" + result * 100 + "%");
		} finally {
			// TODO: handle finally clause
			input.close();
		}

	}

}

```

程序正常运行
