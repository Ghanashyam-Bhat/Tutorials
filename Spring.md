# Spring Tutorial

 |Spring| Spring MVC| Hibernate |
 | :--| :--| :-- |
 | [YouTube](https://www.youtube.com/watch?v=If1Lw4pLLEo&ab_channel=Telusko)|[YouTube](https://www.youtube.com/watch?v=g2b-NbR48Jo&list=PLOEG1MmaatwcG3oPNxP-Pu_yCsB6d4FjX&index=13&ab_channel=Telusko) | [YouTube](https://www.youtube.com/watch?v=2IibiNUjuHo&ab_channel=LearnCodeWithDurgesh)|
 |  | [Doc](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html) |[Doc](https://tutorialspedia.com/spring-mvc-step-by-step-tutorial-with-hibernate-mysql-jsp-using-java-configurations/) | 

---

## Introduction to Maven

### Gives thrid party libraries for java for development of applications. In this case we use the dependencies for Spring.

### To get dependencies go to spring.io [Maven Repository](https://mvnrepository.com/) and search for the framework name. When using this dependencies for the first time all the jar files gets downloaded to local repository. Therefore we don't need internet to access the dependencies.

### An alternative for maven is gradle, which can be used for getting all the dependencies.

### We can either create a project using Eclipse IDE or we can use [website](https://start.spring.io/) to add maven dependencies.

### Once we create the project we need to add spring dependencies into the pom.xml file from [here](https://www.baeldung.com/spring-with-maven).

<br/>

## Spring Framework to achieve dependency injection

### We can inject the class from outside instead of using new keyword to create the object. This is beacause  will increase the dependencies.
- ### xml based configuration. 
- ### Annotation based confguration
- ### Java configuration

### In xml based configuration we use applicationContext and getBean method to inject the class from outside using xml files by linking the class name to the bean tag in the xml file

### In annotation based configuration  we need to mention the object as *@Component*, then we can directly use the class name (in lowercase) to access it using getBean method without explicitly defining bean tag

### **Note**: We need to typecast while using getBean method

### **Setter Injection** :  Inorder to initialize a class variable using bean tag, we use property tag inside beans tag. This property tag works like a setter method to initialize a vaiable.

### **Contructor injection** : Instead of using Setter property we can directly use constructor to initialize the class variable using xml file using \<constructor-arg> tag.

### **Autowired Annotation** : For combining xml based config and annotation based config we use *@Autowired* annotation. While using xml config element as a property for annotation config class if we make the property as Autowired, it will look into xml and file and initialize it accordingly. This also works when both are annotation config.

<br/>

### **Configuration Bean**:
### Instead of xml file, we use configuration class inorder to create the objects using annotation based configuration. 
### Inorder to make a class as configuration class, we need to use *@Configuration* annotation and also mention the class name in the new ConfigurationAnnotationApplicationContext() of type AnnotationContext.
### For each method of *@Configuration* class, we need to annotate as *@Bean*
### We can use *@Autowired* annotatoin before creating a class variable inorder to make it initialize by itself based on the methods present in the configuration file. The *@Autowired* will map the variable with the method with same return type in the configuration file.

### We can actually remove the methods inside the configuration file which returns *new* object and still make the system work.
### **Annotation Component - *AutoWired primary qualifier*** :
### Inorder to make a class *@bean* by default, before the class defination add *@component* annotation and in the configuration file, after *@Configuration* annotation add *@ComponentScan(basePackeges="\<package name>")*
### We can also change the component name (by defualt it will be same as class name in lowercase) by giving the component name as *@Component("\<name>")*
### **Spring Core Annotations**
### WKT the return type is checked when we use *@AutoWired* annotation. If same interface is implemented by multiple classes there will be an error due to conflict. To solve this after making a class as *@Component* we need to make it as *@Primary*. In case of conflict, primary component will be considered.
### Or we can also use *@Qualifier("\<component name>")* annoration after *@AutoWired*  inorder to specify which component to autowire.
<br/>


# Spring MVC
### Create new project with web framework for maven and add spring dependecies in the file inorder to download the jar files.
<br>

### Since we are working on web application we need to link the app with webserver. 
### Properties > Targeted Runtime > New > Select the server > Download and Install 
<br>
 
### Run index.jsp file by right clicking and the selecting 
### Run As > Run on Server
<br>
 
### We can also change the browser in which we display page by 
### window > Browser > Default Browser
<br>
 
### Never add java code into index.jsp page. Always create survelets and call them

 ### index.jsp
 
    <html>
    <body>
    <!-- Here 'add' is the survelet which is called on clicking the submit button -->
    <form action="add"> 
        <input type="text" name="t1"><br>
        <input type="text" name="t2"><br>
        <input type="submit">
    </form>
    </body>
    </html>
<br>

### In an MVC application there can be multiple controllers which handle the requests. These multiple controllers are inturn controlled by Front-Controller. 
### This front controller is called dispatcher survelt. We need to configure this in **web.xml** file
### We can get the dependencies from [here](https://www.dropbox.com/s/8dbsipjnl33xizq/cheetSheetSpring%20.rtf?dl=0&save_as=true&save_as_action=PDF)

<br/>

### In **web.xml** add these under <web-app> tag
####   '/' in <url-pattern> means every request is being redireccted to dispatcher survelet
#### This Dispatcher Survlet is a pert of Spring MVC. So we need to add it's dependencies in the *pom.xml* file
    <servlet>
		<servlet-name>telusko</servlet-name>
		<servlet-class>
			org.springframework.web.servlet.DispatcherServlet
		</servlet-class>
	</servlet>
	<servlet-mapping>
		<servlet-name>telusko</servlet-name>
        <url-pattern>/</url-pattern> 
	</servlet-mapping>

<br/>

### In **Maven dependency (pom.xml)** add the following
    <dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>4.1.8.RELEASE</version>
		</dependency>

		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>4.1.8.RELEASE</version>
		</dependency>
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.36</version>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>

<br/>

### In **telusko-servlet.xml** add the following
#### The filename should be \<name>-sevlet.xml
#### The \<name> depends on the survlet name 
#### **Don't forget to edit the package name**. We are also enbling annotation based configuration here.

    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:ctx="http://www.springframework.org/schema/context"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:mvc="http://www.springframework.org/schema/mvc"
        xsi:schemaLocation="http://www.springframework.org/schema/beans 
        http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-2.5.xsd ">
        
        
        <ctx:annotation-config></ctx:annotation-config>
        <ctx:component-scan base-package="<package-name-here>"></ctx:component-scan>
    </beans>

<br/>


### Now create a class 'add' which is being called by the .jsp file with the help of survlet make it *@Controller*
### In this class we also need to mention which type of request we are handling. To do this we use *@RequestMapping("/add")* annotation and also mention the route which handles the request (This should be mentioned inside the class for the method which needs to be called).

<br/>

### Now inorder to create other web pages, create a jsp file inside *webapp* folder. Then return the webpage in the method.

<br/>


	@Controller
	public class AddController
	{
		@RequestMapping("/add)
		//Change the return type from string to ModelAndView
		public ModelAndView add(HttpServletRequest request, HttpServletRequest response )
		{
			//To get the data from the request
			int i = Integer.parseInt(request.getParameter("t1));
			int j = Integer.parseInt(request.getParameter("t2));
			int k = i+j;

			//Inorder to pass the data we need to use ModelAndView object

			mv.setViewName("display.jsp);
			//We need to create a object with an label and data
			mv.addObject("result",k);

			//System.out.println("I am here);
			//return "display.jsp" //This is just to return static page
			//Inorder to return dynamic page, we need to return ModelAndView obeject
			return mv;
		}
	}



### Now in the HTML page / jsp page, inorder to return the result we need to use the following expression
### <% request.getAttribute("\<label-name>") %>

<br/>


### **Spring MVC Expression Language**
### Instead of request.getAttribute we can use Expression Language. This can be done by using **${\<label-name>}**
### Inorder to enable EL, we need to add isELIgnored="false" after pageEncoding option in the .jsp file. (Sometimes EL will not work if we are using lower version)

<br/>

### In actual application we should not do any functionality inside the Controller class. All the functionality should be handled by the service class and controller should only act as the medium for communication between service class and the view.

### Use **Control+Space** or **control+Shift+O** to import the packages for user defined packages

<br/>

### Till now we have been using xml file as configuration file for dispatcher survlet. With Survlet version greater than 3.0, we can use annotation configuration which is using a class to act as configuration file instead of xml file 
### The config class looks like this

	@Configuration
	@ComponentScan({"com.telusko"})
	public class TeluskoConfig
	{

	}

### Now the code will work even without the telusko-servlet.xml file

<br/>

### Now to replace web.xml file with class based configuration file we need to create a class myWeb which extends AbstractionAnnotationConfigDispatcherSurvletInitializer

	public class MyWebInitializer extends AbstractionAnnotationConfigDispatcherSurvletInitializer{

		@Override
		protected Class <?>[] getRootConfigClasses(){
			//TODO 
			return null;
		}

		@Override
		protected Class <?>[] getServletConfigClasses(){
			//TODO
			return new Class[] {TeluskoConfig.class};
			//Returning class array with configuration class names. In this case we are returning only 1 config class
		}

		@Override
		protected String[] getServeletMapping(){
			//TODO
			return new String[] {"/"} //This means 
		}
	}

<br/>

### While returning the webpage from the controller class, we should avoid mentioning the file extension. To do this we need to use **internal view resolver** to search for the view.
### To do this, make this modification to Configuratio file (TeluskoConfig.java)

	@Configuration
	@ComponentScan({"com.telusko"})
	public class TeluskoConfig
	{
		@Bean
		public InternalResourceResolver viewResolver(){
			
			InternalResourceResolver vr = new InternalResourceResolver();
			var.setPrefix("/WEB-INF/"); //This is the folder in which the view files are created
			vr.setSuffix(".jsp"); //This is the file extension

			return vr;
		}
		
	}

### Now in the class which returns the view file, we just have to mention the file name without the extension.

<br/>

### **Spring MVC Annotation RequestParam**
### When we submit the form, we can see that in the URL we are passing the request parameters. 
### Till now we were using *HttpServletRequest request* object in the *@Controller* class to fetch these parameters and then perform the operations. We can avoid this using RequestParam annotation.

	@Controller
	public class AddController
	{
		@RequestMapping("/add)
		//Change the return type from string to ModelAndView
		public ModelAndView add(@RequestParam("t1") int i, @RequestParam("t2") int j)
		{
			int k = i+j;

			//Inorder to pass the data we need to use ModelAndView object

			mv.setViewName("display.jsp);
			//We need to create a object with an label and data
			mv.addObject("result",k);

			//System.out.println("I am here);
			//return "display.jsp" //This is just to return static page
			//Inorder to return dynamic page, we need to return ModelAndView obeject
			return mv;
		}
	}

 <br/> <br/>
 
 ---

 ## We have seen xml based. Now we look into **Java based configuration**.

<br/>

### **Note 1:** Sometimes java folder won't be created by default in the src/main/. In such cases we need to create java folder overselves.

### **Note 2:** Sometimes everything will be in default package. We need to change it to user defined package. Example: com.telusko

### For java configuration we create **DispatcherSurvlet** just like we do in Annotation based configuration by extending AbstractionAnnotationConfigDispatcherSurvletInitializer.

	public class MyWebInitializer extends AbstractionAnnotationConfigDispatcherSurvletInitializer{

		@Override
		protected Class <?>[] getRootConfigClasses(){
			//TODO 
			return new Class[] {MvcConfig.class};
		}

		@Override
		protected Class <?>[] getServletConfigClasses(){
			//TODO
			return null;
		}

		@Override
		protected String[] getServeletMapping(){
			//TODO
			return new String[] {"/"} //This means 
		}
	}

### Then instead of a normal configuration class like annotation configuration we create MvcConfig.class
### When we do this we don't have to specify all the beans manually.

	@Configuration
	@EnableWebMvc
	@ComponentScan("com.telusko")
	public class MvcConfig extends WebMvcConfigurationAdapter
	{
		
	}

<br/> <br/>

# Connection of Hibernate with spring MVC
## Hibernate is the framework used to store data in the database (SQL database)

<br/>

### **Note** : Use the same version of dependencies as of the spring version we are using!

### Now add hibernate dependencies in pom.xml from [here](https://mvnrepository.com/artifact/org.hibernate/hibernate-core)

	<!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-core -->
	<dependency>
		<groupId>org.hibernate</groupId>
		<artifactId>hibernate-core</artifactId>
		<version>6.1.7.Final</version>
		<type>pom</type>
	</dependency>

### Add Spring ORM dependencies from [here](https://mvnrepository.com/artifact/org.springframework/spring-orm)

	<!-- https://mvnrepository.com/artifact/org.springframework/spring-orm -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-orm</artifactId>
		<version>4.3.13.RELEASE</version>
	</dependency>

### Now we need mySQLConnector dependecies. Add that from [here](https://mvnrepository.com/artifact/mysql/mysql-connector-java)

	<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
	<dependency>
		<groupId>mysql</groupId>
		<artifactId>mysql-connector-java</artifactId>
		<version>5.1.49</version>
	</dependency>

### Now update the dependencies by Right Click on project > Maven > Update project > Ok

<br/>

### For performing database operations we need to create methods to get data, save data, update data and delete data
### These methods use hibernet functionalities. Hence these classes need to use **HibernetTemplate**
### This HibernateTemplate provides the session functionality.
### We need to inject these functions of HibernetTemplate into our class using spring dependency injection
### This HibernetTemplate inturn uses SessionFactory. Since Session factory is just an interface, we use teh class that implements session factory, which is **LocalSessionFactoryBean**.
### **LocalSessionFactoryBean** takes DataSource as parameter inorder to interact with database.
### DataSource interface is implemented by **DriverManagerDataSource** class which actually interacts with the database.

<br/>

### We need to configure \<servlet-name>-servlet.xml file to connect with the database using xml based configuration

	<bean id="ViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix" value="/WEB-INF/pages/" />
		<property name="suffix" value=".jsp" /> 
	</bean>

	<bean class="org.springframework.jdbc.datasource.DriverManagerDataSource" name="dataSource">
		<property name="driverClassName" value="com.mysql.jdbc.Driver" />
		<property name="url" value="jdbc:mysql://localhost:3306/todomanager" />
		<property  name="username" value="root" />
		<property  name="password" value="root" />
	</bean>

### Inorder to get the package name, Control+Shift+T then search for the package > Goto the class > In the top of the code we can find the package name
### Also get the class name from the same file
### Then mention \<package-name>.\<class-name> for the class section

### Here we have mentioned the name of the bean class as **dataSource**. Whenever we need to use this class, we need to refer to it as **dataSource**.

<br/>

### Now we need to configure the session too. This class will use the above dataSource class which we have created.


#### Since we are using annotated class for model, we need to give list inside the property called annotatedClasses


	<bean class="org.springframework.orm.hibernate5.LocalSessionFactoryBean" name="sessionFactory">
		<property name="dataSource" ref="dataSource" />
		
		<property name="hibernateProperties">
			<props key="hibernate.dialect">org.hibernate.dialect.MySQL57Dialect</props>
			<props key="hibernate.hbm2ddl.auto">true</props>
			<props key="hibernate.show_sql>true</props>
		</property>

		<property name="annotatedClasses">
			<list>
				<value>
					com.entities.Todo
				</value> 
			</list>
		</property>
		
	</bean>

### Now to create a class which acts as model


### Note: We can create multiple packages inside the project and all the classes inside the package can be interrelated.
### New package should be used for creating classes surving completely different purpose.

<br/>

### Now We create hibernate template and pass the localsessionbfactorybean we have created above

