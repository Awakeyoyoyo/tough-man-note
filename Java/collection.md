

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