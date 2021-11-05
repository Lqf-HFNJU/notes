# spring boot

[TOC]

## 基本入门

### 作用：简化spring开发

* 不需要配太多配置文件
* 不需要纠结maven的依赖
* 嵌入式服务器，不需要tomcat

### 特点：

* 不需要太多的无意义的重复的代码
* 打的是jar包，由一个主函数入口启动工程
* 注解开发
* 基于约定，约定大于配置



------

### 快速搭建springboot工程

* #### maven方式：

  * ##### 先构建一个maven工程

  * ##### 修改pom.xml文件

    * 打的是jar包

    * 继承一个父工程
    * 引入几个依赖
    * 插件可要可不要

    * ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
          <modelVersion>4.0.0</modelVersion>
          <parent>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-parent</artifactId>
              <version>2.5.4</version>
              <relativePath/> <!-- lookup parent from repository -->
          </parent>        <!--引入父工程-->
          <groupId>com.hflqf</groupId>
          <artifactId>helloworld</artifactId>
          <version>0.0.1-SNAPSHOT</version>
          <packaging>jar</packaging>
      
          <properties>
              <java.version>11</java.version>
          </properties>
          <dependencies>
              <dependency> <!--引入web的依赖-->
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
              </dependency>
              <dependency> <!--tomcat的依赖-->
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-tomcat</artifactId>
                  <scope>provided</scope>
              </dependency>
              <dependency> <!--测试类的依赖-->
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-test</artifactId>
                  <scope>test</scope>
              </dependency>
          </dependencies>
      
          <build>              <!--插件可要可不要-->
              <plugins>
                  <plugin>
                      <groupId>org.springframework.boot</groupId>
                      <artifactId>spring-boot-maven-plugin</artifactId>
                  </plugin>
              </plugins>
          </build>
      
      </project>
      ```

  * ##### 写一个引导类作为工程的开启入口

    * 写法比较固定

    * `@SpringBootApplication`其实就是一个配置类，可以自定义Bean

    * ```java
      package com.hflqf;
      
      import org.springframework.boot.SpringApplication;
      import org.springframework.boot.autoconfigure.SpringBootApplication;
      
      @SpringBootApplication
      public class HelloApplication {
          public static void main(String[] args) {
              SpringApplication.run(HelloApplication.class, args);
          }
      }
      
      ```

  * ##### 剩下的就开始写Controller了

    * 这一步好像就和spring的步骤差不多了

    * emm似乎要写上几个注解

    * ###### ssm我现在也没学，暂时还不知道是怎么回事...(2021.8)

      * ###### 现在我会了 我学过了hhh（2021.10）

    * `@RestController`相当于`@RequestBody`+`@Controller`

    * ```java
      package com.hflqf.controller;
      
      import org.springframework.web.bind.annotation.RequestMapping;
      import org.springframework.web.bind.annotation.RestController;
      
      @RestController
      public class HelloController {
      
          @RequestMapping("/hello")
          public String hello() {
              return "hello spring boot!";
        }
      }
      
      ```

      

* ### spring工程直接构建方式：

  * 无脑按着图形化界面点就行了
  * 点完全部内容就都配置好了



------

### 两种配置方式

#### 名字必须叫application，后缀名可以是properties或者yml/yaml

* #### application.properties

  * 这种的就是properties文件，和之前的一样

* #### application.yml

  * yaml格式，一种便于阅读和更加注重数据的格式

  * 后缀名可以是yml和yaml

  * 两种数据类型

    * 内置数据类型：可以被自动识别
    * 自定义数据类型：需要手动去读取

  * 三种数据格式

    * 对象
    * 数组
    * 纯量

  * 允许参数引用

  * ```yml
    #大小写敏感
    #数据值前边必须有空格符，至少一个
    #使用缩进表示层级关系
    #缩进时不允许使用tab 只允许使用空格
    #缩进的空格数不重要，只要相同层级的元素左侧对齐即可
    #使用空格缩进表示层级关系，相同缩进表示同一级
    ##########################################################################
    
    #数据格式
    #对象（map）：键值对的集合
    person:
      name: zhangsan
      age: 19
      
    #行内写法
    person2: {name: lqf,age: 18}
    
    #数组：一组按次序排列的值
    address:
      - beijing
      - shanghai
    
    #行内写法
    address2: [beijing,shanghai]
    
    #纯量：单个的，不可再分的值
    #idea下面会显示出不同
    msg1: 'hello \n world'  #单引号忽略转义字符
    msg2: "hello \n world"  #双引号识别转义字符
    
    ##########################################################################
    
    #参数引用
    name: lqf
    person3: ${name}
    ```

* #### 三种方式的优先级顺序：

  * properties>yml>yaml

### 三种读取配置注入的方式

* #### 必须是application.properties或者application.xml才可以默认读取

* #### @Value

  * 直接在需要赋值的地方加上一个注解
  * 获取yml里的相应的属性

  * ```java
    package com.hflqf.springbootinit;
    
    import org.springframework.beans.factory.annotation.Value;
    import org.springframework.web.bind.annotation.RestController;
    
    @RestController
    public class ReadYml {
        /**
         * 方法一
         * 加上一个注解
         * 获取yml里面的 name属性
         */
    
        //属性注入
        @Value("${name}")
        private String thisName;
    
        //对象注入
        @Value("${person.name}")
        private String thisName2;
        @Value("${person.age}")
        private String age;
    
        //数组注入
        @Value("${address[0]}")
        private String address1;
    
        @Value("${msg1}")
        private String msg1;
    }
    
    ```

    

* #### Environment

  *  新建一个`Environment`类型的对象，再在这个对象上加上 `@Autowired`注解

  * yml所有的自定义内容都会封装到这个对象里，直接调用即可

  * 一般来说自定义的内容较多，则使用这种方法

  * ```java
    package com.hflqf.springbootinit;
    
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.core.env.Environment;
    import org.springframework.web.bind.annotation.RestController;
    
    @RestController
    public class ReadYml {
        /**
         * 方法二
         * 环境变量，加上注解就能用
         */
        @Autowired
        private Environment env;
        
        //直接调用
        private String name = env.getProperty("person.age");
    
    }
    ```

    

* #### @ConfigurationProperties

  *  在bean加上一个`@Component`注解，使得被spring识别是一个bean

  * 再加上`@ConfigurationProperties(prefix = "xxx")`注解，直接注入配置文件的内容，前缀表示指定属性

  * 变量名字保持一致就能一一注入了

  * ```java
    package com.hflqf.springbootinit;
    
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.context.properties.ConfigurationProperties;
    import org.springframework.stereotype.Component;
    import org.springframework.web.bind.annotation.RestController;
    
    @RestController
    public class ReadYml {
    	/**
    	  * 方法三
    	  * 配合一个类来使用
    	*/
        @Autowired
        private Person person;
    }
    
    /**
     * 对象和配置属性的绑定
     */
    @Component//被spring识别是一个bean
    @ConfigurationProperties(prefix = "person")//直接注入配置文件的内容,前缀表示指定属性，一一注入
    class Person {
    
        private String name;
        private int age;
    
        public String getName() {return name;}
        public void setName(String name) {this.name = name;}
        public int getAge() {return age;}
        public void setAge(int age) {this.age = age;}
    
        @Override
        public String toString() {return "Person{" +"name=" + name + ", age=" + age +'}';}
    }
    ```

  * 在pom.xml文件加上一个依赖可以获得自动提示功能

  * ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-configuration-processor</artifactId>
    </dependency>
    ```



