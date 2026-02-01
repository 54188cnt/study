# 一、Java基础概念
## 1.1 Java基本知识
> JDK是Java开发工具包; JRE是java运行环境  
> JDK = JVM + 核心类库 + 开发工具   
> JRE = JVM + 核心类库 + 运行工具  

## 1.2 注释和关键字
> 注释是代码中的非执行部分，用于解释代码的功能或目的。  
> 关键字是编程语言中预定义的保留字，具有特定含义，不能用作变量名。  

```
// 这是单行注释
/*  这是多行注释  */
/** 这是文档注释，用于生成文档 */

# 关键字
    if, else, for, while, return ...
```
## 1.3 字面量
> 整数，小数，字符串，字符，布尔型，空类型

| 特殊字符 | 含义                 |
|------|--------------------|
| \t   | 制表符（补齐字符串，长度为8的倍数） |
| \n   | 换行符                |

## 1.4 变量
> 变量是存储数据的命名空间，可以在程序中使用和修改。  
> 形式：数据类型 变量名 = 初始值;   
> 命名：变量名由字母、数字、下划线和美元符号组成，不能以数字开头，且不能使用关键字。  

注意事项： 
- 变量名区分大小写，且不能包含空格。  
- 变量名不能重复。  
- 使用前要赋值。  

## 1.5 计算机的存储规则
> 计算机使用二进制存储数据，所有数据都转换为0和1的形式存储。  

进制：
- 二进制：0b开头
- 八进制：0开头
- 十进制：不带前缀
- 十六进制：0x开头  

进制转换：
- 十进制转其他：除基取余法
- 其他转十进制：乘基取和法  

### 1.5.1 图片数据存储
> 图片数据是由像素点组成的，每个像素点包含颜色信息。  
> 灰度图像素点用一个字节表示，范围0 - 255。  
> 彩色图像素点用三个字节表示，，范围为0 ~ 255，分别表示红、绿、蓝三种颜色的强度。  

### 1.5.2 音频数据存储
> 音频数据是由采样点组成的，每个采样点包含音频信号的强度信息。  

### 1.5.1 视频数据存储
> 视频数据是由一系列连续的图像帧组成，每帧包含图像数据和时间戳。  

## 1.6 数据类型
### 1.6.1 基本数据类型
> 整型：byte(-128 ~ 127), short, int(default), long(定义的时候数据后面需要添加L) </br>
> 浮点型：float(定义的时候数据后面需要添加F), double(default) </br>
> 字符型：char </br>
> 布尔型：boolean </br>
> 大小关系：double > float > long > int > short > byte </br>

> 字符串型数据：String</br>

### 1.6.2 引用数据类型
> 除开基本数据类型外的所有数据类型都属于引用数据类型。</br>
> 凡是new关键字创建的对象都是引用数据类型。</br>
> 引用数据类型存储的是对象的地址值，而不是对象本身。  
> example:
> - 字符串：String
> - 数组：int[], String[], double[]
> - 类：自定义类


## 1.7 标识符
> 标识符是程序中用于标识变量、方法、类等的名称。</br>
> 命名规则：由字母、数字、下划线和美元符号组成，不能以数字开头，不能使用关键字，且区分大小写。</br>
> 小驼峰命名法(方法，变量)：首字母小写，后续单词首字母大写，如：myVariable </br>
> 大驼峰命名法(类名)：每个单词首字母大写，如：MyClass </br>
> 命名必须见名知意


## 1.8 键盘录入
> 键盘录入是通过控制台输入数据，使用Scanner类来实现。  
> 体系1：
> - nextInt()：读取整数
> - nextDouble()：读取小数
> - next()：读取字符串  
>> 体系1遇到空格、制表符或回车就会结束读取  
> 
> 体系2：
> - nextLine()：读取一行字符串，包括空格  
>> 体系2遇到回车就会结束读取，可以接收空格和制表符  
> 
> 注意：使用nextLine()时，前面如果有nextInt()或nextDouble()等方法，
> 需要先清除输入缓冲区的换行符，否则会导致读取不到数据。</br>
```java
// 步骤一：导包
import java.util.Scanner;

// 步骤二：创建Scanner对象
Scanner sc = new Scanner(System.in);

// 步骤三：使用Scanner对象的方法获取输入
int i = sc.nextInt(); // 获取整数

```

# 二、Java运算符
## 2.1 算术运算符(+ - * / %)
> 整数参与计算，结果只能得到整数。</br>
> 小数参与计算，结果不一定精确。</br>
> 除法运算中，整数除以整数结果为整数，小数除以整数结果为小数。</br>

> 隐式转换：小数参与计算时，整数会自动转换为小数。</br>
> - 自动类型提升：取值范围小的类型会自动转换为取值范围大的类型。</br>
> - byte,short,char参与运算时，会先转换为int类型，再进行运算。</br>
> 
> 强制转换：</br>
> - 取值范围大的数值赋值给取值范围小的数值无法直接赋值，必须进行强制转换</br>
> - 当值过大的时候强制转换给取值范围小的类型会导致数据丢失。</br>
> 
> 格式：数据类型 变量名 = (数据类型)值;</br>

> 字符串的 '+'
> - 字符串和其他类型相加时，其他类型会被转换为字符串，然后进行字符串拼接。</br>
> - 连续进行“+”操作时，从左到右逐个执行。</br>
> - 字符相加：字符会通过ASCII码表查询到对应数字再进行计算</br>
> ```java
> String str =  123 + 456 + "abc"; // 结果为"579abc"
> String str = '中' + "abc" + true; // 结果为"中abctrue"
> ```

## 2.2 自增自减运算符(++, --)
> 单独一行使用时在前在后效果相同</br>
```java
int a = 10;
int x = a++; // x = 10, a = 11
int y = ++a; // y = 12, a = 12
```

## 2.3 赋值运算符(= += -= *= /= %=)
> = 是赋值运算符，用于将右侧的值赋给左侧的变量。</br>
> a += b 相当于 a = a + b;</br>
> a -= b 相当于 a = a - b;</br>
> a \*= b 相当于 a = a * b;</br>
> a /= b 相当于 a = a / b;</br>
> a %= b 相当于 a = a % b;</br>
> 细节：+=,-=,*=,/=,%= 底层都隐藏了一个强制转换的过程</br>

## 2.4 关系运算符(== != > < >= <=)
> 成立返回true，不成立返回false。</br>
> == 与 = 是不同的，== 用于比较值是否相等，而 = 用于赋值。</br>
> 注意：在比较浮点数时，由于精度问题，可能会出现不准确的情况。</br>

## 2.5 逻辑运算符(&& || !)
> && 当两个操作数都为true时，结果才为true。当前一个为false，后者操作不进行</br>
> || 当两个操作数中有一个为true时，结果为true。当前一个为true，后者操作不进行</br>
> ! 用于取反操作，将true变为false，false变为true。</br>

## 2.6 位运算符(& | ^ ~ << >> >>>)
> & 按位与：两个二进制位都为1时结果为1，否则为0。</br>
> | 按位或：两个二进制位有一个为1时结果为1，否则为0。</br>
> ^ 按位异或：两个二进制位相同为0，不同为1。</br>
> ~ 按位取反：将二进制位0变为1，1变为0。</br>
> << 左移：将二进制位向左移动指定的位数，高位丢弃，低位补0。</br>
> \>> 右移：将二进制位向右移动指定的位数，低位丢弃，高位补符号位。</br>
> \>>> 无符号右移：将二进制位向右移动指定的位数，低位丢弃，高位补0。</br>

## 2.7 三元运算符(条件 ? 表达式1 : 表达式2)
> 条件为true时返回表达式1的值，条件为false时返回表达式2的值。</br>

# 三、判断和循环
## 3.1 分支结构
### 3.1.1 if语句
> 注：对一个布尔类型变量进行判断不建议用==，直接使用变量即可。</br>
> 格式1：</br>
> ```
> if(关系表达式){
>     语句体;
> }
> ```
> 格式2：</br>
> ```
> if(关系表达式){
>    语句体1;
> }else{
>    语句体2;
> }
> ```
> 格式3：</br>
> ```
> if(关系表达式1){
>     语句体1;
> }else if(关系表达式2){
>     语句体2;
> }
> ...
> else{
>     语句体n + 1;
> }

### 3.1.2 switch语句
> switch语句用于多分支选择，根据表达式的值执行对应的case语句。</br>
> 格式：</br>
> ```
> switch(表达式){
>     case 值1:
>         语句体1;
>         break;
>     case 值2:
>         语句体2;
>         break;
>     ...
>     default:
>         语句体n + 1;
>         break;
> }
> ```
> 注：</br>
> - case后面的值必须是常量(字面量)，不能是变量或表达式。</br>
> - case后面的值可以是整数、字符或字符串，但不能是浮点数，且不能重复。</br>
> - case的值可以有多个，用逗号分隔。</br>
> - default的位置可以在switch语句的任何位置，但通常放在最后。</br>

> switch新特性(->)：</br>
> - 可以使用箭头语法简化case语句(简化了break)。</br>
> - 若case里面会得到一个值，可以使用yield语句返回值。</br>
> ```
> switch(表达式){
>     case 值1 -> {
>         语句体1;
>     }
>     case 值2 -> {
>         语句体2;
>     }
>     ...
>     default -> {
>         语句体n + 1;
>     }
> }
> ```

## 3.2 循环结构
> continue语句用于跳过当前循环的剩余部分，直接进入下一次循环。</br>
> break语句用于终止循环，跳出循环体。</br>

### 3.2.1 for循环
> for循环用于重复执行一段代码，直到满足特定条件为止。</br>
> 格式：</br>
> ```
> for(初始化语句; 条件表达式; 更新语句){
>     语句体;          
> }
> ```

### 3.2.2 while循环
> while循环用于在满足条件的情况下重复执行一段代码。</br>
> 格式：</br>
> ```
> 初始化语句;
> while(条件判断语句){
>     循环体语句;
>     条件控制语句;
> }
> ```

### 3.2.3 do-while循环
> do-while循环与while循环类似，但至少执行一次循环体。</br>
> 格式：</br>
> ```
> 初始化语句;
> do{
>     循环体语句;
>     条件控制语句;
> }while(条件判断语句);
> ```
> 注：do-while循环先执行循环体，再判断条件。</br>

### 3.2.4 for-each循环
> for-each循环用于遍历数组或集合中的元素。</br>
> 格式：</br>
> ```
> for(数据类型 变量名 : 数组或集合){
>     语句体;
> }
> ```

# 四、数组
## 4.1 数组的概念
> 数组是存储同一类型数据的集合，可以通过索引访问每个元素。</br>
> 数组的长度在创建时确定，不能动态改变。</br>
> 数组的索引从0开始，最后一个元素的索引为长度-1。</br>

## 4.2 数值的定义与初始化
> 数组的定义格式：</br>
> ```
> 数据类型[] 数组名;
> ```
> 数组的静态初始化格式：</br>
> ```
> 数据类型[] 数组名 = new 数据类型[]{元素1, 元素2, ...};
> // 简化格式
> 数据类型[] 数组名 = {元素1, 元素2, ...}; 
> ```
> 数组的动态初始化格式：</br>
> 动态初始化是指在定义数组时只指定数组的长度，元素的值系统默认。</br>
> ```
> 数据类型[] 数组名 = new 数据类型[长度];
> ```
> 数组默认值：
> - 整型：0
> - 浮点型：0.0
> - 字符型：'\u0000' (空字符)
> - 布尔型：false
> - 引用类型：null

## 4.3 数值的地址值和元素访问
> 数组的地址值是数组在内存中的起始地址，可以通过数组名直接访问。</br>
> ```
> int[] arr = new int[]{1, 2, 3};
> System.out.print(arr); // 输出数组的地址值
> ```
> 通过索引访问数组元素， **<font color="red"> 索引值从0开始 </font>** 。</br>
> 数值的遍历：</br>
> ```
> // 普通遍历
> for(int i = 0; i < arr.length; i++){
>     System.out.println(arr[i]); // 访问数组元素
> }
> // arr.length 获取数组的长度
> 
> // for-each遍历
> for(int element : arr){
>     System.out.println(element); // 访问数组元素
> }
> ```

## 4.4 数组的内存分配
> 栈：方法调用时分配内存，方法结束后自动释放。  
> 堆：动态分配内存，手动管理内存，使用 **<font color="red"> new关键字 </font>** 创建对象。</br>
> 方法区：存储可以运行的class文件。</br>
> 本地方法栈：JVM使用操作系统功能的时候使用。</br>
> 寄存器：CPU使用的内存区域</br>

```
int arr1[] = {11, 12};
int arr2[] = arr1; // arr2指向arr1的内存地址
// 此时arr1和arr2指向同一块内存区域
```

## 4.5 二维数组
> 二维数组是数组的数组，可以看作一个表格或矩阵。</br>
> 二维数组的定义格式：</br>
> ```
> 数据类型[][] 数组名;
> ```
> 二维数组的静态初始化格式：</br>
> ```
> // 其中的一维数组长度可以不同
> 数据类型[][] 数组名 = new 数据类型[][]{{元素1, 元素2}, {元素3, 元素4}, ...};
> // 简化格式
> 数据类型[][] 数组名 = {{元素1, 元素2}, {元素3, 元素4}, ...};
> ```
> 二维数组的动态初始化格式：</br>
> ```
> 数据类型[][] 数组名 = new 数据类型[行数][列数];
> int[][] arr = new int[2][]; // 定义一个二维数组，第一维长度为2，第二维长度未指定
> // 相当于只创建了二维数组，但是其中的以为数组没有创建
> // 可以在后续对每一维进行初始化
> arr[0] = {1, 2, 3};
> arr[1] = {4, 5, 6};
> // 可以改变arr[0]指向的一维数组
> int[] arr1 = {7, 8, 9};
> arr[0] = arr1; // arr[0]现在指向arr1的一维数组
> // 此时打印arr中的元素为：7 8 9 4 5 6
> ```
> 二维数组的访问：</br>
> ```
> // 访问二维数组元素
> 数组名[行索引][列索引];
> // 遍历二维数组
> for(int i = 0; i < 数组名.length; i++){ // 遍历行
>     for(int j = 0; j < 数组名[i].length; j++){ // 遍历列
>         System.out.print(数组名[i][j] + " "); // 访问元素
>     }
>     System.out.println(); // 换行
> }
> ```


# 五、方法
## 5.1 方法的概念
> 方法是执行特定任务的代码块，可以重复使用。</br>
> 方法是程序中最小的执行单元。</br>

## 5.2 方法的格式
> 方法的定义格式：</br>
> ```
> 修饰符 返回值类型 方法名(参数列表){
>     方法体;
>     return 返回值; // 可选
> }

