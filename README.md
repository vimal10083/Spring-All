# Spring Framework

All about Java spring framework with demo Projects. I hope my work will help you to improve your spring knowledge/concepts, Spring certification exam practice, crack an interview and find a good job.

<h2> List of Topics : </h2>

<ol>
  <li> Spring Core </li>
  <li> Spring MVC </li>
  <li> Spring Boot </li>
  <li> Spring AOP </li>
  <li> Spring Test </li>
  <li> Spring Data JPA </li>
  <li> Spring Rest </li>
  <li> Spring Security </li>
</ol>

<h3> Spring Framework Runtime </h3>

![](Runtime.PNG)

<h3> 1. Spring Core </h3>

<h4> What is the spring container?</h4>

Spring container is the core part of the spring framework. The container generally, Create the objects, wired them all together, configure them and manage their life cycle (creation to destroy)

<h4> Spring container configurations:</h4>

The most common ways to configure spring container are:

1. XML based configuration (old, famous & legacy way).
2. Java Annotations (the best and easy way)
3. Java Source code

<b> Development process is in simple steps </b>

1. Configure Spring beans
2. Create a Spring container
3. Retrieve beans from spring containers

<h4> XML based configuration </h4>

Step-01: Configure Spring beans

Create test.xml

```
<beans>
	 <bean id="demo" class="org.catmanscode.Test"></bean>
</beans>
```

Step-02: Create a Spring container (It is also known as ApplicatonContext)

Spring container/application contet can be create on multiple ways

1. ClassPathXmlApplicationContext
2. AnnotationConfigApplicationContext
3. GenericWebApplicationContext

Step-03: Retrieve beans from spring containers

![](SpringBeans.png)

[Spring-Ioc-Xml-Configuration-Demo-One : Demo Project](https://github.com/catMansCodes/Spring-All/tree/master/03_SpringCore/Spring-Ioc-Xml-Configuration-Demo-One)

<h4> What is spring beans?</h4>

Spring beans simply a nothing but java object.
When Java objects created by spring container it is known as spring beans. 
In simple terms, Java objects are the spring beans.

<b>Note:</b> Spring beans and java beans are not the same because springs beans/objects maintained by container. 

<h4> Spring container functionality: </h4>

1. Create and manage spring objects (inversion of controls - IOC)
2. Inject object's dependencies (Dependency injection - DI)

The most common way of Dependency injections are :

1. Constructor injection
2. Setter Injection

<h4> Constructor injection </h4>

* Define the dependency interface and class
* Create a constructor in class for injection
* Configure the dependency injection in the spring config file

[Spring-Ioc-Xml-Config-DI-Constructor-Injection : Demo Project](https://github.com/catMansCodes/Spring-All/tree/master/03_SpringCore/Spring-Ioc-Xml-Config-DI-Constructor-Injection) 

<h5> What is purpose of no-arg constructor? </h5> 

When you don’t define any constructor in your class, compiler defines default one for you, however when you declare any constructor (in your example you have already defined a parameterized constructor), compiler doesn’t do it for you.

Since you have defined a constructor in class code, compiler didn’t create default one. While creating object you are invoking default one, which doesn’t exist in class code. Then the code gives an compilation error.


<h4> Setter injection </h4>

* Define the dependency interface and class
* Create a setter method in class for injection
* Configure the dependency injection in the spring config file

[Spring-Ioc-Xml-Config-DI-Setter-Injection : Demo Project](https://github.com/catMansCodes/Spring-All/tree/master/03_SpringCore/Spring-Ioc-Xml-Config-DI-Setter-Injection)

If you want to get some literal values using setter injection, It is quite simple as setter injection.
We just need to set values in our xml file.i.e

* Same as above example, Add 2 private parameters/string called animalType and animalName.

```
private String animalType;

private String animalName;

//generate getters and setter

```

* Now to inject above parameters, Add a property for the same.

```
<beans>
	 <bean id="demo" class="fully qualified name of package">
	 	
		<property name="animalName" value="nini" />
		<property name="animalType" value="Cat" />
	 </bean>
</beans>
```

* Next, Get property values on MyApp.Java i.e

```
	AnimalServiceImpl myAnimalServiceImpl = context.getBean("animalService",AnimalServiceImpl.class);
		
	System.out.println(myAnimalServiceImpl.getAnimalType());
	System.out.println(myAnimalServiceImpl.getAnimalName());

```

[Spring-Ioc-Xml-Config-DI-Setter-Values-Injection : Demo Project](https://github.com/catMansCodes/Spring-All/tree/master/03_SpringCore/Spring-Ioc-Xml-Config-Setter-Values-Injection)

If we want to get/read data from an external file or say properties file. it is possible in a simple way. We just need to create a new file and Add this file on XML configuration.

1. Create application.properties

```
animal.animaltype = cat
animal.animalname = nini
```
2. Add file path/class path in xml file and get values.

```
	<context:property-placeholder location="classpath:application.properties"/>

	<bean id="animalService" class="org.catmanscodes.service.AnimalServiceImpl">
		<property name="animalDao" ref="animalDao1"></property>
		
		<property name="animalName" value="${animal.animalname}" />
		<property name="animalType" value="${animal.animaltype}" />
		
	</bean>

```

Note: Make sure you are using proper version of XML schema, otherwise it may not work.

[Spring-Ioc-Xml-Config-Setter-Values-from-property-file : Demo Project](https://github.com/catMansCodes/Spring-All/tree/master/03_SpringCore/Spring-Ioc-Xml-Config-Setter-Values-from-property-file)

<h4> Bean Scopes: </h4>
- Scope refers to the life cycle of a bean.
- It defines how long bean lives, how many instances will create and store in memory, How they shared in the environment.

There is a main 5 type of scope.
1. Singleton: It is default one If we don't define a scope spring is use it. Only one instance is created and shared in singleton.
2. Prototype: It creates a new instance for each request.
3. Request: It is part of HTTP web request and uses in web applications.
4. Session: It is also part of the HTTP session and uses in web applications only.
5. Global-session: Same as Session, We can use global session based on the requirement.

<h4> Singleton VS Prototype </h4>

```
<!--by default scope="singleton" -->
	<bean id="myAnimal" class="org.catmanscodes.main.service.AnimalServiceImpl" />

```
Or define scope manually.

```
<!-- Manually defined scope="singleton" -->
 <bean id="myAnimal" class="org.catmanscodes.main.service.AnimalServiceImpl" scope="singleton"/>

```
```
<!-- scope="prototype" -->
	 <bean id="myAnimal" class="org.catmanscodes.main.service.AnimalServiceImpl" scope="prototype"/>
```

![](Scope.png)

[Spring-Ioc-Xml-Config-Bean-Scopes : Demo Project](https://github.com/catMansCodes/Spring-All/tree/master/03_SpringCore/Spring-Ioc-Xml-Config-Bean-Scopes)
