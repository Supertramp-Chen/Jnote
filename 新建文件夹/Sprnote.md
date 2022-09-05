# 1、Spring.





## 1.1、概述



Spring理念：

​	使得现有技术更加容易使用，本身是个大杂烩，整合了现有的技术框架



框架：

​	相当于简历的模板，可以套过来，直接在上面填东西就可以用了



maven地址，导入包，maven会把其他依赖的包下载下来

```java
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>

```



## 1.2、优点



Spring是个开源的免费的框架（容器）



Spring是个轻量级（本身很小，把包下载下来就能用）、非入侵的框架（引入Spring不会改变原来代码的情况，不会对原来项目产生影响，然而用了它可能会更加简单）



控制反转IOC，面向切面编程AOP



支持事务的处理（因为AOP的原因），对框架整合的支持（几乎面向所有的java框架都能整合进去）





## 1.3、总结



Spring是个轻量级的，控制反转和面向切面的框架



## 1.4、组成



## 1.5、扩展



现代java开发 即基于Spring的开发



your app --- spring boot(build anything) -- spring cloud(coordinate anything) -- spring cloud date flow(connect everything)



Spring Boot:

​	一个快速开发的脚手架（和框架一样，用了spring boot后 只需要进行一些简单的配置既可开发出一个网站）

​	基于spring boot可以快速开发单个微服务

​	约定大于配置（学起来更轻松）



Spring Cloud：

​	Spring Cloud 基于Spring boot实现（构建之后才能协调）



大多数公司使用spring boot进行快速开发，而学习spring boot前提是完全掌握spring和spring mvc



弊端：

​	发展太久，违背原来的理念，大杂烩杂的太多 配置十分繁琐 “配置地狱” 到spring boot即可解放



# 2、IOC理论推导（一种思想）





（maven导入jar包）



UserDao接口

UserDaoImpl实现类

UserService 业务接口

UserSserviceImpl 业务实现类



组合的概念



程序是死的，但是用户可以根据不同的条件变成不同的样子



程序的架构也不需要改变



控制反转，写出来的程序放在谁那都能跑 而且可以自己去定义



在之前的业务中，用户的需求会影响原来的代码，需要过呢根据用户的需求去修改原代码，吴国陈旭代码十分大，修改依次的成本十分昂贵



使用一个set接口实现，使发送革命性的变化

```java
 private UserDao userDao;

    //利用set进行动态实现值的注入
    public void setUserDao(UserDao userDao){
        this.userDao = userDao;
    }
```



之前 程序是主动创建对象，控制权在程序员手上



使用set注入后，程序不再具有主动性，而是变成了被动的接受对象



这种思想，从本质上解决了问题，程序员不需要再去管理对象的创建了



系统耦合性大大降低，可以更加专注再业务的实现上

这是IOC的原型



由用户选择我要去调用哪种业务，本来主动权在业务层





## 2.1、IOC本质



IOC是一种设计思想，DI是实现IOC的一种方法



没有IOC的程序，使用面向对象编程，对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制

控制反转后将程序的创建转移给第三方

IOC，获得依赖对象的方式反转了



采用xml方式配置bean时，bean的定义信息和实现是分离的，采用注解方式可以把二者合二为一

bean的定义信息直接以注解的形式定义在实现类中，达到零配置的目的



IOC是一种通过描述（xmlor注解）并通过第三方去生产or获取特定对象的方式



Spring中实现控制反转的是IOC容器，实现方法是依赖注入（DI）













对象由Spring创建，对象的属性由Spring容器设置

原来需要主动new一个对象，现在只需要交给容器去做（给它配置一下即可），用的时候去容器里拿就行了，没有去new对象



传统的程序对象由程序本身创建（即new），用Spring后 对象由Spring创建



容器指的是beans



反转：程序本身不创建对象，变成被动的接收对象



依赖注入：本质是靠set方法 注入



IOC是一种编程思想，由主动的编程变成被动的接收



彻底不用再到程序中进行改动了，要实现不同的操作，只需要在xml配置文件中进行修改

IOC：对象由Spring来创建，管理，装配



# 3、HelloSpring



id 变量名

class 要new的对象

property 给对象里的属性注入值





# 4、IOC创建对象的all方式（IOC2）





 



​	java对象要能使用一定要经过new出来



创建对象，创建bean，bean和对象是一个东西



方式1 - 使用无参构造创建对象，默认！！！



方式2 - 若使用有参构造创建对象（多种方式）



第一种，下标赋值

```java
<!--第一种，下标赋值-->
    <bean id="user" class="com.chen.User">
        <constructor-arg index="0" value="我的名字"></constructor-arg>
    </bean>
```



