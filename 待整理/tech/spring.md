1. 启动预置profile：-Dspring.profiles.active="local"

1. maven设置profile：maven only
<profiles>
    <profile>
        <id>local</id>
        <properties>
            <profiles.active>local</profiles.active>
            <package.environment>local</package.environment>
        </properties>
    </profile>
    <profile>
        <id>dev</id>
        <properties>
            <profiles.active>dev</profiles.active>
            <package.environment>dev</package.environment>
        </properties>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
</profiles>


## spring boot
* [Eclipse中创建新的Spring Boot项目](https://blog.csdn.net/ClementAD/article/details/51334064)

## mybatis
打印查询语句：mybatis-config.xml中加入<setting name="logImpl" value="STDOUT_LOGGING" />


idea：http://www.cnblogs.com/Brake/p/create_maven_multi_module_project_via_intellij_idea.html
