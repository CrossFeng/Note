# Tomcat目录结构

**Tomcat目录结构**

　　**1、bin目录**

　　这个目录只要是存放了一些bat文件或者sh文件。比如说我们需要启动tomcat的bat就在这个目录下

　　启动tomcat的方式：

　　1).点击 startup.bat可以启动tomcat

　　2).在黑窗口下运行 catalina.bat 后面需要跟命令：start启动 stop关闭

　　3).关闭容器 shutdonw.bat或者是直接关闭黑窗口。

　　**2、conf**

　　这个目录中存放的都是一些配置文件 xml

　　**3、lib**

　　这个目录中存放的是一些jar文件。

　　这里的jar文件重要有两大类：

　　1)tomcat自身的jar，

　　2)实现javaEE平台下部分标准的实现类(比如：jsp servlet...)

　　**4、log**

　　存放的都是tomcat的日志文件。如果我们想了解黑窗口在启动时的打印信息，可以进到这个目录下找到cataline.log文件在这个文件中可以看到相关记录。

　　**5、temp**

　　在这个目录中存放的是tomcat在运行时所产生的一些临时文件。这些文件是否存在并不影响tomcat的运行，所以这个目录下的内容可以被删除掉。但是：temp文件夹不能删。

　　**6、webapps**

　　这个目录主要是存放需要让tomcat去管理的资源的目录。

　　**7、work**

　　这个目录主要存放的是tomcat对jsp编译完后得原文件以及class文件。

　　**8、doc**

　　存放Tomcat文档;