第二种，类型

```java
 <!--第二种方式，通过类型创建，不建议使用，若两个地方都是String就不行-->
    <bean id="user" class="com.chen.User">
        <constructor-arg type="java.lang.String" value="王二"></constructor-arg>
    </bean>
```



第三种，直接通过参数名

```java
<!--第三种，直接通过参数名-->
    <!--
    <bean id="user" class="com.chen.User">
        <constructor-arg name="name" value="chenj"></constructor-arg>
    </bean>
    -->
```







在配置文件加载的时候，容器中管理的文件就已经初始化了

​	两个类（一个有参，一个无参）注册到bean里，在bean里用有参和无参分别创建对象

​	测试类中only getBean有参，另一个类的无参也会执行





```java
//spring容器
ApplicationContext context=new ClassPathXmlApplicationContext("beans.xml");//拿到容器后,get我们需要的bean即可
//在配置文件加载的时候，容器中管理的文件就已经初始化了
User user=(User) context.getBean("user");//getbean的时候对象已经被创建了
User user2=(User) context.getBean("user");
System.out.println(user==user2);//内存中只有一份实例，取的都是那一个
```





# 5、Spring配置



## 5.1、别名



可以多个名字

```xml
<bean id="user" class="com.chen.User">
        <constructor-arg name="name" value="chenj"></constructor-arg>
    </bean>

<!--别名，如果添加了别名，我们也可以用别名获取到这个对象，给对象起的另外一个名字-->
    <alias name="user" alias="usernew"></alias>
```



## 5.2、bean的配置



```xml
<!--bean的配置，通过name也可以取别名，空格逗号分号都可以间隔
    id：bean的唯一标识符，也就是相当于我们学的对象名
    class：bean对象所对应的全限制定名：包名+类名
    name：也是别名，且name可同时取多个别名
    -->
    <bean id="user" class="com.chen.User" name="user2 user3,user4">
    </bean>
```



## 5.3、import

 

import一般用于团队开发，它可以把多个配置文件合并为一个



beans只是代表一部分，全称是applicationContext，最后只通过applicationContext来做



如现在项目中有多个人开发，三个人负责不同的类开发，不同的类需注册在不同的bean中

我们可以利用import将all人的beans.xml合并为一个总的



```xml
<import resource="beans.xml"></import>
```

使用的时候使用总的即可







# 6、DI 依赖注入



## 6.1、构造器注入



前面已经介绍



## 6.2、 不同种类的set方式注入（重点）



依赖注入（本质是set注入）



​	依赖：bean对象的创建依赖于容器

​	注入：bean对象中的所有属性，由容器来注入



```java
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext();//CPX,ClassPath代表类路径下的xml
```





环境搭配：



​	复杂类型：

```java
public class Address {//引用对象
    private String address;
    public String getAddress() {
        return address;
    }
    public void setAddress(String address) {
        this.address = address;
    }

    @Override
    public String toString() {
        return "Address{" +
                "address='" + address + '\'' +
                '}';
    }
}
```

​	

​	真实测试对象：

```java
private String name;//通过value赋值
private Address address;//通过ref赋值
private String[] books;
private List<String> hobbys;
private Map<String,String> card;
private Set<String> games;
private String wife;
private Properties info;
```

​	

​	beans.xml :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="address" class="com.chen.Address">
        <property name="address" value="厦门"></property>
    </bean>
    <bean id="student" class="com.chen.Student">
        <!--第一种，普通值注入，使用value即可-->
        <property name="name" value="楚江东"></property>
        <!--第二种，bean注入，使用ref-->
        <!--因为是个引用类型 所以用ref-->
        <property name="address" ref="address"></property>
        <!--第三种，数组-->
        <property name="books">
            <array>
                <value>挪威的森林</value>
                <value>倾城之恋</value>
            </array>
        </property>
        <!--第四种，List-->
        <property name="hobbys">
            <list>
                <value>打游戏</value>
                <value>再打游戏</value>
                <value>还是打游戏</value>
            </list>
        </property>
        <!--第五种，Map-->
        <property name="card">
            <map>
                <entry key="身份证" value="326451"></entry>
                <entry key="银行卡号" value="24358642"></entry>
            </map>
        </property>
        <!--第六种，Set-->
        <property name="games">
            <set>
                <value>LOL</value>
                <value>CF</value>
                <value>CS</value>
            </set>
        </property>
        <!--第七种，String null-->
        <property name="wife">
            <null></null>
        </property>
        <!--第八种，Properties-->
        <property name="info">
            <props>
                <prop key="password">456</prop>
                <prop key="username">王二</prop>
            </props>
        </property>
    </bean>
