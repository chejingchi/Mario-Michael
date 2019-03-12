# javaee

## java反射--Field用法实践

### Field是什么
Field是一个类,位于java.lang.reflect包下。在Java反射中Field类描述的是类的属性信息，功能包括：
1. 获取当前对象的成员变量的类型
2. 对成员变量重新设值

### 如何使用field
#### 如何获取field类对象
1. Class.getFields(): 获取类中public类型的属性，返回一个包含某些 Field 对象的数组，该数组包含此 Class 对象所表示的类或接口的所有可访问公共字段
2. getDeclaredFields(): 获取类中所有的属性(public、protected、default、private)，但不包括继承的属性，返回 Field 对象的一个数组
3. getField(String name)： 获取类特定的方法，name参数指定了属性的名称
4. getDeclaredField(String name): 获取类特定的方法，name参数指定了属性的名称