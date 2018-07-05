## Java基础
### 面向对象有哪些基本特征？
面向对象有4个基本特征：封装、继承、多态、抽象。

1)抽象：抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么。

2)继承：继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的重要手段。

3)封装：通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口（可以想想普通洗衣机和全自动洗衣机的差别，明显全自动洗衣机封装更好因此操作起来更简单；我们现在使用的智能手机也是封装得足够好的，因为几个按键就搞定了所有的事情）。

4)多态性：多态性是指允许不同子类型的对象对同一消息作出不同的响应。简单的说就是用同样的对象引用调用同样的方法但是做了不同的事情。多态性分为编译时的多态性和运行时的多态性。如果将对象的方法视为对象向外界提供的服务，那么运行时的多态性可以解释为：当A系统访问B系统提供的服务时，B系统有多种提供服务的方式，但一切对A系统来说都是透明的（就像电动剃须刀是A系统，它的供电系统是B系统，B系统可以使用电池供电或者用交流电，甚至还有可能是太阳能，A系统只会通过B类对象调用供电的方法，但并不知道供电系统的底层实现是什么，究竟通过何种方式获得了动力）。方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2. 对象造型（用父类型引用引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。

### 访问修饰符public,private,protected,以及不写（默认）时的区别？

区别如下：

|   作用域  |  当前类   | 同包 | 子类 | 其他 |
| --- | --- | --- | --- | --- |
|  public   |   ✔  |  ✔ | ✔    | ✔  |
|  protected  |✔ | ✔ | ✔    |  ✘  |
| default | ✔ | ✔  |   ✘  |  ✘ |
| private| ✔ | ✘   |   ✘  |  ✘ |

类的成员不写访问修饰时默认为default。默认对于同一个包中的其他类相当于公开（public），对于不是同一个包中的其他类相当于私有（private）。受保护（protected）对子类相当于公开，对不是同一包中的没有父子关系的类相当于私有。

### String 是最基本的数据类型吗?

不是。Java中的基本数据类型只有8个：byte、short、int、long、float、double、char、boolean；除了基本类型（primitive type）和枚举类型（enumeration type），剩下的都是引用类型（reference type）。

### float f=3.4;是否正确?

不正确。3.4是双精度数，将双精度型（double）赋值给浮点型（float）属于下转型（down-casting，也称为窄化）会造成精度损失，因此需要强制类型转换float f =(float)3.4; 或者写成float f =3.4F;。
5、short s1 = 1; s1 = s1 + 1;有错吗?short s1 = 1; s1 += 1;有错吗?
答：对于short s1 = 1; s1 = s1 + 1;由于1是int类型，因此s1+1运算结果也是int 型，需要强制转换类型才能赋值给short型。而short s1 = 1; s1 += 1;可以正确编译，因为s1+= 1;相当于s1 = (short)(s1 + 1);其中有隐含的强制类型转换。
6、int 和Integer 有什么区别?
1、Integer是int的包装类，int则是java的一种基本数据类型 
2、Integer变量必须实例化后才能使用，而int变量不需要 
3、Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值 

### Integer的默认值是null，int的默认值是0
Java 为每个原始类型提供了包装类型：
原始类型: boolean，char，byte，short，int，long，float，double
包装类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double

``` javascript
1.	public class TestInteger {  
2.	    public static void main(String[] args) {  
3.	        int i = 128;  
4.	        Integer i2 = 128;  
5.	        Integer i3 = new Integer(128);  
6.	        System.out.println(i == i2); //Integer会自动拆箱为int，所以为true  
7.	        System.out.println(i == i3); //true，理由同上  
8.	        Integer i4 = 127;//编译时被翻译成：Integer i4 = Integer.valueOf(127);  
9.	        Integer i5 = 127;  
10.	        System.out.println(i4 == i5);//true  
11.	        Integer i6 = 128;  
12.	        Integer i7 = 128;  
13.	        System.out.println(i6 == i7);//false  
14.	        Integer i8 = new Integer(127);  
15.	        System.out.println(i5 == i8); //false  
16.	        Integer i9 = new Integer(128);  
17.	        Integer i10 = new Integer(128);  
18.	        System.out.println(i9 == i10);  //false  
19.	    } 
20.}  
```

简单的说，Integer 缓存池的大小默认为 -128~127，如果字面量的值在-128到127之间，那么不会new新的Integer对象，而是直接引用常量池中的Integer对象。 

new Integer(123) 与 Integer.valueOf(123) 的区别在于，new Integer(123) 每次都会新建一个对象，而 Integer.valueOf(123) 可能会使用缓存对象，因此多次使用 Integer.valueOf(123) 会取得同一个对象的引用。编译器会在自动装箱过程调用 valueOf() 方法，因此多个 Integer 实例使用自动装箱来创建并且值相同，那么就会引用相同的对象。valueOf() 方法的实现比较简单，就是先判断值是否在缓存池中，如果在的话就直接使用缓存池的内容。

Java 还将一些其它基本类型的值放在缓冲池中，包含以下这些：

 - boolean values true and false
 - all byte values
 - short values between -128 and 127
 - int values between -128 and 127
 - char in the range \u0000 to \u007F

因此在使用这些基本类型对应的包装类型时，就可以直接使用缓冲池中的对象。

总结如下：

  ①无论如何，Integer与new Integer不会相等。不会经历拆箱过程，i3的引用指向堆，而i4指向专门存放他的内存（常量池），他们的内存地址不一样，所以为false
  ②两个都是非new出来的Integer，如果数在-128到127之间，则是true,否则为false
  java在编译Integer i2 = 128的时候,被翻译成-> Integer i2 = Integer.valueOf(128);而valueOf()函数会对-128到127之间的数进行缓存
  ③两个都是new出来的,都为false
  ④int和integer(无论new否)比，都为true，因为会把Integer自动拆箱为int再去比