</beans>
```



​	测试类：

```java
public class MyTest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");//CPX,ClassPath代表类路径下的xml
        Student student = (Student) context.getBean("student");
        System.out.println(student.toString());
    }
}
```





## 6.3、拓展方式注入



可以导入一些约束



可以使用p命名空间和c命名空间进行注入



注意：

​	p命名空间和c命名空间不能直接使用，需要导入xml约束

```xml
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
```





使用：



```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--p命名空间注入(对应set注入)，可直接注入属性的值，property，要先导入-->
    <bean id="user" class="com.chen.User" p:age="23" p:name="秦川"></bean>
    <!--c命名空间注入(对应构造器注入)，通过构造器注入，contruct-args，要先导入-->
    <bean id="user2" class="com.chen.User" c:age="42" c:name="楚江东"></bean>
</beans>
```





测试：



```java
@Test//导入junit jar包(在pom.xml中)
public void text2(){
    ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
    User user = (User) context.getBean("user2");
    System.out.println(user);
}
```



```xml
<dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
```





## 6.4、bean的作用域



1. 单例模式（Spring默认机制）（单线程）



```xml
<bean id="user2" class="com.chen.User" c:age="42" c:name="楚江东" scope="singleton"></bean>
```



```java
ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
User user = (User) context.getBean("user2");
User user2 = (User) context.getBean("user2");
System.out.println(user==user2);//true
```



只有一个bean的实例（all 共享）



2. 原型模式：(会浪费资源，多线程)

   每次从容器中get的时候，都会产生一个新对象

   每一个bean创建的都是单独的对象



```xml
<bean id="user2" class="com.chen.User" c:age="42" c:name="楚江东" scope="prototype"></bean>
```



```java
ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
User user = (User) context.getBean("user2");
User user2 = (User) context.getBean("user2");
System.out.println(user==user2);//false
```



其余的request、session、application 只能在web开发中使用到















明白spring是个容器的概念，可以把上面这些放在里面，并由此创造一些东西







# 7、bean的自动装配



自动装配是spring满足bean依赖的一种方式

spring会在上下文中自动寻找，并自动给bean装配属性



在spring中有三种装配的方式

	1. 在xml中显示的配置
	2. 在java中显示的配置
	3. 隐式的自动装配bean （重要）



## 7.1、测试



环境搭配：

​	一个人有两个宠物



## 7.2、byName自动装配



自动装配基于上下文

首先类里面要有，而后bean里面要进行注册



```xml
<bean id="cat" class="com.chen.pojo.Cat"></bean>
<bean id="dog" class="com.chen.pojo.Dog"></bean>
<!--
    byName:会自动在容器上下文中查找，和自己对象中set方法后面的值相对应的 beanid
-->
<bean id="person" class="com.chen.pojo.Person" autowire="byName">
    <property name="name" value="楚江东" ></property>
   	<!-- 
	 <property name="cat" ref="cat"></property>
    <property name="dog" ref="dog"></property>
	-->
 </bean>
```



## 7.3、 byTper自动装配



```xml
<bean id="cat" class="com.chen.pojo.Cat"></bean>
    <bean class="com.chen.pojo.Dog"></bean>
<!--    <bean id="dog22" class="com.chen.pojo.Dog"></bean>-->
    <!--
        byType:会自动在容器上下文中查找，和自己对象类型属性类型相同的bean（需保证类型全局唯一）,可以省略id，因为它是根据类型
    -->
    <bean id="person" class="com.chen.pojo.Person" autowire="byType">
        <property name="name" value="楚江东" ></property>
       <!-- <property name="cat" ref="cat"></property>
        <property name="dog" ref="dog"></property>-->
     </bean>
```





## 小结



byName的时候，需要保证所有bean的id唯一，且该bean id需要和自动注入的属性的set方法的值一样

byType的时候，需要保证所有bean的class唯一，且该bean class需要和自动注入的属性的类型一样



## 7.4、使用注解实现自动装配





导入约束：

​	context约束



配置注解的支持：

​	context:annotation-config/



```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```





@Autowired（通过byType方式实现）

 直接在属性上使用，也可在set方法上使用

使用@Autowired可以不用编写set方法，前提是自动装配的属性在IOC（spring）容器中存在，且符合名字byType





科普：



```
@Nullable 字段标记这个注解，说明这个字段可以为null
```



```java
public @interface Autowired{
	boolean required() default true;
}
```



测试代码：

```java
public class people{
	
