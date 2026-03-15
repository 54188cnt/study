## 创建Optional对象
```java
private static final Optional<?> EMPTY = new Optional<>();
/**
如果value是null返回EMPTY, 否则返回of(value)
*/
public static <T> Optional<T> ofNullable(T value) {
	return value == null ? empty() : of(value);
}

public static <T> Optional<T> empty() {
	Optional t = (Optional<T>) EMPTY;
	return t;
}
/**
如果value是null会产生NullPointerException异常
*/
public static <T> Optional<T> of(T value) {
	return new Optional<>(value);
}
```

## map() 和 flatMap() 区别
`map` 和 `flatMap` 都是将一个函数应用于集合中的每个元素，但不同的是`map`返回一个<font color="#92cddc">新的集合</font>，`flatMap`是将<font color="#92cddc">每个元素都映射为一个集合，最后再将这个集合展平</font>。
在实际应用场景中，如果`map`返回的是数组，那么最后得到的是一个二维数组，使用`flatMap`就是为了将这个二维数组展平变成一个一维数组。
可以理解为 flatMap() 将 map() 的结果展开

## 常见操作

### 判断 value 是否为 null
```java
/**
* value是否为null
*/
public boolean isPresent() {
    return value != null;
}
/**
* 如果value不为null执行consumer.accept
*/
public void ifPresent(Consumer<? super T> consumer) {
   if (value != null) 
       consumer.accept(value);
}
```

### 获取 value
```java
/**
* Return the value if present, otherwise invoke {@code other} and return
* the result of that invocation.
* 如果value != null 返回value，否则返回other的执行结果
*/
public T orElseGet(Supplier<? extends T> other) {
    return value != null ? value : other.get();
}

/**
* 如果value != null 返回value，否则返回T
*/
public T orElse(T other) {
    return value != null ? value : other;
}

/**
* 如果value != null 返回value，否则抛出参数返回的异常
*/
public <X extends Throwable> T orElseThrow(Supplier<? extends X> exceptionSupplier) throws X {
    if (value != null) {
        return value;
    } else {
        throw exceptionSupplier.get();
    }
}
/**
* value为null抛出NoSuchElementException，不为空返回value。
*/
public T get() {
    if (value == null) {
        throw new NoSuchElementException("No value present");
    }
    return value;
}
```

### 过滤值
```java
/**
* 1. 如果是empty返回empty
* 2. predicate.test(value)==true 返回this，否则返回empty
*/
public Optional<T> filter(Predicate<? super T> predicate) {
    Objects.requireNonNull(predicate);
    if (!isPresent())
        return this;
    else
        return predicate.test(value) ? this : empty();
}
```

<font color="#ff0000">注意</font>：如果坚决不想看见 NPE，就不要用 of()、 get()、flatMap(..)。


