# 基础知识





## 位运算总结：

## 基础热身

#### 一、二进制

1.1 二进制是计算机采用的表示数字的方式, 每个数位上只有0和1；

1.2 任何整数一定可以采用二进制的方式表示, 小数的二进制这里不多说；

1.3 字节内部采用二进制方式记录数字, 一个字节分成八段, 每个分段有一个编号, 最右边分段编号是0, 向左逐渐递增

1.4 相邻分段之间有2倍关系, 某个分段的数字相当于2的编号次方, 如下

![da](../images/21.jpeg)

**二进制转十进制：**

把每个数位单独转换后把所有的转换结果求和

例：01001110 = 2^6 + 2^3 + 2^2 + 2^1 = 64 + 8 + 4 + 2 = 78

![da](../images/22.jpeg)

计算机字节里采用二进制补码记录数字

所有非负数整数, 补码和原码一样

# 原码、反码、补码

### 1. 原码

原码就是符号位加上真值的绝对值, 即用第一位表示符号, 其余位表示值. 比如如果是8位二进制:

> [+1]原 = 0000 0001
>
> [-1]原 = 1000 0001

第一位是符号位. 因为第一位是符号位, 所以8位二进制数的取值范围就是:

> [1111 1111 , 0111 1111]

即

> [-127 , 127]

原码是人脑最容易理解和计算的表示方式.

### 2. 反码

反码的表示方法是:

正数的反码是其本身

负数的反码是在其原码的基础上, 符号位不变，其余各个位取反.

> [+1] = [00000001]原 = [00000001]反
>
> [-1] = [10000001]原 = [11111110]反

可见如果一个反码表示的是负数, 人脑无法直观的看出来它的数值. 通常要将其转换成原码再计算.

### 3. 补码

补码的表示方法是:

正数的补码就是其本身

负数的补码是在其原码的基础上, 符号位不变, 其余各位取反, 最后+1. (即在反码的基础上+1)

> [+1] = [00000001]原 = [00000001]反 = [00000001]补
>
> [-1] = [10000001]原 = [11111110]反 = [11111111]补

对于负数, 补码表示方式也是人脑无法直观看出其数值的. 通常也需要转换成原码在计算其数值.

可见原码, 反码和补码是完全不同的. 既然原码才是被人脑直接识别并用于计算表示方式, 为何还会有反码和补码呢?

首先, 因为人脑可以知道第一位是符号位, 在计算的时候我们会根据符号位, 选择对真值区域的加减. (真值的概念在本文最开头). 但是对于计算机, 加减乘数已经是最基础的运算, 要设计的尽量简单. 计算机辨别"符号位"显然会让计算机的基础电路设计变得十分复杂! 于是人们想出了将符号位也参与运算的方法. 我们知道, 根据运算法则减去一个正数等于加上一个负数, 即: 1-1 = 1 + (-1) = 0 , 所以机器可以只有加法而没有减法, 这样计算机运算的设计就更简单了.

于是人们开始探索 将符号位参与运算, 并且只保留加法的方法. 首先来看原码:

计算十进制的表达式: 1-1=0

> 1 - 1 = 1 + (-1) = [00000001]原 + [10000001]原 = [10000010]原 = -2

如果用原码表示, 让符号位也参与计算, 显然对于减法来说, 结果是不正确的.这也就是为何计算机内部不使用原码表示一个数.

为了解决原码做减法的问题, 出现了反码:

计算十进制的表达式: 1-1=0

> 1 - 1 = 1 + (-1) = [0000 0001]原 + [1000 0001]原= [0000 0001]反 + [1111 1110]反 = [1111 1111]反 = [1000 0000]原 = -0

发现用反码计算减法, 结果的真值部分是正确的. 而唯一的问题其实就出现在"0"这个特殊的数值上. **虽然人们理解上+0和-0是一样的, 但是0带符号是没有任何意义的. 而且会有[0000 0000]原和[1000 0000]原两个编码表示0.**

