# ORM工具比较  
----
## 传 统 的 JDBC  
相关工具：Dbutits（QueryRunner），jdbcTemplate

**传统JDBC的操作流程**

![传统jdbc的操作流程](pic\hibernate操作流程.png)

功能简单；SQL语句编写在Java代码中；硬编码高耦合的方式不利于维护  

## Hibernate操作  

全自动映射ORM框架，旨在相除对SQL的学习；提供了自定义SQL的模块HQL。  

![hibernate操作数据库的流程](pic\hibernate操作流程.png)  

**期望**：SQL语句由开发人员编写，以不失去灵活性  

## Mybatis操作  

​	半自动，轻量级框架，将SQL由开发人员编写，编写在xml配置文件中，实现SQL与Java代码的分离。  

![Mybatis操作数据库](pic\mybatis操作流程.png)

## 为什么使用Mybatis  

![](F:\学习\学习笔记\Java\尚硅谷Mybatis\pic\为什么使用Mybatis.png)

# Mybatis的历史  

![](pic\mybatis的历史.png)

# 使用Mybatis

项目引入 *mybatis* 和 *mysql-connector-java* 的jar包  

----
## old方式

1. 创建 *mybatis-config.xml* 配置文件，该文件在项目中为 *全局配置文件*   

   ```xml
   <configuration>
       <environments default="development">
           <environment id="development">
               <transactionManager type="JDBC"/>
               <dataSource type="POOLED">
                   <property name="driver" value="jdbc驱动"/>
                   <property name="url" value="数据库连接的url"/>
                   <property name="username" value="用户名"/>
                   <property name="password" value="密码"/>
               </dataSource>
           </environment>
       </environments>
   </configuration>
   ```

2. 根据 *mybatis-config.xml*  获取一个SqlSessionFactory对象  

   ```java
   String resource = "mybatis-config.xml的路径";
   InputStream inputStream = Resources.getResourceAsStream(resource);
   SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
   ```

3. 打开一个SqlSession对象，用于执行SQL语句

   ```java
   SqlSession sqlSession=sqlSessionFactory.openSession();
   ```

   SqlSession对象使用结束后，需要进行关闭

   ```java
   sqlSession.close();
   ```

4. 对于数据库中的每一张实体表和各实体的class类，配置一个专门的映射文件（*类名Mapper.xml*），该文件用于配置该表**CRUD**的SQL语句，实现表记录到对象的映射。

   ```xml
   <mapper namespace="qf.mybatis.study">
       <select id="selectEmp" resultType="tb.bean.Employee">
           select * from tb_employee where id = #{id}
       </select>
   </mapper>
   ```

   每个mapper文件有一个唯一的 **namespace**（命名空间），而其中的每个SQL语句有一个唯一的 **id**，“**namespace.id**"的形式就构成一个SQL语句的唯一标识。

   **resultType** 指明将查询结果封装成指定的类对象。

5. 在 *mybatis-config.xml* 中添加 mapper文件的资源，保证SQLSession可以使用mapper的SQl语句。

   ```xml
   <mappers>
       <mapper resource="mapper文件的路径"/>
   </mappers>
   ```

6. 使用SQLSession对象，指定mapper文件配置的SQL语句的id执行一条SQl语句  

   ```java
   Employee emp=sqlSession.selectOne("qf.mybatis.study.selectEmp",args);
   ```
**selectOne** 第一个参数为SQL语句的唯一标识，第二个参数为需要传入的参数值

## new方式

使用SQL映射接口的方式执行SQL语句，将SQL语句转化为java的方法，约束参数的类型，方便方法调用。

1. 针对每一个 *maper.xml* 文件，添加一个同名的接口，为其中每一条SQL语句定制一个方法

2. 将该mapper接口的完整类名作为 *mapper.xml* 的名称空间，将方法名作为对应SQL语句的id值

3. 调用 **SqlSession** 对象的 *getMapper(Class)* 方法获取一个mapper接口的代理实现类对象

   ```java
   EmployeeMapper mapper=sqlSession.getMapper(EmployeeMapper.class);
   Employee emp=mapper.getEmpById(2);
   ```

4. 调用mapper接口代理实现类对象的方法执行数据库操作

## 注意

SQLSession是一个非线程安全的类，因而不适宜作为成员变量，而是在每次需要时再获取对象。

----
## Mybatis的两个dtd约束
mybatis-config.xml： http://mybatis.org/dtd/mybatis-3-config.dtd
mapper.xml：http://mybatis.org/dtd/mybatis-3-mapper.dtd
这两个dtd文件位于 `org.apache.ibatis.builder.xml `  包中

----
# 全局配置文件 mybatis-config.xml
### properties 标签
用于引用外部 *.properties* 配置文件，通常在 *.properties* 文件中配置数据库连接的配置信息。包括 *url* 和 *resource* 两个属性。
* url：引用网络上的配置文件
* resource：引用项目（本地）的配置文件

引用配置文件后，可用 ** ${参数名称}** 的形式获取配置文件中的数据，如：
```xml
 <dataSource>
    <property name="driver" value="${driver}"/>
    <property name="url" value="${url}"/>
    <property name="username" value="${username}"/>
    <property name="password" value="${password}"/>
  </dataSource>
```
### settings 标签
控制mybatis框架的各种设置项，通过其子标签为setting来设置各种设置项。
#### setting 标签
一个setting标签就代表mybatis框架的一个设置项，它包括 *name* 和v *alue* 两个属性。
* name：设置项的名称
* value：设置项的值

settings的设置项非常多，多数的值（value）为true或false的类型。
#### mapUnderscoreToCamelCase 映射下划线和驼峰
数据库字段通常使用下划线（\_）连接单词，而Java的变量通常采用驼峰命名法，该设置项用于将下划线与驼峰命名映射起来。默认值为false，表示关闭映射。
```xml
  <settings>
    <setting name="mapUnderscoreToCamelCase" value="true"/>
  </settings>
```
#### typeAliases 
