# Maven

[TOC]

## Maven基础操作：

### Maven是什么

> * 一个项目管理工具
> * 由项目对象模型（POM），依赖管理，构建生命周期/阶段（为此做了许多插件）构成
> * <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210720214154454.png" alt="image-20210720214154454" style="zoom: 50%;" />
> * 作用：
>   * 项目构建（可以跨平台）
>   * 依赖管理（管理资源（jar包），避免产品冲突）
>   * 规定了统一的开发结构
> * POM：
>   * 把一个项目当成对象来看

------



### Maven基础概念

* #### 仓库：

  * 用于存储资源，包含各种jar包
  * 远程仓库：
    * 中央仓库：maven来管理维护，开源的
    * 私服仓库
  * 本地仓库

* #### 坐标：

  * Maven用于描述仓库中资源的位置，让maven来找资源的

  * 组成：

    * groupId：组织名（域名）
    * artifactId：项目名（模块名）
    * version：项目版本号

  * 寻找方式：

    * 打开网站直接搜

    * ```http
      mvnrepository.com
      ```

------



### 创建Maven项目

* #### src同层目录下创建一个xml文件

  * ~~随便找一个最少的复制就行~~

  * 格式：

    * 包含两部分
      * 自己的文件配置
      * 用到的依赖

    * ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <project
              xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xmlns="http://maven.apache.org/POM/4.0.0">
          <modelVersion>4.0.0</modelVersion>
      
          <!--自己文件的配置   -->
          <groupId>com.hflqf</groupId>
          <artifactId>project-java</artifactId>
          <version>1.0</version>
          
           <!--打包方式   -->
          <packaging>jar</packaging>
      
          <!--依赖   -->
          <dependencies>
              <dependency>
                  <!--要用到的项目资源   -->
                  <groupId>junit</groupId>
                  <artifactId>junit</artifactId>
                  <version>4.12</version>
              </dependency>
          </dependencies>
      
      </project>
      ```

* #### maven工程目录结构

  <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210721021230484.png" alt="image-20210721021230484" style="zoom:50%;" />

* #### cmd里的项目构建命令

  ```css
  mvn compile     //编译
  mvn clean       //清理，删掉编译的东西
  mvn test        //测试
  mvn package     //打包，打包前会编译和测试
  mvn install     //安装到本地仓库，根据立得xml文件的配置来安装到相应目录，安装前会打包
  ```

------



### 创建Maven项目步骤（IDEA版）

* #### 前期准备

  * 下载maven

  * 调整`settings.xml`的配置：

    *  配置本地仓库的路径

      ```xml
       <!-- localRepository
         | The path to the local repository maven will use to store artifacts.
         |
         | Default: ${user.home}/.m2/repository
        <localRepository>/path/to/local/repo</localRepository>
        -->
        <localRepository>D:\Maven\repository</localRepository>
      ```

    * 配置中央仓库的镜像（ 有删改）

      ```xml
      <mirrors>
      	<mirror>
      	<!--  此镜像的唯一标识符，用来区分不同的mirror元素  -->
            <id>nexus-aliyun</id>
      	  <!--  对哪个仓库进行镜像  -->
            <mirrorOf>central</mirrorOf>
            <name>Nexus aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
          </mirror>
        </mirrors>
      ```

* #### IDEA里创建maven项目

  * 在一个新建项目中，先配置好maven的本地版本，本地仓库路径，本地maven的`conf/settings.xml`文件

  * 新建模块，点击maven选项，配置<groupId>， <artifactId>和  <version>（让IDEA帮忙自动生成`pom.xml`文件）

  * 继续配置模块的名字和路径

  * 标记源代码的根目录，资源目录等

  * 添加测试jar包

    * 直接在`pom.xml`文件里面加入需要用到的依赖以及属性（指定jdk）

      ```xml
        <!--依赖   -->
          <dependencies>
              <dependency>
                  <!--要用到的项目资源   -->
                  <groupId>junit</groupId>
                  <artifactId>junit</artifactId>
                  <version>4.12</version>
              </dependency>
          </dependencies>
                  <!--要用到的jdk版本属性   -->
          <properties>
              <maven.compiler.source>15</maven.compiler.source>
              <maven.compiler.target>15</maven.compiler.target>
          </properties>
      ```

    * 做完记得刷新

* #### 快捷Java生成项目

  * 在一个新建项目中，先配置好maven的本地版本，本地仓库路径，本地maven的`conf/settings.xml`文件
  * 新建模块，用参考骨架
    * `maven-archetype-quickstart`
  * 自动创建时没有配好resources，包也没标注（根目录等）
  * 也需要自己更改`pom.xml`的`jdk`属性等

* #### 快捷Web生成项目

  * 在一个新建项目中，先配置好maven的本地版本，本地仓库路径，本地maven的`conf/settings.xml`文件

  * 新建模块，用参考骨架

    * `maven-archetype-webapp`

  * 自动创建时很多东西没有配好）

  * 也需要自己更改`pom.xml`的`jdk`属性等

  * <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210721024801142.png" alt="image-20210721024801142" style="zoom:75%;" />

  * 之后要配置`tomcat 7`的插件

    * 一个能够运行网页的插件

    * 上`mvnrepository.com`直接搜索

    * `pom.xml`里面配置插件:

      ```xml
      <!--构建-->
          <build>
              <!--配置插件-->
              <plugins>
                  <plugin> 
                      <groupId>org.apache.tomcat.maven</groupId>
                      <artifactId>tomcat7-maven-plugin</artifactId>
                      <version>2.1</version>
                    <!--  配置端口，网址之类-->
                      <configuration>
                        <!--  端口-->
                          <port>80</port>
                         <!-- 虚拟路径-->
                          <path>/</path>
                      </configuration>
                  </plugin>
              </plugins>
          </build>
      ```

  * 完成

------



### 依赖管理

* #### 格式：

  ```xml
  <dependencies>
          <dependency>
              <!--要用到的项目的坐标   -->
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.12</version>
          </dependency>
               <!--可以添加多个依赖   -->
               <!--依赖也可以是其他的资源，写入那三个东西即可   -->
             <dependency></dependency>
      </dependencies>
  ```

* #### 依赖传递

  * ###### 直接依赖

  * ###### 间接依赖

    <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210721173108741.png" alt="image-20210721173108741" style="zoom:50%;" />

* #### 依赖传递冲突

  * **路径优先：**层级越深，优先级越低
  * **声明优先：**资源在相同层级时，配置顺序靠前的覆盖配置顺序靠后的
  * **特殊优先：**同级配置相同资源的不同版本，后配置的覆盖先配置的

* #### 可选依赖

  * 对外隐藏使用过何种依赖，不透明
  * **被依赖者**写上true即可

  ```xml
   <dependency>
              <groupId>log4j</groupId>
              <artifactId>log4j</artifactId>
              <version>1.2.14</version>
              
             <!-- 依赖隐藏-->
              <optional>true</optional>
          </dependency>
  ```

  

* #### 排除依赖

  * **依赖者**主动断开间接依赖资源
  * 不需添加版本号

  ```xml
  <!-- 加入web01-->
          <dependency>
              <groupId>com.hflqf</groupId>
              <artifactId>web01</artifactId>
              <version>1.0-SNAPSHOT</version>
              
              <!--  排除依赖,不需要版本号-->
              <exclusions>
                  <exclusion>
                      <groupId>log4j</groupId>
                      <artifactId>log4j</artifactId>
                  </exclusion>
              </exclusions>
          </dependency>
  ```

* #### 依赖范围

  * 在依赖中通过scope来限定范围

    ```xml
                <!--依赖范围-->
                <scope>provided</scope>
    ```

    * compile
    * test
    * provided
    * runtime

  * <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210721182542933.png" alt="image-20210721182542933" style="zoom:80%;" />

  * ##### 依赖范围的传递

  <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210721182422160.png" alt="image-20210721182422160" style="zoom:80%;" />

------



### 生命周期与插件

* 插件是配合生命周期过程的

* 可以去官网下载和查看各种生命周期过程和功能的插件

  * `https://maven.apache.org/`