于是补码的出现, 解决了0的符号以及两个编码的问题:

> 1-1 = 1 + (-1) = [0000 0001]原 + [1000 0001]原 = [0000 0001]补 + [1111 1111]补 = [0000 0000]补=[0000 0000]原

这样0用[0000 0000]表示, 而以前出现问题的-0则不存在了.而且可以用[1000 0000]表示-128:

> (-1) + (-127) = [1000 0001]原 + [1111 1111]原 = [1111 1111]补 + [1000 0001]补 = [1000 0000]补

-1-127的结果应该是-128, 在用补码运算的结果中, [1000 0000]补 就是-128. 但是注意因为实际上是使用以前的-0的补码来表示-128, 所以-128并没有原码和反码表示.(对-128的补码表示[1000 0000]补算出来的原码是[0000 0000]原, 这是不正确的)

使用补码, 不仅仅修复了0的符号以及存在两个编码的问题, 而且还能够多表示一个最低数. 这就是为什么8位二进制, 使用原码或反码表示的范围为[-127, +127], 而使用补码表示的范围为[-128, 127].

因为机器使用补码, 所以对于编程中常用到的32位int类型, 可以表示范围是: [-231, 231-1] 因为第一位表示的是符号位.而使用补码表示时又可以多保存一个最小值.

## 1.位运算概述

从现代计算机中所有的数据二进制的形式存储在设备中。即0、1两种状态，计算机对二进制数据进行的运算(+、-、*、/)都是叫位运算，即将符号位共同参与运算的运算。

看例子吧直接：

```
int a = 35;
int b = 47;
int c = a + b;
```

计算两个数的和，因为在计算机中都是以二进制来进行运算，所以上面我们所给的int变量会在机器内部先转换为二进制在进行相加：

```
35:  0 0 1 0 0 0 1 1
47:  0 0 1 0 1 1 1 1
————————————————————
82:  0 1 0 1 0 0 1 0
```

所以，相比在代码中直接使用(+、-、*、/)运算符，合理的运用位运算更能显著提高代码在机器上的执行效率。

## 2.位运算概览

| 符号 | 描述 | 运算规则                                                     |
| ---- | ---- | :----------------------------------------------------------- |
| &    | 与   | 两个位都为1时，结果才为1                                     |
| \|   | 或   | 两个位都为0时，结果才为0                                     |
| ^    | 异或 | 两个位相同为0，相异为1                                       |
| ~    | 取反 | 0变1，1变0                                                   |
| <<   | 左移 | 各二进位全部左移若干位，高位丢弃，低位补0                    |
| >>   | 右移 | 各二进位全部右移若干位，对无符号数，高位补0，有符号数，各编译器处理方法不一样，有的补符号位（算术右移），有的补0（逻辑右移） |

## 3.按位与运算符（&）

定义：参加运算的两个数据，按二进制位进行“与”运算。

运算规则：

```
0&0=0  0&1=0  1&0=0  1&1=1
```

#### 总结：两位同时为**1**，结果才为**1**，否则结果为**0**。

例如：`3&5` 即 0000 0011& 0000 0101 = 0000 0001，因此 3&5 的值得1。

-3&5。 1000 0011&0000 0101 ->0111 1101&0000 0101=0000 0101=5

注意：负数按**补码**形式参加按位与运算。



与运算的用途：

**1）清零**

如果想将一个单元清零，即使其全部二进制位为0，只要与一个各位都为零的数值相与，结果为零。

**2）取一个数的指定位**

比如取数 X=1010 1110 的低4位，只需要另找一个数Y，令Y的低4位为1，其余位为0，即Y=0000 1111，然后将X与Y进行按位与运算（X&Y=0000 1110）即可得到X的指定位。

**3）判断奇偶**

只要根据最未位是0还是1来决定，为0就是偶数，为1就是奇数。因此可以用`if ((a & 1) == 0)`代替`if (a % 2 == 0)`来判断a是不是偶数。

