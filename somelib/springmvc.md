# Spring MVC

## Spring MVC   web.xml配置

在`web.xml`中主要是配置 `DispatcherServlet`

```xml
<servlet>
        <servlet-name>action</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
</servlet>
<servlet-mapping>
<servlet-name>action</servlet-name>
        <url-pattern>*.action</url-pattern>
</servlet-mapping>
```

当然如果我们把`springmvc-servlet`放入`src`目录下 web.xml会找不到servlet而出错 因此我们需要添加初始化参数配置

```xml
<init-param>
	<param-name>contextConfigLocation</param-name>
  	<param-value>classpath:springmvc-servlet.xml</param-value>
</init-param>
```

## HandlerMapping 

### BeanNameUrlHandlerMapping

在`springmvc-servlet.xml`中配置 beans 默认的HandlerMapping

```xml
<!-- 声明 handlerMapping -->
<!-- 声明 BeanNameURI 处理器映射，其为默认的处理器映射 -->
<bean id="beanNameUrlHandlerMapping" class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
<!-- 声明 Controller -->
<bean name="/home.action" class="spring.mvc.controller.CeshiController" />
<!-- 内部资源视图解析器，前缀 + 逻辑名 + 后缀 -->
<bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
	<property name="prefix" value="/WEB-INF/pages/"/>
	<property name="suffix" value=".jsp"/>
</bean>
```

