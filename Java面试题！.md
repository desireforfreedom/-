[toc]

# 一、Java基础

## 	1、基础

#### 1.1  JDK 和 JRE 有什么区别？

> - JDK：Java Development Kit 的简称，java 开发工具包，提供了 java 的开发环境和运行环境。
> - JRE：Java Runtime Environment 的简称，java 运行环境，为 java 的运行提供了所需环境。
>
> 具体来说 JDK 其实包含了 JRE，同时还包含了编译 java 源码的编译器 javac，还包含了很多 java 程序调试和分析的工具。简单来说：如果你需要运行 java 程序，只需安装 JRE 就可以了，如果你需要编写 java 程序，需要安装 JDK。

#### 1.2 == 和 equals 的区别是什么？

>== 对于基本类型来说是值比较，对于引用类型来说是比较的是引用；而 equals 默认情况下是引用比较，只是很多类重新了 equals 方法，比如 String、Integer 等把它变成了值比较，所以一般情况下 equals 比较的是值是否相等。

#### 1.3  部分包装类型，如Interger 如果用 == 比较

> Integer/Short/Long/Byte 包装类里面有一个IntegerCache/shortCache/......，里面上限值是127 下限值是-128.这之间的比较比的是数值是否相等，超过这个范围只能创建新对象，地址不一致则为false。CharacterCache 只有0~1271`1

#### 1.4 两个对象的 hashCode()相同，则 equals()也一定为 true，对吗？ 

> 不对，两个对象的 hashCode()相同，equals()不一定 true。
> 因为在散列表中，hashCode()相等即两个键值对的哈希值相等，然而哈希值相等，并不一定能得出键值对相等。

#### 1.5 java中的final关键字的作用

> **可以用来修饰类，方法和引用**
>
> 被final修饰的类无法被继承
>
> 被final修饰的方法无法被重写
>
> 被final修饰的引用，引用不可变但引用内容可以修改，比如对象、数组，其本身可以被修改，但指向该对象的或数组得地址的引用不可被修改
>
> 当final修饰基本数据类型时，则会变为常量，值无法修改

#### 1.6 String str="i"与 String str=new String("i")一样吗？

> 不一样，因为内存的分配方式不一样。String str="i"的方式，java 虚拟机会将其分配到常量池中；而 String str=new String("i") 则会被分到堆内存中。

#### 1.7 抽象类和接口

> 抽象类和接口都不能用final修饰
>
> * 抽象类
>
>   > * 抽象类使用abstract关键字声明
>   > * 一个类只能继承一个抽象类，并且需要实现其所有抽象方法，否则该类仍是抽象类
>   > * 抽象类可以有非抽象方法，字段属性，可以有构造方法，但不可直接实例化，只有当实例化子类的时候才会调用父类构造方法初始化父类
>   > * 抽象类的子类使用 **extends** 来继承
>   > * 抽象类可以有 main 方法，并且我们能运行它
>
> * 接口
>
>   > * 接口使用interface关键字声明
>   >
>   > * 一个类可以实现多个接口
>   >
>   > * 一个接口可以**extends**多个接口
>   >
>   > * 接口必须使用 **implements** 来实现接口
>   >
>   > * 接口可以包含变量、方法；变量被隐式指定为**public static final**，方法被隐式指定为**public abstract**（JDK1.8之前）；
>   >
>   > * 接口也可以有 main 方法，并且我们能运行它
>   >
>   > * JDK1.8中对接口增加了新的特性：
>   >
>   >   （1）、默认方法（**default method**）：JDK 1.8允许给接口添加非抽象的方法实现，但必须使用**default**关键字修饰；定义了default的方法可以不被实现子类所实现，但只能被实现子类的对象调用；如果子类实现了多个接口，并且这些接口包含一样的默认方法，则子类必须重写默认方法；
>   >
>   >   （2）、静态方法（**static method**）：JDK 1.8中允许使用**static**关键字修饰一个方法，并提供实现，称为接口静态方法。接口静态方法只能通过接口调用（接口名.静态方法名）。

#### 1.8 BIO、NIO、AIO 有什么区别？

> * BIO：Block IO 同步阻塞式IO，就是我们平常使用的传统IO，特点是模式简单，使用方便，并发处理能力低
> * NIO：New IO 同步非阻塞式IO，是传统IO的升级，客户端和服务器端通过Channel（通道）通讯，实现了多路复用
> * AIO：是NIO的升级，也叫NIO2，实现了异步非阻塞IO，异步IO的操作基于事件和回调机制

#### 1.9 Files的常用方法都有哪些？

> - Files.exists()：检测文件路径是否存在。
> - Files.createFile()：创建文件。
> - Files.createDirectory()：创建文件夹。
> - Files.delete()：删除一个文件或目录。
> - Files.copy()：复制文件。
> - Files.move()：移动文件。
> - Files.size()：查看文件个数。
> - Files.read()：读取文件。
> - Files.write()：写入文件。

#### 1.10 String能被继承吗？为什么？为什么要用final修饰？

> 不能被继承，被final修饰了。为了安全性和效率。
>
> String类用final修饰一方面保证在多线程环境下的线程安全，如果字符串是可变的，那么可以通过改变引用地址指向的值去修改字符串的值，从而导致安全漏洞。
>
> 另一方面可以节约字符串常量池内存和提升性能，因为不同的字符串变量指向相同的字面量时，都是指向字符串常量池中的同一个对象。这样一方面能够节约内存，另一方面也提升了性能。

#### 1.11 String、StringBuffer、StringBuilder 的区别？

> [string、stringbuffer和stringbuilder的区别是什么？](https://www.php.cn/java/base/464289.html#:~:text=区别：Strin,，且非线程安全。)
>
> String 不可变 ；StringBuffer 可变 线程安全；StringBuilder 可变 不安全 效率更高。

#### 1.12 类的实例化顺序

> 当new的时候  加载顺序如下
>
> 父类静态变量和父类静态代码块-->子类静态变量和子类静态代码块-->父类实例成员变量-->父类构造函数-->子类实例成员变量--> 子类构造函数

#### 1.13 Java创建对象的方式

> * 使用new关键字
> * 使用反射机制
>   * 使用Class类的newInstance方法
>   * 使用Constructor类的newInstance方法
> * 使用clone
> * 使用反序列化

#### 1.14 浅拷贝和深拷贝的区别

> 浅拷贝：
> 被复制对象的所有变量都含有与原来的对象相同的值，而所有的对其他对象的引用仍然指向原来的对象。即对象的浅拷贝会对“主”对象进行拷贝，但不会复制主对象里面的对象。”里面的对象“会在原来的对象和它的副本之间共享。`简而言之，浅拷贝仅仅复制所考虑的对象，而不复制它所引用的对象。`
>
> 深拷贝：
> 深拷贝是一个整个独立的对象拷贝，深拷贝会拷贝所有的属性,并拷贝属性指向的动态分配的内存。当对象和它所引用的对象一起拷贝时即发生深拷贝。深拷贝相比于浅拷贝速度较慢并且花销较大。`简而言之，深拷贝把要复制的对象所引用的对象都复制了一遍。`

#### 1.15 switch语句在JDK1.7前后所接受的类型

> 数据类型接受 byte short int char enum(枚举)，String 六种类型

#### 1.16 访问修饰符public，private，protected，以及不写时的区别？

> ​						当前类	同包  子类	其他包
>
> * public 	√			√			√			√
> * protect   √            √            √            x
> * 不写        √             √            x（不同包子类）           x
> * private    √            x            x           x

#### 1.17 String s = new String("xyz") 创建了几个字符串对象？

> 一个或两个。如果字符串常量池已经有“xyz”，则是一个；否则，两个。
>
> 当字符创常量池没有 “xyz”，此时会创建如下两个对象：
>
> 一个是字符串字面量 "xyz" 所对应的、驻留（intern）在一个全局共享的字符串常量池中的实例，此时该实例也是在堆中，字符串常量池只放引用。
>
> 另一个是通过 new String() 创建并初始化的，内容与"xyz"相同的实例，也是在堆中。

#### 1.18 String s = "xyz" 和 String s = new String("xyz") 区别？

> 两个语句都会先去字符串常量池中检查是否已经存在 “xyz”，如果有则直接使用，如果没有则会在常量池中创建 “xyz” 对象。
>
> 另外，String s = new String("xyz") 还会通过 new String() 在堆里创建一个内容与 "xyz" 相同的对象实例。
>
> 所以前者其实理解为被后者的所包含。

#### 1.19 Java面向对象的三大特征

> * 封装：是指隐藏对象的属性和实现细节，仅对外提供公共访问方式。
>
> * 继承：从已有的类中派生出新的类，新的类能吸收已有类的数据属性和行为，并能扩展新的能力；
>
> * 多态：一个方法可以有多种实现版本，即“一种定义， 多种实现”。
>
>   * **多态存在的必要条件：**
>
>     1、要有继承；
>
>     2、要有重写；
>
>     3、父类引用指向子类对象。
>
>   * 实现多态的方式：
>
>     * 接口实现；
>     * 继承父类进行方法重写；
>     * 同一个类中进行方法重载。



****



## 	2、反射

#### 2.1 什么是反射？

> 反射是在运行过程中，对于任意一个类都能能够知道其所有属性和方法，对于任意一个对象，都能调用它的任意方法和属性，这种动态的获取信息和调用方法的功能就是Java的反射机制。

#### 2.2 反射的实现方式都有什么？

> 获取Class对象有这些方法：
>
> * Class.forName(“类的路径”)
> * 类名.class
> * 对象名.getClass()
> * 基本类型的包装类，可以调用包装类的Type属性来获得该包装类的Class对象。

#### 2.3 实现java反射的类有什么？

> (1)Class 类：反射的核心类，可以获取类的属性，方法等信息。
>
> (2)Field 类：Java.lang.reflec 包中的类，表示类的成员变量，可以用来获取和设置类之中的属性值。
>
> (3)Method 类：Java.lang.reflec 包中的类，表示类的方法，它可以用来获取类中的方法信息或者执行方法。
>
> (4)Constructor 类：Java.lang.reflec 包中的类，表示类的构造方法。

#### 2.4 set()可以访问私有属性嘛？

> 不可以，需要打破封装，才可以。
>
> public void setAccessible(boolean flag)	默认false，设置为true为打破封装

#### 2.5 什么是 java 序列化？什么情况下需要序列化？

> 序列化：将 Java 对象转换成字节流的过程。
>
> 反序列化：将字节流转换成 Java 对象的过程。
>
> 序列化的实现：类实现 Serializable 接口，
>
> 什么情况下需要序列化：
> a）当你想把的内存中的对象状态保存到一个文件中或者数据库中时候；
> b）当你想用套接字在网络上传送对象的时候；
> c）当你想通过RMI传输对象的时候；

****



## 	3、 集合

#### 3.1 什么是集合？

> * 集合就是一个存放数据对象引用的容器
> * 集合存放的只是引用，而不是对象的本身
> * 集合类型主要有3中 set（集），list（列表）和map（映射）

#### 3.2 集合和数组的区别

> - 数组是固定长度的；集合可变长度的。
> - 数组可以存储基本数据类型，也可以存储引用数据类型；集合只能存储引用数据类型。集合并没有直接存储基本类型，而是将基本类型转化为继承制Object的包装类，所以集合只能接受Object的子类作为值。
> - 数组存储的元素必须是同一个数据类型；集合存储的对象可以是不同数据类型。

#### 3.3 常用的集合类有哪些？

> **Map接口和Collection接口是所有集合框架的父接口：**
>
> * Collection下面常用的有Set和List，queue不常用
>   * Set
>     * HashSet
>     * LinkedHashSet
>     * TreeSet
>   * List
>     * ArrayList
>     * LinkedList
>     * Vector
> * Map下面常用的有：
>   * HashMap
>   * HashTable
>   * LinkedHashMap
>   * TreeMap
>   * ConcurrentHashMap
>
> >* 其中线程安全的有：Vector、HashTable、ConcurrentHashMap
> >
> >* 有序的集合有：ArrayList、LinkedList、Vector、TreeSet、LinkedHashSet、TreeMap、LinkedHashMap
> >
> >* set集合唯一不可重复，只能存放一个null
> >
> >* List都可以添加null元素
> >* HashMap可以有1个key为null的元素，TreeMap不能有key为null的元素
> >*  Set底层是Map，所以HashSet可以有1个null的元素，TreeSet不能有key为null的元素。
> >
> >- HashTable底层为散列表，无论是**key为null，还是value为null，都会报错**

#### 3.4 ArrayList和LinkedList有什么区别？

> * ArrayList的实现是基于数组，LinkedList的实现是基于双向链表。
> * 对于查询操作ArrayList速度快于LinkedList
> * 对于增删操作LinkedList更快一些
> * LinkedList比ArrayList更占内存，因为LinkedList的节点除了存储数据，还存储了两个引用，一个指向前一个元素，一个指向后一个元素。

#### 3.5 怎么确保一个集合不能被修改？

> - 可以使用 Collections. unmodififiableCollection(Collection c) 方法来创建一个只读集合，这样改变集合的任何操作都会抛出 Java. lang. UnsupportedOperationException 异常。

#### 3.6 迭代器 Iterator 是什么？

> Iterator接口提供遍历任何Collection的接口，我们可以从一个Collection中使用迭代器方法来获取迭代器实例。
>
> 其使用方法如下：
>
> ```java
> List<String> list = new ArrayList<>();
> Iterator<String> it = list.iterator();
> while(it.hasNext()){
> String obj = it. next();
> System. out. println(obj);
> }
> ```

#### 3.7 如何边遍历边移除 Collection 中的元素？

> 在迭代器遍历中，使用 Iterator.remove()方法

#### 3.8  Iterator 和 ListIterator 有什么区别？

> Iterator 可以遍历 Set 和 List 集合，而 ListIterator 只能遍历 List。
> Iterator 只能单向遍历，而 ListIterator 可以双向遍历（向前/后遍历）。
> ListIterator 实现 Iterator 接口，然后添加了一些额外的功能，比如添加一个元素、替换一个元素、获取前面或后面元素的索引位置。

#### 3.9 如何实现数组和 List 之间的转换？

> - 数组转 List：使用 Arrays. asList(array) 进行转换。
> - List 转数组：使用 List 自带的 toArray() 方法。

#### 3.10  多线程场景下如何使用 ArrayList 或者 HashMap？

> ArrayList 不是线程安全的，如果遇到多线程场景，可以通过 Collections 的 synchronizedList / synchronizedMap 方法将其转换成线程安全的容器后再使用。

#### 3.11 HashMap的实现原理 

> hashMap使用的是数组+链表+红黑树的存储结构，初始默认大小是16（1.7之前，1.7之后初始为0，当加入第一个元素后才会扩容为16），负载因子为0.75，当进行put操作时，它会首先根据key然后getHashCode，然后根据hashcode计算出在数组中位置并存入，当该位置已经有元素存在时，会再根据hashcode判断是否是同一个元素，是的话覆盖掉原来的元素，不是的话，它会以链表的形式追加在该位置上，当链表长度大于8个的时候，链表会转为红黑树，当存入元素后会判断HashMap的大小是否需要扩容，扩容时会检查树节点的个数是否小于等于6，符合条件则会从红黑树再次转换为链表。进行get操作时则会先进行containsKey操作，计算key的hash值，找到对应的位置后进行equals比较，最后得到对应的value。
>
> **hashmap 2倍扩容 ArrayList 1.5倍  vector 2倍**

#### 3.12 HashMap中红黑树退化成链表的条件

> * 扩容 resize( ) 时，红黑树拆分成的 树的结点数小于等于临界值6个，则退化成链表。
> * 移除元素 remove( ) 时，在removeTreeNode( ) 方法会检查红黑树是否满足退化条件，与结点数无关。如果红黑树根 root 为空，或者 root 的左子树/右子树为空，root.left.left 根的左子树的左子树为空，都会发生红黑树退化成链表。
>
> ```java
> //remove时
> //在removeTreeNode()的方法中，满足一定条件后会退化成链表
> //条件中的movable是remove()方法传进来的true，ctrl+f没有发现哪里有做更改
> //如果红黑树根root为空，或者root的左子树/右子树为空，root.left.left根的左子树的左子树为空
> //这几种情况都会发生红黑树退化成链表
> if (root == null
>     || (movable
>         && (root.right == null
>             || (rl = root.left) == null
>             || rl.left == null))) {
>     tab[index] = first.untreeify(map);  // too small
>     return;
> }
> ```

#### 3.12 HashSet如何检查重复

> 当你把对象加入HashSet时，HashSet会先计算对象的hashcode值来判断对象加入的位置，同时也会与其他加入的对象的hashcode值作比较，如果没有相符的hashcode，HashSet会假设对象没有重复出现。但是如果发现有相同hashcode值的对象，这时会调用equals()方法来检查hashcode相等的对象是否真的相同。如果两者相同，HashSet就不会让加入操作成功。

#### 3.13 TreeMap

> - TreeMap 是一个有序的key-value集合，它是通过红黑树实现的。

#### 3.15 hashTable

> `HashTable`是线程安全的,但是`HashTable`在对集合元素操作的方法上都加了`synchronized`。虽然安全但性能低下。

#### 3.14  ConcurrentHashMap详解

>  `ConcurrentHashMap`是线程安全的，`ConcurrentHashMap`并非锁住整个方法，而是通过原子操作和局部加锁的方法保证了多线程的线程安全，且尽可能减少了性能损耗。
>
> * 在jdk1.7及其以下的版本中，使用的是分段锁保证安全。结构是用Segments数组 + HashEntry数组 + 链表实现的，Segments数组中每一个元素就是一个段，每段里面存放一个entry数组，结构相当于一个hashmap，所以在高并发场景下，每次修改内容时只会锁住segment数组的每个元素，
> *  在JDK1.8中，对ConcurrentHashMap的结构做了一些改进，其中最大的区别就是jdk1.8抛弃了Segments数组，摒弃了分段锁的方案，而是改用了和HashMap一样的结构操作，也就是数组 + 链表 + 红黑树结构，每次加锁在链表的头结点，锁的粒度减小了，效率更高了，在并发方面，使用了cas + synchronized的方式保证数据的一致性；

#### 3.15 列表去重的方法

> * 把List数据放入Set
>
>   ```java
>    //简写的方法
>    List<String> newList = new ArrayList<>(new HashSet<>(list));
>   ```
>
> * 先用stream方法将集合转换成流，然后distinct去重，最后在将Stream流collect收集为List。
>
>   ```java
>   List<String> newList = list.stream().distinct().collect(Collectors.toList());
>   ```
>
> * 利用set.add(T),如果T元素已经存在集合中，就返回false。利用这个方法进行是否重复的数据判断，如果不重复就放入一个新的newList中，这个newList就是最终的去重结果
>
> * 使用newList.contains(T)方法，在向新的List添加数据的时候判断这个数据是否已经存在，如果存在就不添加，从而达到去重的效果。

****



## 	4、锁

#### 4.1 java锁是什么？

> - 多线程同步操作的实现需要给对象一个互斥体，这个互斥体就可以叫做锁

#### 4.2 锁的实现方式

> - java中锁的实现方式有两种，synchronized关键字和并发包（java.util.current）中的锁类

#### 4.3 死锁

> - 线程之间相互等待着对方释放资源，而自己的资源又不释放给别人，这种情况就是死锁
> - 导致死锁的条件有四个，也就是这四个条件同时满足就会产生死锁。
>   - 互斥条件，共享资源 X 和 Y 只能被一个线程占用；
>   - 请求和保持条件，线程 T1 已经取得共享资源 X，在等待共享资源 Y 的时候，不释放共享资源 X；
>   - 不可抢占条件，其他线程不能强行抢占线程 T1 占有的资源；
>   - 循环等待条件，线程 T1 等待线程 T2 占有的资源，线程 T2 等待线程 T1 占有的资源，就是循环等待。
> - 按照死锁发生的四个条件，只需要破坏其中的任何一个，就可以解决，但是，互斥条件是没办法破坏的，因为这是互斥锁的基本约束，其他三方条件都有办法来破坏：
>   - 设置超时时间，超时可以退出，防止死锁
>   - 降低锁的使用粒度，尽量不要几个功能用同一把锁
>   - 我们可以一次性申请所有的资源，这样就不存在等待了

#### 4.4 公平锁、非公平锁、可重入锁、独占锁

> - 公平锁是指在分配时候考虑线程排队等待的情况，优先将该锁分配给排队时间最长的线程
> - 非公平锁指在分配时候不考虑线程排队等待的情况，直接尝试获得锁，在获取不到锁时候再排队，到队尾等待
> - 可重入锁也叫递归锁，指在同一个线程中，在外层函数获得该锁之后，内层的递归函数依旧可以继续获取该锁
> - 独占锁指该锁在同一个时间只能被同一个线程获得，而没有获得锁的其他线程只能在同步队列中等待

#### 4.5 自旋锁、自适应自旋锁

> - 自旋锁
>   - 线程在没有获得锁时不会被挂起，而是一直执行一个空循环，默认10次
>   - 自旋锁的目的是减少线程被挂起的次数，线程的挂起和释放都是耗费资源的
>   - 自旋锁不适合时间长的并发情况，因为自旋时间过长还是会被挂起
> - 自适应自旋锁
>   - 是对自旋锁的一种优化，当一个线程自旋获得锁之后，那么下次自旋的次数就会增加，相反假如没有获得锁，下次会减少自旋次数

#### 4.6 Synchronized 与 ReentrantLock 的区别

> **1.1 底层实现的区别**
>
> - synchronized 是 JVM 层面的锁，是 Java 关键字，通过 monitor 对象来完成，synchronized 的实现涉及到锁的升级，具体为无锁、偏向锁、自旋锁、重量级锁
> - 而 ReentrantLock 是由 java api 去实现的。ReentrantLock 实现则是通过利用CAS自旋机制保证线程操作的原子性和 `volatile` 保证数据可见性以实现锁的功能。
>
> **1.2 是否可手动释放**
>
> - synchronized 不需要用户去手动释放锁，synchronized 代码执行完后系统会自动让线程释放对锁的占用。
> - ReentrantLock 则需要用户去手动释放锁，如果没有手动释放锁，就可能导致死锁现象。一般通过 lock() 和 unlock() 方法配合 try / finally 语句块来完成，使用释放更加灵活。
>
> **1.3 是否可中断**
>
> - synchronized 是不可中断类型的锁，除非加锁的代码中出现异常或正常执行完成。
> - ReentrantLock 则可以中断，可通过 trylock(long timeout,TimeUnit unit) 设置超时方法；或者将 lockInterruptibly() 放到代码块中，调用 interrupt 方法进行中断。
>
> **1.4 是否公平锁**
>
> - synchronized 为非公平锁。
> - ReentrantLock 则即可以选公平锁也可以选非公平锁，通过构造方法 new ReentrantLock 时传入 boolean 值进行选择，为空默认 false 非公平锁，true 为公平锁。
>
> **1.5 锁是否可绑定条件 Condition**
>
> - synchronized 不能绑定。
> - ReentrantLock 通过绑定 Condition 结合 await() / singal() 方法实现线程的精确唤醒，而不是像 synchronized 通过 Object 类的 wait() / notify() / notifyAll() 方法要么随机唤醒一个线程要么唤醒全部线程。
>
> **1.6 锁的对象**
>
> - synchronzied 锁的是对象，锁是保存在对象头里面的，根据对象头数据来标识是否有线程获得锁 / 争抢锁。
> - ReentrantLock 锁的是线程，根据进入的线程和 int 类型的 state 标识锁的获得 / 争抢。

#### 4.7 synchronized和lock有什么区别

> - 1：synchronized 是 JVM 层面的锁，是 Java 关键字，通过 monitor 对象来完成，synchronized 的实现涉及到锁的升级，具体为无锁、偏向锁、自旋锁、重量级锁，而Lock是java.util.concurrent.Locks 包下的一个接口；
> - 2：Synchronized 使用过后，会自动释放锁，而Lock需要手动上锁、手动释放锁。（在 finally 块中）
> - 3：synchronized 关键字不能响应中断；Lock可以响应中断、可定时
> - 4：synchronized关键字是非公平锁，即，不能保证等待锁的那些线程们的顺序，而Lock的子类ReentrantLock默认是非公平锁，但是可通过一个布尔参数的构造方法实例化出一个公平锁；
> - 5：synchronized无法判断，是否已经获取到锁，而Lock通过tryLock()方法可以判断，是否已获取到锁；
> - 6：Lock可以通过分别定义读写锁提高多个线程读操作的效率。
> - 7：二者的底层实现不一样：synchronized是同步阻塞，采用的是悲观并发策略；Lock是同步非阻塞，采用的是乐观并发策略（底层基于volatile关键字和CAS算法实现）

#### 4.8 synchronized 和 volatile 的区别是什么？

> - volatile本质是在告诉jvm当前变量在寄存器（工作内存）中的值是不确定的，需要从主存中读取； synchronized则是锁定当前变量，只有当前线程可以访问该变量，其他线程被阻塞住。
> - volatile仅能使用在变量级别；synchronized则可以使用在变量、方法、和类级别的。
> - volatile仅能实现变量的修改可见性，不能保证原子性；而synchronized则可以保证变量的修改可见性和原子性。
> - volatile不会造成线程的阻塞；synchronized可能会造成线程的阻塞。
> - volatile标记的变量不会被编译器优化；synchronized标记的变量可以被编译器优化。



#### 4.9 Volatile如何保证可见性

> *Volatile有两个特性：*
>
> - 一种是保证该变量对所有的线程可见
> - 一种是禁止指令重排，即Volatile变量不会被缓存在寄存器或是对其他处理器不可见的地方
>
> *volatile修饰的变量，JMM将在写操作后插入一个写屏障指令，在读操作前插入一个读屏障指令，这代表着：*
>
> - 一旦对变量写入了新值，任何访问这个变量的线程都会得到新的值
> - 在写入前，也会保证所有之前发生的事情已经发生，并且更新过的数据值也是可见的。内存屏障会把之前的写入值都刷新到主内存
>
> 所以Volatile可以保证可见性

****



##  	5、多线程

#### 5.1 并行和并发有什么区别？

> - 并行是指两个或者多个事件在同一时刻发生；而并发是指两个或多个事件在同一时间间隔发生。
> - 并行是在不同实体上的多个事件，并发是在同一实体上的多个事件。

#### 5.2 线程和进程的区别？

> 简而言之，进程是程序运行和资源分配的基本单位，一个程序至少有一个进程，一个进程至少有一个线程。线程是进程的一个实体，是cpu调度和分派的基本单位，是比程序更小的能独立运行的基本单位。同一进程中的多个线程之间可以并发执行。

#### 5.3  守护线程是什么？

> 守护线程（即daemon thread），是个服务线程，准确地来说就是服务其他的线程。

#### 5.4 创建线程有哪几种方式？

> * 继承Thread类，重写run()方法
>
> * 实现Runnable接口，重写run()方法， 无返回值
>
> * 实现Callable接口，重写call()方法， 有返回值 ，和Future、FutureTask配合可以用来获取异步执行的结果。
>
> * 通过线程池创建
>
> * Timer创建，本质还是继承了Thread 类
>
>   ```java
>   public class MyTimer {
>         
>       public static void main(String[] args) {
>           timer();
>       }
>       /**
>        * 指定时间 time 执行 schedule(TimerTask task, Date time)
>        */
>       public static void timer() {
>           Timer timer = new Timer();
>           // 设定指定的时间time,此处为2000毫秒
>           timer.schedule(new TimerTask() {
>               public void run() {
>                   System.out.println("执行定时任务");
>               }
>           }, 2000);
>       }
>   }
>   ```

#### 5.5 线程有哪些状态？

> 线程通常都有五种状态，创建、就绪、运行、阻塞和死亡。

#### 5.6 sleep() 和 wait() 有什么区别？

> * sleep是Thread类的方法，wait是Object的方法
> * sleep不会释放同步锁，wait会
> * sleep 让调用线程进入睡眠状态，等到休眠时间结束后会再执行，。wait 线程需要被notify唤醒
> * wait，notify和notifyAll只能在同步控制方法或者同步控制块里面使用，而sleep可以在
>       任何地方使用

#### 5.7 notify()和 notifyAll()有什么区别？

> - 如果线程调用了对象的 wait()方法，那么线程便会处于该对象的等待池中，等待池中的线程不会去竞争该对象的锁。
> - 当有线程调用了对象的 notifyAll()方法（唤醒所有 wait 线程）或 notify()方法（只随机唤醒一个 wait 线程），被唤醒的的线程便会进入该对象的锁池中，锁池中的线程会去竞争该对象锁。也就是说，调用了notify后只要一个线程会由等待池进入锁池，而notifyAll会将该对象等待池内的所有线程移动到锁池中，等待锁竞争。
> - 优先级高的线程竞争到对象锁的概率大，假若某线程没有竞争到该对象锁，它还会留在锁池中，唯有线程再次调用 wait()方法，它才会重新回到等待池中。而竞争到对象锁的线程则继续往下执行，直到执行完了 synchronized 代码块，它会释放掉该对象锁，这时锁池中的线程会继续竞争该对象锁。

#### 5.8 线程的 run()和 start()有什么区别？

> start()方法来启动一个线程，真正实现了多线程运行。这时无需等待run方法体代码执行完毕，可以直接继续执行下面的代码； 这时此线程是处于就绪状态， 并没有运行。 然后通过此Thread类调用方法run()来完成其运行状态， 这里方法run()称为线程体，它包含了要执行的这个线程的内容， Run方法运行结束， 此线程终止。然后CPU再调度其它线程。
> run()方法是在本线程里的，只是线程里的一个函数,而不是多线程的。 如果直接调用run(),其实就相当于是调用了一个普通函数而已，直接待用run()方法必须等待run()方法执行完毕才能执行下面的代码，所以执行路径还是只有一条，根本就没有线程的特征，所以在多线程执行时要使用start()方法而不是run()方法。

#### 5.9 创建线程池有哪几种方式？

> ①. newFixedThreadPool(int nThreads)
> 创建一个固定长度的线程池，每当提交一个任务就创建一个线程，直到达到线程池的最大数量，这时线程规模将不再变化，当线程发生未预期的错误而结束时，线程池会补充一个新的线程。
> ②. newCachedThreadPool()
> 创建一个可缓存的线程池，如果线程池的规模超过了处理需求，将自动回收空闲线程，而当需求增加时，则可以自动添加新线程，线程池的规模不存在任何限制。
> ③. newSingleThreadExecutor()
> 这是一个单线程的Executor，它创建单个工作线程来执行任务，如果这个线程异常结束，会创建一个新的来替代它；它的特点是能确保依照任务在队列中的顺序来串行执行。
> ④. newScheduledThreadPool(int corePoolSize)
> 创建了一个固定长度的线程池，而且以延迟或定时的方式来执行任务，类似于Timer。

#### 5.10 线程池都有哪些状态？

> **（1）RUNNING；**
>
> ​     ● 线程池处于RUNNING状态时，线程池能够接收新任务，也能够对已经添加的任务进行处理；
>
> ​     ● 线程池一被创建，线程池的状态就是RUNNING状态；
>
> **（2）SHUTDOWN；**
>
> ​     ● 线程池已经被关闭了，不再接收新任务；但是，其还是会处理队列中的剩余的任务；
>
> ​     ● 调用线程池的shutdown()方法后，线程池的状态就会由RUNNING转为SHUTDOWN；
>
> **（3）STOP；**
>
> ​     ● 线程池处于STOP状态，此时线程池不再接收新任务，不处理已经添加进来的任务，并且会中断正在处理的任务； 
>
> ​     ● 调用线程池的shutdownNow()方法后，线程池的状态就会由RUNNING或SHUTDOWN转为STOP；
>
> **（4）TIDYING；**
>
> ​     ● 如果线程状态已经是SHUTDOWN了，并且线程中以及队列中都没有任务时，线程池就会由SHUTDOWN转为TIDYING；如果线程池状态为STOP，那么当线程池把所有的任务都给清理干净时，线程池就会由STOP转为TIDYING；
>
> **（5）TERMINATED；**
>
> ​     ● 线程池就结束了；线程池就不能重新启动了；
>
> ​     ● 如果线程池处于TIDYING状态，那么当线程池执行完terminated()方法后，线程池状态就会由TIDYING转为TERMINTED；

#### 5.11  线程池中 submit()和 execute()方法有什么区别？

> - 接收的参数不一样
> - submit有返回值，而execute没有
> - submit方便Exception处理

#### 5.12 在 java 程序中怎么保证多线程的运行安全？

> 线程安全在三个方面体现：
>
> - 原子性：提供互斥访问，同一时刻只能有一个线程对数据进行操作，（atomic,synchronized）；
> - 可见性：一个线程对主内存的修改可以及时地被其他线程看到，（synchronized,volatile）；
> - 有序性：一个线程观察其他线程中的指令执行顺序，由于指令重排序，该观察结果一般杂乱无序，（happens-before原则）。

****



## 	6、设计模式

#### 6.1 单例模式

> 1. 为什么要有单例模式
>
>    > 实际编程应用场景中，有一些对象其实我们只需要一个，比如线程池对象、缓存、系统全局配置对象等。这样可以就保证一个在全局使用的类不被频繁地创建与销毁，节省系统资源。
>
> 2. 单例模式的特点
>
>    > * 单例类只能有一个实例。 
>    > * 单例类必须自己创建自己的唯一实例。 
>    > * 单例类必须给所有其他对象提供这一实例。
>
> 3. 单例模式的7种实现，推荐枚举方式
>
>    * **饿汉式—静态常量方式（线程安全）** 类加载时就初始化实例，避免了多线程同步问题。天然线程安全。
>
>      ```java
>      public class Singleton {
>          private final static Singleton singleton = new Singleton();
>          private Singleton (){}
>          public static Singleton getInstance() {
>              return singleton;
>          }
>      }
>      ```
>
>    * **懒汉式（线程不安全）**这是最基本的实现方式，第一次调用才初始化，实现了懒加载的特性。多线程场景下禁止使用，因为可能会产生多个对象，不再是单例。
>
>      ```java
>      public class Singleton {
>          private static Singleton singleton;
>          private Singleton(){}
>          public static Singleton getInstance(){
>              if (singleton == null) {
>                  singleton = new Singleton();
>              }
>              return singleton;
>          }
>      }
>      ```
>
>    * **懒汉式（线程安全）**获取实例的getInstance()方法上加了同步锁。保证了多线程场景下的单例。但是效率会有所折损。
>
>      ```java
>      public class Singleton {
>          private static Singleton singleton;
>          private Singleton(){}
>          public static synchronized Singleton getInstance(){
>              if (singleton == null) {
>                  singleton = new Singleton();
>              }
>              return singleton;
>          }
>      }
>      ```
>
>    * **双重校验锁（线程安全 效率高）**此种实现中不用每次需要获得锁，减少了获取锁和等待的事件。
>      注意volatile关键字的使用，保证了各线程对singleton静态实例域修改的可见性。
>
>      ```java
>      public class Singleton {
>      private static volatile Singleton singleton;
>          private Singleton(){}
>          public static Singleton getInstance(){
>              if (singleton == null) {
>                  synchronized (Singleton.class) {
>                      if (singleton == null){
>                          singleton = new Singleton();
>                      }
>                  }
>              }
>              return singleton;
>          }
>      }
>      ```
>
>    * **静态内部类实现单例（线程安全、效率高）**这种方式下 Singleton 类被装载了，instance 不一定被初始化。因为 SingletonHolder 类没有被主动使用，只有通过显式调用 getInstance 方法时，才会显式装载 SingletonHolder 类，从而实例化 instance。注意内部类SingletonHolder要用static修饰且其中的静态变量INSTANCE必须是final的。
>
>      ```java
>      public class Singleton {  
>          private static class SingletonHolder {  
>          private static final Singleton INSTANCE = new Singleton();  
>          }  
>          private Singleton (){}  
>          public static final Singleton getInstance() {  
>          return SingletonHolder.INSTANCE;  
>          }  
>      }
>      ```
>      
>    * **枚举类实现单例（利用枚举的特性来解决线程安全和单一实例的问题，还可以防止反射和反序列化对单例的破坏,最为推荐），**因为Java虚拟机会保证枚举对象的唯一性，因此每一个枚举类型和定义的枚举变量在JVM中都是唯一的，在实现过程中，**Java虚拟机会保证枚举类型不能被反射并且构造函数只被执行一次**。
>    
>      * 最简单的实现方式如下
>    
>      ```java
>      public enum Singleton {
>           INSTANCE;
>           public void businessMethod() {
>                System.out.println("我是一个单例！");
>           }
>      }
>      ///////////////////////////////////////////
>      public class MainClass {
>          public static void main(String[] args) {
>              Singleton s1 = Singleton.INSTANCE;
>              Singleton s2 = Singleton.INSTANCE;
>              System.out.println(s1==s2);
>          }
>      }
>      ```
>    
>      * 经典实现
>    
>      ```java
>      public class Singleton {
>          private Singleton(){
>          }   
>          public static enum SingletonEnum {
>              SINGLETON;
>              private Singleton instance = null;
>              private SingletonEnum(){
>                  instance = new Singleton();
>              }
>              public Singleton getInstance(){
>                  return instance;
>              }
>          }
>      }
>      ///////////////////////////////////////////////
>          ……	
>          public static void main(String args[]) {
>          	Singleton s1 = SingletonEnum.SINGLETON.getInstance();
>          	Singleton s2 = SingletonEnum.SINGLETON.getInstance();
>          	System.out.println(s1==s2);
>          }
>          ……
>      ```
>    
>      

#### 6.2 策略模式

> 1. 策略模式的优点
>
>    > ①、算法可以自由切换
>    >
>    > 这是策略模式本身定义的， 只要实现抽象策略， 它就成为策略家族的一个成员， 通过封装角色对其进行封装， 保证对外提供“可自由切换”的策略。
>    >
>    > ②、避免使用多重条件判断
>    >
>    > 简化多重if-else，或多个switch-case分支。
>    >
>    > ③、扩展性良好
>    >
>    > 增加一个策略，只需要实现一个接口即可。
>
> 2. 应用场景
>
>    > ①、多个类只有在算法或行为上稍有不同的场景。
>    >
>    > ②、算法需要自由切换的场景。
>    >
>    > ③、需要屏蔽算法规则的场景。
>
> 3. 代码实现
>
>    ```java
>    public class Context {
>        // 抽象策略
>        private Strategy strategy = null;
>        // 构造函数设置具体策略
>        public Context(Strategy strategy) {
>            this.strategy = strategy;
>        }
>        // 封装后的策略方法
>        public void doAnything(){
>            this.strategy.doSomething();
>        }
>    }
>    ```
>
>    ```java
>    public interface Strategy {
>        // 策略模式的运算法则
>        public void doSomething();
>    }
>    ```
>
>    ```java
>    public class ConcreteStrategy1 implements Strategy{
>        @Override
>        public void doSomething() {
>            System.out.println("ConcreteStrategy1");
>        }
>    }
>    ```
>
>    ```java
>    public class ConcreteStrategy2 implements Strategy{
>        @Override
>        public void doSomething() {
>            System.out.println("ConcreteStrategy2");
>        }
>    }
>    ```
>
>    测试：
>
>    ```java
>    public class StrategyClient {
>        public static void main(String[] args) {
>            // 声明一个具体的策略
>            Strategy strategy = new ConcreteStrategy1();
>            // 声明上下文对象
>            Context context = new Context(strategy);
>            // 执行封装后的方法
>            context.doAnything();
>        }
>    }
>    ```

#### 6.3 代理模式

> 代理模式是一种比较好理解的设计模式。简单来说就是 **我们使用代理对象来代替对真实对象(real object)的访问，这样就可以在不修改原目标对象的前提下，提供额外的功能操作，扩展目标对象的功能。**代理模式的主要作用是扩展目标对象的功能，比如说在目标对象的某个方法执行前后你可以增加一些自定义的操作。
>
> 代理模式有静态代理和动态代理两种实现方式。
>
> * 静态代理
>
>   > 静态代理中**，**我们对目标对象的每个方法的增强都是手动完成的,非常不灵活
>   >
>   > 静态代理实现步骤:
>   >
>   > 1. 定义一个接口及其实现类；
>   > 2. 创建一个代理类同样实现这个接口
>   > 3. 将目标对象注入进代理类，然后在代理类的对应方法调用目标类中的对应方法。这样的话，我们就可以通过代理类屏蔽对目标对象的访问，并且可以在目标方法执行前后做一些自己想做的事情。
>
> * 动态代理
>
>   > 相比于静态代理来说，动态代理更加灵活。我们不需要针对每个目标类都单独创建一个代理类，动态代理常见的有JDK动态代理，cglib动态代理。
>   >
>   > * **JDK 动态代理类使用步骤**
>   >
>   >   > 定义一个接口及其实现类；
>   >   >
>   >   > 自定义 `InvocationHandler` 并重写`invoke`方法，在 `invoke` 方法中我们会调用原生方法（被代理类的方法）并自定义一些处理逻辑；
>   >   >
>   >   > 通过 `Proxy.newProxyInstance(ClassLoader loader,Class<?>[] interfaces,InvocationHandler h)` 方法创建代理对象；
>   >
>   > * **cglib动态代理**
>   >
>   >   > **JDK 动态代理有一个最致命的问题是其只能代理实现了接口的类。**为了解决这个问题，我们可以用 CGLIB 动态代理机制来避免。 CGLIB 允许我们在运行时对字节码进行修改和动态生成。CGLIB 通过继承方式实现代理,**Spring 中的 AOP 模块中：如果目标对象实现了接口，则默认采用 JDK 动态代理，否则采用 CGLIB 动态代理。**
>   >   >
>   >   > ##### CGLIB 动态代理类使用步骤：
>   >   >
>   >   > > 定义一个类；
>   >   > >
>   >   > > 自定义 `MethodInterceptor` 并重写 `intercept` 方法，`intercept` 用于拦截增强被代理类的方法，和 JDK 动态代理中的 `invoke` 方法类似；
>   >   > >
>   >   > > 通过 `Enhancer` 类的 `create()`创建代理类

****



## 	7、jvm

/////////////////////////////

****



# 二、spring

## 1、 spring是什么？

> Spring是一个轻量级的，可以简化开发的Java开发框架，拥有IoC和AOP两大功能核心。通过IoC容器管理对象以及他们之间的耦合关系；通过AOP以动态非侵入的方式增强服务，IoC让相互协作的组件保持松散的耦合，而AOP编程允许你把遍布于应用各层的功能分离出来形成可重用的功能组件。
>
> 它的优点有：
>
> * 方便解耦，简化开发
> * aop编程的支持
> * 声明式事务的支持
> * 方便程序测试
> * 可以集成各种优秀的框架
> * 降低JAVAEE API的使用难度
>
> 缺点：
>
> * 配置复杂
> * Spring依赖反射，反射影响性能

## 2、Spring 框架中都用到了哪些设计模式？

> * 工厂模式：BeanFactory就是简单工厂模式的体现，用来创建对象的实例；
> * 单例模式：Bean默认为单例模式。
> * 代理模式：Spring的AOP功能用到了JDK的动态代理和CGLIB字节码生成技术；
> * 模板方法：用来解决代码重复的问题。比如. RestTemplate, JmsTemplate, JpaTemplate。
> * 观察者模式：定义对象键一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都会得到通知被制动更新，如Spring中listener的实现–ApplicationListener。

## 3、Spring 是如何简化开发的

> * 基于POJO的轻量级和最小侵入式编程
> * 通过依赖注入和面向接口实现松耦合
> * 基于切面和惯例进行声明式编程
> * 通过切面和模板减少样板式代码
>
> **主要还是通过IOC控制翻转和AOP切面编程简化开发**
>
> 

## 4 、IOC是什么？

> IOC是控制反转，DI是依赖注入，是实现IOC的方式，原来我们创建对象，给对象添加依赖都是手动完成的，现在都转交给了IOC容器来实现，用户操作变得非常简单。

## 5、Spring AOP是什么以及实现原理？

> AOP 即面向切面编程，简单地说就是将代码中重复的部分抽取出来，在需要执行的时候使用动态代理技术，在不修改[源码]()的基础上对方法进行增强。
>
> Spring AOP中的动态代理主要有两种方式，JDK动态代理和CGLIB动态代理：
>
> JDK动态代理只提供接口的代理，不支持类的代理。核心InvocationHandler接口和Proxy类，InvocationHandler 通过invoke()方法反射来调用目标类中的代码，动态地将横切逻辑和业务编织在一起；接着，Proxy利用 InvocationHandler动态创建一个符合某一接口的的实例, 生成目标类的代理对象。
> 如果代理类没有实现 InvocationHandler 接口，那么Spring AOP会选择使用CGLIB来动态代理目标类。CGLIB（Code Generation Library），是一个代码生成的类库，可以在运行时动态的生成指定类的一个子类对象，并覆盖其中特定方法并添加增强代码，从而实现AOP。CGLIB是通过继承的方式做的动态代理，因此如果某个类被标记为final，那么它是无法使用CGLIB做动态代理的。

## 6、Spring事务

> 先开启事务支持，@EnableTransactionManagement
>
> 使用@Transactional
>
> spring的事务是基于aop实现的
>
> spring事务的传播行为说的是，当多个事务同时存在的时候，spring如何处理这些事务的行为。
>
> ① PROPAGATION_REQUIRED：如果当前没有事务，就创建一个新事务，如果当前存在事务，就加入该事务，该设置是最常用的设置。
>
> ② PROPAGATION_SUPPORTS：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就以非事务执行。
>
> ③ PROPAGATION_MANDATORY：支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就抛出异常。
>
> ④ PROPAGATION_REQUIRES_NEW：创建新事务，无论当前存不存在事务，都创建新事务。
>
> ⑤ PROPAGATION_NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。
>
> ⑥ PROPAGATION_NEVER：以非事务方式执行，如果当前存在事务，则抛出异常。
>
> ⑦ PROPAGATION_NESTED：如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则按REQUIRED属性执行。
>
> * ####  说一下 spring 的事务隔离？
>
>   > spring 有五大隔离级别，默认值为 ISOLATION_DEFAULT（使用数据库的设置），其他四个隔离级别和数据库的隔离级别一致：
>   >
>   > ISOLATION_DEFAULT：用底层数据库的设置隔离级别，数据库设置的是什么我就用什么；
>   > ISOLATION_READ_UNCOMMITTED：未提交读，最低隔离级别、事务未提交前，就可被其他事务读取（会出现幻读、脏读、不可重复读）；
>   > ISOLATION_READ_COMMITTED：提交读，一个事务提交后才能被其他事务读取到（会造成幻读、不可重复读），SQL server 的默认级别；
>   > ISOLATION_REPEATABLE_READ：可重复读，保证多次读取同一个数据时，其值都和事务开始时候的内容是一致，禁止读取到别的事务未提交的数据（会造成幻读），MySQL 的默认级别；
>   > ISOLATION_SERIALIZABLE：序列化，代价最高最可靠的隔离级别，该隔离级别能防止脏读、不可重复读、幻读。
>   > 脏读 ：表示一个事务能够读取另一个事务中还未提交的数据。比如，某个事务尝试插入记录 A，此时该事务还未提交，然后另一个事务尝试读取到了记录 A。
>   >
>   > 不可重复读 ：是指在一个事务内，多次读同一数据。
>   >
>   > 幻读 ：指同一个事务内多次查询返回的结果集不一样。比如同一个事务 A 第一次查询时候有 n 条记录，但是第二次同等条件下查询却有 n+1 条记录，这就好像产生了幻觉。发生幻读的原因也是另外一个事务新增或者删除或者修改了第一个事务结果集里面的数据，同一个记录的数据内容被修改了，所有数据行的记录就变多或者变少了。

## 7、Spring bean的生命周期

> class ==》推断构造方法 ==》实例化（普通对象）==》依赖注入（先byType，再byName） ==》初始化前（@PostConstruct，@PreDestroy）==》初始化（InitialzingBean）afterPropertiesSet方法==》初始化后（AOP）==》若aop则会产生代理对象 ==》放入单例池map（为了实现单例bean的效果，多例bean无需放入单例池中，每次初始化后会直接生成新的对象）-->bean对象 --->使用完了后， DisposableBean接口的destroy()方法或自定义的destory方法进行销毁。

## 8、 使用@Autowired注解自动装配的过程是怎样的？

> 使用@Autowired注解来自动装配指定的bean。在使用@Autowired注解之前需要在Spring配置文件进行配置，<context:annotation-config />。
>
> 在启动spring IoC时，容器自动装载了一个AutowiredAnnotationBeanPostProcessor后置处理器，当容器扫描到@Autowied、@Resource或@Inject时，就会在IoC容器自动查找需要的bean，并装配给该对象的属性。在使用@Autowired时，首先在容器中查询对应类型的bean：
>
> 如果查询结果刚好为一个，就将该bean装配给@Autowired指定的数据；
> 如果查询的结果不止一个，那么@Autowired会根据名称来查找；
> 如果上述查找的结果为空，那么会抛出异常。解决方法时，使用required=false。

## 9、 解释Spring支持的几种bean的作用域

> Spring框架支持以下五种bean的作用域：
>
> singleton : bean在每个Spring ioc 容器中只有一个实例。
> prototype：一个bean的定义可以有多个实例。
> request：每次http请求都会创建一个bean，该作用域仅在基于web的Spring ApplicationContext情形下有效。
> session：在一个HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。
> global-session：在一个全局的HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。
> 注意： 缺省的Spring bean 的作用域是Singleton。使用 prototype 作用域需要慎重的思考，因为频繁创建和销毁 bean 会带来很大的性能开销。

## 10、Spring框架中的单例bean是线程安全的吗？

> 不是
>
> Spring中的bean，有状态的bean是不安全的，无状态的安全
>
> - 有状态就是有数据存储功能。
> - 无状态就是不会保存数据。

## 11、Spring如何处理线程并发问题？

> **在一般情况下，只有无状态的Bean才可以在多线程环境下共享，在Spring中，绝大部分Bean都可以声明为singleton作用域，因为Spring对一些Bean中非线程安全状态采用ThreadLocal进行处理，解决线程安全问题。ThreadLocal会为每一个线程提供一个独立的变量副本，从而隔离了多个线程对数据的访问冲突。**因为每一个线程都拥有自己的变量副本，从而也就没有必要对该变量进行同步了。ThreadLocal提供了线程安全的共享对象，在编写多线程代码时，可以**把不安全的变量封装进ThreadLocal**。

## 11 、@Autowired和@Resource之间的区别

> * @Autowired 是Spring提供的，@Resource是JDK提供的
> * @Autowired 先byType再byName @Resource 先byName再byType

## 12、@Qualifier 注解有什么作用

> 一般配合@Autowired使用消除歧义

## 13、循环依赖

> 创建A需要B，创建B又需要A，产生循环依赖。spring提供了三级缓存解决循环依赖。
>
> 第一级缓存：单例池  singletonObjects  保存创建完整的单例bean 
>
> 第二级缓存 				earlySingletonObjects 保存创建过程中出现了循环依赖还未创建完成就得给其他对象去用的单例bean
>
> 第三级缓存				singleFactories  打破循环
>
>  
>
> 创建一个bean对象A
>
> 0. creatingSet  记录下 A 正在创建
> 1. 实例化得到 A 的普通对象，生成一个lambda表达式（判断 A 是否需要生成代理对象）存到三级缓存singletonFactories里 
> 2. 开始填充 A 的属性 B，先去单例池找，没找到，开始创建 B
>    1. 创建过程中发现 B 需要属性 A ，去单例池找，没找到，然后发现 A 正在创建，这时候 B 知道这是产生循环依赖了，然后去二级缓存 earlySingletonObjects找，没找到，然后去三级缓存里找，找到了一开始 A 存进去的对象，返回一个 A 的普通对象或代理对象，之后会把这个对象放入到二级缓存中并删除三级缓存的lambda表达式 
>    2. 接下来就按正常流程创建 B ，创建完成放入到单例池中
> 3. B 的事情处理完了，A 的创建继续往下执行，然后从二级缓存earlySingletonObjects.get（beanName）放入到单例池中

## 14、单例Bean和单例模式的区别？

> 单例模式是指在一个jvm进程(运行的Java程序)中仅有一个实例。
>
> Spring的单例bean是指一个Spring Bean容器ApplicationContext中仅有一个实例。同时同一个容器中类型相同但是名称不同也会是不同实例。

****



# 三、spring mvc

## 1、什么是Spring MVC？简单介绍下你对Spring MVC的理解

> Spring MVC是一个基于Java的实现了[MVC设计模式](https://so.csdn.net/so/search?q=MVC设计模式&spm=1001.2101.3001.7020)的请求驱动类型的轻量级Web框架，通过把模型-视图-控制器分离，将web层进行职责解耦，把复杂的web应用分成逻辑清晰的几部分，简化开发，减少出错，方便组内开发人员之间的配合。

## 2、 Spring MVC的流程

> ![SpringMVC学习总结(七).SpringMVC运行流程与源码解析 - Java天堂](https://img.javatt.com/3d/3d7e973867258bf3d1e25c799dcb784e.png)
>
> （1）用户发送请求至前端控制器DispatcherServlet；
> （2） DispatcherServlet收到请求后，调用HandlerMapping处理器映射器，请求获取Handle；
> （3）处理器映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet；
> （4）DispatcherServlet 调用 HandlerAdapter处理器适配器；
> （5）HandlerAdapter 经过适配调用 具体处理器(Handler，也叫后端控制器)；
> （6）Handler执行完成返回ModelAndView；
> （7）HandlerAdapter将Handler执行结果ModelAndView返回给DispatcherServlet；
> （8）DispatcherServlet将ModelAndView传给ViewResolver视图解析器进行解析；
> （9）ViewResolver解析后返回具体View；
> （10）DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）
> （11）DispatcherServlet响应用户。

## 3、Spring MVC常用的注解有哪些？

> @RequestMapping：用于处理请求 url 映射的注解，可用于类或方法上。用于类上，则表示类中的所有响应请求的方法都是以该地址作为父路径。
>
> @RequestBody：注解实现接收http请求的json数据，将json转换为java对象。
>
> @ResponseBody：注解实现将conreoller方法返回对象转化为json对象响应给客户。

## 4、SpingMvc中的控制器的注解一般用哪个,有没有别的注解可以替代？

> 一般用@Controller注解,也可以使用@RestController,@RestController注解相当于@ResponseBody ＋ @Controller,表示是表现层,除此之外，一般不用别的注解代替。

****



# 四、spring boot

## 1、什么是Spring Boot及其优点？

> Spring Boot 是 Spring 开源组织下的子项目，是 Spring 组件一站式解决方案，主要是简化了使用 Spring 的难度，简省了繁重的配置，提供了各种启动器，开发者能快速上手。
>
> Spring Boot 主要有如下优点：
>
> 容易上手，提升开发效率，为 Spring 开发提供一个更快、更广泛的入门体验。
> 开箱即用，远离繁琐的配置。
> 提供了一系列大型项目通用的非业务性功能，例如：内嵌服务器、安全管理、运行数据监控、运行状况检查和外部化配置等。
> 没有代码生成，也不需要XML配置。
> 避免大量的 Maven 导入和各种版本冲突。

## 2、Spring Boot 的核心注解是哪个？它主要由哪几个注解组成的?

> 启动类上面的注解是@SpringBootApplication，它也是 Spring Boot 的核心注解，主要组合包含了以下 3 个注解：
>
> @SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。
>
> @EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })。
>
> @ComponentScan：Spring组件扫描。

## 3、Spring boot是如何做到简化配置的？(Spring Boot 自动配置原理是什么？)

> 主要是@EnableAutoConfiguration这个注解起的作用，这个注解是间接隐藏在springboot启动类注解@SpringbootApplication中。通过这个注解，SpringApplication.run（…）的内部就会执行selectImports()方法，去扫描每个jar包下的META-INF/xxxx.factories文件，这个文件是一个key-value形式的配置文件，里面存放了这个jar包具体依赖的自动配置类。这些自动配置类又通过@EnableAutoConfigurationProperties注解支持通过xxxxProperties读取application.properties/yml属性文件中我们配置的值。如果我们没有配置值就是用默认值，这就是所谓约定大于配置具体的落地点。

## 4、 Spring Boot 是否可以使用 XML 配置 ?

>  Spring Boot 中也可以使用 XML 配置，通过 @ImportResource 注解可以引入一个 XML 配置。

## 5、Spring Boot 中的 starter 到底是什么 ?

> **Starters可以理解为启动器，它包含了一系列可以集成到应用里面的依赖包，你可以一站式集成 Spring 及其他技术，而不需要到处找示例代码和依赖包。**
>
> 这个 Starter 并非什么新的技术点，基本上还是基于 Spring 已有功能来实现的。首先它提供了一个自动化配置类，一般命名为 XXXAutoConfiguration ，在这个配置类中通过条件注解来决定一个配置是否生效（条件注解就是 Spring 中原本就有的），然后它还会提供一系列的默认配置，也允许开发者根据实际情况自定义相关配置，然后通过类型安全的属性注入将这些配置属性注入进来，新注入的属性会代替掉默认属性。正因为如此，很多第三方框架，我们只需要引入依赖就可以直接使用了。

## 6、Spring Boot 打成的 jar 和普通的 jar 有什么区别 ?

> Spring Boot 的 jar 无法被其他项目依赖，主要还是他和普通 jar 的结构不同。普通的 jar 包，解压后直接就是包名，包里就是我们的代码，而 Spring Boot 打包成的可执行 jar 解压后，在 \BOOT-INF\classes 目录下才是我们的代码，因此无法被直接引用。如果非要引用，可以在 pom.xml 文件中增加配置，将 Spring Boot 项目打包成两个 jar ，一个可执行，一个可引用。

## 7、运行 Spring Boot 有哪几种方式？

> 1）打包用命令或者放到容器中运行
> 2）用 Maven/ Gradle 插件运行
> 3）直接执行 main 方法运行

## 8、如何替换内置服务器？

> ```java
> 
>     <!-- 使用jetty服务器-->
>     <dependency>
>     	<groupId>org.springframework.boot</groupId>
>    	 	<artifactId>spring-boot-starter-web</artifactId>
>     	<exclusions>
>       		<exclusion>
>         		<groupId>org.springframework.boot</groupId>
>         		<artifactId>spring-boot-starter-tomcat</artifactId>
>       		</exclusion>
>     	</exclusions>
>   	</dependency>
>   	<dependency>
>     	<groupId>org.springframework.boot</groupId>
>     	<artifactId>spring-boot-starter-jetty</artifactId>
>     </dependency>    
> ```

## 9、Spring Boot 中如何实现定时任务 ?

> 在 Spring Boot 中使用定时任务主要有两种不同的方式，一个就是使用 Spring 中的 @Scheduled 注解，另一个则是使用第三方框架 Quartz。
>
> 使用 Spring 中的 @Scheduled 的方式主要通过 @Scheduled 注解来实现。
>
> 使用 Quartz ，则按照 Quartz 的方式，定义 Job 和 Trigger 即可。

## 10、**springboot读取配置文件的方式**

> springboot默认读取配置文件为application.properties或者是application.yml

****



# 五、Mybatis

## 1、MyBatis是什么？

>  MyBatis 是一款优秀的持久层框架，一个半 ORM（对象关系映射）框架，它支持定制化 SQL、存储过程以及高级映射。
>
> ORM：对象关系映射，是一种为了解决关系型数据库数据与简单Java对象（POJO）的映射关系的技术。简单的说，ORM是通过使用描述对象和数据库之间映射的元数据，将程序中的对象自动持久化到关系型数据库中。

## 2、#{}和${}的区别？

> {}是占位符，预编译处理；${}是拼接符，字符串替换，没有预编译处理。
>
> Mybatis在处理#{}时，#{}传入参数是以字符串传入，会将SQL中的#{}替换为?号，调用PreparedStatement的set方法来赋值。
>
> Mybatis在处理时 ， 是 原 值 传 入 ， 就 是 把 {}时，是原值传入，就是把时，是原值传入，就是把{}替换成变量的值，相当于JDBC中的Statement编译
>
> 变量替换后，#{} 对应的变量自动加上单引号 ‘’；变量替换后，${} 对应的变量不会加上单引号 ‘’
>
> #{} 可以有效的防止SQL注入，提高系统安全性；${} 不能防止SQL 注入
>
> #{} 的变量替换是在DBMS 中；${} 的变量替换是在 DBMS 外

## 3、在mapper中如何传递多个参数

> 方法1：顺序传参法
>
> ```java
> public User selectUser(String name, int deptId);
> <select id="selectUser" resultMap="UserResultMap">
>     select * from user
>     where user_name = #{0} and dept_id = #{1}
> </select>
> ```
>
> #{}里面的数字代表传入参数的顺序。
> 这种方法不建议使用，sql层表达不直观，且一旦顺序调整容易出错。
>
> 方法2：@Param注解传参法
>
> ```java
> public User selectUser(@Param("userName") String name, int @Param("deptId") deptId);
> <select id="selectUser" resultMap="UserResultMap">
>     select * from user
>     where user_name = #{userName} and dept_id = #{deptId}
> </select> 
> ```
>
> #{}里面的名称对应的是注解@Param括号里面修饰的名称。
> 这种方法在参数不多的情况还是比较直观的，推荐使用。
>
> 方法3：Map传参法
>
> ```java
> public User selectUser(Map<String, Object> paramsMap);
> <select id="selectUser" parameterType="java.util.Map" resultMap="UserResultMap">
>     select * from user
>     where user_name = #{userName} and dept_id = #{deptId}
> </select>
> ```
>
> #{}里面的名称对应的是Map里面的key名称。
> 这种方法适合传递多个参数，且参数易变能灵活传递的情况。
>
> 方法4：Java Bean传参法
>
> ```java
> public User selectUser(User user);
> <select id="selectUser" parameterType="com.jourwon.pojo.User" resultMap="UserResultMap">
>     select * from user
>     where user_name = #{userName} and dept_id = #{deptId}
> </select>
> ```
>
> #{}里面的名称对应的是User类里面的成员属性。
> 这种方法直观，需要建一个实体类，扩展不容易，需要加属性，但代码可读性强，业务逻辑处理方便，推荐使用。

## 4、 Mybatis如何执行批量操作

> **使用foreach标签**
>
> foreach标签的属性主要有`collection，item，index，open，separator，close`

## 5、如何获取生成的主键

> **对于支持主键自增的数据库（MySQL）**
>
> ```java
> <insert id="insertUser" useGeneratedKeys="true" keyProperty="userId" >
>     insert into user( 
>     user_name, user_password, create_time) 
>     values(#{userName}, #{userPassword} , #{createTime, jdbcType= TIMESTAMP})
> </insert>
> ```
>
> **不支持主键自增的数据库（Oracle）**
>
> 对于像Oracle这样的数据，没有提供主键自增的功能，而是使用序列的方式获取自增主键。
> 可以使用＜selectKey＞标签来获取主键的值，这种方式不仅适用于不提供主键自增功能的数据库，也适用于提供主键自增功能的数据库
> ＜selectKey＞一般的用法
>
> ```java
> <selectKey keyColumn="id" resultType="long" keyProperty="id" order="BEFORE">
> </selectKey>
> ```

## 6、当实体类中的属性名和表中的字段名不一样 ，怎么办

> * 给查询字段起别名
> * 建立resultMap映射

## 7、Mybatis动态sql是做什么的？都有哪些动态sql？能简述一下动态sql的执行原理不？

> Mybatis动态sql可以让我们在Xml映射文件内，以标签的形式编写动态sql，完成逻辑判断和动态拼接sql的功能，Mybatis提供了9种动态sql标签trim|where|set|foreach|if|choose|when|otherwise|bind。
>
> 其执行原理为，使用OGNL从sql参数对象中计算表达式的值，根据表达式的值动态拼接sql，以此来完成动态sql的功能。

## 8、Mybatis的一级、二级缓存

> 1）一级缓存: 基于 PerpetualCache 的 HashMap 本地缓存，其存储作用域为 Session，当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认打开一级缓存。
>
> 2）二级缓存与一级缓存其机制相同，默认也是采用 PerpetualCache，HashMap 存储，不同在于其存储作用域为 Mapper(Namespace)，并且可自定义存储源，如 Ehcache。默认不打开二级缓存，要开启二级缓存，使用二级缓存属性类需要实现Serializable序列化接口(可用来保存对象的状态),可在它的映射文件中配置 ；
>
> 3）对于缓存数据更新机制，当某一个作用域(一级缓存 Session/二级缓存Namespaces)的进行了C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear。

## 9、MyBatis实现一对一，一对多有几种方式，怎么操作的？

> 有联合查询和嵌套查询。联合查询是几个表联合查询，只查询一次，通过在resultMap里面的association，collection节点配置一对一，一对多的类就可以完成
>
> 嵌套查询是先查一个表，根据这个表里面的结果的外键id，去再另外一个表里面查询数据，也是通过配置association，collection，但另外一个表的查询通过select节点配置。

## 10、Mybatis映射文件中，如果A标签通过include引用了B标签的内容，请问，B标签能否定义在A标签的后面，还是说必须定义在A标签的前面？

> 虽然Mybatis解析Xml映射文件是按照顺序解析的，但是，被引用的B标签依然可以定义在任何地方，Mybatis都可以正确识别。
>
> 原理是，Mybatis解析A标签，发现A标签引用了B标签，但是B标签尚未解析到，尚不存在，此时，Mybatis会将A标签标记为未解析状态，然后继续解析余下的标签，包含B标签，**待所有标签解析完毕，Mybatis会重新解析那些被标记为未解析的标签**，此时再解析A标签时，B标签已经存在，A标签也就可以正常解析完成了。

## 11、Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？

> 不同的Xml映射文件，如果配置了namespace，那么id可以重复；如果没有配置namespace，那么id不能重复；毕竟namespace不是必须的，只是最佳实践而已。
>
> 原因就是namespace+id是作为Map<String, MappedStatement>的key使用的，如果没有namespace，就剩下id，那么，id重复会导致数据互相覆盖。有了namespace，自然id就可以重复，namespace不同，namespace+id自然也就不同。

## 12、最佳实践中，通常一个Xml映射文件，都会写一个Dao接口与之对应，请问，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗

> Dao接口，就是人们常说的Mapper接口，接口的全限名，就是映射文件中的namespace的值，接口的方法名，就是映射文件中MappedStatement的id值，接口方法内的参数，就是传递给sql的参数。Mapper接口是没有实现类的，当调用接口方法时，接口全限名+方法名拼接字符串作为key值，可唯一定位一个MappedStatement，举例：
>
> com.mybatis3.mappers.StudentDao.findStudentById，可以唯一找到namespac e为com.mybatis3.mappers.StudentDao下面id = findStudentById的MappedStatement。在Mybatis中，每一个、、、标签，都会被解析为一个MappedStatement对象。
>
> **Dao接口里的方法，是不能重载的，因为是全限名+方法名的保存和寻找策略。**
>
> **Dao接口的工作原理是JDK动态代理，Mybatis运行时会使用JDK动态代理为Dao接口生成代理proxy对象，代理对象proxy会拦截接口方法，转而执行MappedStatement所代表的sql，然后将sql执行结果返回。**

****



# 六、数据库相关

## 1、什么是SQL？

> 结构化查询语言，是一种数据库查询语言

## 2、数据库中的三大范式

> **第一范式**：每个列都不可以再拆分。
>
> **第二范式**：在第一范式的基础上，非主键列完全依赖于主键，而不能是依赖于主键的一部分。
>
> **第三范式**：在第二范式的基础上，非主键列只依赖于主键，不依赖于其他非主键。

## 3、 mysql有哪些数据类型

> * 整数类型：包括TINYINT、SMALLINT、MEDIUMINT、INT、BIGINT，分别表示1字节、2字节、3字节、4字节、8字节整数。
> * 实数类型：包括FLOAT、DOUBLE、DECIMAL。
> * 字符串类型：CHAR、VARCHAR、TEXT、BLOB
> * 日期和时间类型: DATETIME、timestamp、date

## 4、索引

#### 4.1 什么是索引？

> 索引是对数据库表的一列或者多列的值进行排序的一种数据结构，使用索引可以快速访问数据表中的特定信息
>
> ###### 索引的优缺点
>
> > **优点**
> >
> > - 提高数据检索的效率，降低数据库IO成本。
> > - 通过索引对数据进行排序，降低数据的排序成本，降低CPU的消耗。
> >
> > **缺点**
> >
> > - 建立索引需要**占用物理空间**
> > - 会降低表的增删改的效率，因为每次对表记录进行增删改，需要进行**动态维护索引**，导致增删改时间变长
>
> ###### 索引主要分哪几种类？
>
> > MySQL主要的几种索引类型：1.普通索引 2.[唯一索引](https://so.csdn.net/so/search?q=唯一索引&spm=1001.2101.3001.7020) 3.主键索引 4.组合索引 5.全文索引。
> >
> > * 普通索引: 是最基本的索引，它没有任何限制
> > * 唯一索引: 索引列的值必须唯一，但允许有空值。如果是组合索引，则列值的组合必须唯一
> > * 主键索引: 是一种特殊的唯一索引，一个表只能有一个主键，不允许有空值。
> > * 组合索引: 一个索引包含多个列，实际开发中推荐使用组合索引。
> > * 全文索引: 全文搜索的索引。FULLTEXT 用于搜索很长一篇文章的时候，效果最好。只能用于InnoDB或MyISAM表，只能为CHAR、VARCHAR、TEXT列创建。

#### 4.2 索引的数据结构

> 索引的数据结构主要有**B+树**和**哈希表**，对应的索引分别为B+树索引和Hash索引。
>
> * 哈希索引
>
>   > 哈希索引是基于哈希表实现的，当我们要给某张表某列增加索引时，存储引擎会对这列进行哈希计算得到哈希码，将哈希码的值作为哈希表的key值，将指向数据行的指针作为哈希表的value值。这样查找一个数据的时间复杂度就是O(1)，一般多用于精确查找。所以在= in <=>(安全等于的时候）的效率是非常高的，但我们开发一般会选择Btree，因为Hash会存在如下一些缺点。
>   >
>   > 1. Hash索引仅仅能满足"=",“IN"和”<=>"查询，不能使用范围查询。
>   > 2. Hash 索引无法被用来避免数据的排序操作。
>   > 3. Hash索引不能利用部分索引键查询。
>   > 4. Hash索引在任何时候都不能避免表扫描。
>   > 5. Hash索引遇到大量Hash值相等的情况后性能并不一定就会比B-Tree索引高。
>
> * B+树索引
>
>   > 使用B+树索引的好处在于操作过程中极大的减少了磁盘I/O的次数，提高了效率，
>   >
>   > 因为B+树 
>   >
>   > 1. **非叶子节点只存储键值信息**。
>   > 2. **所有叶子节点之间都有一个链指针**。
>   > 3. **数据记录都存放在叶子节点中**。
>   >
>   > **Q：B+树一个非叶子节点能放多少指针，一个B+树可能放多少数据？**
>   > InnoDB中聚簇索引的B+树的一个节点被设计成一页，一页大小在InnoDB中默认为16k，当然也可以通过参数设置。
>   > 假设主键索引类型为bigint则为8字节，指针在InnoDB中为6字节，一共14字节。因为非叶子节点中一个key值就会
>   > 对应一个指针即N个key+N指针，这样算下来则16k能存放 16 * 1024 / 14 = 1170个索引指针。
>   >
>   > 假设一条数据大小为1k，那么一个叶子节点就可以存储16条数据，对于一个高度为2的B+树则会有1170个叶子节点
>   > 每个叶子节点可以存储16条数据，一共 1170 x 16 = 18720 条数据。对于一个高度为3的B+树就可以存放1170 x 1170 x 16 = 21902400条数据
>   > InnoDB 中B+树高度一般为3层时，就能满足千万级的数据存储，所以一个节点为1页，也就是16k是比较合理的。

#### 4.3 聚集索引相对于非聚集索引的区别？

> - 聚簇索引：将数据存储与索引放到了一块，找到索引也就找到了数据
>
>   非聚簇索引：将数据存储于索引分开结构，索引结构的叶子节点指向了数据的对应行，myisam通过key_buffer把索引先缓存到内存中，当需要访问数据时（通过索引访问数据），在内存中直接搜索索引，然后通过索引找到磁盘相应数据，这也就是为什么索引不在key buffer命中时，速度慢的原因
>   
>
> * 聚簇索引
>
>   > 聚簇索引就是按照每张表的主键构造一颗B+树，同时叶子节点中存放的就是整张表的行记录数据，也将聚集索引的叶子节点称为数据页。这个特性决定了索引组织表中数据也是索引的一部分，每张表只能拥有一个聚簇索引。
>   >
>   > 如果表设置了主键，则主键就是聚簇索引
>   > 如果表没有主键，则会默认第一个NOT NULL，且唯一（UNIQUE）的列作为聚簇索引
>   > 以上都没有，则会默认创建一个隐藏的row_id作为聚簇索引
>   > 聚集索引的叶子节点就是整张表的行记录。InnoDB 主键使用的是聚簇索引。聚集索引要比非聚集索引查询效率高很多。
>
> * 非聚簇索引
>
>   >  就是普通索引（也叫二级索引）

#### 4.4 什么是回表查询？

> 非聚簇索引查询就是回表查询。先通过普通索引的值定位聚簇索引值，再通过聚簇索引的值定位行记录数据，需要扫描两次索引B+树，它的性能较扫一遍索引树更低。

#### 4.5 什么是索引覆盖？

> 只需要在一棵索引树上就能获取SQL所需的所有列数据，无需回表，速度更快。

#### 4.6 什么是最左匹配原则？

> 如果我们创建了(age, name)的组合索引，那么其实相当于创建了(age)、(age, name)两个索引，这被称为最佳左前缀特性。因此我们在创建组合索引时应该将最常用作限制条件的列放在最左边，依次递减。
>
> **最左前缀匹配原则：在MySQL建立联合索引时会遵守最左前缀匹配原则，即最左优先，在检索数据时从联合索引的最左边开始匹配。**
>
> 这是为什么呢？
>
> 我们这里以组合索引(age, name)来画一下索引树就明白了。
>
>
> 我们再仔细观察索引结构，可以看到索引key在排序上，首先按age排序，age相等的节点中，再按name排序。因此，如果查询条件是age或age和name联查时，是可以应用到索引的。如果查询条件是单独使用name，因为无法确定age的值，因此无法使用索引。
>
> 如果当我们创建好组合索引(age, name)，那么下面的sql还需要回表查询吗？
>
> select id,age,name from user where age = 30;
>
> 答案是否定的，因为id,age,name字段，在这个索引树上已经都有了，我们也不需要拿着id的值再去聚簇索引定位行记录数据了。
>
> 所以在实际开发中如果你创建了(age, name)的组合索引，那就根本无需再去单独创建age的索引。同时也建议创建组合索引，只是在创建的时候需要考虑将最常用字段的列放在最左边，依次递减

#### 4.7 索引失效场景有哪些？

> * **组合索引未使用最左前缀**，例如组合索引（age，name），where name='张三’不会使用索引;
> * **or会使索引失效。**如果查询字段相同，也可以使用索引。例如where age=20 or age=30（索引生效），where age=20 or name=‘张三’（这里就算你age和name都单独建索引，还是一样失效）;
> * **如果列类型是字符串，不使用引号**。例如where name=张三(索引失效），改成where name=‘张三’(索引有效);
> * **like查询以%开头**，where A like ‘%China’;
> * **在索引列上做任何操作计算、函数，会导致索引失效而转向全表扫描;**
> * **如果mysql估计使用全表扫描要比使用索引快,则不使用索引**;
> * **使用 <>、NOT、in、not exists**
> * **当查询条件存在隐式转换时，索引会失效**

#### 4.8 索引的设计原则

> 索引列的区分度越高，索引的效果越好。比如使用性别这种区分度很低的列作为索引，效果就会很差。
> 尽量使用短索引，对于较长的字符串进行索引时应该指定一个较短的前缀长度，因为较小的索引涉及到的磁盘I/O较少，查询速度更快。
> 索引不是越多越好，每个索引都需要额外的物理空间，维护也需要花费时间。
> 利用最左前缀原则。

#### 4.9  创建索引的三种方式，删除索引

> 第一种方式：在执行CREATE TABLE时创建索引
>
> 第二种方式：使用ALTER TABLE命令去增加索引
>
> ```mysql
> ALTER TABLE table_name ADD INDEX index_name (column_list);
> ```
>
> 第三种方式：使用CREATE INDEX命令创建
>
> ```mysql
> CREATE INDEX index_name ON table_name (column_list);
> ```
>
> **删除索引**
>
> alter table 表名 drop KEY 索引名

#### 4.10  非聚簇索引一定会回表查询吗？

> 不一定，这涉及到查询语句所要求的字段是否全部命中了索引，如果全部命中了索引，那么就不必再进行回表查询。
>
> 举个简单的例子，假设我们在员工表的年龄上建立了索引，那么当进行select age from employee where age < 20的查询时，在索引的叶子节点上，已经包含了age信息，不会再次进行回表查询。

## 5、清空表数据

> 1.delete------ 是逐行删除速度极慢，不适合大量数据删除。
>
> 2.truncate---- 删除所有数据，保留表结构，不能撤消还原。
>
> 3.drop-------- 删除表，数据和表结构一起删除，快速。

## 6、事物的四大特性(ACID)介绍一下?

> * 原子性： 事务是最小的执行单位，不允许分割。事务的原子性确保动作要么全部完成，要么完全不起作用；
> * 一致性： 执行事务前后，数据保持一致，多个事务对同一个数据读取的结果是相同的；
> * 隔离性： 并发访问数据库时，一个用户的事务不被其他事务所干扰，各并发事务之间数据库是独立的；
> * 持久性： 一个事务被提交之后。它对数据库中数据的改变是持久的，即使数据库发生故障也不应该对其有任何影响

## 7、 什么是脏读？幻读？不可重复读？

> * 脏读(Drity Read)：某个事务已更新一份数据，另一个事务在此时读取了同一份数据，由于某些原因，前一个RollBack了操作，则后一个事务所读取的数据就会是不正确的。
> * 不可重复读(Non-repeatable read):在一个事务的两次查询之中数据不一致，这可能是两次查询过程中间插入了一个事务更新的原有的数据。
> * 幻读(Phantom Read):在一个事务的两次查询中数据笔数不一致，例如有一个事务查询了几列(Row)数据，而另一个事务却在此时插入了新的几列数据，先前的事务在接下来的查询中，就会发现有几列数据是它先前所没有的。

## 8、什么是事务的隔离级别？MySQL的默认隔离级别是什么？

> 为了达到事务的四大特性，数据库定义了4种不同的事务隔离级别，由低到高依次为Read uncommitted、Read committed、Repeatable read、Serializable，这四个级别可以逐个解决脏读、不可重复读、幻读这几类问题。

## 9、按照锁的粒度分数据库锁有哪些？锁机制与InnoDB锁算法

> 在关系型数据库中，可以按照锁的粒度把数据库锁分为行级锁(INNODB引擎)、表级锁(MYISAM引擎)和页级锁(BDB引擎 )。
> MyISAM和InnoDB存储引擎使用的锁：
>
> MyISAM采用表级锁(table-level locking)。
> InnoDB支持行级锁(row-level locking)和表级锁，默认为行级锁
> 行级锁，表级锁和页级锁对比
>
> 行级锁 行级锁是Mysql中锁定粒度最细的一种锁，表示只针对当前操作的行进行加锁。行级锁能大大减少数据库操作的冲突。其加锁粒度最小，但加锁的开销也最大。行级锁分为共享锁 和 排他锁。
>
> 特点：开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低，并发度也最高。
>
> 表级锁 表级锁是MySQL中锁定粒度最大的一种锁，表示对当前操作的整张表加锁，它实现简单，资源消耗较少，被大部分MySQL引擎支持。最常使用的MYISAM与INNODB都支持表级锁定。表级锁定分为表共享读锁（共享锁）与表独占写锁（排他锁）。
> 特点：开销小，加锁快；不会出现死锁；锁定粒度大，发出锁冲突的概率最高，并发度最低。
>
> 页级锁 页级锁是MySQL中锁定粒度介于行级锁和表级锁中间的一种锁。表级锁速度快，但冲突多，行级冲突少，但速度慢。所以取了折衷的页级，一次锁定相邻的一组记录。
>
> 特点：开销和加锁时间界于表锁和行锁之间；会出现死锁；锁定粒度界于表锁和行锁之间，并发度一般

## 10、什么是存储过程？有哪些优缺点？

> 存储过程是一个预编译的SQL语句，优点是允许模块化的设计，就是说只需要创建一次，以后在该程序中就可以调用多次。如果某次操作需要执行多次SQL，使用存储过程比单纯SQL语句执行要快。
>
> * 好处
>   * 存储过程是预编译过的，执行效率高。
>   * 存储过程的代码直接存放于数据库中，通过存储过程名直接调用，减少网络通讯。
>   * 安全性高，执行存储过程需要有一定权限的用户。
>   * 存储过程可以重复使用，减少数据库开发人员的工作量。
> * 坏处
>   * 调试麻烦，但是用 PL/SQL Developer 调试很方便！弥补这个缺点。
>   * 移植困难
>   * 重新编译问题，因为后端代码是运行前编译的，如果带有引用关系的对象发生改变时，受影响的存储过程、包将需要重新编译（不过也可以设置成运行时刻自动编译）。
>   * 维护困难

## 11、Mysql 中 MyISAM 和 InnoDB 的区别有哪些？

> 1. InnoDB 支持事务，MyISAM 不支持事务。这是 MySQL 将默认存储引擎从 MyISAM 变成 InnoDB 的重要原因之一；
> 2. InnoDB 支持外键，而 MyISAM 不支持。.
> 3. InnoDB 是聚集索引，MyISAM 是非聚集索引。
> 4. InnoDB 最小的锁粒度是行锁，MyISAM 最小的锁粒度是表锁。
> 5. InnoDB不保存表的具体行数，执行select count(*) from table时需要全表扫描。而MyISAM用一个变量保存了整个表的行数，
> 6. InnoDB表必须有唯一索引（如主键）（用户没有指定的话会自己找/生产一个隐藏列Row_id来充当默认主键），而Myisam可以没有

## 12、MySQL 的存储引擎

| 存储引擎  | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| ARCHIVE   | 用于数据存档的引擎，数据被插入后就不能在修改了，且不支持索引。 |
| CSV       | 在存储数据时，会以逗号作为数据项之间的分隔符。               |
| BLACKHOLE | 会丢弃写操作，该操作会返回空内容。                           |
| FEDERATED | 将数据存储在远程数据库中，用来访问远程表的存储引擎。         |
| InnoDB    | 具备外键支持功能的事务处理引擎                               |
| MEMORY    | 置于内存的表                                                 |
| MERGE     | 用来管理由多个 MyISAM 表构成的表集合                         |
| MyISAM    | 主要的非事务处理存储引擎                                     |
| NDB       | MySQL 集群专用存储引擎                                       |

## 13、mysql和Oracle分页操作

> oracle 使用嵌套子查询配合rownum 进行分页查询，mysql使用limit进行分页查询，
>
> db2也没有limit，借助 row_num(） 给我们的表 生成序号，再通过 where 对行号进行区间判断。
>
> ```mysql
> select * from ( select row_num() over() as rownum, a.name, a.age ,b.id  from user a left join work b on a.id=b.id ) where rownum>20 and rownum<30
> ```

## 14、merge into语句

> ```mysql
> merge into 目标表 a
>  
> using 源表 b
>  
> on(a.条件字段1=b.条件字段1 and a.条件字段2=b.条件字段2 ……)  
>  
> when matched then update set a.字段=b.字段 --目标表别称a和源表别称b都不要省略
>  
> when  not matched then insert (a.字段1,a.字段2……)values(b.字段1,b.字段2……) --目标表别称a可省略,源表别称b不可省略
> ```

## 15、sql优化

> * 避免全表扫描的操作
> * 不使用select *
> * 尽量不要出现索引失效的情况 如上面  **4.7 索引失效场景有哪些？**

## 16、sql执行计划

> ##### MySQL 执行计划
>
> > MySQL 中获取执行计划的方法很简单，就是在 SQL 语句的前面加上EXPLAIN关键字：
>
> #### Oracle 执行计划
>
> > 使用EXPLAIN PLAN FOR 命令生成并保存执行计划；
> >
> > 查看执行计划select * from table (dbms_xplan.display)
>
> 查看执行时间和执行效率（查看访问类型一般要达到range级别，使用索引查找）

# 七、Redis

# 八、MQ

# 九、微服务相关





​							

> 