## 4.按位或运算符（|）[ ](https://www.cnblogs.com/yueshutong/p/11244534.html#3267481343)

定义：参加运算的两个对象，按二进制位进行“或”运算。

运算规则：

```
0|0=0  0|1=1  1|0=1  1|1=1
```

#### 总结：参加运算的两个对象只要有一个为1，其值为1。

例如：`3|5`即 0000 0011| 0000 0101 = 0000 0111，因此，`3|5`的值得7。　

注意：负数按**补码**形式参加按位或运算。

或运算的用途：

**1）常用来对一个数据的某些位设置为1**

比如将数 X=1010 1110 的低4位设置为1，只需要另找一个数Y，令Y的低4位为1，其余位为0，即Y=0000 1111，然后将X与Y进行按位或运算（X|Y=1010 1111）即可得到。

## 5.异或运算符（^）[ ](https://www.cnblogs.com/yueshutong/p/11244534.html#4028003129)

定义：参加运算的两个数据，按二进制位进行“异或”运算。

运算规则：

```
0^0=0  0^1=1  1^0=1  1^1=0
```

#### 总结：参加运算的两个对象，如果两个相应位相同为0，相异为1。

异或的几条性质:

1、交换律

2、结合律 (a^b)^c == a^(b^c)

3、对于任何数x，都有 x^x=0，x^0=x

4、自反性: a^b^b=a^0=a;

异或运算的用途：

**1）翻转指定位**

比如将数 X=1010 1110 的低4位进行翻转，只需要另找一个数Y，令Y的低4位为1，其余位为0，即Y=0000 1111，然后将X与Y进行异或运算（X^Y=1010 0001）即可得到。

**2）与0相异或值不变**

例如：1010 1110 ^ 0000 0000 = 1010 1110

**3）交换两个数**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
void Swap(int &a, int &b){
    if (a != b){
        a ^= b;
        b ^= a;
        a ^= b;
    }
}
// a=2,b=5 
a:0000 0010 b:0000 0101
//a=a^b=0000 0111=7
//b=b^a=0000 0010=2
//a=a^b=0000 0101=5
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

## 6.取反运算符 (~)[ ](https://www.cnblogs.com/yueshutong/p/11244534.html#909117224)

定义：参加运算的一个数据，按二进制进行“取反”运算。
运算规则：　

```
~1=0
~0=1
```

#### 总结：对一个二进制数按位取反，即将0变1，1变0。

异或运算的用途：

**1）使一个数的最低位为零**

使a的最低位为0，可以表示为：`a & ~1`。~1的值为 1111 1111 1111 1110，再按"与"运算，最低位一定为0。因为“ ~”运算符的优先级比算术运算符、关系运算符、逻辑运算符和其他运算符都高。

## 7.左移运算符（<<）[ ](https://www.cnblogs.com/yueshutong/p/11244534.html#1958716193)

定义：将一个运算对象的各二进制位全部左移若干位（左边的二进制位丢弃，右边补0）。

设 a=1010 1110，`a = a<< 2` 将a的二进制位左移2位、右补0，即得a=1011 1000。

若左移时舍弃的高位不包含1，则每左移一位，相当于该数乘以2。

## 8.右移运算符（>>）[ ](https://www.cnblogs.com/yueshutong/p/11244534.html#2076073887)

定义：将一个数的各二进制位全部右移若干位，正数左补0，负数左补1，右边丢弃。

例如：a=a>>2 将a的二进制位右移2位，左补0 或者 左补1得看被移数是正还是负。

操作数每右移一位，相当于该数除以2。





# java序列化与反序列化

### 序列化和反序列化的概念

**1、把对象转换为字节序列的过程称为对象的序列化**。

**2、把字节序列恢复为对象的过程称为对象的反序列化**。

对象的序列化主要有两种用途：

1） 把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中；

2） 在网络上传送对象的字节序列。

