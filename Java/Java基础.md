# 面向对象
Java通过下述不同的功能支持了面向对象的封装，继承和多态。  
封装：访问权限关键字。  
继承：类与类继承extends，接口与接口实现implements。 （**`Java类不支持多继承，通过接口可以实现多继承`**）   
多态：重写override，重载。（此外，对继承提供支持的功能也对多态提供支持）  
## 三大特性：封装/继承/多态
**封装**：将数据与对数据的操作封装在一起构成实体，保护数据并尽可能隐藏内部细节，仅通过对外接口与外部交互。（解耦（可复用性，更利于分析可用性与高性能），易理解）  
**继承**：对IS-A关系的实现，即父子关系。（**`应遵循里氏替换原则，即子类实例必须能够替换所有父类实例`**）  
**多态**：方法具备多种不同的状态在具体场景可以实现不同的行为。  
**多态的种类**：  
（1）编译时多态：由方法的**重载**提供支持；  
（2）运行时多态：见**运行时多态的三个必要条件**小节。  
>重载：同一个类中，同名但参数列表（类型，个数，顺序任一）不同的方法，由编译器根据传入参数来选择实际调用的方法。（同名但返回值类型不同的方法会导致编译出错）
### 运行时多态的三个必要条件
（1）继承；  
（2）覆盖（重写override）；  
（3）向上转型：父类/接口引用子类/实现类实例；  
**重写override**：指子类实现一个与父类方法的声明完全相同的方法，并将其覆盖。  
子类重写方法必须添加@Override注解，提供编译检查子类方法是否满足里氏替换原则。（要求子类重写方法的访问权限>=父类等）
## 面向对象相关关键字
### 访问权限关键字
（封装的实现基础）  
**public**：允许不同包下访问。  
**protected**：允许同一包下&子类访问。  
**default**：（即不使用关键字）允许同一包下访问。  
**private**：仅允许本类访问。  
**访问权限关键字作用对象**：类（protected不能用于类），方法，变量。  
类的内部属性设为private，使用Getter/Setter获取&修改的原因：（首先这符合封装的思想）（1）更方便使用者调用（2）更方便代码检索。  
### this和super关键字
this和super关键字用于指代实例本身/父类实例，同时也是解决成员变量与局部变量冲突的方案。
**this**：只能使用在方法内部，this代表当前方法所属的实例（在构造方法内，则代表构造方法正在创建的实例）。（this()代表实例的构造方法，super()同理）  
> 一般this关键字不显式使用，只有在发生同名冲突时才会显式的使用this，如构造器属性赋值。

**super**：与this用法类似，代表当前实例的父类实例。（只能访问protected和public修饰的成员）  
（由于覆盖的存在）调用方法时，默认的访问顺序是：（1）this.func(子类方法参数列表)；（2）super.func(子类方法参数列表)；（3）this.func(转型为父类方法参数列表)；（4）super.func(转型为父类方法参数列表)。  

