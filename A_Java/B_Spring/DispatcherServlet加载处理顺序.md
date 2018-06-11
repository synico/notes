# DispatcherServlet

#### 加载顺序

1. 在创建DispatcherServlet的WebApplicationContext之前，先查找root context（通过ContextLoader加载）并将其设置为DispatcherServlet的WebApplicationContext的parent context。

2. DispatcherServlet的WebApplicationContext创建过程同ContextLoader创建ApplicationContext的过程。

3. 在XmlWebApplicationContext发布事件后，会继续初始化DispatcherServlet的stratgies对象。该初始化包含初始化一下组件：  
1) multipartResolver  
2) localeResolver  
3) themeResolver  
4) handlerMappings  
5) handlerAdapters  
6) handlerExceptionResolvers  
7) requestToViewNameTranslators  
8) viewResolvers  
9) flashMapManager  

#### 处理request顺序

1. 查找WebApplicationContext（servletContext中属性名为DispatcherServlet.WEB\_APPLICATION\_CONTEXT\_ATTRIBUTE）,并将其绑定到request上。

2. locale resolver被绑定到request上，使request在处理过程中需要解析locale的element可以使用该resolver。

3. theme resolver被绑定到request。

4. 如果指定了multipart file resolver，并且在request中检测出multipart，则request将会被包装成MultipartHttpServletRequest。

5. 在handlerMappings中查找匹配的handler, 则execution chain会和handler（preprocessors，postprocessors和controllers）关联，并按顺序执行。开始准备model或rendering。

6. 如果model已返回，则页面随之被render。
