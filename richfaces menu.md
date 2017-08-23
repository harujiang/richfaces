# richfaces
documents
RichFaces开发指南3.3.3
 
1  介绍
 
RichFaces是一个开源框架，它不借助于JavaScript而增加Ajax能力到存在的JSF应用程序中。
 
RichFaces利用了JavaServer Faces框架，包括生命周期，验证，转换工具，以及静态和动态的资源管理。具用内建Ajax 支持和高度可定制观感的RichFaces组件能够容易地被纳入到JSF应用程序中。
 
RichFaces准许：
 
    强化了整套JSF的好处，而且与Ajax一起工作。RichFaces完全集成到了JSF的生命周期内。虽然其它框架只给了你存取管理的beans的工具，而RichFaces在Ajax请求响应周期的时候，却促进了动作和值改变的侦听器，以及调用服务器边的验证和转换。
    增加了Ajax能力到存在的JSF应用程序中。框架提供了两个组件库(Core Ajax 和 UI)。Core库设置Ajax功能到存在的页面，所以不需要编写任何JavaScript代码或者用新的Ajax组件替换存在的组件。RichFaces启用页面范围的Ajax支持，而不是传统的组件范围的支持，并且它给了在页面上定义事件的机会。 一个事件调用一个Ajax请求，并且在由根据客户端引发的事件的Ajax请求改变了在服务器上的数据之后，变成为同步于JSF组件树的页面区域。
             快速创建基于开箱即用的组件的复杂视图。RichFaces UI库包含组件，用于添加富裕用户界面的功能到JSF应用程序。它扩展了RichFaces框架，包含了大量（不断增长的）强大的富裕的Ajax可用的带有广泛皮肤支持的组件的集合。
           利用内建Ajax支持编写你自己的定制富裕组件。我们始终致力于组件开发包（CDK）的改善，它用于RichFaces UI库的创建。CDK包括了一个代码生成工具和一个使用了类似于JSP语法的模板工具。这些工具帮助避免了创建组件的常规流程。组件工厂就象一个运行良好的机器，允许创建一流的带有Ajax功能的富裕组件，比用传统编码方式的手段创建的简单组件要容易的多。
            使用java类打包资源。除了它的核心，RichFaces的Ajax功能提供一个高级支持，用于不同的资源管理：图片、JavaScript代码和CSS样式表。资源框架可以容易地使得你的资源连同你定制组件的代码一起打包到jar文件中。
            快速轻松地生成二进制资源。资源框架可以快速地生成图象、声音、Excel电子表格等等，因此，例如，使用“Java Graphics2D”库熟悉的方法创建图象成为可能。
           利用基于皮肤的技术，创建一个现代的富裕的用户界面的观感。RichFaces提供了一个可换肤的功能，它允许你容易定义和管理色彩方案，以及其他带有命名皮肤参数帮助的UI参数。因此，可以从JSP代码或JAVA代码访问这些皮肤参数（例如，调整基于UI文本部分生成的快速图象）。RichFaces自带大量的让你着手的预定义皮肤，但是你也可以轻松地创建你自己的定制皮肤。
          让你同时测试和创建组件、动作、侦听器和页面。一个自动测试工具是在我们将来不久的发展蓝图中。这个工具会生成测试案例，用于你尽可能快地开发你的组件。测试框架不仅测试组件，而且也用于任何其他服务边或者客户端的包含JavaScript代码的功能。此外，它不用部署测试应用程序到Servlet容器中就会做这一切。
 
RichFaces UI组件成为了准备就绪开箱即用，因此，节约了开发者的时间，并且立刻得到上面提及的在网页应用程序创建中的功能的好处。所以，可以更快、更轻松地获得使用的经验。
 
2 技术要求
 
开发RichFaces使用了一个开放的体系结构，可以最广泛地兼容各种环境。
 
下面是你开始运行RichFaces 3.3.3需要的东西：
 
1 Java
2 JavaServer Faces
3 Java 应用程序服务器或servlet容器
4 浏览器(在客户边)
5 RichFaces框架
 
2.1          支持的java版本
 
1 JDK 1.5 或更高
 
2.2          支持的JavaServer Faces实现和框架
 
1 Sun JSF-RI - 1.2_x (1.2_14 recommended), 2.x
2 MyFaces 1.2.x (1.2.5 recommended), 2.x
3 Facelets 1.1.x
4 Seam 2.x
 
2.3          支持的服务器
 
1 Apache Tomcat 5.5 - 6.0
2 BEA WebLogic 9.1 - 10.0
3 Resin 3.1.x
4 Jetty 6.1.x
5 Sun Application Server 9 (J5EE)
6 Glassfish V2, V3
7 JBoss 4.2.x - 5
8 Websphere 7.0. 或更高
9 Geronimo 2.0或更高
 
2.4          支持的浏览器
 
Linux环境：
1 Firefox 3.0或更高
2 Opera 9.5或更高r
 
Windows环境：
1 Firefox 3.0或更高
2 Google Chrome
3 Internet Explorer 6.0或更高
4 Opera 9.5或更高
5 Safari 3.0或更高
 
Mac OS环境
1 Safari 3.0或更高
2 Firefox 3.5或更高
 
这个列表是基于我们的用户的报告构成。我们假设这个列表不完整，并在该列表缺少你的环境，但并不意味着不兼容.
 
我们感激你反馈有关不在该列表中的，但与RichFaces兼容的平台和浏览器。帮助我们保持列表的更新
 
3           RichFaces入门
 
本章描述所有必要的行为和应该做的配置，用于将RichFaces组件插入到一个JSF应用程序中。该描述依靠一个简单JSF，它具有RichFaces应用程序从下载库到在浏览器中运行应用程序的创建过程。在这里描述的应用程序创建过程是通用的，并不依赖于使用的IDE。
 
3.1          下载RichFaces
 
