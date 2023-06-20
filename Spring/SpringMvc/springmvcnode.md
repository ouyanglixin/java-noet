# springmvc

## 1.springmvc 的概念

- 介绍

**SpringMVC 也叫Spring web mvc。是Spring 框架的一部分，是在Spring3.0 后发布的。**

- 优点

基于 MVC 架构，功能分工明确。解耦合

容易理解，上手快，使用简单

作为Spring框架一部分，能够使用Spring的IOC和AOP

SpringMVC 强化注解的使用

> 在Controller, Service, Dao 都可以使用注解。方便灵活。使用**@Controller** 创建处理器对象**,@Service** 创建业务对象，**@Autowired** 或者**@Resource** 在控制器类中注入 Service,在Service 类中注入 Dao



- springMvc的优化方向

![image-20230620140358532](assets/image-20230620140358532.png)

1. 数据提交的优化
2. 携带数据优化
3. 简化返回处理
