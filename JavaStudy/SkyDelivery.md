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

# 二、基础业务

## 2.1 购物车功能

### 清除购物车
购物车的数据存储在 redis 里面，便于清理，但是清除购物车的时候就会出现BigKey问题


### 添加购物车
使用Hash数据结构，以`[dishId ? 0]:[setmealId ? 0]:[dishFlavor ? none]` 作为 field , value 表示的时物品数量