当两个进程在进行远程通信时，彼此可以发送各种类型的数据。无论是何种类型的数据，都会以二进制序列的形式在网络上传送。发送方需要把这个Java对象转换为字节序列，才能在网络上传送；接收方则需要把字节序列再恢复为Java对象。

​    **举个真实的案例：当我们需要使用的对象很复杂或者需要很长时间去构造，这时就会引入使用代理模式(Proxy)。例如：如果构建一个对象很耗费时间和计算机资源，代理模式(Proxy)允许我们控制这种情况，直到我们需要使用实际的对象。一个代理(Proxy)通常包含和将要使用的对象同样的方法，一旦开始使用这个对象，这些方法将通过代理(Proxy)传递给实际的对象。** 

解读：在微服务化盛行的今天，很多复杂的对象构造起来比较耗时，为了节省开支，某些公司将这部分复杂的对象先圈起来，写成服务起在远端B,并在调用端A端以代理（Proxy）的形式提供对服务的访问，这期间从B到A远程调的过程形成了Java对象序列化和反序列化的相关操作！

### jdk类库中序列化api

**java.io.ObjectOutputStream**

代表对象输出流，它的writeObject(Object obj)方法可对参数指定的obj对象进行序列化，把得到的字节序列写到一个目标输出流中。

**java.io.ObjectInputStream**

代表对象输入流，它的readObject()方法从一个源输入流中读取字节序列，再把它们反序列化为一个对象，并将其返回。

只有实现了Serializable和Externalizable接口的类的对象才能被序列化。Externalizable接口继承自 Serializable接口，实现Externalizable接口的类完全由自身来控制序列化的行为，而仅实现Serializable接口的类可以 采用默认的序列化方式 

​		**对象序列化包括如下步骤：**

　　1） 创建一个对象输出流，它可以包装一个其他类型的目标输出流，如文件输出流；

　　2） 通过对象输出流的writeObject()方法写对象。

　	**对象反序列化的步骤如下：**

　　1） 创建一个对象输入流，它可以包装一个其他类型的源输入流，如文件输入流；

　　2） 通过对象输入流的readObject()方法读取对象。

java代码实现：

```java
package com.awakeyo.serializable;

import java.io.Serializable;

/**
 * @author awakeyoyoyo
 * @className Person
 * @description TODO
 * @date 2020-03-31 13:53
 */
public class Person implements Serializable {
    private static final long serialVersionUID=13316311153L;
    private int age;
    private String name;
    private String sex;

    @Override
    public String toString() {
        return "Person{" +
                "age=" + age +
                ", name='" + name + '\'' +
                ", sex='" + sex + '\'' +
                '}';
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }
}

```



```java
package com.awakeyo.serializable;

import com.sun.org.apache.bcel.internal.generic.NEW;

import java.io.*;

/**
 * @author awakeyoyoyo
 * @className SerializePersonTest
 * @description TODO
 * @date 2020-03-31 13:57
 */
public class SerializePersonTest {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        Person person=new Person();
        person.setName("lqhao");
        person.setAge(21);
        person.setSex("男");
        ObjectOutputStream oo=new ObjectOutputStream(new FileOutputStream(new File("./person.txt")));
        oo.writeObject(person);
        System.out.println("Person对象序列化成果");
        oo.close();
        System.out.println("--------------------");
        ObjectInputStream ois=new ObjectInputStream(new FileInputStream("./person.txt"));
        Person person1=(Person) ois.readObject();
        System.out.println("Persion反序列化成果");
        System.out.println(person1.toString());
        ois.close();
    }

}
```

运行结果

![serialize](../images/serialize.jpg)

**serialVersionUID的作用**

serialVersionUID适用于Java的序列化机制。简单来说，Java的序列化机制是通过判断类的serialVersionUID来验证版本一致性的。在进行反序列化时，JVM会把传来的字节流中的serialVersionUID与本地相应实体类的serialVersionUID进行比较，如果相同就认为是一致的，可以进行反序列化，否则就会出现序列化版本不一致的异常，即是InvalidCastException。

