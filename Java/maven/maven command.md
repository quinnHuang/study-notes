## mvn archetype:generate
创建Java的maven项目
> mvn archetype:generate  
-DgroupId=com.how2java   
-DartifactId=j2se   
-DarchetypeArtifactId=maven-archetype-quickstart  
-DinteractiveMode=false
 
* archetype:generate: 表示创建个项目
* -DgroupId: 项目包名，com.how2java
* -DartifactId: 项目名称，j2se
* -DarchetypeArtifactId: 项目类型，maven-archetype-quickstart
* -DinteractiveMode: false，表示前面参数都给了，就不用一个一个地输入了