* 在`pom.xml`里使用插件

* ```xml
   <build>
          <plugins>
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-source-plugin</artifactId>
                  <version>3.2.0</version>
                  <!--执行-->
                  <executions>
                      <execution>
                          <!-- 要干什么-->
                          <goals>
                              <goal>jar</goal>
                          </goals>
                          <!--进行的阶段-->
                          <phase>generate-test-resources</phase>
                      </execution>
                  </executions>
              </plugin>
          </plugins>
      </build>
  ```

------



## Maven进阶：

### 分模块拆分与设计

* 只选取和这个模块相关的资源，其他无关的全部删掉（配置文件也要部分截取）
* 复制文件的一些操作
  * 新建含有Maven工程的模块之后直接复制过来，连同包一起
  * 然后开始删除不要的内容（包括部分的配置文件）
* 模块之间的依赖
  * 先写在`pom.xml`里
  * 然后被依赖的资源要先 install 在本地仓库
* -* 通配符的使用
  * 配置文件拆分时，要改名
  * 一般改成`xxx-xxx.xml`
  * 这样当服务器端需要使用拆分前配置文件的资源时，只需将源代码修改成`xxx-*.xml`即可

------



### 聚合

* 起到一个统筹管理各模块的作用，可以统一编译，测试，打包等，解决被依赖者更新但依赖者未知的情况