------

### profile

* #### 作用：完成不同环境下，配置动态切换的功能

* #### 配置方式：

  * ##### 多profile文件方式：写多个配置文件，每个代表一种环境

    * ###### 前缀名要保持一致，后缀名是唯一的标识符

      * application-dev.properties/yml 开发环境
      * application-test.properties/yml 测试环境
      * application-pro.properties/yml 生产环境

  * yml多文档方式：

    * 在yml中使用 `---` 来分割不同的配置

    * 每一段加上如下属性来指定不同配置的名称（现在已经过时？）

      ```yml
      spring:
        profiles: dev
        
      #spring.profiles已经弃用 换成spring.config.active.on-profile  
      ```

* #### 激活方式：

  * ##### 配置文件：

    * 在配置文件中配置
      * `spring.profiles.active=xxx`

  * ##### IDEA中配置虚拟机参数:

    * 打开`Run/Debug Configurations`
  
  * 在`VM options` 指定：
  
* `-Dspring.profiles.active=xxx`
  
* ##### 命令行参数：
  
    * 打成jar包后命用令行执行
    
    * `java -jar xxx.jar --spring.profiles.active=xxx`



------

### 内部配置文件的加载顺序

 1. ##### 当前项目（工程）下的/config目录下

    * `../config/`

 2. ##### 当前项目（工程）的根目录下

    * `../`

	3. ##### classpath的/config目录下

    * 其实也就是resources下的config目录
    * `classpath:/config/`
    * `resources/config/`

	4. ##### classpath的根目录下

    * 其实也就是resources下的根目录
    * `classpath:/`
    * `resources/`

