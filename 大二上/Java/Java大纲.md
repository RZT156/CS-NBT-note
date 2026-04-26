# 第二节
对象
创建：new方法
实例化：对象名 = new 类名()
声明、实例化：类名 对象名 = new 类名()
类名 对象名 = new 构造器()

类：成员变量，构造器，方法
- 构造器
当一个类**没有显式定义任何构造器** 时，编译器才会**自动生成一个默认的无参构造**并初始化成员变量器；**==显式定义==了任意构造器** ，编译器就==**不会再自动生成无参构造器**==了
`super()`
`this(参数n，...)`**调用**同类其他**含n个参数**的构造器，==必须第一行==

包装类
# 第三节
- 复合：其他类作为组成部分构建新类
- Java源文件组成
类数量：可包含多个类（1个类对应1个class文件）
关键规则：最多1个public类，文件名与该类一致
- 深入研究方法
返回值类型：原始数据类型、引用数据类型
参数类型：原始数据类型、引用数据类型
传递方式：按值传递、引用传递
- 包
 缺省包：未指定package时的默认归属
`package 包名`
 命名：全小写、域名反向顺序（如cn.net.nit）
 导入：单个类（import 包名.类名）、整个包（import 包名.\*）
- 访问修饰符
public、默认、private、protected
==不写访问控制修饰符==即**默认修饰符**==默认只限于包访问==
# 第四节
static
**用类名**访问方法及变量
静态方法/类方法中==this==**不能访问变量不能访问方法**
static变量：**类共享**，重复调用时，不一定是默认值
# 第五节
省略super()语句，则父类中无参构造器还是会被调用；
super()必须写在子类构造器第一行。
无参构造器加`super()`这句
`this()`, `super()`都会执行对应参数构造器，都在第一行使用，this()调同类，super()调父类

子类重新定义父类成员时，访问控制修饰符不能更为**严格**！
final防止被继承

包装类->大写
# 第六节
String类
`charAt(int index);subString(int index);indexof(char key);`
Object类
`对象 instanceof 类型 return true/false`
`对象.equals(类) return true/false`
Abstract类
- 抽象函数无{}，无返回值；
- 抽象方法必须加absract修饰；
`访问控制修饰符 abstract class 类名{}`
`访问控制修饰符 abstract 类型 方法名(可以有参数);`
# 第七节
多态
方法重写，方法覆盖
# 第八节
接口
`interface 接口名{//对于接口，abstract是冗余的`
`void print();//对于接口方法，abstract,public是冗余的`
}`
- 可以继承但是不用implements因为下一行
- 都是抽象方法
- 成员变量自动具有public static final属性
- abstract方法默认public修饰符
 
类的完整定义
`修饰符 class 类名 [extends 父类] [implements 接口1,2...]{
`public 类型 抽象方法名(){}`==其中，public不能省，abstract不用写==
}`
类里要把接口抽象方法全部实现
# 第九节
[[第九节]]
**集合类**
java.util
ArrayList：
	遍历：for循环；增强for==不适用于int==；迭代器；
自带`ArrayList变量名.add(代添加变量);remove()方法`
	remove方法使用同add
**Collection**是根接口（就像Object和类的关系）

**泛型**
相当于标签<>，在具体使用的时候才会确定类型
可以确定在集合中存放的数据类型
只能为引用数据类型（对象）
**泛型标识**
- E - 元素
- T - Java类
- K - 键
- V - 值
- N - 数值类型
`class (类名)<泛型标识,泛型标识,···>{`
	`private T 变量名;`
`}`
Generic 类；Generic\<T>泛型
**实例化对象时，不指定泛型相当于Object类。推荐指定泛型**

**Random类**
# 第十节 异常处理
### 异常处理语法 try-catch 
try检查代码
catch异常处理
finally必须执行
![[异常.png]]
- **常用方法**
Throwable类

- **出异常两种方式：**
1.throw程序抛出
`throw new 某一异常("错误信息");`
程序抛出一般抛*自定义异常*，抛*系统内置异常*无意义

2.throws指定方法抛出
![[Throws.png]]
`[修饰符] 返回类型 方法(参数序列) throws 异常类型1,...{`
	`方法体`
`}`
throws必须使用try-catch来捕获
### 自定义异常
extends Exception
必须直接或间接继承Throwable类，通常从Exception类直接继承

# 第十一节 设计模式
工厂模式
1.简单工厂
2.工厂方法
3.抽象工厂
Scanner类
# 第十二/十三节 Java IO
java.io.*

路径：'/'和'\\\\'都可以表示文件构造
'\\'用来表示占位

字节数组`byte 对象名[] = new byte[128];`

*UTF-8/ GBK*转码
UTF-8:一个中文一般3个字节，GBK:一个中文两个字节
中文会乱码，默认一个字节一个字节读入。用字节数组控制读入字节个数，字节数组给几位，读入文件就是几位
英文和数字在任何编码集中都占一个字节，可通用，不会乱码
## 流
[[IO流]]
### ==按流向区分==
输入流->read->数据源（数据来源）
输出流->write->数据宿（接收数据）

**输入流**
**InputStream**
\[类型] available()
子类：FileInputStream()
**Reader**
\[类型] read(参数序列)
子类：BufferedReader()特有方法：readLine()

**输出流**
**OutputStream**
**Writer**
子类：FileOutputStream()
### ==按内容==
字节流->byte->一切
字符流->char->文本

**字节流**
处理一切文件复制
**FileInputStream()、FileOutputStream()**
数据流、对象流

**字符流**
处理文本
**FileReader()、FileWriter()**

### ==按功能==
**节点流**：低级文件可以直接使用

**处理流**：不能单独使用，在其他流基础上使用
缓冲流Buffered
提高字节字符流读写性能
# 第十四节
代理模式

行为模式
发布-订阅模式（观察者模式）
推模型：发布出去
拉模型：需要什么自取
# 第十五节
IO
**字节流**
数据流
对象流

**Serializable接口**

