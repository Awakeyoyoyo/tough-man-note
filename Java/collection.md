

# 集合



**java集合主要由2个体系组成。分别是Collection体系和Map体系，其中Collection和Map是两大体系的顶层接口。**

- Collection主要由三个子接口，分别是List(列表)、Set（集）、Queue( 队列)。其中，list、queue中的元素是有序并且重复的，而set中的元素是无需不可重复的。
- Map同属于java.util包中，是集合的一部分，但与Collection是相互独立的，没有任何关系。Map中都是以key-value的形式存在，其中key必须唯一，主要有HashMap、HashTable、TreeMap三个实现类

下面是结构图

![](/Users/awakeyoyoyo/Desktop/Java_Development_Note/images/WechatIMG1262.jpeg)







## **集合框架体系的组成**

集合框架体系是由Collection、Map(映射关系)和Iterator(迭代器)组成，各部分的作用如下所示。

### **[1]Collection体系中有三种集合：Set、List、Queue**

 Set(集)： 元素是无序的且不可重复。

 List(列表)：元素是有序的且可重复。

 Queue(队列)：封装了数据结构中的队列。

### **[2]Map体系**

 Map用于保存具有映射关系的数据，即key-value(键值对)。Map集合的key是唯一的，不可重复，而value可以重复。所以一个value可以对应多个key。

 Map体系除了常用类之外，还有Properties（属性类）也属于Map体系。

## **Collection的由来**

 由于数组中存放对象，对对象操作起来不方便。java中有一类容器，专门用来存储对象。

 集合可以存储多个元素,但我们对多个元素也有不同的需求

 多个元素,不能有相同的

 多个元素,能够按照某个规则排序

 针对不同的需求：java就提供了很多集合类，多个集合类的数据结构不同。但是，结构不重要，重要  的是能够存储东西,能够判断,获取.

把集合共性的内容不断往上提取,最终形成集合的继承体系---->Collection

并且所有的Collection实现类都重写了toString()方法.

//todo





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