	//如果显示定义Autowired的required属性为false，说明该属性可以为null，否则不允许为null
	@Autowired(required = false)
	private Cat cat;
	@Autowired
	private Dog dog;
}
```





如果@Autowired自动装配的环境比较复杂，自动装配无法通过一个注解（@Autowired）完成的时候

可以使用@Qualifier(value = "XX")去配置@Autowired的使用，指定一个唯一的bean对象注入



```java
 	@Autowired
    @Qualifier(value = "cat11")
    private Cat cat;
    @Autowired
    @Qualifier(value = "dog22")
    private Dog dog;
    private String name;

```



@Resource注解



```
public class People{
	@Resource(name = "cat2")
	private Cat cat;
	@Resource
	private Dog dog;
}
```



### 7.4.1、小结，@Autowired和@Resource的区别



都是用来自动装配，都可以放在属性字段上



@Autowired通过byType方式实现，且要求对象存在【常用】

@Resource默认通过byName实现，如果找不到名字则通过byType实现，两个都找不到则报错

执行顺序不同









# 8、使用注解开发



在Spring4之后要使用注解开发，必须保证 导入aop的包



使用注解需要导入context约束，增加注解的支持



```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```



## 8.1、bean





## 8.2、属性如何注入：



```java
//等价于    <bean id="user" class="com.chen.pojo"></bean> id默认小写user
@Component// 组建
public class User {
    /*//相当于      <property name="name" value="www"></property>
    @Value("wwww")*/
    public String name;
    public void show(){
        System.out.println("wwwwww");
    }

    //相当于      <property name="name" value="www"></property>
    @Value("wwww")
    public void setName(String name) {
        this.name = name;
    }
}
```





## 8.3、衍生的注解：



​	@Component 有几个衍生注解，在web开发中，会按照mvc三层架构分析

​		dao【@Repository】

​			（一般和Component一样 都代表会注册到spring里面 相当于一个bean，只是一般dao层的东西习惯用Repository标注）

​		service【@Service】

​			（同）

​		controller【@Controller】



​			这四个注解功能是一样的，都代表将某个类注册到spring中，装配Bean





## 8.4、自动装配：



```
- @Autowired
- @Nullable
- @Resource
```





## 8.5、作用域：



```java
//等价于    <bean id="user" class="com.chen.pojo"></bean> id默认小写user
@Component// 组建
@Scope("prototype")
public class User {
    /*//相当于      <property name="name" value="www"></property>
    @Value("wwww")*/
    public String name;
    public void show(){
        System.out.println("wwwwww");
    }

    //相当于      <property name="name" value="www"></property>
    @Value("wwww")
    public void setName(String name) {
        this.name = name;
    }
```



## 小结



xml与注解：

​	xml更加万能，适用于任何场合，维护简单方便

​	注解 不是自己的类使用不了，维护相对复杂



xml与注解最佳实践：

​	xml用来管理bean

​	注解只负责完成属性的注入

​	



​	在使用过程中只需注意一个问题：

​		必须让注解生效，就需要开启注解的支持

```xml
<!--    指定要扫描的包，这个包的注解就会生效，扫描一个指定的包-->
<context:component-scan base-package="com.chen"></context:component-scan>
<!--    只是注解驱动-->
<context:annotation-config/>
```





# 9、使用java方式配置spring



现在完全不使用spring的xml配置，全权交给java来做

javaConfig是spring的一个子项目，在spring4后 它成为了一个核心功能





实体类：

```java
@Component//该注解就是说明这个类被Spring接管了，注册到了容器中
public class User {
    private String name;

    public String getName() {
        return name;
    }
    @Value("WWW")//属性注入值
    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
```





配置文件：

```java
@Configuration//这个也会被spring容器托管，注册到容器中，因为它本身就是一个@Component
//@Configuration代表这是一个配置类，和我们之前看的beans.xml一样
@ComponentScan("com.chen.pojo")
@Import(ChenConfig2.class)
public class ChenConfig {//配置类
    //注册了一个bean 就相当于我们之前写的一个bean标签
    //这个方法的名字 相当于bean标签中的id属性
    //这个方法的返回值 相当于bean标签中的class属性
    @Bean
    public User getUser(){
        return new User();//就是返回要注入到bean的对象
    }
}
```





测试类：

```java
public class MyText {
    public static void main(String[] args) {
        //如果完全使用了配置类方式去做，就只能通过AnnotationConfig 上下文来获取对象，并通过配置类的class对象加载
        ApplicationContext context = new AnnotationConfigApplicationContext(ChenConfig.class);
        User user = (User) context.getBean("user");
        System.out.println(user.toString());
    }
}
```





这种纯java的配置方式在springboot中随处可见