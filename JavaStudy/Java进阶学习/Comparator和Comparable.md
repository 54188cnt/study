`Comparable` 接口和 `Comparator` 接口都是 Java 中用于<font color="#ff0000">排序</font>的接口，它们在实现类对象之间比较大小、排序等方面发挥了重要作用：

- `Comparable` 接口实际上是出自`java.lang`包 它有一个 `compareTo(Object obj)`方法用来排序
- `Comparator`接口实际上是出自 `java.util` 包它有一个`compare(Object obj1, Object obj2)`方法用来排序

一般我们需要对一个集合使用自定义排序时，我们就要重写`compareTo()`方法或`compare()`方法，当我们需要对某一个集合实现两种排序方式，比如一个 `song` 对象中的歌名和歌手名分别采用一种排序方法的话，我们可以重写`compareTo()`方法和使用自制的`Comparator`方法或者以两个 `Comparator` 来实现歌名排序和歌星名排序，第二种代表我们只能使用两个参数版的 `Collections.sort()`.

<span style="background:#affad1">Comparable: </span>
需要对要排序的类实现接口 `Comparable<T>` 并重写compareTo方法  
<span style="background:#fff88f">此时compareTo里面的参数的对象是要比较的对象，当前对象作为要插入的对象，返回值为正数表示当前对象应当往后插入，为负数往前插入。</span>  
```java
a.compareTo(b)
// a > b 返回 1
// a < b 返回 -1
// a = b 返回 0
```

<span style="background:#affad1">Comparator: </span>
排序的方法是 `compare` , 不需要修改原类  
<span style="background:#fff88f">compare 函数有两个参数，此时后者表示要比较的对象，前者表示当前对象，返回值大于0表示将当前对象往后插，返回值小于0表示将当前对象往前插。</span>  
实现方式有两种：
- 法1：实现 XxComparator 类并实现接口 `Comparator<T>` 
- 法2：匿名内部类( Lambda 表达式)

场景：<font color="#ff0000">Comparable需要需改原有类</font>