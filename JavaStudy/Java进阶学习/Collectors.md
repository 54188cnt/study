## 概览
`java.util.stream.Collectors` 是 “终端操作”之一，负责把 `Stream` 的元素聚合成各种容器或标量。  
官方分类：
- 归约（reduction） → 计数、求和、最值、平均值、汇总
- 分组（grouping） → 按条件拆分成 `Map<K, List<T>`
- 分区（partitioning） → 特殊分组，key 只有 true/false
- 拼接（joining） → 字符串拼接
- 收集到任意容器 → toList / toSet / toMap / toCollection(Supplier)

## 10个重要工厂方法
| 目的        | 代码示例                                                           | 返回类型                                            |
| :-------- | :------------------------------------------------------------- | :---------------------------------------------- |
| 转 List    | `Collectors.toList()`                                          | `List<T>`                                       |
| 转 Set     | `Collectors.toSet()`                                           | `Set<T>`                                        |
| 转指定集合     | `Collectors.toCollection(ArrayList::new)`                      | `C`                                             |
| 计数        | `Collectors.counting()`                                        | `Long`                                          |
| 求和        | `Collectors.summingInt/Long/Double(ToXxxFunction)`             | `Integer/Long/Double`                           |
| 平均值       | `Collectors.averagingInt/Long/Double(...)`                     | `Double`                                        |
| 最值        | `Collectors.maxBy(Comparator)`                                 | `Optional<T>`                                   |
| 拼接        | `Collectors.joining(", ","[","]")`                             | `String`                                        |
| 汇总统计      | `Collectors.summarizingInt(...)`                               | `IntSummaryStatistics`（含 count/sum/min/avg/max） |
| reduce 通用 | `Collectors.reducing(BinaryOperator)` / `reducing(id, fn, op)` | `Optional<T>` / `T`                             |

## 分组分区
### 普通分组
```java
// 一级分组(按城市)
Map<String, List<Person>> byCity = persons.stream()
    .collect(Collectors.groupingBy(Person::getCity));
    

// 二级分组(先按城市，再按性别)
Map<String, Map<String, List<Person>>> twoLevel = persons.stream()
    .collect(Collectors.groupingBy(Person::getCity,
        Collectors.groupingBy(Person::getGender)));
```

### 分组后做下游收集
```java
// 计数
Map<String, Long> cityCount =
    persons.stream()
        .collect(Collectors.groupingBy(Person::getCity,
            Collectors.counting()));
// 求和
Map<String, Integer> cityTotalAge =
    persons.stream()
        .collect(Collectors.groupingBy(Person::getCity,
            Collectors.summingInt(Person::getAge)));
// 最值
Map<String, Optional<Person>> oldestInCity =
    persons.stream()
        .collect(Collectors.groupingBy(Person::getCity,
            Collectors.maxBy(Comparator.comparingInt(Person::getAge))));
// 分区(只能分true/false)
Map<Boolean, List<Person>> isAdult = persons.stream()
    .collect(Collectors.partitioningBy(p -> p.getAge() >= 18));
```