## 5.3 方法的重载
> 方法重载是指在 **<font color="red">同一个类</font>** 中定义多个同名但参数列表不同的方法。</br>
> 重载方法可以有不同的参数类型、参数个数或参数顺序。</br>
> 重载方法的返回值类型可以相同也可以不同，但不能仅通过返回值类型来区分。</br>
> 重载方法的调用是根据参数列表来决定的。</br>

## 5.4 方法的值传递
> Java中方法参数是值传递，即将实参的值复制给形参。</br>

# 六、面向对象基础
## 6.1 面向对象的概念
> 面向对象是一种编程范式，通过将数据和操作数据的代码封装在一起，形成对象来组织程序。</br>
> 面向对象的核心概念包括类、对象、继承、多态和封装。</br>
> 面向对象的优点包括代码重用、易于维护和扩展。</br>

## 6.2 类和对象
> 类是对象的模板或蓝图，定义了对象的属性和行为。</br>
> 对象是类的实例，具有类定义的属性和行为。</br>
> 类的定义格式：</br>
> ```
> 修饰符 class 类名 {
>     // 属性
>     数据类型 属性名;
>     // 方法
>     返回值类型 方法名(参数列表) {
>         方法体;
>         return 返回值; // 可选
>     }
> }
> ```
> 对象的创建格式：</br>
> ```
> 类名 对象名 = new 类名();
> // 使用对象
> 对象名.属性名 = 值; // 设置属性
> 对象名.方法名(参数); // 调用方法
> ```

## 6.3 封装
> 封装是将数据和操作数据的代码封装在一起，形成一个独立的单元。</br>
> 就是使用private关键字修饰类的属性和方法，提供公共方法来访问和修改属性。</br>
> 对每个属性提供getXxx()和setXxx()方法来访问和修改属性。</br>

## 6.4 就近原则和关键字this
> 就近原则是指在方法中访问属性时，优先访问局部变量，如果没有则访问类的属性。  
> 关键字this用于引用<font color="red">当前对象</font>的属性或方法。  
> 在方法中使用this可以区分局部变量和类的属性。  


## 6.4 构造方法
> 构造方法是用于创建对象时<font color="red">初始化对象</font>的特殊方法，名称与类名相同，没有返回值类型。</br>
> 构造方法可以有参数，用于初始化对象的属性。也可以无参数，属性值为默认值</br>
> 无参构造方法默认存在，如果定义了有参构造方法，则空参构造方法不再存在。</br>
> 实际中无参构造和带全部参数的构造方法都需要定义</br>