* 新开一个**只**有`pom.xml`的含有Maven工程的模块

* 修改`pom.xml`

  * 修改打包方式（`pom`）

  * 设置模块参数

    ```xml
     <packaging>pom</packaging>
    
        <modules>
            <module>../java01</module>
            <module>../java02</module>
            <module>../web01</module>
        </modules>
    ```

  * 关于打包方式：

    * 默认打包方式是jar
    * Java源代码是jar
    * Web是war
    * pom是用于聚合的

------



### 继承

* 起到统一版本的作用，父模块先定义好子模块要用到的插件和依赖等，子模块也要写出相应插件和依赖，只是不需要写版本了

* 父模块:

  * 修改打包方式（`pom`），一般和聚合一起构成一个模块
  * 设置要统一管理的插件和依赖

  ```xml
      <dependencyManagement>
          <dependencies>
              <dependency>
                  <groupId>junit</groupId>
                  <artifactId>junit</artifactId>
                  <version>4.12</version>
                  <scope>test</scope>
              </dependency>
  
              <dependency>
                  <groupId>log4j</groupId>
                  <artifactId>log4j</artifactId>
                  <version>1.2.14</version>
              </dependency>
          </dependencies>
      </dependencyManagement>
  ```

* 子模块：

  * 写出继承的父类，和父类的相对路径

  * 子类的坐标的`groupId`和`version`就可以省略

  * ```xml
        <parent>
            <groupId>com.hflqf</groupId>
            <artifactId>java00</artifactId>
            <version>1.0-SNAPSHOT</version>
            <relativePath>../java00/pom.xml</relativePath>
        </parent>
    ```

  * 子类需要使用的插件和依赖的`version`也可以省略

  * ```xml
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </dependency>
    ```

------



### 属性

* **属性有五种**

  * 自定义属性
    * 主要是这个运用较多
  * 内置属性
    * Maven 里关键字 `version`是当前版本号的定义好的变量，直接使用`${version}`即可
  * Settings属性
    * 使用`conf/settings.xml`里的标签属性，如`${settings.localRepository}`
  * Java属性
    * 读取Java系统属性
  * 环境变量属性

* **系统里属性查询方式：**

  * `mvn help：system`
  * 可查取Java和环境变量的属性

* **Maven里的变量，自定义在properties里**

  ```xml
  <properties>
      <log4j.version>1.2.14</log4j.version>
      <junit.version>4.12</junit.version>
  </properties>
  ```

* **用的时候直接`${xxxx}`即可**

* ```xml
  <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>${log4j.version}</version>
  </dependency>
  ```

