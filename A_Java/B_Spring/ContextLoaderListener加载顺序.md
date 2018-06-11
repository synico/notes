# ContextLoaderListener加载顺序

1. 首先创建ApplicationContext实例，如果ContextLoader通过加载xml配置文件，则先创建XmlWebApplicationContext实例。

2. 调用AbstractApplicationContext（XmlWebApplicationContext的父类）的refresh方法初始化ApplicationContext实例，包括：  
1) 查找或创建beanFactory实例（DefaultListableBeanFactory）。在创建beanFactory实例的过程中使用BeanDefinitionReader读取bean的定义，如通过Xml定义配置文件，则使用XmlBeanDefinitionReader读取整个xml文件，逐行读取处理配置信息。  
2) 在逐行处理Spring配置文件信息过程中，Spring通过配置文件头<beans>定义的namespace信息，加载对应的NamespaceHander。然后获取相应NamespaceHandler中为特定节点注册的BeanDefinitionParser。最后使用该Parser创建定义的beans，并通过事件将beans注册到beanFactory（DefaultListableBeanFactory实现接口BeanDefinitionRegistry）。  
3) Spring除了扫描classpath下注解的components，还会创建META-INF/spring.handlers里配置的handlers。

3. 调用以bean的方式注册在context中的factory process的processors。

4. 为创建bean的processors注册拦截器。

5. 初始化messageSource。

6. 初始化event multicaster。

7. 注册listeners。

8. 初始化余下的Singletons（non-Lazy-init）。

9. 发布相应的事件。

10. 将初始化完成的ApplicationContext实例放入到ServletContext中，其中属性名为WebApplicationContext.ROOT\_WEB\_APPLICATION\_CONTEXT\_ATTRIBUTE。
