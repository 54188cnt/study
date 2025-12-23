## 1. 什么是 Record？

在 Java 中，我们经常需要编写一些只负责保存数据的类（比如 POJO、DTO、VO）。在传统写法中，即使只有两个属性，我们也得写一大堆样板代码：

- 私有字段（private final fields）
- 构造器（Constructor）
- Getter 方法
- `equals()` 和 `hashCode()`
- `toString()`

**Record 的本质**：它是一种特殊的 **类（Class）**，专门用于建模“不可变数据”。你只需要定义数据的组成，Java 编译器会自动为你生成上述所有的样板代码。

---

## 2. 怎么用？（基础语法）

### 传统写法 vs Record 写法

假设我们要定义一个“用户信息”对象：

**传统写法（冗长）：**

```java
public class User {
    private final String name;
    private final int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }

    @Override
    public boolean equals(Object o) { ... }
    @Override
    public int hashCode() { ... }
    @Override
    public String toString() { ... }
}
```

**Record 写法（一行搞定）：**

```java
public record User(String name, int age) { }
```

### 自动生成的内容

当你写下上面这行代码时，编译器自动帮你完成了：

1. **不可变字段**：生成 `private final String name` 和 `private final int age`。
    
2. **构造函数**：一个包含所有参数的全参构造器。
    
3. **Getter 方法**：注意，方法名不再是 `getName()`，而是直接叫 `name()` 和 `age()`。
    
4. **toString()**：打印类似 `User[name=张三, age=25]` 的清晰字符串。
    
5. **equals() & hashCode()**：基于属性值的逻辑判断。

---

## 3. 核心特性与限制

为了保证 Record 的简洁性和设计初衷，它有一些强制规则：

- <font color="#ff0000">不可变性</font>：所有字段默认都是 `final` 的，一旦创建就不能修改（Setter 方法不存在）。
    
- <font color="#ff0000">不可继承性</font>：Record 类隐式继承自 `java.lang.Record`，且它是 `final` 类。因此：
    - Record 不能继承其他类。
    - 其他类不能继承 Record。
    
- <font color="#ff0000">不能定义实例变量</font>：除了在括号里声明的组件，你不能在 Record 大括号里再写 `private int x;`。但你可以定义**静态变量**。
    
- <font color="#ff0000">嵌套Record</font>：可以将大 Record 拆分成多个小的嵌套 Record。

---

## 4. 进阶用法：自定义逻辑

虽然编译器会自动生成代码，但你依然可以根据需要进行定制。

### (1) 紧凑型构造函数 (Compact Constructor)

这是 Record 特有的语法，用于做**参数校验**，不需要重复写赋值语句。

```java
public record User(String name, int age) {
	// 与无参构造方法进行区别
    public User {
        if (age < 0) {
            throw new IllegalArgumentException("年龄不能为负数！");
        }
        // 不需要写 this.name = name，它会自动赋值
    }
}
```

### (2) 添加实例方法

可以像普通类一样为它添加业务方法：

```java
public record User(String name, int age) {
    public String getInfo() {
        return name + " is " + age + " years old.";
    }
}
```



