### 容器：

# String,StringBuffer 和 StringBuilder 类

String和StringBuffer，StringBuilder的区别：

和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。但是String的修改也就是产生新的对象。当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。修改是否产生新的对象可以从C++的引用概念去理解。

StringBuilder 类（快速）和 StringBuffer（线程安全，不能同步访问） 。

由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。

```java
public class Test{
    public static void main(String args[]){
        StringBuffer sBuffer = new StringBuffer("菜鸟教程官网：");
        sBuffer.append("www");  
        sBuffer.append(".runoob");     
        sBuffer.append(".com");     
        System.out.println(sBuffer);     
    } 
}
```

## Arrays