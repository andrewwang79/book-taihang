# C++知识
## 资料
* [C++ 异常处理](https://www.runoob.com/cplusplus/cpp-exceptions-handling.html)
* [gcc,make,cmake](https://blog.csdn.net/libaineu2004/article/details/77119908)
* [gcc编译选项](https://www.jianshu.com/p/223d8b6aa879)

## 命令
* 查看链接库路径：echo $LD_LIBRARY_PATH
* 重新加载库：ldconfig /usr/local/lib
* 查看依赖库：ldd xxx.so
* 查看符号：nm xxx.so
* 查看文件(执行文件/库)是否是debug版本：readelf -S ri.out |grep debug

## core dump
* [GCC如何产生core dump并定位问题](https://blog.csdn.net/pbymw8iwm/article/details/7035736)
* gcc -g // 加符号，否则很难定位问题

### 启用
* Ubuntu运行
  * 启用apport，service apport start
  * 默认在当前目录，echo后log在/tmp/core*
* docker运行
```
【log在/tmp/core*】
1. 宿主机上执行：echo '/tmp/core.%t.%e.%p' | sudo tee /proc/sys/kernel/core_pattern。
2. docker-compose文件里设置启用GDB工具
cap_add:
  - SYS_PTRACE
```

### 编译调试
#### 流程
https://www.cnblogs.com/tinywan/p/7230039.html
1. 安装依赖库：conan install
1. 生成Makefile文件
  1. cmake .
  1. configure  
1. 编译：make -j8
1. 安装：make install

#### Linux直接编译程序
```
cd 代码目录conan install . -s arch=x86_64 -s os=Linux -r cloud --update
conan install ../ -s arch=x86_64 -s os=Linux -s build_type=Debug -r cloud --update
cmake .
make -j 8
```

#### 在Windows开发调试Linux上运行的程序

#### 库调用无效的解决
```
nm -D baseLib1.so 查看symbol
symbol找不到(有，但加了装饰)的解决：
头文件定义：
extern "C" {
double power1(double base, int exponent);
}
```

## 开发规范
1. [editorconfig](https://juejin.im/post/5b9cba4c6fb9a05cf67a79a4)

## 第三方库
### Linux系统库
https://blog.csdn.net/haibosdu/article/details/77094833

| 项 | 说明 |
| :-: |  |
| libc | Linux的标准C库 |
| glibc | GNU C Library，替代了libc。Linux中最底层的API |
| libstdc++ | C++标准库，和gcc配套 |

### boost
* [C++使用Boost实现HTTP服务端——同步、异步、协程](https://blog.csdn.net/luchengtao11/article/details/100928141)
* [Boost Beast要点解析](https://blog.csdn.net/guxch/article/details/106780832)
