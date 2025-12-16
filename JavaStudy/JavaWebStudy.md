# 一、JavaWeb开发介绍
前端程序 + 服务端程序 + 数据库  

1. 前端程序：HTML CSS JavaScript
2. 服务端程序：Java
3. 数据库：MySQL

[学习文档](https://developer.mozilla.org/zh-CN/docs/Web)  
[线上讲义](https://heuqqdmbyk.feishu.cn/wiki/LYVswfK4eigRIhkW0pvcqgH9nWd)

# 二、HTML-CSS-JS
HTML用来控制页面结构，CSS用来控制页面样式，JS用来控制页面行为。  

## 2.1 HTML
常见标签：
> 标题标签：h1-h6   
> 超链接: \<a href="" target="_blank/_self(默认值)">\</a>    
> 图片标签: \<img src="" alt="">\</img>  
>   - src: 图片路径（绝对路径/相对路径）
>   - alt: 图片描述
>   - width/height: 图片大小（px / %）
> 
> 视频标签: \<video src="" controls width/height="" autoplay>\</video>
>   - controls：显示播放控件  
>   - width, height：设置宽高（只设置一个，另一个等比例缩放）  
>   - autoplay：自动播放  
>   - src: 视频源  
> 
> 音频标签: \<audio src="" controls autoplay>\</audio>
> 无语义标签(盒子模型): div span  
>   - div一行只显示一个，span可以显示多个
> 
> 输入输出标签: input output    
> 字体类型标签：通常使用后者  
>   - 加粗：b strong  
>   - 下划线：u ins
>   - 倾斜：i em
>   - 删除线：s del
>   - 字符实体：空格：&nssp; <：\&lt; >：\&gt;
>
> 表单标签：form
>   - action: 提交地址（URL）
>   - method: 提交方式（GET(default), POST）
>     - get: 有隐私数据不推荐，不适合提交大数据批量表单
>     - post: 安全，大小没限制
>   - 注意：表单里面的表单项必须要有<font color="red">name</font>属性
> 
> 表单项标签：
>   - input: 通过type(text, password, radio, checkbox, file, hidden, data/time/datetime-local, 
>     submit/reset/button)控制输入形式
>   - textarea: 
>   - select(下拉列表): option标签定义列表项
>   - 提升用户体验可以使用<font color="red">label</font>标签来包裹某一表单项
>
> 表格标签(table)：
>   - 表头：thead th
>   - 表格主体：tbody tr(表格的行，可包含多个td) td
> 
> 页脚标签：footer

盒子模型：
> - margin: 外边距(margin-top margin-right margin-bottom margin-left)(上下 左右)(上右下左)
> - border: 边框(line-width line-style line-color)
> - padding: 内边距
> - content: 内容

弹性布局(flex):  
> 是一个以为布局模型，可以设置多个子元素，子元素会自动排布  
> - 弹性容器：display: flex;
> - 设置主轴：flex-direction: row(default)   column;
> - 子元素对齐方式：justify_content
>   - flex-start(default)
>   - flex-end
>   - center
>   - space-around
>   - space-between

## 2.2 CSS
引入方式：
> 行内样式：写在标签的style属性中(配合JavaScript使用)  
> 内部样式：写在head标签中(在head中加入\<style>\</style>)  
> 外部样式：写在一个单独的.css文件中(需要通过link标签引入)  
>   `<link rel="stylesheet" href="">`

颜色表示方式：
> 16进制: #000000  
> RGB: rgb(0,0,0)  
> 颜色名称: black  
> rgba: rgba(0,0,0,0.5), a表示透明度(0-1)  

CSS选择器：  
> 元素选择器：直接写元素名(span, h1...)  
> ``` css
> <style>
>     元素名{
>         color:gray;
>     }
> </style>
> ```
> id选择器：#id属性值  
> ``` css
> <style>
>     #id名{
>         color:gray;
>     }
> </style>
> ```
> class选择器：.class属性值  
> ``` css
> <style>
>     .class名{
>         color:gray;
>     }
> </style>
> ```
> 优先级：id > class > 元素  
> 分组选择器：选择器1，选择器2，选择器3...{样式}  
> 属性选择器：
>   - 元素名称\[属性]{...}
>   - 元素名称\[属性名="值"]{...}  
> 
> 后代选择器：元素1 元素2{...}, 表示元素1的子元素元素2  

## 2.3 JS
组成：ECMAScript + BOM + DOM  

内部引入：JS需要包裹在script标签包裹，写在body最下面  
外部引入：写在外部js文件中，用script标签引入  
``` html
<script src="js/demo.js"></script>
```
常用输出函数：  
> alert() 弹出框  
> console.log() 输出到控制台  
> document.write() 输出到页面(不常用)  

变量申明（弱类型语言，直接用let）：  
> 声明变量：```let 变量名 = 值;```  
> 声明常量：```const 变量名 = 值;```

数据类型：
> 可以使用typeof运算符来获取数据类型  
> 基本数据类型：  
> - number: NaN也是
> - boolean
> - null
> - undefined
> - string: 双引号、单引号和反引号(推荐单引号)  
>   反引号字符串通常作为模板字符串使用，模板字符串中可以包含变量，变量会自动替换。  
>   e.g:   
>   ``` JavaScript
>   let name = 'Tom'
>   let age = 18
>   console.log(`${name} is ${age} years old`)
>   console.log(name + ' is ' + age + ' years old')
>   ```
> 
> 引用数据类型：  
> 

函数(function)：  
> 语法：  
> ``` JavaScript
> // 具名函数
> function 函数名(参数1, 参数2, ...){
>     函数体
>     return 函数返回值
> }
> 
> // 匿名函数
> // add为函数名，a b为参数
> let add = function(a, b){
>     return a + b
> }
> 
> let add = (a, b) => {
>     return a + b
> }
> 
> let add = (a, b) => a + b
> ```

自定义对象：
> 语法：    
> ``` JavaScript
> let 对象名 = {
>     属性1: 属性值1,
>     属性2: 函数1,
>     属性3: 函数2,
>     方法名: function(参数1, 参数2, ...){}
> }
> // 方法中要是要调用属性，则用this.属性名
> ```

JSON: 
> json: 数据载体  
> 解析: JSON.parse(json)  
>   - 作用是把json解析为对象
> 构建: JSON.stringify(json)  
>   - 作用是把对象构建为json

DOM: 
> [学习文档](http://w3school.com.cn/index.html)  
> 概念：文档对象模型    
> 将标记语言的各个部分封装为对象：
>   - Document: 整个文档对象
>   - Element: 元素对象（每个标签）
>   - Attribute： 属性对象
>   - Text: 文本对象
>   - Comment: 注释对象
>
> 获取DOM对象
> - document.querySelector(selector)
> - document.querySelectorAll(selector): 返回一个NodeList节点集合，是一个伪数组

事件监听：  
> 语法：`事件源.addEventListener(事件类型, 事件触发执行的函数)`  
> - 事件源：那个dom元素触发了事件，要获取dom元素对象
> - 事件类型：鼠标单击(click)等
> - 事件触发执行的函数：要做什么事(一个函数)
> - 绑定多个事件会都执行
>
> 早期方式：`事件源.onclick = function(){...}`
> - 缺点：只能绑定一个事件,后绑定的事件会覆盖先绑定的事件
>
> 常见事件：
> - 鼠标：click, mouseenter, mouseleave
> - 键盘事件：keydown, keyup
> - 焦点事件：focus, blur
> - 表单事件：submit, input

程序优化：
> 引用其他js文件中的函数：
> - 方式：`import {函数名} from '文件路径'`
> - 一个函数能被其他js文件引用需要在前面添加export
> - html引用js文件要加上属性`type="module"`

# 三、vue3和Ajax
[官方文档](https://cn.vuejs.org/)  
Vue是一款构建用户界面的渐进式的JavaScript框架  
优点：大大提升前端项目的开发效率  
缺点：需要理解记忆框架的使用规则  

## 3.1 vue快速使用  
使用官方框架
> ``` html
> <div id="app">
>     <h1>{{message}}</h1>
> </div>
> <script type="module"> 
> import {createApp} from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
> createApp({
>     data(){
>         return{
>             message: "Hello Vue"
>         }
>     }
> }).mount("#app")
> </script>
> ```
> 注意点:
> - 导包并设置模块类型为module
> - 使用createApp创建app
> - 引用数据用{{message}}
> - 指定容器(div)：使用mount方法指定要接管的容器

## 3.2 vue常用指令
指令：HTML标签上带有v-xxx的特殊属性，不同的指令有不同的含义，可以实现不同的功能   
常用指令：
> v-for: 列表渲染，遍历容器的元素或者对象的属性  
> - 语法：`v-for="(item, index) in items" :key="item.id"`
> 
> v-bind: 为html标签绑定属性值，如设置href,css样式  
> - 语法：`v-bind:属性名="值"`
> - 简化：`:属性名="值"`
> - 这里的值不需要加{{ }}
> 
> v-if/v-else-if/v-else: 条件渲染, 满足条件则显示，否则不显示  
> - 满足条件则显示，否则不显示
> - e.g: `<div v-if="item.xxx == xx">...</div>`
> 
> v-show: 根据条件展示某元素，区别在于切换的是display属性的值  
> - 全部都会渲染，只不过只有满足条件的元素会显示
>
> v-model: 双向数据绑定(方便获取和设置表单项数据)，将数据绑定到表单，用户输入数据后，数据会自动更新
> - 先在Vue的createApp里面添加对象再在标签里面绑定
> - e.g: `<input v-model="searchForm.name">`
> 
> v-on: 绑定监听事件，如click, blur, mouseenter, mouseleave  
> - 语法：`v-on:事件名="方法名"`
> - 可以简写为`@事件名="方法名"`
> - 在createApp的data同级加上methods,在里面写事件的方法

## 3.3 Ajax
Axios: [学习文档](https://axios-http.cn/docs/intro)  
使用步骤：  
- 引入Axios的js文件(`<script src=https://unpkg.com/axios/dist/axios.min.js></script>`)
- 使用Axios发送请求，并获取响应数据
``` JavaScript
axios({
    method: 'GET',
    url: ''
}).then((result)=>{
    console.log(result.data)
}).catch((err)=>{
    alert(err)
})
```
- 若是POST还需要加入参数data
- Axios简化代码  
```  JavaScript
axios.get('', ...).then((result)=>{
    console.log(result.data)
}).catch((err)=>{
    alert(err)
})
```
- async 声明异步方法，await等待异步任务执行
``` JavaScript
async search(){
    let result = await axios.get('', ...)
    this.list = result.data.data
}
```

八个生命周期方法(钩子):
> - beforeCreate: 创建之前
> - created: 创建之后
> - beforeMount: 挂载之前
> - mounted: 挂载完成
> - beforeUpdate: 更新之前
> - updated: 更新完成
> - beforeUnmount: 组件销毁之前
> - unmounted: 组件销毁完成

# 四、Maven
Maven: [学习文档](https://maven.apache.org)
安装步骤：  
- jdk21
- Maven 3.9+
- 配置Java和Maven全局环境变量
- 更改idea中配置(全局配置，包括setting.xml和repository)

Maven坐标：
> groupId: 唯一标识符，一般使用域名倒序，如com.example  
> artifactId: 项目名称，一般使用项目名
> version: 版本号（SNAPSHOT/RELEASE）

导入Maven模块：
> 方法一：
> - 拷贝项目到目录下
> - 在project structure中添加Maven模块
> - 导入的时候选择<font color="red">pom.xml</font>导入  
> 
> 方法二：
> - idea右边菜单中添加Maven模块

依赖配置：
> 官方网站：[Maven仓库](https://mvnrepository.com)  
> 最外层使用<font color="red">dependencies</font>标签  
> 每一个依赖使用<font color="red">dependency</font>标签包裹  
> 内部包含groupId, artifactId, version三个标签  
> 排除依赖使用<font color="red">exclusions</font>标签包裹  
> 依赖范围使用<font color="red">scope</font>标签包裹，包含compile(default)/test/provided/runtime

单元测试(JUnit)：
> 类名称必须以Test结尾，方法名称必须以test开头    
> 方法必须是public void  
> 使用断言进行测试(Assertions.assertXxxx())  
> 常见注解：  
> - @BeforeEach: 每个测试方法执行之前执行
> - @AfterEach: 每个测试方法执行之后执行
> - @BeforeAll: 所有测试方法执行之前执行
> - @AfterAll: 所有测试方法执行之后执行
> - @Test: 测试方法
> - @ParameterizedTest: 参数化测试(此时不需要@Test注解)  
>   @ValueSource: 参数源
>   ``` Java
>   @ParameterizedTest
>   @ValueSource(strings = {"121313", "123143", "12312"})
>   public void testXxxx(String str){
>       方法体;
>   }
>   ```
> - @DisplayName("xxx"): 测试方法名称

# 五、Spring
Spring: [官网](https://spring.io/)  
<font color="red">三层架构</font>：Controller - Service - DAO  
> Controller：类要加上@RestController注解, 方法要加上@RequestMapping("/xxx")注解  
> 拆分后使用接口以及接口实现类(XxxxImpl)来进行模块化  
> 分层解耦：使用容器管理各个对象(控制反转IOC和依赖注入DI)，IOC创建和管理的对象称为Bean对象  
> 分层解耦要管理的类加上注解@Component,管理的对象添加@Autowired注解   
> 依赖注入(@Autowired注解)有三种方法：   
> - 构造器注入(10%)
> - 属性注入(90%)
> - setter注入

Component衍生注解:  
> Service：业务层  
> Controller：控制层  
> Repository：数据访问层  

多种依赖注入解决方法：
> 由于依赖注入通过接口多态实现，当实现类不是单一的则会报错  
> 解决方法：
> - @Primary注解：指定默认实现类(在默认实现类前加入该注解)  
> - @Qualifier("xxxImpl")注解：指定实现类的Bean类(在管理的对象处添加该注解)  
> - @Resource(name = "xxxImpl")注解：指定实现类的Bean类(首字母小写)(在管理的对象处添加该注解)
> - @Resource注解融合了@Autowired和@Qualifier注解

Controller参数传递：
> 方法1：HttpServletRequest,调用request.getParameter("参数名")获取参数  
> 方法2：<font color="yellow">@RequestParam(value = "参数名",required = true, defaultValue = "默认值")</font>注解,required表示接受参数时是否必须提供该参数，默认为true  
> 方法3：将请求参数名和形参变量名书写一致后可以直接接收(<font color="lightblue">推荐</font>)    
> <font coloe="yellow">@RequestBody</font>注解：将请求体中的数据(JSON)映射为对象  
> 接收路径参数：@PathVariable("参数名")

Controller路径：
> @PostMapping("/xxx"): 用来指定POST请求（增）  
> @GetMapping("/xxx"): 用来指定GET请求（查）  
> @PutMapping("/xxx"): 用来指定PUT请求（改）  
> @DeleteMapping("/xxx"): 用来指定DELETE请求（删）  
> @RequestMapping("/xxx"): 用来指定上述4种方法的共有路径，放在Controller类前  

日志技术：
> 日志记录对象Logger: `private static final Logger log = LoggerFactory.getLogger(LogTest.class);`  
> 日志级别：trace < debug < info < warn < error  
> 也可以使用lombok的@Slf4j注解  

<font color="yellow">@Value</font>注解：
> 这个注解用于获取配置文件中的属性值  
> 当使用这个注解太多可以创建一个实体类使用<font color="yellow">@ConfigurationProperties(prefix = "xxx")</font>注解

全局异常处理：
> 创建一个类GlobalExceptionHandler类并添加<font color="yellow">@ControllerAdvice</font>注解  
> 添加方法时加上<font color="yellow">@ExceptionHandler</font>注解


# 六、MySQL
DQL:
> 完整句式：  
> ``` mysql
> select 
>     字段列表
> from
>     表名列表
> where
>     条件列表
> group by
>     分组字段列表
> having
>     分组后的条件列表
> order by
>     排序字段列表
> limit
>     分页参数
> ```
> 
> 注意：
> - where不能有聚合函数，having可以有聚合函数  
> - 有了group by之后查询字段只能是聚合字段或者分组字段  
> - distinct：去重  
> 
> 字符串拼接：concat    

动态SQL:
> 语法：`<where><if test="条件">SQL语句</if></where>`  
> where标签是方便自动识别多余的and  
> if标签条件为true则拼接SQL语句  
> set标签可以识别多余的逗号  
> `<foreach collection="集合" item="元素" separator=",">`标签：  

SQL流程控制:  
> `case when cond1 then res1[when cond2 then res2]...[else res] end`  
> `if(gender=1, "男", "女")`
 
JDBC:
> 注册驱动：`Class.forName("com.mysql.cj.jdbc.Driver")`  
> 获取数据库连接：
> - `String url = "jdbc:mysql://localhost:3306/databaseName";`
> - `String username = "root";`
> - `String password = "root";`
> - `Connection conn = DriverManager.getConnection(url, username, password);`
> 
> 获取SQL语句执行对象：`Statement stmt = conn.createStatement()`  
> 执行SQL语句：`int i = stmt.executeXxxx(SQL语句)`
> 释放资源：
> - `stmt.close()`
> - `conn.close()`
> 
> 预编译SQL语句：
> - `PreparedStatement pstmt = conn.prepareStatement(SQL语句)`
> - `pstmt.setXxx(参数索引, 参数值)`

Mybatis: [官网](https://mybatis.org/mybatis-3/zh_CN/index.html)  
> XxxMapper接口放在src/main/java/mapper下，在接口前加上注解@Mapper  
> 
> ## 使用Mybatis要设置的配置文件：
> ``` properties
> # 配置数据库连接信息
> spring.datasource.url=jdbc:mysql://localhost:3306/web01
> spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
> spring.datasource.username=root
> spring.datasource.password=root
> 
> # mybatis的配置
> mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
> ```
> 
> 底层使用数据库连接池，实现了连接复用(类似线程池的线程复用)   
> 
> 切换数据库连接池：  
> ``` xml
> <dependency>
>     <groupId>com.alibaba</groupId>
>     <artifactId>druid-spring-boot-starter</artifactId>
>     <version>1.2.19</version>
> </dependency>
> ```
> ``` properties
> spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
> ```
> 
> ## 查询用户列表：
> ``` java
> @Select("select * from user")
> public List<User> findAll();
> 
> //传递多个形参使用@Param，此时#{}里面传递的是@Param注解的值
> @Select("select * from user where username=#{username} and password=#{password}")
> public User findByUsernameAndPassword(@Param("username") String username,@Param("password") String password);
> ```
> <font color="lightblue">注意: </font>若是基于官方骨架创建的springboot项目，则@Param可以省略  
> 删除用户：
> ``` java
> @Delete("delete from user where id = #{id}")
> public int deleteById(Integer id);
> ```
> 添加用户：
> ``` java
> //主键返回
> @Options(useGeneratedKeys = true,keyProperty = "id")
> // values里面的是User的属性名
> @Insert("insert into user(username,password,name,age) values(#{username},#{password},#{name},#{age})")
> public Integer insert(User user);
> ```
> 更新用户：
> ``` java
> // 同样是属性值
> @Update("update user set username=#{username},password=#{password},name=#{name},age=#{age} where id=#{id}")
> public Integer update(User user);
> ```
> 
> <font color="red">注意</font>：
> - #{...}为占位符，执行时会替换为'?', 生成预编译SQL,应用于参数值传递
> - ${...}为拼接符，把参数拼接在SQL语句中，用于表名、字段名动态设置
> 
> ## XML映射配置：  
> 除了上述的注解方式，还可以使用XML映射配置来配置SQL语句
> 默认规则:
> - XML文件名称与Mapper接口名称一致，并放在resource下同包名中
> - XML文件中namespace属性与Mapper接口全限定名一致
> - XML中SQL语句的id与Mapper接口中方法名一致并保持返回类型一致
> 
> 应用场景：简单增删查改用注解，复杂查询用XML映射配置  
> 自定义mapper的xml文件路径：`mybatis.mapper-locations=classpath:mapper/*.xml`
> 
> ## Mybatis<font color="red">数据封装</font>： 
> - 对于名字相同的属性，Mybatis会自动封装成对象
> - 不同的需要使用注解：`@Results({@Result(column,property)})`  
> - 也可以在SQL语句处起别名来实现
> - <font color="lightblue">开启驼峰命名转换</font>：`mybatis.configuration.map-underscore-to-camel-case=true`
> 
> ## 分页查询插件：PageHelper
> PageHelper是Mybatis的一个分页插件，使用PageHelper插件后，只需要在查询方法前添加PageHelper.startPage(pageNum, pageSize)即可实现分页功能
> 步骤：
> - 添加依赖
> ``` xml
> <dependency>
>     <groupId>com.github.pagehelper</groupId>
>     <artifactId>pagehelper-spring-boot-starter</artifactId>
>     <version>1.4.7</version>
> </dependency>
> ```  
> - 调用PageHelper：`PageHelper.startPage(pageNum, pageSize);` 
> - 封装Mapper结果： `Page<T> page = (Page<T>)mapper.list();`
> - 调用方法：`page.getTotal() page.getResult()`
> 
> 细节：  
> - SQL语句结尾不能加分号  
> - 只对紧跟的第一次查询有分页效果  
> 
> ## 封装表格数据：
> 会每一行封装成一个Map<String, Object>,用List<Map<String, Object>>接收就可以了  

Mybatis自定义封装数据：
``` xml
<resultMap id="empWithExprMap" type="Emp">
    <id property="id" column="emp_id"/>
    <!-- 其他emp字段映射,使用result -->
    <result property="name" column="emp_name"/>
    <collection property="exprList" ofType="EmpExpr">
        <id property="id" column="expr_id"/>
        <!-- 其他expr字段映射,使用result -->
        <result column="ee_empid" property="empId"/>
    </collection>
</resultMap>

<select id="selectEmpWithExpr" resultMap="empWithExprMap">
    SELECT e.*, ex.* 
    FROM emp e LEFT JOIN emp_expr ex ON e.id = ex.emp_id
    WHERE e.id = #{id}
</select>
```

SpringBoot配置文件：
> 常见配置文件有properties、yaml和yml  
> 通常使用yml，其有清晰的层级结构  
> yml配置文件(若是配置项的值为0开头的数字，则需要加引号)
> ``` yml
> # 定义对象/Map集合
> user:
>   name: Tom
>   age: 18
>   gender: 男
> 
> # 定义数组/List/Set集合  
> hobby:
>   - java
>   - sing
>   - sport
>   - game
> ```

事务管理：  
> 事务：一个业务操作，多个SQL语句，多个对象操作组成的一个不可分割的工作单位  
> 注解：<font color="yellow">@Transactional</font>   
> 位置：服务层方法上(常用)、类上、接口上，一般加在多个操作的方法上  
> 默认运行时异常才会回滚，可以加上属性`rollbackFor = Exception.class`  
> 传播行为：propagation  
> - REQUIRED: 支持当前事务，如果不存在则创建一个新的事务  
> - REQUIRES_NEW: 创建一个新的事务，如果存在则挂起原事务  
>
> 四大特性：ACID,原子性，一致性，隔离性，持久性  

# 七、登录  

## 7.1 登录校验：  

三种会话跟踪：  
- Cookie:  
> 原理：请求头(Cookie) 响应头(Set-Cookie)  
> 优点：Http协议中支持的技术  
> 缺点：不安全，用户可以禁用自己的Cookie；移动端APP无法使用Cookie；Cookie不能跨域  
- Session:
> 原理：底层使用Cookie(Set-Cookie, Cookie)  
> 优点：安全，存储在服务端  
> 缺点：Cookie的缺点；服务器集群环境下无法直接使用Session  
- <font color="red">Token(令牌)</font>:  
> 优点：支持PC端、移动端；解决集群环境下的认证问题；减轻服务器端存储压力  
> 缺点：只能自己实现  

JWT令牌：[官网](https://jwt.io/)  
> JWT令牌：JSON Web Token  
> 组成：Header(头), Payload(有效载荷), Signature(签名)  
> 生成令牌:  
> ``` java
> String jwt  = Jwts.builder().signWith(SignatureAlgorithm.HS256, "eGlhb21pbmc=")  //指定加密算法，密钥
>           .addClaims(dataMap) // 添加自定义信息
>           .setExpiration(new Date(System.currentTimeMillis() + 3600 * 1000))  // 设置过期时间
>           .compact();//  compact()方法生成jwt
> ```
> 解析令牌：  
> ``` java
> Claims claims = Jwts.parser().setSigningKey("eGlhb21pbmc=")
>           .parseClaimsJws(token)
>           .getBody();
> ```

令牌校验(Filter):  
> 步骤：  
> 1. 编写接口Filter的实现类  
> 2. 实现类前加上<font color="yellow">@WebComponent(urlPatterns = "/*")</font>注解  
> 3. 启动类添加注解<font color="yellow">@ServletComponentScan</font>  
> 4. 实现抽象方法doFilter()  
> 
> 当执行完访问对应资源后，会回到Filter的doFilter()方法

令牌校验(Interceptor):  
> 拦截器：
> 步骤：  
> 1. 定义拦截器: 实现HandlerInterceptor接口并实现所有方法(在实现类前添加注解<font color="yellow">@Component</font>)
> 2. 注册拦截器: 新建包config并实现<font color="red">创建配置类WebConfig</font>(接口WebMvcConfigurer的实现类)
> 3. WebConfig中添加方法addInterceptors()来添加拦截器  
> 
> /*只拦截以及路径，/**会拦截所有路径  
> <font color="lightblue">Filter和Interceptor区别</font>：  
> - 接口规范不同：一个是实现接口Filter，一个实现接口HandlerInterceptor  
> - 拦截范围不同：Filter是拦截所有请求，Interceptor是只拦截Spring环境中的资源  

# 八、AOP编程  

AOP：Aspect Oriented Programming(面向切面编程)  
作用：面向特定方法编程  
场景：多个方法需要相同的功能，比如日志记录、权限控制、事务处理等，这时就可以使用AOP编程  
优势：减少重复代码，提高开发效率，代码无侵入，维护方便  

example：
``` java
@Slf4j
@Aspect
@Component
public class RecordTimeAspect {

    @Around("execution(* com.itheima.service.impl.*.*(..))")
    public Object recordTime(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("记录方法执行时间");
        long begin = System.currentTimeMillis();

        Object result = pjp.proceed();

        long end = System.currentTimeMillis();
        log.info("方法{}执行耗时：{}ms", pjp.getSignature(), end - begin);
        return result;
    }
}
```

AOP核心概念：  
> JoinPoint：连接点，即可以被AOP控制的方法  
> Advice: 通知，即AOP要执行重复操作的方法  
> Pointcut：切入点，即AOP要拦截的连接点(注解<font color="yellow">@Around</font>里面的表达式)  
> Aspect: 切面，即AOP要执行的通知和连接点  
> Target: 目标对象，即被AOP控制对象(Impl)  

AOP通知类型：
> <font color="yellow">@Around</font>：环绕通知，即AOP要执行的通知方法,在目标方法执行前后执行  
> <font color="yellow">@Before</font>：前置通知，即AOP要执行的通知方法,在目标方法执行前执行  
> <font color="yellow">@After</font>：后置通知，即AOP要执行的通知方法,在目标方法执行后执行(无论是否异常)  
> <font color="yellow">@AfterReturning</font>：返回通知，即AOP要执行的通知方法,在目标方法返回后执行(正常返回)  
> <font color="yellow">@AfterThrowing</font>：异常通知，即AOP要执行的通知方法,在目标方法抛出异常后执行(异常返回)  
> 执行顺序: 
> - 不同切面类中根据类名字母排序：Before是字母小的先执行，After是字母大的先执行
> - 也可以使用<font color="yellow">@Order(数字)</font>指定执行顺序：Before数字越小越先执行，After数字越大越先执行
> 
> 注意：
> - <font color="red">@Around</font>是最常用的通知类型，其他通知类型也可以实现，但@Around是最常用的  
> - @Around需要调用proceed()方法，表示调用目标方法  
> - @Around环绕通知方法的返回值必须指定为Object来接收原始方法的返回值  
> 
> <font color="yellow">@PointCut</font>: 设置公共切入点表达式  
> ```  java
> @Pointcut("execution(* com.itheima.service.impl.*.*(..))")
> public void pointCut(){}
> 
> @Around("pointCut()")
> public Object recordTime(ProceedingJoinPoint pjp) throws Throwable { 
>     方法体
> }
> ```

切入点表达式：  
> 常见形式：execution(返回值类型 包名.类名.方法名(参数列表)), @annotation(全类名)  
> execution:
> > \* 表示单个独立的符号，也可以匹配包名、类名、方法名的一部分  
> > .. 表示多个连续的任意符号，可以匹配任意层级的包或者任意类型、任意个数的参数  
> > 根据业务需要加入&& || !来组合复杂的切入点表达式  
> 
> @annotation(全类名)：
> > 1. 构建一个注解类  
> > ``` java
> > @Target(ElementType.METHOD)
> > @Retention(RetentionPolicy.RUNTIME)
> > public @interface LogOperation {
> > }
> > ```
> > 2. 在通知里添加@annotation(注解类的全类名)  
> > 3. 在需要的方法前面添加自己定义的注解  

连接点：
> Spring中用JointPoint抽象了连接点，用这个可以获取连接点信息，如类名、方法名、参数、返回值、异常等信息  
> 对于@Around通知获取连接点信息只能使用<font color="red">ProceedingJoinPoint</font>  
> 其他四种通知只能使用JoinPoint，是ProceedingJoinPoint的父类  
> JoinPoint方法：  
> > getTarget()：获取目标对象  
> > getTarget().getClass().getName(): 获取目标对象类名  
> > getSignature()：获取方法签名  
> > getSignature().getName(): 获取方法名  
> > getArgs()：获取参数  

ThreadLocal:  
> 是Thread的局部变量  
> 常用方法：set(T), T get(), remove()

# 九、SpringBoot原理

## 9.1 配置优先级
配置文件优先级：properties > yml(常用) > yaml  
命令行参数 > Java属性 > 配置文件

## 9.2 Bean管理
[//]: # (Bean管理：Spring容器管理Bean，将Bean交给Spring容器管理，Spring容器会自动创建Bean实例并管理Bean的生命周期  )  

作用域(<font color="YELLOW">@Scope("xxx")</font>)：
- singleton(default，单例容器，所有对象都共享一个实例),在项目启动时创建  
  <font color="YELLOW">@Lazy</font>会延时创建Bean实例  
  应用场景(绝大多数都是单例Bean)：无状态的Bean(不保存数据，Controller, Service, Dao均为这类Bean)  
- prototype(多例容器，每次获取的实例都是新的)  
  应用场景：有状态的Bean(保存数据)

管理第三方Bean: 
> 使用<font color="YELLOW">@Bean</font>注解在启动类中定义第三方Bean(不推荐,通常使用配置类来创建第三方Bean)  
> ``` java
> @Bean
> public AliyunOSSOperator aliyunOSSOperator(AliyunOSSProperties aliyunOSSProperties){
>     return new AliyunOSSOperator(aliyunOSSProperties);
> }
> ```

Gson类: 将对象转换为JSON


## 9.3 SpringBoot原理  

起步依赖：Maven的依赖传递  

### 9.3.1 自动配置

实现方案：  
> 方案一：启动类新增注解<font color="YELLOW">@ComponentScan(basePackages = {"xxx","yyy"})</font>并指定扫描的包(一旦配置扫描的包则不会默认扫描，需要手动指定所有要扫描的包)  
> 方案二：启动类新增注解<font color="YELLOW">@Import({xxx.class})</font>并指定要导入的类(普通类、配置类均可)  
> 方案三：创建<font color"RED">ImportSelector</font>的实现类，并实现selectImports方法，返回需要导入的类,再利用方案2添加到启动类中    
> 方案四(常用)：第三方依赖提供注解<font color="YELLOW">@EnableXxx</font>，启动类添加注解即可(这个注解会封装@Import)  

自定义starter:  
> starter包含了起步依赖和自动配置  
> 步骤：
> 1. 创建aliyun-oss-spring-boot-starter模块
> 2. 创建aliyun-oss-spring-boot-autoconfigure模块，在starter中引入该模块  
> 3. 在autoconfigure模块中定义自动配置功能，并定义自动配置文件 META-INF/spring/xxxx.imports  

Maven分模块开发：
> 1. 创建父模块
> 2. 编写子模块
> 3. 父模块引入子模块依赖

Maven的继承：
> 这里的继承是两个工程之间的继承关系，子工程可以继承父工程的配置  
> 父工程(xxx-parent)的打包方式必须为pom(默认的是pom)  
> 子工程pom.xml需要配置继承关系  
> 父工程配置各个子工程<font color="RED">公有的依赖</font>  
> 当子类与与父类有相同依赖时，子类会覆盖父类的依赖   

Maven版本锁定：
> 在父工程内添加`<dependencyManagement>`标签，并添加`<dependency>`标签，锁定版本，子工程仍需引入该依赖但是可以不指定版本  

Maven聚合：  
聚合工程：一般就是项目的父工程   
父工程中添加`<modules>`标签，并添加子工程名称  

私服：  
1. 配置私服的访问用户名/密码( Settings.xml 中的servers中配置)  
2. settings.xml中配置mirror以及profile  
3. 在父工程pom.xml中添加 `distributionManagement` 标签，并添加`repository`、`snapshotRepository` 标签，指定私服地址   


# 十、前端工程化  

前端工程化：模块化 -> 组件化 -> 规范化 -> 自动化  

vue工程化:  
> npm create vue@version  
> npm install  
> npm run dev  

ElementPlus:[官网](https://element-plus.org/zh-CN/)  
> Button, Table, Pagination(分页条), Dialog(对话框), Form(表单), Date Picker(日期选择器), Container(布局容器), Layout(布局)  

Vue Router:[官网](https://router.vuejs.org/zh/guide/)  
- Vue Router是Vue官方的客户端路由解决方案。  
- 客户端路由的作用是在单页应用(SPA)中将浏览器的URL和用户看到的内容绑定起来。
- 当用户在应用中浏览不同页面时，URL会随之更新，但页面不需要从服务器重新加载。   
- <font color="#c00000">嵌套路由</font>: 强制嵌套路由(还可以默认一个子路由redirect)

动态URL和结果解析优化：
> 步骤：新建utils/request.js; 添加url的动态配置(创建axios实例对象并添加baseURL和timeout, 同时添加响应拦截器);
> 异步交互封装到对应的api/xxx.js中; 更改index.vue中请求方式  
> 1. url动态配置  
> ``` js
> import axios from 'axios'
> // 创建axios实例对象
> const request = axios.create({
>   baseURL: 'https://apifoxmock.com/m1/3128855-1224313-default',
>   timeout: 600000
> })
> 
> // 添加响应拦截器
> request.interceptors.response.use(
>   (response) => {
>     return response.data
>   },
>   (error) => {
>     return Promise.reject(error)
>   }
> )
> 
> export default request
> ```  
> 2. 异步交互封装  
> ``` js
> import request from '@/utils/request'
> 
> // 封装异步交互示例
> export const queryAllApi = () => request.get('/depts')
> ```
> 3. 更改index.vue中请求方式
> ``` vue
> import { queryAllApi } from '@/api/dept'
> const search = async () => {
>   const result = await queryAllApi()
>   if(result.code){
>     deptList.value = result.data
>   }
> }
> ```

侦听(watch):
> ``` vue
> watch(destination, (newValue, oldValue) => {})
> ```
> 侦听对象全部属性：加上属性{deep: true}  
> 侦听对象单个属性值：  
> ``` vue
> watch(() => xxx.value.name, (newVal, oldVal => {})
> ```

携带token访问服务器：
> 1. 存储token到哪儿就在哪儿取token
> 2. upload 组件中添加headers属性
> 3. .js之中不能使用useRouter函数

前端项目打包:  
> nginx:[官网](https://nginx.org/)
> 1. build生成dist文件夹
> 2. 下载nginx
> 3. 配置nginx.conf文件
> 4. 把dist文件夹下的东西放到html下
> 命令：nginx.exe -s reload(重载)  nginx.exe -s stop(停止)

# 十一、Docker

常用命令：
> docker pull：拉取镜像  
> docker images：列出所有镜像  
> docker rmi：删除镜像  
> docker build：构建镜像  
> docker save：保存/打包镜像  
> docker load：加载镜像  
> docker push: 推送镜像     
> docker run：创建容器  
> docker start/stop/restart：启动/停止/重启容器  
> docker ps：列出所有容器  
> docker rm：删除容器  
> docker exec：进入容器  
> docker logs：查看容器日志  

核心技术：
> 数据卷挂载  
> 本地目录挂载  
> 自定义镜像(镜像分层): 可以使用Dockerfile帮我们构建镜像  
> 自定义网络  

DockerCompose:  
> 1. 创建docker-compose.yml文件
> 2. docker compose up

# 十二、[设计模式](https://zhuanlan.zhihu.com/p/651451595)

类图：  
- 可见性：public(+)、private(-)、protected(#)
- 属性：可见性 名称: 类型
- 方法：可见性 函数名(参数: 参数类型): 返回值类型

类之间表示方式：
- 关联
  - 单向关联： A -> B（箭头实线）
  - 双向关联： A <-> B（直线）
  - 自关联： A <-> A(指向自身箭头)
- 聚合
  - 整体与部分(成员变量)
  - 空心菱形实线，菱形指向整体
- 组合
  - 强聚合关系，整体不存在则部分对象也不存在
  - 实心菱形实线，菱形指向整体
- 依赖
  - 通过局部变量、方法的参数或者静态方法的调用访问另一个类(被依赖类)
  - 虚线箭头，箭头指向被依赖类
- 继承
  - 父类与子类
  - 实现空心三角箭头，箭头指向父类
- 实现
  - 接口与是实现类
  - 虚线空心三角箭头，箭头指向接口

软件设计原则：  
- 开放封闭原则：对扩展开放，对修改关闭
- 里氏代换原则：子类继承父类时除新增方法外，尽量不重写父类方法
- 依赖倒转原则：抽象与实现分离(对抽象进行编程)；高层模块不能依赖于低层模块
- 接口隔离原则：接口尽量小，接口中方法尽量少
- 迪米特原则：一个对象应该尽可能少地与其他对象发生相互作用(只与关联、聚合和组合对象发生相互作用)
- 合成复用原则：尽量使用组合、聚合，少使用继承

## 12.1 创建者模式  

主要目的是创建对象，将对象的创建与使用分离，将对象的创建过程封装，将对象的创建过程与使用过程解耦。  

### 12.1.1 单例模式
最简单的设计模式之一， 单例模式保证一个类只有一个实例，并提供一个访问它的全局访问点。  
分类： 
- 饿汉式：类加载时创建对象
  - 存在浪费内存
  ``` java
  // 静态成员变量
  public class Singleton {
      private Singleton(){} 
      private static Singleton instance = new Singleton();
      private static Singleton getInstance(){
          return instance;
      }
  }
  // 静态代码块
  public class Singleton {
      private Singleton(){}
      private static Singleton instance;
      static{
          instance = new Singleton();
      }
      private static Singleton getInstance(){
          return instance;
      }
  }
  ```
- 懒汉式：类加载时不会创建对象，首次使用时创建对象
  - 线程不安全
  ``` java
  public class Singleton {
      private Singleton(){}
      private static Singleton instance;
      private static Singleton getInstance(){
          if(instance == null){
              instance = new Singleton();
          }
          return instance;
      }
  }
  // 双重检查锁方式
  public class Singleton {
      private Singleton(){}
      private static volatile Singleton instance;
      private static Singleton getInstance(){
          if(instance == null){
              synchronized (Singleton.class){
                  if(instance == null){
                      instance = new Singleton();
                  }
              }
          }
          return instance;
      }
  }
  // 静态内部类方式
  public class Singleton {
      private Singleton(){}
      private static class SingletonHolder{
          private static final Singleton INSTANCE = new Singleton();
      }
      public static Singleton getInstance(){
          return SingletonHolder.INSTANCE;
      }
  }
  ```
  - [volatile](https://blog.csdn.net/u012723673/article/details/80682208)
- 枚举方式(恶汉式)
  ``` java
  public enum Singleton {
      INSTANCE;
  }
  ```
  - <font color="RED">不考虑浪费内存，使用枚举方式</font>
  - 线程安全且不可能被破坏
- 一般使用懒汉式中的<font color="RED">静态内部类方式</font>

如何破坏单例模式：
- 序列化反序列化
- 反射
- 解决方法
  - 实现readResolve()可以解决序列化反序列化的问题
    ``` java
    public Object readResolve(){
        // 以静态内部类为例
        return Singleton.INSTANCE;
    }
    ```
  - 解决反射的问题可以在私有构造方法中判断，不为空抛异常
    ``` java
    private static boolean flag = false;
    private Singleton(){
        synchronized (Singleton.class){
            if(flag){
                throw new RuntimeException("单例对象已存在");
            }
            flag = true;
        }
    }
    ```

### 12.1.2 工厂模式(Factory)  
主要是创建对象，将对象的创建与使用分离，将创建过程封装，将创建过程与使用过程解耦。  
常见例子：使用到`getXxxInstance()`一般都会用到这个思想  
简单工厂模式：缺点是还需要修改工厂类，增加新的产品类时需要修改工厂类。违背开闭原则  

工厂方法模式：
- 组成：抽象工厂、具体工厂、抽象产品、具体产品
- 缺点：每增加一个产品类，就需要增加一个具体工厂类，增加了系统复杂度

抽象工厂模式：产品等级(同一类型)、产品族(同一品牌)。将品牌作为工厂，一个工厂生产多个不同产品  
缺点：当产品族新增产品时所有工厂都需要修改  
 
模式扩展：通过在配置文件中配置具体类(全类名)解除工厂对象和产品对象的耦合
```java
public class CoffeeFactory{
    private static Map<String, Coffee> map = new HashMap<>();
    
    static {
        Properties properties = new Properties();
        // 加载配置文件
        InputStream is = CoffeeFactory.class.getClassLoader().getResourceAsStream("bean.properties");
        try{
            p.load(is);
            // 从p集合中获取全类名并创建对象
            Set<Object> keys = p.keySet();
            for(Object key : keys){
                String className = p.getProperty(key.toString());
                // 通过反射创建对象
                Class clazz = Class.forName(className);
                Coffee coffee = (Coffee) clazz.newInstance();
                // 存到map中
                map.put((String) key, coffee);
            }
        }catch (Exception e){
            e.printStackTrace();
        }
    }
    
    public static Coffee createCoffee(String name){
        return map.get(name);
    }
}
```

### 12.1.3 原型模式
原型模式：以一个创建的实例为原型，通过复制该对象，创建新的对象

组成：抽象原型类(规定必须实现clone()方法)、具体原型类(实现clone()方法)、访问类(使用clone()方法)  
本质上是一个浅拷贝，属性是(String, 包装类, LocalDate...)不会出现交叉污染，但是引用类型会出现交叉污染  

使用场景：对象创建复杂；性能和安全要求高。  

### 12.1.4 建造者模式(Builder)
建造者模式：将复杂对象的构建与表示分离，使得同样的构建过程可以创建不同的表示  
组成：抽象建造者 、具体建造者、指挥者、产品  

使用场景：对象创建复杂，由多个不见构成，各部件面临复杂的变化；创建对象的算法独立于该对象的组成各部分和装配方式  

模式扩展：静态内部类实现Builder
```java
public class Phone{
    private String cpu;
    private String screen;
    private String memory;
    private String mainboard;
    // 私有化构造方法
    private Phone(Builder builder){
        this.cpu = builder.cpu;
        this.screen = builder.screen;
        this.memory = builder.memory;
        this.mainboard = builder.mainboard;
    }
    
    public static class Builder{
        private String cpu;
        private String screen;
        private String memory;
        private String mainboard;
        
        public Builder setCpu(Strign cpu){
            this.cpu = cpu;
        }
        
        public Builder setScreen(Strign screen){
            this.screen = screen;
        }
        
        public Builder setMemory(Strign memory){
            this.memory = memory;
        }
        
        public Builder setMainboard(Strign mainboard){
            this.mainboard = mainboard;
        }
        
        public Phone build(){
            // 静态内部类调用外部类私有构造方法
            return new Phone(this);
        }
    }
}

public class Client{
    public static void main(String[] args) {
        Phone phone = new Phone.Builder()
                .setCpu("Intel")
                .setScreen("OLED")
                .setMemory("16G")
                .setMainboard("华硕")
                .build();
        System.out.println(phone);
    }
}
```

## 12.2 结构型模式
### 12.2.1 代理模式(Proxy)
代理模式：给某一个对象提供一个代理以控制对该对象的访问。分为静态代理和动态代理  

组成：抽象主题类(通过接口/抽象类声明真实主题和代理之间要实现的业务方法)、
真实主题类(实现具体业务，是代理对象所代表的真实对象)、代理类  

静态代理：火车站卖票
```java
public interface SellTickets{
    void sell();
}

public class TrainStation implements SellTickets{
    @Override
    public void sell(){
        System.out.println("火车站卖票");
    }
}

public class ProxyPoint implements SellTickets{
    private TrainStation trainStation = new TrainStation();
    
    @Override
    public void sell(){
        System.out.println("代理点收取一些服务费用");
        trainStation.sell();
    }
}

public class Client{
    public static void main(String[] args) {
        ProxyPoint proxyPoint = new ProxyPoint();
        proxyPoint.sell();
    }
}
```

JDK动态代理：同上例子
```java
public interface SellTickets{
    void sell();
}

public class TrainStation implements SellTickets{
    @Override
    public void sell(){
        System.out.println("火车站卖票");
    }
}

public class ProxyFactory{
    private TrainStation trainStation = new TrainStation();
    public SellTickets getProxyInstance(){
        /*
            ClassLoader loader: 类加载器，用于加载代理类。可以通过目标对象获取类加载器
            Class<?>[] interfaces: 代理类实现的接口的字节码对象
            InvocationHandler handler: 代理对象的调用处理程序
         */
        SellTickets proxyObject = (SellTickets) Proxy.newProxyInstance(
                trainStation.getClass().getClassLoader(),
                trainStation.getClass().getInterfaces(),
                new InvocationHandler() {
                    /*
                        proxy: 代理对象（基本不使用），与proxyObject是同一个对象
                        method: 对接口中的方法进行封装的method对象
                        args: 正在被代理的方法的参数
                        
                        @return: 就是方法的返回值(sell的返回值)
                     */
                    @Override
                    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                        System.out.println("代理点收取一些服务费用");
                        Object obj = method.invoke(trainStation, args);
                        return obj;
                    }
                }
        );
        return proxyObject;
    }
}

public class Client{
    public static void main(String[] args) {
        // 获取代理对象
        // 1. 创建代理工厂对象
        ProxyFactory factory = new ProxyFactory();
        // 2.使用factory对象的方法获取代理对象
        SellTickets proxyObject = factory.getProxyInstance();
        // 3. 调用售卖的方法
        proxyObject.sell();
    }
}
```

cglib动态代理(没有接口的类，如上述TranStation没有接口的时候不能使用JDK动态代理)：同上例子
需要导入maven依赖cglib  

代理模式优缺点  
优点：
- 代理模式在客户端与目标对象之间起到一个中介作用和保护目标对象的作用
- 代理模式可以扩展目标对象
- 将客户端和目标对象进行解耦合  

缺点：
- 增加了系统复杂度  



### 12.2.2 适配器模式(Adapter)
适配器模式：将一个类的接口转换成客户希望的另外一个接口。  
适配器模式分为类适配器模式和对象适配器模式。  
结构：目标接口(抽象类或者接口)、适配者类(被访问和适配的现存组件库中的组件接口)、适配器类(是一个转换器)

类适配器模式：
```java
public interface TFCard{
    String readTF();
    void writeTF(String msg);
}
// 适配者类
public class TFCardImpl implements TFCard{
    @Override
    public String readTF() {
        return "TF卡读取数据";
    }
    @Override
    public void writeTF(String msg) {
        System.out.println("TF卡写入数据：" + msg);
    }
}

// 目标接口
public interface SDCard{
    String readSD();
    void writeSD(String msg);
}

public class SDCardImpl implements SDCard{ 
    @Override
    public String readSD() {
        return "SD卡读取数据";
    }
    
    @Override
    public void writeSD(String msg) {
        System.out.println("SD卡写入数据：" + msg);
    }
}

public class Computer {
    public String readSD(SDCard sdCard){
        if(sdCard == null) {
            throw new NullPointerException("sd card is null");
        }
        return sdCard.readSD();
    }
}

// 适配器类
public class SDAdapterTF extends TFCardImpl implements SDCard{
    @Override
    public String readSD() {
        System.out.println("adapter read TF card");
        return readTF();
    }
    @Override
    public void writeSD(String msg) {
        System.out.println("adapter write TF card");
        writeTF(msg);
    }
}

// 客户端
public class Client {
    public static void main(String[] args) {
        Computer computer = new Computer();
        String msg = computer.readSd(new SDCardImpl());
        System.out.println(msg);

        System.out.println("================");
        
        String msg1 = computer.readSD(new SDAdapterTF());
        System.out.println(msg1);
    }
}
```
类适配器违背了合成复用原则。类适配器是客户类有一个接口规范的情况下可用。

对象适配器：
实现方式：采用将现有组件库中已经实现的组件引入适配器类中，该类同时实现当前系统的业务接口。
```java
// 与类适配器相比主要修改适配器类和Client类
public class SDAdapterTF implements SDCard{ 
    private TFCard tfCard;
    // 意味着必须在创建适配器类的时候传入一个TFCard对象
    public SDAdapterTF(TFCard tfCard) {
        this.tfCard = tfCard;
    }
    @Override
    public String readSD() {
        System.out.println("adapter read TF card");
        return tfCard.readTF();
    }
    
    @Override
    public void writeSD(String msg) {
        System.out.println("adapter write TF card");
        tfCard.writeTF(msg);
    }
}
```

接口适配器：当不希望实现一个接口的所有方法时可以创建一个抽象类Adapter, 实现所有方法。后续我们只需要继承改抽象类即可。  

应用场景：
- 以前开发的系统存在满足新系统功能需求的类，但其接口同新系统的接口不一致。
- 使用第三方提供的组件，但组件接口定义与自己要求的接口定义不同。

### 12.2.3 装饰者模式(Decorator)
装饰者模式：动态地给一个对象添加额外的职责。一个类聚合并继承一个抽象类  
结构：抽象构件角色(定义一个接口以规范准备接收附加责任的对象)、具体构件角色(实现抽象构件，通过装饰角色为其添加职责)、
抽象装饰角色(继承或实现抽象构件，并包含具体构件的实例，可以通过其子类扩展具体构件的功能)、
具体装饰角色(实现抽象装饰的方法，并给具体构件对象添加附加责任)  

示例：
```java
// 抽象构件角色
public abstract class FastFood {
    private float price;
    private String desc;
    public FastFood(float price, String desc) {
        this.price = price;
        this.desc = desc;
    }
    public FastFood(){}
    
    public float getPrice() {
        return price;
    }
    public void setPrice(float price) {
        this.price = price;
    }
    public String getDesc() {
        return desc;
    }
    public void setDesc(String desc) {
        this.desc = desc;
    }
    public abstract float cost();
}

// 具体构件角色(炒饭)
public class FriedRice extends FastFood{
    public FriedRice() {
        super(10, "炒饭");
    }
    @Override
    public float cost() {
        return getPrice();
    }
}

// 具体构件角色(炒面)
public class FriedNoodles extends FastFood{
    public FriedNoodles() {
        super(10, "炒面");
    }
    @Override
    public float cost() {
        return getPrice();
    }
}

// 抽象装饰角色(抽象类)
public abstract class Garnish extends FastFood{
    private FastFood fastFood;
    
    public Garnish(FastFood fastFood, float price, String desc) {
        this.fastFood = fastFood;
        super(price, desc);
    }
    
    public FastFood getFastFood() {
        return fastFood;
    }
    
    public void setFastFood(FastFood fastFood) {
        this.fastFood = fastFood;
    }
}

// 具体装饰角色(鸡蛋)
public class Egg extends Garnish{
    public Egg(FastFood fastFood) {
        super(fastFood, 2, "鸡蛋");
    }
    @Override
    public float cost() {
        return getPrice() + getFastFood().cost();
    }
    
    @Override
    public String getDesc() {
        return super.getDesc() + getFastFood().getDesc();
    }
}

// 具体装饰角色(培根)
public class Bacon extends Garnish{
    public Bacon(FastFood fastFood) {
        super(fastFood, 3, "培根");
    }
    @Override
    public float cost() {
        return getPrice() + getFastFood().cost();
    }

    @Override
    public String getDesc() {
        return super.getDesc() + getFastFood().getDesc();
    }
}

// 客户端
public class Client {
    public static void main(String[] args) { 
        FriedRice food = new FriedRice();
        System.out.println(food.getDesc() + ": " + food.cost() + "元");
        
        System.out.println("===============");
        
        food = new Egg(food);
        System.out.println(food.getDesc() + ": " + food.cost() + "元");
        
        System.out.println("===============");
        
        food = new Bacon(food);
        System.out.println(food.getDesc() + ": " + food.cost() + "元");
    }
}
```
使用场景：
- 不能采用继承的方式对系统进行扩充或者采用继承不利于系统的扩展和维护时。  
  不能采用继承的情况：存在大量独立扩展使得子类数目爆炸性增长；类定义不能继承(final)
- 不影响其他对象情况下以动态、透明的方式给单个对象添加职责
- 对象的功能可以动态的添加或者删除

静态代理和装饰者模式对比
相同点：
- 都实现与目标类相同的业务接口
- 两个类中都需要声明目标对象
- 都可以在不修改目标类的前提下增强目标方法

不同点：
- 目的不同：代理是为了隐藏和保护目标对象，装饰是为了扩展/增强目标对象
- 获取目标对象构件的方式不同：静态代理内部创建，装饰者需要外部传递

### 12.2.4 桥接模式(Bridge)
定义：将抽象部分与它的实现部分分离，使它们都可以独立地变化。利用组合来替代继承关系  
结构：抽象化角色(定义抽象类并包含一个引用指向实现化角色), 扩展抽象化角色(抽象化角色的子类，实现抽象化角色的抽象方法，通过组合关系调用实现化角色的业务方法), 
实现化角色(定义实现化角色的接口，供扩展抽象化角色调用), 具体实现化角色(给出实现化角色接口的具体实现)  

示例：
```java
// 实现化角色
public interface VideoFile {
    void decode(String fileName);
}

// 具体实现化角色(Avi视频文件)
public class AviFile implements VideoFile{
    @Override
    public void decode(String fileName) {
        System.out.println("avi视频: " + fileName);
    }
}

// 具体实现化角色(Rmv视频文件)
public class RmvFile implements VideoFile{
    @Override
    public void decode(String fileName) {
        System.out.println("rmv视频: " + fileName);
    }
}

// 抽象化角色
public abstract class OperatingSystem {
    protected VideoFile videoFile;
    public OperatingSystem(VideoFile videoFile) {
        this.videoFile = videoFile;
    }
    public abstract void play(String fileName);
}

// 扩展抽象化角色(windows操作系统)
public class Windows extends OperatingSystem{
    public Windows(VideoFile videoFile) {
        super(videoFile);
    }
    
    @Override
    public void play(String fileName) {
        System.out.println("windows播放 " + fileName);
    }
}

// 扩展抽象化角色(windows操作系统)
public class Mac extends OperatingSystem{
    public Mac(VideoFile videoFile) {
        super(videoFile);
    }

    @Override
    public void play(String fileName) {
        System.out.println("Mac播放 " + fileName);
    }
}
```

使用场景：
- 当一个类存在两个独立变化的维度，且这两个维度需要进行扩展时  
- 当一个系统不希望使用继承或因为多层次继承导致系统类的个数急剧增加时
- 当一个系统需要在构件的抽象化角色和具体化角色之间增加更多的灵活性时。避免两个层次之间建立静态的继承联系，通过桥接模式可以使他们
  在抽象层建立一个关联关系。

### 12.2.5 外观模式(Facade)
定义：是一种通过为多个复杂的子系统提供一个一致的接口，而使这些子系统更加容易被访问的模式。
外观模式是 <font color="#f79646">"迪米特法则"</font> 的典型应用。  

示例：
```java
public class Light {
	public void on(){
		System.out.println("关闭电灯");
	}
	
	public void off() {
		System.out.println("打开电灯");
	}
}

public class TV {
	public void on(){
		System.out.println("关闭电视");
	}
	
	public void off() {
		System.out.println("打开电视");
	}
}

public class AirCondition {
	public void on(){
		System.out.println("关闭空调");
	}
	
	public void off() {
		System.out.println("打开空调");
	}
}

public class SmartAppliancesFacade {
	private Light light;
	private TV tv;
	private AirCondition airCondition;
	public SmartAppliancesFacade(){
		light = new Light();
		tv = new TV();
		airCondition = new AirCondition();
	}
	
	public void say(Stirng msg) {
		if(msg.contains("打开")) {
			on();
		} else if(msg.contains("关闭")) {
			off();
		} else {
			System.out.println("我还听不懂你说的");
		}
	}
	
	private void on() {
		light.on();
		tv.on();
		airCondition.on();
	}
	
	private void off() {
		light.off();
		tv.off();
		airCondition.off();
	}
}
```

优点：
- 降低了子系统与客户端的耦合度，使得子系统变化不会用想调用它的客户类
- 对客户屏蔽系统组件，减少客户处理的对象数目并使子系统使用起来更容易
缺点：
- 不符合开闭原则，修改麻烦

源码应用：<font color="#b2a2c7">HttpServletRequest</font> 的实现类 <font color="#b2a2c7">RequestFacade</font> 和 <font color="#b2a2c7">Request</font>, RequestFacade 里面有私有成员对象request, 此时就算强制转换成RequestFacade类也无法访问Request里面的方法

### 12.2.6 组合模式
定义：又名部分整体模式。用于把一组相似的对象当作单一的对象。组合模依据树形结构来组合对象，表示部分以及整体层次。

组成：
- 抽象根节点(Component)：定义系统各层次对象公有方法和属性
- 树枝节点：定义树枝节点的行为，存储子节点，组合树枝节点和叶子节点形成一个树形结构
- 叶子节点：叶子节点对象，其下再无分支，是系统层次遍历的最小单位

示例：
```java
// 菜单组件
public abstract class MenuComponent {
	protected String name;
	protected int level;
	
	// 添加子菜单
	public void add(MenuComponent menuComponent) {
		throw new UnsupportedOpeationException();
	}
	
	// 移除子菜单
	public void remove(MenuComponent menuComponent) {
		throw new UnsupportedOpeationException();
	}
	
	// 获取指定的子菜单
	public MenuComponent getChild(int index) {
		throw new UnsupportedOpeationException();
	}
	
	public String getName() {
		return name;
	}
	
	// 打印菜单名称的方法(包含子菜单和子菜单项)
	public abstract void print();
}

// 菜单
publci class Menu extends MenuComponent{
	private List<MenuComponent> menuComponentList = new ArrayList<>();
	
	public Menu(String name, int leve) {
		this.name = name;
		this.level = level;
	}

	@Override
	public void add(MenuComponent menuComponent) {
		menuComponentList.add(menuComponent);
	}
	
	@Override
	public void remove(MenuComponent menuComponent) {
		menuComponentList.remove(menuComponent);
	}
	
	@Override
	public MenuComponent getChild(int index) {
		return menuComponentList.get(index);
	}
	
	@Override
	public void print() {
		System.out.print(name);
		for(MenuComponent component: menuComponentList) {
			component.print();
		}
	}
}

public class MenuItem extends MenuComponent {
	public MenuItem(String name, int level) {
		this.name = name;
		this.level = level;
	}
	
	@Override
	public void print() {
		System.out.println(name);
	}
}
```

分类：
- 透明组合模式(如上示例)
    透明组合模式中对于所有构件类都有相同的接口，但是不够安全，叶子和容器有区别，且违背了接口隔离原则。
- 安全组合模式
    安全组合模式的抽象构件角色中没有声明任何用于管理成员对象的方法，而是在树枝节点里面是西安这些方法，但是缺点就是客户端<font color="#ff0000">不能完全针对抽象编程</font>，需要区别对待叶子构件和容器构件。

优点：
- 清晰定义层次的复杂对象，表示对象全部或部分层次，让客户端忽略层次差异
- 客户端可以一致的操作一个组合结构或者其中的单个对象，不必进行细致区分
- 新增树枝节点和叶子节点都很方便，符合 <font color="#f79646">"开闭原则"</font>
- 组合模式为树形结构的面向对象是西安提供了一种灵活的解决方案，通过叶子节点和树枝节点的递归组合，可以形成复杂的树形结构，但对树形结构的控制很简单

使用场景：出现树形结构的应用场景

### 12.2.7 享元模式(FlyWeight)
定义：运用共享技术来有效地支持大量细粒度对象的复用。它通过共享已经存在的对象来大幅度减少需要创建的对象数量、避免大量相似对象的开销，提高系统资源利用率

结构：
- 两种状态：内部状态(共享部分)和外部状态(非共享部分)
- 三种角色
    - 抽象享元角色：一个接口或者抽象类，里面声明具体享元类公共方法，这些方法可以向外提供想元对象的内部数据（内部状态），同时也可以根据这些方法设置外部数据（外部状态）。
    - 具体享元角色：实现抽象享元类，成为享元对象；为内部状态提供了存储空间，通常结合单例模式来设计具体享元类，为每一个具体享元类提供唯一的享元对象。
    - 非享元角色：不能被共享的抽象享元类的子类可以设计为非共享具体享元类；需要这个类的对象直接实例化创建。
    - 享元工厂角色：负责创建和管理享元角色。当对象请求一个享元对象是，享元工厂检查系统中是否存在符合要求的享元对象，有则提供，无则创建。

 



## 12.3 行为型模式