------



### 版本管理

* **RELEASE**
  * 发布版
* **SNAPSHOT**
  * 快照版
* 一般来说子模块可以不继承父模块的版本号，可以有自己独立的版本号

------



### 资源配置

* 在管理的`pom.xml`的properties里定义一些变量（一般是URI,用户名之类的），使得旗下的所有模块都可以选择性使用

* 在build里添加要如此替换的目录和过滤

* **在父类里：**

  ```xml
      <properties>
          <username>201830168</username>
      </properties>
  ```

  ```xml
      <build>
          <resources>
              <resource>
                  <directory>${project.basedir}/src/main/resources</directory>
                  <filtering>true</filtering>
              </resource>
          </resources>
  
          <testResources>
              <testResource>
                  <directory>${project.basedir}/sre/test/resources</directory>
                     <filtering>true</filtering>
              </testResource>
          </testResources>
      </build>
  ```

* 这里使用通配符`${project.basedir}`来表示旗下所有模块都如此改动，连`../`都不需要

* **在子类里：**把要统一调配的变量使用属性的写法即可

  ```xml
  ${username}
  ```

------



### 多环境配置

* 个性化配置属性值

* 把属性的变量根据环境的不同（开发环境，生产环境等），设置为不同的值

* 在`profiles`里设置不同环境不同的值，并且可以设置是否默认操作

  ```xml
      <!-- 多环境配置-->
      <profiles>
          <profile>          <!--每一个环境-->
              <id>pro_env</id>
              <properties>
                  <username>201830168</username>
              </properties>
              <!--设为默认启动-->
              <activation>
                  <activeByDefault>true</activeByDefault>
              </activation>
          </profile>
  
          <profile>          <!--每一个环境-->
              <id>dev_env</id>
              <properties>
                  <username>201830168@smail.nju.edu.cn</username>
              </properties>
          </profile>
      </profiles>
  ```

* 设置默认就不需要设置参数了

* 在执行`install`操作时设置参数

  <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210722231010277.png" alt="image-20210722231010277" style="zoom:60%;" />

* 或者dos指令：

  * `mvn 指令 -P 环境定义id`

------



### 跳过测试

* **有三种方式：**

  1. IDEA中Maven管理栏中点击闪电的图标，可跳过任意生命周期过程

     <img src="C:\Users\18933\AppData\Roaming\Typora\typora-user-images\image-20210723000348490.png" alt="image-20210723000348490" style="zoom:50%;" />

  2. 使用dos指令

     `mvn 指令 -D skipTests`

  3. 在父模块的`pom.xml`中`pluginManagement`中对插件做属性修改

     ```xml
                     <plugin>
                         <!--下面这句话可以不用写-->              
                         <groupId>org.apache.maven.plugins</groupId>
                         
                         <artifactId>maven-surfire-plugin</artifactId>
                         <version>2.22.1</version>
                         <configuration>
                             <!--跳过测试-->
                             <skipTests>true</skipTests>
                             <!--指定测试-->
                             <includes>
                                 <include>**/De*Test.java</include>
                             </includes>
                             <!--排除指定测试-->
                             <excludes>
                                 <exclude>**/De*TestCase.java</exclude>
                             </excludes>
                         </configuration>
                     </plugin>
     ```

* `**/ De*Test.java`又是一个通配符

------



### 私服

* **可以用Nexus（要下载）**(好像南大的那个有？)
  * 启动：（命令行启动）
    * `nexus.exe /run nexus`
  * 访问服务器：（默认端口号8081）
    * `http://localhost:8081`
  * 修改基础信息
    * 安装路径下etc目录下中`nexus-default.properties`文件中修改
  * 修改服务器配置信息
    * 安装路径下bin目录下中`nexus.vmoptions`文件中修改
* 不想学了，需要的时候再搞了，先扔下URL
  * [黑马程序员Maven全套教程，Maven项目管理从基础到高级，Java项目开发必会管理工具Maven_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ah411S7ZE?p=27&spm_id_from=pageDriver)