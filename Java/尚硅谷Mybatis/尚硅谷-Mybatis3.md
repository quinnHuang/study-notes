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

![](pic\为什么使用Mybatis.png)

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
## properties 标签
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
## settings 标签
控制mybatis框架的各种设置项，通过其子标签为setting来设置各种设置项。
### setting 标签
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
## typeAliases 别名管理器
为类指定别名，方便引用；有两种方式：typeAlias和package
mybatis中的别名都是不区分大小写的
### typeAlias 标签
直接为一个类指定别名，包括type和alias两个属性
* type：指定类的全类名
* alias：别名，**可省略**，则默认为类名

```xml
  <typeAliases>
    <typeAlias type="tb.bean.Employee" alias="emp">
  </typeAliases>
```
### package 标签+注解
指定包下的所有类使用默认别名（类名），只有一个name属性
* name：指定一个包

```xml
  <typeAliases>
    <package name="tb.bean"/>
  </typeAliases>
```
同时，可以使用 **Alias** 注解为类单独指定别名：
```java
  @Alias("emp")
  public class Employee {
    ...
  }
```

### 框架默认别名
mybatis已经为java常用的一些类指定好了别名，因此使用别名是应注意避免冲突

| 数据类型 | 别名 |
| :- | :-: |
| 基本数据类型 | _ 数据类型 |
| 包装类、集合 | 类名小写 |

## typeHandlers 类型处理器
用于java和数据库数据类型的转换
## plugins 插件
实际上使用中拦截器的功能，主要能拦截四大对象
* **Executor** (update, query, flushStatements, commit, rollback, getTransaction, close, isClosed)
* **ParameterHandler** (getParameterObject, setParameters)
* **ResultSetHandler** (handleResultSets, handleOutputParameters)
* **StatementHandler** (prepare, parameterize, batch, update, query)

## environments 运行环境
通过 **environment** 子标签可以配置多个数据环境，以便在使用、开发、测试等不同情况下可以切换不同的数据库环境。
只有一个 **default** 属性。
* default：指定一个 **environment** 的 **id** ，即选择一个程序执行的环境

### environment 标签
只有 **id** 属性，作为环境的唯一标识。
一个 *环境* 必须包含 **transactionManager** 和 **dataSource** 两个子标签。
### transactionManager 事务管理器标签
用于指定该环境的事务管理的方式，用 **type** 属性指定。
* type：事务管理的类型，有 **JDBC** 和 **MANAGED** 两种，这两个字符串实际上是两个类的别名，因而也可以自定义实现事务管理器类，在这里指定全类名.

### dataSource 数据源标签
实际上通过 **property** 子标签配置数据库连接。
通过 **type** 属性指定数据库连接方式。
* type：数据库连接方式，有 **UNPOOLED** 、**POOLED** 和 **JNDI** 三种方式，实质与 **transactionManager** 标签的 **type** 是一样的.
### property 标签
用于配置数据可连接信息，有 **name** 和 **value** 两个属性。
* name：数据库连接项，包括 *driver*、*url*、*username*、*password* 等项目。
* value：连接项的具体值。

```xml
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
```

## databaseIdProvider 数据库产商管理器
针对不同的数据产商，配置不同的SQL语句。
通过 **property** 子标签为不同数据库产商指定标识（name为数据库产商名称，value为别名），在 *mapper.xml* 文件中为SQL语句指定在哪个数据库软件下使用。
只有一个type属性。
* type：默认值 **DB_VENDOR** ，自动识别数据库产商，该值也是一个别名。

```xml
  <databaseIdProvider type="DB_VENDOR">
    <property name="SQL Server" value="sqlserver"/>
    <property name="DB2" value="db2"/>
    <property name="Oracle" value="oracle" />
  </databaseIdProvider>
```
在 *mapper.xml* 文件中，通过 **databaseId** 属性指定一个数据库产商的标识。