* ##### 加载顺序是上面的排列顺序，高优先级配置的属性会生效

* ##### 通过命令行打开jar文件时不会加载，因为前两种方式的配置文件`不会`打入jar包中



------

### 外部配置文件的加载顺序

* ##### 去看官网的配置文档

* ##### 可以在控制台指定配置文件的读取：

  * 通过`--spring.config.location=xxx`

* ##### 配置文件如果放在/target/下，（和jar包同级）处，可以自动加载

* ##### 放在/target/config下，（比jar包小一级），也可以自动加载

  * 优先级比放在/target/要高

------



## 整合其他框架

### 整合Junit

* 测试类头加上`@SpringBootTest(classes = xxx.class)`
  * xxx是启动主函数所在的类名
  * 如果测试类所在的包名和源代码所在的包名是一致的，这个`classes`也不用写了
* `@RunWith`什么的也不用了
* 直接`@Autowired`啥的照常写就可以了

------



### 整合redis

* ##### 配置/勾选redis的依赖

* ##### 配置redis相关属性

  * 连接本地的都不需要配
  * 在`application.yml`里面配`spring.redis`就行了

* ##### 注入RedisTemplate模板

  * 在`private RedisTemplate rt`上面加上注解
  * 这里不能`@Autowired`自动注入，因为有两个模板
  * `@Qualifier("redisTemplate")`即可

* 搞定了

------



### 整合MyBatis

* ##### 配置/勾选mybatis的依赖，添加mysql驱动

* ##### 配置DataSource和MyBatis相关配置

  * 在`application.yml`里面配`spring.datasource`
* 驱动用`com.mysql.cj.jdbc.Driver`
    
* 可能要配上时区
    
* ##### 写dao和mapper文件/纯注解开发

  * ###### 注解开发：

    * mapper上加上`@Mapper`注解，不需要加上`@Repository`
    
  * ###### mapper文件开发：

    * 照常写映射文件
    * 在`application.yml`里面配置mybatis
      * mybatis核心文件中有大部分内容可以直接配在`application.yml`里面

* 搞定了



------

## 原理分析

### 自动配置

* #### Condition

  * ##### 根据指定条件判断是否创建该Bean

  * 在配置的实体类的创建Bean的方法上加上`@Conditional(ClassCondition.class)`

    * 需要传入一个`Condition`的实现类 重写`matches`方法 如果返回`true` 那么会帮忙创建，`false`则不会
    * `Condition`的实现类里面的`matches`方法有两个参数：
      * context:  上下文对象 用于获取属性值 类加载器 BeanFactory之类
      * metadata: 元数据对象 用于获取注解的属性

  * springboot已经提供好常用的条件注解:
    * `@ConditionOnProperty`:  判断配置文件中是否有对应的属性和值才初始化Bean
    * `@ConditionOnClass`:  判断环境中是否有对应的字节码文件
    * `@ConditionOnMissingBean`:  判断环境中没有对应Bean

* #### 切换内置服务器

  * ##### 原理仍然是`Condition`条件配置

  * 只需要在`Maven`里排除tomcat的依赖，引入相应服务器的依赖就行了

* #### @Enable*注解

  * ##### springboot工程不能直接获取其他工程定义的Bean

    * 原因：`@SpringBootApplication`的`@ComponentScan`没有将其他工程的Bean添加进组件扫描
    * `@ComponentScan` 扫描范围：当前引导类所在包及其子包
      * 这也是为什么把service那些写在其他包下就无法扫描的原因
      * 解决方案：
        * 1. 使用 `@ComponentScan(包名)`把配置类所在的包扫描一下   成功扫描的原因是导入了相应jar包
          2. 使用 `@import(类名.class)` 来加载一些类 被这个注解导入的类都会被自动创建入容器
          3. 对`@Import`注解进行封装
             * 由第三方提供该封装，使用时只需`@Enablexxx`就行了
             * `@Enablexxx`是第三方提供好的封装`@Import`的注解

  * ##### @Enable*注解是用于动态开启某些功能的，底层原理就是使用@Import注解导入一些配置类，实现Bean的动态加载

