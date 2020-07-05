### Java知识整理

#### 一、Basic

##### 1.java编译运行过程：

1.1编译器(.java源文件,经过编译,生成.class字节码文件)
1.2运行期：JVM加载.class文件并运行.class文件

##### 2.JVM、JRE、JDK的关系：

2.1JVM：是java虚拟机

2.2JRE：java运行环境，除了包含jvm以外还包含java程序所必须的环境
（JRE=JVM+java开发工具包）

2.3JDK:java开发工具包，JDK=JRE+编译、运行等命令工具

- 运行java程序的最小的环境为JRE
- 开发java程序的最小的环境为JRE

##### 3.变量命名规则：

- 只能包含字母、数字、_和$符，并且不能以数字开头
- 严格区分大小写
- 不能使用关键字
- 驼峰命名法

##### 4.变量初始化及使用

```
/*int b;
		b=3.14;//编译错误，不能赋值与不匹配的类型
		System.out.print(b);*/		
 /*int c;
		System.out.print(c);//编译错误，使用前必须赋值*/
```

#### 5.基本数据类型

- byte 

- char

- short

- int 

- float

- long

- double

- bollean

  