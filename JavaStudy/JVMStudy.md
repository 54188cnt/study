# 一、清单

- [JVM 内存结构](JavaStudy/JVM/01-jvm-memory-structure.md)
- [HotSpot 虚拟机对象探秘](JavaStudy/JVM/02-hotspot-jvm-object.md)
- [垃圾收集策略与算法](JavaStudy/JVM/03-gc-algorithms.md)
- [HotSpot 垃圾收集器](JavaStudy/JVM/04-hotspot-gc.md)
- [内存分配与回收策略](JavaStudy/JVM/05-memory-allocation-gc.md)
- [JVM 性能调优](JavaStudy/JVM/06-jvm-performance-tuning.md)
- [类文件结构](JavaStudy/JVM/07-class-structure.md)
- [类加载的时机](JavaStudy/JVM/08-load-class-time.md)
- [类加载的过程](JavaStudy/JVM/09-load-class-process.md)
- [类加载器](JavaStudy/JVM/10-class-loader.md)

# 二、基础篇

JVM功能

- 即时编译(JIT)
- 内存管理
- 解释执行虚拟机指令

常见虚拟机

- HotSpot（Oracle JDK版，Open JDK版）
- GraalVM
- Dragonwell JDK（对高性能，高并发进行优化）
- Eclipse OpenJ9

## 字节码文件
查看字节码文件的工具 [jclasslib](https://github.com/ingokegel/jclasslib/releases) 

### 组成

- 基础信息
	魔数、字节码文件对应的Java版本号访问标识(public final等等)父类和接口
- 常量池
    保存了字符串常量、类或接口名、字段名主要在字节码指令中使用
- 字段
	当前类或接口声明的字段信息
- 方法
	当前类或接口声明的方法信息 <font color="#ff0000">字节码指令</font> 
- 属性
	类的属性，比如源码的文件名内部类的列表等






# 三、实战篇



# 四、高级篇



# 五、原理篇



# 六、面试篇

Q：为什么C++和C无法跨平台，而Java可以？
A：[回答](./JVM/Java为何可以跨平台.md) 








