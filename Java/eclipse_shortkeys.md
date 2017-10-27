### 添加注释

快捷键为：ALT + SHIFT +J

```java
/**
  * @param  
  * @return

  */
```

### 更换为其他的快捷键：

Window-->Preferences-->General-->Keys;找到"add javadoc comment"更改自己喜欢的快捷键。

### 如果觉得注释也不爽时也可以改改，修改的方法有两种：

- 直接在eclipse给的模板下进行修改

- 自己编写一个xml文档导入进去 

### 直接在eclipse给的模板下进行修改

- 打开eclipse

- Window-->Preferences-->Java-->Code Style --> Code Templates --> Comments --> types --> Edit

```java
/**   
*    
* 项目名称：${project_name}   
* 类名称：${type_name}   
* 类描述：   
* 创建人：${user}   
* 创建时间：${date} ${time}   
* 修改人：${user}   
* 修改时间：${date} ${time}   
* 修改备注：   
* @version    
*    
*/
```
