



# 集合



**java集合主要由2个体系组成。分别是Collection体系和Map体系，其中Collection和Map是两大体系的顶层接口。**

- Collection主要由三个子接口，分别是List(列表)、Set（集）、Queue( 队列)。其中，list、queue中的元素是有序并且重复的，而set中的元素是无需不可重复的。
- Map同属于java.util包中，是集合的一部分，但与Collection是相互独立的，没有任何关系。Map中都是以key-value的形式存在，其中key必须唯一，主要有HashMap、HashTable、TreeMap三个实现类

下面是结构图

![](/Users/awakeyoyoyo/Desktop/Java_Development_Note/images/WechatIMG1262.jpeg)

![这里写图片描述](https://img-blog.csdn.net/20180612094225630?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW5ncXVuc2h1YWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)







## **集合框架体系的组成**

集合框架体系是由Collection、Map(映射关系)和Iterator(迭代器)组成，各部分的作用如下所示。

### **[1]Collection体系中有三种集合：Set、List、Queue**

 Set(集)： 元素是无序的且不可重复。

 List(列表)：元素是有序的且可重复。

 Queue(队列)：封装了数据结构中的队列。

### **[2]Map体系**

 Map用于保存具有映射关系的数据，即key-value(键值对)。Map集合的key是唯一的，不可重复，而value可以重复。所以一个value可以对应多个key。

 Map体系除了常用类之外，还有Properties（属性类）也属于Map体系。

## **[3]Collection的由来**

 由于数组中存放对象，对对象操作起来不方便。java中有一类容器，专门用来存储对象。

 集合可以存储多个元素,但我们对多个元素也有不同的需求

 多个元素,不能有相同的

 多个元素,能够按照某个规则排序

 针对不同的需求：java就提供了很多集合类，多个集合类的数据结构不同。但是，结构不重要，重要  的是能够存储东西,能够判断,获取.

把集合共性的内容不断往上提取,最终形成集合的继承体系---->Collection

并且所有的Collection实现类都重写了toString()方法.

## **(4)集合和数组**

集合与数组的区别：

1.数组的长度固定的，而集合长度时可变的

2.数组只能储存同一类型的元素，而且能存基本数据类型和引用数据类型。集合可以存储不同类型的元素，只能存储引用数据类型

集合类和数组不一样,数组元素既可以是基本类型的值,也可以是对象(实际上保存的是对象的引用变量);而集合只能保存对象。

**数组和集合的主要区别包括以下几个方面：**

一：数组声明了它容纳的元素的类型，而集合不声明。这是由于集合以object形式来存储它们的元素。

二：一个数组实例具有固定的大小，不能伸缩。集合则可根据需要动态改变大小。

三：数组是一种可读/可写数据结构没有办法创建一个只读数组。然而可以使用集合提供的ReadOnly方  只读方式来使用集合。该方法将返回一个集合的只读版本。

## **(5)泛型**

本质就是在编译阶段就告诉编译器，数据结构中元素的种类，既然编译器知道了元素的种类，自然就避免了拆箱、封箱的操作，从而显著提高java程序的性能。 

比如List<string>就直接使用string对象作为List的元素，而避免使用object对象带来的封箱、拆箱操作，从而提高程序性能。

# **集合接口与类**

## **(1)数组和集合一般就用到下面接口和集合**

Array  数组

Arrays  数组工具

**Collection** 最基本的集合接口

**Collections  集合工具类**

List  接口

ArrayList 一种可以动态增长和缩减的索引序列

LinkedList 一种可以在任何位置进行高效地插入和删除操作的有序序列

**Vector**   一种可以动态增长和缩减的索引序列,Vector中的操作是线程安全的。

Set

HashSet 一种没有重复元素的无序集合

TreeSet 一种有序集

LinkHashSet 一种可以记住元素插入次序的集合

map

HashMap 一种存储key：value关联的映射

HashTable 线程安全

TreeMap 一种key有序的映射

LinkedHashMap 一种可以记住插入次序的映射

Deque 双端队列

Stack

ArrayDeque 一种用循环数组实现的双端队列

Queue	

PriorityQueue 一种可以高效删除最小元素的集合

## **3)Arrays**

数组的工具类,里面都是操作数组的工具.

常用方法:

1、数组的排序:Arrays.sort(a);//实现了对数组从小到大的排序//注：此类中只有升序排序，而无降序排序。

2、数组元素的定位查找:Arrays.binarySearch(a,8);//二分查找法

3、数组的打印:Arrays.toString(a);//String 前的a和括号中的a均表示数组名称

4、 查看数组中是否有特定的值:Arrays.asList(a).contains(1);

## **(4)Collection**

Collection是最基本的集合接口，一个Collection代表一组Object，即Collection的元素（Elements）。一些 Collection允许相同的元素而另一些不行。一些能排序而另一些不行。Java SDK不提供直接继承自Collection的类， Java SDK提供的类都是继承自Collection的“子接口”如List和Set。

所有实现Collection接口的类都必须提供两个标准的构造函数：无参数的构造函数用于创建一个空的Collection，有一个Collection参数的构造函数用于创建一个新的 Collection，这个新的Collection与传入的Collection有相同的元素。后一个构造函数允许用户复制一个Collection。

如何遍历Collection中的每一个元素？不论Collection的实际类型如何，它都支持一个iterator()的方法，该方法返回一个迭代子，使用该迭代子即可逐一访问Collection中每一个元素。典型的用法如下：

　　　　Iterator it = collection.iterator(); // 获得一个迭代子

　　　　while(it.hasNext()) {

　　　　Object obj = it.next(); // 得到下一个元素

由Collection接口派生的两个接口是List和Set。

Collection返回的是Iterator迭代器接口，而List中又有它自己对应的实现-->**ListIterator接口** Collection。标识所含元素的序列，这里面又包含多种集合类，比如List，Set，Queue；它们都有各自的特点，比如List是按顺序插入元素，Set是不重复元素集合，Queue则是典型的FIFO结构

Collection接口描述：

　　Collection接口常用的子接口有List 接口和Set接口

　　List接口中常用的子类有：ArrayList类（数组列表）和LinkedList（链表）

　　Set接口中常用的子类有：HashSet （哈希表）和LinkedHashSet（基于链表的哈希表）

***Collection\*** *层次结构* 中的根接口。Collection 表示一组对象，这些对象也称为 collection 的元素。一些 collection 允许有重复的元素，而另一些则不允许。一些 collection 是有序的，而另一些则是无序的。JDK 不提供此接口的任何*直接* 实现：它提供更具体的子接口（如 Set和 List）实现。此接口通常用来传递 collection，并在需要最大普遍性的地方操作这些 collection。（面向接口的编程思想）

## **(6)List**

**List：有序(元素存入集合的顺序和取出的顺序一致)，元素都有索引。元素可以重复。**

List本身是Collection接口的子接口，具备了Collection的所有方法。

List的特有方法都有索引，这是该集合最大的特点。

**List集合支持对元素的增、删、改、查。**

List中存储的元素实现类排序，而且可以重复的存储相关元素。

**次序是****List最重要的特点：它保证维护元素特定的顺序。**

 

List是有序的Collection，使用此接口能够精确的控制每个元素插入的位置。用户能够使用索引（元素在List中的位置，类似于数组下标）来访问List中的元素，这类似于Java的数组。

和下面要提到的Set不同，List允许有相同的元素。

 

除了具有Collection接口必备的iterator()方法外，List还提供一个listIterator()方法，返回一个 ListIterator接口，和标准的Iterator接口相比，ListIterator多了一些add()之类的方法，允许添加，删除，设定元素，还能向前或向后遍历。

 

**优点**：操作读取操作效率高，基于数组实现的，可以为null值，可以允许重复元素，有序，异步。

**缺点**：由于它是由动态数组实现的，不适合频繁的对元素的插入和删除操作，因为每次插入和删除都需要移动数组中的元素。 

 

## **(7)**ArrayList

ArrayList 是基于数组实现，内存中分配连续的空间，需要维护容量大小。随机访问.

ArrayList就是动态数组，也是一个对象。

ArrayList不自定义位置添加元素和LinkedList性能没啥区别，ArrayList默认元素追加到数组后面，而LinkedList只需要移动指针，所以两者性能相差无几。

如果ArrayList自定义位置插入元素，越靠前，需要重写排序的元素越多，性能消耗越大，LinkedList无论插入任何位置都一样，只需要创建一个新的表项节点和移动一下指针，性能消耗很低。

ArrayList是基于数组，所以查看任意位置元素只需要获取当前位置的下标的数组就可以，效率很高，然而LinkedList获取元素需要从最前面或者最后面遍历到当前位置元素获取，如果集合中元素很多，就会效率很低，性能消耗大。

**频繁遍历查看元素,使用 ArrayList 集合,**ArrayList 查询快，增删慢

**ArrayList线程不安全的**

1、ArrayList是用数组实现的，该对象存放在堆内存中，这个数组的内存是连续的，不存在相邻元素之间还隔着其他内存。底层是一个可动态扩容的数组

2、索引ArrayList时，速度比原生数组慢是因为你要用get方法，这是一个函数调用，而数组直接用[ ]访问，相当于直接操作内存地址，速度当然比函数调用快。

3、新建ArrayList的时候，JVM为其分配一个默认或指定大小的连续内存区域（封装为数组）。

4、每次增加元素会检查容量，不足则创建新的连续内存区域（大小等于初始大小+步长），也用数组形式封装，并将原来的内存区域数据复制到新的内存区域，然后再用ArrayList中引用原来封装的数组对象的引用变量引用到新的数组对象：

**elementData = Arrays.copyOf(elementData, newCapacity);**

　　ArrayList里面的removeIf方法就接受一个Predicate参数，采用如下Lambda表达式就能把，所有null元素删除:

**list.removeIf(e -> e == null)；**

ArrayList：每次添加元素之前会检查是否需要扩容,是按照原数组的1.5倍延长。构造一个初始容量为 10 的空列表。

get访问List内部任意元素时，ArrayList的性能要比LinkedList性能好。LinkedList中的get方法是要按照顺序从列表的一端开始检查，直到另一端。

在ArrayList的 中间插入或删除一个元素意味着这个列表中剩余的元素都会被移动；

ArrayList的空 间浪费主要体现在在list列表的结尾预留一定的容量空间

ArrayList只能包含对象类型。

ArrayList的大小是动态变化的。 

对于基本类型数据，集合使用自动装箱来减少编码工作量

够对自身进行枚举(因为实现了IEnumerable接口)。

具有索引(index),即可以通过index来直接获取和修改任意项。

ArrayList允许存放（不止一个）null元素

允许存放重复数据，存储时按照元素的添加顺序存储

ArrayList可以存放任何不同类型的数据（因为它里面存放的都是被装箱了的Object型对象，实际上ArrayList内部就是使用"object[] _items;"这样一个私有字段来封装对象的）

## **8)****linkedList**

LinkedList 是基于循环双向链表数据结构，不需要维护容量大小。顺序访问。

**频繁插入删除元素 使用 LinkedList 集合**

**LinkedList 线程不安全的**

LinkedList在随机访问方面相对比较慢，但是它的特性集较ArrayList 更大。

LinkedList提供了大量的首尾操作

LinkedList：底层的数据结构是链表，线程不同步，增删元素的速度非常快。

LinkedList：底层基于链表实现，链表内存是散乱的，每一个元素存储本身内存地址的同时还存储下一个元素的地址。链表增删快，查找慢 

LinkedList由双链表实现，增删由于不需要移动底层数组数据，其底层是链表实现的，只需要修改链表节点指针，对元素的插入和删除效率较高。

LinkedList缺点是遍历效率较低。HashMap和双链表也有关系。

LinkedList是一个继承于AbstractSequentialList的双向链表，它可以被当做堆栈、队列或双端队列进行操作

LinkedList可被用作堆栈（stack），队列（queue）或双向队列（deque）。

 

使用foreach适合循环LinkedList，使用双链表结构实现的应当使用foreach循环。

LinkedList实现了List接口，允许null元素。

LinkedList没有同步方法。如果多个线程同时访问一个List，则必须自己实现访问同步。一种解决方法是在创建List时构造一个同步的List：

Deque 和 Queue 是 LinkedList 的父接口，那么 LinkedList 也可以看成一种 Deque 或者 Queue；Queue表示一种队列，也是一种数据结构，它的特点是先进先出，因此在队列这个接口里面提供了一些操作队列的方法，同时LinkedList也具有这些方法；Deque(Double ended queues双端队列)，支持在两端插入或者移除元素; 那也应该具有操作双端队列的一些方法；LinkedList 是他们的子类，说明都具有他们两者的方法；LinkedList也可以充当队列，双端队列，堆栈多个角色。

## **(9)vector**

Vector：底层的数据结构就是数组，线程同步的，Vector无论查询和增删都巨慢。

Vector：是按照原数组的2倍延长。

Vector是基于线程安全的，效率低 元素有放入顺序，元素可重复 

Vector可以由我们自己来设置增长的大小，ArrayList没有提供相关的方法。

Vector相对ArrayList查询慢(线程安全的)

Vector相对LinkedList增删慢(数组结构)

以前还能见到Vector和Stack，但Vector太过古老，被ArrayList取代，所以这里不讲；而Stack已经被ArrayDeque取代。

 

对于想在迭代器迭代过程中针对集合进行增删改的，可以通过返回ListIterator来操作。

Vector：底层结构是数组，线程是安全的，添加删除慢，查找快，（同ArrayList）

 

ArrayList 和Vector是采用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元素，都允许直接序号索引元素，但是插入数据要涉及到数组元素移动等内存操作，所以索引数据快，插入数据慢，Vector由于使用了synchronized方法（线程安全）所以性能上比ArrayList要差，LinkedList使用双向链表实现存储，按序号索引数据需要进行向前或向后遍历，但是插入数据时只需要记录本项的前后项即可，所以插入数度较快。

## **(10)****Set**

**无序(存入和取出顺序有可能不一致)，不可以存储重复元素。必须保证元素唯一性。**

**元素无放入顺序，元素不可重复（注意：元素虽然无放入顺序，但是元素在set中的位置是有该元素的HashCode决定的，其位置其实是固定的）**

 

Set具有与Collection完全一样的接口，因此没有任何额外的功能,只是行为不同。这是继承与多态思想的典型应用：表现不同的行为。

Set不保存重复的元素(至于如何判断元素相同则较为负责)

存入Set的每个元素都必须是唯一的，因为Set不保存重复元素,加入Set的元素必须定义equals()方法以确保对象的唯一性。

Set 是基于对象的值来确定归属性的。 

Set本身有去重功能是因为String内部重写了hashCode()和equals()方法，在add里实现了去重, Set集合是不允许重复元素的，但是集合是不知道我们对象的重复的判断依据的，默认情况下判断依据是判断两者是否为同一元素（euqals方法，依据是元素==元素），如果要依据我们自己的判断来判断元素是否重复，需要重写元素的equals方法（元素比较相等时调用）hashCode()的返回值是元素的哈希码，如果两个元素的哈希码相同，那么需要进行equals判断。【所以可以自定义返回值作为哈希码】 equals()返回true代表两元素相同，返回false代表不同。

set集合没有索引，只能用迭代器或增强for循环遍历

set的底层是map集合

Set最多有一个null元素

必须小心操作可变对象（Mutable Object）。如果一个Set中的可变元素改变了自身状态导致Object.equals(Object)=true将导致一些问题。

Set具有与Collection完全一样的接口，没有额外的任何功能。所以把Set就是Collection，只是行为不同（这就是多态）；Set是基于对象的值来判断归属的，由于查询速度非常快速，HashSet使用了散列，HashSet维护的顺序与TreeSet或LinkedHashSet都不同，因为它们的数据结构都不同，元素存储方式自然也不同。TreeSet的数据结构是“红-黑树”，HashSet是散列函数，LinkedHashSet也用了散列函数；如果想要对结果进行排序，那么选择TreeSet代替HashSet是个不错的选择

**HashSet类直接实现了Set接口， 其底层其实是包装了一个HashMap去实现的。HashSet采用HashCode算法来存取集合中的元素，因此具有比较好的读取和查找性能。**

![1583846340264](/Users/awakeyoyoyo/Desktop/Java_Development_Note/images/1583846340264.jpg)

**元素值可以为NULL,但只能放入一个null**

　     **HashSet集合保证元素唯一性：通过元素的hashCode方法，和equals方法完成的。**

 

当元素的hashCode值相同时，才继续判断元素的equals是否为true。

如果hashCode值不同，那么不判断equals，从而提高对象比较的速度。

**对于HashSet集合，判断元素是否存在，或者删除元素，底层依据的是hashCode方法和equals方法。**　　

特点：存储取出都比较快

1、不能保证元素的排列顺序，顺序可能与添加顺序不同，顺序也有可能发生变化。

2、HashSet不是同步的，必须通过代码来保证其同步。

3、集合元素可以是null,但只能有一个

原理：简单说就是链表数组结合体

**对象的哈希值：普通的一个整数,可以理解为身份证号，是hashset存储的依据***

HashSet按Hash算法来存储集合中的元素。在存取和查找上有很好的性能。

当向HashSet集合中存入一个元素时，HashSet会调用该对象的hashCode()方法来得到该对象的hashCode值，然后根据该hashCode值决定该hashCode值决定该对象在HashSet中存储的位置。

如果有两个元素通过equals()方法比较返回true,但它们的hashCode()方法返回值不相等,hashSet将会把它们存储在不同位置，依然可以添加成功。如果两个对象的hashCode()方法返回的hashCode值相同，当它们的equals()方法返回false时，会在hashCode所在位置采用链式结构保存多个对象。这样会降低hashSet的查询性能。

 #### 在使用HashSet中重写hashCode()方法的基本原则

**1、在程序运行过过程中，同一个对象多次调用hashCode()方法应该返回相同的值。**

**2、当两个对象的equals()方法比较返回true时，这个两个对象的hashCode()方法返回相同的值。**

**3、对象中用作equals()方法比较标准的实例变量，都应该用于计算hashCode值。 **

把对象内的每个意义的实例变量(即每个参与equals()方法比较标准的实例变量)计算出一个int类型的hashCode值。用第1步计算出来的多个hashCode值组合计算出一个hashCode值返回 

 **return f1.hashCode()+(int)f2;** 

为了避免直接相加产生的偶然相等(两个对象的f1、f2实例变量并不相等，但他们的hashCode的和恰好相等)，可以通过为各个实例变量的hashCode值乘以一个质数后再相加

 **return f1.hashCode()\*19+f2.hashCode()\*37;** 

如果向HashSet中添加一个可变的对象后，后面的程序修改了该可变对想的实例变量，则可能导致它与集合中的其他元素的相同（即两个对象的equals()方法比较返回true,两个对象的hashCode值也相等），这就有可能导致HashSet中包含两个相同的对象。

## **(12)****Linkedhashset**

 LinkedHashSet : 具有HashSet的查询速度，且内部使用链表维护元素的顺序(插入的次序)。于是在使用迭代器遍历Set时，结果会按元素插入的次序

 **LinkedHashSet** 综合了链表+哈希表，根据元素的**hashCode**值来决定元素的存储位置，它同时使用**链表**维护元素的次序。

当遍历该集合时候，**LinkedHashSet** 将会以元素的添加顺序访问集合的元素。

对于 **LinkedHashSet** 而言，它继承与 **HashSet**、又基于 **LinkedHashMap** 来实现的。

**这个相对于HashSet来说有一个很大的不一样是LinkedHashSet是有序的。LinkedHashSet在迭代访问Set中的全部元素时，性能比HashSet好，但是插入时性能稍微逊色于HashSet。**

与HashSet相比，特点：

 对集合迭代时，按增加顺序返回元素。

 性能略低于HashSet，因为需要维护元素的插入顺序。但迭代访问元素时会有好性能，因为它采用链表维护内部顺序。

**LinkedHashSet不允许元素的重复**

存储的顺序是元素插入的顺序。

## **(13)****TreeSet**

TreeSet : 保存次序的Set, 底层为树结构。使用它可以从Set中提取有序的序列。

**TreeSet** 继承AbstractSet类，实现NavigableSet、Cloneable、Serializable接口。与HashSet是基于HashMap实现一样，**TreeSet** 同样是基于**TreeMap** 实现的。由于得到**Tree** 的支持，**TreeSet 最大特点在于排序，它的作用是提供有序的Set集合。**

 

用于对 Set 集合进行元素的指定顺序排序，排序需要依据元素自身具备的比较性。

如果元素不具备比较性，在运行时会抛出**ClassCastException** 异常。 所以元素需要实现Comparable 接口 ，让元素具备可比较性， 重写 compareTo 方法 。依据 compareTo 方法的返回值，确定元素在 TreeSet 数据结构中的位置。 或者用比较器方式，将Comparator对象传递给TreeSet构造器来告诉树集使用不同的比较方法

　

TreeSet底层的数据结构就是二叉树。

  　不能写入空数据

​    写入的数据是有序的。

​     不写入重复数据

**TreeSet会调用集合元素的compareTo(Object object)方法来比较元素之间的大小关系，然后将元素按升序排列**

**如果试图把一个元素添加到TreeSet中，则该对象必须实现Comparable接口实现Comparable接口必须实现compareTo(Object object)，两个对象即通过这个方法进行比较Comparable的典型实现**

**BigDecimal、BigInteger以及所有的数值类型对应的包装类型，按对应的数值大小进行比较**

**Character：按字符的Unicode值进行比较**

**Boolean：true对应的包装类实例大于false包装类对应的实例**

**String：按字符对应的Unicode值进行比较**

**Date、Time：后面的时间、日期比前面的时间、日期大**

 

**向TreeSet中添加一个元素，只有第一个不需要使用compareTo()方法，后面的都要调用该方法**

**因为只有相同类的两个实例才会比较大小，所以向TreeSet中添加的应该是同一个类的对象**

对于TreeSet集合而言，它判断两个对象的是否相等的唯一标准是:两个对象的通过compareTo(Object obj)方法比较是否返回0--如果通过compareTo(Object obj)方法比较返回0，TreeSet则会认为它们相等，否则认为它们不相等。对于语句，obj1.compareTo(obj2),如果该方法返回一个正整数，则表明obj1大于obj2;如果该方法返回一个负整数，则表明obj1小于obj2.

 

**在默认的compareTo方法中，需要将的两个的类型的对象的转换同一个类型，因此需要将的保证的加入到TreeSet中的数据类型是同一个类型，但是如果自己覆盖compareTo方法时，没有要求两个对象强制转换成同一个对象，是可以成功的添加treeSet中**

 

如果两个对象通过CompareTo(Object obj)方法比较返回0时，但它们通过equals()方法比较返回false时，TreeSet不会让第二个元素添加进去

## **(14)Map**

Map主要用于存储健值对，根据键得到值，因此不允许键重复，但允许值重复。

Map接口概述：**Java.util.Map**接口：是一个双列集合

Map集合的特点： 是一个双列集合，有两个泛型key和value，使用的时候key和value的数据类型可以相同。也可以不同.

 Key不允许重复的，value可以重复的；

 一个key只能对应一个value

底层是一个哈希表（数组+单向链表）：查询快，增删快, 是一个无序集合

 

Map接口中的常用方法：

 1.get(key) 根据key值返回对应的value值，key值不存在则返回null

 2.put(key , value); 往集合中添加元素（key和value）

 　注意：添加的时候，如果key不存在，返回值null

 　如果Key已经存在的话，就会新值替换旧值，返回旧值

 \3. remove(key); 删除key值对应的键值对；如果key不存在 ，删除失败。返回值为   null，如果key存在则删除成功，返回值为删除的value

 

Map遍历方式

第一种方式：通过key找value的方式：

　　　Map中有一个方法：

　　　　　　Set <k> keySet(); 返回此映射包含的键的Set 集合

　　　操作步骤:

 　　　1.调用Map集合的中方法keySet,把Map集合中所有的健取出来,存储到Set集合中

  　　  2.遍历Set集合,获取Map集合中的每一个健

 　　　3.通过Map集合中的方法get(key),获取value值

　　　  可以使用迭代器跟增强for循环遍历

 第二种方式：Map集合遍历键值方式

　　　　Map集合中的一个方法：

　　　　Set<Map.Entry<k,v>> entrySet(); 返回此映射中包含的映射关系的Set视图

　使用步骤

 　　　* 1.使用Map集合中的方法entrySet,把键值对(键与值的映射关系),取出来存储到Set  集合中

 　　　* 2.遍历Set集合,获取每一个Entry对象

 　　　* 3.使用Entry对象中的方法getKey和getValue获取健和值

　　可以使用迭代器跟增强for循环遍历

 

Collection中的集合元素是孤立的，可理解为单身，是一个一个存进去的，称为单列集合

Map中的集合元素是成对存在的，可理解为夫妻，是一对一对存进去的，称为双列集合

 

Map中存入的是：键值对，键不可以重复，值可以重复

Map主要用于存储带有映射关系的数据（比如学号与学生信息的映射关系）

 

Map没有继承Collection接口，Map提供key到value的映射。一个Map中不能包含相同的key，每个key只能映射一个 value。Map接口提供3种集合的视图，Map的内容可以被当作一组key集合，一组value集合，或者一组key-value映射。

Map具有将对象映射到其他对象的功能，是一个K-V形式存储容器，你可以通过containsKey()和containsValue()来判断集合是否包含某个减或某个值。Map可以很容以拓展到多维（值可以是其他容器甚至是其他Map）：

**Map>**

Map集合的数据结构仅仅针对键有效，与值无关。 

TreeSet采用红黑树的数据结构来存储集合元素

 **(15)HashMap**

HashMap非线程安全，高效，支持null；

根据键的HashCode 来存储数据，根据键可以直接获取它的值，具有很快的访问速度。**遍历时，取得数据的顺序是完全随机的。**

HashMap最多只允许一条记录的键为Null；允许多条记录的值为 Null。（不允许键重复，但允许值重复）

HashMap不支持线程的同步（任一时刻可以有多个线程同时写HashMap，即线程非安全），可能会导致数据的不一致。如果需要同步，可以用 Collections的synchronizedMap() 方法使HashMap具有同步的能力，或者使用ConcurrentHashMap。

**SynchronizedMap和ConcurrentHashMap 区别**

Collections.synchronizedMap()和Hashtable一样，实现上在调用map所有方法时，都对整个map进行同步，而ConcurrentHashMap的实现却更加精细，它对map中的所有桶加了锁。所以，只要要有一个线程访问map，其他线程就无法进入map，而如果一个线程在访问ConcurrentHashMap某个桶时，其他线程，仍然可以对map执行某些操作。这样，ConcurrentHashMap在性能以及安全性方面，明显比Collections.synchronizedMap()更加有优势。同时，同步操作精确控制到桶，所以，即使在遍历map时，其他线程试图对map进行数据修改，也不会抛出ConcurrentModificationException。

ConcurrentHashMap从类的命名就能看出，它必然是个HashMap。而Collections.synchronizedMap()可以接收任意Map实例，实现Map的同步

 

线程安全，并且锁分离。ConcurrentHashMap内部使用段(Segment)来表示这些不同的部分，每个段其实就是一个小的hashtable，它们有自己的锁。只要多个修改操作发生在不同的段上，它们就可以并发进行。 

Hashtable与 HashMap类似。不同的是：它不允许记录的键或者值为空；它支持线程的同步（任一时刻只有一个线程能写Hashtable，即线程安全），因此也导致了 Hashtable 在写入时会比较慢。

HashMap里面存入的值在取出的时候是随机的，它根据键的HashCode来存储数据，根据键可以直接获取它的值，具有很快的访问速度。在Map 中插入、删除和定位元素，HashMap 是最好的选择。

HashMap基于哈希表的 Map 接口的实现。此实现提供所有可选的映射操作，并允许使用 null 值和 null 键。（除了不同步和允许使用 null 之外，HashMap 类与 Hashtable 大致相同。）此类不保证映射的顺序，特别是它不保证该顺序恒久不变。

值得注意的是HashMap不是线程安全的，如果想要线程安全的HashMap，可以通过Collections类的静态方法synchronizedMap获得线程安全的HashMap。

**Map map = Collections.synchronizedMap(new HashMap());**

HashMap的底层主要是基于**数组和链表**来实现的，它之所以有相当快的查询速度主要是因为它是通过计算散列码来决定存储的位置。HashMap中主要是通过key的hashCode来计算hash值的，只要hashCode相同，计算出来的hash值就一样。如果存储的对象对多了，就有可能不同的对象所算出来的hash值是相同的，这就出现了所谓的hash冲突。学过数据结构的同学都知道，解决hash冲突的方法有很多，HashMap底层是通过**链表**来解决hash冲突的。

HashMap其实也是一个线性的数组实现的,所以可以理解为其存储数据的容器就是一个线性数组。这可能让我们很不解，一个线性的数组怎么实现按键值对来存取数据呢？这里HashMap有做一些处理。首先HashMap里面实现一个静态**内部类Entry**，其重要的属性有 key , value, next，从属性key,value我们就能很明显的看出来Entry就是HashMap键值对实现的一个基础bean，我们上面说到HashMap的基础就是一个线性数组，这个数组就是Entry[]，Map里面的内容都保存在Entry[]里面。

HashMap是常用的Java集合之一，是基于哈希表的Map接口的实现。与HashTable主要区别为不支持同步和允许null作为key和value。由于HashMap不是线程安全的，如果想要线程安全，可以使用ConcurrentHashMap代替。

HashMap的底层是哈希数组，数组元素为Entry。HashMap通过key的hashCode来计算hash值，当hashCode相同时，通过“拉链法”解决冲突



相比于之前的版本，jdk1.8在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为8）时，将链表转化为红黑树，以减少搜索时间。**原本Map.Entry接口的实现类Entry改名为了Node**。转化为红黑树时改用另一种实现TreeNode

![](/Users/awakeyoyoyo/Desktop/Java_Development_Note/images/1584193220239.jpg)

![img](https://images2018.cnblogs.com/blog/588112/201806/588112-20180626171656243-895639630.jpg)

1.8中最大的变化就是在一个Bucket中，如果存储节点的数量超过了**8个**，就会将该Bucket中原来以链表形式存储节点转换为以树的形式存储节点;而**如果少于6个，就会还原成链表形式存储。**

为什么要这样做？前面已经说过LinkedList的遍历操作不太友好，如果在节点个数比较多的情况下性能会比较差，而树的遍历效率是比较好的，主要是**优化遍历，提升性能**。

 

HashMap:去掉了contains(),保留了containsKey(),containsValue()

HashMap:key,value可以为空.null作为key只能有一个,null作为value可以存在多个

HashMap:使用Iterator

HashMap:**数组初始大小为16,扩容方式为2的指数幂形式**

HashMap:重新计算hash值

HashMap是基于哈希表的Map接口的实现，HashMap是一个散列表，存储的内容是键值对（key-value）映射，键值对都可为null；

HashMap继承自 AbstractMap<K, V> 并实现 Map<K, V>, Cloneable, Serializable接口；

HashMap实际上是一个“链表散列”的数据结构，即数组和链表的结合体。底层是个数组，数组上存储的数据是Entry<K,V>类型的链表结构对象。

HashMap是无序的，LinkedHashMap和treeMap是有序的；

HashMap基于哈希原理，可以通过put和get方法存储和获取对象。当我们将键值对传递给put方法时，它调用键对象的hashCode()方法来计算hashcode，然后找到对应的bucket位置存储键对象和值对象作为Map.Entry；**如果两个对象的hashcode相同，所以对应的bucket位置是相同的，HashMap采用链表解决冲突碰撞**，这个Entry（包含有键值对的Map.Entry对象）会存储到链表的下一个节点中；**如果对应的hashcode和key值都相同**，则修改对应的value的值。HashMap在每个链表节点中存储键值对对象。当使用get()方法获取对象时，HashMap会根据键对象的hashcode去找到对应的bucket位置，找到对应的bucket位置后会**调用keys.equals()方法去找到连表中对应的正确的节点**找到对象。

 

 HashMap是基于哈希表实现的，每一个元素是一个key-value对，其内部通过单链表解决冲突问题，容量不足（超过了阀值）时，同样会自动增长。

 HashMap 实现了Serializable接口，因此它支持序列化，实现了Cloneable接口,能被克隆。

HashMap存数据的过程是：

   HashMap内部维护了一个存储数据的Entry数组，HashMap采用**链表解决冲突**，每一个Entry本质上是一个单向链表。当准备添加一个key-value对时，首先通过hash(key)方法计算hash值，**然后通过indexFor(hash,length)求该key-value对的存储位置**，计算方法是先用**hash&0x7FFFFFFF后**，**再对length取模**，这就保证每一个key-value对都能存入HashMap中，当计算出的位置相同时，由于存入位置是一个链表，**则把这个key-value对插入链表头。**

 HashMap中key和value都允许为null。**key为null的键值对永远都放在以table[0]为头结点的链表中。**

HashMap内存储数据的Entry数组默认是16，如果没有对**Entry扩容机制**的话，当存储的数据一多，**Entry内部的链表会很长**，这就失去了HashMap的存储意义了。所以HasnMap内部有自己的扩容机制。HashMap内部有：

   变量size，它记录HashMap的底层数组中**已用槽的数量（bucket）**；

   变量threshold，它是HashMap的阈值，用于判断是否需要调整HashMap的容量**（threshold = 容量乘以加载因子）16乘以0.75  **

   变量DEFAULT_LOAD_FACTOR = 0.75f，默认加载因子为0.75

   HashMap扩容的条件是：**当size大于threshold时，对HashMap进行扩容 **

 扩容是是**新建了一个HashMap的底层数组，而后调用transfer方法，将就HashMap的全部元素添加到新的HashMap中**（要重新计算元素在新的数组中的索引位置）。 很明显，扩容是一个相当耗时的操作，因为它需要重新计算这些元素在新的数组中的位置并进行复制处理。因此，**我们在用HashMap的时，最好能提前预估下HashMap中元素的个数，这样有助于提高HashMap的性能。**

加载因子，**如果加载因子越大，对空间的利用更充分，但是查找效率会降低（链表长度会越来越长）**；**如果加载因子太小，那么表中的数据将过于稀疏（很多空间还没用，就开始扩容了），对空间造成严重浪费。**如果我们在构造方法中不指定，则系统默认加载因子为0.75，这是一个比较理想的值，一般情况下我们是无需修改的。另外，无论我们指定的容量为多少，构造方法都会将实际容量设为不小于指定容量的2的次方的一个数，且最大值不能超过2的30次方。 

HashMap的初始容量为16，Hashtable初始容量为11，两者的填充因子默认都是0.75。

HashMap扩容时是当前容量翻倍即:capacity*2，Hashtable扩容时是容量翻倍+1即:capacity*2+1。

HashMap和Hashtable的底层实现都是数组+链表结构实现。

HashMap计算hash对**key的hashcode**进行了二次hash，以获得更好的散列值，然后对table数组长度取摸：

**static int hash(int h) {**   

**h ^= (h >>> 20) ^ (h >>> 12);**   

**return h ^ (h >>> 7) ^ (h >>> 4);**

**}**

**static int indexFor(int h, int length) {**   

**return h & (length-1);**

**}**

 

HashMap多线程put操作后，get操作导致死循环。**为何出现死循环？**

大家都知道，HashMap采用链表解决Hash冲突，具体的HashMap的分析因为是链表结构，那么就很容易形成闭合的链路，这样在循环的时候只要有线程对这个HashMap进行get操作就会产生死循环。但是，我好奇的是，这种闭合的链路是如何形成的呢。在单线程情况下，只有一个线程对HashMap的数据结构进行操作，是不可能产生闭合的回路的。那就只有在多线程并发的情况下才会出现这种情况，**那就是在put操作的时候，如果size>initialCapacity*loadFactor，那么这时候HashMap就会进行rehash操作，随之HashMap的结构就会发生翻天覆地的变化。很有可能就是在两个线程在这个时候同时触发了rehash操作，产生了闭合的回路。**

 

**简单来说，HashMap由数组+链表组成的，数组是HashMap的主体，链表则是主要为了解决哈希冲突而存在的，如果定位到的数组位置不含链表（当前entry的next指向null）,那么对于查找，添加等操作很快，仅需一次寻址即可；如果定位到的数组包含链表，对于添加操作，其时间复杂度依然为O(1)，因为最新的Entry会插入链表头部，仅需要简单改变引用链即可，而对于查找操作来讲，此时就需要遍历链表，然后通过key对象的equals方法逐一比对查找。所以，性能考虑，HashMap中的链表出现越少，性能才会越好。**

HashMap存储自定义类型:**使用HashMap储存自定义类形式，因为要保证key的唯一性。需要 自定义类重写  hashCode()跟equals()方法；**

HashMap的方法基本都是Map中声明的方法

实现原理：实现一个哈希表，存储元素(key/value)时，**用key计算hash值**，如果hash值没有碰撞，则只用数组存储元素；如果hash值碰撞了，则相同的hash值的元素用链表存储；如果相同hash值超过8个，则相同的hash值的元素用**红黑树存储**。获取元素时，用key计算hash值，用hash值计算元素在数组中的下标，取得元素如果命中，则返回；如果不是就在红黑树或链表中找。

PS：存储元素的数组是有冗余的。

采用了Fail-Fast机制，通过一个modCount值记录修改次数，在迭代过程中，判断modCount跟初始过程记录的expectedModCount是否相等，如果不相等就表示已经有其他线程修改了Map，马上抛出异常；另外扩容过程中还有可能产生环形链表。

synchronized是针对整张Hash表的，即每次锁住整张表让线程独占**注意死锁问题**

## **(16)HashTable**

HashTable线程安全，低效，不支持null ,Hashtable是同步的

HashTable这个类实现了哈希表从key映射到value的数据结构形式。任何非null的对象都可以作为key或者value。

要在hashtable中存储和检索对象，作为key的对象必须实现hashCode、equals方法。

 

一般来说，默认的加载因子（0.75）提供了一种对于空间、时间消耗比较好的权衡策略。太高的值（指加载因子loadFactor）虽然减少了空间开销但是增加了检索时间，这反应在对hashtable的很多操作中，比如get、put方法。

初始容量的控制也是在空间消耗和rehash操作耗时(该操作耗时较大)二者之间的权衡。 如果初始容量大于哈希表的当前最大的条目数除以加载因子，则不会发生rehash。但是，将初始容量设置过高会浪费空间。

如果有大量的数据需要放进hashtable，则**选择设置较大的初始容量比它自动rehash更优。**

 如果不需要线程安全的实现，建议使用HashMap代替Hashtable

如果想要**一个线程安全的高并发实现，那么建议使用**java.util.concurrent.ConcurrentHashMap取代了Hashtable。

HashTable的父类是Dictionary

 **concurrent同时**    **synchronized已同步**

HashTable:线程安全,HashTable方法有synchronized修饰

HashTable:保留了contains(),containsKey(),containsValue()

HashTable:key,value都不能为空.原因是源码中方法里会遍历entry,然后用entry的key或者value调用equals(),所以要先判断key/value是否为空,如果为空就会抛出异常

HashTable:使用Enumeration,Iterator

HashTable:数组初始大小为11,扩容方式为2*old+1

HashTable: 直接使用hashcode()

Hashtable同样是基于哈希表实现的，同样每个元素是一个key-value对，其内部也是通过单链表解决冲突问题，容量不足（超过了阀值）时，同样会自动增长。

 

Hashtable也是JDK1.0引入的类，是线程安全的，能用于多线程环境中。

Hashtable同样实现了Serializable接口，它支持序列化，实现了Cloneable接口，能被克隆。

Hashtable计算hash是直接使用key的hashcode对table数组的长度直接进行取模：

**int hash = key.hashCode(); int index = (hash & 0x7FFFFFFF) % tab.length;**

 

底层数据结构是哈希表,特点和 hashMap 是一样的

 　　　Hashtable 是线程安全的集合,是单线程的,运行速度慢

 　　　HashMap 是线程不安全的集合,是多线程的,运行速度快

 　　　Hashtable 命运和 Vector 是一样的,从 JDK1.2 开始,被更先进的 HashMap 取代

　　　　 HashMap 允许存储 null 值,null 健

 　　　Hashtable 不允许存储 null 值,null 健

　　　　 Hashtable 他的孩子,子类 Properties 依然活跃在开发舞台

 

**Properties**

Java.util.Properties 集合 extends Hashtable<k,v> 集合

Properties 集合特点：

Properties集合也是一个双列集合，key跟value都已经被内置为String类型

Properties集合是一个唯一和IO流相结合的集合

可以将集合中存储的临时数据，持久化到硬盘的文件中储存

可以把文件中储存对的键值对，读取到集合中使用

 

Properties集合的基本操作：添加数据，遍历集合,Key和value都已经被内置为String类型。里面包含了一些和String类的相关方法

 Object setProperty(String key ,String value) 往集合中添加键值对，调用Hashtable的方法put添加

 String getProperty(String key ) 通过key获取value的值，相当于Map集合中的get(key) 方法

 Set<String >  stringPropertyNames()返回此属性列表的键集。相当于Map集合中的keySet()方法；

 

Properties类的load方法：

  可以把文件中存储的键值对,读取到集合中使用

 void load(Reader reader)  

 void load(InputStream inStream)  

 参数:

 Reader reader:字符输入流,可以使用FileReader

 InputStream inStream:字节输入流,可以使用FileInputStream

 操作步骤:

 1.创建Properties集合对象

 2.创建字符输入流FileReader对象,构造方法中绑定要读取的数据源

 3.使用Properties集合中的方法load,把文件中存储的键值对,读取到集合中使  用

 4.释放资源

 5.遍历Properties集合

注意:

 1.流使用Reader字符流,可以读取中文数据

 2.流使用InputStream字节流,不能操作中文,会有乱码

 3.Properties集合的配置文件中,可以使用注释单行数据,使用#

 4.Properties集合的配置文件中,key和value默认都是字符串,不用添加""(画蛇  添足)

 5.Properties集合的配置文件中,key和value的连接符号可以使用=,也可以使用  空格

 

Properties类的store方法使用：

可以把集合中存储的临时数据,持久化都硬盘的文件中存储

   void store(Writer writer, String comments)  

​           void store(OutputStream out, String comments)

 参数:

 Writer writer:字符输出流,可以使用FileWriter

 OutputStream out:字节输出流,可以使用FileOutputStream

 String comments:注释,解释说明存储的文件,不能使用中文(乱码),默认编码格式为  Unicode编码

可以使用""空字符串

 操作步骤:

 1.创建Properties集合,往集合中添加数据

 2.创建字符输出流FileWriter对象,构造方法中绑定要写入的目的地

 3.调用Properties集合中的方法store,把集合中存储的临时数据,持久化都硬盘的文  件中存储

 4.释放资源

注意:

 1.流使用Writer字符流,可以写入中文数据的

 2.流使用OutputStream字节流,不能操作中文,会有乱码

 3.Propertie集合存储的文件,一般都以.properties结尾(程序员默认)

 **(18)Queue**

 Queue用于模拟队列这种数据结构，实现“FIFO”等数据结构。即第一个放进去就是第一个拿出来的元素（从一端进去，从另一端出来）。队列常作被当作一个可靠的将对象从程序的某个区域传输到另一个区域的途径。通常，队列不允许随机访问队列中的元素。

 

Queue 接口并未定义阻塞队列的方法，而这在并发编程中是很常见的。BlockingQueue 接口定义了那些等待元素出现或等待队列中有可用空间的方法，这些方法扩展了此接口。

 

 Queue 实现通常不允许插入 null 元素，尽管某些实现（如 LinkedList）并不禁止插入 null。即使在允许 null 的实现中，也不应该将 null 插入到 Queue 中，因为 null 也用作 poll 方法的一个特殊返回值，表明队列不包含元素。 

 

LinkedList提供了方法以支持队列的行为，并且实现了Queue接口。通过LinkedList向上转型（up cast）为Queue，看Queue的实现就知道相对于LinkedList，Queue添加了element、offer、peek、poll、remove方法

offer：在允许的情况下，将一个元素插入到队尾，或者返回false

peek，element：在不移除的情况下返回队头，peek在队列为空返回null，element抛异常NoSuchElementException

poll,remove：移除并返回队头，poll当队列为空是返回null，remove抛出NoSuchElementException异常

注意：queue.offer在自动包装机制会自动的把random.nextInt转化程Integer，把char转化成Character

#### (19)**Deque**

Deque是Queue的子接口,我们知道Queue是一种队列形式,而Deque则是双向队列,它支持从两个端点方向检索和插入元素,因此Deque既可以支持LIFO形式也可以支持LIFO形式.Deque接口是一种比Stack和Vector更为丰富的抽象数据形式,因为它同时实现了以上两者.

添加功能

void push(E) 向队列头部插入一个元素,失败时抛出异常

void addFirst(E) 向队列头部插入一个元素,失败时抛出异常

void addLast(E) 向队列尾部插入一个元素,失败时抛出异常

boolean offerFirst(E) 向队列头部加入一个元素,失败时返回false

boolean offerLast(E) 向队列尾部加入一个元素,失败时返回false

获取功能

E getFirst() 获取队列头部元素,队列为空时抛出异常

E getLast() 获取队列尾部元素,队列为空时抛出异常

E peekFirst() 获取队列头部元素,队列为空时返回null

E peekLast() 获取队列尾部元素,队列为空时返回null

删除功能

boolean removeFirstOccurrence(Object) 删除第一次出现的指定元素,不存在时返回false

boolean removeLastOccurrence(Object) 删除最后一次出现的指定元素,不存在时返回false

弹出功能

E pop() 弹出队列头部元素,队列为空时抛出异常

E removeFirst() 弹出队列头部元素,队列为空时抛出异常

E removeLast() 弹出队列尾部元素,队列为空时抛出异常

E pollFirst() 弹出队列头部元素,队列为空时返回null

E pollLast() 弹出队列尾部元素,队列为空时返回null

迭代器

Iterator<E> descendingIterator() 返回队列反向迭代器

 

同Queue一样,Deque的实现也可以划分成通用实现和并发实现.

　　通用实现主要有两个实现类ArrayDeque和LinkedList.

　　ArrayDeque是个可变数组,它是在Java 6之后新添加的,而LinkedList是一种链表结构的list,LinkedList要比ArrayDeque更加灵活,因为它也实现了List接口的所有操作,并且可以插入null元素,这在ArrayDeque中是不允许的.

　　从效率来看,ArrayDeque要比LinkedList在两端增删元素上更为高效,因为没有在节点创建删除上的开销.最适合使用LinkedList的情况是迭代队列时删除当前迭代的元素.此外LinkedList可能是在遍历元素时最差的数据结构,并且也LinkedList占用更多的内存,因为LinkedList是通过链表连接其整个队列,它的元素在内存中是随机分布的,需要通过每个节点包含的前后节点的内存地址去访问前后元素.

　　总体ArrayDeque要比LinkedList更优越,在大队列的测试上有3倍与LinkedList的性能,最好的是给ArrayDeque一个较大的初始化大小,以避免底层数组扩容时数据拷贝的开销.

　　LinkedBlockingDeque是Deque的并发实现,在队列为空的时候,它的takeFirst,takeLast会阻塞等待队列处于可用状态

## **(20)Stack**

Stack继承自Vector，实现一个后进先出的堆栈。Stack提供5个额外的方法使得 Vector得以被当作堆栈使用。基本的push和pop方法，还有peek方法得到栈顶的元素，empty方法测试堆栈是否为空，search方法检测一个元素在堆栈中的位置。Stack刚创建后是空栈。

 

栈，是指“LIFO”先进后出的集合容器，最后一个压入的元素是第一个出来的，就好比我们洗碗一样（或者叠罗汉）第一个摆放的碗放在最下面，自然是最后一个拿出来的。Stack是由LinkedList实现的，作为Stack的实现，下面是《java编程思想》给出基本的Stack实现：

peek和pop是返回T类型的对象。peek方法提供栈顶元素，但不删除栈顶，而pop是返回并删除栈顶元素;

##  

## **(20)ArrayDeque**

ArrayDeque类是双端队列的实现类，类的继承结构如下面，继承自AbastractCollection（该类实习了部分集合通用的方法，其实现了Collection接口），其实现的接口Deque接口中定义了双端队列的主要的方法，比如从头删除，从尾部删除，获取头数据，获取尾部数据等等。

public class ArrayDeque<E> extends AbstractCollection<E>              implements Deque<E>, Cloneable, Serializable

 

ArrayDeque基本特征

就其实现而言，ArrayDeque采用了**循环数组**的方式来完成双端队列的功能。 

\1. 无限的扩展，自动扩展队列大小的。（当然在不会内存溢出的情况下。） 

\2. 非线程安全的，不支持并发访问和修改。 

\3. 支持fast-fail. 

\4. 作为栈使用的话比比栈要快. 

\5. 当队列使用比linklist要快。 

\6. null元素被禁止使用。

 

最小初始化容量限制8(必须是2的幂次)

 

扩容:之所以说该ArrayDeque容量无限制，是因为只要检测到head==tail的时候，就直接调用doubleCapacity方法进行扩容。

 

删除元素:删除元素的基本思路为确定那一侧的数据少，少的一侧移动元素位置，这样效率相对于不比较更高些，然后，判断head是跨越最大值还是为跨越最大值，继而可以分两种不同的情况进行拷贝。但是该方法比较慢，因为存在数组的拷贝。

 

获取并删除元素:这里在举个简单点的例子，中间判断是不是null，可以看出该队列不支持null,通过把其值设为null就算是将其删除了。然后head向递增的方向退一位即可。 

 

ArrayDeque和LinkedList是Deque的两个通用实现

ArrayDeque不是线程安全的。 

ArrayDeque不可以存取null元素，因为系统根据某个位置是否为null来判断元素的存在。 

当作为栈使用时，性能比Stack好；当作为队列使用时，性能比LinkedList好。 

 **(22)PriorityQueue**

我们知道队列是遵循先进先出（First-In-First-Out）模式的，但有些时候需要在队列中基于优先级处理对象。举个例子，比方说我们有一个每日交易时段生成股票报告的应用程序，需要处理大量数据并且花费很多处理时间。客户向这个应用程序发送请求时，实际上就进入了队列。我们需要首先处理优先客户再处理普通用户。在这种情况下，Java的PriorityQueue(优先队列)会很有帮助。

 

PriorityQueue类在Java1.5中引入并作为 Java Collections Framework 的一部分。PriorityQueue是基于优先堆的一个无界队列，这个优先队列中的元素可以默认自然排序或者通过提供的Comparator（比较器）在队列实例化的时排序。

优先队列不允许空值，而且不支持non-comparable（不可比较）的对象，比如用户自定义的类。优先队列要求使用Java Comparable和Comparator接口给对象排序，并且在排序时会按照优先级处理其中的元素。

优先队列的头是基于自然排序或者[Comparator](http://www.journaldev.com/780/java-comparable-and-comparator-example-to-sort-objects)排序的最小元素。如果有多个对象拥有同样的排序，那么就可能随机地取其中任意一个。当我们获取队列时，返回队列的头对象。

优先队列的大小是不受限制的，但在创建时可以指定初始大小。当我们向优先队列增加元素的时候，队列大小会自动增加。

PriorityQueue是非线程安全的，所以Java提供了PriorityBlockingQueue（实现BlockingQueue接口）用于Java多线程环境。

由于知道PriorityQueue是基于Heap的，当新的元素存储时，会调用siftUpUsingComparator方法

 

 

PriorityQueue的逻辑结构是一棵完全二叉树，存储结构其实是一个数组。逻辑结构层次遍历的结果刚好是一个数组。

PriorityQueue优先队列,它逻辑上使用堆结构（完全二叉树）实现，物理上使用动态数组实现，并非像TreeMap一样完全有序，但是如果按照指定方式出队，结果可以是有序的。

这里的堆是一种数据结构而非计算机内存中的堆栈。堆结构在逻辑上是完全二叉树，物理存储上是数组。

完全二叉树并不是堆结构，堆结构是不完全有序的完全二叉树。

 

## **(23)BlockingQueue**

Java中Queue的最重要的应用大概就是其子类BlockingQueue了。

考虑到生产者消费者模型，我们有多个生产者和多个消费者，生产者不断提供资源给消费者，但如果它们的生产/消费速度不匹配或者不稳定，则会造成大量的生产者闲置/消费者闲置。此时，我们需要使用一个缓冲区来存储资源，即生产者将资源置于缓冲区，而消费者不断地从缓冲区中取用资源，从而减少了闲置和阻塞。

BlockingQueue，阻塞队列，即可视之为一个缓冲区应用于多线程编程之中。当队列为空时，它会阻塞所有消费者线程，而当队列为满时，它会阻塞所有生产者线程。

在queue的基础上，BlockingQueue又添加了以下方法：

 put：队列末尾添加一个元素，若队列已满阻塞。

 take：移除并返回队列头部元素，若队列已空阻塞。

 drainTo:一次性获取所有可用对象，可以用参数指定获取的个数，该操作是原子操作，不需要针对每个元素的获取加锁。

 

 

## **(24) ArrayBlockingQueue**

由一个定长数组和两个标识首尾的整型index标识组成，生产者放入数据和消费者取出数据对于ArrayBlockingQueue而言使用了同一个锁（一个私有的ReentrantLock），因而无法实现真正的并行。可以在初始化时除长度参数以外，附加一个boolean类型的变量，用于给其私有的ReentrantLock进行初始化（初始化是否为公平锁，默认为false）。

 

## **(25) LinkedBlockingQueue**

LinkedBlockingQueue的最大特点是，若没有指定最大容量，其可以视为无界队列（有默认最大容量限制,往往系统资源耗尽也无法达到）。即，不对生产者的行为加以限制，只在队列为空的时候限制消费者的行为。LinkedBlockingQueue采用了读写分离的两个ReentrantLock去控制put和take，因而有了更好的性能（类似读写锁提供读写场景下更好的性能），如下：

  /** Lock held by take, poll, etc */   private final ReentrantLock takeLock = new ReentrantLock();   /** Wait queue for waiting takes */   private final Condition notEmpty = takeLock.newCondition();   /** Lock held by put, offer, etc */   private final ReentrantLock putLock = new ReentrantLock();   /** Wait queue for waiting puts */   private final Condition notFull = putLock.newCondition();

ArrayBlockingQueue和LinkedBlockingQueue是最常用的两种阻塞队列。

 

## **(26) PriorityBlockingQueue**

PriorityBlockingQueue是对PriorityQueue的包装，因而也是一个优先队列。其优先级默认是直接比较，大者先出队，也可以从构造器传入自定义的Comparator。由于PriorityQueue从实现上是一个无界队列，PriorityBlockingQueue同样是一个无界队列，对生产者不做限制。

 

## **(27) DelayQueue**

DelayQueue是在PriorityBlockingQueue的基础上包装产生的，它用于存放Delayed对象，该队列的头部是延迟期满后保存时间最长的Delayed元素（即，以时间为优先级利用PriorityBlockingQueue），当没有元素延迟期满时，对其进行poll操作将会返回Null。take操作会阻塞。

 

## **(28) SynchronousQueue**

SynchronousQueue十分特殊，它没有容量——换言之，它是一个长度为0的BlockingQueue，生产者和消费者进行的是无中介的直接交易，当生产者/消费者没有找到合适的目标时，即会发生阻塞。但由于减少了环节，其整体性能在一些系统中可能更加适合。该方法同样支持在构造时确定为公平/默认的非公平模式，如果是非公平模式，有可能会导致某些生产者/消费者饥饿。

 

## **(29)WeakHashMap**

WeakHashMap是一种改进的HashMap，它对key实行“弱引用”，如果一个key不再被外部所引用，那么该key可以被GC回收。

 

## **(30)EnumSet类**

EnumSet是一个专门为枚举设计的集合类，EnumSet中的所有元素都必须是指定枚举类型的枚举值，该枚举类型的创建Enumset时显示会隐式的指定。Enumset的集合元素也是有序的，EnumSet以枚举值在Enum类内定义的顺序来决定集合元素的顺序。

#### (32)使用java 8 新增的Stream操作集合

Java8新增了Stream、IntStream、LongStream、DoubleStream等流式API，这些API代表了多个支持串行和并行聚集操作的元素，其中Stream是一个通用的流接口，而IntStream、LongStream、DoubleStream则代表了类型为int，long，double的流。

   独立使用Stream的步骤如下:

  1、使用Stream或XxxStream的builder()类方法创建该Stream对应的Builder。

   2、重复调用Builder的add()方法向该流中的添加多个元素

   3、调用Builder的build()方法获取对应的Stream

   4、调用Stream的聚集方法。

 

在Stream中方法分为两类中间方法和末端方法

中间方法：中间操作允许流保持打开状态,并允许直接调用后续方法。上面程序中的map()方法就是中间方法。

末端方法：末端方法是对流的最终操作。当对某个Stream执行末端方法后，该流将会被"消耗"且不再可用。上面程序中的sum()、count()、average()等方法都是末端方法。

除此之外，关于流的方法还有如下特征：

有状态的方法：这种方法会给你流增加一些新的属性，比如元素的唯一性、元素的最大数量、保证元素的排序的方式被处理等。有状态的方法往往需要更大的性能开销

短路方法:短路方法可以尽早结束对流的操作，不必检查所有的元素。

 

## 迭代器**

### **[1**].迭代器模式**

把访问逻辑从不同类型的集合类中抽取出来，从而避免向外部暴露集合的内部结构。在java中它是一个对象，其目的是遍历并选中其中的每个元素，而使用者（客户端）无需知道里面的具体细节。

### **[2].Iterator**

ollection集合元素的通用获取方式：在取出元素之前先判断集合中有没有元素。如果有，就把这个元素取出来，继续再判断，如果还有就再取出来，一直把集合中的所有元素全部取出来，这种取出元素的方式专业术语称为迭代。

java.util.Iterator:在Java中Iterator为一个接口，它只提供了迭代的基本规则。在JDK中它是这样定义的：对Collection进行迭代的迭代器。迭代器取代了Java Collection Framework中的Enumeration。

**Collection中有一个抽象方法iterator方法，所有的Collection子类都实现了这个方法；返回一个Iterator对象**

**定义:**

```java
package java.util;

public interface Iterator<E> {

    boolean hasNext();//判断是否存在下一个对象元素

    E next();//获取下一个元素

    void remove();//移除元素

}
```

在使用Iterator的时候禁止对所遍历的容器进行改变其大小结构的操作。例如: 在使用Iterator进行迭代时，如果对集合进行了add、remove操作就会出现ConcurrentModificationException异常。

在进行集合元素取出的时候，如果集合中没有元素了，还继续使用next()方法的话，将发生NoSuchElementException没有集合元素的错误

修改并发异常：在迭代集合中元素的过程中，集合的长度发生改变（进行了元素增加或者元素删除的操作), 增强for的底层原理也是迭代器，所以也需要避免这种操作；

解决以上异常的方法:使用**ListIterator**

任何集合都有迭代器。

任何集合类，都必须能以某种方式存取元素，否则这个集合容器就没有任何意义。

迭代器，也是一种模式（也叫迭代器模式）。迭代器要足够的“轻量”——创建迭代器的代价小。

### **Iterable(1.5)**

Java中还提供了一个Iterable接口，Iterable接口实现后的功能是‘返回’一个迭代器，我们常用的实现了该接口的子接口有:Collection<E>、List<E>、Set<E>等。该接口的iterator()方法返回一个标准的Iterator实现。实现Iterable接口允许对象成为Foreach语句的目标。就可以通过foreach语句来遍历你的底层序列。

Iterable接口包含一个能产生Iterator对象的方法，并且Iterable被foreach用来在序列中移动。因此如果创建了实现Iterable接口的类，都可以将它用于foreach中。

**定义:**

```java
Package java.lang; import java.util.Iterator; 
public interface Iterable { 
Iterator iterator();
}
```

Iterable是Java 1.5的新特性, 主要是为了支持forEach语法, 使用容器的时候, 如果不关心容器的类型, 那么就需要使用迭代器来编写代码. 使代码能够重用.

使用方法很简单:

```java
List strs = Arrays.asList("a", "b", "c"); 

for (String str: strs) { 

out.println(str);

}


```

好处：代码减少，方便遍历

弊端：没有索引，不能操作容器里的元素

增强for循环底层也是使用了迭代器获取的，只不过获取迭代器由jvm完成，不需要我们获取迭代器而已，所以在使用增强for循环变量元素的过程中不准使用集合对象对集合的元素个数进行修改；

### **[4].**forEach()(1.8)

使用接收lambda表达式的forEach方法进行快速遍历.

**List strs = Arrays.asList("a", "b", "c");** // 使用Java 1.8的lambda表达式 strs.forEach(out::println);

### **[5].Spliterator迭代器**

　  Spliterator是1.8新增的迭代器,属于并行迭代器,可以将迭代任务分割交由多个线程来进行。

Spliterator可以理解为Iterator的Split版本（但用途要丰富很多）。使用Iterator的时候，我们可以顺序地遍历容器中的元素，使用Spliterator的时候，我们可以将元素分割成多份，分别交于不于的线程去遍历，以提高效率。使用 Spliterator 每次可以处理某个元素集合中的一个元素 — 不是从 Spliterator 中获取元素，而是使用 tryAdvance() 或 forEachRemaining() 方法对元素应用操作。但Spliterator 还可以用于估计其中保存的元素数量，而且还可以像细胞分裂一样变为一分为二。这些新增加的能力让流并行处理代码可以很方便地将工作分布到多个可用线程上完成

### **[6].ListIterator**

ListIterator是一个更强大的Iterator子类型，能用于各种List类访问，前面说过Iterator支持单向取数据，ListIterator可以双向移动，所以能指出迭代器当前位置的前一个和后一个索引，可以用set方法替换它访问过的最后一个元素。我们可以通过调用listIterator方法产生一个指向List开始处的ListIterator，并且还可以用过重载方法listIterator(n)来创建一个指定列表索引为n的元素的ListIterator。

**ListIterator可以往前遍历，添加元素，设置元素** 

**Iterator和ListIterator的区别：**

两者都有next()和hasNext()，可以实现向后遍历，但是ListIterator有previous()和hasPrevious()方法，即可以实现向前遍历

ListIterator可以定位当前位置，nextIndex()和previous()可以实现

ListIterator有add()方法，可以向list集合中添加数据

都可以实现删除操作，但是ListIterator可以实现对对象的修改，set()可以实现，Iterator仅能遍历，不能修改

### **[7]Fail-Fast**

类中的iterator()方法和listIterator()方法返回的iterators迭代器是**fail-fast**的：当某一个线程A通过iterator去遍历某集合的过程中，若该集合的内容被其他线程所改变了；那么线程A访问集合时，就会抛出ConcurrentModificationException异常，产生fail-fast事件。

**迭代器与枚举有两点不同:**

　　1. 迭代器在迭代期间可以从集合中移除元素。

　　2. 方法名得到了改进，Enumeration的方法名称都比较长。

迭代器的好处：屏蔽了集合之间的不同，可以使用相同的方式取出







## 自我总结

最近在复习基础的东西，学着看了一下hashmap源码，一步步看下来，不懂得就google，发现收获挺大的

## Jdk1.8的源码分析：

```java

    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; 

    static final int MAXIMUM_CAPACITY = 1 << 30;

    static final float DEFAULT_LOAD_FACTOR = 0.75f;

    static final int TREEIFY_THRESHOLD = 8;

    static final int UNTREEIFY_THRESHOLD = 6;
     
    static final int MIN_TREEIFY_CAPACITY = 64;
		
		transient Node<K,V>[] table;

    transient Set<Map.Entry<K,V>> entrySet;

    transient int size;

    transient int modCount;

    int threshold;

```



- DEFAULT_INITIAL_CAPACITY:桶的初始化大小默认16 (必须为2的次方数)

- MAXIMUM_CAPACITY ：桶最大值(2的一次幂至2的30次幂之间)

- DEFAULT_LOAD_FACTOR:默认的负载因子（0.75)

- TREEIFY_THRESHOLD:用于判断是否需要将链表转换为红黑树的阈值。默认为8

- UNTREEIFY_THRESHOLD：用于判断是否需要将红黑树转换为链表的阈值。默认为6

- MIN_TREEIFY_CAPACITY：在转变成红黑树之前，还会有一次判断，只有键值对数量大于 64 才会发生转换。这是为了避免在哈希表建立初期，多个键值对恰好被放入了同一个链表中而导致不必要的转化(例子：即如果有一个桶中有九个键值对大于8个，则会触发是否转化为红黑树，此时还需要判断总键值对是否大于64，否则不会对该桶的链表转化为红黑树，只是对table进行扩容)

  即链表长度大于8而且整个map中的键值对大于等于64

- table：真正存放数据的数组。其实就是Entry<k,v>

- size:存放键值对数量的大小。

- entrySet:保存缓存的entrySet（）。 用于keySet（）和values（）。

- threshold:扩容的阀值

- loadFactor:负载因子，可在初始化时显式指定

  ### 构造函数

  ```java
  //初始化
  public HashMap(int initialCapacity, float loadFactor) {
          if (initialCapacity < 0)
              throw new IllegalArgumentException("Illegal initial capacity: " +
                                                 initialCapacity);
          if (initialCapacity > MAXIMUM_CAPACITY)
              initialCapacity = MAXIMUM_CAPACITY;
          if (loadFactor <= 0 || Float.isNaN(loadFactor))
              throw new IllegalArgumentException("Illegal load factor: " +
                                                 loadFactor);
          this.loadFactor = loadFactor;
          this.threshold = tableSizeFor(initialCapacity);
      }
  //默认构造方法
  public HashMap() {
          this.loadFactor = DEFAULT_LOAD_FACTOR; // all other fields defaulted
      }
  
  ```

  initialCapacity、loadFactor用于初始化hasp的loadFactor的初始容量、负载因子。Map 在使用过程中不断的往里面存放数据，当数量达到了 `16 * 0.75 = 12` 就需要将当前 16 的容量进行扩容，而扩容这个过程涉及到 rehash、复制数据等操作，所以非常消耗性能。

  ### 真正存储内容的table

  ```java
  
   transient Node<K,V>[] table;
  
  
  static class Node<K,V> implements Map.Entry<K,V> {
          final int hash;
          final K key;
          V value;
          Node<K,V> next;
  
          Node(int hash, K key, V value, Node<K,V> next) {
              this.hash = hash;
              this.key = key;
              this.value = value;
              this.next = next;
          }
  
          public final K getKey()        { return key; }
          public final V getValue()      { return value; }
          public final String toString() { return key + "=" + value; }
  
          public final int hashCode() {
              return Objects.hashCode(key) ^ Objects.hashCode(value);
          }
  
          public final V setValue(V newValue) {
              V oldValue = value;
              value = newValue;
              return oldValue;
          }
  
          public final boolean equals(Object o) {
              if (o == this)
                  return true;
              if (o instanceof Map.Entry) {
                  Map.Entry<?,?> e = (Map.Entry<?,?>)o;
                  if (Objects.equals(key, e.getKey()) &&
                      Objects.equals(value, e.getValue()))
                      return true;
              }
              return false;
          }
      }
  ```

  Node<K,V>是 HashMap 中的一个内部类，实现了Map.Entry<K,V>接口,从他的成员变量很容易看出：

  ```java
  				final int hash;
       		final K key;
          V value;
          Node<K,V> next;
  ```

  

  - key 就是写入时的键。
  - value 自然就是值。
  - 开始的时候就提到 HashMap 是由数组和链表组成，所以这个 next 就是用于实现链表结构。
  - hash 存放的是当前 key 的 hashcode。
  - 最总存储键值对就是一个Node数组咯
  
  ### put函数
  
  ```java
  		public V put(K key, V value) {
          return putVal(hash(key), key, value, false, true);
      }
      final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                     boolean evict) {
          Node<K,V>[] tab; Node<K,V> p; int n, i;
        //判断table数组是否为空，以及table数组长度是否等于0
          if ((tab = table) == null || (n = tab.length) == 0)
            	//扩容，resize方法中如果table.length为0，即代表这是第一次初始化该hashmap，则用DEFAULT_INITIAL_CAPACITY(桶的默认大小默认16)初始化table的长度
              n = (tab = resize()).length;
        //根据当前 key 的 hashcode 定位到具体的桶中并判断是否为空，为空表明没有 Hash 冲突就直接在当前位置创建一个新桶即可
          if ((p = tab[i = (n - 1) & hash]) == null)
              tab[i] = newNode(hash, key, value, null);
          else {
              Node<K,V> e; K k;
            //如果hasp值相等，并且key相等，就覆盖当前的value
              if (p.hash == hash &&
                  ((k = p.key) == key || (key != null && key.equals(k))))
                  e = p;
              else if (p instanceof TreeNode)
                //如果已经转换成红黑树，就用红黑树的方式插入
                  e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
              else {
                //否则就是链表的形式，就将当前的 key、value封装成一个新节点写入到当前桶后面（形成链表）
                  for (int binCount = 0; ; ++binCount) {
                      if ((e = p.next) == null) {
                          p.next = newNode(hash, key, value, null);
                        //接着判断当前链表的大小是否大于预设的阈值默认0.75*16=12，大于时就要调用转换为红黑树的方法，此时不一定转换，还需进去treeifybin进行判断（判断table长度是否大于MIN_TREEIFY_CAPACITY=64）。
                          if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                              treeifyBin(tab, hash);
                          break;
                      }
                    //如果在遍历过程中找到 key 相同时直接退出遍历。
                      if (e.hash == hash &&
                          ((k = e.key) == key || (key != null && key.equals(k))))
                          break;
                      p = e;
                  }
              }
            //如果 e != null 就相当于存在相同的 key,那就需要将值覆盖。
              if (e != null) { // existing mapping for key
                  V oldValue = e.value;
                  if (!onlyIfAbsent || oldValue == null)
                      e.value = value;
                  afterNodeAccess(e);
                  return oldValue;
              }
          }
        //最后判断是否需要进行扩容。
          ++modCount;
          if (++size > threshold)
              resize();
          afterNodeInsertion(evict);
          return null;
      }
  
  ```
  
  ### get函数
  
  ```java
  		public V get(Object key) {
          Node<K,V> e;
          return (e = getNode(hash(key), key)) == null ? null : e.value;
      }
  
      /**
       * Implements Map.get and related methods.
       *
       * @param hash hash for key
       * @param key the key
       * @return the node, or null if none
       */
      final Node<K,V> getNode(int hash, Object key) {
          Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
        //table为空，未插入过数据，未初始化就直接返回null
          if ((tab = table) != null && (n = tab.length) > 0 &&
              (first = tab[(n - 1) & hash]) != null) {
            //检查是否是node链表或者红黑树中的头节点，是就直接返回
              if (first.hash == hash && // always check first node
                  ((k = first.key) == key || (key != null && key.equals(k))))
                  return first;
              if ((e = first.next) != null) {
                //根据是否是红黑树结点，区分链表以及红黑树的查找方式
                  if (first instanceof TreeNode)
                      return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                  do {
                      if (e.hash == hash &&
                          ((k = e.key) == key || (key != null && key.equals(k))))
                          return e;
                  } while ((e = e.next) != null);
              }
          }
          return null;
      }
  
  ```
  
  

**两个核心方法（get/put）可以看出 1.8 中对大链表做了优化，修改为红黑树之后查询效率直接提高到了 `O(logn)`。**

### resize函数

```java
final Node<K,V>[] resize() {
        Node<K,V>[] oldTab = table;
  			//获取旧table的长度
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
 			 //获取旧的扩容阈值
        int oldThr = threshold;
        int newCap, newThr = 0;
        if (oldCap > 0) {
        		//判断容器是否大于桶的个数的最大值
            if (oldCap >= MAXIMUM_CAPACITY) {
              //将下一个扩容的阀值调到最大，即无法在扩容
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
          //否则翻倍
          // 将新table长度赋值为旧table的2倍，
          // 判断旧table长度的二倍是否小于最大容量，且旧容量大于等于初始容量，
          // 以上判断成立则将新的扩容阀值赋值为旧的扩容阈值的二倍
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
  			//将旧table中的元素放到扩容后的newTable中
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                      //如果数组对应下标位置只有一个元素，对hashCade取余并根据结果直接放到newTable相应的位置
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                      //如果数组对应下标位置的元素是一个红黑树,则拆分红黑树放到newTable中
                        // 如果拆分后的红黑树元素小于6，则转化为链表
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                     //数组对应下标位置的元素是一个链表的情况
                    //根据(e.hash & oldCap)条件对链表进行拆分并放到newTable
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }
```

### treeifbin函数：

```java
final void treeifyBin(Node<K,V>[] tab, int hash) {
        int n, index; Node<K,V> e;
  //上面put函数提到过一下，这里还有一个限制条件，当table的长度小于MIN_TREEIFY_CAPACITY（64）时，只是进行扩容
        if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
            resize();
        else if ((e = tab[index = (n - 1) & hash]) != null) {
            TreeNode<K,V> hd = null, tl = null;
            do {
              // //将链表中的结点转换为树结点，形成一个新链表
                TreeNode<K,V> p = replacementTreeNode(e, null);
                if (tl == null)
                    hd = p;
                else {
                    p.prev = tl;
                    tl.next = p;
                }
                tl = p;
            } while ((e = e.next) != null); //将新的树结点链表赋给第index个桶
            if ((tab[index] = hd) != null)
                hd.treeify(tab);						//执行 TreeNode中的treeify()方法
        }
    }

```

### treeify与untreeify函数

```java
//将链表转化为红黑树
final void treeify(Node<K,V>[] tab) {
            TreeNode<K,V> root = null;
  					//遍历链表中的每一个TreeNode，当前结点为x
            for (TreeNode<K,V> x = this, next; x != null; x = next) {
                next = (TreeNode<K,V>)x.next;
                x.left = x.right = null;
             	 //对于第一个树结点，当前红黑树的root == null，所以第一个结点是树的根，设置为黑色         
                if (root == null) {
                    x.parent = null;
                    x.red = false;
                    root = x;
                }
                else {
                    K k = x.key;
                    int h = x.hash;
                    Class<?> kc = null;
										//从根结点开始遍历，寻找当前结点x的插入位置
                    for (TreeNode<K,V> p = root;;) {
                        int dir, ph;
                        K pk = p.key;
                       //如果当前结点的hash值小于根结点的hash值，方向dir = -1；
                        if ((ph = p.hash) > h)
                            dir = -1;
                      //如果当前结点的hash值大于根结点的hash值，方向dir = 1；
                        else if (ph < h)
                            dir = 1;
                      //如果x结点的key没有实现comparable接口，或者其key和根结点的key相等（k.compareTo(x) == 0）仲裁插入规则
                        else if ((kc == null &&
                                  (kc = comparableClassFor(k)) == null) ||
                                 (dir = compareComparables(kc, k, pk)) == 0)
                            dir = tieBreakOrder(k, pk);

                        TreeNode<K,V> xp = p;
                       //如果p的左右结点都不为null，继续for循环，否则执行插入
                        if ((p = (dir <= 0) ? p.left : p.right) == null) {
                            x.parent = xp;
                            if (dir <= 0)
                                xp.left = x;
                            else
                                xp.right = x;
                          //插入后进行树的调整，使之符合红黑树的性质
                            root = balanceInsertion(root, x);
                            break;
                        }
                    }
                }
            }
            moveRootToFront(tab, root);
        }

        /**
        红黑树转换成链表
         */
        final Node<K,V> untreeify(HashMap<K,V> map) {
            Node<K,V> hd = null, tl = null;
            for (Node<K,V> q = this; q != null; q = q.next) {
                Node<K,V> p = map.replacementNode(q, null);
                if (tl == null)
                    hd = p;
                else
                    tl.next = p;
                tl = p;
            }
            return hd;
        }
```

### 确定hash桶索引的位置

参考博客：https://blog.csdn.net/qq_42034205/article/details/90384772

```java
//方法一：
static final int hash(Object key) {   //jdk1.8 & jdk1.7
     int h;
     // h = key.hashCode() 为第一步 取hashCode值
     // h ^ (h >>> 16)  为第二步 高位参与运算  h右移16位
     return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
//方法二：
static int indexFor(int h, int length) {  //jdk1.7的源码，jdk1.8没有这个方法，但是实现原理一样的,在方法体中运用
     return h & (length-1);  //第三步 取模运算
}
//即hashCode()的低16位与高16位右移16位相异或。
```

**1. h >>> 16 是什么，有什么用?**

h是hashcode。h >>> 16是用来**取出h的高16**，(>>>是无符号右移)  如下展示

```java
0000 0100 1011 0011  1101 1111 1110 0001
 
>>> 16 
 
0000 0000 0000 0000  0000 0100 1011 0011
```

即保留后高位 16位，即左边的16位噢



讲到这里还要看一个方法indexFor，在jdk1.7中有indexFor(int h, int length)方法。jdk1.8里没有，但原理没变。下面看下1.7源码

1.8中用tab[(n - 1) & hash]代替但原理一样。(n是table长度)

static int indexFor(int h, int length) {
    return h & (length-1);
}
这个方法返回值就是**数组下标**。我们平时用map大多数情况下map里面的数据不是很多。这里与（length-1）相&,

但由于绝大多数情况下length一般都小于2^16即小于65536。所以return h & (length-1);结果始终是h的低16位与（length-1）进行&运算。如下例子（hashcode为四字节）

**例如1：为了方便验证，假设length为8。HashMap的默认初始容量为16**

length = 8;  （length-1） = 7；转换二进制为111；

假设一个key的 hashcode = 78897121 转换二进制：100101100111101111111100001，与（length-1）& 运算如下

```java
    0000 0100 1011 0011 1101 1111 1110 0001
 
&运算
 
    0000 0000 0000 0000 0000 0000 0000 0111
 
=   0000 0000 0000 0000 0000 0000 0000 0001 （就是十进制1，所以下标为1）
```



**当length=8时  下标运算结果取决于哈希值的低三位**

**当length=16时 下标运算结果取决于哈希值的低四位**

**当length=32时 下标运算结果取决于哈希值的低五位**

**当length=2的N次方， 下标运算结果取决于哈希值的低N位**

因为&和|都会使得结果偏向0或者1 ,并不是均匀的概念,所以用^。

#### hashMap：

#### 1. 结构

HashMap结构由**数组**加**链表(或红黑树)**构成。主干是Node<K,V>[]  table数组，Node<K,V>是HashMap的基本单位，而每个table中的元素Node可看位链表的头节点或者红黑树的头节点。当链表中的节点个数超过8时，会触发链表转为红黑树进行元素存储。 小于6又会触发由红黑树转为链表.

#### 2. 总结

HashMap中的每个键值对，通过对key的哈希值与table-1(即桶的数目-1)进行&运算，得到数组下标，进而确认该键值对所存储的位置(对应的那个桶)，插入的时候如果对应桶Node的hash为空，即当前桶为空，直接覆盖当前即可。若不为空，那么就要比较当前桶中的 key和key的hashcode 与写入的 key 是否相等，相等就赋值给，否则即存在相同相同hash值或者不同hash值与(桶的数目)table-1&运算后得到相同的数组下标（哈希冲突），然后呢就将当前的 key、value封装成一个新节点写入到当前桶的最后面（即链表的最后面），然后就是比较判断当前链表的大小是否大于预设的阈值默认0.75*16=12，大于时就要调用转换为红黑树的方法，此时不一定转换，还需进去treeifybin进行判断（判断table长度是否大于MIN_TREEIFY_CAPACITY=64）。

> 哈希冲突：哈希冲突也叫哈希碰撞，当对两个不同数进行hash函数计算后可能会得到相同的hash值，即存入数组下标相同，此时就发生了碰撞，hashMap使用链地址法存储具有相同hash值的元素。

除此之外，解决hash冲突的办法还有开放地址法（发生hash冲突，寻找下一块未被占用的存储地址）、再散列函数法（对求得的hash值再进行一遍hash运算）。那么就要比较当前桶中的 `key、key 的 hashcode` 与写入的 key 是否相等，相等就赋值给

**注意：HashMap是线程不安全，当多个线程进行put操作时，可能会造成put死循环。**

精力有限。。。留下几个问题后期再解决：

#### hashmap为什么线程不安全？

####  hashmap为什么数组长度一定是2的次方？

#### ConcurrentHashMap：



