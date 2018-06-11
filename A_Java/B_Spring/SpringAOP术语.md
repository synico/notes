# Spring AOP术语

#### AOP术语
1. Aspect（切面）：一个关注点的模块化，这个关注点会横切多个对象。
2. Join point（连接点）：程序执行中某个特定的点，在Spring AOP中表示一个方法的执行过程。
3. Advice（通知）：在切面上某个特定的连接点上执行的动作，在Spring中，以拦截器为通知模型，并维护一个以连接点为中心的拦截器链。
4. Pointcut（切入点）：匹配连接点的断言，通知和一个切入点表达式关联，并在满足这个切入点的连接点上执行通知里定义的动作。
5. Introduction（引入）：声明额外的方法或某个类型的字段，Spring AOP允许为任何被通知的类引入新的接口。
6. Target object（目标对象）：被一个或多个切面通知的对象，也被称为被通知对象。因为Spring使用运行时代理，这个对象永远是被代理的对象。
7. AOP proxy（AOP代理）：由AOP Framework创建用来实现切面契约。在Spring AOP中，一个AOP代理由JDK dynamic代理或cglib代理实现。
8. Weaving（织入）：把切面关联到其他应用类型或对象，并生成一个被通知对象。这些可以在编译时，载入时或运行时执行。Spring在运行时执行织入。

#### AOP的两种代理方式
Spring中AOP默认使用Java动态代理(standard JDK dynamic proxies)来实现AOP代理，也可以指定使用CGLIB(Code Generation Library)实现AOP代理。

##### Java动态代理
1. 代理的目标对象基于接口，并且仅能代理接口中声明的方法。
2. 使用动态代理机制生成一个实现代理接口的匿名类，在调用具体方法前调用InvokeHandler来处理。

##### CGLIB
1. 对目标对象是否基于接口无限制。
2. 在运行期，加载目标对象的class文件，通过修改其字节码生成子类来实现代理。
