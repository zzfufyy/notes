### 注解说明

-------

#### 1. 注解说明

- @Autowired：

  自动装配，通过类型、名字

  如果Autowired不能唯一自动装配上属性，则需要通过@Qualifier(value="xxx")

- @Resource

  自动装配，通过名字、类型

- @Nullable：

  字段标记了这个注解，说明这个字段可为null

- @Component：

  组件，放在类上，说明这个类被Spring管理了，就是bean。