## 6.5 标准的Javabean类
> Javabean是符合特定规范的Java类，用于封装数据。</br>
> Javabean的规范包括：</br>
> - 类必须是public的，且有一个无参和带全部参数的构造方法。</br>
> - 属性必须是private的，且提供公共的getXxx()和setXxx()方法。</br>
>
> [//]: 类必须是可序列化的，即实现Serializable接口。  
> IDEA中快速生成Javabean：ptg插件或者 ALT + Insert</br>

## 6.6 对象的内存分配
> 对象在堆内存中分配内存空间，引用类型的变量存储的是对象的地址值。</br>
> 对象的内存分配过程：</br>
> 1. 使用new关键字创建对象。</br>
> 2. JVM在堆内存中分配足够的空间来存储对象的属性。</br>
> 3. 对象的地址值被存储在引用类型变量中。</br>
> 4. 当对象不再被引用时，JVM会自动进行垃圾回收，释放对象占用的内存空间。</br>

## 6.7 成员变量和局部变量
> 成员变量是类中定义的变量，属于对象或类的属性。  
> 局部变量是在方法或代码块中定义的变量，只在该方法或代码块内有效。  
> 
> | 区别 | 成员变量 | 局部变量 |
> |------|----------|----------|
> | 类中位置不同| 类中，方法外 | 方法内，代码块内 |
> | 生命周期 | 对象创建时分配内存，销毁时释放内存 | 方法调用时分配内存，方法结束后释放内存 |
> | 初始化值不同 | 有默认初始值 | 无默认初始值，必须手动初始化 |
> | 内存位置不同 | 堆内存 | 栈内存 |
> | 作用域 | 整个类 | 方法或代码块内 |

# 七、字符串
## 7.1 API
> API（Application Programming Interface）是应用程序编程接口，是一组预定义的函数、类和方法，用于与特定的软件或服务进行交互。</br>
> API帮助文档：
> - [java23 API帮助文档](https://docs.oracle.com/en/java/javase/23/docs/api/index.html "中文版")  
> - [本地位置](file:///D://Download/google/docs/api/index.html "英文版")  

## 7.2 String的概述
> String是Java中用于表示字符串的类，是 **<font color="red">不可变</font>** 的字符序列。  

## 7.3 String的创建
> String的创建方式有两种：</br>
> 1. 字面量创建：直接使用双引号括起来的字符序列
>   ```java
>   String str1 = "Hello, World!";
>   ```
> 2. 使用new关键字创建：使用String类的构造方法
>   ```java
>   String str2 = new String("Hello, World!");
>   char[] chars = {'H', 'e', 'l', 'l', 'o'};
>   String str3 = new String(chars); // 使用字符数组创建字符串
>   byte[] bytes = {72, 101, 108, 108, 111}; // H e l l o的ASCII码
>   String str4 = new String(bytes); // 使用字节数组创建字符串
>   ```
> 
> 注意：  
> - 使用new关键字创建的字符串对象会在堆内存中分配空间，而字面量创建的字符串会在字符串常量池中分配空间。
> - 通常采用字面量创建字符串，因为它更简洁且更节省空间

> 内存分配：  
> - 字符串常量池(StringTable 串池)：存储字面量创建的字符串，避免重复创建相同内容的字符串。(JDK7开始，字符串常量池移到了堆内存中)  
> - 堆内存：存储使用new关键字创建的字符串对象。

## 7.4 String的常用方法
> 比较字符串：  
> - equals(String  anotherString)：比较字符串内容是否相同，返回true或false。
> - equalsIgnoreCase(String anotherString)：比较字符串内容是否相同，忽略大小写。
> - ==：基本数据类型比较<font color="red">值</font>是否相等，引用类型比较<font color="red">地址值</font>是否相等。
> 
> 注：键盘录入的字符串是通过new关键字创建的。  
> ```
> String str1 = "abc";
> Scanner sc = new Scanner(System.in);
> String str2 = sc.next(); // 键盘录入的字符串
> System.out.println(str1 == str2); // false，因为str2是通过new创建的
> ```
> 常见方法：  
> - charAt(int index)：返回指定索引处的字符。  
> - length(): 返回字符串的长度。  
> - substring(int beginIndex)：返回从指定索引开始到字符串末尾的子字符串。  
> - substring(int beginIndex, int endIndex)：返回从指定起始索引到结束索引的子字符串。  
> - replace(char oldChar, char newChar)：返回替换字符串中的指定字符后新的字符串。也可以是字符串进行替换。  
> - valueOf(Object obj)：将对象转换为字符串，参数也可以是基本数据类型。
> - contains(CharSequence sequence)：判断字符串是否包含指定的字符序列。

## 7.5 StringBuilder类
> StringBuilder是一个可变的字符序列，用于高效地操作字符串。  
> StringBuilder的创建方式：  
> ```
> StringBuilder sb = new StringBuilder(); // 创建一个空的StringBuilder
> StringBuilder sb = new StringBuilder("Hello, World!"); // 创建一个包含初始内容的StringBuilder
> ```
> 
> 常用方法：</br>
> - append(String str)：在字符串末尾追加内容。
> - reverse()：将字符串反转。
> - length(): 返回字符串的长度。
> - toString()：将StringBuilder转换为String。
> 
> 注意：  
> - 直接打印StringBuilder对象会输出字符串内容，而不是地址值(与String区别)。
> - StringBuilder是线程不安全的，如果在多线程环境中使用，可能会导致数据不一致。
>
> 链式编程：  
> 定义：依赖前一个方法的结果继续调用下一个方法。  
> 使用场景：字符串的<font color="red">拼接以及反转</font>等操作。

## 7.6 StringJoiner类
> StringJoiner是一个用于连接字符串的类，可以指定分隔符、前缀和后缀。  
> 构造方法：  
> ```
> StringJoiner sj = new StringJoiner(String delimiter, String prefix, String suffix);
> StringJoiner sj = new StringJoiner(String delimiter); 
> ```
> 创建方式：  
> ```
> StringJoiner sj = new StringJoiner(", ", "[", "]"); // 分隔符为逗号，前缀为[，后缀为]
> sj.add("Hello").add("World"); // 添加字符串
> String result = sj.toString(); // 获取连接后的字符串
> System.out.println(result); // 输出结果：[Hello, World]
> ```
> 注意：
> - length()：返回连接后的字符串长度(包括添加的字符串总长度和开始结束以及定界符的长度)。
> - add(String str)：添加字符串到连接器中。

## 7. 7 字符串拼接底层原理
> 字符串拼接使用StringBuilder类来实现，避免了频繁创建新的字符串对象。  
> 当使用“+”进行字符串拼接时，编译器会自动将其转换为StringBuilder的append()方法调用。  
> 拼接原理：
> - 如果没有变量参与会复用串池中的字符串
> - 如果有变量参与会在栈中创建一个新的StringBuilder对象

# 八、集合基础
## 8.1 集合的基本使用
> 集合是Java中用于存储一组对象的容器，可以动态地添加、删除和访问元素。  
> 集合与数组的区别：  
> 
> | 特点 | 数组 | 集合 |  
> |------|------|------|  
> | 大小 | 固定大小 | 动态大小 |  
> | 存储类型 | 只能存储同一类型 | 可以存储不同类型(一般情况不能存基本数据类型) |  
> 
> 集合的分类：
> - List：有序集合，允许重复元素。常用实现类有ArrayList、LinkedList等。
> - Set：无序集合，不允许重复元素。常用实现类有HashSet、TreeSet等。
> - Map：键值对集合，允许通过键快速访问值。常用实现类有HashMap、TreeMap等。

## 8.2 ArrayList
> ArrayList是Java中最常用的动态数组实现类，属于List接口的实现类。
> 构造方法：
> ```
>  ArrayList< T> list = new ArrayList<>();  // 创建一个空的ArrayList
> ```
> 
> 常用方法：
> - add(Type element)：添加元素到ArrayList的末尾，返回true/false。
> - remove(int index)：删除指定索引处的元素，返回被删除的元素。
> - remove(Object element)：删除指定元素，返回是否成功。
> - get(int index)：获取指定索引处的元素，返回该元素。
> - set(int index, Type element)：设置指定索引处的元素，返回被替换的元素。
> - size()：返回ArrayList的大小，即元素个数。
> 
> 基本数据对应的包装类：  
> 
> | 基本数据类型 | 包装类 |
> |----------------|--------|
> | byte           | Byte   |
> | short          | Short  |
> | int            | Integer|
> | long           | Long   |
> | float          | Float  |
> | double         | Double |
> | char           | Character|
> | boolean        | Boolean|
> 注意：重点记忆int 和 char的包装类  

# 九、面向对象进阶
## 9.1 static
> static修饰符用于定义类的静态成员，包括静态变量和静态方法。
> 静态变量：  
> - 静态变量在类加载时分配内存(堆中的静态区)，优先于对象出现。
> - <font color="red">属于类</font>而不是对象，可以通过<font color="red">类名</font>直接访问。
> 
> 静态方法：
> - 静态方法可以通过<font color="red">类名</font>直接调用。
> - 多用在测试类和工具类(帮我们做事情的类)中，很少在Javabean(描述一类事物的类)中使用。
> - 静态方法不能访问非静态成员变量和方法，因为非静态成员属于对象，而静态方法属于类。
>
> 注意：
> - 工具类需要见名知意，且要私有化构造方法
> - 静态方法<font color="red">只能</font>访问静态变量和静态方法
> - 非静态方法可以访问静态变量和静态方法，也可以访问非静态变量和非静态方法
> - 静态方法中<font color="red">没有this关键字</font>，因为静态方法不属于任何对象，而this关键字指向当前对象。

## 9.2 继承
### 9.2.1 继承的概念
> 继承是面向对象编程中的一个重要特性，用于创建一个新类(子类)从现有类(父类)继承属性和方法。  
> Java提供的关键字是extends，用于表示继承关系。  
> 何时使用：当类与类之间存在相同内容且满足子类是父类的一个特例时，可以使用继承。  
> 继承的好处：
> - 代码复用：子类可以继承父类的属性和方法，减少代码重复。
> - 逻辑清晰：通过继承可以建立类之间的层次结构，使代码更易于理解和维护。
> - 多态支持：继承是实现多态的基础，可以通过父类引用指向子类对象。
> - 增强可扩展性：可以通过继承来扩展现有类的功能，而不需要修改原有代码。
> 
> 继承的格式：```public class 子类名 extends 父类名 {}```  
> 继承后子类的特点：
> - 子类拥有父类的所有<font color="red">非私有</font>属性和方法。
> - 子类可以添加自己的属性和方法。
> - 子类可以重写父类的方法(覆盖父类方法)，实现自己的逻辑。
> 
> 子类可以继承父类的哪些：
> - 构造方法：无法继承父类的构造方法
> - 成员变量：可以继承父类的所有成员变量(私有的无法调用)
> - 成员方法：可以继承父类的非私有成员方法，但无法继承私有方法。
> 
> 注意：Java只支持单继承，即一个类只能继承一个父类，但支持多层继承(父类的子类可以继续继承父类)。

### 9.2.2 继承中成员变量访问特点
> 子类继承父类后，子类可以访问父类的非私有成员变量和方法，但不能访问私有成员变量和方法。  
> 就近原则：谁离得近就用谁(现在局部位置找，再在本类成员找，父类成员找，逐级往上找)。  

### 9.2.3 继承中成员方法访问特点
> 就近原则：子类方法优先访问子类的成员方法，如果子类没有则访问父类的成员方法。 
> 方法的重写：
> - 子类可以重写父类的方法，重写后子类的方法会覆盖父类的方法。
> - 重写方法必须与父类方法具有<font color="red">相同的</font>方法名、参数列表和返回类型。
> - 重写的方法需要在方法前加上<font color="red">@Override</font>注解，表示这是一个重写方法。
> 
> 注意：  
> 子类重写方法的访问修饰符必须与父类方法的修饰符相同，或者更宽松（如protected可以变为public，但不能变为private）。  
> 重写方法的名称、形参列表必须与父类中的一致。  
> 子类重写父类方法时，返回值类型子类必须小于等于父类。  
> <font color="red">重写的方法尽量和父类保持一致</font>。  
> 只有被添加到[虚方法表](https://blog.csdn.net/ouhexie/article/details/141749123)中的方法才能被重写。  
> 
> 小tips: 当子类重写父类的方法时是在父类方法的基础上新增功能，而不是完全替换父类方法的功能。
> 此时可以使用super关键字调用父类的方法，然后再加入新增代码即可。

### 9.2.4 继承中构造方法的访问特点
> 子类的构造方法会隐式调用父类的无参构造方法，如果父类没有无参构造方法，则需要在子类构造方法中显式调用父类的有参构造方法。  
> 子类初始化之前，一定要调用父类的构造方法完成父类数据空间的初始化。  
> 子类构造方法<font color="red">第一行语句默认都是```super()```</font>，表示调用父类的无参构造方法。即使不写也存在，且必须在第一行。  
> 如果要调用父类的有参构造方法，需要<font color="red">手动</font>使用```super(参数)```来显式调用。

### 9.2.5 this, super关键字总结
> this关键字用于引用当前对象的成员变量和方法。
> - 在构造方法中可以使用```this```调用其他构造方法，必须放在第一行。
> - 但是此时不会在默认调用```super()```，需要手动调用父类的构造方法。
>
> super关键字用于访问父类的成员变量和方法。
> - 在子类中可以使用```super.成员变量```或```super.方法()```来访问父类的成员。
> - 在子类构造方法中可以使用```super(参数)```来显式调用父类的有参构造方法。
> - 注意：super关键字只能在子类中使用，不能在父类中使用。

## 9.3 多态
> 概念：对象的多态性是指同一个方法在不同对象上表现出不同的行为。  
> 多态的实现方式：
> 1. 继承：子类继承父类，重写父类的方法。
> 2. 方法重写：子类重写父类的方法，实现自己的逻辑。
> 3. 父类引用指向子类对象：使用父类类型的引用变量指向子类对象。
> 4. 方法调用：通过父类引用调用子类重写的方法，实现多态效果。
> 
> 方式：
> ```java
> 父类类型 变量名 = new 子类类型();
> ```
> 好处：使用父类型作为参数可以接受所有子类类型的对象，增强了代码的灵活性和可扩展性。
> 坏处：不能访问子类的特有功能。

> 多态调用成员特点：
> - 成员变量：编译看左边，运行也看左边
> - 成员方法：编译看左边，运行看右边(实际调用的是子类的重写方法)

> 优势与弊端：  
> - 优势：可以通过父类引用调用子类的重写方法，实现代码的灵活性和可扩展性。
> - 弊端：编译时无法确定调用哪个子类的方法，可能导致运行时错误。
> - 解决1：强制转换。使用```(子类类型)父类引用```进行强制类型转换，确保父类引用指向的对象确实是子类类型。
> - 解决2：使用instanceof关键字判断对象类型，确保安全转换。
> ```
> 父类类型 父类引用 = new 子类类型();
> 子类类型 变量名 = (子类类型) 父类引用; // 强制转换
> 变量名.方法(); // 调用子类方法
> 
> if(父类引用 instanceof 子类类型 变量名) {
>     变量名.方法(); // 调用子类方法
> }
> ```

## 9.4 包和final关键字
> 包名规则：公司域名反写 + 包的作用  
> 使用其他类时，需要使用<font color="red">全类名</font>(包名 + 类名)来引用。  
> 规则：
> - 使用同一个包中的类或者java.lang包中的类不需要导包
> - 使用其他包中的类需要导入包
> - 两个不同包的同名类需要使用全类名来区分
> 导包格式：```import 包名.类名;```

> final关键字的作用：
> - 修饰类：表示该类不能被继承，不能有子类。  
> - 修饰方法：表示该方法不能被重写，子类不能覆盖父类的该方法。  
> - 修饰变量：表示该变量是<font color="red">常量</font>，不能被修改(只能赋值一次)，且必须<font color="red">在声明时或构造方法中初始化</font>。  
> 
> 常量：
> - 一般作为系统的配置文件，方便维护，提高代码可读性。
> - 常量是指在程序运行过程中不会改变的值。
> - 常量的命名规则：通常使用大写字母(每个单词全部大写)和下划线(单词之间)分隔，如```MAX_VALUE```。
> - 细节：
>   - 修饰基础数据类型的变量时，表示该变量的值不能被修改；
>   - 修饰引用类型的变量时，表示该引用不能指向其他对象(地址值不能发生改变)，但对象本身的内容可以修改。

## 9.5 权限修饰符和代码块
> 权限修饰符用于控制类、方法和变量的访问权限。Java中有四种权限修饰符：public、protected、default(无修饰符)和private。   
> 
> |    修饰符     | 同一个类中 | 同一个包中其他类 | 不同包下的子类 | 不同包下的无关类 |
> |:----------:|:----------:|:----------------:|:---------------:|:----------------:|
> |   public   |  可以访问  |     可以访问     |    可以访问     |     可以访问     |
> | protected  |  可以访问  |     可以访问     |    可以访问     |    不可以访问    |
> |  default   |  可以访问  |     可以访问     |   不可以访问    |    不可以访问    |
> |  private   |  可以访问  |    不可以访问    |   不可以访问    |    不可以访问    |
> 多数情况下只使用private 和 public修饰符。  

> 代码块：  
> - 局部代码块(如今不咋使用，节省内存)：在方法或代码块中定义的代码块，用于限制变量的作用域，通常用于临时变量的定义和使用。
> - 构造代码块(渐渐淘汰了，不够灵活)：在构造方法执行前执行，通常用于初始化对象的属性(抽取多个构造方法共有代码)，
> <font color="red">优先于</font>构造方法执行。
> - 静态代码块：使用static修饰的代码块，在类加载时执行一次(也只执行一次)，通常用于初始化<font color="red">静态变量</font>。  

## 9.6 抽象类和抽象方法
> 抽象方法：将共性的行为(方法)抽取到父类之后，由于每一个子类的实现方式不同，
> 所以父类无法提供具体的实现，该方法就可以定义为抽象方法。  
> 抽象类：包含抽象方法的类称为抽象类，使用abstract关键字修饰。  
> 格式：  
> ```java
> public abstract class 类名{} // 抽象类
> public abstract 返回值 方法名(); // 抽象方法
> ```
> 注意：  
> - 抽象类不能被实例化(不能创建对象)，只能被继承。
> - 抽象类中不一定有抽象方法，但如果有抽象方法，则必须是抽象类。
> - 抽象类可以有构造方法。
> - 抽象类的子类<font color="red">必须实现所有</font>抽象方法，除非子类也是抽象类。  
> - 抽象方法可以强制子类按照规定格式实现这一方法。

## 9.7 接口
> 接口是Java中一种特殊的抽象类，用于定义一组方法的规范，接口中的方法没有具体实现。  
> 接口是一种规则，对行为进行抽象。  
> 接口的定义格式：```public interface 接口名 {}```  
> 接口不可以实例化。  
> 接口和类之间是实现关系，通过implements关键字表示。```public class 类名 implements 接口名 {}```  
> 接口的子类(实现类):要么重写接口中所有方法，要么是抽象类。  
> 注意：  
> - 接口和类的实现关系可以是单实现，也可以多实现。  
> ```public class 类名 implements 接口1, 接口2 {}```
> - 实现类还可以继承一个类的同时实现多个接口。  
> ```public class 类名 extends 父类 implements 接口1, 接口2 {}```

> 接口中成员的特点：  
> - 成员变量：接口中的成员变量默认是public static final的，即常量。
> - 构造方法：接口中没有构造方法，因为接口不能被实例化。
> - 成员方法：接口中的方法默认是public abstract的，即抽象方法。

> 接口和类之间的关系：
> - 类和类的关系：继承关系，只能单继承，但是可以多层继承。
> - 类和接口的关系：实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现多个接口。
> - 接口和接口的关系：继承关系，可以单继承，也可以多继承。

> 接口新特性：  
> - 默认方法：接口中可以定义默认方法，使用default关键字修饰。  
>   格式：``` public default 返回值类型 方法名(参数列表) {} ```
>   - 默认方法不是抽象方法，所以不被强制重写。如果要被重写，重写时去掉default关键字。  
>   - public可以省略，default不可以省略。  
>   - 如果实现了多个接口，且这些接口中有同名的默认方法，则需要在实现类中重写该方法，并使用super关键字调用指定接口的默认方法。  
>   ```接口名.super.方法名(参数);```
> - 静态方法：接口中可以定义静态方法，使用static关键字修饰。  
>   格式：```public static 返回值类型 方法名(参数列表) {}```
>   - 静态方法只能通过接口名调用，不能通过实现类名或者对象名调用。
>   - public可以省略，static不可以省略。
>   - 静态方法不能被重写，因为静态方法属于接口本身，而不是实现类。
> - 私有方法：接口中可以定义私有方法，使用private关键字修饰。  
>   格式1(给默认方法服务)：```private 返回值类型 方法名(参数列表) {}```  
>   格式2(给静态方法服务)：```private static 返回值类型 方法名(参数列表) {}```  
> - 接口多态：接口的多态是指通过接口引用指向<font color="red">实现类对象</font>，调用实现类的方法。

> 接口适配器：  
> - 接口适配器是一种设计模式，用于简化接口的使用。
> - 场景：当接口中有多个方法，但只需要使用其中的部分方法时，可以使用接口适配器。
> - 实现方式：创建一个<font color="red">抽象类</font>实现接口，并提供默认实现(空方法)，然后继承该抽象类并重写需要的方法。
> - 命名规范：通常是 **接口名 + Adapter**，如```MyInterfaceAdapter```。

## 9.8 内部类
内部类是定义在另一个类内部的类，可以访问外部类的成员变量和方法(包括私有)。   
外部类访问内部类成员必须要创建对象。  
场景：B类表示的事物是A类的一个特例，且B类单独存在没有意义。  

### 9.9.1 成员内部类
> 写在成员位置的，属于外部类成员。  
> 可以被修饰符修饰：private, protected, public, default(无修饰符)，static(静态内部类)  
> JDK16后可以在成员内部类内部定义静态方法和静态变量。  
> 获取成员内部类对象方式：  
> - 外部类编写方法，对内提供内部对象(内部类被private修饰时)  
> - 直接创建```外部类名.内部类名 对象名 = 外部类对象(new 外部类名).内部类对象(new 内部类名);```  
> 
> 外部类成员变量和内部类成员变量重名时，在内部类如何访问：  
> > Outer.this 表示外部类对象，Outer.this.变量名表示访问外部类的成员变量。

### 9.9.2 静态内部类
> 静态内部类是定义在外部类中的静态类，可以直接通过外部类名访问。  
> 静态内部类<font color="red">不能访问</font>外部类的非静态成员变量和方法，但可以访问外部类的静态成员变量和方法。  
> 创建静态内部对象格式：```外部类名.静态内部类名 对象名 = new 外部类名.静态内部类名();```  
> 调用静态方法格式：```外部类名.静态内部类名.方法名();```

### 9.9.3 局部内部类
> 将内部类定义在方法里面的类就是局部内部类，类似于方法里的局部变量。  
> 外界无法直接使用局部内部类，需要在方法内部创建对象并使用。  
> 该类可以直接访问外部类成员，也可以访问方法内的局部变量

### 9.9.4 匿名内部类
> 格式：
> ``` java
> new 类名或者接口名(){
>     重写方法;
> };
> ```
> 注意：
> - 包含了继承或实现，方法重写，创建对象。
> - 整体就是一个类的子类对象或者接口的实现类对象。
> - 分号不能忘记写了。
>
> 应用场景：
> - 方法的参数是接口或者类时。
> - 以接口为例，可以传递这个接口的实现类对象。
> - 如果实现类只要使用一次，就可以用匿名内部类简化代码。
>

# 十、GUI编程
## 10.1 JFrame
> JFrame是Java Swing库中的一个类，用于创建窗口应用程序。  
> 常用设置：  
> - setSize(int width, int height)：设置窗口的大小。  
> - setVisible(boolean visible)：设置窗口是否可见(<font color="red">一般放在末尾</font>)。  
> - setTitle(String title)：设置窗口的标题。  
> - setAlwaysOnTop(boolean alwaysOnTop)：设置窗口是否 AlwaysOnTop。  
> - setLocationRelativeTo(Component c)：设置窗口相对于某个组件的位置(通常null)。  
> - setDefaultCloseOperation(int operation)：设置窗口关闭时默认的操作。  
>   - DO_NOTHING_ON_CLOSE(0)：什么都不做。  
>   - HIDE_ON_CLOSE(1)：隐藏窗口(<font color="red">默认</font>)。  
>   - DISPOSE_ON_CLOSE(2)：销毁窗口。  
>   - EXIT_ON_CLOSE(3)：退出程序。  
> - setJMenuBar(JMenuBar menuBar)：设置菜单栏。  
> - setLayout(LayoutManager layout)：设置布局管理器，取消默认布局，使用自定义布局(方便使用XY轴添加组件)。设置参数null。  
> - setResizable(boolean resizable): 设置窗口是否可改变大小。
> - getContentPane()：获取内容面板(获取隐藏容器)。
> - getContentPane.removeAll()：删除所有图片。  
> - getContentPane.repaint()：刷新界面。  

## 10.2 JMenuBar/ JMenu/ JMenuItem
> JMenuBar是Java Swing库中的一个类，用于创建菜单栏。  
> JMenu是Java Swing库中的一个类，用于创建菜单(功能)。  
> JMenuItem是Java Swing库中的一个类，用于创建菜单项。  
> 菜单制作步骤：  
> 1. 创建菜单栏对象。
> 2. 创建菜单对象。
> 3. 创建菜单项对象。
> 4. JMenuItem放在JMenu中，JMenu放在JMenuBar中。
> 
> 注：JMenu里面可以添加其他JMenu。  

## 10.3 图片添加相关步骤
> 1. 创建ImageIcon对象。```new ImageIcon(String path)```  
> 2. 创建JLabel对象，并设置图片。 ```new JLabel(ImageIcon icon)```  
> 3. 设置图片位置。```jLabel.setBounds(x, y, width, height)```  
> 4. 添加JLabel对象到JFrame中。 ```this.getContenPane.add(JLabel label)```  
> 
> 注意：先加载的图片会在上方显示，后加载的图片会在下方显示。  

> 给图片添加边框(顶层：Border)：  
> 设置边框：jLabel.setBorder(new BevelBorder(bevelType));
> BevelBorder:  
> - BevelBorder.RAISED: 凸起 0
> - BevelBorder.LOWERED: 凹陷 1

## 10.4 事件
> 事件源：事件发生源。如按钮，图片，文本框等。  
> 事件：某些操作。鼠标单击，鼠标划入，键盘录入。  
> 事件监听：监听事件源，并执行相应的操作(接口)(KeyListener, MouseListener, ActionListener(动作监听))。  
> JButton:  
> - setBounds(int x, int y, int width, int height): 设置按钮的位置和尺寸。

> addActionListener(ActionListener listener): 添加动作监听器。只有左键和空格会触发。  
> - 当按钮只用一次的情况下可以使用匿名类，参数就是这个匿名类。  
> ```new ActionListener() {重写的actionPerformed(ActionEvent e)方法}```
> - 也可以当前类实现ActionListener接口，并重写actionPerformed(ActionEvent e)方法，此时参数直接传this即可(接口多态)。

> MouseListener:  
> 需要重写的方法：  
> - mouseClicked(MouseEvent e): 鼠标单击。
> - mousePressed(MouseEvent e): 鼠标按下。
> - mouseReleased(MouseEvent e): 鼠标释放。
> - mouseEntered(MouseEvent e): 鼠标划入。
> - mouseExited(MouseEvent e): 鼠标划出。
>
> 使用addMouseListener(MouseListener listener)方法添加鼠标监听器。  

> KeyListener:  
> 需要重写方法：
> - keyTyped(KeyEvent e): 键盘按下并释放。
> - keyPressed(KeyEvent e): 键盘按下。<font color="red">当一直按下某个键不松时，会触发多次</font>。
> - keyReleased(KeyEvent e): 键盘释放。
>
> 使用addKeyListener(KeyListener listener)方法添加键盘监听器。  
> 如何获取键盘录入的字符：
> - 获取字符：```int code = e.getKeyChar();```
> - 一般写在keyReleased(KeyEvent e)方法中。

## 10.5 弹框内容
> JDialog:  
> - 创建对象JDialog对象;
> - 使用容器管理对象JLabel;
> - 设置相应属性。
>   - setModal(true): 弹框不关闭无法进行其他操作。

## 10.6 文本/密文输入框/JButton
> JTextField:  
> - 创建对象JTextField对象;
> - 使用JLabel进行管理;
> - 设置相应属性;
> - 添加事件监听器。
> 
> JPasswordField:  
> - 创建对象JPasswordField对象;
> - 使用JLabel进行管理;
> - 设置相应属性;
> - 添加事件监听器。
> 
> JButton:
> - 创建对象JButton对象（可以添加ImageIcon对象作为按钮图标）;
> - 设置属性：
>   - setBounds(int x, int y, int width, int height): 设置按钮的位置和尺寸。
>   - setBorderPainting(false): 删除按钮边框。
>   - setContentAreaFilled(false): 删除按钮填充。

# 十一、常用的API
## 11.1 Math
> 常用方法：  
> - abs(int a): 返回参数的绝对值。可以改用absExact(int a)来避免某一负数绝对值溢出。  
> - ceil(double a): 向上(往正轴方向)取整，返回值也是double类型。  
> - floor(double a): 向下(往负轴方向)取整，返回值也是double类型。  
> - round(float a): 四舍五入，返回值是int类型。负数会向负轴方向取   
> - max(int a, int b): 返回两个参数中的较大值。  
> - pow(double a, double b): 返回a的b次方。  
> - random() : 返回[0.0, 1.0)之间的随机数。 
> - sqrt(double a): 返回参数的(算术)平方根。

## 11.2 System
> 常用方法：
> - exit(int status): 退出程序。  
> - currentTimeMillis(): 返回当前时间(毫秒)（相对于时间原点到现在的时间）。
> - arraycopy(Object src, int srcPos, Object dest, int destPos, int length): 拷贝数组。
>   - src: 源数组。dest: 目标数组。
>   - srcPos: 源数组的起始位置。destPos: 目标数组的起始位置。
>   - length: 拷贝的长度。
>   - 若src和dest均为基本数据类型需要一致才能拷贝。
>   - 拷贝的时候要注意数组的长度，避免超出数组范围。  
>   - 若src和dest为引用数据类型，则子类类型可以赋给父类类型。

## 11.3 Runtime
> 常用方法： 
> - getRuntime(): 获取当前运行环境对象。
> - exit(int status): 停止虚拟机。
> - availableProcessors(): 获取CPU线程数。
> - maxMemory(): JVM能从系统中获取的最大内存。单位都是byte
> - totalMemory(): JVM已经从系统中获取的总内存。
> - freeMemory(): JVM剩余的内存大小。
> - exec(String command): 执行系统命令。

## 11.4 Object
> 常用方法：  
> - toString(): 返回对象的字符串表示。
> - equals(Object obj): 判断两个对象是否相等(比较地址)。可以重写equals()方法来判断内容是否相同。

> 1. 浅克隆 clone()  
>   - 重写Object中的clone()方法  {return super.clone();}
>   - 让Javabean类实现Cloneable(标记性接口，无任何抽象方法)接口
>   - 创建原对象并调用clone()就可以了
> 2. 深克隆
>   - 重写Object中的clone()方法
>   - 基本数据直接拷贝，字符串复用，引用数据类型新建再拷贝  
>   - 第三方工具 Gson
>     ```
>     Gson gson = new Gson();
>     String json = gson.toJson(object);
>     Object object = gson.fromJson(json, Object.class);
>     ```
> 3. Objects
>   - Objects.equals(Object a, Object b): 判断两个对象是否相等。
>   - Objects.isNull(Object obj): 判断对象是否为null。
>   - Objects.nonNull(Object obj): 判断对象是否不为null。

## 11.5 BigInteger和BigDecimal
> [BigInteger](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/math/BigInteger.html):   
> 创建一个数：  
> - BigInteger(String val): 创建一个数。
> - BigInteger(int numBits, Random rnd): 随即返回数值，范围是\[0, 2^numBits - 1]
> - BigInteger(String val, int radix): 创建一个指定进制数。
> - static BigInteger valueOf(long val): 创建一个数。  
> 
> 注：对象一旦创建值无法改变。  
> 常见方法：  
> - 加/减/乘/除：add(val), subtract(val), multiply(val), divide(val)
> - divideAndRemainder(val): 返回商和余数
> - 最大最小值: max(val), min(val)
> - equals(val): 判断是否相等
> - pow(int n): 返回n次方
> - int intValue(val): 返回int值, 如果超出范围会抛出异常

> BigDecimal:  
> 创建一个小数：  
> - BigDecimal(String val)：创建一个字符串表示的小数
> - static BigDecimal valueOf(double val)：创建一个double表示的小数
> 
> 常用方法：
> - 加/减/乘/除: add/subtract/multiply/divide
>   - 参数：BigDecimal val
>   - divide(BigDecimal val, int scale, RoundingMode mode)这是除法的另一个方法，
>     scale表示保留的小数位数，mode表示舍入模式
> - 比较大小要使用 <font color="#ff0000">compareTo</font>，不建议使用 equals  

## 11.6 正则表达式
> <font color="red">单个</font>字符类：
> - \[abc]：匹配a或b或c
> - \[^abc]: 匹配除了a或b或c之外的字符
> - \[a-zA-Z]: 匹配a到z或A到Z之间的字符
> - \[a-d\[m-p]]: 匹配a到d或者m到p之间的字符
> - \[a-z&&\[def]]: 匹配a到z之间的字符，并且这些字符必须包含在def中
> - \[a-z&&\[^bc]]: 匹配a到z之间的字符，但是这些字符不能包含在bc中
> - \[a-z&&\[^m-p]]: 匹配a到z之间的字符，但是这些字符不能包含在m到p之间

> 预定义字符(<font color="red">单个</font>字符)：  
> - .：匹配任意字符，除了换行符
> - \d：匹配数字
> - \D：匹配非数字
> - \s: 一个空白符(\[\t\n\x0B\f\r])
> - \S: 非空白符
> - \w: \[a-zA-Z_\\d]
> - \W: 非\[a-zA-Z_\\d]

> 数量词： 
> - ?：匹配0个或1个
> - +：匹配1个或多个
> - *：匹配0个或多个
> - {n}：匹配n个
> - {n,}：匹配n个或更多
> - {n,m}：匹配n到m个，不超过m个
> - 注意：{n,}和{n,m}逗号后不能有空格

> 注意：
> - 当某一段字符串可能<font color="red">出现多次</font>可以用()括起来在加上数量词。  
>   e.g: regexEmail = "\\w+@[\\w&&[^_]]{2,6}<font color="red">(\\.[a-zA-Z]{2,3})</font>{1,2}";
> - 当某一段字符串可能出现<font color="red">多种形式</font>用|隔开，再用()括起来。  
>   e.g: regexTime = "<font color="red">([0-1]\\d|2[0-3])</font>(:[0-5]\\d){2}";  

> 有条件的正则表达式：
> - (?i)表示不区分大小写  
>   e.g: regexVerifyCode = "(?i)([\\w&&[^_]]{5})"
> - (?=pattern)表示前置条件，匹配的字符串必须满足前置条件  
>   e.g: 'Windows (?=95|98|NT|2000)' 匹配"Windows 2000"中的"Windows"，但不匹配"Windows 3.1"中的"Windows"。
> - (?:pattern)表示匹配子表达式，但不捕获匹配的子表达式,不存储供以后使用的匹配。这对于用"or"字符 (|) 组合模式部件的情况很有用。  
>   e.g: 'industr(?:y|ies) 是比 'industry|industries' 更经济的表达式。  
> - (?!pattern)表示匹配的字符串不满足pattern的字符串。  
>   e.g: 'Windows (?!95|98|NT|2000)' 匹配"Windows 3.1"中的 "Windows"，但不匹配"Windows 2000"中的"Windows"。  

> 贪婪爬取和非贪婪爬取：
> - Java中默认贪婪爬取，即尽可能多的匹配。
> - 如果在数量词+、*后面加上?，则变为非贪婪爬取。

> 正则表达式在字符串方法中的使用：
> boolean matches(String regex): 判断字符串是否匹配正则表达式。
> String[] split(String regex): 按照正则表达式进行字符串的分割。
> String replaceAll(String regex, String newStr): 替换所有匹配的字符串。

> 捕获分组(组号根据左括号计算，从1开始)：  
> \\组号表示把第x组的内容拿出来再用一次(组内使用)  
>   ```String regex = "(.).+\\1";```  把第一组的内容再用一次，判断字符首尾相同  
>   ```String regex = "((.+)\\2).+\\1``` 把第二组的内容用一次，判断字符首尾相同(且每部分也相同)    
> $组号表示把第x组内容拿出来用(组外使用)  
>   ```
>   String s = "我爱爱爱学学习习习习习编编编编编程程程程程程";
>   System.out.println(s.replaceAll("(.)\\1+", "$1"));
>   ```
> 
> 非捕获分组：(?:)  (?=)  (?!)  
> 特点：不占用组号

## 11.7 爬虫
> 1. 获取正则表达式对象  
>   ```Pattern pattern = Pattern.compile(regex);```
> 2. 获取文本匹配器对象  
>   ```Matcher matcher = pattern.matcher(text);```
> 3. 利用循环获取匹配结果  
>   ```
>   while(matcher.find()){
>       String match = matcher.group();  // 获取匹配的字符串
>       System.out.println(match);  
>   } 
>   ```

## 11.8 时间相关类
目前标准时间(UTC)已经替换为<font color="red">原子钟</font>。  
中国标准时间：世界标准时间 + 8
### 11.8.1 JDK7以前的时间类
> Date:精确到毫秒  
> 构造方法：  
>   ```public Date(){}``` 当前时间   
>   ```public Date(long date)```  指定时间   
> 常用方法：  
> - getTime(): 返回时间戳  
> - setTime(long date): 设置时间戳

> SimpleDateFormat:格式化时间，把字符串表示的时间解析为Date对象   
> 构造方法：  
>   ```public SimpleDateFormat(String pattern)```  指定格式  
>   ```public SimpleDateFormat()```  
> 常用方法：  
> - final String format(Date date): 格式化日期  
> - Date parse(String source): 解析字符串为日期

> Calendar: 是一个抽象类，提供了很多方法，用于操作日期和时间。  
> 获取日历对象：  
> - static Calendar getInstance(): 获取当前日历对象
> 
> 常用方法：  
> - Date getTime(): 获取日历对象对应的Date对象
> - setTime(Date date): 设置日历对象对应的Date对象
> - int get(int field): 获取指定字段的值 1：年 2：月 5：日期
> - set(int field, int value): 设置指定字段的值
> - add(int field, int amount): 为指定字段增加指定值
> - long getTimeInMillis(): 获取日历对象对应的时间戳（毫秒级）
> - setTimeInMillis(long millis): 设置日历对象对应的时间戳 
>
> 细节：  
> - 月份范围是0-11
> - 星期：老外认为周日是第一天

### 11.8.2 JDK8之后的时间类
JDK8新增时间对象是不可变的，线程安全。
> ZoneId: 时区  
> - static ZoneId of(String zoneId): 获取指定时区对象(e.g: "Asia/Shanghai")  
> - static ZoneId systemDefault(): 获取系统默认时区  
> - static Set< String> getAvailableZoneIds(): 获取所有时区  

> Instant: 时间戳  
> - static Instant now(): 获取当前时间戳
> - static Instatant ofXxxx(long epochMilli): 根据(s/ms/ns)获取Instant对象
> - zonedDateTime atZone(ZoneId zoneId): 获取指定时区的ZoneDateTime对象
> - boolean isXxx(Instant otherInstant): 判断系列方法
> - Instant minusXxxx(long millisToSubtract): 减去时间系列方法
> - Instant plusXxxx(long millisToSubtract): 增加时间系列方法

> ZonedDateTime: 含有时区的时间
> - static ZonedDateTime now(): 获取当前时间
> - static ZonedDateTime ofXxxx(...): 获取指定时区的ZonedDateTime对象
> - ZoneDateTime withXxxx(long millisToSubtract): 修改时间系列方法
> - ZoneDateTime plusXxxx(long millisToSubtract): 添加时间系列方法
> - ZoneDateTime minusXxxx(long millisToSubtract): 减去时间系列方法

> DateTimeFormatter: 时间格式化
> - static DateTimeFormatter ofPattern(String pattern): 获取指定格式的DateTimeFormatter对象
> - String format(ZonedDateTime zonedDateTime): 格式化ZonedDateTime对象

> LocalDate: 只包含日期（年、月、日）  
> LocalTime: 只包含时间（时、分、秒）  
> LocalDateTime: 包含时间和日期  
> - static XXX now(): 获取当前时间
> - static XXX of(...): 获取指定时间
> - getXxxx(): 获取Xxxx
> - isBefore(), isAfter(): 判断
> - withXxx(), plusXxx(), minusXxx(): 修改/增加/减少
> - LocalDateTime可以转换为其他两个时间类：toXxx()

> MonthDay: 只包含月日

> Duration: 时间间隔（s/ns）
> Period: 时间间隔（y/M/d）
> ChronoUnit: 时间间隔
> static XXX between(Temporal start, Temporal end): 获取时间间隔

## 11.9 包装类
JDK5以后增加了自动拆箱和自动装箱
> Integer: 
> - `static parseInt(String s)`: 字符串转int
> - `static String toXxxString(int i)`: int转字符串(二进制、八进制、十六进制)  
> - `static Integer valueOf(int/String v)`: 转换为包装类对象

注：除了Character都有 `parseXxx()` 的方法

包装类的缓存机制：
- `Byte`,`Short`,`Integer`,`Long` 这 4 种包装类默认创建了数值 $[-128，127]$ 的相应类型的缓存数据
- `Character` 创建了数值在 $[0,127]$ 范围的缓存数据
- `Boolean` 直接返回 `TRUE` or `FALSE` 
- <font color="#ff0000">只有 valueOf 和 自动装箱才会走缓存</font>，新建对象不会走缓存 

# 十二 集合进阶
二分查找改进：  
$$
mid = left + (value - arr[left]) / (arr[right] - arr[left]) * (right - left);
$$
(要求数据分布均匀)  

## 12.1 Arrays
> 常用方法(均为静态方法):  
> - toString(Object[] a): 数组转字符串
> - binarySearch(Object[] a, Object key): 二分查找
> - copyOf(Object[] original, int newLength): 复制数组
> - copyOfRange(Object[] original, int from, int to): 复制指定那个范围数组
> - fill(Object[] a, Object val): 填充数组
> - sort(Object[] a): 升序排序
> - sort(Object[] a, 排序规则): 按照指定排序规则排序
>   - Comparator: 排序规则
>   - 底层是插入排序 + 二分查找
>   - int compare(a, b)返回值：
>   - 返回值是负数，拿着A跟前面的数字比较
>   - 返回值是正数或者0，拿着A跟后面的数比较
>   - 参数a: 无序序列遍历得到的每一个元素
>   - 参数b: 有序序列中的元素
>   - 可以理解为a-b升序，b-a降序

## 12.2 Lambda表达式(函数式编程)
本质是一个匿名函数
> 语法：  
> ```(参数列表) -> {方法体}```
> 作用：简化匿名内部类的书写
> 使用范围：函数式接口(只有一个抽象方法的接口)，可以在<font color="red">接口</font>上方加上@FunctionalInterface注解
> 省略规则：
> - 参数类型可以省略
> - 只有一个参数，参数类型可以省略，同时()也可以省略
> - 当表达式只有一行可以省略大括号、分号和return(同时省略)

## 12.3 单列集合Collection
### 12.3.1 List系列集合
添加的元素有序、可重复、有索引  
List，Collection是接口，ArrayList和LinkedList是接口实现类
> <font color="pink">Collection(接口)</font>: 单列集合的父接口  
> 单列集合公有方法：  
> - boolean add(E e): 添加元素（添加元素成功返回true）
> - void clear(): 清空集合
> - boolean contains(Object o): 判断集合中是否包含某个元素
> (如果判断自定义的类，必须重写equals方法)
> - boolean remove(Object o): 删除元素
> - boolean isEmpty(): 判断集合是否为空
> - int size(): 获取集合大小  
> 
> 遍历方式：  
> - 迭代器遍历: 
>   - Iterator< E> iterator(): 获取迭代器
>   - iterator常用方法(类似于指针)：
>     - boolean hasNext(): 判断当前元素有无元素
>     - E next(): 获取当前元素并指向下一元素
>   ```
>   for(Iterator<E> iterator = list.iterator(); iterator.hasNext();) {
>       E e = iterator.next();
>       System.out.println(e);
>   }
>   Iterator<E> it = list.iterator();
>   while(it.hasNext()) {
>       E e = it.next();
>       System.out.println(e);
>   }
>   ```
>   注：迭代器遍历时不建议对集合进行修改(不过删除是可行的)
> - 增强for循环遍历:
>   ```
>   for(E e : list) {
>       System.out.println(e);
>   }
>   ```
>   注：增强for循环遍历时修改值无效
> - Lambda表达式遍历：
>   - default void forEach(Consumer< ? super E> action): 遍历集合
>   ```
>   list.forEach(e -> System.out.println(e));
>   list.forEach(System.out::println);
>   ```

> <font color="pink">List(接口)</font>:  
> 常用方法：  
> - boolean add(int index, E element): 指定位置添加元素
> - E remove(int index): 删除指定索引的元素
> - E set(int index, E element): 替换指定索引的元素
> - E get(int index): 获取指定索引的元素
> 
> 遍历方式：
> - 迭代器遍历
> - 列表迭代器遍历:  
>   - ListIterator< E> listIterator(): 获取列表迭代器,默认指向0索引
>   ```
>   for(ListIterator<E> listIterator = list.listIterator(); listIterator.hasNext();){
>       E e = listIterator.next();
>   }
>   ListIterator<E> listIterator = list.listIterator();
>   while(listIterator.hasNext()) {
>       E e = listIterator.next();
>   }
>   注意：列表迭代器遍历时可以增加和删除元素
>   ```
> - 增强for循环遍历
> - Lambda表达式
> - 普通for循环:  
>   ```
>   for(int i = 0; i < list.size(); i++) {
>       E e = list.get(i);
>   }
>   ```

> <font color="pink">ArrayList</font>:  
> 底层原理：  
> - 数组实现
>   - 空参构造创建长度为0的数组
>   - 当进行添加元素后创建一个新的长度为10的数组
> - 扩容机制：
>   - 默认扩容1.5倍
>   - 当一次添加元素个数太多，1.5倍还放不下，则长度为实际元素个数

> <font color="pink">LinkedList</font>:  
> 底层原理：   
> - <font color="red">双向链表</font>实现，查询慢，增删快
> - 包含许多特有的对首尾操作的API
> 
> 独有方法：
> - void addFirst(E e): 添加元素到链表头
> - void addLast(E e): 添加元素到链表尾
> - E getFirst(): 获取链表头元素
> - E getLast(): 获取链表尾元素
> - E removeFirst(): 删除链表头元素
> - E removeLast(): 删除链表尾元素

> <font color="pink">Vector</font>:(被移除)  

> <font color="pink">泛型</font>:  
> 格式：<数据类型>，数据类型只能是引用数据类型，传入的数据可以是其子类(但是不建议)  
> 好处: 统一数据类型，避免类型转换可能出现的异常。  
> Java中的泛型是<font color="red">伪泛型</font>，JVM会进行类型擦除，将泛型参数变为Object。  
> 应用：
> - 泛型类
>   当一个类某个数据类型不确定时，可以定义成泛型类  
>   ```public class 类名<T/E/K/V>{}```
> - 泛型方法
>   当一个类只有一个方法的数据类型无法确定时，可以定义成泛型方法  
>   ```修饰符< T> 返回值类型 方法名(T t) {}```  
>   当无法确定某一类型参数的个数可以E... e表示参数
> - 泛型接口
>   当一个接口某个数据类型不确定时，可以定义成泛型接口
>   ```修饰符 interface 接口名< T> {}```
>
> 泛型的继承和通配符:  
> 泛型本身没有继承性，但是数据类型有继承性(就是在参数是有泛型其子类不一定能传进去，但是单纯的数据类型可以传子类)  
> 通配符: 
> - ? 表示不确定的任意数据类型
> - ? extends E: 表示该泛型参数的子类和自身
> - ? super E: 表示该泛型参数的父类和自身

### 12.3.2 Set系列集合
添加的元素无序、不重复、无索引  
Set是Collection的子接口，HashSet、TreeSet和LinkedHashSet是Set的实现类  
> <font color="pink">红黑树</font>:  
> 红黑树是特殊的二叉查找树。  
> 红黑规则：  
> - 每个节点要么红色要么黑色
> - 根节点必须是黑色
> - 一个节点没有子节点(任意一个没就算)或者父节点，这些节点相应的指针值(left、right)为Nil，
>   视为叶节点，<font color="red">每个Nil是黑色的</font>
> - 如果一个节点是红色的，那么它的两个子节点都是黑色的(不会有两个红节点相连)
> - 对每一个节点，从该节点到期所有后代叶结点的简单路径上有<font color="red">>相同数目</font>的黑色节点
> - 添加节点的时候节点值默认红色
> 
> 添加节点:  
> - 根节点：直接变为黑色
> - 非根节点：  
>   - 父节点是黑色：不做改变
>   - 父节点是红色：  
>     - 叔叔节点是红色：
>       - 父变黑，叔叔变黑，祖父变红色
>       - 祖父为跟再把根变为黑色，祖父为非根把祖父设置为当前节点在进行其他判断
>     - 叔叔节点是黑色且当前节点为父的<font color="red">左节点</font>：
>       - 父变黑色，祖父变为红色，以祖父为支点右旋
>     - 叔叔节点是黑色且当前节点为父的<font color="red">右节点</font>：
>       - 将父节点设置为当前节点并左旋，再进行判断

> <font color="pink">Set(接口)</font>:  
> 包含Collection接口的所有基本方法  
> 遍历方式：迭代器，增强for，Lambda表达式

> <font color="pink">HashSet</font>:    
> 底层是哈希表(数组+链表+红黑树)存储数据
> - 创建一个默认长度16，默认加载因子0.75的数组table
> - 相同值形成链表挂在之前的值之后
> - 当数组长度不够(填充的空位为 数组长度*0.75)时，扩容为原来的2倍
> - 当<font color="red">数组长度达到64且链表长度超过8时</font>链表会变成红黑树
> 
> 哈希值：
> - 根据hashCode()计算的int类型整数
> - 默认使用地址值进行计算
> - 一般重写，利用属性值计算哈希值
> 
> 注意：存储自定义对象要重写hashCode()和equals()方法

> <font color="pink">LinkedHashSet</font>(有序):  
> 父类是HashSet  
> 这里的有序是指存储和取出元素顺序一致  
> 底层原理：  
> - 哈希表 + 双向链表(用来保证数据存储和取出顺序一致)

> <font color="pink">TreeSet</font>(可排序):
> 默认规则(升序)：
> - 数值类型按照从小到大排序
> - 字符、字符串按照ASCII码的顺序排序
>
> 自定义排序：
> - 实现Comparable接口，重写compareTo()方法，规则跟sort一样
> - 创建集合时添加比较器进行排序

## 12.4 双列集合Map
Map: 双列集合顶层接口，全部双列集合均可以继承使用  
HashMap, TreeMap, LinkedHashMap均为Map实现类 
> <font color="pink">Map(接口)</font>:  
> 泛型接口：```public interface Map<K, V>{}```  
> 常用方法：  
> - V put(K key, V value): 添加元素(键不存在直接添加，键存在则覆盖)
> - V remove(Object key): 删除key对应的键值对元素
> - void clear(): 清空所有元素
> - boolean containsKey(Object key): 判断集合中是否包含指定key
> - boolean containsValue(Object value): 判断集合中是否包含指定value
> - boolean isEmpty(): 判断集合是否为空
> - int size(): 获取集合大小
> - V get(Object key): 获取指定key对应的value
> - Set< K> keySet(): 获取所有键的集合
> - Collection< V> values(): 获取所有值的集合
> - entrySet(): 获取所有键值对的集合
> 
> 遍历方式（迭代器，增强for，Lambda表达式）：
> - 键找值：  
>   - 获取键的集合：```Set< E> keys = map.keySet();```
> - 键值对：
>   - 获取键值对集合：```Set<Map.Entry<K, V>> entries = map.entrySet();```
>   - 利用Entry内部接口的方法获取键值对：getKey(), getValue()
> - Lambda表达式：
>   - ```map.forEach((k, v) -> {})```

> <font color="pink">HashMap</font>:  
> 底层是哈希表(数组+链表+红黑树)存储数据  
> 是Map的一个实现类  

> <font color="pink">LinkedHashMap</font>(有序):  
> 这里的有序是指保证存储与取的顺序一致  
> Map的实现类，是HashMap的子类
> 底层是哈希表(数组+双向链表)

> <font color="pink">HashTable</font>:   







> <font color="pink">Properties</font>:    
> HashTable的子类，专门用来存储键值对的集合。






> <font color="pink">HashMap(可排序)</font>:   
> 这里的可排序是指可以对键进行排序。  
> 两种排序规则：  
> - 实现Comparable接口，重写compareTo()方法，规则跟sort一样
> - 创建集合时添加比较器进行排序
> 
> 底层原理：基于红黑树实现的Map

## 12.5 可变参数
> 可变参数：在方法中可以传入任意个数的参数(包括0个)  
> 本质上其实是一个数组，传入的参数会自动封装成一个数组。  
> 格式：  
> ```
> public void 方法名(数据类型... args){}
> ```
> 注意：  
> - 可变参数只能有一个
> - 可变参数必须是方法的最后一个参数

## 12.6 Collections
> 集合的工具类，有许多方法来操作集合。  
> 常用方法：  
> - `static void shuffle(List<?> list)`: 打乱集合顺序
> - `static <T> boolean addAll(Collection< ? super T> c, T... elements)`: 向集合c中添加元素
> - `static < T> void sort(List< T> list)` : 排序
> - static < T> void sort(List< T> list, Comparator< ? super T> c): 按照指定规则排序
> - static < T> int binarySearch(List< ? extends Comparable< ? super T>> list, T key): 二分查找
> - static < T> void copy(List< T> dest, List< T> src): 拷贝集合
> - static < T> int fill(List< T> list, T obj): 向list中填充元素
> - static < T> void max/min(Collection< T> coll): 获取集合中的最大值/最小值
> - static < T> void swap(List< T> list, int i, int j): 交换集合中两个指定位置的元素
> - static < T> void reverse(List< T> list): 反转集合list

## 12.7 不可变集合
> 理解：不想让别人修改集合中的内容  
> 实现：在List、Set和Map的接口中有一个静态方法of可以获取不可变集合  
> - List.of(E... e): 获取不可变List集合
> - Set.of(E... e): 获取不可变Set集合
> - Map.of(E... e): 获取不可变Map集合，最多传入10个键值对
> - Map.ofEntries(Map.Entry<K, V>... entries): 获取不可变Map集合，可以传入任意个键值对
> - Map.copyOf(Map< ? extends K, ? extends V> map): 获取不可变Map集合，传入一个已有的Map集合

## 12.8 Stream流
> 结合Lambda表达式和链式编程简化集合操作  
> 步骤：  
> - 获取流对象：
>   - <font color="red">Collection</font>.stream(): 获取流对象  
>     注意：Collection是接口，可以用其实现类进行调用
>   - 双列集合无法直接使用stream()方法获取流对象
>     - keySet(): 获取所有键的集合，然后调用stream()方法获取流对象
>     - entrySet(): 获取所有键值对的集合，然后调用stream()方法获取流对象
>   - 数组：<font color="red">Arrays</font>.stream(T[] arr)
>   - 零散数据：Stream.of(T... values)，但是需要<font color="red">数据的类型统一</font>
> - 对流进行操作（先中间方法，最后加上终止方法）：  
>   - 中间方法：
>     - filter(Predicate< ? super T> predicate): 过滤流中的元素(符合predict的元素会被保留)
>     - limit(long maxSize): 限制(获取)流中的元素个数
>     - skip(long n): 跳过流中的前n个元素
>     - distinct(): 去重，依赖hashCode()和equals()方法
>     - concat(Stream a, Streeam b): 合并两个流(Stream里面的<font color="red">静态方法</font>)
>     - map(Function< ? super T, ? extends R> mapper): 对流中的元素进行映射  
>     - 注意：对流进行修改不影响原集合
>   - 终止方法(一个流一旦使用了终止方法就不再存在了)：
>     - void forEach(Consumer< ? super T> action): 遍历流中的元素
>     - long count(): 统计
>     - toArray(): 收集流中的数据存入数组内
>       ``` java
>       list.stream().toArray(IntFunction< ? extends T[]> generator)
>       // generator是一个函数式接口，传入一个int参数，返回一个数组
>       list.stream().toArray(value -> new String[Value]);
>       ```
>     - collect(): 收集流中的数据放入集合中
>       ``` java
>       // List:
>       List<E> newList = list.stream().collect(Collectors.toList());
>       // Set:
>       Set<E> newSet = list.stream().collect(Collectors.toSet());
>       // Map: 
>       Map<K, V> newMap = list.stream().collect(Collectors.toMap(F1, F2));
>       // groupingBy
>       Map<K, V> newMap = list.stream.collect(Collectors.groupingBy(Function, Supplier, Collector));
>       // 相当于就是把一个列对象列表按照对象的某个属性就行分组
>       ```
>       [Colletors学习](Java进阶学习/Collectors)  
>       注意：F1和F2是函数式接口，分别表示键和值的映射关系  
>       每个接口重写一个函数public K apply(T s, K k)  
>       第一个参数表示流中的元素类型，第二个参数表示键/值的类型(
>       <font color="red">与apply的返回值类型相对应</font>)  
>       <font color="red">键不能重复</font>，如果重复会抛出异常

## 12.9 方法引用
> 方法引用是把已经有的方法拿过来当作<font color="red">函数式接口</font>中抽象方法的方法体  
> 细节：  
> - 引用处必须是<font color="red">函数式接口</font>
> - 被引用的方法必须已经存在
> - 被引用的方法的形参和返回值需要跟抽象方法一致  
> - 被引用的方法的功能要满足当前需求
> - :: 是方法引用符
>
> 分类：  
> - 引用静态方法：```类名::方法名```
> - 引用成员方法：```对象::成员方法```
>   - 其他类：```对象名::方法名```
>   - 本类：```this::方法名```
>   - 父类：```super::方法名```
>   - this和super引用处不能是静态方法
> - 引用构造方法：```类名::new```
> - 其他调用方式：
>   - 类名::成员方法(有独有规则)
>     - 引用处有函数式接口
>     - 引用的方法已经存在
>     - 被引用的方法的形参需要跟抽象方法的<font color="red">第二个到最后一个</font>形参保持一致，返回值需要保持一致  
>       <font color="red">注意：</font>第一个参数决定了可以引用那些类中的方法
>     - 被引用方法的功能需要满足当前功能需求
>   - 数据类型[]::new
>     - 目的是创建一个指定类型的数组
>     - 数组的类型需要跟流中的数据保持一致

# 十三、异常
含义：异常就是代表程序出现的问题  
Error：这个是sun公司自己用的，不用管  
Exception: 代表程序可能出现的问题，分为<font color="red">运行时异常</font>(RuntimeException及其子类)和编译时异常

## 13.1 异常的分类
> 编译时异常：编译阶段必须处理，否则代码报错  
> 运行时异常：RuntimeException及其子类,一般由于参数传递错误导致  

## 13.2 异常的作用
1. 查看bug关键参考信息  
2. 可以作为方法内部的一种特殊返回值，以便通知调用者底层的执行情况

## 13.3 处理方式
1. JVM默认处理方式：打印错误信息并退出程序
2. 自己处理（捕获异常）
> 自己处理(try...catch)
> 格式：
> ```
> try{
>   可能出现异常的代码
> }catch(Exception e){
>   异常处理
> }
> ```
> 注意：
> - try中无问题会执行完所有try中代码，不会执行catch里的代码
> - 当try中出现多个异常要对应<font color="red">每个异常</font>写一个catch进行捕获
> - 当捕获的异常出现父子关系时，<font color="red">子类异常必须写在父类异常之前</font>，否则捕获父类异常则无法执行其他捕获其子类的异常
> - JDK7之后一个catch里面可以<font color="red">用 | 来捕获多个异常</font>  
>   ```catch(Exception1 | Exception2 e){}```
> - try中的异常未被捕获会由虚拟机来默认处理
> - 每次<font color="red">只会捕获一个异常</font>，直接跳转到对应的catch，try后面的语句不会执行

> 自己处理(try...catch...finally):  
> 格式：  
> ``` java
> try{
>   可能会出现异常的代码
> }catch(Exception e){
>   异常处理
> }finally{
>   释放资源
> }
> ```

> Throwable的成员方法：  
> - String getMessage(): 返回详细消息字符串
> - String toString(): 返回可抛出的简述
> - void printStackTrace(): 打印异常信息，底层用System.err.println进行输出(红色)


## 13.4 抛出异常
> throws: 写在方法定义处，声明一个异常告诉调用者，使用本方法可能会有哪些异常  
> 运行时异常可以省略不写
> ```
> public void method() throws XxxException{}
> ```
> throw: 写在方法内，结束方法手动抛出异常对象，交给调用者下方的代码不再执行
> ```
> public void method(){
>     if(xxx) throw new XxxException();
> }
> ```

## 13.5 自定义异常
1. 定义一个类继承Exception或者RuntimeException
2. 空参构造和有参构造

# 十四、File和IO
## 14.1 File 
> 构造方法：  
> - File(String pathname): 通过文件名创建File对象
> - File(String parent, String child): 通过父目录和子路径创建File对象(拼接)
> - File(File parent, String child): 通过父目录文件对象和子路径创建File对象(拼接)
> 
> 常见成员方法：
> - 判断、获取：  
>   - boolean isDirectory(): 判断是否是目录
>   - boolean isFile(): 判断是否是文件
>   - boolean exists(): 判断文件是否存在
>   - long length(): 获取文件大小(字节数)，<font color="red">无法获取文件夹大小</font>
>   - String getName(): 获取文件名
>   - long lastModified(): 获取最后一次修改时间(毫秒值)
>   - String getAbsolutePath(): 获取绝对路径
>   - String getPath(): 获取定义文件时使用的路径
> - 创建、删除：
>   - boolean createNewFile(): 创建文件
>   - boolean mkdirs(): 创建多级文件夹
>   - boolean mkdir(): 创建单级文件夹
>   - boolean delete(): 删除文件/文件夹
> - 获取并遍历：
>   - File[] listFiles(): 获取当前目录下的所有文件/文件夹
>     - 路径不存在或者是文件返回null
>     - 空文件夹返回长度为0数组
>     - 有内容的文件夹返回路径存储到File数组里(包含隐藏文件)
>     - 无权限访问的文件夹会返回null
>   - static File[] listRoots(): 获取所有盘符
>   - String[] list()： 只包含名字
>   - String[] list(FilenameFilter filter)： 使用文件名过滤器
>   - File[] listFiles(FilenameFilter filter), File[] listFiles(FileFilter filter)（文件名过滤器）

## 14.2 IO流
作用：用于读取文件中的数据  
分类：
- 流的方向：输入流、输出流
- 操作文件类型：字节流(所有类型文件按)、字符流(纯文本文件)   
<font color="red">注意</font>: IO流最好是随用随创，当创建了输入流后立马创建输出流(同一文件)会<font color="red">清空文件内容</font>
### 14.2.1 基础流
> 字节流抽象基类：InputStream、OutputStream  
> 字符流抽象基类：Reader、Writer  
> 字节流实现类：FileInputStream、FileOutputStream  
> 字符流实现类：FileReader、FileWriter  

> FileOutputStream:
> 1. 创建输出流：
>   - 参数可以是路径字符串、File对象(new FileOutputStream(file))
>   - 文件不存在会创建，文件存在会清空文件内容，但要求<font color="red">父级目录存在</font>
>   - 如果想<font color="red">续写</font>，需要使用带参构造(new FileOutputStream(file,boolean append),append表示是否需要续写)
> 2. 写数据：
>   - write(int b): 写一个字节，实际写的是参数b在ASCII上对应的字符
>   - write(byte[] b): 写一个字节数组
>   - write(byte[] b, int off, int len): 写字节数组的一部分
>   - 当想写一个字符串时，必须把<font color="red">字符串转换成字节数组(str.getBytes())</font>
>   - 换行符：Windows(\r\n), Linux(\n), Mac(\r)
> 3. <font color="red">释放资源</font>：每次使用完流都要关闭(流名.close())

> FileInputStream:
> 1. 创建输入流：
>   - <font color="red">文件不存在会报错(空指针异常)</font>
> 1. 读数据：
>   - int read(): 读一个字节，返回字节值(对应的ASCII码值)，如果已读到末尾则返回-1
>   - int read(byte[] b): 读一个字节数组，每次最多读b.length个字节，
>     返回<font color="red">实际读的字节数</font>，如果已读到末尾则返回-1
>   - int read(byte[] b, int off, int len): 读字节数组的一部分，每次最多读len个字节，返回实际读的字节数，如果已读到末尾则返回-1
> 3. 释放资源：每次使用完流都要关闭(流名.close())

> 异常处理：  
> try后面括号中写的代码<font color="red">必须实现AutoCloseable接口</font>的类才能在小括号创建对象  
> JDK7及其以前：  
> ``` java
> try(创建流对象1; 创建流对象2; ...){
>     可能异常的代码
> }catch(异常类名 e){
>     异常处理
> }
> ```
> JDK9及其之后：  
> ``` java
> 创建流对象1;
> 创建流对象2;
> try(流对象1; 流对象2; ...){
>     可能异常的代码
> }catch(异常类名 e){
>     异常处理
> }
> ```
> 基本处理：  
> ``` java
> try{
>     可能异常的代码
> }catch(Exception e){
>     e.printStackTrace();
> }finally{
>     释放资源操作;
> }
> ```

> Java中的编码与解码
> 编码：把字符串转换成字节数组
> - byte[] str.getBytes(): 使用默认编码
> - byte[] str.getBytes(String charsetName): 使用指定的编码
> - charsetName: GBK, UTF-8...
> 解码：把字节数组转换成字符串
> - new String(byte[] bytes): 使用默认方式解码
> - new String(byte[] bytes, String charsetName): 使用指定的编码解码

> FileReader:  
> 1. 创建字符输入流：
>   - ```
>     FileReader fr = new FileReader(File file);
>     FileReader fr = new FileReader(String path); 
>     ```
> 2. 读取数据：
>   - int read(): 读取一个字符，返回字符值，如果已读到末尾则返回-1
>   - int read(char[] buf): 读取一个字符数组，每次最多读取buf.length个字符，
>     返回<font color="red">实际读取的字符数</font>，如果已读到末尾则返回-1
>   - 返回十进制，是字符集上的数字，若要看到原字符需要进行<font color="red">强转(char)</font>
>   - 读取数据会尽可能从文件将数据先填满缓冲区，<font color="red">读取数据都是在缓冲区读取</font>
> 3. 释放资源：
>   - fr.close()

> FileWriter:  
> 1. 创建字符输出流：
>   - ``` java
>     FileWriter fw = new FileWriter(File file);
>     FileWriter fw = new FileWriter(String path);
>     ```
>   - 文件不存在会创建，文件存在会清空文件内容，但要求<font color="red">父级目录存在</font>
>   - 是否进行续写可以加上参数(boolean append)
> 2. 写数据：
>   - write(int c): 写一个字符
>   - write(char[] cbuf): 写一个字符数组
>   - write(char[] cbuf, int off, int len): 写一个字符数组的一部分
>   - write(String str): 写一个字符串
>   - write(String str, int off, int len): 写一个字符串的一部分
>   - 写数据也是先写入缓冲区，缓冲区满了或者flush以及close都会将缓冲区中的数据写入文件
>   - flush和close的区别：flush将缓冲区数据写入本地后还能继续写入，但是close是先写数据在释放资源
> 3. 释放资源：
>   - fw.close()
> 字节流常用于拷贝文件，字符流常用于处理文本文件

### 14.2.2 缓冲流
字节缓冲流：BufferedInputStream、BufferedOutputStream  
字符缓冲流：BufferedReader、BufferedWriter   
缓冲流就是<font color="red">基本流包装成高级流</font>，缓冲流提高效率   
> 字节缓冲流:   
> 1. 创建缓冲流：
>   - ``` java
>     BufferedInputStream bis = new BufferedInputStream(InputStream is);
>     ```
>   - ``` java
>     BufferedOutputStream bos = new BufferedOutputStream(OutputStream os);
>     ```
> 2. 缓冲区为长度为8192的字节数组
> 
> 字符缓冲流：  
> 1. 创建缓冲流：
>   - ``` java
>     BufferedReader br = new BufferedReader(Reader r); // 字符输入流
>     BufferedWriter bw = new BufferedWriter(Writer w); // 字符输出流
>     ```
> 2. 特有方法：
>   - String readLine(): 读取一行数据，返回读取的字符串，如果已读到末尾则返回null
>     (<font color="red">字符缓冲输入流独有</font>)    
>     注意：readLine()遇到回车换行符号就截止读取，但<font color="red">不会读入回车换行符号</font>，需要手动换行
>   - void newLine(): 跨平台换行(<font color="red">字符缓冲输出流独有</font>)
> 3. 缓冲区为长度为8192的字符数组

### 14.2.3 转换流
字符流和字节流之间的桥梁  
JDK11之后FileReader和FileWriter已经包含了编码转换功能，不再需要使用InputStreamReader和OutputStreamWriter  
编码转换使用<font color="red">Charset.forName("编码名")</font>指定
> InputStreamReader: 字节流转换为字符流  
> OutputStreamWriter: 字符流转换为字节流

### 14.2.4 序列化流
可以把Java中的对象写到本地文件中  
序列化流/对象操作输出流：ObjectOutputStream(OutputStream out) 
- 成员方法：final void writeObject(Object obj) 把对象序列化(写出)到文件中  

反序列化流/对象操作输入流：ObjectInputStream(InputStream in)  
- 成员方法：Object readObject() 把对象从文件中读取出来

> 序列化：把Java中的对象写到本地文件中  
> 反序列化：把本地文件中的对象读取出来  
> 注意：
> - 类必须实现Serializable接口
> - 类中的属性必须是可序列化的
> - 序列化的版本号：public static final long serialVersionUID;
> - 序列化的版本号可以不写，但是不写的话反序列化时会有警告
> - 序列化的版本号可以写在类的第一行，也可以写在类的最后一行，也可以写在类的中间一行
> - 如果某个属性不想序列化可以使用<font color="red">transient关键字</font>
> - 如果要序列化<font color="red">多个对象</font>可以先存到ArrayList里面，然后把ArrayList序列化即可

### 14.2.5 打印流
分类：PrintStream(字节打印流), PrintWriter(字符打印流)  
特点：  
- 打印流只操作文件的目的地，不操作数据源
- 特有写出方法可以实现数据原样写出
- 特有写出方法可以实现自动刷新和换行

> PrintStream:
> - 构造方法： 
>   - PrintStream(OutputStream/File/String): 关联字节输出流/文件/文件路径
>   - PrintStream(String fileName, Charset charset): 指定字符编码
>   - PrintStream(OutputStream out, boolean autoFlush): 设置自动刷新
>   - PrintStream(OutputStream out, boolean autoFlush, String encoding): 指定字符编码并自动更新
>   - <font color="red">注意</font>：字节流底层没有缓冲区，开不开自动刷新都一样
> - 常规方法： write(int b)
> - 特有方法：
>   - print(Xxx x): 打印任意数据不会换行
>   - println(Xxx x): 打印任意数据并换行
>   - printf(String format, Object... args): 格式化打印(带有占位符的打印语句，不换行)，保证数据原样输出
>   - 占位符：%n(换行), %c, %d, %f, %s, %b(boolean), %x(十六进制数), %o(八进制), %a(十六进制), %e(科学计数法), 
>     %%(百分比), %t(时间)

> PrintWriter:  
> - 构造方法：
>   - PrintWriter(Write/OutputStream/File/String): 创建打印流对象
>   - 其他三个构造方法同PrintStream
>   - 需要后动开启自动刷新(只有关联Write和OutputStream的构造方法含有自动刷新参数)
> - 方法同 `PrintStream`


### 14.2.6 解压缩流和压缩流
解压缩流：独属于输入流，只能解压文件(ZipInputStream)  
压缩流：独属于输出流，只能压缩文件(ZipOutputStream)  
java中只能识别zip文件  
> 解压缩流：  
> 1. 创建解压缩流：
>   - ZipInputStream zis = new ZipInputStream(InputStream is);
> 2. 创建压缩包文件和解压缩后的位置：
>    - File src = new File(压缩包位置);
>    - File dest = new File(解压缩文件位置);
> 3. 获取压缩文件列表：
>   - ZipEntry entry = zis.getNextEntry();
>   - ZipEntry常用方法：
>     - String getName(): 获取条目名称
>     - boolean isDirectory(): 判断是否是目录
>     - String toString(): 获取文件名
>   - 读取数据：zip.read()
>   - 拷贝数据：使用FileOutputStream写出数据
>   - 关闭entry：zip.closeEntry(), 表示一个zipEntry文件解压完成
> 4. 关闭流：
>   - zip.close();
> 
> 代码：
> ``` java
> public static void unZip(File src, File dest) throws IOException {
>     ZipInputStream zis = new ZipInputStream(new FileInputStream(src));
>     ZipEntry entry = null;
>     while ((entry = zis.getNextEntry();) != null) {
>         if(entry.isDirectory()) {
>             File dir = new File(dest, entry.toString());
>             dir.mkdirs();
>             continue;
>         }
>         FileOutputStream fos = new FileOutputStream(new File(dest, entry.toString()));
>         int b = -1;
>         while ((b = zis.read()) != -1) {
>             fos.write(b);
>         }
>         fos.close();
>         zis.closeEntry();
>     }
>     zis.close();
> }
> ```

> 压缩流：
> 1. 创建压缩流：
>   - ZipOutputStream zos = new ZipOutputStream(OutputStream os);
> 2. 创建压缩文件和压缩包位置：
>   - File src = new File(文件位置);
>   - File dest = new File(压缩包位置);
> 3. 获取ZipEntry对象并写入压缩包：
>   - ZipEntry entry = new ZipEntry(文件名);
>   - zos.putNextEntry(entry);
>   - 写数据用FileInputStream读取src数据后使用zos.write()写出
>   - 关闭entry对象: zos.closeEntry();
> 4. 关闭流：
>   - zos.close();
>  
> 代码：
> ``` java
> // 压缩单个文件
> public static void toZip(File src, File dest) throws IOException { 
>     ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(dest, "xxx.zip"));
>     ZipEntry entry = new ZipEntry("xxx");  // src.getName()???
>     zos.putNextEntry(entry);
>     FileInputStream fis = new FileInputStream(src);
>     int b = -1;
>     while ((b = fis.read()) != -1) {
>         zos.write(b);
>     }
>     zos.closeEntry();
>     fis.close();
>     zos.close();
> }
> ```
> ``` java
> // 压缩一个文件夹
> public static void main(String[] args) throws IOException {
>     File src = new File(pathName);  //pathName是文件路径
>     File destParent = src.getParentFile();
>     File dest = new File(destParent, src.getName() + ".zip");
>     ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(dest));
>     toZip(src, zos, src.getName());
>     zos.close();
> }
> 
> public static void toZip(File src, ZipOutput zos, String name) throws IOException {
>     File[] files = src.listFiles();
>     for (File file : files) { 
>         if(file.isDirectory()) {
>             toZip(file, zos, name + "\\" + file.getName());
>             continue;
>         }
>         ZipEntry entry = new ZipEntry(name + "\\" + file.getName());
>         zos.putNextEntry(entry);
>         FileInputStream fis = new FileInputStream(file);
>         int b = -1;
>         while ((b = fis.read()) != -1) {
>             zos.write(b);
>         }
>         fis.close();
>         zos.closeEntry();
>     }
> }
> ```

### 14.2.7 工具包
> Commons-io是一个开源的java工具包，提供了很多io操作的封装，方便开发人员使用。  
> Commons-io使用步骤: 
> - 在项目中创建一个文件夹:lib
> - 将jar包复制粘贴到lib文件夹
> - 右键点击jar包，选择 Add as Library ->点击OK
> - 在类中导包使用

> [Hutool](https://plus.hutool.cn/apidocs/ "API文档")：一个Java工具类库，提供了大量工具类，简化开发工作。  

> 配置文件properties:
> Properties类：继承Hashtable，专门用来处理配置文件的类（双列集合）  
> 基本方法：  
> - 包含Map所有基本方法
> 
> 特有方法：  
> - store(Writer/OutputStream writer/os, String comments): 保存文件
> - load(InputStream/Reader is/reader): 读取数据
> - getProperty(String key): 获取key对应的value

# 十五、多线程
线程：程序执行的最小单位，线程是进程中的一个执行路径  
并发：同一时刻多个指令在单个CPU上<font color="red">交替</font>执行
并行：同一时刻多个指令在单个CPU上<font color="red">同时</font>执行  
<font color="red">线程的栈是私有的，而堆空间是公有的</font>

## 15.1 实现方式
> 常见实现方式(前三种常用)：
> 1. 实现类继承Thread类并重写run()方法
>   - 创建线程对象：```实现类名 t = new 实现类名();```
>   - 设置名字：```t.setName(String name);```
>   - 启动线程：```t.start();```
> 2. 实现类实现Runnable接口并重写run()方法
>   - 创建实现类对象
>   - 创建Thread对象并传入实现类对象：```Thread t = new Thread(实现类对象);```
>   - 设置名字：```t.setName(String name);```
>   - 启动线程：```t.start();```
>   - 注意：无法在实现类中调用Thread的getName()方法，需要先获取当前线程对象  
>     获取当前线程对象：```Thread t = Thread.currentThread()```
> 3. 实现类实现Callable接口并重写call()方法
>   - 创建实现类对象：```实现类名 实现类对象 = new 实现类名();```
>   - 创建FutureTask的对象(作用是管理多线程运行的结果): ```FutureTask< V> ft = new FutureTask<>(实现类对象);```
>   - 创建Thread对象并传入FutureTask的对象: ```Thread t = new Thread(ft);```
>   - 获取线程的结果：```V res = ft.get();```
> 4. 使用Lambda表达式或者匿名内部类创建线程(不咋用)  
>
> 三种方式的对比： 
> 
> |      方式      | 优点 |          缺点           |
> |:------------:|:---:|:---------------------:|
> |  继承Thread类   | 简单，直接使用Thread类的成员方法 |     无法继承其他类，无法复用      |
> | 实现Runnable接口 | 可以继承其他类，复用性高 |   不能直接使用Thread类中的方法   |
> | 实现Callable接口 | 可以继承其他类，复用性高 |   不能直接使用Thread类中的方法   |
> 注意：只有实现Callable接口的方式可以获取线程的返回值，其他两种方式无法获取线程的返回值

## 15.2 常用成员方法
> Thread类的常用成员方法：
> - String getName(): 获取线程名称
> - void setName(String name): 设置线程名称
> - <font color="red">static</font> Thread currentThread(): 获取当前线程对象
> - <font color="red">static</font> void sleep(long millis): 让当前线程休眠指定毫秒数
> - setPriority(int newPriority): 设置线程优先级
> - final int getPriority(): 获取线程优先级
> - final void setDaemon(boolean on): 设置线程是否为守护线程  
>   注意：守护线程会在其他非守护线程执行完毕后<font color="red">陆续</font>结束
> - <font color="red">static</font> void yield(): 让当前线程让出CPU资源
> - <font color="red">static</font> void join(): 插入线程/礼让线程  

## 15.3 线程的生命周期
> 线程的生命周期：
> - 新建状态：创建线程对象后，线程处于新建状态
> - 就绪状态：调用start()方法后，线程进入就绪状态，等待CPU分配时间片
> - 运行状态：CPU分配时间片后，线程进入运行状态（Java未定义，JVM会把线程交给操作系统）
> - 阻塞状态：线程因为某种原因被阻塞，无法继续执行(无法获得锁对象)
> - 等待状态：线程调用wait()方法后，进入等待状态，等待其他线程唤醒
> - 计时等待状态：线程调用sleep()方法后，进入超时等待状态
> - 死亡状态：线程执行完毕或者被强制结束后，线程进入死亡状态

## 15.4 线程同步
> 线程安全：多个线程同时访问同一个资源时，能够保证数据的正确性和一致性  
> 同步代码块：使用synchronized关键字修饰代码块，保证同一时刻只有一个线程可以执行该代码块
> ``` java
> synchronized(锁对象){
>    // 同步代码块
> }
> ```
> 注意：
> - 锁对象一定要是唯一的(static修饰)，通常使用类名.class作为锁对象
> - 要注意锁对象的位置  

> Lock锁:  
> Lock是一个接口(不可实例化)，提供了比synchronized更灵活的锁机制  
> 通常采用ReentrantLock(Lock接口的实现类)来实现锁机制  
> 两个方法： void lock(), void unlock()

> 死锁：两个或多个线程互相等待对方释放锁，导致程序无法继续执行

> 生产者消费者  
> 常见方法：
> - wait(): 让当前线程等待，直到被notify()或notifyAll()唤醒
> - notify(): 唤醒一个等待的线程
> - notifyAll(): 唤醒所有等待的线程
>
> 方法(等待唤醒机制)：
> - 法1：使用Object类的wait()和notify()方法
> - 法2：使用BlockingQueue接口的实现类(如ArrayBlockingQueue)

## 15.5 线程池
> 线程池：线程复用技术，提高效率，避免频繁创建线程  
> 代码实现：
> 1. 创建线程池
>   - Executors: 线程池的工具类通过调用方法创建不同类型的线程池对象
>     - public static ExecutorService newCachedThreadPool(): 创建一个线程池，线程数量不固定(int类型最大值)
>     - public static ExecutorService newFixedThreadPool(int nThreads): 创建一个线程池，线程数量固定，超出数量将等待
> 2. 提交任务
>   - 线程池.submit(Runnable task): 提交任务
> 3. 所有任务执行完毕，关闭线程池(通常情况下不关闭线程池)
>   - 线程池.shutdown();

> 自己定义线程池：  
> ThreadPoolExecutor: 线程池类  
> 参数：  
> - corePoolSize: 线程池中核心线程数量
> - maximumPoolSize: 线程池中最大线程数量
>   - CPU密集型：最大并行数 + 1
>   - I/O密集型：最大并行数 * CPU期望利用率 * (总时间 / CPU计算时间)
> - keepAliveTime: 线程空闲时间
> - keepAliveTimeUnit: 线程空闲时间单位(TimeUnit的属性)
> - 阻塞队列：ArrayBlockingQueue<>(),可以添加capacity参数
> - 创建线程方式：Executors.defaultThreadFactory()
> - 任务拒绝策略（ThreadPoolExecutor的静态内部类）：
>   - AbortPolicy: 默认策略，任务被拒绝，抛出RejectedExecutionException异常
>   - DiscardPolicy: 丢弃任务，不处理（不推荐用）
>   - DiscardOldestPolicy: 丢弃队列中最旧的任务
>   - CallerRunsPolicy: 调用任务的run方法绕过线程池直接执行

# 十六、网络编程
C/S架构：客户端/服务器  
B/S架构：浏览器/服务器  

## 16.1 网络编程三要素
> IP：设备在网络中的地址，是唯一的标识  
> 端口号：应用程序在设备中的唯一标识  
> 协议：数据在网络中的传输规则，常见的有UDP,TCP,http,https,ftp  

> IP: ipv4和ipv6  
> 特殊IP地址：127.0.0.1(本机IP)

> cmd命令：  
> ipconfig 查看ip  
> ping 检查网络是否连通  

> InetAddress: Java中的表示IP类  
> 包含两个子类：Inet4Address,Inet6Address  
> 获取IP地址：
> - static InetAddress getByName(String host): 根据主机名（IP地址或者机器名称）获取IP地址
> - String getHostAddress(): 获取IP地址字符串
> - String getHostName(): 获取主机名

>端口号：一个端口号只能被一个应用程序占用

>协议：
> - UDP协议：<font color="red">无连接协议</font>，数据不保证传输成功，数据不保证顺序，数据不保证不重复
> - TCP协议：<font color="red">有连接协议</font>，数据保证传输成功，数据保证顺序，数据保证不重复

## 16.2 UDP通信
> **UDP通信程序：**  
> 发送消息步骤：
> 1. 创建发送端的DatagramSocket对象  
>   空参：随机选一个可用端口进行使用  
>   有参：使用指定端口号
>   ``` java
>   DatagramSocket ds = new DatagramSocket();
>   ```
> 2. 数据打包：DatagramPacket(byte[] bytes, int length, InetAddress address, int port)
>   ``` java
>   DatagramPacket dp = new DatagramPacket(bytes, bytes.length, InetAddress.getByName("192.168.1.100"), 10086);
>   ```
> 3. 发送数据: 
>   ``` java
>   ds.send(dp);
>   ```
> 4. 释放资源
>   ``` java
>   ds.close()
>   ```
>
> 接收消息步骤：
> 1. 创建接收端的DatagramSocket对象  
>   ```DatagramSocket ds = new DatagramSocket(10086);```
> 2. 数据解包：DatagramPacket(byte[] bytes, int length)  
>   ``` java
>   byte[] bytes = new byte[1024];
>   DatagramPacket dp = new DatagramPacket(bytes, bytes.length);
>   ```
> 3. 接收数据:  
>   ```ds.receive(dp);```
> 4. 获取数据:  
>   ``` java
>   byte[] data = dp.getData();
>   int len = dp.getLength();
>   InetAddress address = dp.getAddress();
>   int port = dp.getPort();
>   System.out.println("接受的数据：" + new String(data, 0, len));
>   System.out.println("来自：" + address + ":" + port);
>   ```
> 5. 关闭资源：  
>   ```ds.close();```

> **UDP三种通信方式：**  
> 1. 单播  
>   之前所学就是单播
> 2. 组播：地址为224.0.0.0 ~ 239.255.255.255, 其中224.0.0.0 ~ 224.0.0.255为保留地址  
>   实现类：MulticastSocket  
>   实现方法类似于单播，但是要指定组播地址  
>   接收端需要先将本机加入到组播组中
>   
> 3. 广播：地址为255.255.255.255  

## 16.3 TCP通信
> **TCP通信程序：**  
> 客户端：  
> 1. 创建发送端的Socket对象  
>   ```Socket(String host, int port)```
> 2. 获取输出流，发送数据  
>   ```OutputStream getOutputStream()```
> 3. 结束标记(某些情况才需要)  
>   ```socket.shutdownOutput()```
> 4. 释放资源  
>   ```void close()```
>
> 服务器端：  
> 1. 创建服务器端ServerSocket对象  
>   ```ServerSocket(int port)```
> 2. 监听客户端连接，返回一个Socket对象  
>   ```Socket accept()```
> 3. 获取输入流，读数据并在控制台显示  
>   ```InputStream getInputStream()```
> 4. 释放资源  
>   ```void close()```

> [TCP三次握手，四次挥手](https://blog.csdn.net/m0_56649557/article/details/119492899)

> 解决类名重复问题：  
> 类：UUID  
> 方法：static String randomUUID()

# 十六、反射
反射允许对成员变量，成员方法和构造方法的信息进行编程访问  
作用：获取一个类里面的所有信息，获取到之后在执行其他业务逻辑；结合配置文件动态的创建对象并调用方法
含义：从类里面拿出能拿的信息展示出来

## 16.1 获取Class字节码对象
> 三种方式：  
> 1. Class.forName("全类名")
>   - <font color="red">源代码阶段</font>获取字节码对象
>   - 最为常用
> 2. 类名.class
>   - <font color="red">加载阶段</font>获取字节码对象
>   - 当参数：例如同步代码块
> 3. 对象.getClass()
>   - <font color="red">运行阶段</font>获取字节码对象
>   - 需要已经有了这个类的对象

## 16.2 获取Class内部信息
### 16.2.1 获取构造方法(Constructor)
- Constructor< ?>[] getConstructors(): 获取当前类中所有公有构造方法
- Constructor< ?>[] getDeclaredConstructors(): 获取当前类中所有构造方法
- Constructor< T> getConstructor(Class< ?>... parameterTypes): 获取当前类中指定参数的公有构造方法
- Constructor< T> getDeclaredConstructor(Class< ?>... parameterTypes): 获取当前类中指定参数的构造方法

Constructor常用方法：
- setAccessible(boolean flag): 设置是否允许访问(临时)
- Object newInstance(Object... initargs): 创建当前类对象
- int getModifiers(): 获取当前类成员变量的访问权限修饰符
- Parameter[] getParameters(): 获取当前类成员方法的参数列表

### 16.2.2 获取成员变量(Field)
- Filed[] getFields(): 获取当前类中所有公有成员变量
- Filed[] getDeclaredFields(): 获取当前类中所有成员变量
- Filed getField(String name): 获取当前类中指定名称的公有成员变量
- Filed getDeclaredField(String name): 获取当前类中指定名称的成员变量

Field常用方法：
- setAccessible(boolean flag): 临时设置访问权限
- int getModifiers(): 获取当前类成员变量的访问权限修饰符
- Class< ?> getType(): 获取当前类成员变量的类型
- String getName(): 获取当前类成员变量的名称
- Object get(Object obj): 获取当前类成员变量的值（已知类型可以直接强转）
- void s et(Object obj, Object value): 设置当前类成员变量的值

### 16.2.3 获取成员方法(Method)
- Method[] getMethods(): 获取当前类中所有公有成员方法，包括继承的
- Method[] getDeclaredMethods(): 获取当前类中所有成员方法，不包括继承的
- Method getMethod(String name, Class< ?>... parameterTypes): 获取当前类中指定名称的公有成员方法
- Method getDeclaredMethod(String name, Class< ?>... parameterTypes): 获取当前类中指定名称的成员方法

Method常用方法：
- setAccessible(boolean flag): 临时设置访问权限
- int getModifiers(): 获取当前类成员方法访问权限修饰符
- Class< ?> getReturnType(): 获取当前类成员方法返回值类型
- Class< ?>[] getParameterTypes(): 获取当前类成员方法参数列表
- Parameter[] getParameters(): 获取当前类成员方法参数列表
- String getName(): 获取当前类成员方法名称
- Object invoke(Object obj, Object... args): 调用方法并得到返回值

## 16.3 动态代理
Proxy类提供了为对象产生代理对象的方法  
方法：`public static Object newProxyInstance(ClassLoader loader, Class< ?>[] interfaces, InvocationHandler h)`   
创建方法：  
``` java
Star star = (Star)Proxy.newProxyInstance(
    ProxyUtils.class.getClassLoader(),  // 哪个类指定加载器
    new Class[]{Star.class},   // 指定接口
                // 要干啥
    new InvocationHandler() {
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 代理对象
        // 要运行的方法
        // 方法的参数
        if("sing".equals(method.getName())){
            System.out.println("准备话筒，收钱");
        }else if("dance".equals(method.getName())){
            System.out.println("准备场地，收钱");
        }
        return method.invoke(bigStar, args);
    }
});
```