## Spring

### 介绍一下Spring的IOC和AOP？

- IOC：控制反转也叫依赖注入，IOC利用Java反射机制。控制反转是指，本来被调用者的实例是由调用者来创建的，这样的缺点是耦合性太强，IOC则是统一交给Spring管理创建，将对象交给容器管理。当你需要调用时Spring会将需要的对象分配给你的类。
- AOP：是对OOP地补充和完善，对OOP中产生地重复代码进行抽取和统一嵌入业务代码中。实现AOP地技术主要分为两大类，一类使用动态代理，包括CGlib动态代理和JDK动态代理实现，利用截取消息地形式对该消息进行装饰增强。一类是使用静态代理，在编译时织入相关代码。

### JDK动态代理和CGlib动态代理地区别？

- JDK动态代理只能对实现了接口地类生成代理，而不能针对类
- CGlib是针对类实现代理，主要是对制定地类生成一个子类，覆盖其中地方法实现，底层采用ASM字节码生成框架，使用字节码技术生成代理类
- CGlig创建代理慢但是运行速度快，JDK动态代理相反

### Spring在什么时候初始化bean？

默认情况在加载Spring配置文件的时候
如果修改了作用域为原型模式或者设置了延迟加载，那么在getBean方法后才被实例化

### Spring 事务？

Spring事务机制主要由声明式和编程式两种，前者被广泛使用。事务属性主要由事务的传播行为、事务的隔离级别、事务的超时值以及事务可读标志组成。Spring会使用AOP支持声明式事务，隔离级别除了数据库对应的隔离级别还有一种默认数据库的隔离级别。

### Bean的生命周期？
 
 1. 实例化Bean对象
 2. 设置Bean属性
 3. 通过各种Aware接口在容器里设置相应的Bean ID，Bean Factory，或者Application Context
 4. 调用前置初始化方法postProcessBeforeInitialization 
 5. 如果实现了InitializingBean接口，则会调用afterPropertiesSet方法
 6. 调用Bean自身的init方法
 7. 调用后置初始化方法postProcessAfterInitialization 
 
### Spring事务传播行为？

在TransactionDefinition接口里面定义了7种传播行为：
- PROPAGATION_REQUIRED:如果有事务则使用当前事务，否则新建一个（默认）
- PROPAGATION_SUPPORTS:有事务则使用当前事务，否则以无事务方式执行
- PROPAGATION_MANDATORY:表示方法必须在事务中运行，如果当前事务不存在则抛出异常
- PROPAGATION_REQUIRES_NEW:总是开启一个新事务
- PROPAGATION_NOT_SUPPORTS:总以非事务方式执行，并挂起所有事务
- PROPAGATION_NEVER:总以非事务方式执行，有事务运行时抛出异常
- PROPAGATION_NESTED:有事务时以嵌套事务形式存在，否则按REQUIRED方式执行

### 拦截器和过滤器的区别？

1. 拦截器是基于Java的反射机制，而过滤器是基于函数回调。
2. 拦截器不依赖于servlet容器，过滤器依赖于servlet容器。
3. 拦截器只能对action请求起作用，而过滤器可以对几乎所有的请求起作用。
4. 在action的生命周期中，拦截器可以被多次调用，而过滤器只能在容器初始化时被调用一次。
5. 拦截器可以获取容器里的bean，过滤器不行
6. 拦截器可以访问action上下文、值栈里的对象，而过滤器不能访问
