# 性能

## 命令
* 查看内存分配命令(可以看到大量占用内存的对象)：jmap –histo:live [pid]
* dump命令：jmap -dump:live,format=b,file=p.dump [pid]

## 工具
1. visualvm
外部工具
  * [visualvm](https://visualvm.github.io/)
  * [Jstatd方式远程监控Linux下 JVM运行情况](http://www.cnblogs.com/catkins/p/5970364.html)TODO

2. JavaMelody
内置到项目
  * [JavaMelody](https://github.com/javamelody/javamelody)
  * [Spring Boot集成](https://github.com/javamelody/javamelody/tree/master/javamelody-for-spring-boot)TODO