## 抽象类与接口
抽象类与接口提供更好的继承关系设计。
>Tips：抽象类/接口也可以在实例化对象时作为引用的接收类，如List list = new ArrayList()。  
### 抽象类abstract class
使用**abstract关键字**声明抽象类和抽象方法。  
**抽象类特点**：  
（1）不能实例化；  
（2）子类必须重写所有抽象方法。  
**抽象方法特点**：  
（1）只能定义在抽象类中；  
（2）构造方法和静态方法不能定义为抽象方法。  
### 接口interface
（多继承的实现基础）
**接口的特点**：
（1）成员变量&方法只支持public（Java9支持其他访问权限）；
（2）成员变量只支持静态变量/常量。
### 抽象类&接口的适用场景
**抽象类适用场景**：（1）需继承非静态/常量的成员变量（2）需控制继承的成员的访问权限。
**接口适用场景**：需**多继承方案**（大多数情况下，设计类间关系时接口的优先级高于抽象类）
# Object类
## Object类成员方法
```Java
// 判断实例是否相等（基本类型判值，引用类型判hashCode值）
// 常重写用于：业务场景判等逻辑
public boolean equals(Object obj)
// 获取实例的hashCode值
// 重写equals方法则必须重写hashCode方法
public native int hashCode()
// 默认获取实例的类名@HashCode
// 常重写用于：解析类对象为Json字符串
public String toString()
// 获取实例的类对象
public final native Class<?> getClass()
// 线程间通信 限时等待
public final native void wait(long timeout) throws InterruptedException
// 线程间通信 限时等待
public final void wait(long timeout, int nanos) throws InterruptedException
// 线程间通信 无限时等待
public final void wait() throws InterruptedException
// 线程间通信 唤醒指定的阻塞线程
public final native void notify()
// 线程间通信 唤醒所有阻塞线程
public final native void notifyAll()
//
protected native Object clone() throws CloneNotSupportedException  
//
protected void finalize() throws Throwable {}
```
## hashCode方法的作用
**作用**：利用Hash算法快速判断两个实例是否相等。极大的提升Java集合操作的性能。
>例：如果不使用Hash算法，对于有1w个元素的Set集合（不允许元素重复）来说，插入操作要执行1w次判等；
如果使用Hash算法，同样的Set，插入操作只需要对映射到同一个hashCode的链表/红黑树遍历判等即可，这通常会<8（不了解的同学请自行搜索哈希算法，以及[Java集合](https://github.com/mooneed/JavaBackendNotes/blob/main/Java/Java%E9%9B%86%E5%90%88.md)）；  
## 重写equals&hashCode方法
**重写equals方法的原因**：equals默认实现是判断引用是否为同一实例，不符合很多业务场景的判等逻辑。
**重写hashCode方法的原因**：重写equals方法必须重写hashCode方法，否则会违反Object类的规范，导致HashSet/HashMap/HashTable等基于hash值的类的操作出现错误。  
>Tips：equals方法判断相等的两个实例，则hashCode也需相等；反之，不作要求。（Object类的规范之一）  

>例：如果equals判等的Set的两个元素，hashCode不等，则在插入的过程中，不会映射到哈希表的相同位置，无法被重复检测逻辑检测到，故导致两个元素都成功插入到Set里，导致Set元素重复。
# 关键字
**面向对象相关关键字**：public/protected/private，this/super；（详见面向对象一节）
**异常关键字**：try/catch/finally，throw，throws；（详见异常一节）
**线程&并发相关关键字**：
**其他常用关键字**：final，static。
# 数据类型
待完善
## 基本类型
## 包装类型
## String
# 运算
待完善
# 反射
待完善
# 异常
**Throwable**：所有异常的父类，包括Error（JVM无法处理的错误）和Exception。**Exception**分为两种：  
（1）可检查异常：可使用try/catch/finally语句显式监听&捕获异常，实现对异常的处理并从异常中恢复。  
（2）不可检查异常：无法捕获，导致程序中止。如运算异常Arithmetic Exception（除 0 会引发）。  
## 异常关键字
**try**：监听异常。  
**catch**：捕获异常（try-catch为一对多关系）。  
**finally**：通常用于try-catch后的资源回收。  
**throw**：抛出异常（**`可检查异常的来源`**）。
**throws**：用于方法声明的尾部，声明方法可能抛出的异常类型。  

# 泛型
泛型可以理解为重载的上位替代（类似，但不是多态）。
**泛型的作用**：类型参数化。使类型作为一个参数传递，在建立实例时指定类中有**占位符**的变量/参数/返回值的数据类型。
```Java
public class ResDto<U> { // 此处声明占位符，如本样例中的U
    private int code;
    private String msg;
    private U data; // 成员变量使用占位符
    public U getData() { // 方法返回值使用占位符
        return data;
    }
    public void setData(U data) { // 方法参数使用占位符
        this.data = data;
    }
}
```
**泛型的优点**：（相比于重载）  
（1）可读性强；  
（2）代码复用；  
**泛型的向上转型**：支持传入类及其子类的实例作为参数，语法<? extends 类名>。  
>Tips：泛型支持编译时参数类型检查。  
# 注解
Annotation
**Java注解的作用**：用于在编译、运行时被解析并使用，起到说明、配置的功能。注解通常通过反射被handler获取，后对带有注解的类/方法/变量执行对应的逻辑。
**常见场景**：
（1）生成文档。Java最常见&最早提供的注解，如@param，@return等；
（2）配置功能。使用注解代替配置文件；
（3）编译时检查。如@override注解，检查是否满足里氏替换原则。
除Java提供的注解外，很多其他组件也提供丰富的注解，如Spring，Lombok等。
## 自定义注解
待完善
# 序列化
待完善
# Java8特性
（1）接口支持默认的方法实现；
（2）支持lambda表达式；
（3）支持stream流操作；