**具体的序列化过程是这样的**：序列化操作的时候系统会把当前类的serialVersionUID写入到序列化文件中，当反序列化时系统会去检测文件中的serialVersionUID，判断它是否与当前类的serialVersionUID一致，如果一致就说明序列化类的版本与当前类版本是一样的，可以反序列化成功，否则失败。

serialVersionUID有两种显示的生成方式：     
一是默认的1L，比如：private static final long serialVersionUID = 1L;     
二是根据类名、接口名、成员方法及属性等来生成一个64位的哈希字段，比如：     
private static final long  serialVersionUID = xxxxL;

当实现java.io.Serializable接口的类没有显式地定义一个serialVersionUID变量时候，Java序列化机制会根据编译的Class自动生成一个serialVersionUID作序列化版本比较用，这种情况下，如果Class文件(类名，方法明等)没有发生变化(增加空格，换行，增加注释等等)，就算再编译多次，serialVersionUID也不会变化的

## 静态变量序列化

修改代码

```java
package com.awakeyo.serializable;

import java.io.Serializable;

/**
 * @author awakeyoyoyo
 * @className Person
 * @description TODO
 * @date 2020-03-31 13:53
 */
public class Person implements Serializable {
    private static final long serialVersionUID=13316311153L;
    private int age;
    private String name;
    private String sex;
    public static int staticVar = 10;

    @Override
    public String toString() {
        return "Person{" +
                "age=" + age +
                ", name='" + name + '\'' +
                ", sex='" + sex + '\'' +
                '}';
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }
}

```

```java
package com.awakeyo.serializable;

import com.sun.org.apache.bcel.internal.generic.NEW;

import java.io.*;

/**
 * @author awakeyoyoyo
 * @className SerializePersonTest
 * @description TODO
 * @date 2020-03-31 13:57
 */
public class SerializePersonTest {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        Person person=new Person();
        person.setName("lqhao");
        person.setAge(21);
        person.setSex("男");
        ObjectOutputStream oo=new ObjectOutputStream(new FileOutputStream(new File("./person.txt")));
        oo.writeObject(person);
        System.out.println("Person对象序列化成果");
        oo.close();
        System.out.println("--------------------");
        Person.staticVar=999;
        ObjectInputStream ois=new ObjectInputStream(new FileInputStream("./person.txt"));
        Person person1=(Person) ois.readObject();
        System.out.println("Persion反序列化成果");
        System.out.println(person1.toString());
        System.out.println("staticvar="+person1.staticVar);
        ois.close();
    }

}
```

最终结果

![serialize2](../images/serialize2.jpg)

最后的输出是 999，打印的 staticVar 是从读取的对象里获得的，应该是保存时的状态才对。之所以打印 999的原因在于序列化时，并不保存静态变量，这其实比较容易理解，序列化保存的是对象的状态，静态变量属于类的状态，**因此 序列化并不保存静态变量。**

## 父类的序列化与 Transient 关键字

##### 父类的序列化

要想将父类对象也序列化，就需要让父类也实现Serializable 接口。如果父类不实现的话的，就 需要有默认的无参的构造函数。在父类没有实现 Serializable 接口时，虚拟机是不会序列化父对象的，而一个 Java 对象的构造必须先有父对象，才有子对象，反序列化也不例外。所以反序列化时，为了构造父对象，只能调用父类的无参构造函数作为默认的父对象。因此当我们取父对象的变量值时，它的值是调用父类无参构造函数后的值。如果你考虑到这种序列化的情况，在父类无参构造函数中对变量进行初始化，否则的话，父类变量值都是默认声明的值，如 int 型的默认是 0，string 型的默认是 null。

##### Transient 关键字

作用是控制变量的序列化，在变量声明前加上该关键字，可以阻止该变量被序列化到文件中，在被反序列化后，transient 变量的值被设为初始值，如 int 型的是 0，对象型的是 null。