* #### @Import注解

  * ##### 使用@Import导入的类会被Spring加载到IOC容器里

  * ##### @Import有四种用法：

    1. 直接导入Bean
    2. 导入配置类
       * 配置类里所有定义的Bean都能注入
       * 配置类的`@Configuration`都不需要添加了
    3. 导入ImportSelector实现类
       * 一般用于加载配置文件中的类
    4. 导入ImportBeanDefinitionRegistrar实现类

* #### 自动配置原理

  * ##### 核心注解是`@SpringBootApplication`的`@EnableAutoConfiguration`

  * ##### 该注解内部使用@Import(AutoConfigurationImportSelector.class)来加载类

  * 所有需要加载的类全在META-INF/spirng.factories 里定义，springboot启动时，会自动加载这些配置类，初始化Bean

  * 并不是所有的Bean都会被初始化，在配置类中使用Condition来加载满足条件的Bean

* #### 自动配置的手动实现

  * 自己写好一个`xxxAutoConfiguration`类，里面提供一些创建Bean的方法

    * 或许需要一个和配置文件相操作的类

  * 然后在resources下创建一个META-INF/spring.factories

    * 里面写上：

      ```properties
      org.springframework.boot.autoconfigure.EnableAutoConfiguration=自己写的配置类的全包名
      ```

  * 这样就可以实现第三方的自动配置了

------

### 监听机制

* ##### 在项目启动时，会对几个监听器进行回调，只需实现这些监听器接口，在项目启动时完成一些操作

* ##### 继承实现了java的监听类

  * ###### ApplicationContextInitializer

    * 要在META-INF/spring.factories里配置才能生效

      * ```properties
        org.springframework.context.ApplicationContextInitializer=${自己实现的全包名}
        ```

    * 用于在ioc容器准备之前检测资源是否存在

  * ###### SpringApplicationRunListener

    * 要在META-INF/spring.fatories里配置才能生效
      * 配置方法同上
    * 对生命周期的监听

  * ###### CommandLineRunner

    * 直接放入IOC容器里（加上`@Component`）就能自动执行
    * 项目启动后会执行重写的Run方法
    * 一般用于预热缓存

  * ###### ApplicationRunner

    * 直接放入IOC容器里（加上`@Component`）就能自动执行
    * 和上面的那个几乎完全一样，只是重写的方法的参数名不一样



------

### 启动流程

* ##### 人直接听傻 学不动了

  * [黑马程序员SpringBoot教程，6小时快速入门Java微服务架构Spring Boot_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Lq4y1J77x?p=29)

* 



------

## 监控

* #### 自带监控插件Actuator，可以实现对程序内部运行情况的监控 Bean加载状况

  * 如配置属性，日志信息等
  * 导入jar包即可无脑使用

* #### 图形化界面的监控

  * 开源的社区项目Spring Boot Admin
  * 具有两个角色：客户端(client)和服务端(server)
    * server:
      * 创建server模块
      * 引入坐标admin-stater-server
      * 引导类上加上监控功能@EnableAdminServer
    * client:
      * 创建client模块
      * 引入坐标admin-stater-client
      * 配置相关信息：server地址等

------

## 项目部署

* #### 两种打包方式

  * jar(官方推荐)

  * war

    * 可以放在外部的服务器里去运行,不使用内置的tomcat服务器

    * 需要在引导类里继承`SpringBootServletInitializer`

    * 重写`configure`方法

    * ```java
      @SpringBootApplication
      public class SpringbootListenerApplication extends SpringBootServletInitializer {
      
          public static void main(String[] args) {
              SpringApplication.run(SpringbootDeployApplication.class, args);
          }
      
          @Override
          protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
              return builder.sources(SpringbootDeployApplication.class);
          }
      }
      ```

* 直接将jar/war包发送去相应服务器即可

