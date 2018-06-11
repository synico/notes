# DispatcherServlet和ContextLoaderListener

DispatcherServlet的context仅仅是springmvc的上下文，而spring container加载的context是通过ContextLoaderListener加载。一般基于springmvc的web项目会同时使用这两个context。其中，前者负责加载mvc相关的配置（如viewResolver,Controller,MultipartResolver等）,后者负责加载由spring container管理的资源（如service,dao等）。

#### DispatcherServlet--->Servlet Web ApplicationContext
1. Controllers
2. HandlerMapping
3. viewResolver

#### ContextLoaderListener--->Root Web ApplicationContext
1. Services
2. Repositories