最新的RichFaces组件发行版可以在JBoss社区下载： [http://labs.jboss.com/jbossrichfaces/downloads]。二进制文件（这里是以*.bin.zip或 *.bin.tar.gz档案形式上传的）包含编译的，准备使用的带有基本皮肤集的RichFaces版本。
 
要开始使用RichFaces，在计算机文件系统创建一个名为“RichFaces”的文件夹，下载并在这里解压二进制文件。
 
对那些希望下载并自己编译RichFaces的人，在JBoss社区有一篇文章，它描述RichFaces的知识库的结构概要[http://www.jboss.org/community/docs/DOC-11864]，以及操作它的一些情况。
 
3.2          使用RichFaces的简单的JSF应用程序
 
简单的应用程序RichFaces Greeter，类似于hello-world应用程序，但有一点不同：RichFaces的世界会首先对用户说：“Hello!”。
 
使用所有必要的库创建标准的JSF 1.2项目；命名项目为“Greeter”，并遵循描述。
 
3.2.1     添加RichFaces库到项目
 
去到早先解码RichFaces二进制文件的文件夹，并打开lib文件夹。这个文件夹包含三个*.jar，它们是API，UI和实现库。拷贝lib文件夹的jars到“Greeter”JSF应用程序的WEB-INF/lib文件夹中。
 
[重要： 使用RichFaces的JSF应用程序假定下列包可用于项目中：commons-beanutils-1.7.0.jar, commons-collections-3.2.jar, commons-digester-1.8.jar, commons-logging-1.0.4.jar, jhighlight-1.0.jar
]
 
3.2.2     在web.xml中注册RichFaces
 
在RichFaces的库添加到项目内后，需要在web.xml中注册它们。在web.xml添加下列行：
 
...
<!-- Plugging the "Blue Sky" skin into the project -->
<context-param>
   <param-name>org.richfaces.SKIN</param-name>
   <param-value>blueSky</param-value>
</context-param>
 
<!-- Making the RichFaces skin spread to standard HTML controls -->
<context-param>
      <param-name>org.richfaces.CONTROL_SKINNING</param-name>
      <param-value>enable</param-value>
</context-param>
 
<!-- Defining and mapping the RichFaces filter -->
<filter> 
   <display-name>RichFaces Filter</display-name> 
   <filter-name>richfaces</filter-name> 
   <filter-class>org.ajax4jsf.Filter</filter-class> 
</filter> 
  
<filter-mapping> 
   <filter-name>richfaces</filter-name> 
   <servlet-name>Faces Servlet</servlet-name>
   <dispatcher>REQUEST</dispatcher>
   <dispatcher>FORWARD</dispatcher>
   <dispatcher>INCLUDE</dispatcher>
</filter-mapping>
...
 
有关如何操作RichFaces的皮肤的详情见“换肤”章节。
 
web.xml最终结果如下：
 
<?xml version="1.0"?>
<web-app version="2.5" 
                xmlns="http://java.sun.com/xml/ns/javaee"
                xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance
                xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/
javaee/web-app_2_5.xsd">
<display-name>Greeter</display-name>
  
<context-param>
   <param-name>javax.faces.STATE_SAVING_METHOD</param-name>
   <param-value>server</param-value>
</context-param>
  
<context-param>
   <param-name>org.richfaces.SKIN</param-name>
   <param-value>blueSky</param-value>
</context-param>
<context-param>
      <param-name>org.richfaces.CONTROL_SKINNING</param-name>
      <param-value>enable</param-value>
</context-param>
 
<filter> 
   <display-name>RichFaces Filter</display-name> 
   <filter-name>richfaces</filter-name> 
   <filter-class>org.ajax4jsf.Filter</filter-class> 
</filter> 
<filter-mapping> 
   <filter-name>richfaces</filter-name> 
   <servlet-name>Faces Servlet</servlet-name>
   <dispatcher>REQUEST</dispatcher>
   <dispatcher>FORWARD</dispatcher>
   <dispatcher>INCLUDE</dispatcher>
</filter-mapping>
  
<listener>
   <listener-class>com.sun.faces.config.ConfigureListener</listener-class>
</listener>
  
<!-- Faces Servlet -->
<servlet>
   <servlet-name>Faces Servlet</servlet-name>
   <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
   <load-on-startup>1</load-on-startup>
</servlet>
<!-- Faces Servlet Mapping -->
<servlet-mapping>
   <servlet-name>Faces Servlet</servlet-name>
   <url-pattern>*.jsf</url-pattern>
</servlet-mapping>
  
<login-config>
   <auth-method>BASIC</auth-method>
   </login-config>
</web-app>
 
3.2.3     管理的bean
 
“RichFaces Greeter”应用程序需要一个管理的bean。在项目的JavaSource文件夹中的demo包中创建一个名为user的管理的bean。代码如下：
 
package demo;
 
public class user {
   private String name="";
   public String getName() {
      return name;
   }
   public void setName(String name) {
      this.name = name;
   }
}
 
3.2.4     在faces-cofig.xml注册bean
 
接下来user bean应该在faces-config.xml文件中被注册：
 
<?xml version="1.0" encoding="UTF-8"?>
<faces-config version="1.2" 
                    xmlns="http://java.sun.com/xml/ns/javaee"
                    xmlns:xi="http://www.w3.org/2001/XInclude"
                    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/
ns/javaee/web-facesconfig_1_2.xsd">
   <managed-bean>
      <description>UsernName Bean</description>
      <managed-bean-name>user</managed-bean-name>
      <managed-bean-class>demo.user</managed-bean-class>
      <managed-bean-scope>request</managed-bean-scope>
      <managed-property>
         <property-name>name</property-name>
         <property-class>java.lang.String</property-class>
         <value/>
      </managed-property>
   </managed-bean>
</faces-config>
 
3.2.5     RichFaces Greeter index.jsp
 
“RichFaces Greete”应用程序只有一个JSP页面。在WEB CONTENT文件夹的根部创建index.jsp页面，内容如下：
 
<!doctype html public "-//w3c//dtd html 4.0 transitional//en">
<%@ taglib uri="http://java.sun.com/jsf/core" prefix="f" %>
<%@ taglib uri="http://java.sun.com/jsf/html" prefix="h" %>
<!-- RichFaces tag library declaration -->
<%@ taglib uri="http://richfaces.org/a4j" prefix="a4j"%>
<%@ taglib uri="http://richfaces.org/rich" prefix="rich"%>
 
<html>
      <head>
            <title>RichFaces Greeter</title>
      </head>
      <body>
            <f:view>
                  <a4j:form>
                        <rich:panel header="RichFaces Greeter" style="width: 315px">
                              <h:outputText value="Your name: " />
                              <h:inputText value="#{user.name}" >
                                    <f:validateLength minimum="1" maximum="30" />
                              </h:inputText>
                              
                              <a4j:commandButton value="Get greeting" reRender="greeting" />
                              
                              <h:panelGroup id="greeting" >
                                    <h:outputText value="Hello, " rendered="#{not empty user.name}" />
                                    <h:outputText value="#{user.name}" />
                                    <h:outputText value="!" rendered="#{not empty user.name}" />
                              </h:panelGroup>
                        </rich:panel>
                  </a4j:form>
            </f:view>
      </body>
</html>
 
应用程序使用了三个RichFaces组件：<rich:panel>用来作为信息的可视化容器；带有内建Ajax 支持的<a4j:commandButton>允许在响应返回之后，动态地显示一个问候；<a4j:form>帮助按钮执行动作。
 
注意，RichFaces标签库应该在每个JSP页面声明。
 
对Facelets，你应该添加下列行，用于标签库的声明：
 
<ui:composition xmlns="http://www.w3.org/1999/xhtml"
                xmlns:ui="http://java.sun.com/jsf/facelets"
                xmlns:a4j="http://richfaces.org/a4j"
                xmlns:rich="http://richfaces.org/rich">
   ...
</ui:composition>
 
好了！在服务器上运行该应用程序。在你的浏览器中输入: http://localhost:8080/Greeter/index.jsf，结果如下：
 
3.3          集成RichFaces到Maven项目
 
本节我们将告诉你如何使用Maven，创建一个带有RichFaces的简单的JSF应用程序。
 
首先，你需要确保你在本地机器上安装了Maven。我们将在Tomcat 6.0服务器上运行该JSF应用程序，所以，如果你还没有这样估，请下载并安装它。
 
现在我们可以继续创建应用程序了。要创建项目结构，并用最小的内容填充它，我们将使用“maven-archetype-jsfwebapp” Maven原型，它是RichFaces CDK的一部分。
 
“maven-archetype-jsfwebapp”原型和项目自身要求提供额外的知识库，即“http://snapshots.jboss.org/maven2/”和“http://repository.jboss.com/maven2/”。要使知识库对Maven成为可见的，最容易的方法是在“maven_installation_folder/conf/settings.xml”的<profiles>元素中创建一个配置。内容如下：
 
<profile>
    <id>jsf-app-profile</id>
    <repositories>
        <repository>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
                <updatePolicy>always</updatePolicy>
            </snapshots>
            <id>snapshots.jboss.org</id>
            <name>Snapshot Jboss Repository for Maven</name>
            <url>http://snapshots.jboss.org/maven2/</url>
            <layout>default</layout>
        </repository>
        <repository>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
                <updatePolicy>always</updatePolicy>
            </snapshots>
            <id>repository.jboss.com</id>
            <name>Jboss Repository for Maven</name>
            <url>http://repository.jboss.com/maven2/</url>
            <layout>default</layout>
        </repository>
    </repositories>
</profile>
 
当配置被添加后，你需要在<activeProfiles>元素中激活它，如下所示：
 
<activeProfiles>
  <activeProfile>jsf-app-profile</activeProfile>
</activeProfiles>
...
 
现在，我们有了使用“maven-archetype-jsfwebapp”原型创建项目的一切了。创建一个文件夹，它将收藏你的项目。然后，在它里面运行下面的命令：
 
...
mvn  archetype:generate  -DarchetypeGroupId=org.richfaces.cdk  -DarchetypeArtifactId=maven-
archetype-jsfwebapp  -DarchetypeVersion=3.3.3-SNAPSHOT  -DgroupId=org.docs.richfaces  -
DartifactId=jsf-app
...
 
你可以调整命令的一些参数。
 
参数	 描述
-DgroupId	 定义用于管理的bean的包。
-DartifactId	 定义项目的名字
 
这个命令生成的一个JSF项目，结构如下：
 
jsf-app
|-- pom.xml
`-- src
    |-- main
    |   |-- java
    |   |   `-- org
    |   |       `-- docs
    |   |           `-- richfaces
    |   |               `-- Bean.java
    |   |-- resources
    |   `-- webapp
    |       |-- WEB-INF
    |       |   |-- faces-config.xml
    |       |   `-- web.xml
    |       |-- index.jsp
    |       `-- pages
    |           |-- index.jsp
    |           `-- index.xhtml
    `-- test
        `-- java
            `-- org
                `-- docs
                    `-- richfaces
                        `-- BeanTest.java
 
现在，进入“jsf-app”文件夹，它包含了一个项目描述符（pom.xml）。打开项目描述符，编辑并添加依赖关系到<dependencies>元素。如下所示：
 
...
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.4</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jsp-api</artifactId>
        <version>2.0</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>jstl</groupId>
        <artifactId>jstl</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>jsp-api</artifactId>
        <version>2.1</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>javax.faces</groupId>
        <artifactId>jsf-api</artifactId>
        <version>1.2_12</version>
    </dependency>
    <dependency>
        <groupId>javax.faces</groupId>
        <artifactId>jsf-impl</artifactId>
        <version>1.2_12</version>
    </dependency>
    <dependency>
        <groupId>javax.el</groupId>
        <artifactId>el-api</artifactId>
        <version>1.0</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>el-impl</groupId>
        <artifactId>el-impl</artifactId>
        <version>1.0</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>javax.annotation</groupId>
        <artifactId>jsr250-api</artifactId>
        <version>1.0</version>
    </dependency>
    <!-- RichFaces libraries -->
    <dependency>
        <groupId>org.richfaces.framework</groupId>
        <artifactId>richfaces-api</artifactId>
        <version>3.3.3-SNAPSHOT</version>
    </dependency>
    <dependency>
        <groupId>org.richfaces.framework</groupId>
        <artifactId>richfaces-impl</artifactId>
        <version>3.3.3-SNAPSHOT</version>
    </dependency>
    <dependency>
        <groupId>org.richfaces.ui</groupId>
        <artifactId>richfaces-ui</artifactId>
        <version>3.3.3-SNAPSHOT</version>
    </dependency>
</dependencies>
...
 
最后三个依赖关系添加RichFaces库到项目。你现在可以用mvn install命令构建项目。
 
当看见“BUILD SUCCESSFUL”消息时，项目已被装配，就可以导入IDE和运行在服务器上了。
 
使用命令mvn eclipse:eclipse -Dwtpversion=2.0，可以为Eclipse IDE构建项目。
 
然后你可以导入项目到Eclipse。在导入Eclipse之后，你可以打开“jsf-app/src/main/
webapp/WEB-INF/web.xml”，并根据指南的“在web.xml中注册RichFaces”的章节所列内容的配置它。
 
配置了项目，现在你可以开始使用RichFaces。打开“jsf-app/src/main/webapp/pages/index.jsp”文件，并添加标签库声明：
 
...
<%@ taglib uri="http://richfaces.org/rich" prefix="rich"%>
... 
 
添加一些RichFaces组件到index.jsp页面，如<rich:calendar>实例。如下所示：
 
...
<%@ taglib uri="http://java.sun.com/jsf/html" prefix="h" %>
<%@ taglib uri="http://java.sun.com/jsf/core" prefix="f"%>
<%@ taglib uri="http://richfaces.org/rich" prefix="rich"%>
<html>
    <head>
        <title>JSF Application with RichFaces built by Maven</title>
    </head>
    <body>
        <f:view>
        <rich:calendar />
        </f:view>
    </body> 
</html>  
...
 
现在，在Tomcat服务器上运行应用程序，在你喜爱的浏览器中输入“http://localhost:8080/jsf-app/”打开它。
 
3.4 相关的资源连接
 
The Photo Album Application [http://livedemo.exadel.com/photoalbum]，使用RichFaces设计和开发。
 
Maven Resource Dependency Plugin Reference
[http://www.jboss.org/community/wiki/MavenResourceDependencyPluginReference]，该文章讨论了插件的配置和使用。
 
JBoss Developer Studio
 [https://www.redhat.com/apps/store/developers/jboss_developer_studio.html]，带有一个RichFaces组件框架的紧密集成。 下面的链接可能对那些已使用IDE和RichFaces开发应用程序的人和那些希望改善开发流程的人是有用的。
 
1 Rich 组件
 [http://download.jboss.org/jbosstools/nightly-docs/en/GettingStartedGuide/html/first_seam.html#rich_components] 。
在“JBoss Developer Studio指南”中的“Rich组件”章节，描述了如何添加RichFaces组件进入到一个CRUD应用程序；
 
2 JBoss工具箱 [http://download.jboss.org/jbosstools/nightly-docs/en/jsf/html/palette.html] 。
 
在“可视网页工具参考指南”中的“JBoss工具箱”章节，描述了用于包含RichFaces应用程序的快速、方便的页面制作处理的特定工具箱（连同JBDS一起）的优势；
 
3 开发网页应用程序的RichFaces工具包
 [http://docs.jboss.org/tools/movies/demos/rich_faces_demo/rich_faces_demo.htm]
 
这个视频教程演示了与JBoss Developer Studio交互，同时又操作RichFaces的某些方面的内容；
1. 如何为RichFaces配置Maven
 [http://docs.jboss.org/tools/movies/demos/rich_faces_demo/rich_faces_demo.htm]
 
该文章简洁地讨论了用于RichFaces的Maven配置；
1 RichFaces发布步骤[http://www.jboss.org/community/docs/DOC-13446]
 
该文章描述了RichFaces发布构建如何制作；
RichFaces installing and configuration
[http://www.jboss.org/community/wiki/RichFacesinstallingandconfiguration]， 阅读该文章会找到如何集成RichFaces和Trinidad ，以及在JBoss服务器上启动RichFaces例子时可以发生的问题。



4         不同环境的设置
 
RichFaces带有对包含在JavaServer Faces规则中的所有标签（组件）的支持。要添加RichFaces能力到存在的JSF项目，你应该只放置RichFaces库到该项目的lib文件夹中，并添加过滤器映射。存在的项目的行为没有被改变，仅是因为RichFaces。
 
4.1          网页应用程序描述符参数
 
RichFaces不需要在你的web.xml中定义任何参数。但是列在下面的RichFaces参数可以帮助开发，并可 以增加RichFaces的灵活性。
 
表4.1. 初始化参数
名字	 默 认	描述
org.richfaces.SKIN	DEFAULT	使用在应用程序中的一个皮肤的名字。它可以是一个文字字符串，利用 一个名字或者EL表达式 (#{...})指向一个String属性（皮肤名）或  org.richfaces.framework.skin 类型的一个属性。 在最末的皮肤，它的实现被用于当前皮肤。
org.richfaces.LoadScriptStrategy	 DEFAULT 	定义RichFaces脚 本文件如何加载到应用程序。可能的值是： ALL, DEFAULT, NONE。详情见“脚本和样式加载策略” 。
org.richfaces.LoadStyleStrategy	DEFAULT	定义RichFaces样 式文件如何加载到应用程序。可能的值是： ALL, DEFAULT, NONE。详情见“脚本和样式加载策略” 。
org.ajax4jsf.LOGFILE	 none	一个应用程序的或一个容器日志文件（如果可能）的URL。如果这个参数被设置，来自特定的URL的内容被显示在 iframe窗口中的一个调试错误页面上。 
org.ajax4jsf.VIEW_HANDLERS	 none	是一个逗号分隔的定制视图处理器实例列表，用于插入链中。处理器以 特定的顺序被插在RichFaces视图处理器之前。例如，在facelets应用程序中，这个参数必须包括 com.sun.facelets.FaceletViewHandler ，而不是faces-config.xml声明的。
org.ajax4jsf.CONTROL_COMPONENTS	 none	是一个逗号分隔的名字列表 ，用于一个组件作为一个特殊的控件情况，比如消息包加载器，别名bean组件等等。是一个组件类型，通过从一个静 态字段COMPONENT_TYPE反射而获得。对带有这种类型编码的方法的组件总是在渲染Ajax响应中被调用，即使一个组件不是一个更新部分。
org.ajax4jsf.ENCRYPT_RESOURCE_DATA	 false	对生成的资源，比如加密生成的数据，它被编码在资源URL中。例如，根据包含了一个生成方法的名字的mediaOutput组件生成一个图象的URL， 因为对一个黑客攻击而言，可能创建一个请求，用于任何JSF后台beans或其他属性。要预防这种攻击 ，在关键的应用程序中设置这个参数为“true” （使用的JRE > 1.4）。
org.ajax4jsf.ENCRYPT_PASSWORD	 random	是一个密码，用于资源数据的加密。如如没有设置， org.ajax4jsf.COMPRESS_SCRIPT 使用一个随机密码。
org.ajax4jsf.RESOURCE_URI_PREFIX	 a4j 	定义前缀，它添加到所有生成资源的URLs。这个前缀设计来处理RichFaces生成资源的请求。 
org.ajax4jsf.GLOBAL_RESOURCE_URI_PREFIX	 a4j/g	定义前缀，它添加到全局资源的URLs。这个前缀设计来处理RichFaces生成资源的请求。 
org.ajax4jsf.SESSION_RESOURCE_URI_PREFIX	 a4j/s 	定义前缀，它被用于生成资源的会话跟踪。这个前缀设计来处理RichFaces生成资源的请求。
org.ajax4jsf.DEFAULT_EXPIRE 	86400 	用秒定义，流回到浏览器的资源可以被缓存多长时间。
org.ajax4jsf.SERIALIZE_SERVER_STATE	 false	如果启用，组件状态（不是树）在被存贮在会话中之前会被序列化。应 用程序可能不希望这样，使用对模式变化敏感的视图状态可能有问题。相反，这些参数可以使用相应环境的 com.sun.faces.serializeServerState 和org.apache.myfaces.SERIALIZE_STATE_IN_SESSION 参数 
 
[注意：使用org.richfaces.SKIN的方法是相同与org.ajax4jsf.SKIN]
 
表4.2. org.ajax4jsf.Filter初始化参数
名字	默认	描述
log4j-init-file	-	是一个路径（相对于网页网页应用程序），用于log4j.xml配置文件，它可以用来设置每应用程序的定制日志。
enable-cache	true	启用框架生成资源的缓存（JavaScript, CSS, 图象等等）。为了调试目的，开发的定制JavaScript和样式，防止使用在浏览器中旧的缓存数据。
forcenotrf	true	强制通过一个在任何JSF页 面上的HTML语法检查器的过滤器解析。 
 
4.2          Sun JSF RI
 
RichFaces不用任何另外的设置就能与JSF (JSF 1.2_12)和大部分JSF组件库一起工作。详情见：java.sun.com  [http://java.sun.com/javaee/javaserverfaces/]
 
当RichFaces与JSF 1.2_12一起使用时，如何获得ViewExpiredExceptions的其他信息，你可以在RichFaces Cookbook一文[http://wiki.jboss.org/auth/wiki//RichFacesCookbook/ViewExpiredException]中找到。
 
4.3          Apache MyFaces
 
RichFaces与Apache MyFaces 1.2.5版一起工作，包括特殊的库，如TOMAHAWK Sandbox 和Trinidad (早先的ADF Faces)。然而，要MyFaces与RichFaces一起工作，有一 些用于应用程序的配置的因素要顾及。
 
[注意：使用定义在web.xml文件中的不同过滤器存在冲突问题。要避免这些问题，RichFaces过滤器必须是 第一个，除了在web.xml配置文件中的其他过滤器之外。]
 
详情见http://myfaces.apache.org
 
在使用MyFaces + Seam时 还有一个问题。如果你使用这种组合，你应该在<f:view>（在你的代码 内，在它之后的右边）内部使用<a4j:page>包裹在你的页面内的其他内容，因为在myFaces内的<f:view>的具体实现有一些问题。
 
 
4.4          Facelets支持
 
Facelets高级功能支持是我们主要支持的功能之一，当与RichFaces一起工作时，使用Facelets的什么发布版是没有什么区别的。
 
你也应该顾及某些JSF框 架，比如Facelets使用自己的ViewHandler，你需要让它在视图处理器链中的首位出现，并且RichFaces AjaxViewHandler也不例外。在任何情况下，RichFaces首先安装它的视图处理器，所以在两种框架的情况下，例如RichFaces + Facelets，在设置中是没必要改变。虽然，在使用多于一个框架（除了RichFaces）时，可以使用VIEW_HANDLERS参数，根据它使用的顺序定义这些框架的视图处理器，例如，声明：
 
...
<context-param>
     <param-name>org.ajax4jsf.VIEW_HANDLERS</param-name>
     <param-value>com.sun.facelets.FaceletViewHandler</param-value>
</context-param>
...
 
正式说Facelets是第一位，然 而，AjaxViewHandler会临时超前一点，做一些小的，但是非常重要的工作。
 
[注意：在这种情况下，你不必在WEB-INF/faces-config.xml中定义FaceletViewHandler]
 
4.5          JBoss Seam支持
 
现在RichFaces开箱即可与JBoss Seam和Facelets一起使用，运行在JBoss AS4.0.4或更高版中。不再需要共享JAR文 件。你不过必须将RichFaces库与你的应用程序一起打包。
 
对Seam 1.2，你的web.xml应该是这样的：
 
<?xml version="1.0" ?>
<web-app xmlns="http://java.sun.com/xml/ns/j2ee"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                   xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/
j2ee/web-app_2_4.xsd"
                   version="2.4">
     <!-- richfaces -->
     <filter>
          <display-name>RichFaces Filter</display-name>
          <filter-name>richfaces</filter-name>
          <filter-class>org.ajax4jsf.Filter</filter-class>
     </filter>
     <filter-mapping>
          <filter-name>richfaces</filter-name>
          <url-pattern>*.seam</url-pattern>
     </filter-mapping>
     <!-- Seam -->
     <listener>
          <listener-class>org.jboss.seam.servlet.SeamListener</listener-class>
     </listener>
     <servlet>
          <servlet-name>Seam Resource Servlet</servlet-name>
          <servlet-class>org.jboss.seam.servlet.ResourceServlet</servlet-class>
     </servlet>
     <servlet-mapping>
          <servlet-name>Seam Resource Servlet</servlet-name>
          <url-pattern>/seam/resource/*</url-pattern>
     </servlet-mapping>
     <filter>
          <filter-name>Seam Filter</filter-name>
          <filter-class>org.jboss.seam.web.SeamFilter</filter-class>
     </filter>
     <filter-mapping>
          <filter-name>Seam Filter</filter-name>
          <url-pattern>/*</url-pattern>
     </filter-mapping>
     <!-- MyFaces -->
     <listener>
           <listener-class>org.apache.myfaces.webapp.StartupServletContextListener</listener-
class>
     </listener>
     <!-- JSF -->
     <context-param>
          <param-name>javax.faces.STATE_SAVING_METHOD</param-name>
          <param-value>client</param-value>
     </context-param>
     <context-param>
          <param-name>javax.faces.DEFAULT_SUFFIX</param-name>
         <param-value>.xhtml</param-value>
     </context-param>
     <servlet>
          <servlet-name>Faces Servlet</servlet-name>
          <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
          <load-on-startup>1</load-on-startup>
     </servlet>
     <servlet-mapping>
          <servlet-name>Faces Servlet</servlet-name>
          <url-pattern>*.seam</url-pattern>
     </servlet-mapping>
</web-app>
 
Seam 2支持RichFaces过滤器。因此， 对Seam 2，你的web.xml应该是这样的：
 
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5"
                   xmlns="http://java.sun.com/xml/ns/javaee"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                   xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/
ns/javaee/web-app_2_5.xsd">
     <context-param>
          <param-name>org.ajax4jsf.VIEW_HANDLERS</param-name>
          <param-value>com.sun.facelets.FaceletViewHandler</param-value>
     </context-param>
     <!-- Seam -->
     <listener>
          <listener-class>org.jboss.seam.servlet.SeamListener</listener-class>
     </listener>
     <servlet>
          <servlet-name>Seam Resource Servlet</servlet-name>
          <servlet-class>org.jboss.seam.servlet.SeamResourceServlet</servlet-class>
     </servlet>
     <servlet-mapping>
          <servlet-name>Seam Resource Servlet</servlet-name>
          <url-pattern>/seam/resource/*</url-pattern>
     </servlet-mapping>
     <filter>
          <filter-name>Seam Filter</filter-name>
          <filter-class>org.jboss.seam.servlet.SeamFilter</filter-class>
     </filter>
     <filter-mapping>
          <filter-name>Seam Filter</filter-name>
          <url-pattern>/*</url-pattern>
     </filter-mapping>
     <!-- JSF -->
     <context-param>
          <param-name>javax.faces.DEFAULT_SUFFIX</param-name>
          <param-value>.xhtml</param-value>
     </context-param>
     <context-param>
          <param-name>facelets.DEVELOPMENT</param-name>
          <param-value>true</param-value>
     </context-param>
     <servlet>
          <servlet-name>Faces Servlet</servlet-name>
          <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
          <load-on-startup>1</load-on-startup>
     </servlet>
     <servlet-mapping>
          <servlet-name>Faces Servlet</servlet-name>
          <url-pattern>*.seam</url-pattern>
     </servlet-mapping>
</web-app>
 
在Seam与MyFaces一起使用时，仍继续存在有一个问题。请看本节的myFaces部分。
 
有关如何集成Richfaces和Trinidad，以及如何隐藏在URL中 的“.seam”后缀的详细信息，你可以在RichFaces Cookbook文章[http://wiki.jboss.org/auth/wiki/RichFacesWithTrinidad]中找到。
 
4.6          Portlet支持
 
自从Ajax4jsf 1.1.1版本 开始，就已经支持JBoss Portlets。从RichFaces3.2.1改善这个支持。如果你面临某些问题，请提供你的有关RichFaces的兼容回馈。
 
4.7          Sybase EAServer
 
对Faces Servle的load-on-startup，你必须在web.xml中设置为0。
 
例子：
...
<servlet>
     <servlet-name>Faces Servlet</servlet-name>
     <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
     <load-on-startup>0</load-on-startup>
</servlet>
...
 
这是因为，EAServer在ServletContextInitializer之前调用init()。在Servlet 2.3规范中，不是一个EAServer程序错误。
 
4.8          Oracle AS/OC4J
 
为了部署你的使用了RichFaces组件的项目到一个Oracle AS中，你只是必须防止应用程序的类加载器导入Oracle XML解析器。在orion-application.xml中使用下面的注释：
 
...
<imported-shared-libraries>
     <remove-inherited name="oracle.xml"/>
     <remove-inherited name="oracle.xml.security"/>
</imported-shared-libraries>
...

5           RichFaces框架的基本概念
5.1          介绍
 
框架以一个组件库的方式实现，它增加了Ajax能力到存在的页面，所以，你不需要编写任何JavaScript代码或者用Ajax小配件替换存在的组件。RichFaces启用了页面范围的Ajax支持，而不是传统的组件范围支持。因此，你可以在页面上定义事件， 它调用一个Ajax请求，并且在由根据客户端引发的事件的Ajax请求改变了在服务器上的数据之后，应该变成为同步于JSF组件树的页面区域。
 
下图显示了它如何工作：
 

图5.1. 请求处理流
 
RichFaces允许定义（借助JSF标签）你希望使用Ajax请求更新的JSF页面的不同局部，并且提供许多选项用于发送Ajax请求到服务器。JSF也没有改变“标准”的JSF页面，并且你不需要手动编写任何JavaScript或XMLHTTPRequest，完全自动实现。
 
5.2          RichFaces体系结构概述
 
下图列出了RichFaces框架的几个重要元素
 

图5.2. 核心Ajax组件结构
 
Ajax Filter. 要得到RichFace的所有好处，你应该在你的应用程序中的web.xml文件中注册过滤器。过滤器识别多种请求类型。有关过滤器配置的必要信息可以在“过滤器配置”一节找到。在图5.3.中的序列图显示了一个“标准”JSF和一个Ajax请求不同处理方法。
 
在第一种情况，整个JSF树会被编码，在第二种情况，一个选项它取决于Ajax region（范围）的大小。正如你看见的一样，过滤器在发送Ajax响应内容到客户端之前会先解析它。
 
看下图，理解这种方法：

图5.3. 请求处理序列图
 
在两种情况中，有关需要的静态资源或你的应用程序请求的动态资源的信息被注册在的ResourseBuilder类中。
 
当一个资源请求来了时（图5.4），RichFaces过滤器在资源缓存中查找这个资源，如果有，则发送到客户端。否则，过滤器搜索在那些被ResourceBuilder注册的资源。如果资源已被注册，RichFaces过滤器会发送一个请求到ResourceBuilder，要求创建（递传）该资源。
 
下图显示了资源请求处理的方法

图5.4. 资源请求序列图
 
AJAX Action Components.  Ajax动作组件有： <a4j:commandButton> ,<a4j:commandLink> , <a4j:poll>和<a4j:support>等等。你可以使用它们从客户边来发送Ajax请求。
 
AJAX Containers.  AjaxContainer是一个接口，它描述了在一个Ajax请求期间应该被解码的你的JSF页面的一个区域。AjaxViewRoot和 AjaxRegion 是这个接口的实现。
 
JavaScript Engine.   RichFaces JavaScript Engine运行在客户边。它知道如何基于来自Ajax 的响应的信息更新你的JSF页面的不同区域。不直接使用JavaScript代码，因为它是自动可用的。
 
5.3          局部渲染
 
RichFaces框架利用启用了Ajax能力的组件的局部渲染增强了JSF框架。这意味着只有页面的局部应该受到某些更新改变的影响。组件的Ajax能力可以通过“mode”、“switchType”等等方式启用。这些方法防止了多页面刷新，它减少了服务器的负荷。
 
说明这个功能的一个好例子是显示<rich:tabPanel>的tabs（标签）。默认时，组件更新整个页面来显示点击tabs时tabs的内容，要启用局部显示，“switchType”属性就应该使用“"ajax”设置。
 
...
<rich:tabPanel switchType="ajax">
    <rich:tab label="Tab 1">
        Content of Tab 1
    </rich:tab>
    <rich:tab label="Tab 2">
        Content of Tab 2
    </rich:tab>
    <rich:tab label="Tab 3">
        Content of Tab 3
    </rich:tab>
</rich:tabPanel>
...
 
5.4          RichFaces的构成部件
 
RichFaces带有大量的构成部件（框架，库）：
 
         Prototype 1.6.0.3 [http://prototypejs.org]
          jQuery 1.3.1 [http://jquery.com]
          Script.aculo.us 1.8.1 [http://script.aculo.us]
 
有关框架和库加载的详情，见在FAQ中的[http://www.jboss.org/community/wiki/Commonclientside#resourcesfromjars]。
 
[注意：为了防止JavaScript版本冲突，你应该只使用一个版本的框架和库。有关库的排除，你可以找到更多信息，在FAQ 中的[http://www.jboss.org/community/wiki/Commonclientside#jsconflicts]

 
5.5          限制和规则
 
为了正确地创建RichFaces应用程序，要记住以下要点：
 
          任何Ajax框架不应该添加或删除，但是仅替换在页面中的元素。对成功的更新，具有与在响应中的相同ID的元素必须在页面中存在。如果你喜欢添加一些代码到页面，你应该为它们使用点位符（一些空元素）。同理，建议设置消息在“AjaxOutput”组件中（因为没有消息，也是一个消息）。
          不要对自显示容器使用<f:verbatim>，因为这个组件是暂时性的，没有保存了在树中。
          用XML格式的XMLHTTPRequest函数产生Ajax请求，但是这个XML绕过了可以在一个浏览器中进行的大部分验证和修正。因此，对HTML和XHTML，只创建一个严格的符合标准的代码，不要跳过任何所需的元素或属性。任何必要的XML修正是由在服务器上的XML过滤器自动产生，但是许多不可预料的效果可能由不正确的代码产生。
          RichFaces ViewHandler（视图处理器）放置在Facelets ViewHandlers的前面。
          RichFaces组件必须使用它们自己的渲染器。在渲染响应阶段，RichFaces框架遍历组件数，调用它自己的渲染器，并放置结果到Faces响应中。
 
5.6          Ajax请求优化
 
5.6.1     重新渲染
 
Ajax属性通用于Ajax组件，比如<a4j:support>，<a4j:commandButton>，<a4j:jsFunction>，<a4j:poll>，<a4j:push>等等。大多数带有内置Ajax支持的RichFaces组件也有这些用于相同目的的属性。Ajax组件的属性帮助暴露它的功能。大部分属性有默认值。因此，你不用了解这些属性也可以开始使用RichFaces。然而，它们的使用允许仔细地微调需要的Ajax行为。
 
“reRender”是一个主要属性。这个属性指向在一个页面上的区域，该区域应该用一个在Ajax交互中的响应进行更新。“reRender”属性的值是一个JSF组件的id或一个id列表。
 
下面是一个简单的例子：
 
...
<a4j:commandButton value="update" reRender="infoBlock"/>
...
<h:panelGrid id="infoBlock">
    ...
</h:panelGrid>
...
 
<a4j:commandButton>标签的“reRender”属性的值定义了你的页面的哪部分会被更新。在这个案例中，页面更新的部分只是<h:panelGrid>标签，因为它的id值与“reRender”属性的相匹配。正如你所见，更新页面上的多个元素并不困难，只是把它们的id列在“reRender”属性的值中即可。
 
“reRender”使用UIComponent.findComponent()算法[http://java.sun.com/javaee/
javaserverfaces/1.2_MR1/docs/api/javax/faces/component/UIComponent.html#findComponent(java.lang.String)]（带有某些附加的异常）查找在组件树中的组件。正如你所见，该算法假定了几个步骤。如果前面的步骤没有成功，才使用其他的每一个步骤。因此，你可以定义如何快速查找到更精确提及的组件。下面的例子显示了使用方法的区别（两个按钮会成功）。
 
...
<h:form id="form1">
    ...
    <a4j: commandButton value="Usual Way" reRender="infoBlock, infoBlock2" />
    <a4j:commandButton value="Shortcut" reRender=":infoBlockl,:sv:infoBlock2" />
    ...
</h:form>
<h:panelGrid id="infoBlock">
    ...
</h:panelGrid>
...
<f:subview id="sv">
    <h:panelGrid id="infoBlock2">
        ...
    </h:panelGrid>
    ...
</f:subview>
...
 
也可以使用JSF EL表达式作为reRender属性的一个值。它可能是一个Set、 Collection、Array 或者简单String类型的属性。在渲染响应阶段之前，用于reRender的EL会被正确解析。因此，你可以计算出在Ajax请求处理期间在任何前面的阶段中什么应该被重新渲染。
 
最普遍的问题是使用的reRender它指向的一个组件有一个“reRender”属性。注意，JSF没有在浏览器DOM中标识位置，在reRender条件返回false的情况时，组件的结果应该被放置在什么地方。因而，在Ajax请求期间，在组件被变成为渲染之后，RichFaces传递交渲染代码到客户端，但没有更新页面，因为不知道更新的位置。你需要指向没有“reRender”属性的父组件中的一个。作为选择，你也可以使用  <a4j:outputPanel>  layout="none" 包裹组件。
 
<a4j:outputPanel>的“ajaxRendered”属性设置为“true”，允许定义会被重新渲染的页面区域，即使在reRender属性中没有显示地指向它。如果在页面上你有一个区域，它应该用任何Ajax请求中的响应进行更新，这是非常有用的。例如，无论Ajax请求引起验证阶段什么样的失败，下面的代码都允许输出错误消息。
 
...
<a4j:outputPanel ajaxRendered="true">
    <h:messages />
</a4j:outputPanel>
...
 
“limitToList”属性允许解除<a4j:outputPanel>“ajaxRendered”属性的行为。limitToList = "true"意味着只更新在reRender属性中显示提及的区域。所有使用ajaxRendered="true"的面板被忽略。下面是一个例子：
 
...
<h:form>
    <h:inputText value="#{person.name}">
        <a4j:support event="onkeyup" reRender="test" limitToList="true"/>
    </h:inputText>
    <h:outputText value="#{person.name}" id="test"/>
</form>
...
 
5.6.2     队列和预防通信泛滥
 
“eventsQueue”属性定义队列的名字，它会被用来排序预定的Ajax请求。默认时，RichFaces没有排队Ajax请求。如果事件同时产生，他们会同时达到服务器。JSF实现（尤其是，第一个）不能保证第一个达到的请求会第一个被服务或传递到JSF生命周期。服务器边的数据如何依次被修改，在请求同时达到的情况下，是不可预料的。使用eventsQueue允许避免可能的混乱。如果你希望在你的应用程序中加强Ajax的通信，应显式定义队列名字。
 
如果“eventsQueue”属性被定义，在前一个请求没有处理和Ajax响应没有返回之前，接下来的请求会传递到相同的队列。此外，RichFaces开始从队列中删除“相似”的请求。“相似”的请求由相同的事件产生的请求。例如，根据下面的代码，如果你输入很快且已经输入了几个字符，在前面的Ajax响应还没有返回之前，只有新的请求会被送到服务器。
 
...
<h:inputText value="#{userBean.name}">
    <a4j:support event="onkeyup" eventsQueue="foo" reRender="bar" />
</h:inputText>
...
 
“requestDelay”属性定义请求在它准备好发送之前在队列中等待的时间（秒）。当延迟时间结束，请求会被发送到服务器，或被删除，如果一个最新的“相似”请求已经是在队列之中。
 
如果最新“相似”请求已经是在队列之中，“ignoreDupResponses”属性命令忽略请求产生的Ajax响应。ignoreDupResponses"="true"，不会中止请求，而是会在服务器上处理它，但只是允许如果响应丢失现状，用于避免在客户端上不必要的更新。
 
定义“eventsQueue”以及“requestDelay”，允许用于防止通信泛滥和同步Ajax请求序列。如果你有几个不同的Ajax请求源，在这里你可以定义相同的队列名字。如果你拥有组件，它根据用户事件产生的请求异步调用请求，这是非常有用的。例如，<a4j:poll> 或<a4j:push>。在这种情况下，来自这样的组件的请求修改相同的数据，同步可能是非常有用的。
 
详情见RichFace用户论坛[http://jboss.com/index.html?module=bb&op=viewtopic&t=105766]
 
“timeout”属性，用于设置一个特殊请求的响应等待的时间。如果在这个期间没有收到响应，请求被中止。
 
5.6.3     队列原则
 
从3.3.0版开始， RichFaces有一个改进的队列。
 
为什么改进队列是有一些原因的。在前面的版本，队列实现十分简单：在请求延迟期间，它只发送进入队列中的所有请求中的最后一个Ajax 请求。
 
改进后的队列准许：
 
          在几个JSF请求同时通过JSF生命周期时，消除了可能的冲突。队列预防发送这样的请求。只有一个请求被处理，其余的要等待。
          减少了在浏览器和服务器之间的通讯。“类似”的请求会被吸收。实际上只有最后一个会被发送。减少了请求数量，减少了服务器负荷。
 
有四种类型的队列：
 
          全局默认队列，定义在web.xml文件中。
          视图域默认队列。
         视图域命名队列。
          基于表单的默认队列。
 
本节我们会仔细看看上面列出来的四种队列类型，并且详细地了解它们的区别。详细的用法包含在<a4j:queue>章节。
 
5.6.3.1    全局默认队列，定义在web.xml文件中
 
设计细节
 
          在一个视图中只有一个全局队列会永远存在。
 
如果你用相同的名字定义了多个，而且试图设置它的属性，在渲染期间，一个警告会显示在服务器控制台。在第一个实例之后，所有相同名字的队列会被忽略。
 
         队列的类名是“org.richfaces.queue.global”
 
全局默认队列拥有应用程序域，并且在web.xml文件中定义。
 
如下所示：
 
...
<context-param>
   <param-name>org.richfaces.queue.global.enabled</param-name>
   <param-value>true</param-value>
</context-param>
...
 
默认时，全局默认队列被禁用，因为在一个页面上的所有Ajax请求的人工序列化会严重影响预期的行为。全局默认队列通过单个全局队列导致所有异步JavaScript和XML请求成为同步的。如何全局队列被打开，它可能改变在没有使用任何visible或obvious设置的应用程序的所有视图中的行为。
 
5.6.3.2    视图域默认队列
 
设计细节
 
          在每次特定视图或表单时，只有一个队列永远是活动的。
          如果发现了多个，在渲染期间，一个警告会显示在服务器控制台。在第一个实例之后，所有相同名字的队列会被忽略。
          拥有下面属性的组件（在这种情况下，队列有一个组件域）也会创建视图域默认队列：
 
             “requestDelay”
             “ignoreDupResponce”
 
          如果在一个组件中使用相同的名字定义了“eventsQueue”属性，但在视图中没有发现，会自动创建视图域默认队列。
 
视图域默认、命名和基于表单类型的队列利用<a4j:queue>标签覆盖在web.xml文件中定义的全局队列设置。
 
你也可以使用下面的内容，编程启用或禁用在单视图中的全局队列。
 
...
<a4j:queue name="org.richfaces.queue.global" disabled="true"... />
...
 
因此，要启用单视图页面的队列，你需要定义“disabled”属性为false。
 
现在，你使用<a4j:queue>组件的属性覆盖默认设置。完整的属性列表在指南的6.20. <a4j:queue>章节 [file:///C:/Projects/RichFaces/docs/userguide/en/target/docbook/publish/en-US/html_single/index.html#d0e10019]给出。
 
例子：
 
...
<a4j:queue name="org.richfaces.queue.global" requestDelay="1000" />
...
 
视图域队列也可以不用名字定义队列来进行添加。在这种情况下，它应该放置在表单外面的任何地方，目的在于不要被认为是基于表单的队列。
 
...
<a4j:queue ... />
...
 
5.6.3.3    视图域命名队列
 
设计细节
 
          命名队列必须有一个唯一的名字，如果第二个队列用相同的名字定义，所有相同名字的队列，在第一个实例之后，会被完全忽略。
         表单元素被用来作为队列的命名容器。例如，定义在表单内部的定制队列不能被在这个具体表单的外面的组件使用。
 
你可以从任何支持“eventsQueue”属性的Ajax4JSF或RichFaces的组件引用命名队列。下面是组件如何能够引用一个命名队列的一个例子：
 
例子：
 
...
<a4j:queue name="sampleQueue"/>                         
<h:inputText value="#{bean.inputValue}" >
    <a4j:support id="inputSupport" event="onkeyup" eventsQueue="sampleQueue"/>
</h:inputText>
<rich:comboBox  value="#{bean.state}"  suggestionValues="#{bean.suggestions}"  eventsQueue="sampleQueue"  /
>    
...
 
在这个例子中，两个组件（<a4j:queue>， <rich:comboBox>）通过“eventsQueue ”属性引用了命名队列（ "sampleQueue"）。
 
5.6.3.4    基于表单的默认队列
 
设计细节
 
         在一次只有一个基于表单的默认队列是活动的。
          如果多个基于表单的队列存在，在渲染期间，一个警告会显示在服务器控制台。在第一个实例之后，所有相同名字的队列会被忽略。
         用户可以定义多个表单队列，然而，除了一个之外，其他的都应该被禁用。
 
队列常用在表单内部，但是在表单内部的每个组件上定义“eventsQueue”属性可能是令人厌烦的工作。要避免了这样，你可以为一个表单创建一个默认队列（覆盖全局默认队列）。
 
你可以使用JSF <h:form>或Ajax4JSF <a4j:form>标签。
 
例子：
 
...
<h:form ... >
    <a4j:queue ... /><!-- note no name specified -->
    ...
</h:form>
...
 
尽管，使用Ajax4JSF <a4j:form>时，你可以通过“eventsQueue”引用一个命名队列。
 
例子：
 
...
<a4j:form eventsQueue="fooQueue" ...>
    ...
</a4j:form>
...
 
然而，队列的实现，允许你从一个具有一个基于表单的队列的表单中引用一个命名队列。
 
例子：
 
...
<a4j:queue name="sampleQueue" ... /> <!-- named queue -->
...
<h:form ... >
    <a4j:queue ... /><!-- form-based queue-->
    <a4j:commandButton ... /> <!-- uses the form-based queue -->
    <a4j:commandButton eventsQueue="sampleQueue" /> <!-- uses named queue -->
</h:form>
...
 
5.6.3.5    队列的功能性
 
本节将介绍一些队列的功能性等方面的问题。
 
5.6.3.5.1   事件的相似性
 
默认时，对对列而言，由相同组件引发的所有事件是相似的（根据事件源的客户端id）。这意味着，如果新的请求来自相同的组件，它们会与前面的组合。例如，如果在一个输入字段域上使用a4j:support，并且用户频繁的输入，在requestDelay期间，由键盘输入引发的所有请求会被组合为一个。
 
你也可以手工指定多个组件，它们会产生相似的请求。“similarityGroupingId”属性可以添加到3.3.0发布的Ajax动作组件。因此，例如，你可以添加两个<a4j:support/>组件到一个输入字段域上（一个用于键盘事件，一个用于鼠标的blur事件），并且定义请求事件是相似于similarityGroupingId指定的事件。
 
5.6.3.5.2   在请求延迟期间的相似请求
 
在requestDelay期间，如下面编写的请求被收集在队列之中，并且相似的会被组合。但是，如果相似请求连续地被引发，他们只能被组合。这样做是为了不阻塞队列，并且不改变请求的顺序。
 
例如：
 
一个带有一些延迟的请求到达队列，让这个请求的延迟计数器从A1开始。如果相似请求（例如，来自相同的组件 —— A2）出现 —— 这两个请求被组合（A1 A2为Acombined）且计数器被复位。
 
但是不相似请求到达队列B1 —— 它被放置在第一个的后面（Acombined，B1）。并且如果Acombined没有存在队列中，而另外的请求到达A（让它为A3）再出现 —— 这些请求不会与第一个组合，而是放置在B1的之后（Acombined，B1，A3）。
 
这样的行为准许：
 
          最大限度的提高相似请求的吞吐量。
         只发送相似请求的最新字段域的状态。
          如果不同类型的请求到达队列，不会阻塞队列，并且应该再等待一个。
 
从3.3.0版开始，<a4j:poll>组件默认时，延迟时间为0，目的在于不使用队列延迟（参数它自身的值重新定义队列的参数）来避免在队列中的阻塞定期更新。如果需要，你可以在组件级上定义它。
 
5.6.3.5.3   JavaScript API
 
表5.1 JavaScript API
函数	 描述
getSize()	返回当前队列的大小。
getMaximumSize()	返回队列的最大尺寸，用"size" 属性指定的。
 
 
5.6.4     数据处理选项
 
RichFaces使用基于Ajax请求发送的方法的表单。这意味着每次，当你点Ajax按钮或 <a4j:poll>产生一个异步请求时，来自最近表单的数据随XMLHTTPRequest对象一起被提交。表单数据包含来自表单输入元素的值，以及辅助信息，比如保存数据的状态。
 
当“ajaxSingle”属性的值为“ true”，它命令只包括当前组件的一个值（连同  <f:param> 或 <a4j:actionparam> 的值一起，如果有）到请求映射。在<a4j:support>的情况中，它是父组件的一个值。下面是一个例子：
 
...
<h:form>
    <h:inputText value="#{person.name}">
        <a4j:support event="onkeyup" reRender="test" ajaxSingle="true"/>
    </h:inputText>
    <h:inputText value="#{person.middleName}"/>
</form>
...
 
在这个例子中，因为ajaxSingle="true"的使用，请求只包含引起请求产生的输入组件，没有包含在表单中的所有组件。
 
注意，ajaxSingle="true"减少了即将到来的通讯，但并不会阻碍在服务器边上的其他输入组件的解码。某些JSF组件，比如<h:selectOneMenu>，识别在请求映射值中的遗漏数据，如一个null值，并尝试使用失败结果通过验证过程。因此，使用 <a4j:region>来限制组件树的一部分，在需要的时候，会在服务器边处理它。
 
"immediate"属性与其他任何非JSF组件一样有相同的用途。默认的"ActionListener"应该立刻被执行（即在一个请求处理生命周期的应用请求值阶段期间），而不是等待，直到调用应用程序阶段。使用immediate="true"是让某些数据模型的值更新的方法之一，在其他方法由于一个具有成功通过验证阶段的问题不能被更新时。
 
"bypassUpdates"属性允许绕过更新阶段。如果你需要根据你的验证器检查你的输入，但又不想使用这些数据更新模型，它可能是非常有用的。注意，如果验证阶段是成功通过，这个动作只会在验证阶段结束时被调用。
 
5.6.5     动作和导航
 
Ajax组件是相似于任何其他非Ajax JSF组件，如<h:commandButton>。它允许提交表单。你可以使用"action"和"actionListener"属性调用动作方法和定义动作事件。
 
如果你希望使用带有局部页面更新的一个Ajax响应，"action"方法必须返回null。而所谓的“Ajax请求生成的非Ajax响应”普通模式。在这种情况下，动作不会返回null，但是动作输出一个与导航规则相匹配的结果，RichFaces启动时使用“Ajax请求生成的非Ajax响应”模式。这种模式主要用于以下两种情况：
 
          RichFaces准许在<a4j:include>内组织一个页面流。这是一种典型情况，用于向导，如行为。新的内容在<a4j:include>区域内被渲染。内容取自faces配置文件（通常是faces-config.xml）的导航规则。注意，该“向导”的内容不是独立于页面的其余部分。包含的页面应该没有自己的 <f:view>（如果使用facelets，它不要紧）。你需要在<a4j:include>内使用Ajax组件来导航向导页面。否则，会执行整个页面更新。
          如果你希望调用服务器边验证器，并且如果成功通过了验证阶段，你只希望导航到下一个页面，你可以使用<a4j:commandButton>替换<h:commandButton>，并指向导航到下一个页面的动作方法。如果验证处理失败，一个局部页面更新会发生，并且你会看见一个错误消息。否则，应用程序进行到下一个页面。要避免内存泄漏，确保你定义了<redirect/>，用于导航规则。 

5.6.6     JavaScript交互
 
RichFaces准许不用任何Javascript代码编写启用了Ajax的JSF应用程序。然而，如果你需要，你仍然可以调用Javascrip代码。有几个Ajax属性可以帮助来完成它。
 
"onsubmit"属性允许在Ajax请求被发送之前调用Javascrip代码。如果"onsubmit"返回"false"，则Ajax请求被中止。"onsubmit"代码被插入在RichFaces Ajax调用之前。因此，如果你希望Ajax请求被发送，"onsubmit"不应该有"return"语句。如果你打算调用一个返回"true"或 "false"的 JavaScript函数，当你需要中止请求时，只使用条件语句返回。例如：
 
...
onsubmit="if (mynosendfunct()==false){return false}"
...
 
"onclick"属性类似于"onsubmit"，但是用于可点击组件，比如<a4j:commandLink>和<a4j:commandButton>。如果返回"false"，Ajax请求也被中止。
 
"oncomplete"属性，用于Ajax响应被返回和DOM被更新之后，传递给会被正确调用的JavaScript 。不推荐在EL表达式内部使用this关键字，因为它始终不会指向Ajax请求会被初始化的组件。
 
"onbeforedomupdate"属性定义调用的JavaScript代码，用于一个客户边上，在收到Ajax响应之后和在 DOM更新之前。
 
"data"属性允许在Ajax调用期间，从服务器获得其他数据。你可以使用JSF EL指向管理的bean的属性，并且它的值以JSON格式被序列化，且可用于客户边。你可以使用"data"变量引用它。例如：
 
...
<a4j:commandButton  value="Update"  data="#{userBean.name}"  oncomplete="showTheName(data.name)"  /
>
...
 
RichFaces不仅允许序列化原始类型成为JSON格式，而且也支持复杂类型，包括数组和集合。使用"data"引用的bean应该被序列化。
 
有大量有用的函数可以用于JavaScript中：
 
     rich:clientId('id') —— 用短id返回客户端id，或者如果组件指定的id没有发现使用null。
     rich:element('id') —— 是document.getElementById(#{rich:clientId('id')})的快捷方式。
     rich:component('id') ——  是#{rich:clientId('id')}.component的快捷方式。
     rich:findComponent('id') —— 返回UIComponent的一个实例，以组件的短id作为参数。 
 
...
<h:inputText id="myInput">
    <a4j:support event="onkeyup" reRender="outtext"/>
</h:inputText>
<h:outputText id="outtext" value="#{rich:findComponent('myInput').value}" />
...
 
5.6.7     迭代组件的Ajax属性
 
"ajaxKeys"属性定义在Ajax请求之后被更新的字符串。它可以提供独立地更新几个子组件，而不用更新整个页面。
 
...
<a4j:poll intervall="1000" action="#{repeater.action}" reRender="text">
    <table>
        <tbody>
            <a4j:repeat value="#{bean.props}" var="detail" ajaxKeys="#{repeater.ajaxedRowsSet}">
                <tr>
                    <td>
                        <h:outputText value="detail.someProperty" id="text"/>
                    </td>
                </tr>
            </a4j:repeat>
        </tbody>
    </table>
</a4j:poll>
...
 
5.6.8     其他有用的Ajax属性
 
"status"属性用于Ajax组件（比如，<a4j:commandButton>，<a4j:poll>等等）指向<a4j:status>组件的ID。如果你希望在来自不同区域的不同Ajax组件之间共享<a4j:status>组件，使用这个属性。如下所示：
 
...
<a4j:region id="extr">
    <h:form>
        <h:outputText value="Status:" />
        <a4j:status id="commonstatus" startText="In Progress...." stopText=""/>
        <h:panelGrid columns="2">
            <h:outputText value="Name"/>
            <h:inputText id="name" value="#{userBean.name}">
                <a4j:support event="onkeyup" reRender="out" />
            </h:inputText>
            <h:outputText value="Job"/>
            <a4j:region  id="intr">
 
                <h:inputText id="job" value="#{userBean.job}">
                    <a4j:support event="onkeyup"  reRender="out" status="commonstatus"/>
                </h:inputText>
            </a4j:region>
        </h:panelGrid>
        <a4j:region>
            <h:outputText id="out" value="Name: #{userBean.name}, Job: #{userBean.job}" />
            <br />
            <a4j:commandButton ajaxSingle="true" value="Clean Up Form" reRender="name, job,
 out"  status="commonstatus">
                <a4j:actionparam name="n" value=""  assignTo="#{userBean.name}" />
                <a4j:actionparam name="j" value=""  assignTo="#{userBean.job}" />
            </a4j:commandButton>
        </a4j:region>
    </h:form>
</a4j:region>
...
 
在这个例子中， <a4j:support>和<a4j:commandButton>被定义在不同的区域。这些组件的"status"属性的值指向<a4j:status>（	原文为 <a4j:support>）的ID。因此，<a4j:status>（	原文为 <a4j:support>）组件被来自不同区域的两个组件共享。
 
详情见RichFaces Live Demo [http://livedemo.exadel.com/richfaces-demo/richfaces/status.jsf?c=status] 。
 
其它有用的属性是"focus"。它指向一个组件的ID，在Ajax请求之后，组件会被设置为焦点。
 
5.6.9     通常Ajax属性
 
本节汇总了rich和a4j组件拥有的所有与Ajax相关的属性。
 
表5.2. 通常的Ajax属性
属性	描述	A4j组件	Rich组件
ajaxSingle	限制JSF树的处理（解码，转换，验证和模型更新）只对发送请求的组件。 布尔值。默认为"false"。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>	<rich:dataFilterSlider>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:toolTip>
<rich:calendar>
<rich:fileUpload>
<rich:suggestionbox>
bypassUpdates	如果为 "true"，在验证处理阶段 ，它根据一个强制渲染响应跳过模型bean的更新。它可以被用来验证组件的输入。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>	<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:calendar>
<rich:suggestionbox>
limitToList	如果为"true"，则在页面上所有那些AJAX渲染的组件才会被更新，它的ID传递给组件可描述的"reRender"属性。默认值为"false"意味着所有使用ajaxRendered="true"的组件会被更新。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:calendar>
<rich:suggestionbox>
reRender	组件的id（用调用UIComponent.findComponent()的形式），如果由这个组件引发Ajax请求，渲染。可以是单个id、逗号分隔的Id列表或使用数组和集体的EL表达式。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:dataTable>
<rich:extendedDataTable>
<rich:scrollableDataTable>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:calendar>
<rich:suggestionbox>
process	组件的id（用调用UIComponent.findComponent()的形式），如果由这个组件引发Ajax请求，在2-5阶段处理。可以是单个id、逗号分隔的Id列表或使用数组和集体的EL表达式。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>	<rich:dataFilterSlider>
<rich:datascroller>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:calendar>
<rich:suggestionbox>
status	请求状态组件的id（用调用UIComponent.findComponent()的形式）	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>
<a4j:queue>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dragSupport>
<rich:dropSupport>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:calendar>
<rich:fileUpload>
<rich:suggestionbox>
eventsQueue	队列名字，用于避免在完成来自相同事件的其他请求之前发送下一个请求。可以被用来减少频繁请求的数量（按键，鼠标移动等等）。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:calendar>
<rich:suggestionbox>
requestDelay	定义时间（用秒）的属性，在请求准备发送之前，它在队列中等待的时间。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:queue>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:simpleTogglePanel>
<rich:tab>
<rich:calendar>
<rich:suggestionbox>
data	序列化（在默认时，以JSON格式）在客户端由开发者在AJAX请求时传递的数据。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:paint2D>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:calendar>
ignoreDupResponses	如果最新“相似”请求已经是在队列之中，“ignoreDupResponses”属性命令忽略请求产生的Ajax响应。ignoreDupResponses"="true"，不会中止请求，而是会在服务器上处理它，但只是允许如果响应丢失现状，用于避免在客户端上不必要的更新。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>
<a4j:queue>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:calendar>
<rich:suggestionbox>
timeout	在一个特殊请求时的响应等待时间。如果在这个时间没有收到响应，中止请求。	<a4j:form>
<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>
<a4j:queue>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:suggestionbox>
similarityGroupingId	如果任何组件使用了相同的ID，那么这些组件会被分组。	<a4j:form>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>	<rich:ajaxValidator>
<rich:dataFilterSlider>
<rich:datascroller>
<rich:scrollableDataTable>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:treeNode>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tab>
<rich:toggleControl>
<rich:calendar>
<rich:suggestionbox>
<rich:message>
<rich:messages>
keepTransient	标志用于标记所有子组件为临时的。如果为"true"，所有子组件会被设置为非临时的状态，并且维持在保存的组件树中。用于输出在自渲染区域中的所有内容（默认时，所有在<f:verbatim>标签中所有内容和在Facelets中的非JSF元素，标记为临时的，因为自渲染区域不是用于ajax处理的简单输出区域）。默认值为"false"。	<a4j:include>
<a4j:outputPanel>	 
ajaxListener	方法表达式，表示一个动作侦听器方法，当这个组件被ajax请求激活时会通知它，并且处理它。表达式的计算结果必须为一个带有AjaxEvent参数的public void方法。	<a4j:include>
<a4j:outputPanel>	 
selfRendered	如果为"true"，在调用应用程序（或解码，如果immediate属性设置为真）阶段时，自渲染子树。	<a4j:page>
<a4j:region>	<rich:suggestionbox>
immediate	标志指明，如果组件被ajax请求激活，通知应该立即被传递到感兴趣的侦听器和动作。（即，在应用请求值阶段期间），而不是等待直到调用应用程序阶段。	<a4j:region>
<a4j:region>
<a4j:support>
<a4j:commandButton>
<a4j:commandLink>
<a4j:jsFunction>
<a4j:poll>
<a4j:push>
<a4j:page>
<a4j:htmlCommandLink> 	<rich:dataFilterSlider>
<rich:datascroller>
<rich:dragSupport>
<rich:dropSupport>
<rich:menuItem>
<rich:tree>
<rich:panelBar>
<rich:panelMenu>
<rich:panelMenuGroup>
<rich:panelMenuItem>
<rich:progressBar>
<rich:simpleTogglePanel>
<rich:tabPanel>
<rich:tab>
<rich:togglePanel>
<rich:toggleControl>
<rich:toolTip>
<rich:calendar>
<rich:colorPicker>
<rich:comboBox>
<rich:editor>
<rich:inplaceInput>
<rich:inplaceSelect>
<rich:inputNumberSlider>
<rich:inputNumberSpinner>
<rich:suggestionbox>
<rich:listShuttle>
<rich:orderingList>
<rich:pickList>
mode	定义提交类型：Ajax或 Sever	 	<rich:panelMenu>
<rich:panelMenuItem>
<rich:progressBar>
<rich:toolTip>
switchType	定义渲染模式：Ajax，
server，client。	 	<rich:calendar>
<rich:simpleTogglePanel>
<rich:tabPanel>
<rich:tab>
<rich:togglePanel>
<rich:tree>
<rich:simpleTogglePanel>
 
5.7          如何……
 
5.7.1     发送一个Ajax请求
 
有不同的方法从你的JSF页面发送Ajax请求。例如，你可以使用<a4j:commandButton>，<a4j:commandLink> ，<a4j:poll>或 <a4j:support>标签或者任何其他的。
 
所有这些标签隐藏了普通的JavaScript行为，XMHTTPRequest对象构建和Ajax请求发送需要它。它们也允许你决定你的JSF页面的那个组件利用Ajax响应来重新被渲染（你可以在"reRender" 属性中列出这些组件的ID）。
 
<a4j:commandButton>和 <a4j:commandLink>标签被用来根据"onclick"  JavaScript事件发送Ajax请求。
 
<a4j:poll>标签被用来周期性的发送Ajax请求，使用一个计时器。
 
<a4j:support>标签允许你添加Ajax功能到标准的JSF组件，并且发送Ajax请求到一个选定的JavaScript事件中："onkeyup"，"onmouseover"等等。
 
5.7.2     决定发送什么
 
你可以在页面上描述一个你希望发送到服务器的区域，使用这种方法，当你发送一个Ajax请求时，你可以控制在JSF视图中的那部分在服务器边被解码。
 
最容易的方法是在你的JSF页面上描述一个什么也不做的Ajax区域，因为在  <f:view>和</f:view>标签之间的内容被认为是默认的Ajax区域。
 
使用<a4j:region>标签，你可以在你的JSF页面上定义多个Ajax区域（甚至嵌套它们）。
 
如果你希望活动区域之外渲染一个Ajax响应的内容，那么"renderRegionOnly"属性的值应该设置为"false"（"false"是默认值）。否则，你的Ajax更新被限制为活动区域的元素。
 
5.7.3     决定改变什么
 
在多数情况下，在"reRender"属性中使用ID来定义"AJAX zones" ，用于更新工作会更好。
 
如果你的页面包含，例如，一个<f:verbatim>标签，并且你希望根据一个Ajax响应更新它的内容，那么你可以不使用这种方法。
 
使用<f:verbatim/> 标签的问题，象上面描述一样，与JSF组件的transientFlag的值有关联。如果这个标志的值为true，组件必须不参与状态保存和恢复的过程。
 
以便解决这类问题，RichFaces使用了一个输出面板的概念，它使用<a4j:outputPanel>标签定义。如果你设置一个<f:verbatim>标签在该输出面板的内部，那么<f:verbatim/>标签的内容和其他面板的子标签的内容可以根据Ajax响应被更新。 有两种方法控制它：
 
          通过设置"ajaxRendered"属性的值为"true"。
          通过设置一个动作组件的"reRender"属性的值为输出面板的ID。
 
5.7.4     决定处理什么
 
"process"属性允许定义与ajaxSingle标识的或区域包裹的组件一起被处理的组件id。
 
当你需要在视图的不同局部仅处理两个组件时，你可以使用"process"属性。
 
设想你需要只处理两个输入字段域，而不是所有视图。如果你包裹第一个输入为区域，或者让<a4j:support>组件使用ajaxSingle="true"嵌套第二输入，将不会被处理。
 
下面是一个简单的解决方案：
 
...
<h:inputText value="#{bean.name}" id="name">
    <a4j:support ajaxSingle="true" process="email" event="onblur" reRender="someOut"/>
</h:inputText>
<h:inputTextarea value="#{bean.description}" id="desc" />
<h:inputText value="#{bean.email}" id="email">
    <a4j:support ajaxSingle="true" process="name" event="onblur" reRender="someOut"/>
</h:inputText>
...
 
在上面的例子中，当id="name"的输入字段域失去焦点时，一个Ajax请求被发送。所以只有两个字段域（id="name"和id="email"）被处理：解码、转换/验证和值应用阶段被执行。id="email"的输入字段域根据失焦事件以同样的方式被处理。
 
5.8          过滤器配置
 
RichFaces使用了一个过滤器，用于根据Ajax请求接受到的代码的更正。在“标准”JSF请求的情况下，浏览器独立地做更正。在Ajax请求的情况下，为了防止布局被摧毁，需要使用过滤器，因为收到的代码可能不同与浏览器验证的代码，并且浏览器不能做任何更正。
 
下面是一个在你的应用程序的web.xml文件中设置过滤器的例子：
 
...
<filter>
    <display-name>RichFaces Filter</display-name>
    <filter-name>richfaces</filter-name>
    <filter-class>org.ajax4jsf.Filter</filter-class>
</filter>
...
 
[注意：快速过滤器已被废弃，只用于与前面的RichFaces版本向后兼容。不推荐使用快速过滤器，因为有另外一种方式使用这种功能，通过Neko filter type [58]的手段。]
 
从RichFaces 3.2开始，过滤器的配置变得更灵活。它可以对相同的应用程序的不同的页面集合配置不同的过滤器。
 
可能的过滤器类型是：
 
          TIDY —— TIDY过滤器基于TIDY解析器。这个过滤器推荐用于使用了复杂的或非标准的标记，当响应来自服务器时，当所有必要的代码由过滤器做更正时。
          NEKO —— NEKO过滤器修正了前面的快速过滤器，并且基于NEKO解析器。在使用这个过滤器的情况下，代码没有被严格校验。使用它，你要确保你的应用程序标记是严格用于这个过滤器的。否则可能会导致很多错误和恶化布局结果。这个过滤器大大加快了Ajax请求的处理。
          NONE —— 没有更正
 
一个配置例子，如下所示：
 
...
<context-param>
    <param-name>org.ajax4jsf.xmlparser.ORDER</param-name>
    <param-value>NONE,NEKO,TIDY</param-value>
</context-param>
<context-param>
    <param-name>org.ajax4jsf.xmlparser.NONE</param-name>
    <param-value>/pages/performance\.xhtml,/pages/default.*\.xhtml</param-value>
</context-param>
<context-param>
    <param-name>org.ajax4jsf.xmlparser.NEKO</param-name>
    <param-value>/pages/repeat\.xhtml</param-value>
</context-param>
<filter>
    <display-name>RichFaces Filter</display-name>
    <filter-name>richfaces</filter-name>
    <filter-class>org.ajax4jsf.Filter</filter-class>
</filter>
<filter-mapping>
    <filter-name>richfaces</filter-name>
    <servlet-name>Faces Servlet</servlet-name>
    <dispatcher>FORWARD</dispatcher>
    <dispatcher>REQUEST</dispatcher>
    <dispatcher>INCLUDE</dispatcher>
</filter-mapping>
...
 
这个例子显示的ORDER参数，定义了用于页面代码更正的特殊过滤器类型的顺序。
 
首先，所有"NONE"类型指定给过滤器。然后，两个不同的页面集合被定义，相应地使用了两个过滤器类型（NONE和NEKO）。如果页面涉及第一个集合，如下定义它：
 
<param-value>/pages/performance\.xhtml,/pages/default.*\.xhtml</param-value>
 
没有更正，因为这个页面的过滤器类型被定义为"NONE"。如果页面不是出自于第一个集合，则设置"NEKO"类型。
 
如果页面涉及第二个集合，如下定义它：
 
<param-value>/pages/repeat\.xhtml</param-value>
那么"NEKO"类型被用于更正。如果没有涉及第二个集合，则为该过滤器设置为"TIDY"（"TIDY"过滤器类型用于代码更正）。
 
5.9          脚本和样式加载策略
 
在3.1.3版本之前，RichFaces根据需要加载样式表和脚本。即如果在一个特定页面上需要它们，才加载文件。从RichFaces 3.1.3开始，是可以管理RichFaces脚本和样式表文件如何被加载到应用程序。
 
org.richfaces.LoadScriptStrategy
 
下面在你的web.xml文件中的声明，准许加载完整的脚本文件。
 
...
<context-param>
    <param-name>org.richfaces.LoadScriptStrategy</param-name>
    <param-value>ALL</param-value>
</context-param>
...
 
如果你在web.xml文件中没有声明org.richfaces.LoadScriptStrategy，它等价于：
 
...
<context-param>
    <param-name>org.richfaces.LoadScriptStrategy</param-name>
    <param-value>DEFAULT</param-value>
</context-param>
...
 
第三种可能值是"NONE"。你没有一个特殊原因使用它，除非你获得了一个最新的（或修改）脚本版本，并且希望手动包括它在页面头中。
 
org.richfaces.LoadStyleStrategy
 
下面在你的web.xml文件中的声明，准许只加载一个完整的样式表文件。
 
...
<context-param>
    <param-name>org.richfaces.LoadStyleStrategy</param-name>
    <param-value>ALL</param-value>
</context-param>
...
 
完整的样式表包含用于所有加载的组件的样式。换肤功能仍然工作。
"DEFAULT"的值是一个典型的按需变量。
 
"NONE"停止加载任何样式。重新设置较早引入的纯皮肤的所有颜色和字体的参数为null。org.richfaces.LoadStyleStrategy的"NONE"值，意味着RichFaces的预定义样式不被使用。
     详情见RichFaces User Forum
 [http://www.jboss.com/index.html?module=bb&op=viewtopic&p=4114033]
 
5.10       请求的错误和会话期满处理
 
RichFaces准许重新定义标准的处理器，负责不同的异常情况的处理。它帮助定义自己的JavaScript，在那些情况发生时，执行它。
 
添加下面的代码到web.xml中：
 
<context-param>
    <param-name>org.ajax4jsf.handleViewExpiredOnClient</param-name>
    <param-value>true</param-value>
</context-param>
        
5.10.1 请求的错误处理
 
假如在Ajax请求期间的一个错误，在客户端要执行你自己的代码，需要重新定义标准的"A4J.AJAX.onError"方法。
 
A4J.AJAX.onError = function(req, status, message){
    window.alert("Custom onError handler "+message);
}
 
以这种方式定义的函数访问的参数：
 
          req ——  一个参数，调用错误的请求的字符串
          status ——  由服务器返回的错误号
          message ——  特定错误的默认消息。
 
因此，你可以创建你自己的处理器，它在超时、内部服务器错误等等时被调用。
 
5.10.2 会话期满处理
 
也可以重新定义"onExpired"框架方法，它在"Session Expiration"事件时被调用。例如：
 
A4J.AJAX.onExpired = function(loc, expiredMsg){
    if(window.confirm("Custom onExpired handler "+expiredMsg+" for a location: "+loc)){
      return loc;
    } else {
     return false;
    }
}
 
该函数接收的参数：
 
          loc  ——  当前页面的URL（根据需要可以被更新）
         expiredMsg —— 在 "Session Expiration"事件中默认的一个消息。 
 
[注意：在MyFaces下定制的"onError",  "onExpire"不能运行。MyFaces通过它内部生成的调试页面处理异常。要防止这样的行为，你可以使用下面的代码：
...
<context-param>
    <param-name>org.apache.myfaces.ERROR_HANDLING</param-name>
    <param-value>false</param-value>
</context-param> 
...
]
 
  
5.11       换肤
 
5.11.1 为什么换肤
 
如果你看看在企业应用程序中的一个CSS文件，例如，你现在运行的一个，你常常会看到相同的颜色如何被记录在它里面。标准的CSS没有办法来定义一个特殊抽象的颜色，用于定义面板标题的颜色，活动弹出菜单项的背景颜色，分隔带的颜色等等。要定义普通的界面样式，你不得不反复拷贝相同的值，并且你的界面元素越多，你需要执行的拷贝和粘贴的活动就越多。
 
因此，如果你希望改变应用程序的调色板，你必须改变所有相互关联的值，否则，你的界面可能会显得有点笨拙。发生这种界面的机会是很高的，因为CCS编辑变成了普通开发者的任务，而他并不一定有很多用户界面设计的知识。
 
此外，如果消费者希望有一个可以由终端用户快速调节的界面观感，你的工作会翻倍，因为你必须处理几个CCS文件的变体，它们每个包含相同的重复多次的值。
 
这些问题可以使用构建在RichFaces项目内的换肤系统来解决，并且完全由RichFaces实现。每个命名的皮肤有一些用于调色板定义的皮肤参数和其他的用户界面参数。仅通过改变一些参数，你可以改变在一个应用程序中的许多组件的外观，用一种同步的方式，不用破坏用户界面的一致性。
 
换肤功能不能完全替换标准的CSS，并且肯定不能消除它的使用。换肤是标准CSS的一个高级扩展，它可以与标准的CSS声明一起使用。你可以通过EL表达式在CSS中引用皮肤参数。你完全有能力来同步在你页面上的所有元素的外观。
 
5.11.2 使用换肤
 
RichFaces换肤被设计为与下面所列的一起混合使用：
 
          在RichFaces框架中定义的皮肤参数
          组件预定义的CSS类
         用户样式（style）类
 
组件的配色方案，利用下面的三种样式类，可以用于它自己的元素：
 
          插入到框架内的默认样式类。
 
它包含样式参数，其连接到来自一个皮肤的某些常数。它被定义用于每个组件，并且指定一个默认的表示级别。因此，通过改变皮肤参数的值，一个应用程序的界面可以被修改。
 
         皮肤扩展样式类
 
这个类名被定义用于每个组件的元素，并且插入到框架内，允许使用相同的名字定义一个类到它的CCS文件中。因此，使用这个类的所有组件的外观被扩展了。
 
          用户样式类
 
可以使用styleClass参数之一，用于组件元素，并且用它定义你自己的类。结果是，一个特殊组件的外观，根据一个在该类中指定的CSS样式参数，被改变了。
 
5.11.3 例子
 
下面是一个面板组件的例子：
 
<rich:panel> ... </rich:panel>
            
代码在页面生成一个面板，它包括两个元素：一个包裹器<div>元素和一个<div>元素，其用于使用了特殊样式属性的面板主体。包裹器<div>元素如下所示：
 
<div class="dr-pnl rich-panel">
     ...
</div>
 
dr-pnl是在框架中通过皮肤参数指定的一个CSS类：
 
         background-color（背景色）使用generalBackgroundColor定义
        border-color（边界色）使用panelBorderColor定义
 
通过改变这些皮肤参数，可以改变在页面上所有面板的所有的颜色。
 
然而，如果在页面上的某处指定了<rich:panel>类，它的参数也会被在页面上的所有面板获取。
 
开发者也可以改变一个特殊面板的样式属性。如下所示：
 
<rich:panel styleClass="customClass" />
 
可以从customClass增加一些样式属性到一个特定的面板，因此，我们得到第三种样式：
 
<div class="dr_pnl rich-panel customClass"> 
    ...
</div>
            
 
5.11.4 在RichFaces中的皮肤参数表
 
RichFaces在最简单的普通定制层次提供了八个预定义的皮肤参数（皮肤）：
 
          DEFAULT
          plain
         emeraldTown
          blueSky
          wine
          japanCherry
          ruby
          classic
         deepMarine
 
要插入一个进来，需要使用org.richfaces.SKIN上下参数指定一个皮肤的名字。
 
下面是一个例子，使用了主要皮肤之一"blueSky"的值的一个表。
 
表5.3 颜色
参数名	默认值
headerBackgroundColor	#BED6F8
headerGradientColor	#F2F7FF
headTextColor	#000000
headerWeightFont	bold
generalBackgroundColor	#FFFFFF
generalTextColor	#000000
generalSizeFont	11px
generalFamilyFont	Arial,
Verdana,	sans-serif
controlTextColor	#000000
controlBackgroundColor	#ffffff
additionalBackgroundColor	#ECF4FE
shadowBackgroundColor	#000000
shadowOpacity	1
panelBorderColor	#BED6F8
subBorderColor	#ffffff
tabBackgroundColor	#C6DEFF
tabDisabledTextColor	#8DB7F3
trimColor	#D6E6FB
tipBackgroundColor	#FAE6B0
tipBorderColor	#E5973E
selectControlColor	#E79A00
generalLinkColor	#0078D0
hoverLinkColor	#0090FF
visitedLinkColor	#0090FF
 
表5.4 字体
参数名	默认值
headerSizeFont	11px
headerFamilyFont	Arial, Verdana, sans-serif
tabSizeFont	11px
tabFamilyFont	Arial, Verdana, sans-serif
buttonSizeFont	11px
buttonFamilyFont	Arial, Verdana, sans-serif
tableBackgroundColor	#FFFFFF
tableFooterBackgroundColor	#cccccc
tableSubfooterBackgroundColor	#f1f1f1
tableBorderColor	#C0C0C0
 
从3.0.2开始，增加了皮肤"plain"。它没有任何参数。嵌入RichFaces组件到现有项目，而这个项目有自己的样式时，就需要它。
 
要获得到有关可能的特殊参数的更多详情，见章节（？），在那里每个组件都有描述它相应元素的皮肤参数。
 
5.11.5 创建和使用你自己的皮肤文件
 
要创建你自己的皮肤文件，步骤如下：
 
          创建一个文件，并在它里面定义样式类使用的皮肤常量（见章节，“在RichFaces中的皮肤参数表”）。皮肤文件的名字应该对应于格式：<name>.skin.properties。作为这个文件的例子，你可以参看RichFaces的预定义皮肤参数（皮肤）：blueSky，classic，deepMarine等等。这些文件位于/META-INF/skins文件夹下的richfaces-impl-xxxxx.jar内。
          在你的应用程序的web.xml中，添加一个皮肤定义<contex-param>。如下所示：
...
<context-param>
     <param-name>org.richfaces.SKIN</param-name>
     <param-value>name</param-value>
</context-param>
...
         放置<name>.skin.properties文件在类路径内：META-INF/skins/ ，或者类路径文件夹（例如，WEB-INF/classes）。


5.11.6 在RichFaces中的内置换肤
 
RichFaces给了一个机会，合并换肤到UI设计中。利用这个框架，你可以轻松地在属性文件中使用命名参数，控制始终如一地应用到整个组件集的皮肤的外观。有关预定义的皮肤，请查看：http://livedemo.exadel.com/richfaces-demo/。
 
要了解更多有关换肤的可能性，请按照下列步骤：
 
          创建一个定制render-kit（渲染工具包），并在faces-config.xml中注册它，如下所示：
 
<render-kit>
     <render-kit-id>NEW_SKIN</render-kit-id>
<render-kit-class>org.ajax4jsf.framework.renderer.ChameleonRenderKitImpl</render-kit-class>
</render-kit>
 
          然后，你需要创建和注册renderer（渲染器），用于基于预定义观感的组件。
 
<renderer>
    <component-family>javax.faces.Command</component-family>
    <renderer-type>javax.faces.Link</renderer-type>
    <renderer-class>newskin.HtmlCommandLinkRenderer</renderer-class>
</renderer>
 
  最后，你需要放置使用了皮肤参数的属性文件到类路径的根内。对属性文件有两个要求：
  文件必须被命名为<skinName>.skin.properties，这本案中，它会被命名为newskin.skin.properties。
  这个文件的第一行应该是render.kit=<render-kit-id>，在本案中，它会被编写为render.kit=NEW_SKIN。
 
    有关定制渲染器的创建的额外信息，请查看：
http://java.sun.com/javaee/javaserverfaces/reference/docs/index.html。
 
5.11.7 在运行期改变皮肤
 
在运行期间改变皮肤是可能的。要实现它，在web.xml中定义EL表达式。例如：
 
<context-param>
    <param-name>org.richfaces.SKIN</param-name>
    <param-value>#{skinBean.skin}</param-value>
</context-param>
            
skinBean代码如下所示：
 
public class SkinBean {
    private String skin;
    public String getSkin() {
        return skin;
    }
    public void setSkin(String skin) {
        this.skin = skin;
    }
}
 
接下来，需要在配置文件中设置皮肤属性，初始化值。例如，"classic"：
 
<managed-bean>
    <managed-bean-name>skinBean</managed-bean-name>
    <managed-bean-class>SkinBean</managed-bean-class>
    <managed-bean-scope>session</managed-bean-scope>
    <managed-property>
        <property-name>skin</property-name>
        <value>classic</value>
    </managed-property>
</managed-bean>
            
对实例，你可以改变默认皮肤，默认颜色。要实现它，编辑皮肤的属性文件。下面是页面的代码例子：
 
<h:form>
     <div style="display: block; float: left">
        
   <h:selectOneRadio  value="#{skinBean.skin}"  border="0"  layout="pageDirection"  title="Changing  skin" style="font-size: 8; font-family: comic" onchange="submit()">
                <f:selectItem itemLabel="plain" itemValue="plain" />
        <f:selectItem itemLabel="emeraldTown" itemValue="emeraldTown" />
        <f:selectItem itemLabel="blueSky" itemValue="blueSky" />
        <f:selectItem itemLabel="wine" itemValue="wine" />
        <f:selectItem itemLabel="japanCherry" itemValue="japanCherry" />
        <f:selectItem itemLabel="ruby" itemValue="ruby" />
        <f:selectItem itemLabel="classic" itemValue="classic" />
        <f:selectItem itemLabel="laguna" itemValue="laguna" />
        <f:selectItem itemLabel="deepMarine" itemValue="deepMarine" />
        <f:selectItem itemLabel="blueSky Modified" itemValue="blueSkyModify" />
          </h:selectOneRadio>
     </div>
     <div style="display: block; float: left">
          <rich:panelBar height="100" width="200">
               <rich:panelBarItem label="Item 1" style="font-family: monospace; font-size: 12;">
         Changing skin in runtime
    </rich:panelBarItem>
    
    <rich:panelBarItem label="Item 2" style="font-family: monospace; font-size: 12;">
         This is a result of the modification "blueSky" skin
    </rich:panelBarItem>
          </rich:panelBar>
     </div>
</h:form>
 
结果如下：
 
图5.5 在运行期间改变皮肤
 
5.11.8 标准控件的皮肤
 
该功能被设计来统一标准的HTML元素和RichFaces组件的观感。可以依据元素名字和属性类型（在可应用的地方），应用皮肤到页面上的所有控件。这个功能也提供了一组件CSS样式，在于可以用皮肤来指派rich-*类到特殊的元素和到嵌套控件的元素的容器。
 
标准控件的皮肤功能提供2级皮肤：标准的和扩展的。级别是基于浏览器的检测。如果浏览器没有确定，使用高级的。然而，如果你希望显式地指定你希望应用的皮肤级别，你需要添加一个上下文参数到你的web.xml文件中，用org.richfaces.CONTROL_SKINNING_LEVEL作为参数名，并且值设置为basic或extended。
 
 标准级只为基本样式属性提供定制。
    标准级的皮肤适用于以下浏览器：
     Internet Explorer 6
     Internet Explorer 7 in BackCompat mode (请看
       http://msdn2.microsoft.com/en-us/library/ms533687(VS.85).aspx )
      Opera
      Safari
 
 扩展级扩展了基本级，引入更广泛的样式属性数量，并且适用于使用了富裕样式能力的控件的浏览器。
下面的浏览器支持皮肤的扩展级：
  Mozilla Firefox
  Internet Explorer 7 in Standards-compliant mode (CSS1Compat mode)
 
皮肤影响的元素有：
 input
 select
 textarea
 keygen
 isindex
 legend
 fieldset
 hr
  a (连同 a:hover, a:visited“伪”元素)
 
标准HTML控件的皮肤可以用两种方式初始化：
 
 通过添加org.richfaces.CONTROL_SKINNING参数到web.xml。Values为："enable"和"disable"。这种方式暗示皮肤样式属性通过元素名和属性类型（在可应用的地方）被用到元素。不需要附加步骤。请看下面的表，它包含了皮肤可用的元素列表。
  通过添加org.richfaces.CONTROL_SKINNING_CLASSES参数到web.xml。可能的值为："enable"和 "disable"。当启用这个选项，你可以提供一组预定义的CSS类，它可用你的HTML组件的皮肤。
 
通过设置org.richfaces.CONTROL_SKINNING_CLASSES为"enable"，提供给你可能的样式类有：
 
         嵌套在使用了rich-container类的元素内的基本元素，例如：
 
...
.rich-container select {
   //class content
}
...
         具有类的名字的元素，该类名对应于通过方案rich-<elementName>[-<elementType>]映射的基本元素的名字或类型之一。如下所示：
 
...
.rich-select {
  //class content
}
.rich-input-text {
  //class content
}
...
 
[注意：元素使用了基于"link"的类和伪类的名字，例如：rich-link，rich-link-hover， rich-link-visited]
 
另外，我们提供的预定义的rich CSS类，不仅可以作为HTML基本元素的类，而且也可作为某些复杂元素的类。
 
下面是使用它们的例子片断：
 
...
<u:selector name=".rich-box-bgcolor-header">
     <u:style name="background-color" skin="headerBackgroundColor" />
</u:selector>
<u:selector name=".rich-box-bgcolor-general">
     <u:style name="background-color" skin="generalBackgroundColor" />
</u:selector>
...
//gradient elements
...
<u:selector name=".rich-gradient-menu">
     <u:style name="background-image">
          <f:resource f:key="org.richfaces.renderkit.html.gradientimages.MenuGradientImage"/>
     </u:style>
     <u:style name="background-repeat" value="repeat-x" />
</u:selector>
<u:selector name=".rich-gradient-tab">
     <u:style name="background-image">
          <f:resource f:key="org.richfaces.renderkit.html.gradientimages.TabGradientImage"/>
     </u:style>
     <u:style name="background-repeat" value="repeat-x" />
</u:selector>
...
 
                     要获得标准组件皮肤的更好的主意，我们建议研究位于RichFaces svn的ui/core/src/main/resources/org/richfaces/文件夹中的CSS文件。
 
5.11.8.1标准级
 
表5.5  HTML元素的皮肤，用于绑定input, select, textarea, button,keygen, isindex, legend。
CSS属性	Skin参数
font-size	generalSizeFont
font-family	generalFamilyFont
color	controlTextColor
 
表5.6 HTML元素的皮肤，用于绑定fieldset。
CSS属性	Skin参数
border-color	panelBorderColor
 
表5.7 HTML元素的皮肤，用于绑定hr。
CSS属性	Skin参数
border-color	panelBorderColor
 
表5.8 HTML元素的皮肤，用于绑定a。
CSS属性	Skin参数
color	generalLinkColor
 
表5.9 HTML元素的皮肤，用于绑定a:hover。
CSS属性	Skin参数
color	hoverLinkColorgeneralLinkColor
 
表5.10 HTML元素的皮肤，用于绑定a:visited。
CSS属性	Skin参数
color	visitedLinkColor
 
表5.11  HTML元素的皮肤，用于绑定.rich-input, .rich-select, .rich-
textarea, .rich-keygen, .rich-isindex, .rich-link。
CSS属性	Skin参数
font-size	generalSizeFont
font-family	generalFamilyFont
color	controlTextColor
 
表5.12 HTML元素的皮肤，用于绑定.rich-fieldset。
CSS属性	Skin参数
border-color	panelBorderColor
 
表5.13  HTML元素的皮肤，用于绑定.rich-hr。
CSS属性	Skin参数/值
border-color	panelBorderColor
border-width	1px
border-style	solid
 
表5.14 HTML元素的皮肤，用于绑定.rich-link。
CSS属性	Skin参数
color	generalLinkColor
 
表5.15 HTML元素的皮肤，用于绑定.rich-link:hover。
CSS属性	Skin参数
color	hoverLinkColor
表5.16 HTML元素的皮肤，用于绑定.rich-link:visited。
CSS属性	Skin参数
color	visitedLinkColor
 
表5.17 HTML元素的皮肤，用于绑定.rich-field。
CSS属性	Skin参数/值
border-width	1px
border-style	inset
border-color	panelBorderColor
background-color	controlBackgroundColor
background-repeat	no-repeat
background-position	1px 1px
 
表5.18 HTML元素的皮肤，用于绑定.rich-field-edit。
CSS属性	Skin参数/值
border-width	1px
border-style	inset
border-color	panelBorderColor
background-color	editBackgroundColor
 
表5.19 HTML元素的皮肤，用于绑定.rich-field-error。
CSS属性	Skin参数/值
border-width	1px
border-style	inset
border-color	panelBorderColor
background-color	warningBackgroundColor
background-repeat	no-repeat
background-position	center left
padding-left	7px
 
表5.20 HTML元素的皮肤，用于绑定.rich-button, .rich-button-disabled, .rich-button-over。
CSS属性	Skin参数/值
border-width	1px
border-style	solid
border-color	panelBorderColor
background-color	trimColor
padding	2px 10px 2px 10px
text-align	center
cursor	pointer
background-repeat	repeat-x
background-position	top left
 
表5.21 HTML元素的皮肤，用于绑定.rich-button-press。
background-position	top left
 
表5.22 HTML元素的皮肤，用于绑定.rich-container fieldset, .rich-fieldset。
CSS属性	Skin参数/值
border-width	1px
border-style	solid
border-color	panelBorderColor
padding	10px
padding	10px
 
表5.23 HTML元素的皮肤，用于绑定.rich-legend。
CSS属性	Skin参数/值
font-size	generalSizeFont
font-family	generalFamilyFont
color	controlTextColor
font-weight	bold
 
表5.20 HTML元素的皮肤，用于绑定.rich-button, .rich-button-disabled, .rich-button-over。
CSS属性	Skin参数/值
padding	0px
margin	0px
 
 
 
5.11.8.2扩展级
 
表5.25 HTML元素的皮肤，用于绑定input, select, textarea, button,keygen, isindex
CSSproperties	Skinparameters/Value
border-width	1px
border-color	panelBorderColor
color	controlTextColor
 
表5.26 HTML元素的皮肤，用于绑定*|button
CSSproperties	Skinparameters
border-color	panelBorderColor
font-size	generalSizeFont
font-family	generalFamilyFont
color	headerTextColor
background-color	headerBackgroundColor
background-image	org.richfaces.renderkit.html.images.ButtonBackgroundImage
 
表5.27 HTML元素的皮肤，用于绑定button[type=button], button[type=reset], button[type=submit],input[type=reset], input[type=submit], input[type=button
CSSproperties	Skinparameters
border-color	panelBorderColor
font-size	generalSizeFont
font-family	generalFamilyFont
color	headerTextColor
background-color	headerBackgroundColor
background-image	org.richfaces.renderkit.html.images.ButtonBackgroundImage
 
表5.28 HTML元素的皮肤，用于绑定*|button[disabled], .rich-container *|button[disabled], .rich-button-disabled
CSSproperties	Skinparameters
color	tabDisabledTextColor
background-color	tableFooterBackgroundColor
border-color	tableFooterBackgroundColor
background-image	org.richfaces.renderkit.html.images.ButtonDisabledBackgroundImage
 
表5.29 HTML元素的皮肤，用于绑定.rich-button-disabled, .rich-container button[type="button"][disabled], .rich-button-button-disabled, .rich-container  button[type="reset"][disabled], .rich-button-reset-disabled, .rich-container  button[type="submit"][disabled], .rich-button-submit-disabled, .rich-container  input[type="reset"][disabled], .rich-input-reset-disabled, .rich-container  input[type="submit"][disabled], .rich-input-submit-disabled, .rich-container  input[type="button"][disabled], .rich-input-button-disabled
CSSproperties	Skinparameters
color	tabDisabledTextColor
background-color	tableFooterBackgroundColor
border-color	tableFooterBackgroundColor
background-image	org.richfaces.renderkit.html.images.ButtonDisabledBackgroundImage
 
 
           表5.30 HTML元素的皮肤，用于绑定*button[type="button"][disabled],    button[type="reset"][disabled], button[type="submit"][disabled], input[type="reset"][disabled], input[type="submit"][disabled],input[type="button"][disabled]
CSSproperties	Skinparameters
color	tabDisabledTextColor
border-color	tableFooterBackgroundColor
background-color	tableFooterBackgroundColor
 
表5.31 HTML元素的皮肤，用于绑定*|textarea
CSSproperties	Skinparameters
border-color	panelBorderColor
font-size	generalSizeFont
font-family	generalFamilyFont
color	controlTextColor
background-color	controlBackgroundColor
background-image	org.richfaces.renderkit.html.images.InputBackgroundImage
 
表5.32 HTML元素的皮肤，用于绑定textarea[type=textarea],input[type=text], input[type=password], select
CSSproperties	Skinparameters
border-color	panelBorderColor
font-size	generalSizeFont
font-family	generalFamilyFont
color	controlTextColor
background-color	controlBackgroundColor
background-image	org.richfaces.renderkit.html.images.InputBackgroundImage
 
表5.33 HTML元素的皮肤，用于绑定*|textarea[disabled], .rich-container *|textarea[disabled]
CSSproperties	Skinparameters
color	tableBorderColor
 
表5.34 textarea[type="textarea"][disabled], input[type="text"][disabled], input[type="password"][disabled]
CSSproperties	Skinparameters
color	tableBorderColor
 
表5.35 textarea[type="textarea"][disabled], input[type="text"][disabled], input[type="password"][disabled]
CSSproperties	Skinparameters
color	tableBorderColor
 
[注意：如果ajaxPortlet的配置象下面这样，标准皮肤级可能失败：
 
...
<portlet>
   <portlet-name>ajaxPortlet</portlet-name>
   <header-content>
       <script  src="/faces/rfRes/org/ajax4jsf/framework.pack.js"  type="text/javascript" />
      <script src="/faces/rfRes/org/richfaces/ui.pack.js" type="text/javascript" />
       <link  rel="stylesheet"  type="text/css"  href="/faces/rfRes/org/richfaces/skin.xcss" />
   </header-content>
</portlet>
...
 
注意，直到JSR-301[http://jcp.org/en/jsr/detail?id=301]为UIViewRoot组件定义相同的功能，是不推荐使用<a4j:portlet>组件。因而，它是由托管的<f:view>组件隐式定义。
 
]
 
5.11.9 用于扩展皮肤支持的客户边脚本
 
象在指南中早期提及它的一样，HTML的扩展皮肤是自动应用的：浏览器侦测，并且如果一个浏览器不完全支持扩展皮肤功能，则只应用基本皮肤。
 
然而，如果你不希望RichFaces组件和HTML控件自动使用皮肤，并执行你自己的换肤实现，你可能会遭遇一个问题。在浏览器，比如Opera和 Safari中，命名的标准HTML控件会受到标准控件皮肤的影响。（在本节中，你可以获得有关禁用换肤的详细内容。）
 
总之，禁用RichFaces的换肤机制，你需要在web.xml 中将"org.richfaces.LoadStyleStrategy"参数设置为"NONE"。
 
...
<context-param>
    <param-name>org.richfaces.LoadStyleStrategy</param-name>
    <param-value>NONE</param-value>
</context-param>
...
 
此外，你应该包含样式表，它执行RichFaces组件和标准HTML控件的皮肤。
 
要解决在Opera和Safari中的使用扩展皮肤的问题，添加一个客户端脚本（skinning.js）到RichFaces库中。这个脚本侦测浏览器的类型，并且启用只用于那些完全支持扩展皮肤的浏览器的扩展皮肤。
 
通过插入JavaScript代码到该页面，可以激活此脚本：
 
<script type="text/javascript">
    window.RICH_FACES_EXTENDED_SKINNING_ON = true;
</script>
 
当没有使用脚本加载策略，而且扩展皮肤被打开时，那么相应的警告消息会显示在控制台。
你也需要在<link>标签中指定"media"属性，它包含了使用了"rich-extended-skinning"的"extended_both.xcss"样式表。
 
这就是为什么，在自动换肤实现被禁用时，你可以包含样式表到页面。
 
<link  href='/YOUR_PROJECT_NAME/a4j_3_2_2-SNAPSHOTorg/richfaces/renderkit/html/css/basic_both.xcss/DATB/eAF7sqpgb-jyGdIAFrMEaw__.jsf'  type='text/css' rel='stylesheet' class='component' />
 
<link media='rich-extended-skinning' href='/YOUR_PROJECT_NAME /a4j_3_2_2-SNAPSHOTorg/richfaces/renderkit/html/css/extended_both.xcss/DATB/eAF7sqpgb-jyGdIAFrMEaw__.jsf' type='text/css' rel='stylesheet' class='component' />
 
                                                            <link  href='/ YOUR_PROJECT_NAME /a4j_3_2_2-SNAPSHOT/org/richfaces/skin.xcss/DATB/eAF7sqpgb-jyGdIAFrMEaw__.jsf' type='text/css' rel='stylesheet' class='component' />
 
[注意：现在，需要使用a4j/versionXXX前缀，而不是a4j_versionXXX。Base64编码器更改为使用'!'而不是'.']

5.11.10      XCSS文件格式
 
XCCS文件是RichFaces组件换肤的核 心。
 
XCSS是一个XML格式的CSS，它增加了用于皮肤处理的额外功能。XCSS通 过解析包含了一个特殊组件的所有观感参数的XCSS成为一个浏览器可以认识的标准的CSS文件，扩展了皮肤的可能性。
 
XCSS文件包含了CSS属 性和皮肤参数映射。一个CSS选择器到一个皮肤参数的映射通过使用< u:selector >和< u:style> XML标签执行，它们形成映射结构。请研究下面的例子：
 
...
<u:selector name=".rich-component-name">
  <u:style name="background-color" skin="additionalBackgroundColor" />
    <u:style name="border-color" skin="tableBorderColor" />
 <u:style name="border-width" skin="tableBorderWidth" />
 <u:style name="border-style" value="solid" />
</u:selector>
...
 
在处理代码期间，上面显示的例子被解析成一个标准CSS格式。
...
.rich-component-name {
 background-color: additionalBackgroundColor; /*the value of the constant defined by your skin*/
     border-color: tableBorderColor; /*the value of the constant defined by your skin*/
     border-width: tableBorderWidth; /*the value of the constant defined by your skin*/
     border-style: solid;
}
...
 
<u:selector> 标签的"name"属性定义了CSS选择器，面<u:style>标签的"name"属性 定义什么皮肤常量被 映射成一个CSS属性。 <u:style>标 签的"value"属性也被用来指派一个值给一个CSS属 性。
 
使用了相同的皮肤属性的CSS 选 择器可以用一个逗号分隔表被设置。
...
<u:selector  name=".rich-ordering-control-disabled, .rich-ordering-control-top, .rich-ordering-control-bottom, .rich-ordering-control-up, .rich-ordering-control-down">
    <u:style name="border-color" skin="tableBorderColor" />
</u:selector>
...
 
5.11.11      即插即用（Plug-n-Skin）皮肤
 
即插即用皮肤是一种功能，它给你机会方便地创建、定制、插入一个定制皮肤在你的项目中。皮肤可以基 于预定义RichFaces皮肤的参数进行创建。
 
该功能也提供了一个选项，统一了使用标准HTML元 素的富裕控件的外观。
 
要使用即插即用皮肤功能创建你的皮肤，你可以根据下面步骤指令：
 
首先，你需要创建一个新皮肤的模板。使用Maven构建和部署工具可以进行模板的创建。有关如何配置用于RichFaces的Maven的详情，请看http://wiki.jboss.org/wiki/HowToConfigureMavenForRichFaces。你可以拷贝和粘贴这些指令到命令行，并执行它们。
 
...
mvn  archetype:create  -DarchetypeGroupId=org.richfaces.cdk  -DarchetypeArtifactId=maven-archetype-plug-n-skin  -DarchetypeVersion=RF-VERSION  -DartifactId=ARTIFACT-ID  -DgroupId=GROUP-ID -Dversion=VERSION
...
 
命令的主要键值：
 
 archetypeVersion指明RichFaces版本号。例如， "3.3.3-SNAPSHOT"
 artifactId 对象的制成品id
 groupId 对象的组件id
 version 你创建的项目的版本号，默认为"1.0.-SNAPSHOT"
 
在这个操作之后，使用你的"ARTIFACT-ID"的名字的一个文件夹出现。文件夹包含了一个Maven项目的模板。
 
接下来的步骤，会指导你创建皮肤本身。
 
在Maven项目的根文件夹下（包含 了一个"pom.xml"文件），你应该在命令行运行下面的命令：
 
...
mvn cdk:add-skin -Dname=SKIN-NAME -Dpackage=SKIN-PACKAGE
...
 
命令的主要键值：
 
  name 定义新皮肤的名字。
  package 皮肤的基本包。默认为项目使用的"groupId"。
 
 
命令的其他键值：
 
   baseSkin 定义基本皮肤的名字。
   createExt 如果设置为true"， 增加扩展CSS类。详情见“标准控件皮肤”。
 
执行的结果会创建下面的文件和文件夹：
 
 BaseImage.java —— 存储图象的基本类。位置： "\src\main\java\SKIN-PACKAGE\SKIN-NAME\images\"
  BaseImageTest.java —— 存储图象的基本类的测试版。位置： "\src\test\java\SKIN-PACKAGE\SKIN-NAME\images\"
        XCSS files —— XCSS文件定义由新皮肤影响 的RichFaces组件的外观。位置： "\src\main\resources\SKIN-PACKAGE\SKIN-NAME\css\"
         SKIN-NAME.properties —— 包含新皮肤属性的文件。位置： "\src\main\resources\SKIN-PACKAGE\SKIN-NAME\css\"
 
下面的属性被用来配置SKIN-NAME.properties文件：
 
    baseSkin —— 被用来作为基础的基本皮肤名字。你定义的皮肤外观会被新样式的属性影响。
    generalStyleSheet —— 样式表的路径 (SKIN-NAME.xcss)，它导入被新皮肤影响的组件的样式表。
  extendedStyleSheet —— 样式表的路径，它被用来统一RichFaces组件和标准HTML控件的外观。详   情见“标准控制皮肤”章节。
  gradientType —— 预定义属性，用于设置应用到新皮肤的渐变类型。可能的值为：glass, plastic, plain。 有关渐变实现的更多信息，你会在下面的章节看见。
 
   SKIN-NAME.xcss —— 一个 XCSS文件，它导入被新皮肤影 响的组件的XCSS文件。位置："src\main\resources\META-INF\skins "
   XCSS文件，如果使用"DcreateExt" 键值设置为"true"执行命令，定义样式用于标准控件的XCSS (extended_classes.xcss和extended.xcss)文件 会被创建。位置： "\src\main\resources\SKIN-PACKAGE\SKIN-NAME\css\"。
   SKIN-NAME-ext.xcss，如果使用"DcreateExt" 键值设置为"true"执行命令，导入定义了用于标准控件的样式的配置SKIN-NAME-ext.xcss 文件会被创建。位置： "src\main\resources\META-INF\skins "。
  SKIN-NAME-resources.xml —— 该文件包含上面列出的所有描述。位置： Location:"src\main\config\resources ".
 
现在你可编辑"\src\main\resources\SKIN-PACKAGE\SKIN-NAME\css\"下的XCSS文件了。使用两种方式你可 以指派新的样式到选择器（选择器列在XCSS文件中），两个都是有效的，并且取决于你选择什么方式。
 
   标准的CSS代码方法。你可以增加CSS 属性到特定的选择器，你必须记住的是选择必须在<f:verbatim> <![CDATA[ ...]]> </f:verbatim> 标签内部。例 如：
 
...
.rich-calendar-cell {
  background: #537df8;
}
...
 
  使用XCSS代码方法，与XCSS文件在RichFaces 中通常被排列 的方法相同。XCSS标签必须放置在<f:verbatim> <![CDATA[ ...]]> </f:verbatim>标签内部。
 
...
<u:selector name=".rich-calendar-cell">
<u:style name="border-bottom-color" skin="panelBorderColor"/>
 <u:style name="border-right-color" skin="panelBorderColor"/>
 <u:style name="background-color" skin="tableBackgroundColor"/>
 <u:style name="font-size" skin="generalSizeFont"/>
 <u:style name="font-family" skin="generalFamilyFont"/>
</u:selector>
...
 
执行上面的步骤和编辑XCSS文 件，你可以进行构建一个新的皮肤，并且将它插入到你的项目中。在你的皮肤项目的根目录下（包含pom.xml文件），在命令行执行下面的特定命令构建新皮肤。
 
...
mvn clean install
...
 
另外，即插即用皮肤带有大量的渐变，你可以用它来让你的应用程序外观更好看。下面的代码版断显示了 如何使用一个渐变：
 
...
<u:selector name=".rich-combobox-item-selected">
 <u:style name="border-width" value="1px" />
 <u:style name="border-style" value="solid" />
 <u:style name="border-color" skin="newBorder" />
 <u:style name="background-position" value="0% 50%" />
 <u:style name="background-image">
 <f:resource f:key="org.richfaces.renderkit.html.CustomizeableGradient">
 <f:attribute name="valign" value="middle" />
 <f:attribute name="gradientHeight" value="17px" />
 <f:attribute name="baseColor" skin="headerBackgroundColor" />
 </f:resource>
 </u:style>
</u:selector>
...
 
那么，如你所见，background-image CSS使用<f:resourcef:key="org.richfaces.renderkit.html.CustomizeableGradient">来定义，它设置渐变。而且，在SKIN-NAME.properties文件中利用gradientType属性可以指定渐变类型。gradientType属性可以设置为glass, plastic, plain之一。反回来，又可以使用baseColor, gradientColor, gradientHeight,valign属性调整渐变。它们的用法如上所示。
 
现在，你可以在你项目中使用你新建的定制皮肤，通过添加新的皮肤参数到web.xml文件中，并放置带有你的皮肤的jar包 （jar包位于你的皮肤项目的"target"文件夹中）到"\WebContent\WEB-INF\lib\"中。
 
...
<context-param>
 <param-name>org.ajax4jsf.SKIN</param-name>
<param-value>SKIN-NAME</param-value>
</context-param>
...
 
5.11.11.1 使用细节
 
本节包括即插即用皮肤实现的实际问题。假设你已阅读了本指南的如何使用即插即原型创建新皮肤一节的 内容。
 
   首先，我们需要创建一个新皮肤，只需根据上节描述的步骤就可完成。
 
下面的命令用来创建一个新皮肤的模板：
 
mvn  archetype:create  -DarchetypeGroupId=org.richfaces.cdk  -DarchetypeArtifactId=maven-archetype-plug-n-skin  -DarchetypeVersion=3.3.3-SNAPSHOT  -DartifactId=P-n-S  -DgroupId=GROUPID -Dversion=1.0.-SNAPSHOT
 
现在你可浏览"P-n-S"文件夹，查看生成什么文件和文件夹。
 
接下来，我们需要使用Maven添 加需要的文件到皮肤项目。根据下面的命令完成：
 
mvn  cdk:add-skin  -DbaseSkin=blueSky   -DcreateExt=true  -Dname=PlugnSkinDemo  -Dpackage=SKINPACKAGE
 
     正如你从前面一节记住的一样，"-DbaseSkin"键值定义什么样的RichFaces内建皮肤被用来作为它的一个基础。"-DcreateExt=true"确定 新皮肤将与XCSS文件一起，统一使用了标准HTML控 件的富裕组件的外观。
 
  所以，现在，带有所有需要的资源的文件和文件夹被创建，并且可以开始重新定义/编辑新的皮肤了。
 
     现在我们可以开始编辑富裕组件的XCSS文 件。为了了解即插即用皮肤的功能如何运行，我们会改变<rich:calendar>的某些样式属性，以及改变某些基本HTML控件来了解标准控件皮肤如何影响它 们。
 
因此，它将演示如何：
 
    重新着色当前的<rich:calendar>的日期单元的背景色，从而了解新创建的带有即插即用功能帮助的皮肤如何影响组件的样式。
   重新着色标准的HTML提 交按钮。
 
     为了编辑<rich:calendar>的样式属性，你需要打开位于"P-n-S\src\main\resources\skinpackage\plugnskindemo\css\中的"calendar.xcss"文 件。一旦，你打开了文件，请找到".rich-calendar-today"选择器，并且修改它为：background-color:#075ad1;。当前日期的背景色可以被认为重新着色了。
 
     现在，我们将了解标准HTML提 交按钮的字体样式可以如何被改变。请打开位于"P-n-S\src\main\resources\skinpackage\plugnskindemo\css\"中的"extended.xcss"文 件，并且在那些逗号分隔的选择器的花括号内放置：font-weight: bold;。那 么CSS代码看起来应该象这样：
 
button[type=&quot;button&quot;], button[type=&quot;reset&quot;], button[type=&quot;submit&quot;], input[type=&quot;reset&quot;],input[type=&quot;submit&quot;], input[type=&quot;button&quot;] { font-weight: bold;} 
 
     我们计划执行的所有改变做完了，现在你可以开始创建新的PlugnSkinDemo皮肤，并导入到你的项目中。和你在前面一节阅读的一样，通过执行mvn clean install命令，皮肤应该被构建在皮肤项目的"P-n-S"文件夹中。这个过程导致在创建的"target"文件夹中，包含一个带有编 译的新皮肤的.jar文件。在我们这个案例中，文件名为"P-n-S-1.0.-SNAPSHOT.jar"。下一步是将PlugnSkinDemo皮肤导入到项目中。
 
  为了让新皮肤导入到项目中，你需要做是：
 
         复制"P-n-S-1.0.-SNAPSHOT.jar"文件到"\WebContent\WEB-INF\lib\"
         添加新皮肤的名字到"web.xml"文件中，如下所示：
 
<context-param>
<param-name>org.ajax4jsf.SKIN</param-name>
<param-value>PlugnSkinDemo</param-value>
</context-param>
 
请不要忘记了，必须在"web.xml"文件中启用标准控件皮肤，添加以下代码到"web.xml"中来完成：
 
<context-param>
<param-name>org.richfaces.CONTROL_SKINNING</param-name>
<param-value>enable</param-value>
</context-param>
 
下面的图显示了两个操作的结果：
 
图5.6. 即插即用功能在起作用。
 

 
5.12       定制样式类的定义
 
在“参考数据”一节中，有两个使用rich-*类定义的表，用于大多数可视组件（见RichFaces组件一节）。这些类允许 借助CSS为一个特殊的组件重新定义样式。实际上，你应用使用相同的名字创建类，并在他们中定义新的属性。
 
让我们考虑<rich:modalPanel>组件，要改变面具（mask） 的背景颜色，定义.rich-mpnl-mask-div类已足够了。例如：
 
...
.rich-mpnl-mask-div{
    background-color:#fae6b0;
}
...
 
结果如下：图5.7 使 用预定义类重定义样式
 
如果你在页面上有多个组件，重定义样式会应用到他们所有。要改变样式用于页面上的一个特殊组件，创 建你自己的样式类，并在相应的样式类属性中使用它们。如下所示，如何改变样式用于一个特殊模态面板（modal panel）的标题：
 
...
.myClass{
    font-style:italic;
}
...
 
接下来，指定myClass作为 <rich:modalPanel>的"headerClass"属性的值：
 
<rich:modalPanel ... headerClass="myClass"/>
 
结果：图5.8 使 用自己的类重定义样式
 
5.13       状态管理器 API
 
JSF有一个高级的导航机制，它准许你定义从视图到视图的导航。导航发生在一个网页应用程序中，当一个用户 试图通过点击一个按钮、链接或其他的命令组件，从一个页面切换到另外的页面时。但是，在某些视图的某些逻辑状态之间，没有切换机制。例如，在登录或注册（Login/Register）对话中，一个存在的用户使用它的名字和密码签约，但是，如果一个新用户注册，当用户点击"To register"链接时，一个附加的"Confirm"字段显现，按钮标签和方法被改变：
 
图：5.9登录对话

图：5.10注册对话
 
RichFaces状态API允许轻松地为页面定义某些状 态集，以及为这些状态的任何属性。
 
实际上，状态一个映射，它的条目的键是状态的名字，并且值是一个状态映射。特殊的状态映射拥有条 目，条目用一些名字作为键，并且用任何对象作为值，它在状态活动之后使用。因此，你在状态映射中，你可以定义任何值、方法绑定，或一些简单的状态变量（学 量），它拥有用于每个状态的不同的值。
 
图5.11 RichFaces状态API
 
RichFaces状态API最方便的功能之一是在状态之 间导航。RichFaces状态API实现状态改变和标准的JSF导航一样。动作组件只返回结果，而RichFaces状态API用于JSF导航处理器，检查是否这个结 果被注册为一个状态改变结果。如果状态改变结果被发现，相应的状态被激活。否则，调用标准的导航处理。
 
为了使用RichFaces状态API，你应该跟随下面的步骤：
 
       在faces-config.xml中， 注册状态管理EL解析器和导航处理器：
 
...
<application>
     <navigation-handler>org.richfaces.ui.application.StateNavigationHandler</navigation-handler>
    <el-resolver>org.richfaces.el.StateELResolver</el-resolver>
</application>
...
 
      在faces-config.xml中， 注册附加的应用程序工厂：
 
...
<factory>
     <application-factory>org.richfaces.ui.application.StateApplicationFactory</application-factory>
</factory>
...
 
     在faces-config.xml中， 注册两个管理的bean:
 
...
<managed-bean>
    <managed-bean-name>state</managed-bean-name>
    <managed-bean-class>org.richfaces.ui.model.States</managed-bean-class>
    <managed-bean-scope>request</managed-bean-scope>
    <managed-property>
        <property-name>states</property-name>
        <property-class>org.richfaces.ui.model.States</property-class>
        <value>#{config.states}</value>
    </managed-property>
</managed-bean>
<managed-bean>
    <managed-bean-name>config</managed-bean-name>
    <managed-bean-class>org.richfaces.demo.stateApi.Config</managed-bean-class>
    <managed-bean-scope>none</managed-bean-scope>
</managed-bean>
...
 
一个bean（”Config”）定义，存储状态，如下所示：
 
...
public class Config {
    /**
     * @return States
     */
    public States getStates() {
        FacesContext facesContext = FacesContext.getCurrentInstance();
        States states = new States();
       
 // Registering new User State definition
        states.setCurrentState("register"); // Name of the new state
 
        // Text labels, properties and Labels for controls in "register" state
        states.put("showConfirm", Boolean.TRUE); // confirm field rendering
        states.put("link", "(To login)"); // Switch State link label
        states.put("okBtn", "Register"); // Login/Register button label
        states.put("stateTitle", "Register New User"); // Panel title
 
        ExpressionFactory expressionFactory = facesContext.getApplication().getExpressionFactory();
 
        // Define "registerbean" available under "bean" EL binding on the page
        ValueExpression beanExpression = expressionFactory.createValueExpression(facesContext.getELContext(),"#{registerbean}", Bean.class);
 
        states.put("bean", beanExpression);
        // Define "registeraction" available under "action" EL binding on the page
        beanExpression = expressionFactory.createValueExpression(facesContext.getELContext(), "#{registeraction}", RegisterAction.class);
        states.put("action", beanExpression);
 
        // Define method expression inside registeraction binding for this state
        MethodExpression methodExpression = expressionFactory.createMethodExpression(
                facesContext.getELContext(), "#{registeraction.ok}",                String.class, new Class[] {});
        states.put("ok", methodExpression);
 
        // Outcome for switching to login state definition
        states.setNavigation("switch", "login");
        // Login Existent User State analogous definition
        states.setCurrentState("login");
        states.put("showConfirm", Boolean.FALSE);
        states.put("link", "(To register)");
        states.put("okBtn", "Login");
        states.put("stateTitle", "Login Existing User");
        beanExpression = expressionFactory.createValueExpression(facesContext.getELContext(), "#{loginbean}", Bean.class);
        states.put("bean", beanExpression);
        beanExpression = expressionFactory.createValueExpression(facesContext.getELContext(), "#{loginaction}", LoginAction.class);
        states.put("action", beanExpression);
        methodExpression = expressionFactory.createMethodExpression(
                facesContext.getELContext(), "#{loginaction.ok}", String.class, new Class[] {});
        states.put("ok", methodExpression);
        states.setNavigation("switch", "register");
        return states;
    }
}
...
 
另外一个bean(“state”)，使用了org.richfaces.ui.model.States类型，拥有"states"管理属性，它被绑定到定义状态的"config"bean。
 
       在页面上使用绑定状态，如下所示：
 
...
<h:panelGrid columns="3">
    <h:outputText value="username" />
    <h:inputText value="#{state.bean.name}" id="name" required="true" />
    <h:outputText value="password" />
    <h:inputSecret value="#{state.bean.password}" id="password" required="true" />
    <h:outputText value="confirm" rendered="#{state.showConfirm}" />
  
   <h:inputSecret  value="#{state.bean.confirmPassword}"  rendered="#{state.showConfirm}"  id="confirm"  required="true"  />
</h:panelGrid>
<a4j:commandButton  actionListener="#{state.action.listener}"  action="#{state.ok}"  value="#{state.okBtn}"  id="action"/>
...
 
要获得完整的Login/Register对话例子，请看RichFaces Live Demo [http://livedemo.exadel.com/richfaces-demo/richfaces/stateAPI.jsf?c=stateAPI]。
 
5.14       识别用户角色
 
RichFaces提供了一个函数，用于检查是否登录用户属于某种用户角色。 rich:isUserInRole(Object)函数，它使用一个字符串，一个逗号分隔的列表字符串，集合等等。以一个参数返回一个布尔值。
 
例如，你需要只为管理员渲染某些控件。要做这个，你需要在web.xml中创建一个"admin"角色，并实现授权，指派"admin"角色给以管理员身份登录的用户。 之后，你可以利用任何组件的"rendered属性使用rich:isUserInRole(Object) 函数。例子：
 
...
<rich:editor value="#{bean.text}"  rendered="#{rich:isUserInRole('admin')}" />
...
 
在上面例子中，只有角色为"admin"的登录用户可以看见文本编辑器，而对其他角色的用户，组件不会显示。



6   RichFaces组件
 
   本库包括在Rich Faces CDK基础上构建的现存组件。
 
6.1    Ajax 支持
   在本节中的组件让你轻松添加Ajax能 力到其他组件，以及管理Ajax请求。
 
6.1.1     < a4j:ajaxListener >，从3.0.0版开始可用
 
6.1.1.1    描述
 
      <a4j:ajaxListener>组件添加一个动作侦听器到一个父组件，并且象<f:actionListener>或者 <f:valueChangeListener> JSF组件一样工作，但是用于整个Ajax容 器。
 
6.1.1.2    使用细节
 
     <a4j:ajaxListener>组件添加一个动作侦听器到一个父组件。这个侦听器会被在“渲染响应（Render Response）”JSF阶段的每个Ajax请求调用。与标准的JSF<f:actionListener>和<f:valueChangeListener>组件对照，在“更新模型（Update Model）”验证失败的情况时，<a4j:ajaxListener>的调用没有被跳过。<a4j:ajaxListener>保证会被每个Ajax响 应调用。
 
    "type" 属性定义侦听器的完全限定Java类 名 。这个类应该实现org.ajax4jsf.event.AjaxListener  [../../apidoc_framework/index.htmlorg/ajax4jsf/event/AjaxListener.html]接口，它是用于所有侦听器的基本接口，能够接收AJAX事件。在事件初始化时产生的对象，可以使用java.util.EventObject.getSource() [http://java.sun.com/j2se/1.4.2/docs/api/java/util/EventObject.html]方法访问。
 
     当RichFaces运行在“Ajax请求生成非Ajax响 应”模式时， <a4j:ajaxListener>不会被 非Ajax请求调用，所以， <a4j:ajaxListener>是一个很好的Ajax响 应会被处理的指示器。让我们看看下面的例子：
 
例子：
...
<rich:messages/>
<h:form id="form">
<a4j:commandLink value="Click to send Ajax request">
 <a4j:ajaxListener type="org.docs.richfaces.actionListenerBean"/>
</a4j:commandLink>
</h:form>
...
 
例子：
...
public class ActionListenerBean implements org.ajax4jsf.event.AjaxListener {
public void processAjax(AjaxEvent event) {
     FacesContext.getCurrentInstance().addMessage("form", new FacesMessage("Ajax request is sent"));
   }
}        
...
 
结果：

图6.1 <a4j:ajaxListener>的用法。
 
6.1.1.3    参考数据
 
<a4j:ajaxListener>的属性表[../../tlddoc/index.htmla4j/ajaxListener.html]
 
表6.1 组件有关联的参数
名字	值
listener-class	org.ajax4jsf.event.AjaxListener
event-class	org.ajax4jsf.event.AjaxEvent
tag-class	org.ajax4jsf.taglib.html.jsp.AjaxListenerTag
 
6.1.1.4    相关资源链接
 
    组件的用法和它们的资源，请浏览在RichFaces Livedemo的AjaxListener页面[http://livedemo.exadel.com/richfaces-demo/richfaces/ajaxListener.jsf?tab=usage&cid=25043]。
 
    有关<f:valueChangeListener>标签的详情，请查看Sun JSF TLD文档[http://java.sun.com/javaee/javaserverfaces/1.1_01/docs/tlddocs/f/valueChangeListener.html]
 
6.1.2     < a4j:actionparam >，从3.0.0版开始可用
 
6.1.2.1    描述
 
    <a4j:actionparam>组件组合了<f:param>和<f:actionListener>的功能，准许使用"assignTo"属性直接指派值给管理的bean的属性。
 
6.1.2.2    使用细节
<a4j:actionparam>组件有三个主要属性：
 
  "name"  ——定义该参数的名字
 "value"  ——定义该参数的初始化值或一个值绑定。
  "assignTo"   ——定义可更新的bean的 属性。 如果父命令组件执行了一个actionEvent，该属性会 
被更新。与actionEvent被处理一样，更新发生在相同的阶段
（INVOKE_APPLICATION,  PROCESS_VALIDATIONS, 或 APPLY_REQUEST_VALUES, 取决于"immediate"和
"bypassUpdates"属性的值)。
 
例子：
...
<h:form id="form">
<a4j:commandButton value="Set Name to Alex" reRender="rep">
<a4j:actionparam name="username" value="Alex" assignTo="#{actionparamBean.name}"/>
 </a4j:commandButton>
 <br/>
 <h:outputText id="rep" value="Name: #{actionparamBean.name}"/>
</h:form>
...
 
管理的bean:
...
public class ActionparamBean {
 private String name = "John";
public String getName() {
return name;
 }
public void setName(String name) {
this.name = name;
}
}
...
 
     你不仅可以与Ajax 组 件一起使用<a4j:actionparam>，也可以与非Ajax组 件一起使用。这个功能允许更新模型，即使没有调用在服务器边的单行代码。这个功能的用法，你可以查看RichFaces LiveDemo的ActionParameter Usage页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/actionparam.jsf?c=actionparam&tab=usage]
 
  如果你需要在"更新模 型（Update Model）"阶段之前转换值，你可以使用"converter"属性指定转换器。
 
     [注意：在"更新模型（Update Model）"阶段使用了一个参数值指派给属 性。因此，如果表单的验证失败，这个阶段被跳过，并且属性不会被更新。]
 
    在"value"属性中是可以使用JavaScript表达式或函数。在这个案例中， "noEscape"属性应该被设置为"true"。 该JavaScript调用的结果是 用<a4j:actionparam>作为一个值发送到服务器。
 
6.1.2.3    参考数据
 
<a4j:actionparam>属性表 [../../tlddoc/index.htmla4j/actionparam.html]。
 
表6.2组件有关联的参数
名字	值
component-type 	org.ajax4jsf.ActionParameter
component-class	org.ajax4jsf.component.html.HtmlActionParameter
 
6.1.2.4    相关资源链接
 
    组件的用法和它们的资源，请浏览在RichFaces Livedemo的ActionParameter页 面： [http://livedemo.exadel.com/richfaces-demo/richfaces/actionparam.jsf?c=actionparam]。
 
    详情见Ajax4jsf  Users Forum ：
[http://www.jboss.com/index.html?module=bb&op=viewtopic&p=4063764]。
 
    有关<f:param>和 和<f:actionListener>更多信息，请看Sun JSF TLD文档：[http://java.sun.com/javaee/javaserverfaces/1.2/docs/tlddocs/index.html]。
 
6.1.3     < a4j:form >，从3.0.0版开始可用
 
6.1.3.1    描述
 
    <a4j:form>组件利用默认Ajax提 交的可能性，增强了标准JSF  <h:form>组件的功能，并且修补了在表单内使用<h:commandLink>产 生的问题。
 
6.1.3.2    使用细节
 
    连同a4j:htmlCommandLink一起， <a4j:form>组件修补了<h:commandLink>组件的问题，<h:commandLink>组件不使用重新渲染它属于的整个表单，它就不能被重新渲染。详情见RichFaces LiveDemo的Ajax Form Usage页 面：[http://livedemo.exadel.com/richfaces-demo/richfaces/form.jsf?c=form]
 
    <a4j:form>组件添加了额外的功能到非Ajax动 作/命令组件：当"ajaxSubmit"属性设置为"true"时，通过Ajax执行提交。
 
    如果<a4j:form>组 件运行在Ajax模式，可以使用标准的Ajax属 性，比如："reRender"，， "limitToList"，"requestDelay"等等。
 
例子：
...
<a4j:form ajaxSubmit="true" reRender="name">
 <h:panelGrid>
<h:commandButton  value="Set Local Name to John  (Ajax)" action="#{userBean.nameItJohn}" />
<h:outputText id="name" value="Name:#{userBean.name}" />
</h:panelGrid>
</a4j:form>
...
 
相应的bean：
 
...
public class UserBean {
    private String name="";
    public String nameItJohn() {
        setName("John");
        return null;
    }
    public String getName() {
        return this.name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
...
 
    在上面的例子中，ajaxSubmit="true"，所以，在这个表单上的所有标准动作组件变成为ajax可 用的（ajaxable）。"reRender"属性包含了一 个组件id，用于在一个ajax响 应之后重新渲染。
 
    [提示：如果你在表单内使用了<h:commandButton>或 <h:commandLink>，它们象<a4j:commandButton>一样工作。]
 
    [注意：如果<a4j:form>组件内包含了其他的Ajax命 令组件，你不应该使用带有ajaxSubmit="true"的<a4j:form>组 件。此外，由于安全原因，文件上传表单元素不能被转化为ajax可用的（ajaxable）。
 
6.1.3.3    参考数据
 
<a4j:form>属性表[../../tlddoc/index.htmla4j/form.html]。
 
表6.3 组件关联的参数
名字	值
component-type	org.ajax4jsf.Form
component-family	javax.faces.Form
component-class	org.ajax4jsf.component.html.AjaxForm
renderer-type	org.ajax4jsf.FormRenderer
 
6.1.3.4    相关资源链接
 
      组件的用法和它们的资源，请浏览在RichFaces Livedemo的Ajax Form页面 ：[http://livedemo.exadel.com/richfaces-demo/richfaces/form.jsf?c=form]
 
     有关该组件属性的其他信息，请阅读“Ajax属 性”一节：[http://livedemo.exadel.com/richfaces-demo/richfaces/ajaxAttributes.jsf?c=ajaxattributes] 
 
6.1.4     < a4j:region >，从3.0.0版开始可用
 
6.1.4.1    描述
 
    <a4j:region>组件指定组件树在服务器上被处理的部分。如果没有定义<a4j:region>，则整个视图功能元件作为一个区域。
 
6.1.4.2    使用细节
 
    <a4j:region>组件指定组件树在服务器上被处理的部分。处理包括在解码、转换、验证和模型更新期间的数据处理。注 意，整个表单仍然被提交，但只是进入区域（region）的部分会被处理。
 
例子：
 
<h:form>
      ...
      <a4j:region>
            <a4j:commandLink/>
      </a4j:region>
      ...
<h:form>
 
    在上面示意清单中的表单，通过调用<a4j:commandLink>的请求会被提交。但只有在<a4j:region>和 </a4j:region>标签包裹的区域会被服务器处理。如果没有定义<a4j:region>，则整个视图功能元件作为一个区域。
 
  区域可以被嵌套。服务器发现并只解码包含初始化请求组件的区域。
 
例子：
 
<h:form>
       ...
      <a4j:region>
            <a4j:commandLink value="Link 1" id="link1"/>
            <a4j:region>
                 <a4j:commandLink value="Link 2" id="link2"/>
            </a4j:region >
      </a4j:region>
      ...
<h:form>
 
外部的区域用于link1， 而内部的区域用于link2。
 
     当需要在渲染响应阶段排除在页面上的更新区域之外的所有组件时，使用"renderRegionOnly"属性。这种操作准许区域直接被传入解码，并且减少了执行时间。这种优化要小心实现，因为它不准许活 动区域之外的数据被更新。
 
例子：
 
<h:form>
       ...
      <a4j:region renderRegionOnly="true">
            <a4j:commandLink value="Link 1" id="link1"/>
      </a4j:region>
       ...
      <a4j:region renderRegionOnly="false">
            <a4j:commandLink value="Link 2" id="link2"/>
      </a4j:region>
       ...
</h:form>
 
     在上面的这个例子中，如果link1初 始化了一个请求，只有第一个区域会被更新。而当link2初始化一个请求时，刚两个区域都 会被更新。在这个案例中，对要包含到渲染响应内的组件的搜索，会在整个组件树中被执行。
 
     RichFaces准许直接基于组件树节点设置Ajax响 应渲染，不使用JSP (XHTML)代码。这相当快地加速了一个响应输出，并且 可能通过设置  <a4j:region>   "selfRendered"属性为"true"来完成。然而，这种 快速处理可能引起临时组件的丢失，它在视图上呈现，但没有进入组件树，以及会忽略下面描述的<a4j:outputPanel>的使用。
 
例子：
 
<a4j:region selfRendered ="true">
      <a4j:commandLink value="Link" id="link"/>
      <!--Some HTML content-->
</a4j:region>
 
    在这个案例中，处理更快，并且接下来没有引用页面代码。HTML代码没有被保存在组件树中，并且可能被丢失。因此，这种优化应该小心执行，并且需要使用另外的RichFaces组件（例如，<a4j:outputPanel>）。
 
    从RichFaces 3.2.0开 始， <a4j:region>组件可以与迭代组件 一起使用（例如，<rich:column>或<rich:scrollableDataTable>等等）。不用更新整个表，且不用任何另外的侦听器，就可以重新渲染一个表的一行。
 
例子：
 
<rich:column>
      <a4j:region>
            <a4j:commandLink reRender="out"/>
      </a4j:region>
</rich:column>
<rich:column>
      <h:outputText id="out">
</rich:column>
 
在多数情况下，不需要使用<a4j:region>作为视图根（ViewRoot），它是默认的。
 
6.1.4.3    参考数据
 
<a4j:region>属性表 [../../tlddoc/index.htmla4j/region.html]。
 
表6.4 组件关联的参数
名字	值
component-type	org.ajax4jsf.AjaxRegion
component-family	org.ajax4jsf.AjaxRegion
component-class	org.ajax4jsf.component.html.HtmlAjaxRegion
renderer-type	org.ajax4jsf.components.AjaxRegionRenderer
 
6.1.4.4    相关资源链接
 
    组件的用法和它们的资源，请浏览在RichFaces Livedemo的<a4j:region>演示页面 ：[http://livedemo.exadel.com/richfaces-demo/richfaces/region.jsf?c=region]
 
有用的文章和例子：
 
         在RichFaces cookbook中有关JBoss portal的“<a4j:region>和两个<h:inputTexts> ”[http://www.jboss.org/community/docs/DOC-11866]
         I.Shabalov 的个人博客：“关于UIInput的一个悲伤故事”[http://ishabalov.blogspot.com/2007/08/sad-story-about-uiinput.html]"，以及 使用<a4j:region>的帮助解决问题的“彻底的例子”： [http://livedemo.exadel.com/richfaces-local-value-demo/pages/local-value-demo.jsf] 。
6.1.5     < a4j:support >，从3.0.0版开始可用
 
6.1.5.1    描述
 
<a4j:support>组件是RichFaces库中最重要的核心组件。它利用Ajax能力丰富了现有的非Ajax JSF或RichFaces组件。所有其他的RichFaces Ajax组件是基于<a4j:support>所具有的相同原则。
 
6.1.5.2    使用细节
 
<a4j:support>组件有两个关键属性：
 
        强制"event"属性，它定义JavaScript事件，Ajax支持会被附加在上面。
        "reRender"属性，它定义JSF组件的id，在Ajax请求之后应该被渲染的。
 
如上提及的一样，<a4j:support>组件添加Ajax能力到现有的非Ajax JSF或RichFaces组件。让我们创建Ajax化的<h:selectOneMenu>，名为"Planets and Their Moons（行星和它们的卫星）" 
 
我们开始使用普通的行为描述。当页面渲染时，你只看见一个带有行星列表的选择框。当你选择一个行星时，<h:dataTable>表会显示出你所选择的行星的卫星。
 
换言之，我们需要使用嵌套了<a4j:support>组件的<h:selectOneMenu>，它连接到了onchange事件。
 
当一个Ajax响应返回时，<h:dataTable>在服务器边被渲染，并且在客户端被更新。
 
...
 
<h:form id="planetsForm">
    <h:outputLabel value="Select the planet:" for="planets" />
 
    <h:selectOneMenu id="planets" value="#{planetsMoons.currentPlanet}" valueChangeListener="#{planetsMoons.planetChanged}">
        <f:selectItems value="#{planetsMoons.planetsList}" />
        <a4j:support event="onchange" reRender="moons" />
    </h:selectOneMenu>
    <h:dataTable id="moons" value="#{planetsMoons.moonsList}" var="item">
        <h:column>
            <h:outputText value="#{item}"/>
        </h:column>
    </h:dataTable>
</h:form>
 
...
 
 
最后，我们需要一个后台bean:
 
...
public class PlanetsMoons {
    private String currentPlanet="";
    public List<SelectItem> planetsList = new ArrayList<SelectItem>();
    public List<String> moonsList = new ArrayList<String>();
    private static final String [] EARTH = {"The Moon"};
    private static final String [] MARS = {"Deimos", "Phobos"};
    private static final String [] JUPITER = {"Europa", "Gamymede", "Callisto"};
    
    public PlanetsMoons() {
        SelectItem item = new SelectItem("earth", "Earth");
        planetsList.add(item);
        item = new SelectItem("mars", "Mars");
        planetsList.add(item);
        item = new SelectItem("jupiter", "Jupiter");
        planetsList.add(item);
    }
    
    public void planetChanged(ValueChangeEvent event){
         moonsList.clear();
         String[] currentItems;
         if (((String)event.getNewValue()).equals("earth")) {
             currentItems = EARTH;
         }else if(((String)event.getNewValue()).equals("mars")){
             currentItems = MARS;
         }else{
             currentItems = JUPITER;
         }
         for (int i = 0; i < currentItems.length; i++) {
             moonsList.add(currentItems[i]);
         }       
     }
        
    //Getters and Setters
    ...   
}
 
有两个属性planetsList和moonsList。planetsList在构造器中使用行星名字被填充。在你选择行星后，planetChanged()侦听器被调用，并且moonsList使用合适的卫星的值被填充。
 
带有"onsubmit"和"oncomplete"属性帮助的<a4j:support>组件，允许在Ajax请求之前或之后分别使用JavaScript调用。实际上，指定在"oncomplete"属性中的JavaScript，无论Ajax请求是否成功完成都会被执行。
 
在Ajax响应之后，你可以轻松地为行星选择框添加确认对话，以及色彩化   <h:dataTable>。
 
...
<h:form id="planetsForm">
    <h:outputLabel value="Select the planet:" for="planets" />
 
    <h:selectOneMenu id="planets" value="#{planetsMoons.currentPlanet}" valueChangeListener="#{planetsMoons.planetChanged}">
        <f:selectItems value="#{planetsMoons.planetsList}" />
        <a4j:support event="onchange" reRender="moons"  onsubmit="if(!confirm('Are you sure to change the planet?')) {form.reset(); return false;}"  oncomplete="document.getElementById('planetsForm:moonsPanel').style.backgroundColor='#c8dcf9';" />
    </h:selectOneMenu>
    <h:dataTable id="moons" value="#{planetsMoons.moonsList}" var="item">
        <h:column>
            <h:outputText value="#{item}"/>
        </h:column>
    </h:dataTable>
</h:form>
...
 
结果如下：

图6.2 行星和它们的卫星
 
关于"process"属性的使用信息，你可以查看“决定处理什么”指南一节。
 
[提法：在页面上创建的<a4j:support>组件，如下：
 
<h:inputText value="#{bean.text}">
      <a4j:support event="onkeyup" reRender="output" action="#{bean.action}"/>
</h:inputText>
 
在HTML中被解码为：
 
<input  onkeyup="A4J.AJAX.Submit( Some request parameters )"/>
]
 
6.1.5.3    参考数据
 
<a4j:support> 属性表 [../../tlddoc/index.htmla4j/support.html]。
 
表6.5 组件关联的参数
名字	值
component-type	org.ajax4jsf.Support
component-family	org.ajax4jsf.AjaxSupport
component-class	org.ajax4jsf.component.html.HtmlAjaxSupport
renderer-type	org.ajax4jsf.components.AjaxSupportRenderer
 
6.1.5.4    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<a4j:support>演示页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/support.jsf?c=support]
 
6.1.6     < a4j:commandButton >，从3.0.0版开始可用
 
6.1.6.1    描述
 
<a4j:commandButton> 组件是非常相似于JSF <h:commandButton>，唯一的区别是Ajax表单提交由click产生，并且它允许在响应返回之后动态渲染。
 

图6.3  <a4j:commandButton>组件使用Blue Sky skin渲染。
 
6.1.6.2    使用细节
 
<a4j:commandButton> 组件的使用方法相同于JSF <h:commandButton>。区别是 在<a4j:commandButton>情况下，组件更新应该指定。
 
上面的例子生成下面的HTML代码：
 
<input  type="submit"  onclick="A4J.AJAX.Submit(request parameters);return  false;" value="Button"/>
 
点击生成的锚点，引发实用方法A4J.AJAX.Submit()，它执行Ajax请求。
 
[注意：<a4j:commandButton>已经有内置的Ajax支持，不需要添加  <a4j:support>]
 
在JavaScript代码中在"oncomplete"属性值中使用的关键字'this'，取决于  <a4j:commandButton>的位置。如果<a4j:commandButton>位于一个重新渲染区域之外，它可以象下面这样使用关键字'this'：
 
<h:form>
      <a4j:commandButton action="director.rollCamera" onclick="this.disabled=true" oncomplete="this.disabled=false" /> 
</h:form>
 
否则，如果<a4j:commandButton>被包含在一个重新渲染区域之中，当使用关键字'this'时，"oncomplete"属性在获取commandButton对象的引用时有一个问题。在这种情况下，则使用"oncomplete"属性应如下所示：
 
<h:form id="form">
      <a4j:commandButton id="cbutton" action="director.rollCamera" onclick="this.disabled=true" oncomplete="document.getElementById('form:cbutton').disabled=false" /> 
</h:form>
 
在Ajax提交和局部渲染之后，普通的JSF导航可以执行，但是导航情况必须被定义为<redirect/>，目的在于避免使用某些浏览器存在问题。
 
与任何发送Ajax请求和处理服务器响应的核心Ajax组件一样，<a4j:commandButton>拥有提供所需请求行为的所有属性（延迟、提交限制区和渲染等等）。
 
[注意：当附加一个JavaScript API函数到使用了<rich:componentControl> 帮助的<a4j:commandButton>时，不需要使用最后一个"attachTo"属性。属性使用Event.observe添加事件处理器，但是<a4j:commandButton>没有这种事件。下面的例子不会工作：
 
<a4j:commandButton value="Show Current Selection" reRender="table" action="#{dataTableScrollerBean.takeSelection}" id="button">
      <rich:componentControl attachTo="button" for="panel" event="oncomplete" operation="show" />
</a4j:commandButton>
 
这个应该正确工作：
 
<a4j:commandButton value="Show Current Selection" reRender="table" action="#{dataTableScrollerBean.takeSelection}" id="button">
      <rich:componentControl for="panel" event="oncomplete" operation="show" />
</a4j:commandButton>
]
 
关于"process"属性的使用信息，你可以查看“决定处理什么”指南一节。
 
6.1.6.3    参考数据
 
<a4j:commandButton>属性表[../../tlddoc/index.htmla4j/commandButton.html]。
 
表6.6 组件关联的参数 
名字	值
component-type	org.ajax4jsf.CommandButton
component-family	javax.faces.Command
component-class	org.ajax4jsf.component.html.HtmlAjaxCommandButton
renderer-type	org.ajax4jsf.components.AjaxCommandButtonRenderer
 
 
             6.1.6.4    相关资源链接 
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的CommandButton演示页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/commandButton.jsf?c=commandButton]
 
6.1.7     < a4j:commandLink >，从3.0.0版开始可用
 
6.1.7.1    描述
 
<a4j:commandLink>组件是非常相似于<h:commandLink>组件，唯一的区别是Ajax表单提交由click产生，并且它允许在响应返回之后动态渲染。不需要插任何支持到这个组件内，因为Ajax支持已经被内置。
 
6.1.7.2    使用细节
 
<a4j:commandLink>组件的使用方法是想同于JSF  <h:commandLink>。区别是 在<a4j:commandLink>情况下，组件更新应该指定。在本节我们会使用来自RichFaces Greeter的代码，并改变<a4j:commandButton>为  <a4j:commandLink>：
 
...
<a4j:commandLink value="Get greeting" reRender="greeting" />
...
 
因为<a4j:commandLink>已经有内置的Ajax支持，所以不需要嵌套<a4j:support>。作为我们改变的结果，我们会得到一个带有"Get greeting"连接的表单，而不是带按钮的。
 

图6.4  使用<a4j:commandLink>的RicjFaces greeter。 
 
上面的例子生成的HTML代码如下：
 
<a  href="#"  onclick="A4J.AJAX.Submit(?"request  parameters"); return  false;"><span>Get greeting</span></a>
 
如果你点击生成的锚点，实用方法A4J.AJAX.Submit()会被引发。
 
[注意：在Ajax提交和局部渲染之后，普通的JSF导航可以执行，但是导航情况必须被定义为<redirect/>，目的在于避免使用某些浏览器存在问题。]
 
与任何发送Ajax请求和处理服务器响应的核心Ajax组件一样，<a4j:commandLink>拥有提供所需请求行为的所有属性（延迟、提交限制区和渲染等等）。
 
关于"process"属性的使用信息，你可以查看“决定处理什么”指南一节。
 
6.1.7.3    参考数据
 
<a4j:commandLink>属性表 [../../tlddoc/index.htmla4j/commandLink.html]。
 
表6.7 组件关联的参数
名字	值
component-type	org.ajax4jsf.CommandLink
component-family	javax.faces.Command
component-class	org.ajax4jsf.component.html.HtmlAjaxCommandLink
renderer-type	org.ajax4jsf.components.AjaxCommandLinkRenderer
 
6.1.7.4    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的CommandLink演示页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/commandLink.jsf?c=commandLink]。
 
有用的文章：
        在JBoss portal的RichFaces cookbook中的：如何与<a4j:commandLink> "onclick"属性一起使用"window.confirm" JavaScript [http://www.jboss.org/community/docs/DOC-11850]
 
6.1.8     < a4j:jsFunction >，从3.0.0版开始可用
 
6.1.8.1    描述
 
<a4j:jsFunction>组件允许直接从JavaScript代码执行Ajax请求，调用服务器边数据，并且用JSON格式返回它，用于客户端的JavaScript调用。
 
6.1.8.2    使用细节
 
与使用Ajax请求从服务器获取数据的组件一样，<a4j:jsFunction>有所有通用的Ajax动作属性。因此，"action"和"actionListener"可以被调用，并且在引发调用函数之后重新渲染页面的某些部分。
 
当使用<a4j:jsFunction>时，可以从JavaScript初始化Ajax请求，并执行页面局部更新，或者利用Ajax响应返回的数据调用JavaScript函数。
 
...
<body onload="callScript()">
      <h:form>
             ...
          
   <a4j:jsFunction  name="callScript"  data="#{bean.someProperty1}"  reRender="someComponent"  oncomplete="myScript(data.subProperty1, data.subProperty2)">
                  <a4j:actionparam name="param_name" assignTo="#{bean.someProperty2}"/>
            </a4j:jsFunction>
            ...
      </h:form>
      ...
</body>
...
 
<a4j:jsFunction>允许使用<a4j:actionparam>或纯<f:param>，用于传递JavaScrip函数的任何数目的参数到Ajax请求。<a4j:jsFunction>相似于<a4j:commandButton>，但是它可以从JavaScript代码激活。它准许调用某些服务器边功能，并在"oncomplete"属性调用的JavaScript函数中使用返回的数据。因而，可以使用<a4j:jsFunction>代替<a4j:commandButton>。你可以放置它在任何地方，只是不要忘记使用<h:form>和 </h:form>包围它。
 
关于"process"属性的使用信息，你可以查看“决定处理什么”指南一节。
 
6.1.8.3    参考数据
 
<a4j:jsFunction>属性表 [../../tlddoc/index.htmla4j/jsFunction.html]。
 
表6.8 组件关联的参数
名字	值
component-type	org.ajax4jsf.Function
component-family	org.ajax4jsf.components.ajaxFunction
component-class	org.ajax4jsf.component.html.HtmlajaxFunction
renderer-type	org.ajax4jsf.components.ajaxFunctionRenderer
 
6.1.8.4    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的jsFunction演示页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/jsFunction.jsf?c=jsFunction]
 
有用的文章：
 
        "JsFunctionJson [http://www.jboss.org/community/docs/DOC-11856]"，RichFaces Cookbook中的文件描述了使用"a4j:jsFunction"调用jsonTest后台bean，它以JSON字符串随机生成某些数据。
 
6.1.9     < a4j:poll >，从3.0.0版开始可用
 
6.1.9.1    描述
 
<a4j:poll>组件允许定期性地发送Ajax请求到服务器，并被根据指定的时间间隔用于页面的更新。
 
6.1.9.2    使用细节
 
<a4j:poll>被用来周期性地轮询服务器数据。要使用这个组件，需要设置更新间隔。"interval"属性以毫秒在前一个响应和下一个请求之间定义一个间隔。<a4j:poll>组件产生的两个请求之间的总时间，是"interval"属性值和服务器响应时间之和。默认的"interval"属性值设置为"1000"毫秒。定义的例子，请看“使用页面标签创建组件”一节。
 
"timeout"属性以毫秒定义等待时间。在这期间，如果没有收到响应，连接会中止，并且下一个请求被发送。"timeout"属性的默认值没有设置。
 
"enabled"属性定义<a4j:poll>应该发送请求或不发送。渲染<a4j:poll>需要应用正确的"enabled"属性值。对"enabled"属性，你可以使用EL表达式指向一个bean属性。上面提及的用法，例子如下：
 
...
<a4j:region>
      <h:form>
           <a4j:poll id="poll" interval="1000" enabled="#{userBean.pollEnabled}" reRender="poll,grid"/>
      </h:form>
</a4j:region>
<h:form>
      <h:panelGrid columns="2" width="80%" id="grid">
           <h:panelGrid columns="1">
                <h:outputText value="Polling Inactive" rendered="#{not userBean.pollEnabled}" />
                <h:outputText value="Polling Active" rendered="#{userBean.pollEnabled}" />
              
   <a4j:commandButton  style="width:120px"  id="control"  value="#{userBean.pollEnabled?'Stop':'Start'}  Polling" reRender="poll, grid">
                      <a4j:actionparam  name="polling"  value="#{!userBean.pollEnabled}" assignTo="#{userBean.pollEnabled}"/>
                </a4j:commandButton>
          </h:panelGrid>
           <h:outputText  id="serverDate"  style="font-size:16px"  value="Server Date: #{userBean.date}"/>
    </h:panelGrid>
</h:form>
...
 
本例子显示在页面上的日期和时间，如何根据从服务器获取的进行更新。<a4j:poll>组件每秒发送请求到服务器。<a4j:poll>的"reRender"属性包含自己的id。因此，为使用当前的"enabled"属性的值，渲染它自身。
 
[注意：
      <a4j:poll>组件需要form包围。
      当它的limitToList被设置为"true"时，要使<a4j:poll>组件周期发送请求，传递<a4j:poll>  ID到它的reRender属性。
]
 
关于"process"属性的使用信息，你可以查看“决定处理什么”指南一节。
 
6.1.9.3    参考数据
 
<a4j:poll>属性表[../../tlddoc/index.htmla4j/poll.html]。
 
表6.9 组件关联的参数
名字	值
component-type	org.ajax4jsf.Poll
component-family	org.ajax4jsf.components.AjaxPoll
component-class	org.ajax4jsf.component.html.AjaxPoll
renderer-type	org.ajax4jsf.components.AjaxPollRenderer
 
6.1.9.4    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Poll 演示页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/poll.jsf?c=poll]
 
有用的例子和文章：
 
         在RichFaces Wiki 的一文，“使用Effects和Poll创建一个标志” [http://www.jboss.org/community/wiki/CreateABannerUsingEffectsAndPoll]"，给出了一个例子，使用<rich:effect>和<a4j:poll>组件如何创建一个图象标志。
        在RichFaces Wiki 的一文，“使用Effects和Poll创建一个HTML标志” [http://www.jboss.org/community/wiki/ CreateAHTMLBannerUsingEffectsAndPoll]， 给出了使用<rich:effect>和<a4j:poll>组件创建一个HTML 标志的创建方法的代码。
        在RichFaces用户论坛的线索，“RichFaces和幻灯片” [http://www.jboss.org/index.html?module=bb&op=viewtopic&t=125621]" ，包含了利用<a4j:poll>组件帮助制作一个幻灯片的信息和代码 
 
有关组件用法的最新问题，管理RichFaces用户论坛 [http://jboss.com/index.html?module=bb&op=viewtopic&t=103909]。
 
6.1.10 < a4j:push >，从3.0.0版开始可用
 
6.1.10.1描述
 
<a4j:push>定期对服务器执行Ajax请求，模拟“推”数据。
 
<a4j:push>和<a4j:poll>组件的主要区别是<a4j:push>让请求仅针对最小代码（不是针对JSF树），用于检查在队列中的存在的消息。如果消息存在则执行所有的请求。组件不会轮询注册的 bean，而是注册的EventListener，它根据事件接收消息。
 
6.1.10.2使用细节
 
 <a4j:push>实现了倒置Ajax技术。
 
例如，bean可以订阅Java消息服务（JMS[http://java.sun.com/products/jms/]）主题，或者可以用消息驱动bean（MDB）实现它，以便于根据存在的事件发送消息到<a4j:push>组件。在存在的事件中，某些动作发生了。
 
因此，一个使用<a4j:push>组件的工作范例相当于非同步模型，但没象<a4j:poll>组件一样使用缓冲池。下面是最简单的例子：
 
...
class MyPushEventListener implements PushEventListener {
    public void onEvent(EventObject evt) {
        System.out.println(evt.getSource());
            //Some action
    }
}    
...
 
下面是注册在bean中的EventListener代码：
 
...
public void addListener(EventListener listener) {
        synchronized (listener) {
                if (this.listener != listener) {
                    this.listener = (PushEventListener) listener;
               }
        }
}
...
 
用于这个例子的页面代码如下：
 
...
<a4j:status startText="in progress" stopText="done"/>
<a4j:form>
     <a4j:region>
           <a4j:push reRender="msg" eventProducer="#{pushBean.addListener}" interval="2000"/>
     </a4j:region>
     <a4j:outputPanel id="msg">
          <h:outputText value="#{pushBean.date}">
               <f:convertDateTime type="time"/>
          </h:outputText>
     </a4j:outputPanel>
     <a4j:commandButton value="Push!!" action="#{pushBean.push}" ajaxSingle="true"/>
</a4j:form>
...
 
上面的例子，显示了如何根据从服务器获得的数据更新在页面上的日期。在这个例子中，  "interval"属性值设置为"2000"。这个属性以毫秒在前一个响应和下一个请求之间定义一个间隔。默认值为"1000"毫秒。它的值可以设置为0。在这种情况下，连接是永久性的。
 
"timeout"属性以毫秒定义等待时间。在这期间，如果没有收到响应，连接会中止，并且下一个请求被发送。"timeout"属性的默认值没有设置。"interval" 和  "timeout"属性的使用给了一个机会，设置队列状态为短期轮询或是长期连接。 
 
[注意， <a4j:push>组件需要用form包围。] 
 
6.1.10.3参考数据
 
<a4j:push>属性表 [../../tlddoc/index.htmla4j/push.html]。
 
表6.10 组件关联的参数
名字	值
component-type	org.ajax4jsf.Push
component-family	org.ajax4jsf.components.AjaxPush
component-class	org.ajax4jsf.component.html.AjaxPush
renderer-type	org.ajax4jsf.components.AjaxPushRenderer
 
6.1.10.4相关资源链接
 
有<a4j:push>组件的一些额外的用法，你可以查看RichFaces LiveDemo页面[http://livedemo.exadel.com/richfaces-demo/richfaces/push.jsf?c=push]。
 
查看现实世界的<a4j:push>组件的使用，请参考“使用<a4j:push>的简单IRC小部件”一文，[http://www.jboss.org/community/wiki/SimpleIRCWidgetwitha4jpush]。
 
6.1.11 < a4j:queue >，从3.0.0版开始可用
 
6.1.11.1描述
 
<a4j:queue>组件排队一组从客户端发送的Ajax请求。具有内置Ajax功能的RichFaces组件可以查询队列，优化Ajax请求。
 
6.1.11.2使用细节
 
RichFaces队列有四种不同类型：全局默认，视图域默认，视图域命名和基于表单默认队列（好的一般队列原则记录在“队列原则”一节）。本章会围绕基于表单的队列。其他类型的用法是相似的。
 
要禁用或启用在页面上的<a4j:queue>组件，你可以使用"disabled"属性。
 
"requestDelay"属性定义延迟时间，用于动作组件引发的所有请求。
 
"size"属性指定可以同时存储在队列中请求数量。该属性帮助预防服务器超载。当超过大小时，也可以决定队列的行为。为此使用"sizeExceededBehavior" 。有四个可能的越界队列的行为策略：
 
        "dropNext"  删除下一个应该引发的请求。
         "dropNew"  删除进来的请求。
         "fireNext"  立即引发在队中要被引发的下一个请求。
        "fireNew"   立即引来进来的请求。
 
例子：
 
<h:form>
  
   <a4j:queue  size="2"  requestDelay="500"  sizeExceededBehavior="dropNext"  onsizeexceeded="alert('The size of the queue is exceeded')" />
    <h:inputText value="#{bean.a}">
        <a4j:support event="onkeyup" />
    </h:inputText>
    <h:inputText value="#{bean.b}">
        <a4j:support event="onblur" />
    </h:inputText>
    <h:selectBooleanCheckbox value="#{bean.check}" id="checkboxID">
        <a4j:support id="checkboxSupport" event="onchange" />
    </h:selectBooleanCheckbox>
</h:form>
 
在这个例子中，如果队列超过了2个请求，等待处理的下一个请求会被删除，并且一个说队列越界的消息会被显示（"onsizeexceeded"引发一个JavaScript函数）。
 
"ignoreDupResponses"属性，产生一个布尔值，也可用来优化你的Ajax请求。如果设置为true，如果在队列中一个相似请求已经在等待，则请求的响应处理不会发生。当前一个响应返回时，新的请求会立即被引发。
例子：
 
<h:form>
      <a4j:queue requestDelay="500" ignoreDupResponses="true" />
      <h:inputText value="#{bean.a}">
            <a4j:support event="onkeyup" />
      </h:inputText>
</h:form>
 
在这个例子中，请求粘合在一起，只有最新的一个被提交。
 
另外一个减轻服务器负荷的主要属性是"timeout"。该属性指定一个项目在发送事件被中止，并用从队列中删除之前，可以在队列中的时间量。
 
如果请求被发送，而响应在这个属性定义的时间桢中没有返回 ——请求被中止，并发送下一个。
 
例子：
 
<h:form>
      <a4j:queue timeout="1000" />
      <h:inputText value="#{bean.a}">
            <a4j:support event="onkeyup" />
      </h:inputText>
</h:form>
 
在这个案例中，如果服务器在1秒中内没有响应，则请求会被中止。
 
正如你所见，队列的实现提供了一些定制事件处理器，可以用它来调用JavaScript函数。
 
在请求完成之后，"oncomplete"被引发。在这个事件处理器中，请求对象以一个参数被传递。因此，使用request.queue可以访问队列。并且该元素是请求源，可以使用this。
 
例子：
 
<h:form>
      <a4j:queue oncomplete="alert(request.queue.getSize())" requestDelay="1000" />
      <h:inputText value="#{bean.a}">
            <a4j:support event="onkeyup" />
      </h:inputText>
      <h:selectBooleanCheckbox value="#{bean.check}">
            <a4j:support event="onchange"/>
      </h:selectBooleanCheckbox>
</h:form>
 
在这个例子中，你可以看见等待在队列的请求数量如何变化。你会获得具用在队列中请求数量的消息。
 
"onbeforedomupdate"事件处理器在客户端边上的DOM更新之前调用。
 
"onrequestqueue"事件处理器在一个新的请求被添加到队列之后调用。而"onrequestdequeue"事件处理器在一个请求从队列中被删除之后调用。
 
"onsubmit"事件处理器在一个请求被提交完成之后调用。该属性允许在发送Ajax 请求之前调用JavaScript代码。 
 
6.1.11.3参考数据
 
<a4j:queue>属性表[../../tlddoc/index.htmla4j/queue.html]。
 
表6.11 组件关联的参数
名字	值
component-family	org.ajax4jsf.Queue
component-class	org.ajax4jsf.component.html.HtmlQueue
renderer-type	org.ajax4jsf.QueueRenderer
tag-class	org.ajax4jsf.taglib.html.jsp.QueueTag
 
表6.12 JavaScript API
函数	描述
getSize()	返回当前队列的大小
getMaximumSize()	返回在"size"属性中指定的队列的最大数。
 
6.1.11.4相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Queue演示页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/queue.jsf?c=queue]
 
有用的文章：
 
RichFaces 开发指南，“队列原则”一节，描述了一般的队列原则。
 
6.1.12 < a4j:status >，从3.0.0版开始可用
 
6.1.12.1描述
 
<a4j:status>组件生成元素，用于当前Ajax请求状态的显示。有两种状态模式：Ajax请求是在处理或完成的情况下。
 
6.1.12.2使用细节
 
有两种定义Ajax请求的状态被一个组件跟踪的组件或容器的方法。
 
        在<a4j:status>组件上利用"for"属性定义。"for"属性应该指向请求被一个组件跟踪的一个Ajax 容器( <a4j:region> ) 的id。
       利用RichFaces库的任意动作组件获得的"status"属性定义。该属性应该指向<a4j:status>组件id。然后 <a4j:status>组件显示这个动作组件引发的请求的状态。
 
该组件创建两个<span>或 <div>，取决于每个状态内容的"layout" 属性，此元素之一(start)初始被隐藏。在Ajax请求开始时，元素状态被倒置，因此，第二个元素被显示，第一个元素被隐藏。在响应处理结束时，元素的显示状态回复到它的初始值。
 
例子：
 
<a4j:status startText="Started" stopText="stopped" />
 
上面的这个例子在一个页面上被解码为：
 
<span id="j_id20:status.start" style="display: none">
     Started
</span>
<span id="j_id20:status.stop">
     Stopped
</span>
 
在产成的一个Ajax响应被改变之后为：
 
<span id="j_id20:status.start">
     Started
</span>
<span id="j_id20:status.stop" style="display: none">
     Stopped
</span>
 
可以分组一个<a4j:status>元素的内容进入<div>中，而不是<span>。要使用它，只是定义"layout"属性，从"inline" (默认) 改为 "block"。
 
6.1.12.3参考数据
 
<a4j:status>属性表 [../../tlddoc/index.htmla4j/status.html]。
 
表6.13 组件关联的参数
名字	值
component-type	org.ajax4jsf.Status
component-family	javax.faces.Panel
component-class	org.ajax4jsf.component.html.HtmlAjaxStatus
renderer-type	org.ajax4jsf.components.AjaxStatusRenderer
 
表6.14 Facets
Facet名字	描述
start	重定义在请求开始时显示的内容
stop	重定义在请求结束时显示的内容
 
6.1.12.4相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Status演示页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/status.jsf?c=status]
 
在JBoss portal中有用的文章：
 
         RichFacesPleaseWaitBox  [http://wiki.jboss.org/wiki/RichFacesPleaseWaitBox]，描述了在使用<a4j:status>和<rich:modalPanel>组合处理Ajax请求时，如何显示一个“请求等待（Please Wait）”框，并阻塞输入。


6.2          资源或beans的处理
 
本节包含的组件，主要是用于加载资源（样式表、JavaScript文件和资源包），以及维持两个请求之间的bean的状态。
 
6.2.1     < a4j:loadBundle >，从3.0.0版开始可用
 
6.2.1.1    描述
 
<a4j:loadBundle>组件类似于JSF  <f:loadBundle>：它加载一个用于当前视图的区域设置的本地化资源包，并且用一个当前请求的当前请求的属性作为一个映射（map）存储属性。
 
6.2.1.2    使用细节
 
国际化和本地化是网页应用程序适应于不同的语言和文化的过程。在你开发一个英语和德语版的站点时，也可以说你是在本地化英语和德语站点。语言不是经历本地化的唯一事情 ——日期、时间、数字、地址、图形、图标、颜色、个性化标题，甚至喜爱的声音也应因国家而异。它意味着国际化应用程序可以有许多不同的信息，改变它们取决于用户的区域。
 
有几种组织本地化的方法。JSF  <h:loadBundle>在页面被渲染时，加载包到请求域，并更新在人群中所有需要的地方。在处理工作在他自己请求域中的Ajax请求时，用这种方法加载包信息不可行。RichFaces <a4j:loadBundle>组件提供的方法，丰富了使用了Ajax能力的JSF   <h:loadBundle>给定的方法：它允许在Ajax更新期间，使用特殊包条目的引用。
 
<a4j:loadBundle>的用法相当简单。假定一个简单的使用了不同语言显示“hello”的应用程序，在相应的连接被点击时，翻译（在我们案例中，本地化）切换发生，就如你在很多站点看见的一样。在我们的使用了RichFaces 的JSF应用程序中（那些感到不强大的人，应该好好看看“RichFaces入门”一节）创建了用于三种语言：英语、德语和意大利语的"Hello!"消息包。资源包是用*.properties扩展名表示的文件，它使用了键(名字) – 值对保存条目。一个条目的键对所有区域设置应该是相同的。
 

 
 图
6.5 用于多语言应用程序的带有键-值的*.propertie文件资源包。 
 
消息资源包应该被注册在你的应用程序中的Faces配置(faces-config.xml)文件中，用<application>元素中的<message-bundle>。一个资源包的名字应该被指定，不要使用语言或国家代码，不要使用.properties扩展名。支持的区域应该在<supported-locale>元素内被指定。
 
在Faces配置文件中注册资源包：
 
<application>
      <locale-config>
            <default-locale>en</default-locale>
            <supported-locale>en</supported-locale>
            <supported-locale>de</supported-locale>
            <supported-locale>it</supported-locale>
      </locale-config>
      <message-bundle>demo.message</message-bundle>
</application>
 
对本应用程序，我们将使用JSF javax.faces.component.UIViewRoot.setLocale方法，它设置需要的区域（每个链接调用相应的方法 ——当然，有其他办法来完成）。
 
带有三个设置相应区域的方法的ChangeLocale类：
 
package demo;
 import java.util.Locale;
 import javax.faces.context.FacesContext;
 public class ChangeLocale {
    public String germanAction() {
       FacesContext context = FacesContext.getCurrentInstance();
       context.getViewRoot().setLocale(Locale.GERMAN);
       return null;
    }
    public String englishAction() {
       FacesContext context = FacesContext.getCurrentInstance();
       context.getViewRoot().setLocale(Locale.ENGLISH);
       return null;
    }
    
    public String italianAction() {
        FacesContext context = FacesContext.getCurrentInstance();
        context.getViewRoot().setLocale(Locale.ITALIAN);
        return null;
     }
}
 
最后，JSP页面应该如下这样：
 
<h:form>
      <a4j:loadBundle var="msg" basename="demo.message"/>
      <h:outputText id="messageBundle" value="#{msg.greeting}"/>
    
   <a4j:commandLink  value="De"  action="#{changeLocale.germanAction}"  reRender="messageBundle"  />
    
   <a4j:commandLink  value="Eng"  action="#{changeLocale.englishAction}"  reRender="messageBundle"  />
    
   <a4j:commandLink  value="It"  action="#{changeLocale.italianAction}"  reRender="messageBundle"  />
</h:form>
 
 
我们会得到一个简单的使用了默认英语"Hello!"的结果。点击"De"、 "Eng" 和 "It"时，会显示在相应的*.properties文件中指定的消息。在一个Ajax更新期间，引用一个特殊的包条目，需要指向应该被重新渲染的组件（在本案中，利用<a4j:commandLink>   "reRender"属性的帮助来实现）。
 

 
图6.6 使用RichFaces   <a4j:loadBundle>组件为应用程序本地化。
 
6.2.1.3    参考数据
 
<a4j:loadBundle> 属性表 [../../tlddoc/index.htmla4j/loadBundle.html]。
 
表6.15 组件关联的参数
名字	值
component-type	org.ajax4jsf.Bundle
component-family	org.ajax4jsf.Bundle
component-class	org.ajax4jsf.component.html.AjaxLoadBundle
 
6.2.1.4    相关资源链接
 
有关组件的其他信息，请浏览在RichFaces Livedemo的LoadBundle页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/bundle.jsf?c=loadBundle]
 
更有用的例子和文章：
 
n         在java.sun portal的“loadBundle标签参考” [http://java.sun.com/javaee/javaserverfaces/1.1_01/docs/tlddocs/f/loadBundle.html] 
n         在java.sun portal的“利用属性文件支持资源包” [http://java.sun.com/docs/books/tutorial/i18n/resbundle/propfile.html] 
n         “J2EE 应用程序的国际化和本地化” [http://www.objectsource.com/j2eechapters/Ch19-I18N_and_L10N.htm]，解释了应用程序国际化的主要原则。
n         “一个更有用的教程”[http://www.laliluna.de/javaserver-faces-message-resource-bundle-tutorial.html]，解释使用JSF 消息资源包的页面应用程序国际化
n         “使用JSF国际化的一些特殊问题” [http://www.i-coding.de/www/en/jsf/application/locale.html]，解决方案来自i-coding.de portal。
 
6.2.2     < a4j:keepAlive >，从3.0.0版开始可用
 
6.2.2.1    描述
 
<a4j:keepAlive>组件允许在两个请求之间维持bean的状态。
 
6.2.2.2    使用细节
 
如果在配置文件中使用<managed-bean-scope>标签的帮助，声明一个请求域的管理的bean，那么这个bean实例的生命期只对当前请求是有效的。在请求结束后，任何试图对该bean实例做的引用，服务器都会抛出一个非法参数异常。要避免这类异常组件，<a4j:keepAlive>组件被用来维持整个bean对象在后续请求间的状态。
 
例子：
 
<a4j:keepAlive beanName = "#{myClass.testBean}"/>
 
"beanName"属性定义你希望重用的请求域bean的名字。注意这个属性必须指向一个合法JSF EL表达式，它解析管理的bean实例。例如，上面代码定义的类应该看起来象这样：
 
class MyClass{
    ...
    private TestBean testBean;
    // Getters and Setters for testBean.
    ...
}
 
"ajaxOnly"属性声明在非Ajax请求期间bean的值是否应该可用。如果这个属性的值设置为"true"，则请求域的bean在来自特定页面的Ajax请求期间维持相同的值。如果从这个页面发送了一个非Ajax请求，则重新创建一个普通的JSF请求域bean。
 
6.2.2.3    参考数据
 
<a4j:keepAlive> 属性表 [../../tlddoc/index.htmla4j/keepAlive.html]。
 
表6.16 组件关联的参数
名字	值
component-type	org.ajax4jsf.components.KeepAlive
component-family	org.ajax4jsf.components.AjaxKeepAlive
component-class	org.ajax4jsf.components.AjaxKeepAlive
 
6.2.2.4    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的KeepAlive演示页面 ：[http://livedemo.exadel.com/richfaces-demo/richfaces/keepAlive.jsf?c=keepAlive]
 
组件的其他用法，请查阅RichFaces用户论坛：[http://www.jboss.org/index.html module=bb&op=viewforum&f=261]
 
6.2.3     < a4j:loadScript >，从3.0.0版开始可用
 
6.2.3.1    描述
 
< a4j:loadScript >组件准许从其他的资源加载脚本，如一个jar包文件等等。
 
6.2.3.2    使用细节
 
  <a4j:loadScript>的主要属性是"src"，它定义脚本的上下文相关路径。这个属性的值不需要应用程序前缀。在路径中的前导斜线意味着网页上下文件的根，它也可以使用resource:///来访问使用了RichFaces资源框架的脚本文件。
 
例子：
 
<a4j:loadScript src="resource:///org/mycompany/assets/script/focus.js" />
 
"src"传值到应用程序的视图处理器的getResourceURL()方法，结果通过外部上下文（ExternalContext）的方法encodeResourceURL()被传递。
 
6.2.3.3    参考数据
 
<a4j:loadScript> 属性表[../../tlddoc/index.htmla4j/loadScript.html]。
 
表6.17 组件关联的参数
名字	值
component-type	org.ajax4jsf.LoadScript
component-family	org.ajax4jsf.LoadScript
component-class	org.ajax4jsf.component.html.HtmlLoadScript
renderer-type	org.ajax4jsf.LoadScriptRenderer
 
6.2.3.4    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Script演示页面 ：[http://livedemo.exadel.com/richfaces-demo/richfaces/script.jsf?c=loadScript]
 
6.2.4     < a4j:loadStyle >，从3.0.0版开始可用
 
6.2.4.1    描述
 
<a4j:loadStyle>组件是相似于使用src的标准样式标签，但它准许从其他的资源加载样式表，如一个jar包等等。它插入样式表链接到头（head）元素。
 
6.2.4.2    使用细节
 
<a4j:loadStylet>的主要属性是"src"，它定义脚本的上下文相关路径。这个属性的值不需要应用程序前缀。在路径中的前导斜线意味着网页上下文件的根，它也可以使用resource:///来访问使用了RichFaces资源框架的脚本文件。
 
例子：
 
<a4j:loadStyle src="resource:///org/mycompany/assets/css/common.css" /> 
 
 
"src"传值到应用程序的视图处理器的getResourceURL()方法，结果通过外部上下文（ExternalContext）的方法encodeResourceURL()被传递。
 
6.2.4.3    参考数据
 
<a4j:loadStyle>属性表[../../tlddoc/index.htmla4j/loadStyle.html]。
 
表6.18 组件关联的参数
名字	值
component-type	org.ajax4jsf.LoadStyle
component-family	org.ajax4jsf.LoadStyle
component-class	org.ajax4jsf.component.html.HtmlLoadStyle
renderer-type	org.ajax4jsf.LoadStyleRenderer
 
6.2.4.4    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Style页面 ：[http://livedemo.exadel.com/richfaces-demo/richfaces/style.jsf?c=loadStyle]
 
6.3          Ajax 验证器
 
RichFaces组件库提供了三个组件，用于用户输入数据的验证。这些组件利用Ajax支持增加了JSF验证能力，并且可以使用Hibernate验证器。
 
6.3.1     < rich:ajaxValidator >，从3.2.2版开始可用
 
6.3.1.1    描述
 
<rich:ajaxValidator>是一个组件，旨在为JSF输入提供内部Ajax验证。
 
6.3.1.2    关键功能
 
n         除了验证之外，跳过所有JSF处理。
n         可以使用标准和定制验证。
n         可以使用Hibernate验证。
n         基于事件触发验证。
6.3.1.3    使用细节
 
<rich:ajaxValidator>组件应该作为一个子组件被添加到一个数据应该被验证的JSF输入标签，并且触发验证的事件也应该被指定。默认时，该组件是单Ajax的，所以只有当前的字段会被验证。
 
下面的例子演示了<rich:ajaxValidator>如何添加Ajax功能到标准的JSF验证器。当输入字段失去焦点时，请求被发送，动作由设置成"onblur"的"event"属性确定。
 
例子：
...
<rich:panel>
      <f:facet name="header">
            <h:outputText value="User Info:" />
      </f:facet>
      <h:panelGrid columns="3">
            <h:outputText value="Name:" />
            <h:inputText value="#{userBean.name}" id="name" required="true">
                  <f:validateLength minimum="3" maximum="12"/>
                  <rich:ajaxValidator event="onblur"/>
            </h:inputText>
            <rich:message for="name" />
                
            <h:outputText value="Age:" />
                  <h:inputText value="#{userBean.age}" id="age" required="true">
                        <f:convertNumber integerOnly="true"/>
                        <f:validateLongRange minimum="18" maximum="99"/>
                        <rich:ajaxValidator event="onblur"/>
                  </h:inputText>
                  <rich:message for="age"/>
      </h:panelGrid>
</rich:panel>
...
 
该片断的结果为：

 
图6.7  使用<rich:ajaxValidator>的简单例子。
 
上面的例子显示了如何运用标准的JSF验证器。<rich:ajaxValidator>组件完美地与增加了Ajax用法的定制验证器一起工作。
 
可以用两种方式执行定制验证器：
 
n         可以使用在javax.faces.validator包中的JSF验证API。
n         使用Hibernate，为验证的数据指定约束。有关Hibernate验证器的参考，请查看Hibernated的文档[http://www.hibernate.org/hib_docs/validator/reference/en/html_single/]。
 
下面的例子显示了如何使用Hibernate验证器验证用户输入数据：
 
...
<rich:panel>
      <f:facet name="header">
            <h:outputText value="User Info:" />
      </f:facet>
      <h:panelGrid  columns="3">
            <h:outputText value="Name:" />
            <h:inputText value="#{validationBean.name}" id="name" required="true">
                  <rich:ajaxValidator event="onblur" />
            </h:inputText>
            <rich:message for="name" />
            
            <h:outputText value="Email:" />
                  <h:inputText value="#{validationBean.email}" id="email">
                        <rich:ajaxValidator event="onblur" />
                  </h:inputText>
                  <rich:message for="email" />
                  
                  <h:outputText value="Age:" />
                  <h:inputText value="#{validationBean.age}" id="age">
                        <rich:ajaxValidator event="onblur" />
                  </h:inputText>
                  <rich:message for="age" />
      </h:panelGrid>
</rich:panel>
...
 
下面是管理的bean的源代码：
 
package org.richfaces.demo.validation;
import org.hibernate.validator.Email;
import org.hibernate.validator.Length;
import org.hibernate.validator.Max;
import org.hibernate.validator.Min;
import org.hibernate.validator.NotEmpty;
import org.hibernate.validator.NotNull;
import org.hibernate.validator.Pattern;
public class ValidationBean {
    private String progressString="Fill the form please";
    
    @NotEmpty
    @Pattern(regex=".*[^\\s].*", message="This string contain only spaces")
    @Length(min=3,max=12)
    private String name;
    @Email
    @NotEmpty
    private String email;
    
    @NotNull
    @Min(18)
    @Max(100)
    private Integer age;
    
    public ValidationBean() {
    }
    /* Corresponding Getters and Setters */
    
}
 
默认时Hibernate验证器用10种语言（？）生成一个错误消息，虽然在验证失败时，你可以重新定义显示给用户的消息。上面的例子中，你可以添加（message="wrong email format"）到@Email注释来完成。
 
结果看起来象这样：

 
图6.8 使用Hibernate验证器的验证
 
6.3.1.4    参考数据
 
<rich:ajaxValidator> 属性表[../../tlddoc/index.htmlrich/ajaxValidator.html]。
 
表6.19 组件关联的参数
名字	值
component-type	org.richfaces.ajaxValidator
component-class	org.richfaces.component.html.HtmlajaxValidator
component-family	org.richfaces.ajaxValidator
renderer-type	org.richfaces.ajaxValidatorRenderer
tag-class	org.richfaces.taglib.ajaxValidatorTag
 
6.3.1.5    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的AjaxValidator页面 ： [http://livedemo.exadel.com/richfaces-demo/richfaces/ajaxValidator.jsf?c=ajaxValidator]
 
6.3.2     < rich:beanValidator >，从3.2.2版开始可用
 
6.3.2.1    描述
 
<rich:beanValidator>组件旨在使用Hibernate基于模型的约束提供验证。
 
6.3.2.2    主要功能
 
n         使用Hibernate约束验证。
	
6.3.2.3    使用细节
 
从3.2.2 GA版开始， RichFaces提供支持，用于使用Hibernate验证器定义的基于模型的约束。因此，可以象基于应用程序的Seam一样使用Hibernate验证器。
 
<rich:beanValidator>组件以JSF验证器相同的方式被定义。如下所示：
 
<rich:panel>
      <f:facet name="header">
            <h:outputText value="#{validationBean.progressString}" id="progress"/>
      </f:facet>
      <h:panelGrid columns="3">
            <h:outputText value="Name:" />
            <h:inputText value="#{validationBean.name}" id="name">
                  <rich:beanValidator summary="Invalid name"/>
            </h:inputText>
            <rich:message for="name" />
            <h:outputText value="Email:" />
            <h:inputText value="#{validationBean.email}" id="email">
                  <rich:beanValidator summary="Invalid email"/>
            </h:inputText>
            <rich:message for="email" />
            
            <h:outputText value="Age:" />
            <h:inputText value="#{validationBean.age}" id="age">
                  <rich:beanValidator summary="Wrong age"/>
            </h:inputText>
            <rich:message for="age" />
            <f:facet name="footer">
                   <a4j:commandButton  value="Submit"  action="#{validationBean.success}"  reRender="progress"/>
            </f:facet>
      </h:panelGrid>
</rich:panel>
 
请密切注意bean代码，它包含了使用Hibernate注释定义的约束，用于执行输入数据的验证。
 
package org.richfaces.demo.validation;
import org.hibernate.validator.Email;
import org.hibernate.validator.Length;
import org.hibernate.validator.Max;
import org.hibernate.validator.Min;
import org.hibernate.validator.NotEmpty;
import org.hibernate.validator.NotNull;
import org.hibernate.validator.Pattern;
public class ValidationBean {
    private String progressString="Fill the form please";
    
    @NotEmpty
    @Pattern(regex=".*[^\\s].*", message="This string contain only spaces")
    @Length(min=3,max=12)
    private String name;
    @Email
    @NotEmpty
    private String email;
    
    @NotNull
    @Min(18)
    @Max(100)
    private Integer age;
    
    public ValidationBean() {
    }
    /* Corresponding Getters and Setters */
    
    public void success() {
        setProgressString(getProgressString() + "(Strored successfully)");
    }
    public String getProgressString() {
        return progressString;
    }
    public void setProgressString(String progressString) {
        this.progressString = progressString;
    }
}
 
下图显示了验证失败时的结果。

 
 图6.9  <rich:beanValidator>的用法
 
正如你从例子中看见的一样，为了验证，<rich:beanValidator>应该被嵌套在一个输入JSF或RichFaces组件中。
 
组件只有一个属性，"summary"，它显示有关验证错误的验证消息。
 
6.3.2.4    参考数据
 
<rich:beanValidator>属性表[../../tlddoc/index.htmlrich/beanValidator.html]。
 
表6.20 组件关联的参数
名字	值
component-type	org.richfaces.beanValidator
component-class	org.richfaces.component.html.HtmlbeanValidator
component-family	org.richfaces.beanValidator
renderer-type	org.richfaces.beanValidatorRenderer
tag-class	org.richfaces.taglib.beanValidatorTag
6.3.2.5    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:beanValidator>页面 ：   [http://livedemo.exadel.com/richfaces-demo/richfaces/beanValidator.jsf?c=beanValidator] 
 
6.3.3     < rich:graphValidator >，从3.2.2版开始可用
 
6.3.3.1    描述
 
<rich:graphValidator>组件允许注册Hibernate验证器，用于复合输入组件。
 
6.3.3.2    主要功能
 
除了验证之外，跳过所有JSF处理。
 
6.3.3.3    使用细节
 
<rich:graphValidator> 组件的主要行为是相同于<rich:beanValidator>，它们的区别是为了利用<rich:beanValidator>组件验证某些输入数据，它应该是一个输入组件的嵌套元素，然而，<rich:graphValidator>包裹复合输入组件，并验证从它们接受的数据。
 
以下例子，演示了如何使用<rich:graphValidator>的一个模式：
 
...
<rich:graphValidator>
     <h:panelGrid columns="3">
          <h:outputText value="Name:" />
          <h:inputText value="#{validationBean.name}" id="name">
               <f:validateLength minimum="2" />
          </h:inputText>
          <rich:message for="name" />
          <h:outputText value="Email:" />
          <h:inputText value="#{validationBean.email}" id="email" />
          <rich:message for="email" />
     </h:panelGrid>
</rich:graphValidator>
...
 
验证也可以使用Hibernate验证， 与 <rich:beanValidator>使用的方式相同。
 
组件的构架也提供了一种选择，绑定组件到管理的bean，使用"value"属性来完成。该属性确保在通过重新验证bean属性更新模型之后，输入数据是有效的。
 
如下所示：
 
...
<rich:graphValidator summary="Invalid values: " value="#{dayStatistics}">
     <a4j:repeat value="#{dayStatistics.dayPasstimes}" var="pt" id="table">
          <h:outputText value="#{pt.title}" />
          <rich:inputNumberSpinner minValue="0" maxValue="24" value="#{pt.time}" id="time" />
          <rich:message for="time" />
     </a4j:repeat>
</rich:graphValidator>
...
 
因此，在下图说明了上面给定代码的功能：

 图6.10 “Games”字段没有通过验证
 
如上图所见“Games”字段没有通过验证，因为<rich:graphValidator>可以被用来执行单个输入项目的验证。
 

 图6.11 输入值的总和是不正确的。
 
上图显示在所有字段被完成之后，输入的值被验证了，并且因为总和是不正确的，所以数据没有通过验证。
 
6.3.3.4    参考数据
 
<rich:graphValidator> 属性表[../../tlddoc/index.htmlrich/graphValidator.html]
 
表6.21 组件关联的参数
名字	值
component-type	org.richfaces.graphValidator
component-class	org.richfaces.component.html.HtmlgraphValidator
component-family	org.richfaces.graphValidator
renderer-type	org.richfaces.graphValidatorRenderer
tag-class	org.richfaces.taglib.graphValidatorTag
 
6.3.3.5    相关资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的GraphValidator页面 ：[http://livedemo.exadel.com/richfaces-demo/richfaces/graphValidator.jsf?c=graphValidator]



6.4          Ajax 输出
 
在本节描述的组件利用Ajax能力动态地渲染某些内容。
 
6.4.1     < a4j:include >，从3.0.0版开始可用
 
6.4.1.1    描述
 
<a4j:include>组件被用来包含一个视图作为另外的局部，并且使用标准的JSF导航导航到那儿。
 
6.4.1.2    使用细节
    <a4j:include>组件被用来包含一个视图作为另外的局部，并且可以放置在页面代码中的任何地方。'viewID'属性被用来指向被包含的局部，并应该提供一个资源的全上下文关联路径，以便于在JSF导航情况中，被用来作为从视图到视图。通常组件运行如<ui:include>标签一样，但是在Ajax模式下具有局部页面导航的优势。
 
    [注意，当包含局部页面时，要使RichFaces <a4j:include>组件（以及Facelets <ui:include>标签）正常工作，检查被包含的页面不要产生额外的HTML <!DOCTYPE>, <html>, <body>标签。]
 
导航规则可能看起来如下例所示：
 
...
<navigation-rule>
      <from-view-id>/pages/include/first.xhtml</from-view-id>
      <navigation-case>
            <from-outcome>next</from-outcome>
            <to-view-id>/pages/include/second.xhtml</to-view-id>
      </navigation-case>
</navigation-rule>
...
 
6.4.1.3    参数数据
 
<a4j:include> 属性表[../../tlddoc/index.htmla4j/include.html]。
 
表6.22 组件关联的参数
名字	值
component-type	org.ajax4jsf.Include
component-family	javax.faces.Output
component-class	org.ajax4jsf.component.html.Include
renderer-type	org.ajax4jsf.components.AjaxIncludeRenderer
 
6.4.1.4    相关资源链接
 
    组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Include页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/include.jsf?c=include] 。
 
6.4.2     < a4j:mediaOutput >，从3.0.0版开始可用
 
6.4.2.1    描述
 
<a4j:mediaOutput>组件是一个工具，用于生成图象、视频、声音或其他你任意定义的二进制资源。
 
6.4.2.2    使用细节
 
    <a4j:mediaOutput>组件被用来生成任意的图像、视频、声音。让我们考虑图象创建，并生成一个带有数字的JPEG图象验证码（captcha）。（图象只包含数据，没有任何图形噪声和失真。）
 
在页面上编写下行：
 
<a4j:mediaOutput  element="img"  cacheable="false"  session="false"  createContent="#{mediaBean.paint}"  value="#{mediaData}"  mimeType="image/jpeg"/>
 
   如上所示，首先需要指定你希望生成的媒体类型。利用"element"属性来完成，它可取的值为：img, object, applet, script, link或a。
 
   "cacheable"属性定义是否响应会被缓存。本例中，我们不需要图象被缓存，因为我们每次刷新页面时需要改变它。
 
"mimeType"属性定义输出内容的类型。它被用来定义在HTTP响应的头中的相应类型。
 
<a4j:mediaOutput>组件有两个主要属性：
 
   "createContent"属性指定一个用于创建内容的方法。该方法接收两个参数。第一个参数，具有java.io.OutputStream类型，是输出流的一个引用。一个输出流接收输出字节，并发送到一个接收器。第二个参数是组件的"value"  属性的一个引用，并具有java.lang.Object类型。这个参数包含使用了在"value"属性中指定的数据的反序列化对象。
   "value"属性指定一个存储数据的bean类，用于传送数据到在用"createContent"指定的方法中的一个流内。
 
   现在，让我们创建一个MediaBean类，并指定一个原始的随机数生成器和一个paint方法，它会转换生成的数为一个输出流，并提供一个JPEG图象为结果。MediaBean类的代码如下所示：
 
package demo;
import java.awt.Graphics2D;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.io.OutputStream;
import java.util.Random;
import javax.imageio.ImageIO;
public class MediaBean {
    public void paint(OutputStream out, Object data) throws IOException{
        Integer high = 9999;
        Integer low = 1000;
        Random generator = new Random();
        Integer digits = generator.nextInt(high - low + 1) + low;
        if (data instanceof MediaData) {            
            MediaData paintData = (MediaData) data;
            BufferedImage img = new BufferedImage(paintData.getWidth(),paintData.getHeight(),BufferedImage. TYPE_INT_RGB);
            Graphics2D graphics2D = img.createGraphics();
            graphics2D.setBackground(paintData.getBackground());
            graphics2D.setColor(paintData.getDrawColor());
            graphics2D.clearRect(0,0,paintData.getWidth(),paintData.getHeight());
            graphics2D.setFont(paintData.getFont());
            graphics2D.drawString(digits.toString(), 20, 35);
            ImageIO.write(img,"png",out);
        }
    }
}
 
    现在，需要创建保存传送数据的bean，此数据会被用来作为内容创建方法的输入数据。MediaData类的代码如下所示：
  [注意，传送到value内的一个bean类，应该实现Serializable接口，以便于编码到URL的资源。]
 
package demo;
import java.awt.Color;
import java.awt.Font;
import java.io.Serializable;
public class MediaData implements Serializable{
    private static final long serialVersionUID = 1L;
    Integer Width=110;
    Integer Height=50;
    Color Background=new Color(190, 214, 248);
    Color DrawColor=new Color(0,0,0);
    Font font = new Font("Serif", Font.TRUETYPE_FONT, 30);
    
    /* Corresponding getters and setters */
    
}
 
作为结果，<a4j:mediaOutput>组件会生成下列图象，它会在每次页面刷新时更新：

 
图6.12 使用<a4j:mediaOutput>组件，生成验证码（captcha）图象。
 
因此，当使用该组件时，可以在一个使用了Ajax请求的页面上输出你的任何类型的数据。
 
6.4.2.3    参数数据
 
<a4j:mediaOutput> 属性表 [../../tlddoc/index.htmla4j/mediaOutput.html]。
 
表6.23 组件关联的参数
名字	值
component-type	org.ajax4jsf.MediaOutput
component-family	org.ajax4jsf.Resource
component-class	org.ajax4jsf.component.html.MediaOutput
renderer-type	org.ajax4jsf.MediaOutputRenderer
 
6.4.2.4    相关资源链接
 
   组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的MediaOutput页面 ： [http://livedemo.exadel.com/richfaces-demo/richfaces/mediaOutput.jsf?c=mediaOutput]
 
6.4.3     < a4j:outputPanel >，从3.0.0版开始可用
 
6.4.3.1    描述
 
    该组件用于在Ajax输出区的组件分组，它提供了额外的输出机会，比如，在树组件中的非显现（non-present）组件的插入，在Ajax请求之后的临时元素的保存，等等。
 
6.4.3.2    使用细节
 
     在一个组件或多个组件应该随时更新时，使用<a4j:outputPanel>组件。该组件的工作相似于"reRender"属性做的，但不是指定一个逗号分隔的组件列表包装所要更新的组件。在原始的非ajax响应期间，某些组件不被渲染时，在这种情况下，可能是有用的。例子：
 
<a4j:support reRender="mypanel"/>
...
<a4j:outputPanel id="mypanel">
      <h:panelGrid rendered="#{not empty foo.bar}">
       ...
      </h:panelGrid>
</a4j:outputPanel>
 
    默认时<a4j:outputPanel>组件作为闭合（opening and closing）的HTML <span>标签被渲染，并且运行象容器。利用"layout"属性的帮助，这种输出方式可以设置为三种变量中的任何一种：
 
         "inline" （默认）
        "block"
         "none"  
 
     如果layout="block"被设置，该组件作为一对闭合<div>标签被渲染。在这种情况下，可以应用可用的<div>的元素样式属性。layout="none"帮助避免一个不必要的标签，其包围了根据"rendered" 属性的值被渲染或不被渲染的一个内容。在这种情况下，一个内部上下文不被渲染，<a4j:outputPanel>以一个具有ID等于一个子组件ID和display:none样式的 <span>标签被渲染。如果子组件被渲染， <a4j:outputPanel>根本不会出现在最终代码中。例子：
 
<a4j:support reRender="mypanel"/>
 ...
<a4j:outputPanel layout="none">
      <h:panelGrid id="mypanel" rendered="#{not empty foo.bar}">
       ...
      </h:panelGrid>
</a4j:outputPanel>
 
    正如你所见，代码非常相似于上面的一个，但是"reRender "属性直接指向更新的panelGrid，并不指向outputPanel框架，语义上它更正确。
 
    <a4j:outputPanel>允许基于自己的标志更新一个页面的局部。标志由"ajaxRendered"属性定义。当一个页面的一部分必须被更新或根据任何响应被更新时，通常使用这个标志。例子：
 
<a4j:outputPanel ajaxRendered="true">
      <h:messages/>
</a4j:outputPanel>
 
    <a4j:outPanel>应该被用于非JSF组件部分框架，可以根据Ajax应用更新它，RichFaces指定的更新区域列表就象现有的JSF组件列表一样。
 
    在默认时，非JSF上下文没有被保存在组件树中，但每次被重新渲染。要加快处理速度和Ajax响应输入速度，RichFaces默认时保存了非JSF上下文在组件树中。这个选项可以通过"keepTransient"属性被取消，它取消为子组件强迫设置的临时标志。这个设置保存当前值的标志由子组件设置。
 
    [注意，在JSF 1.1实现或更低版中，非JSF组件应该使用<f:verbatim> 组件框起来， <a4j:outputPanel>并没有以任何方式改进这个JSF实现，所以在没有RichFaces用法时，你仍然必须在它需要的地方使用这个标志。]
 
      RichFaces允许设置基于组件树节点直接渲染，不用涉及JSP (XHTML)页面代码。可以通过在<a4j:region>上设置"selfRendered"属性为"true"定义它，并且有助于大大加快响应输出。然而，如果一个临时标志也被保存为"true"，这个快速处理可能引起在页面上显示的，且没有进入组件树的临时组件的失败。 因此，对任何特殊情况，你可以选择一个方式用于你的应用程序的优化：加速处理或用于保存早期定义的一个临时树部分的冗余内存。
 
6.4.3.3    参数数据
 
<a4j:outputPanel> 属性表[../../tlddoc/index.htmla4j/outputPanel.html]。
 
表6.24 组件关联的参数
名字	值
component-type	org.ajax4jsf.OutputPanel
component-family	javax.faces.Panel
component-type	org.ajax4jsf.ajax.OutputPanel
component-class	org.ajax4jsf.component.html.HtmlAjaxOutputPanel
renderer-type	org.ajax4jsf.components.AjaxOutputPanelRenderer
 
6.4.3.4    相关资源链接
 
    组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的OutputPanel页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/outputPanel.jsf?c=outputPanel] 
 
  有用的文章：
 
    有关组件使用的一些其他信息，请查询RichFaces用户论坛：[http://www.jboss.org/index.html?module=bb&op=viewforum&f=26]



6.5          Ajax 杂项
 
一组Ajax杂 项组件
 
6.5.1     < a4j:page >，从3.0.0版开始可用
 
6.5.1.1    描述
 
   <a4j:page>组件编码整个HTML页面结构，并解决了在早期Ajax4Jsf版中JSP与MyFaces一起使用的某些不兼容性。
 
6.5.1.2    使用细节
 
   组件解决了早期Ajax4Jsf版与MyFaces一起使用的问题：在MyFaces实现中的<f:view> JSP标签，在渲染响应阶段不能控制编码内容，因此Ajax不能控制，也不能产生响应。<a4j:page>通过包裹Ajax更新区域解决了这个问题。在最新版的框架中已成功修补了这个问题，所以不需要使用<a4j:page>组件。
 
    该组件使用facet  "head"，定义相应于HTML HEAD的内容。为了定义第一个body部分，不需要使用 "body"  facet。属性"format"定义编码DOCTYPE的页面布局格式。属性"pageTitle"作为标题部分被渲染。
 
根据上面的描述，在页面定义该组件，如下所示： 
 
<a4j:page format="xhtml" pageTitle="myPage">
      <f:facet name="head">
            <!--Head Content here-->
      </f:facet>
      <!--Page Content Here-->
</a4j:page>
 
在页面上会被渲染为：
 
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/
DTD/xhtml1-strict.dtd">
<html>
    <head> 
        <title>myPage</title>
        <!--Head Content here-->
    </head> 
    <body>
        <!--Page Content Here-->
    </body> 
</html>
 
6.5.1.3    参考数据
 
<a4j:page> 属性表[../../tlddoc/index.htmla4j/page.html]。
 
表6.25 组件关联的参数
名字	值
component-type	org.ajax4jsf.components.Page
component-family	org.ajax4jsf.components.AjaxRegion
component-class	org.ajax4jsf.component.html.HtmlPage
renderer-type	org.ajax4jsf.components.AjaxPageRenderer
 
表6.26  Facet
Facet名字	描述
head	定义head内 容
 
6.5.1.4    相关资源链接
 
    组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的AjaxPage页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/page.jsf?c=page]
 
6.5.2     < a4j:portlet >，从3.0.0版开始可用
 
6.5.2.1    描述
 
    直到JSR-301为UIViewRoot组件定义了相同的功能，是不推荐使用<a4j:portlet>组件。因此，它是由托管<f:view>组件隐式定义的。
 
6.5.2.2    使用细节
 
    该组件的主要目的是可以实现在一个页面上创建几个相同的portlet实例。但是对于每个窗口，元素的clientId应该是不同的。在这种情况下，每 个portlet都使用命名空间。  <a4j:portlet> 实现NaimingContainer接口，且添加命名空间到页面上的 所有组件。为解决前面提及的问题，所有portlet内容应该由<a4j:portlet>包裹。
 
6.5.2.3    参考数据
 
<a4j:portlet>属性表[../../tlddoc/index.htmla4j/portlet.html]。
 
表6.27 组件关联的参数
名字	值
component-type	org.ajax4jsf.Portlet
component-family	org.ajax4jsf.component.Portlet
component-class	org.ajax4jsf.component.html.HtmlPortlet
 
6.5.2.4    相关资源链接
 
    组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Portlet页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/portlet.jsf?c=portlet]
 
有用的发布：
 
    有关组件用法的其他信息，请查看Ajax4Jsf用户论坛：[http://www.jboss.com/index.html?module=bb&op=viewtopic&t=107325]
 
  portal ——显示应用程序 [http://anonsvn.jboss.org/repos/ajax4jsf/trunk/samples/portal-echo/]，portal例子，可以从JBoss SVN获取。
 
    portal环境支持的最初快照 [http://www.jboss.com/index.html?module=bb&op=viewtopic&t=107325] ， Portlet例子演示，包含用法介绍。
 
6.5.3     < a4j:htmlCommandLink >，从3.0.0版开始可用
 
6.5.3.1    描述
 
    <a4j:htmlCommandLink>组件是非常相似于JSF HTML库的相同组件，细微的差别只是在链接的产生，以及在使用原始组件时发生的问题解决。
 
6.5.3.2    使用细节
 
   与原始组件的区别是要求命令与子<f:param>元素链接的所有隐藏字段始终被渲染，并且它不依赖于在页面上的链接渲染。它解决了无效链接的问题，链 接不会立即在页面上渲染，而是在一些Ajax请求之后。例子：
 
<a4j:form>
    ...
    <a4j:htmlComandLink action="action" value="link" rendered="#{bean.rendered}">
        <f:param .../>
    <a4j:htmlComandLink>
    ...
</a4j:form>
 
    在这个例子中<a4j:htmlCommandLink>象标准的 <h:commandLink>一样工作，但是在此处，要求正确功能的隐藏字段，在一个页面开始下载之前被渲染，
，但如果它的属性没有设置为"false"，那么它不会发生。
 
6.5.3.3    参考数据
 
<a4j:htmlCommandLink>属性表[../../tlddoc/index.htmla4j/htmlCommandLink.html]。
 
表6.28 组件关联的参数
名字	值
component-type	javax.faces.HtmlCommandLink
component-family	javax.faces.Command
component-class	javax.faces.component.html.HtmlCommandLink
renderer-type	org.ajax4jsf.HtmlCommandLinkRenderer
 
6.5.3.4    相关资源链接
 
    <a4j:htmlCommandLink>组件的其他信息，你可在RichFaces LiveDemo页面[http://livedemo.exadel.com/richfaces-demo/richfaces/htmlCommandLink.jsf?c=htmlCommandLink]找到。
 
    <f:param>组件的其他信息，你可在RichFaces LiveDemo页面  [http://java.sun.com/javaee/javaserverfaces/1.1_01/docs/tlddocs/f/param.html]找到。
 
6.5.4     < a4j:log >，从3.0.0版开始可用
 
6.5.4.1    描述
 
 <a4j:log >组件生成JavaScript，它打开一个带有有用的调试信息的调试窗口。
 
6.5.4.2    使用细节
 
    <a4j:log >组件生成JavaScript，它打开一个带有有用的调试信息的日志窗口，它包含请求和响应的数据、DOM树的变化等等。日志不仅可以在一个新窗口产生，而且也能够在页面上的单独的<div>元素中产生。这个功能利用 "popup"属性来控制。按"CTRL+SHIFT+L"打开窗口，它是默认的注册键。利用"hotkey" 属性可以改变热键，它需要与"CTRL+SHIFT" 一起定义一个字母来打开一个窗口。 
 
  "level" 属性有几个可取值："FATAL", "ERROR", "WARN", "INFO", "ALL"，在改变日志级别时需要使用它们。
 
例子：
 
<a4j:log level="ALL" popup="false" width="400" height="200"/>
 
这种方式定义的该组件在一个页面上会被解码为在一个页面内的<div>，所有的信息产生在其中。
 
[注意：<a4j:log>会在执行Ajax请求之后自动更新。不要使用reRender更新<a4j:log>！]
 
6.5.4.3    参考数据
 
<a4j:log> 属性表 [../../tlddoc/index.htmla4j/log.html]。
 
表6.29 组件关联的参数
名字	值
component-type	org.ajax4jsf.Log
component-family	org.ajax4jsf.Log
component-class	org.ajax4jsf.component.html.AjaxLog
renderer-type	org.ajax4jsf.LogRenderer
 
6.5.4.4    相关资源链接
 
    组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Log页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/log.jsf?c=log]。
 
    当<a4j:log>可能引起JavaScript错误时，你可以找到一些案例，在Ajax核心组件页面 [http://www.jboss.org/community/wiki/AjaxCoreComponents]。




6.6          数据迭代
 
以下组件迭代一个集合的整个数据，并在页面上显示它们。
 
6.6.1     < rich:column >，从3.0.0版开始可用
 
6.6.1.1    描述
 
该组件是指在UIData组件中渲染行。
 

 
图6.13.   <rich:column>组件
 
6.6.1.2    主要功能
 
n         完美的皮肤表行和子元素。
n         可以利用"colspan"的帮助合并行。
n         可以利用"rowspan"和"breakBefore"的帮助合并列。
n         排序列值。
n         过滤列值。
 
[重要，"colspan"、"rowspan"和"breakBefore"属性只影响在<rich:dataTable>中的列，不影响在<rich:extendedDataTable>中的。]
 
6.6.1.3    使用细节
 
要输出简单的表，<rich:column>的用法和标准的<h:column>一样。请下面的例子：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5"> 
     <rich:column>
          <f:facet name="header">State Flag</f:facet>
          <h:graphicImage value="#{cap.stateFlag}"/>
     </rich:column>
     <rich:column>
           <f:facet name="header">State Name</f:facet>
           <h:outputText value="#{cap.state}"/>
     </rich:column>
     <rich:column >
          <f:facet name="header">State Capital</f:facet>
          <h:outputText value="#{cap.name}"/>
     </rich:column>
     <rich:column>
          <f:facet name="header">Time Zone</f:facet>
          <h:outputText value="#{cap.timeZone}"/>
     </rich:column>
</rich:dataTable>
...
 
结果为：

 
图6.14  <rich:column>组件
 
现在，为了将文字信息分组为在一个标志列中的一行中，使用"colspan"属性，它与一个HTML的相似，指定首列包含三列。另外，需要利用breakBefore="true"的帮助指定下列从首行开始。例子：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5"> 
     <rich:column colspan="3">
          <h:graphicImage value="#{cap.stateFlag}"/>
     </rich:column>
     <rich:column breakBefore="true"> 
          <h:outputText value="#{cap.state}"/>
     </rich:column>
     <rich:column >
          <h:outputText value="#{cap.name}"/>
     </rich:column>
     <rich:column>
          <h:outputText value="#{cap.timeZone}"/>
     </rich:column>
</rich:dataTable>
...
 
渲染出下面的结果：

 
图6.15  利用 "colspan"和"breakbefore"属性修改的<rich:column>
 
相同的方法可以用于列分组，只是利用"rowspan" 属性，它与一个HTML的相似，负责当前行占据的行数量的定义。在例子中，唯一要做的事情是一个指令，移动在第二列后每个下一行到下行中。例子：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5"> 
     <rich:column rowspan="3">
          <f:facet name="header">State Flag</f:facet>
          <h:graphicImage value="#{cap.stateFlag}"/>
     </rich:column>
     <rich:column> 
          <f:facet name="header">State Info</f:facet>
          <h:outputText value="#{cap.state}"/>
     </rich:column>
     <rich:column breakBefore="true">
          <h:outputText value="#{cap.name}"/>
     </rich:column>
     <rich:column breakBefore="true">
          <h:outputText value="#{cap.timeZone}"/>
     </rich:column>
</rich:dataTable>
...
 
结果为：

 
图6.16 <rich:column>，利用了"rowspan"属性。
 
对一个特殊行的标准输出，另外用<h:column>组件提供，因此，可以利用特定的HTML属性轻松地分组行。
 
利用后面章节描述的<h:columnGroup>组件的帮助，列也可以用特殊的方式分组。
 
在动态列维基文章[http://wiki.jboss.org/wiki/DynamicColumns]，你可找到有关动态列的基他信息。
 
6.6.1.4    排序和过滤
 
6.6.1.4.1   排序
 
为了排序列，你应该使用"sortBy"属性，它指明什么值被排序。这个属性只能与<rich:dataTable>组件一起使用。在"sortBy"属性中的表达式只能引用"var"属性声明的变量，对那些使用其他属性声明的，比如"rowKeyVar"属性，则不能引用。要排序列，你应该点击它的标题。如下所示：
 
...
<h:form>
    <rich:dataTable value="#{capitalsBean.capitals}" var="cap" width="300px">
        <f:facet name="header">
            <h:outputText value="Sorting Example"/>
        </f:facet>
        <rich:column sortBy="#{cap.state}">
            <f:facet name="header">
                <h:outputText value="State Name"/>
            </f:facet>
            <h:outputText value="#{cap.state}"/>
        </rich:column> 
        <rich:column sortBy="#{cap.name}">
            <f:facet name="header">
                <h:outputText value="State Capital"/>
            </f:facet>
            <h:outputText value="#{cap.name}"/> 
        </rich:column>
    </rich:dataTable>
</h:form>
...
 
结果为：

 
图6.17  使用了"sortBy"属性的<rich:column>
 
"sortExpression"属性定义了一个bean属性，它被用来排序列。这个属性只能与<rich:scrollableDataTable>组件一起使用。属性的用法如下所示：
 
...
<rich:scrollableDataTable
        value="#{dataTableScrollerBean.allCars}" sortMode="single"
        var="category">
        <rich:column sortExpression="#{category.make}">
            <f:facet name="header">
                <h:outputText styleClass="headerText" value="Make" />
            </f:facet>
            <h:outputText value="#{category.make}" />
        </rich:column>
        <rich:column>
            <f:facet name="header">
                <h:outputText styleClass="headerText" value="Model" />
            </f:facet>
            <h:outputText value="#{category.model}" />
        </rich:column>
        <rich:column>
            <f:facet name="header">
                <h:outputText styleClass="headerText" value="Price" />
            </f:facet>
            <h:outputText value="#{category.price}" />
        </rich:column>
</rich:scrollableDataTable>
...
 
"selfSorted"属性是用于添加能够通过点击标题自动排序列。默认为"true"。下面的例子，第二列是不能排序的。
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap">
        <rich:column>
                <f:facet name="header">
                        <h:outputText value="State Flag"/>
                </f:facet>
                <h:graphicImage value="#{cap.stateFlag}"/> 
        </rich:column>
        <rich:column sortBy="#{cap.state}" selfSorted="false"> 
                <f:facet name="header">
                        <h:outputText value="State Name"/>
                </f:facet>
                <h:outputText value="#{cap.state}"/>
        </rich:column> 
</rich:dataTable>
...
 
"sortOrder"属性被用来改变列的排序顺序，通过外部控制手段。
 
可取的值有：
 
n         "ASCENDING" ——用升序排序列
n         "DESCENDING" ——用升序排序列
n         "UNSORTED" ——不排序列
 
例子：
 
...
<h:form>
    <rich:dataTable value="#{capitalsBean.capitals}" var="cap" width="300px">
        <f:facet name="header">
            <h:outputText value="Sorting Example"/>
        </f:facet>
        <rich:column sortBy="#{cap.state}" sortOrder="ASCENDING">
            <f:facet name="header">
                <h:outputText value="State Name"/>
            </f:facet>
            <h:outputText value="#{cap.state}"/>
        </rich:column> 
        <rich:column sortBy="#{cap.name}" sortOrder="DESCENDING">
            <f:facet name="header">
                <h:outputText value="State Capital"/>
            </f:facet>
            <h:outputText value="#{cap.name}"/> 
        </rich:column>
    </rich:dataTable>
</h:form>
...
 
结果如下：

 
图6.18 使用"sortOrder"属性的<rich:column>
 
在上面的例子中，第一列用降序排序。但是如果重复行出现在表中时，相对的第二列用升序排序。
 
如果列值复杂，"sortOrder"属性应该指向一个包含排序顺序的 bean属性。对于<rich:columns>如何实现它，请看LiveDemo [http://livedemo.exadel.com/richfaces-demo/richfaces/columns.jsf?c=columns&tab=usage]
 
使用"rich-sort-icon"类，你也可以定制排序图标元素。
 
[注意，为了排序非英语值的列，你可以在你的web.xml 文件中添加org.richfaces.datatableUsesViewLocale上下文参数。它的值应该为"true"]
 
[注意，"sortBy"和"selfSorted"属性与<rich:dataTable>组件一起使用。"selfSorted"可以与<rich:extendedDataTable>组件一起使用。
 
"sortable"和 "sortExpression"与<rich:scrollableDataTable>组件一起使用。]
 
6.6.1.4.2   过滤
 
有两种方法过滤列值：
 
n         使用内置过滤。它利用startsWith()函数制造过滤。在这种情况下，你需要在你希望过滤的列定义"filterBy"属性。这个属性定义迭代对象的属性，在过滤处理时使用它。在"filterBy"属性中的表达式只能引用"var"属性声明的变量。对那些使用其他属性声明的，比如"rowKeyVar"属性，则不能引用。
 
"filterValue"属性被用来获得或改变当前过滤的值。在页面上可以使用初始过滤值定义它，或者作为值绑定在服务器上获得或改变它。如果  "filterValue"属性非空，在首次渲染时，从一开始表就会被过滤。
 
你可以使用"rich-filter-input" CSS类定制输入表单。
 
为了改变过滤事件，你可以在列上使用"filterEvent"属性，例如，"onblur"（默认值）。
 
如下所示：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" width="200px">
        <f:facet name="header">
            <h:outputText value="Sorting Example"/>
        </f:facet>
        <rich:column filterBy="#{cap.state}" filterEvent="onkeyup">
                <f:facet name="header">
                    <h:outputText value="State Name"/>
                </f:facet>
               <h:outputText value="#{cap.state}"/>
        </rich:column> 
        <rich:column filterBy="#{cap.name}" filterEvent="onkeyup">
            <f:facet name="header">
                <h:outputText value="State Capital"/>
            </f:facet>
            <h:outputText value="#{cap.name}"/> 
        </rich:column>
</rich:dataTable>
...
 
结果：

 
图6.19 内置过滤功能的使用。
 
 
n         使用外部过滤。在这种情况下，你需要编写你的定制过滤函数或表达式，以及定义控件。
 
"filterExpression"属性被用来定义求布尔值的表达式。这个表达式检查是否对象满足过滤条件。
 
"filterMethod"属性被用来定义方法绑定。这个方法访问对象参数，并返回布尔值。因此，这个方法也可以用来检查是否对象满足过滤条件。使用这个属性的最好方式，是用于实现你自己的复杂业务逻辑。
 
"filterExpression"和 "filterMethod"属性使用的简单例子，请看RichFaces  LiveDemo页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/filteringFeature.jsf?tab=ex-usage&cid=4110192]
 
 
6.6.1.5    参数数据
 
<rich:column> 属性表 [../../tlddoc/index.htmlrich/column.html]。
 
表6.30 组件关联的参数
名字	值
component-type	org.richfaces.Column
component-class	org.richfaces.component.html.HtmlColumn
component-family	org.richfaces.Column
renderer-type	org.richfaces.renderkit.CellRenderer
tag-class	org.richfaces.taglib.ColumnTag
 
表6.31. Facets
Facet名字	描述
header	定义页眉内容
footer	定义页脚内容
 
定制<rich:column>的样式类和皮肤参数，与<rich:dataTable>组件相同。
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.1.6    关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Column页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/dataTable.jsf?c=column]
 
如何使用<rich:column> 的"rendered"属性，请看RichFaces Cookbook文章[http://www.jboss.org/community/docs/DOC-9607]的例子。
 
6.6.2     < rich:columnGroup >，从3.0.0版开始可用
 
6.6.2.1    描述
 
该组件在一行中合并列，用于组织一个表的复杂子部分。
 
6.6.2.2    主要功能
 
n         完美的皮肤表行和子元素。
n         在内部可以合并列和行。
n         利用Ajax可以更新一组有限的字符串。
 
6.6.2.3    使用细节
 
<rich:columnGroup>组件合并列集合，包裹它们到<tr>元素，并输出它们到一行。列合并为一组，与在对列使用"breakBefore" 属性移动到下行时的方式相同。因此，以下例子是一样的：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5" id="sublist"> 
        <rich:column colspan="3">
                <f:facet name="header">State Flag</f:facet>
                <h:graphicImage value="#{cap.stateFlag}"/>
        </rich:column>
       <rich:columnGroup>
                <rich:column> 
                    <h:outputText value="#{cap.state}"/>
                </rich:column>
               <rich:column >
                    <h:outputText value="#{cap.name}"/>
               </rich:column>
               <rich:column >
                    <h:outputText value="#{cap.timeZone}"/>
               </rich:column>
        </rich:columnGroup> 
</rich:dataTable>
...
 
下面是一个没有分组的表示：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5" id="sublist"> 
        <rich:column colspan="3">
                <f:facet name="header">State Flag</f:facet>
                <h:graphicImage value="#{cap.stateFlag}"/>
        </rich:column>
        <rich:column breakBefore="true">
                <h:outputText value="#{cap.state}"/>
        </rich:column>
        <rich:column>
                <h:outputText value="#{cap.name}"/>
        </rich:column>
        <rich:column>
                <h:outputText value="#{cap.timeZone}"/>
        </rich:column>
</rich:dataTable>
....
 
结果：

 
图6.21  使用<rich:columnGroup>组件生成的表
 
也可以使用该组件在一个表中输出复杂的标题。例如，以下是一个添加复杂标题到整个表的一个facet例子：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5" id="sublist"> 
        <f:facet name="header">
            <rich:columnGroup>
                <rich:column rowspan="2">
                    <h:outputText value="State Flag"/>
                </rich:column>
                <rich:column colspan="3">
                    <h:outputText value="State Info"/>
                </rich:column>
                <rich:column breakBefore="true">
                    <h:outputText value="State Name"/>
                </rich:column>
                <rich:column>
                    <h:outputText value="State Capital"/>
                </rich:column>
                <rich:column>
                    <h:outputText value="Time Zone"/>
                </rich:column>
            </rich:columnGroup>
        </f:facet>
        <rich:column>
                <h:graphicImage value="#{cap.stateFlag}"/>
        </rich:column>
        <rich:column>
                <h:outputText value="#{cap.state}"/>
        </rich:column>
        <rich:column>
                <h:outputText value="#{cap.name}"/>
        </rich:column>
        <rich:column>
                <h:outputText value="#{cap.timeZone}"/>
        </rich:column>
</rich:dataTable>
...
 
在页面上生成的表如下所示：

 
图6.22  使用复杂标题的<rich:columnGroup>
 
6.6.2.4    参数数据
 
<rich:columnGroup>表属性[../../tlddoc/index.htmlrich/columnGroup.html]
 
表6.32 组件关联的参数
名字	值
component-type	org.richfaces.ColumnGroup
component-class	org.richfaces.component.html.HtmlColumnGroup
component-family	org.richfaces.ColumnGroup
renderer-type	org.richfaces.ColumnGroupRenderer
tag-class	org.richfaces.taglib.ColumnGroupTag
 
定制<rich:columnGroup>的样式类和皮肤参数，与<rich:dataTable>组件相同。
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.2.5    相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:columnGroup>页面：
[http://livedemo.exadel.com/richfaces-demo/richfaces/dataTable.jsf?c=columnGroup]
 
6.6.3     < rich:columns >，从3.0.0版开始可用
 
6.6.3.1    描述
 
<rich:columns>组件，允许你根据你的模型创建动态列集。
 

 图6.23  <rich:columns>组件
 
6.6.3.2    主要功能
 
n       高度定制感观
n       动态表创建
n       可以利用"colspan"和"breakBefore"的帮助合并列
n       可以利用 "rowspan"的帮助合并行
n       排序列值
n       过滤列值
 
6.6.3.3    使用细节
 
<rich:columns>组件从数据模型获取一个列表，并输出到在页面上的<rich:dataTable>内部的相应的列集。可以与<rich:columns>组件一起使用  "header"和 "footer"  facets。
 
 "value"和"var"属性用来访问集合的值。  
 
下面是一个简单的例子：
 
...
<rich:dataTable value="#{dataTableScrollerBean.model}" var="model" width="750">
            <rich:columns value="#{dataTableScrollerBean.columns}" var="columns"  index="ind" id="column#{ind}"> 
                <f:facet name="header">
                    <h:outputText value="#{columns.header}" />
                </f:facet>
            
                <h:outputText value="#{model[ind].model} " />
                <h:outputText value="#{model[ind].mileage} miles " />
                <h:outputText value="#{model[ind].price}$" />       
            </rich:columns> 
</rich:dataTable>                       
...
 
"columns"属性定义列数。
 
"rowspan"属性定义被显示的行数。如果这个属性的值为0，在表中所有剩余的行被显示在页面上。
 
"begin"属性包含第一个迭代项。注意，它从0开始迭代。
 
"end"属性包含最后一个迭代项。
 
利用上面描述的这些属性的帮助，你可以定制输出，例如，定义那个列和多少行显示在页面上。
 
<rich:columns>组件并不阻碍使用<rich:column>。下面的例子，一个列用任何方式渲染，而另一个从模型中选取。
 
例子：
 
...
<rich:dataTable value="#{dataTableScrollerBean.model}" var="model" width="500px" rows="5">
        <f:facet name="header">
                <h:outputText value="Cars Available"></h:outputText>
        </f:facet>
        <rich:columns value="#{dataTableScrollerBean.columns}" var="columns" index="ind">
                <f:facet name="header">
                        <h:outputText value="#{columns.header}" />
                </f:facet>
                <h:outputText value="#{model[ind].model} " />
        </rich:columns>
        <rich:column>
                <f:facet name="header">
                        <h:outputText value="Price" />
                </f:facet>
               <h:outputText value="Price" />
        </rich:column>
        <rich:columns value="#{dataTableScrollerBean.columns}" var="columns" index="ind">
                <f:facet name="header">
                        <h:outputText value="#{columns.header}" />
                </f:facet>
                <h:outputText value="#{model[ind].mileage}$" />
        </rich:columns>
</rich:dataTable>
...                              
                   
对<rich:columns>，可以利用"colspan"、"rowspan"和"breakBefore"属性的帮助，分组列为一列或一行，就象<rich:columnt> 组件执行的方法一样。
 
[注意，<rich:columns>标签在组件树构建处理期间被初始化。这个处理在“渲染响应”JSF阶段的页面渲染之前。要完全地渲染组件，需要在组件树构建时，初始化它所有的变量。如果<rich:columns> 使用的变量从其他组件传入，如果这些变量在渲染期间被初始化，一个javax.servlet.jsp.JspTagException异常发生。因此，当<rich:columns>请求这些变量时，他们并不存在。使用<c:forEach> JSP标准标签作为替代。比较下面两个例子。
 
这个代码调用异常：
 
...
<rich:dataTable value="#{bean.data}" var="var">
        <rich:columns value="#{var.columns}">
                ...
        </rich:columns>
</rich:dataTable>
...
 
这个代码正常运行：
 
...
<c:forEach items="#{bean.data}" var="var">
        <rich:columns value="#{var.columns}">
                ...
        </rich:columns>
</c:forEach>
...
]
 
[注意，从3.3.0GA开始，<rich:columns>]需要显式定义子组件的"id"，以确保解码处理正常运行。你如何为子组件定义唯一"id"，如下所示：
 
...
<rich:columns value="#{bean.columns}" var="col" index="ind" ... >
        <h:inputText id="input#{ind}" value="">
                <a4j:support id="support#{ind}" event="onchange" reRender="someId" />
        </h:inputText>
</rich:columns> 
... 
 
只有如上面的Ajax所示定义"id"，在onchange事件之后，才会象你希望的一样被处理。]
 
<rich:columns>组件的排序和过滤，与 <rich:column>运行的相同。请看“排序和过滤”一节。
 
6.6.3.4    参数数据
 
<rich:columns> 属性表 [../../tlddoc/index.htmlrich/columns.html]。
 
表6.33 组件关联的参数
名字	值
component-type	org.richfaces.Column
tag-class	org.richfaces.taglib.ColumnsTagHandler
 
表6.34. Facets
Facet名字	描述
header	定义页眉内容
footer	定义页脚内容
 
定制<rich:columns>的样式类和皮肤参数，与<rich:dataTable>组件相同。
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.3.5    相关联的资源链接
 
有关<rich:columns>组件用法的其他信息，你可以查看组件LiveDemo页面：
[http://livedemo.exadel.com/richfaces-demo/richfaces/dataTable.jsf?c=columns]
 
6.6.4     < rich:dataDefinitionList >，从3.0.0版开始可用
 
6.6.4.1    描述
 
该组件用于渲染定义列表，它允许从数据模型选择数据，并且获得了内置Ajax更新支持。
 

图6.24   <rich:dataDefinitionList>组件
 
6.6.4.2    主要功能
 
l         完美的皮肤表行和子元素
l         可以利用Ajax更新一组有限的行
l         可以从模型动态地接受值
 
6.6.4.3    使用细节
 
<rich:dataDefinitionList>组件允许根据模型生成定义列表。
 
该组件具有"term"  facet，它相应于<dt> HTML元素的"type"参数。
 
下面是一个例子：
 
...
<h:form>
      
  <rich:dataDefinitionList var="car" value="#{dataTableScrollerBean.allCars}" rows="5" first="4" title="Cars">
                <f:facet name="term">
                    <h:outputText value="#{car.make} #{car.model}"></h:outputText>
                </f:facet>
                <h:outputText value="Price:" styleClass="label"></h:outputText>
                <h:outputText value="#{car.price}" /><br/>
                <h:outputText value="Mileage:" styleClass="label"></h:outputText>
                <h:outputText value="#{car.mileage}" /><br/>
        </rich:dataDefinitionList>
</h:form>
...
 
结果为：

 
图6.25 使用了"term"  facet的<rich:dataDefinitionList>组件
 
在上面例子中，"rows"属性限定了列表输出元素的数量。
 
"first"属性定义输出的第一个元素。"title"用于一个弹出标题。
 
可以利用Ajax局部更新<rich:dataDefinitionList>组件。"ajaxKeys"属性指向一个对象（java.util.Set)），它应该包含在Ajax请求之后被更新的行键。<rich:dataList>组件的"ajaxKeys"属性的使用例子，看RichFacs Cookbook文章 [http://www.jboss.org/community/wiki/UsingtheajaxKeysattributeforrichdataList]
 
6.6.4.4    参数数据
 
<rich:dataDefinitionList>属性表[../tlddoc/index.htmlrich/dataDefinitionList.html]
 
表6.35 组件关联的参数
名字	值
component-type	Org.richfaces.DataDefinitionList
component-class	Org.richfaces.component.html.HtmlDataDefinitionList
component-family	Org.richfaces.DataDefinitionList
renderer-type	Org.richfaces.DataDefinitionListRenderer
tag-class	Org.richfaces.taglib.DataDefinitionListTag
 
表6.36 无皮肤参数的样式类（selectors）
类名	描述	 	 
.rich-deflist定义html	<dl>	元素的样式	 
.rich-definition定义	Html	<dd>	元素的样式
.rich-definition-term定义html	<dt>元素的样式	 	 
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.4.5    相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:dataDefinitionList>页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/dataLists.jsf?c=dataDefinitionList]
 
6.6.5     < rich:dataFilterSlider >，从3.0.0版开始可用
 
6.6.5.1    描述
 
一个基于滑块动作的组件，用于过滤表数据。

 
图6.26  <rich:dataFilterSlider>组件
 
6.6.5.2    主要功能
 
n         依赖于它的子女的值过滤任何基于UIData的组件。
n         完全可换肤的控件和输入元素。
n         可选的，带有一个管理的属性位置的值文本字段。
n         可选的，在一个页面上废弃的组件。
n         可选的，只要拖动句柄就显示当前值的工具提示。
n         鼠标移动后，拖动的状态是稳定的。
n         可选的，如果文本输入字段出现，可以手工输入。
n         手工输入验证。
 
6.6.5.3    使用细节
 
dataFilterSlider组件使用"for"属性绑定到某些UIData组件，并过滤在一个表中的数据。
 
例子：
 
...
<rich:dataFilterSlider sliderListener="#{mybean.doSlide}"
                        startRange="0"
                        endRange="50000"
                        increment="10000"
                        handleValue="1"
                        for="carIndex"
                        forValRef="inventoryList.carInventory" 
                        filterBy="getMileage" />
...
<h:dataTable id="carIndex"> 
        ... 
</h:dataTable>
...
 
在上面的例子中，不同的两个属性用于过滤：
 
n         "forValRef" 是一个字符串，它被用于目标UIData组件的一个值属性。旨在重新设置UIData组件支持由后台bean提供的原始列表。
 
n         "filterBy" 是一个对象成员的getter，用于与滑块值的比较。它的值用于结果过滤。
 
"handleValue"属性，用于保存在dataFilterSlider上当前的句柄的位置。根据当前的值，适当的值，根据"filterBy"定义的getter获得的，被过滤。
 
一个更重要的属性是"storeResults"，它准许dataFilterSlider组件在会话中保存UIData目标对象。
 
如果组件需要根据句柄状态改变的事件提交表单，使用"submitOnSlide"属性。当属性定义为"true"，根据事件提交被定义。
 
有关"process"属性的用法的信息，请查看“决定处理什么”指南一节。
 
6.6.5.4    参数数据
 
<rich:dataFilterSlider>属性表 [../../tlddoc/index.htmlrich/dataFilterSlider.html]。
 
表6.37 组件关联的参数
名字	值
component-type	org.richfaces.DataFilterSlider
component-class	org.richfaces.component.html.HtmlDataFilterSlider
component-family	org.richfaces.DataFilterSlider
renderer-type	org.richfaces.DataFilterSliderRenderer
tag-class	org.richfaces.taglib.dataFilterSliderTag
 
表6.38 使用相应皮肤参数的样式类（selectors）
类名(selectors)	描述	皮肤参数	CSS属性映射
.range, .rich-dataFilterSlider-range	定义组件范围的样式	subBorderColor, panelBorderColor 	border-color
.slider-input-field, .rich-dataFilterSlider-input-field	定义组件输入字段的样式	controlBackgroundColor	background-color
		generalFamilyFont	font-family
		generalSizeFont	font-size
		controlTextColor	color
		panelBorderColor	border-color
		subBorderColor	border-bottom-color,    border-right-color
 
表6.39 无皮肤参数的样式类（selectors）
类名	描述
.trailer, .rich-dataFilterSlider-trailer	定义组件尾部（trailer）的样式
.track, .rich-dataFilterSlider-track	定义组件轨迹（track）的样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.5.5    相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:dataFilterSlider>页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/dataFilterSlider.jsf?c=dataFilterSlider]
 
6.6.6     < rich:dataGrid >，从3.0.0版开始可用
 
6.6.6.1    描述
 
该组件渲染数据为一个网格，它允许从模型选择数据，并且获得了Ajax更新的内置支持。
 
 
图6.27 < rich:dataGrid >组件
 
6.6.6.2    主要功能
 
n         完美的皮肤表和子元素
n         利用Ajax可以更新一组有限的行
n         可以从模型动态地接收值
 
6.6.6.3    使用细节
 
该组件根据模型获得列表，并输出它的方法象使用 <h:panelGrid>输出内嵌数据一样。要定义网络属性和样式，如<h:panelGrid>的一样使用相同的定义。
 
组件允许：
 
n         使用"header"和"footer" facets，用于输出。
n         限制输出元素（"elements"属性）的数量，并且定义输出的开始元素（"first"属性）。
n         使用<rich:datascroller>组件绑定页面。
 
下面是个例子：
 
...
<rich:panel style="width:150px;height:200px;">
        <h:form>
              
  <rich:dataGrid value="#{dataTableScrollerBean.allCars}" var="car" columns="2" elements="4" first="1">
                    <f:facet name="header">
                            <h:outputText value="Car Store"></h:outputText>
                        </f:facet>
                        <rich:panel>
                            <f:facet name="header">
                                    <h:outputText value="#{car.make} #{car.model}"></h:outputText>
                            </f:facet>
                            <h:panelGrid columns="2">
                                    <h:outputText value="Price:" styleClass="label"></h:outputText>
                                    <h:outputText value="#{car.price}"/>
                                    <h:outputText value="Mileage:" styleClass="label"></h:outputText>
                                    <h:outputText value="#{car.mileage}"/>
                            </h:panelGrid>
                        </rich:panel>
                        <f:facet name="footer">
                            <rich:datascroller></rich:datascroller>
                        </f:facet>
                </rich:dataGrid>
        </h:form>
</rich:panel>       
...
 
结果为：

 
图6.28 组件的用法
 
 
该组件是基于<a4j:repeat>组件被创建的，因此它可以使用Ajax局部更新。"ajaxKeys"属性允许定义在一个Ajax请求之后被更新的行键。
 
例子：
 
...
<rich:dataGrid value="#{dataTableScrollerBean.allCars}" var="car" ajaxKeys="#{listBean.list}"  binding="#{listBean.dataGrid}" id="grid" elements="4" columns="2">
        ...
</rich:dataGrid>
...
<a4j:commandButton action="#{listBean.action}" reRender="grid" value="Submit"/>
...
 
在这个例子中，"reRender"属性包含用于<rich:dataGrid>的"id"属性的值。因此，在一个Ajax请求后，组件被更新。
 
6.6.6.4    参数数据
 
<rich:dataGrid>属性表[../../tlddoc/index.htmlrich/dataGrid.html].
 
表6.40 组件关联的参数
名字	值
component-type	org.richfaces.DataGrid
component-class	org.richfaces.component.html.HtmlDataGrid
component-family	org.richfaces.DataGrid
renderer-type	org.richfaces.DataGridRenderer
tag-class	org.richfaces.taglib.DataGridTag
 
定制<rich:dataGrid>的样式类和皮肤参数，与<rich:dataTable>组件相同。
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.6.5    相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:dataGrid>页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/dataGrid.jsf?c=dataGrid]
 
6.6.7     < rich:dataList >，从3.0.0版开始可用
 
6.6.7.1    描述
 
该组件渲染无序列表，它准许从模型选择数据，并且获得了Ajax更新的内置运载。
 
 
图6.29   <rich:dataList>组件
 
6.6.7.2    主要功能
 
n         一个完美的皮肤列表和子元素
n         利用Ajax可以更新一组有限的行
n         可以从模型动态地接收值
 
6.6.7.3    使用细节
 
<rich:dataList>允许从模型生成列表。
 
组件有"type"属性，它相应于<ul>  HTML元素的"type"属性，并且定义了一个标记类型。"type"可取的值有："disc","circle", "square"。
 
例子：
 
...
<h:form>
      
   <rich:dataList  var="car"  value="#{dataTableScrollerBean.allCars}"  rows="5"  type="disc"  title="Car Store">
                <h:outputText value="#{car.make} #{car.model}"/><br/>
                <h:outputText value="Price:" styleClass="label"></h:outputText>
                <h:outputText value="#{car.price} "/><br/>
                <h:outputText value="Mileage:" styleClass="label"></h:outputText>
                <h:outputText value="#{car.mileage} "/><br/>
        </rich:dataList>
</h:form>
...
 
结果为：

 
图6.30.   使用了"type"属性的<rich:dataList>
 
在这个例子中，"rows"属性限定了列表输出元素的数量。
 
"first"属性定义输出的开始元素。"title" 用于弹出标题。如下所示：
 

 
图6.31  使用了"title"属性的<rich:dataList>组件
 
<rich:dataList>组件可以利用Ajax进行局部更新。"ajaxKeys"属性指向一个对象（java.util.Set)），它应该包含在Ajax请求之后被更新的行键。该属性的使用例子，看RichFaces Cookbook 的“使用<rich:dataList>的ajaxKeys 属性”一文： [http://www.jboss.org/community/wiki/UsingtheajaxKeysattributeforrichdataList]
 
6.6.7.4    参数数据
 
<rich:dataList>属性表 [../../tlddoc/index.htmlrich/dataList.html]。
 
表6.42 组件关联的参数
名字	值
component-type	org.richfaces.DataList
component-class	org.richfaces.component.html.HtmlDataList
component-family	org.richfaces.DataList
renderer-type	org.richfaces.DataListRenderer
tag-class	org.richfaces.taglib.DataListTag
 
表6.43 无皮肤参数的样式类（selectors）
类名	描述
.rich-datalist	定义html<ul>元素的样式
.rich-list-item	定义html<li>元素的样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.7.5    相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:dataList>页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/dataLists.jsf?c=dataList]
 
6.6.8     < rich:dataOrderedList >，从3.0.0版开始可用
 
6.6.8.1    描述
 
该组件渲染有序列表，它准许从模型选择数据，并且获得了Ajax更新的内置运载。
 

 
图6.32  <rich:dataOderedList>组件
 
6.6.8.2    主要功能
 
n         一个完美的皮肤列表和子元素
n         利用Ajax可以更新一组有限的行
n         可以从模型动态地接收值
 
6.6.8.3    使用细节
 
<rich:dataOrderedList>允许从模型生成有序列表。
 
组件有"type"属性，它相应于<ol>   HTML元素的"type"属性，并且定义了一个标记类型。"type"可取的值有："A","a", "I", "i", "1"。
 
例子：
...
<h:form>
      
   <rich:dataOrderedList  var="car"  value="#{dataTableScrollerBean.allCars}"  rows="5"  type="1"    title="Car  Store">
                <h:outputText value="#{car.make} #{car.model}"/><br/>
                <h:outputText value="Price:" styleClass="label"></h:outputText>
                <h:outputText value="#{car.price}" /><br/>
                <h:outputText value="Mileage:" styleClass="label"></h:outputText>
                <h:outputText value="#{car.mileage}" /><br/>
        </rich:dataOrderedList>
</h:form>
...
 
结果为：

 
图6.33 使用了"type"属性的 <rich:dataOrderedList>组件
 
在这个例子中，"rows"属性限定了列表输出元素的数量。
 
"first"属性定义输出的开始元素。"title" 用于弹出标题。
 
<rich:dataOrderedList>组件可以利用Ajax进行局部更新。"ajaxKeys"属性指向一个对象（java.util.Set)），它应该包含在Ajax请求之后被更新的行键。该<rich:dataOrderedList>的"ajaxKeys"属性的使用例子，看RichFaces Cookbook的文章：  [http://www.jboss.org/community/wiki/UsingtheajaxKeysattributeforrichdataList]
 
6.6.8.4    参数数据
 
<rich:dataOrderedList>属性表[../../tlddoc/index.htmlrich/dataOrderedList.html]。
 
 
表6.44 组件关联的参数
名字	值
component-type	org.richfaces.DataOrderedList
component-class	org.richfaces.component.html.HtmlDataOrderedList
component-family	org.richfaces.DataOrderedList
renderer-type	org.richfaces.DataOrderedListRenderer
tag-class	org.richfaces.taglib.DataOrderedListTag
 
表6.45 无皮肤参数的样式类（selectors）
类名	描述
.rich-orderedlist	定义html<ol>元素的样式
.rich-list-item	定义html<li>元素的样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.8.5    相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:dataOrderedList >页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/dataLists.jsf?c=dataOrderedList]
 
6.6.9     < rich:datascroller >，从3.0.0版开始可用
 
6.6.9.1    描述
 
该组件旨在使用Ajax请求提供滚动表功能。
 

 
表6．34   <rich:datascroller>组件
 
6.6.9.2    主要功能
 
n         提供表滚动功能
n         内置Ajax处理
n         提供快速控制
n         皮肤支持
 
6.6.9.3    使用细节
 
<rich:datascroller>组件提供滚动表功能，和TOMAHAWK滚动器一样，但TOMAHAWK滚动器不支持Ajax请求的使用。
 
当你改变过滤，根据<rich:dataTable>的当前模型更新排序时，<rich:datascroller>组件也应该与<rich:dataTable>一起被渲染。
 
该组件应该放置在父表的页脚内，或者使用"for"属性绑定它。注意，"for"属性在构建时被求值，而不是在渲染时，这就是为什么它会被JSTL标签忽略。
 
表也应该定义"rows"属性，限定表输入的行数。
 
滚动器也应该利用"maxPages"属性的帮助，限定在页面上显示的链接最大数。
 
组件提供两个控制器组，用于切换： 
 
n         切换到特殊页面的页面数字
 
n         快速切换控件："first", "last", "next","previous", "fastforward", "fastrewind"。
 
利用相应的名字添加facets组件创建快速切换控件：
 
例子：
 
...
<rich:datascroller for="table" maxPages="10">
          <f:facet name="first">
                    <h:outputText value="First"/>
          </f:facet>
          <f:facet name="last">
                    <h:outputText value="Last"/>
          </f:facet>
</rich:datascroller>
...
 

 
图6.35   <rich:datascroller>的快速切换
 
该屏幕截图显示了各组的一个控制器。
 
也有禁用状态的facets："first_disabled","last_disabled",  "next_disabled",  "previous_disabled",  "fastforward_disabled","fastrewind_disabled"。
 
对"fastforward"/"fastrewind"控制的定制，使用另外的"fastStep"属性。在快速滚动使用时，该属性指明切换的页面数。
 
"page"是一个值绑定属性，用于定义和保存当前的页数。如下所示：
 
...
<h:form id="myForm">
  
  <rich:dataTable id="carList" rows="7" value="#{dataTableScrollerBean.allCars}" var="category">
        <f:facet name="header">
            <rich:columnGroup>
                <h:column>
                    <h:outputText value="Make" />
                </h:column>
                <h:column>
                    <h:outputText value="Model" />
                </h:column>
                <h:column>
                    <h:outputText value="Price" />
                </h:column>
            </rich:columnGroup>
        </f:facet>
        <h:column>
            <h:outputText value="#{category.make}" />
        </h:column>
        <h:column>
            <h:outputText value="#{category.model}" />
        </h:column>
        <h:column>
            <h:outputText value="#{category.price}" />
        </h:column>
    </rich:dataTable>
  
   <rich:datascroller  id="sc2"  for="carList"  reRender="sc1"  maxPages="7"  page="#{dataTableScrollerBean.scrollerPage}"  />
 
    <h:panelGrid>
        <h:panelGroup>
            <h:outputText value="Set current page number:" />
            <h:inputText value="#{dataTableScrollerBean.scrollerPage}" id="sc1" size="1"/>
            <h:commandButton value="Set" />
        </h:panelGroup>
    </h:panelGrid>
</h:form>
...
 
结果如下：

 
图6.36  "page"属性的用法
 
"pageIndexVar"和"pagesVar"属性定义一个请求域变量，并在<rich:datascroller>中提供显示当前页和页数的能力。
 
这些属性被用来定义变量名字，它们被用于使用"pages"的facet中。如下所示：
 
...
<h:form>
    <rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5">
        <rich:column>
            <h:outputText value="#{cap.name}" />
        </rich:column>
        <f:facet name="footer">
            <rich:datascroller pageIndexVar="pageIndex" pagesVar="pages">
                <f:facet name="pages">
                    <h:outputText value="#{pageIndex} / #{pages}" />
                </f:facet>
            </rich:datascroller>
        </f:facet>
    </rich:dataTable>
</h:form>
...
 
可以在两个控件中插入随意的分隔符。为这个目的，使用"controlsSeparator"  facet。如下所示：
 
...
<f:facet name="controlsSeparator">
          <h:graphicImage value="/image/sep.png"/>
</f:facet>
...
 
从RichFaces 3.2.1开始，多<rich:datascroller>实例的行为和页面绑定被调整。在模型改变之后，增加了不正确页面的处理。在渲染响应之前，调用阶段侦听器扫描<rich:datascroller>的页面，并且执行下面的操作：
 
n         检查是否<rich:datascroller>被渲染。（如果检查发生异常，<rich:datascroller>被认为不会被渲染）
 
n         如果<rich:datascroller>被渲染 ——附加了<rich:datascroller>的表获得<rich:datascroller>的页面属性的值。
 
有关"process"属性用法的信息，请看“决定处理什么”指南一节。
 
[注意，确保为一个表定义的所有<rich:datascroller>组件，对所有"page"属性有相同的值。在最后一个"page"中指定的页面，在浏览器中会被渲染。]
 
6.6.9.4    参数数据
 
<rich:datascroller>属性表 [../../tlddoc/index.htmlrich/datascroller.html]。
 
表6.46 组件关联的参数
名字	值
component-type	org.richfaces.Datascroller
component-class	org.richfaces.component.html.HtmlDatascroller
component-family	org.richfaces.Datascroller
renderer-type	org.richfaces.DataScrollerRenderer
tag-class	org.richfaces.taglib.DatascrollerTag
 
表6.47. JavaScript API
函数	描述
switchToPage(page)	切换到定义的页面，"page"是一个数字或字符串
next()	导航到下个页面
previous()	导航到上个页面
first()	导航到首页
last()	导航到最后一页页
fastForward()	越过一定数目的页面导航向前。利用fastStep属性定义横过的页面数。
fastRewind()	越过一定数目的页面导航向后。利用fastStep属性定义横过的页面数。
 
表6.48  Facets
Facet	描述
controlsSeparator 	在两个控件之间重新定义随意的分隔符
First	使用内容集合重新定义"first"按钮
first_disabled 	使用内容集合重新定义禁用的"first"按钮
last 	使用内容集合重新定义"last"按钮
last_disabled	使用内容集合重新定义禁用的"last"按钮
Fastrewind	使用内容集合重新定义"fastrewind"按钮
fastrewind_disabled 	使用内容集合重新定义禁用的"fastrewind"按钮
fastforward 	使用内容集合重新定义"fastforward"按钮
fastforward_disabled	使用内容集合重新定义禁用的"fastforward"按钮
previous 	使用内容集合重新定义"previous"按钮
previous_disabled 	使用内容集合重新定义禁用的"previous"按钮
Next	使用内容集合重新定义"next"按钮
next_disabled 	使用内容集合重新定义禁用的"next"按钮
pages 	使用内容集合重新定义"pages"按钮
 
			表6.49使用相应皮肤参数的样式类（selectors）
			
类名(selectors)	描述	皮肤参数	CSS属性映射
.rich-datascr-button	定义按钮的样式	additionalBackgroundColor	background-color
		panelBorderColor	border-color
		panelBorderColor	border-color
		generalFamilyFont	font-family
		generalSizeFont	font-size
.rich-datascr-ctrls-separator	定义两个按钮间分隔符的样式	additionalBackgroundColor 	background-color
		panelBorderColor	border-color
		panelBorderColor	border-color
		generalFamilyFont	font-family
		generalSizeFont	font-size
.rich-datascr-button-dsbld	定义禁用的铵钮的样式	panelBorderColor	color
.rich-datascr-act	定义活动的铵钮的样式	generalTextColor	border-top-color, color
		generalFamilyFont	font-family
		generalSizeFont	font-size
.rich-datascr-inact	定义不活动的铵钮的样式	headerBackgroundColor 	border-top-color, color
		generalFamilyFont	font-family
		generalSizeFont	font-size
.rich-dtascroller-table	定义数据滚动器的包裹器<table>元素的样式	panelBorderColor	border-color
		tableBackgroundColor	background-color
			
表6. 50 无皮肤参数的样式类（selectors）
类名	描述
.rich-datascr	定义数据滚动器的包裹器<div>元素的样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.9.5    相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:datascroller>页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/dataTableScroller.jsf?c=dataTableScroller]
 
使用数据滚动器进行正确的分页（从数据库加载数据）的解决方案，请看RichFaces用户论坛：[http://www.jboss.com/index.html?module=bb&op=viewtopic&p=4060199#4060199]
 
在扩展数据模型上下文中如何使用<rich:dataTable>和 <rich:datascroller>，请看RichFaces用户论坛：[http://www.jboss.com/index.html?module=bb&op=viewtopic&t=115636]
 
这篇文章：[http://www.jboss.org/community/wiki/DataTablemodeldoesntgetupdatedwhenrichdatascrollerused]，描述在使用<rich:datascroller>时，如何解决<rich:datatable>更新问题。
 
在这儿：[http://www.jboss.org/community/wiki/HowtousepairofrichdatascrollersoutsidetheanydataTable]，你可以找到在任何数据表外部如何使用一对<rich:datascrollers>。
 
有关在排序或过滤之后，如何进行<rich:datascroller>更新的解决方案，请看“数据迭代常见问题”：[http://www.jboss.org/community/wiki/richdataScrollerisnotupdatedaftersortingfiltering]



6.6.10 < rich:dataTable >，从3.0.0版开始可用
 
6.6.10.1描述
 
该组件用于渲染表。它准许从模型选择数据，并且获得了Ajax更新的内置支持。
 
  
图6.37 <rich:dataTable>组件
 
6.6.10.2主要功能
 
n         完美的皮肤表 和子元素
n         可以插入复杂 的子组件"colGroup"和"subTable"
n         可以利用Ajax更新一组有限的字符串
n         用于表列的排 序和过滤功能
 
    扩展的表功能，比如，可滚动数据，行选择，以及列重新排序，要求使用<rich:extendedDataTable>组件，而不是<rich:dataTable>。两个组件的区别的详情，请看<rich:extendedDataTable>一节。
 
6.6.10.3使用细节
 
    除了换肤功能和Ajax支持之外，<rich:dataTable>组件是相似于<h:dataTable>。Ajax支 持是可能的，因为该组件是基于<a4j:repeat>，所以可以利用Ajax进行局部更新。"ajaxKeys"属性允许定义在一个Ajax请求之后被更新的行键。有关用于数据迭代组件的"ajaxKeys"属性的用法演示例子，你可在RichFaces Cookbook的文章：[http://www.jboss.org/community/wiki/UsingtheajaxKeysattributeforrichdataList]找到。
 
    [注意，如果你需要使用一些扩展功能渲染表，如数据滚动，利用上下文菜单的帮助隐藏列，等等，那么使 用<rich:extendedDataTable>组件代替。]
 
    该组件允许使用"header", "footer"和"caption" facets用于输出。如下所示：
 
...
<rich:dataTable value="#{capitalsBean.capitals}" var="cap" rows="5">
        <f:facet name="caption">
                <h:outputText value="United States Capitals" />
        </f:facet>
        <f:facet name="header">
                <h:outputText value="Capitals and States Table" />
        </f:facet>
        <rich:column>
                <f:facet name="header">State Flag</f:facet>
                        <h:graphicImage value="#{cap.stateFlag}"/>
                <f:facet name="footer">State Flag</f:facet>
        </rich:column>
        <rich:column>
                <f:facet name="header">State Name</f:facet>
                        <h:outputText value="#{cap.state}"/>
                <f:facet name="footer">State Name</f:facet>
        </rich:column>
        <rich:column >
                <f:facet name="header">State Capital</f:facet>
                        <h:outputText value="#{cap.name}"/>
                <f:facet name="footer">State Capital</f:facet>
        </rich:column>
        <rich:column>
                <f:facet name="header">Time Zone</f:facet>
                    <h:outputText value="#{cap.timeZone}"/>
                <f:facet name="footer">Time Zone</f:facet>
        </rich:column>
        <f:facet name="footer">
                <h:outputText value="Capitals and States Table" />
        </f:facet>
</rich:dataTable>
...
 
结果为：
 
图6.38.   使用facets的<rich:dataTable>组件
 
有关排序和过滤的信息，你可查看相应的章节。
 
   有关如何删除表头的渐变的信息，你可以查看“如何删除rich:dataTable表头背景”一文：[http://wiki.jboss.org/wiki/RichFacesDataTableBackgroundOut]。
 
6.6.10.4参数数据
 
<rich:dataTable>属性表[../../tlddoc/index.htmlrich/dataTable.html]。
 
表6.51 组件关联的参数
名字	值
component-type	org.richfaces.DataTable
component-class	org.richfaces.component.html.HtmlDataTable
component-family	org.richfaces.DataTable
renderer-type	org.richfaces.DataTableRenderer
tag-class	org.richfaces.taglib.DataTableTag
 
表6.53 Facets
Facet	描述
header	定义表头内容
footer	定义表脚内容
caption	定义标题内容
 
表6.53 使用了相应皮肤参数的样式类（selectors）
类名(selectors)	描述	皮肤参数	CSS属性映射
.rich-table	定义表的样式	tableBackgroundColor 	background-color
.rich-table-cell	定义表单元的样式	generalSizeFont 	font-size
		generalTextColor	color
		generalFamilyFont	font-family
.rich-table-header	定义表头行的样式	tableBackgroundColor	background-color
.rich-table-header-continue	定义在第一个之后的所有表头行的样式	headerBackgroundColor 	background-color
.rich-table-headercell	定义表头单元的样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
		headerTextColor	color
		headerWeightFont	font-weight
		generalSizeFont	font-size
		generalFamilyFont	font-family
.rich-table-subheader	定义列头的样式	additionalBackgroundColor	background-color
.rich-table-thead	 	tableBorderWidth,tableBorderColor	border-bottom
.rich-table-subheadercell	定义列头单元的样式	tableBorderWidth,tableBorderColor	border-right
		generalTextColor	color
		generalSizeFont	font-size
		generalFamilyFont	font-family
.rich-table-footer	定义表脚行的样式	tableFooterBackgroundColor 	background-color
.rich-table-footer-continue	定义在第一个之后的所有表脚行的样式	tableFooterBackgroundColor 	background-color
.rich-table-footercell	定义表脚单元的样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
		generalTextColor	color
		headerWeightFont	font-weight
		generalSizeFont	font-size
		generalFamilyFont	font-family
.rich-table-subfooter	定义子列脚的样式	tableSubfooterBackgroundColor 	background-color
.rich-table-subfootercell	定义列脚单元的样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
		generalTextColor	color
		generalSizeFont	font-size
		generalFamilyFont	font-family
 
表6.54 无参数的样式类（selectors）
类名	描述
.rich-table-caption	定义"caption" facet元素的样式
.rich-table-row	定义一个表行的样式
.rich-table-firstrow	定义一个表的首行的样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.10.5相关联的资源链接
 
    组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的<rich:dataTable>页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/dataTable.jsf?c=dataTable]
 
    有关<rich:dataTable>的灵活性，请看“rich:dataTable的灵活性”一文： [http://www.jboss.org/community/docs/DOC-11847]。
 
    “有关dataTable的换肤”一文：[http://www.jboss.org/community/docs/DOC-11848]，提供了一个换肤的简单例子。
 
    使用<rich:dataTable>和 <rich:subTable>的详情，请看RichFaces用户论坛：[http://www.jboss.com/index.html?module=bb&op=viewtopic&p=4059044#4059044]。
 
    如何在扩展数据模型中使用<rich:dataTable>和 <rich:datascroller>，请看RichFaces用户论坛：[http://www.jboss.com/index.html?module=bb&op=viewtopic&t=115636]。
 
    如何设置rich:dataTable的边界为0px， 请看“rich:dataTable的边界为0px”一文：[http://www.jboss.org/community/docs/DOC-11861]。
 
    如何删除rich:dataTable表头背景，请看“dataTable背景外观”一文：[http://www.jboss.org/community/docs/DOC-11860]。
 
   “Richfaces Datatable复选框”一文：[http://www.jboss.org/community/wiki/RichfacesDatatableCheckbox]，帮助您创建一个使用了复选框的列和一个在表头中使用了CheckAll复选框的Richface DataTable。
 
6.6.11  < rich:subTable >，从3.0.0版开始可用
 
6.6.11.1描述
 
该组件被用于插入子表到表内，有机会从一个模型选择数据，以及内置Ajax更新支持。
  
图6.39.   <rich:subTable>元素
 
6.6.11.2主要功能
 
n         完美的皮肤表 行和子元素
n         可以插入复杂 的列组子组件
n         可以在内部合 并行和列
n         利用Ajax可以更新一组有限的行
 
 
6.6.11.3使用细节
 
    除了Ajax支 持和换肤能力之外，<rich:subTable>组件相似于<h:dataTable>。还有一个区别是该组件不添加包裹的<table>和<tbody>标签。Ajax支 持是可能的，因为该组件是基于<a4j:repeat>，所以可以利用Ajax进行局部更新。"ajaxKeys"属性允许定义在一个Ajax请求之后被更新的行键。有关用于数据迭代组件的"ajaxKeys"属性的用法演示例子，你可在RichFaces Cookbook的文章：[http://www.jboss.org/community/wiki/UsingtheajaxKeysattributeforrichdataList]找到。
 
例子：
 
...
 
    <rich:dataTable value="#{capitalsBean.capitals}" var="capitals">
        <rich:column>
            ...
        </rich:column>
        <rich:subTable value="#{capitals.details}" var="detail" ajaxKeys="#{bean.ajaxSet}" binding="#{bean.subtable}" id="subtable">
 
            <rich:column>
                ...
            </rich:column>
        </rich:subTable>
    </rich:dataTable>
...
 
    <a4j:commandButton action="#{tableBean.action}" reRender="subtable"/>
 
...
 
该组件允许使用"header", "footer" facets用于输出。例子见<rich:dataTable>组件。
 
6.6.11.4参数数据
 
<rich:subTable>属性表[../../tlddoc/index.htmlrich/subTable.html]。
 
表6.55 组件关联的参数
名字	值
component-type	org.richfaces.SubTable
component-class	org.richfaces.component.html.HtmlSubTable
component-family	org.richfaces.SubTable
renderer-type	org.richfaces.SubTableRenderer
tag-class	org.richfaces.taglib.SubTableTag
 
表6.56. Facets
Facet名字	描述
header	定义表头内容
footer	定义脚内容
 
 
6.57 使用了相应皮肤参数的样式类（selectors）
类名(selectors)	描述	皮肤参数	CSS属性映射
.rich-subtable-cell	为子表单元定义样式	generalSizeFont	font-size
		generalTextColor	color
		generalFamilyFont	font-family
.rich-subtable-headercell	为子表头单元定义样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
		generalTextColor	color
		generalSizeFont	font-size
		generalFamilyFont	font-family
.rich-subtable-header	为子表头行定义样式	additionalBackgroundColor 	background-color
.rich-subtable-footer	为子表的脚定义样式	tableSubfooterBackgroundColor	background-color
.rich-subtable-footercell	为子表的脚单元定义样式	ableBorderWidth,tableBorderColor
 	border-right, border-bottom
 
6.58无参数的样式类（selectors）
类名	描述
.rich-subtable	定义所有子表样式
.rich-subtable-caption	定义 "caption" facet 元素的样式
.rich-subtable-header-continue	定义所有在第一个之后的子表头行的样式
.rich-subtable-subheader	定个子表的列头样式
.rich-subtable-subfooter	定个子表的列脚样式
.rich-subtable-footer-continue	定义所有在第一个之后的子表脚行的样式
.rich-subtable-subheadercell	定义子表的列头单元的样式
.rich-subtable-row	定义子表行的样式
.rich-subtable-firstrow	定义子表开始行的样式
.rich-subtable-subfootercell	定义子表的列脚单元的样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。



6.6.12 < rich:extendedDataTable >，从3.0.0版开始可用
 
6.6.12.1描述
 
该组件是为了渲染表，与标准<rich:dataTable>组件不同在于它支持一些功能。
 
  图6.40 <rich:extendedDataTable>组件
 
6.6.12.2主要功能
 
n         可以滚动数据
n         可以添加一个属性来设置选择的类型（无、单行或多行）
n         可以通过拖动列头到另外的位置，改变显示列的顺序
n         可以在上下文菜单中通过选择或取消选择，隐藏或显示列
n         可以保存设置（可视列、列宽、列的顺序），重用于下次页面的显示
n         可以合并行为组。
 
<rich:extendedDataTable>包含的，而<rich:dataTable>没有包含的属性有：
 
n         activeClass
n         activeRowKey
n         enableContextMenu
n         groupingColumn
n         height
n         noDataLabel
n         onselectionchange
n         selectedClass
n         selection
n         selectionMode
n         tableState
 
<rich:extendedDataTable>没有包含的，而<rich:dataTable>可用的属性有：
 
n         columns
n         columnsWidth
n         onRowContextMenu
 
6.6.12.3使用细节
 
<rich:extendedDataTable>组件相似于<rich:dataTable>，但<rich:extendedDataTable>支持某些扩展功能（见上面“主要功能”一节）。在这个组件中的数据是可滚动的。你也可以设置选择类型（none","single"或  "multi"）。多行选择可以使用Shift 和Ctrl键。
 
下面是一个例子：
 
...
<rich:extendedDataTable id="edt" value="#{extendedDT.dataModel}" var="edt" width="500px" height="500px" selectedClass="dataTableSelectedRow" sortMode="single" selectionMode="multi" selection="#{extendedDT.selection}" rowKeyVar="rkvar" tableState="#{extendedDT.tableState}">
 
       <rich:column id="id" headerClass="dataTableHeader" width="50" label="Id" sortable="true" sortBy="#{edt.id}" sortIconAscending="dataTableAscIcon" sortIconDescending="dataTableDescIcon">
 
              <f:facet name="header">
                     <h:outputText value="Id" />
              </f:facet>
              <h:outputText value="#{edt.id}" />
       </rich:column>
 
       <rich:column id="name" width="300" headerClass="dataTableHeader" label="Name" sortable="true" sortBy="#{edt.name}" sortIconAscending="dataTableAscIcon" sortIconDescending="dataTableDescIcon" filterBy="#{edt.name}" filterEvent="onkeyup" visible="false"> 
 
              <f:facet name="header"> 
                     <h:outputText value="Name" />
              </f:facet>
              <h:outputText value="#{edt.name}" />
       </rich:column>
 
       <rich:column id="date" width="100" headerClass="dataTableHeader" label="Date" sortable="true" comparator="#{extendedDT.dateComparator}" sortIconAscending="dataTableAscIcon" sortIconDescending="dataTableDescIcon">
 
              <f:facet name="header">
                     <h:outputText value="Date" />
              </f:facet>
              <h:outputText value="#{edt.date}"><f:convertDateTime pattern="yyyy-MM-dd HH:mm:ss" />
              </h:outputText>
       </rich:column>
 
       <rich:column id="group" width="50" headerClass="dataTableHeader" label="Group" sortable="true" sortBy="#{edt.group}" sortIconAscending="dataTableAscIcon" sortIconDescending="dataTableDescIcon">
 
              <f:facet name="header">
                     <h:outputText value="Group" />
              </f:facet>
              <h:outputText value="#{edt.group}" />
       </rich:column>
</rich:extendedDataTable>
...
   
图6.41.   使用了多行选择的<rich:extendedDataTable>组件
 
有关排序和过滤的信息，请看“RichFaces开发指南”排序一节。
 
对外部过滤器，<rich:extendedDataTable>组件支持<rich:column>的"filter"  facet。在这个facet中，你可以自己的过滤器，它会象内置过滤器一样被安置。过滤器的其他情况是相似于“RichFaces开发指南”过滤一节所描述。
 
在这个例子中，"selection"属性包含了一个使用了选择行的对象。
 
[注意，"height"属性是强制的，默认值为"500px"。]
 
在列头右边的菜单被用来执行动作，如排序、分组、隐藏列。
 
如下所示：
  
图6.42 列菜单
 
在选择了"Group by this column"选项后，你可以看见被分组合了。通过点击组头,你可以折叠或展开组。如下所示
  
图6.43.   使用了分组数据的<rich:extendedDataTable>组件
 
在<rich:column>中的"label"属性设置该列的名字，它用于拖动列时（在拖动窗口中）和在上下文菜单中，在"Columns"的子菜单中。例如：
 
...
<rich:column id="name" label="#{msg['name']}"
...
  
图6.44.  使用拖放列'Name'的<rich:extendedDataTable>组件
 
<rich:extendedDataTable>的列可以被隐藏：
 
图6.45. 隐藏了'Id' 和 'Group'的<rich:extendedDataTable>组件
 
"tableState"属性可以用来绑定表的状态（列宽、列的位置、可视的、顺序、分组等等）到后台bean的字符属性，为了以后使用。例如，状态可以被保存到数据库，而且不同于标准的JSF状态保存机制。
 
例子：
 
...
<rich:extendedDataTable tableState="#{extendedDT.tableState}">
...
 
6.6.12.4参数数据
 
<rich:extendedDataTable>属性表 [../../tlddoc/index.htmlrich/extendedDataTable.html]。
 
表6.59 组件关联的参数
名字	值
component-type	org.richfaces.ExtendedDataTable
component-class	org.richfaces.component.html.HtmlExtendedDataTable
component-family	org.richfaces.ExtendedDataTable
renderer-type	org.richfaces.ExtendedDataTableRenderer
tag-class	org.richfaces.taglib.ExtendedDataTableTag
 
表6.60 Facets
Facet	描述
header	重新定义表头内容
footer	重新定义表脚内容
caption 	重新定义标题内容
 
 
表 6.61使用了相应皮肤参数的样式类（selectors）
类名(selectors)	描述	皮肤参数	CSS属性映射
.extdt-empty-cell
 
 	为组件的空白单元定义样式	tableBorderWidth,tableBorderColor	border-bottom
.extdt-table-layout
 	为表的布局定义样式	tableBackgroundColor	background-color
.extdt-cell
 
 
 
 
 
 	为表单元定义样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
 
		generalSizeFont	font-size
		generalTextColor	Color
		generalFamilyFont	font-family
.extdt-header
 	为表头定义样式	headerBackgroundColor 	background-color
.extdt-header-continue
 
 
 	为第一个之后的所有表头行定义样式	headerBackgroundColor 	background-color
.extdt-headercell
 
 
 
 
 
 	为表头单元定义样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
		generalSizeFont	font-size
		headerTextColor	Color
		headerWeightFont	font-weight
		 
generalFamilyFont	font-family
.extdt-subheader
 	为子表头定义样式	additionalBackgroundColor 	background-color
.extdt-table-filterrow
 
 
 	为过滤行定义样式	additionalBackgroundColor 	background-color
 
		tableBorderWidth,
tableBorderColor	border-top
.extdt-subheadercell
 
 
 
 
 	为子表头单元定义样式	tableBorderWidth,tableBorderColor
generalSizeFont
generalTextColor
generalFamilyFont	border-right, border-bottom
font-size
color
font-family
.extdt-caption
 
 
 
 
 
 
 
 	为表的标题定义样式	tableBorderWidth,tableBorderColor	border-bottom
 
		generalSizeFont	font-size
		headerWeightFont	font-weight
		generalTextColor	Color
		generalFamilyFont	font-family
 
		additionalBackgroundColor	background-color
.extdt-footercell
 
 
 
 
 
 	为表脚单元定义样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
		generalSizeFont	font-size
		generalTextColor	Color
		headerWeightFont	font-weight
		generalFamilyFont	font-family
.extdt-subfootercell
 
 
 
 
 	为子表脚单元定义样式	tableBorderWidth,tableBorderColor	border-right, border-bottom
		generalSizeFont	font-size
		generalTextColor	Color
		generalFamilyFont	font-family
.extdt-row-selected
 	定义选择行的样式	additionalBackgroundColor 	background-color
.extdt-row-active	定义活动行的样式	tabDisabledTextColor 	Color
 
表 6.62无参数的样式类（selectors）
类名	描述
.rich-extdt	为所有表定义样式
.rich-extdt-caption	为"caption" facet元素定义样式
.rich-extdt-header	为表头行定义样式
.rich-extdt-header-continue	为在第一个之后的所有表头行定义样式
.rich-extdt-subheader	为列头定义样式
.rich-extdt-footer	为表脚行定义样式
.rich-extdt-footer-continue	为在第一个之后的所有表脚行定义样式
.rich-extdt-subfooter	为列脚定义样式
.rich-extdt-headercell	为表头单元定义样式
.rich-extdt-subheadercell	为列头单元定义样式
.rich-extdt-cell	为表单元定义样式
.rich-extdt-row	为表行单元定义样式
.rich-extdt-firstrow	为表开始行单元定义样式
.rich-extdt-footercell	为表脚单元定义样式
.rich-extdt-subfootercell	为列脚单元定义样式
.rich-extdt-group-cell	为分组件行单元定义样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.12.5相关联的资源链接
 
有关该组件用法的其他信息，请看[http://livedemo.exadel.com/richfaces-demo/richfaces/extendedDataTable.jsf?c=extendedDataTable]
 
6.6.13  < a4j:repeat >，从3.0.0版开始可用
 
6.6.13.1描述
 
<a4j:repeat>组件实现基本的迭代组件，它准放利用Ajax更新一组它的子女。
 
6.6.13.2使用细节
 
<a4j:repeat>组件相似于Facelets  <ui:repeat>标签，它被用来遍历与JSF页面以EL表达式绑定的对象集合。<a4j:repeat>的主要区别是可以更新局部组件（它的子女），而不是所有使用Ajax请求的。使得组件不同的功能是一特殊的"ajaxKeys"属性，它定义在一个Ajax请求之后被更新的行。所以，它可以轻松地分别更新几个子组件，而不用更新整个页面。例如：
 
...
<table>
      <tbody>
          
  <a4j:repeat value="#{repeatBean.items}" var="item" ajaxKeys="#{updateBean.updatedRow}">
                  <tr>
                        <td><h:outputText value="#{item.code}" id="item1" /></td>
                        <td><h:outputText value="#{item.price}" id="item2" /></td>
                  </tr>
            </a4j:repeat>
      </tbody>
</table>
 ...
 
上面的例子指向一个方法，它包含被更新的行键。
 
[注意，<a4j:repeat>被定义为整体更新，但是真正被更新的只是由"ajaxKeys"属性定义的行键。]
 
这个组件的另外一个好处是缺少严格定义的标记（markup），象JSF HTML DataTable和TOMAHAWK拥有的。因此，该组件可以更灵活地用在需要它的任何地方，输出从某些集体中选择的结果。
 
如果你希望以纯HTML列表输出，使用下面这样的结构：
 
...
<ul>
      <a4j:repeat ...>
        <li>...<li/>
                   ...
        <li>...<li/>
      </a4j:repeat>
</ul>
...
 
该组件的所有通用属性，根据迭代组件（<h:dataTable>或 <ui:repeat>）相似的属性被定义，并且以相同的方式使用。
 
6.6.13.3参数数据
 
<a4j:repeat>属性表[../../tlddoc/index.htmla4j/repeat.html]。
 
表6.63 组件关联的参数
名字	值
component-type	org.ajax4jsf.Repeat
component-family	javax.faces.Data
component-class	org.ajax4jsf.component.html.HtmlAjaxRepeat
renderer-type	org.ajax4jsf.components.RepeatRenderer
 
6.6.13.4相关联的资源链接
 
组件的用法和它们的资源的例子，请浏览在RichFaces Livedemo的Repeat页面： [http://livedemo.exadel.com/richfaces-demo/richfaces/repeat.jsf?c=repeat]
 
6.6.14  < rich:scrollableDataTable >，从3.0.0版开始可用
 
6.6.14.1描述
 
<rich:scrollableDataTable>用于类表组件的创建。该组件只是增加了在后面描述的与标准表比较的附加功能集。
   
图6.46  <rich:scrollableDataTable>组件
 
6.6.14.2主要功能
 
n         高定制观感
n         表单元的可变内容
n         当表上下滚动时，从服务器动态获取行。
n         通过鼠村拖动列栅调整大小
n         通过占击表头排序列
n         当表水平滚动时，固定一个或多个左边列。
n         一行或多行选择模式
n         内置拖放支持
n         排序列值
 
<rich:scrollableDataTable>包含下列属性，<rich:dataTable>没有包含的：
 
n         activeClass
n         activeRowKey
n         bypassUpdates
n         data
n         eventsQueue
n         frozenColCount
n         height
n         hideWhenScrolling
n         ignoreDupResponses
n         onselectionchange
n         requestDelay
n         scriptVar
n         selectedClass
n         selection
n         selectionMode
n         similarityGroupingId
n         sortOrder
n         status
n         timeout
 
<rich:scrollableDataTable>不包含下列属性，而<rich:dataTable>可用的：
 
n         align
n         bgcolor
n         border
n         captionClass
n         captionStyle
n         cellpadding
n         cellspacing
n         columns
n         columnsWidth
n         dir
n         frame
n         lang
n         onRowContextMenu
n         onRowMouseMove
n         onRowMouseOut
n         onRowMouseOver
n         onclick
n         ondblclick
n         onkeydown
n         onkeypress
n         onkeyup
n         onmousedown
n         onmousemove
n         onmouseout
n         onmouseover
n         onmouseup
n         rules
n         sortPriority
n         title
 
[使用<rich:column>。<rich:scrollableDataTable>不支持<rich:column>的相对宽度。然而，<rich:dataTable>和<rich:extendedDataTable>支持。]
 
6.6.14.3使用细节
 
该组件在页面上表示为一个可滚动表，带有一些固定（非滚动）的行（有行头和行脚）和列。象其他的表，<rich:scrollableDataTable>也有可选择的表头和表脚，它们可以使用相应的facets实现。表列可随意调整大小。可以通过拖放列的竖向边界调整大小。你可以使用"frozenColCount"属性定义距离左边的固定列的数目，它们在水平滚动时不会滚动。
 
你也可以使用"hideWhenScrolling"属性，增进组件的性能。如果属性值为"true"，在滚动时数据被隐藏。
 
也可以通过点击行选择整个行或某些行组。选择是可选的，并且这个功能的可用性是在组件上被定义。有两种方法选择几行：
 
n         只是依次点击列
n         按着SHIFT键点击某些行。在这种情况下，从开始到最后点击的所有行被选定。
 
是可以在表头上点击后排序表的内容。本功能是可选的（要禁用它，在   <rich:column>中使用"sortable"属性）。每个列应该指向一个比较方法，它用于表的排序。若<rich:scrollableDataTable>已按某些列被排序，并且该列头已被再次点击，则按反方向排序。
 
使用的典型变体：
 
...
<rich:scrollableDataTable value="#{modelBuilder.model}" var="issues"
            frozenColCount="1"
            first="0"
            rows="40" 
            width="300px"
            height="396px">
    <rich:column width="100px">
        <f:facet name="header" >
            <h:outputText value="State"/>
        </f:facet>
        <h:outputText value="#{issues.cell1}"/>
        <f:facet name="footer">
            <h:outputText value="State"/>
        </f:facet>
    </rich:column>      
    <!--Set of columns and header/footer facets-->
</rich:scrollableDataTable>
...
 
在使用一个或选择多行模式时，"selection"属性可被用来获得行的数据。
 
该属性是org.richfaces.model.selection.Selection[../../apidoc_framework/index.htmlorg/richfaces/model/selection/Selection.html]接口实例对象的一个引用，包含你当前选择的对象集合。
 
在下面的例子中，当你提交表单时，当前选择的对象的集合被放置到对象的属性中。然后，在动作完成时，带有选择数据的<rich:modalPanel>被显示。
 
例子：
 
...
<h:form>
        <rich:spacer height="30" />
                <rich:scrollableDataTable rowKeyVar="rkv" frozenColCount="1" height="200px" width="300px" id="carList" rows="40" columnClasses="col" value="#{dataTableScrollerBean.allCars}" var="category" sortMode="single" selection="#{dataTableScrollerBean.selection}">
                        <rich:column id="make">
                               <f:facet name="header"><h:outputText styleClass="headerText" value="Make" /></f:facet>
                               <h:outputText value="#{category.make}" />
                        </rich:column>
                        <rich:column id="model">
                               <f:facet name="header"><h:outputText styleClass="headerText" value="Model"  /></f:facet>
                              <h:outputText value="#{category.model}" />
                        </rich:column>
                        <rich:column id="price">
                              <f:facet name="header"><h:outputText styleClass="headerText" value="Price" /></f:facet>
                              <h:outputText value="#{category.price}" />
                        </rich:column>
                </rich:scrollableDataTable>
                <rich:spacer height="20px"/>
                <a4j:commandButton value="Show Current Selection" reRender="table" action="#{dataTableScrollerBean.takeSelection}" oncomplete="javascript:Richfaces.showModalPanel('panel');"/>
 
</h:form>
<rich:modalPanel id="panel" autosized="true">
        <f:facet name="header">
                <h:outputText value="Selected Rows"/>
        </f:facet>
        <f:facet name="controls">
                <span style="cursor:pointer" onclick="javascript:Richfaces.hideModalPanel('panel')">X</span>
        </f:facet>
        <rich:dataTable value="#{dataTableScrollerBean.selectedCars}" var="sel" id="table">
                <rich:column>
                        <f:facet name="header"><h:outputText value="Make" /></f:facet>
                        <h:outputText value="#{sel.make}" />
                </rich:column>
                <rich:column id="model">
                        <f:facet name="header"><h:outputText value="Model" /></f:facet>
                <h:outputText value="#{sel.model}" />
                </rich:column>
                <rich:column id="price">
                        <f:facet name="header"><h:outputText value="Price" /></f:facet>
                        <h:outputText value="#{sel.price}" />
                </rich:column>
        </rich:dataTable>
</rich:modalPanel>
...
 
结果为：
 
图6.47  "selection"属性的用法
 
在RichFaces LiveDemo页面：[http://wiki.jboss.org/wiki/RichFacesCookbook/ScrollableDataTableSelectionUsage]，你可以找到使用这个属性的完整例子，以及它的例子bean。
 http://community.jboss.org/wiki/RichFacesCookbookScrollableDataTableSelectionUsage
 
<rich:scrollableDataTable>组件拥有下面的额外属性，用于客户端的事件处理：
 
n         "onselectionchange"
n         "onRowClick"
n         "onRowDblClick"
n         "onRowMouseUp"
n         "onRowMouseDown"
 
从组件框架3.3.1开始，利用"selectionMode"属性可以切换选择模式。
 
有关排序和过滤的信息，请看“RichFaces开发指南”的排序一节。
 
有关"process"属性的使用信息，请看“决定处理什么”指南一节。
 
[注意，如果你希望使用特殊的功能，比如在数据库一级分页，你应该传递给<rich:scrollableDataTable>组件的"value"一个对象，这个类继承了org.richfaces.model.ScrollableTableDataModel。]
 
6.6.14.4参数数据
 
<rich:scrollableDataTable>属性表 [../../tlddoc/index.htmlrich/scrollableDataTable.html]
 
表6.64 组件关联的参数
名字	值
component-type	org.richfaces.component.ScrollableDataTable
component-class	org.richfaces.component.html.HtmlScrollableDataTable
component-family	org.richfaces.component.ScrollableDataTable
renderer-type	org.richfaces.renderkit.html.ScrollableDataTableRenderer
tag-class	org.richfaces.taglib.ScrollableDataTableTag
 
表6.65 Facets
Facet	描述
header	定义表头内容
footer	定义表脚内容
 
表 6.66使用了相应皮肤参数的样式类（selectors）
类名(selectors)	描述	皮肤参数	CSS属性映射
.rich-sdt
 
 
 	为组件外观定义样式
 
 	tableBackgroundColor	background-color
 
		tableBorderColor	border-color
		tableBorderWidth	border-width
.rich-std-header-row
 	为表头行定义样式	headerBackgroundColor 	background-color
 
.rich-sdt-header-cell
 
 
 
 
 
 
 
 	为表头行单元定义样式
 
 
 
 
 
 
 	tableBorderWidth
 
 	border-bottom-width,border-right-width
		tableBorderColor
 
 	border-bottom-color,border-right-color
		headerTextColor	Color
		generalFamilyFont	font-family
		generalSizeFont	font-size
.rich-sdt-hsplit	 	tipBorderColor	border-right-color
.rich-std-footer-row
 	为表脚行定义样式	tableSubfooterBackgroundColor 	background-color
.rich-sdt-footer-cell
 	为表脚行单元定义样式	tableBorderColor 	border-right-color
.rich-sdt-column-cel
 
 	为列单元定义样式
 	tableBorderColor	border-bottom-color,border-right-color
.rich-sdt-row-selected
 	为选择行定义样式	additionalBackgroundColor 	background-color
.rich-sdt-row-active
 	为活动行定义样式	tabDisabledTextColor 	color
.rich-sdt-header-cell-body, .rich-sdt-column-cell-body, .rich-sdt-footer-cell-body	为组件单元主体定义样式	generalFamilyFont	font-family
		generalSizeFont	font-size
 
表 6.67无参数的样式类（selectors）
类名	描述
.rich-sdt-hsep
.rich-sdt-column-sort-up
.rich-sdt-column-sort-down	为表头分隔符定义样式
为升序列定义样式
为降序列定义样式
 
在“定制样式类的定义”一节，你可以发现所有需要的有关样式类的信息。
 
6.6.14.5相关联的资源链接
 
<rich:scrollableDataTable>用法的例子，你可以查看组件LiveDemo页面：[http://livedemo.exadel.com/richfaces-demo/richfaces/scrollableDataTable.jsf?c=scrollableDataTable]。
 
Cookbook的“可滚动数据表的选择的用法”一文：[http://www.jboss.org/community/docs/DOC-11857]，提供了你如何使用"selection"属性在<rich:scrollableDataTable>中获得选择的行的例子。


