## 给定一个十进制数，如何转换为二进制数 Java的实现

### 方法一：利用Java API直接转换

十进制数如何转换为二进制数，这在Java API 中有一个方法，Integer.toBinaryString( ) 括号里面写上你要转换的十进制数，这样可以直接转换。

```java
public static void main(String[] args) {

        十进制转换为二进制
        System.out.println(Integer.toBinaryString(10));

    }
```
### 方法二：通过求余，求商，并计算值（例如：把二进制的1010 直接输成十进制的1010）实现

```java
public static void main(String[] args) {
        // TODO Auto-generated method stub

        int a = 123;//定义一个变量并赋给他一个十进制的值
        int remainder;//定义一个变量用于存储余数
        int sum = 0;//定义一个变量用于存放和
        int k = 1;//定义一个变量控制位数

        while(a != 0){

            remainder = a % 2;//对目标数字求余
            a /= 2;//对目标数字求商
            sum = sum + remainder * k;//求和
            k *= 10;//改变位数

        }
        System.out.println("10进制的123转换为2进制结果为：" + sum );
    }
```
但是这种方法存在一个问题：因为int类型是有取值范围的，如果转换的二进制数字超出了范围（例如：10011100110110）这个数字明显超出了int的取值范围，这样我们用int类型的sum进行存储的时候他就会自动转换为一个其他的数字。并且这个方法没有办法求负数的二进制数。

### 方法三：在方法二的基础上使用字符串对结果集进行存储

```java
public static void main(String[] args) {
        int n = -10;
        String result = "";
        boolean minus = false;

        //如果该数字为负数，那么进行该负数+1之后的绝对值的二进制码的对应位取反，然后将它保存在result结果中
        if(n < 0){
            minus = true;
            n = Math.abs(n + 1);
        }

        while(true){
            int remainder = (!minus && n % 2 == 0) || (minus && n % 2 == 1) ? 0 : 1;

            //将余数保存在结果中
            result = remainder + result;
            n /= 2;

            if(n == 0){
                break;
            }
        }

        //判断是否为负数，如果是负数，那么前面所有位补1
        if(minus){
            n = result.length();
            for(int i = 1; i <= 32 - n; i++){
                result = 1 + result;
            }
        }

        System.out.println(result);

    }
```
用这种方法就能很好解决int类型的越界问题，能解决所有的十进制转换二进制的问题。
