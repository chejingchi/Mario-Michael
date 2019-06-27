# spring 
## 学习记录
### Ordered接口介绍
#### 接口定义
`
public interface Ordered {
  
    int HIGHEST_PRECEDENCE = Integer.MIN_VALUE;

    int LOWEST_PRECEDENCE = Integer.MAX_VALUE;

    int getOrder();
  
}
`
#### OrderComparator接口

OrderComparator类：实现了Comparator接口的一个比较器。

提供了2个静态排序方法：sort(List<?> list)用来排序list集合、sort(Object[] array)用来排序Object数组
可以下OrderComparator类的public int compare(Object o1, Object o2)方法，可以看到另外一个类PriorityOrdered，这个方法的逻辑解析如下：
`
1. 若对象o1是Ordered接口类型，o2是PriorityOrdered接口类型，那么o2的优先级高于o1
2. 若对象o1是PriorityOrdered接口类型，o2是Ordered接口类型，那么o1的优先级高于o2
3. 其他情况，若两者都是Ordered接口类型或两者都是PriorityOrdered接口类型，调用Ordered接口的getOrder方法得到order值，order值越大，优先级越小
`

#### Spring中使用Ordered接口在的例子
`
如果配置了<mvc:annotation-driven/>，又配置了自定义的RequestMappingHandlerMapping，并且没有设置RequestMappingHandlerMapping的order值。那么<mvc:annotation-driven/>配置的RequestMappingHandlerMapping优先级高，因为<mvc:annotation-driven />内部会设置RequestMappingHandlerMapping的order为0。
`


转载于[链接](https://segmentfault.com/a/1190000012455485)


### spring 单例 解释
例如Web应用中的Servlet，每个方法中对局部变量的操作都是在线程自己独立的内存区域内完成的，所以是线程安全的。 
对于成员变量的操作，可以使用ThreadLocal来保证线程安全。 


springMVC中，一般Controller、service、DAO层的scope均是singleton；

每个请求都是单独的线程,即使同时访问同一个Controller对象，因为并没有修改Controller对象，相当于针对Controller对象而言，只是读操作，没有写操作，不需要做同步处理。
[spring 单例解释](https://blog.csdn.net/pingdouble/article/details/79493846)