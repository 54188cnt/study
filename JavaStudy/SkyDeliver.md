# 一、Swagger
[官网](https://swagger.org.cn/docs/)  
Knife4j是为Java MVC框架集成的Swagger生成API文档的增强解决方案  

步骤：  
- 创建WebMvcConfiguration配置类

常用注解：
- <font color="YELLOW">@Tag</font>: 类上(controller), 表示对类的说明
- <font color="YELLOW">@Schema</font>: 类上(entity, dto, vo), 表示对类用途的说明
- <font color="YELLOW">@Schema</font>: 属性上, 描述属性信息
- <font color="YELLOW">@Operation</font>: 方法上(controller的方法上), 说明方法的用途、作用
