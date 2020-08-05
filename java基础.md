### Java知识整理

#### 1.基础知识

1.1java编译运行过程

1.1编译器(.java源文件,经过编译,生成.class字节码文件)
1.2运行期：JVM加载.class文件并运行.class文件

1.2JVM、JRE、JDK的关系：

2.1JVM：是java虚拟机

2.2JRE：java运行环境，除了包含jvm以外还包含java程序所必须的环境
（JRE=JVM+java开发工具包）

2.3JDK:java开发工具包，JDK=JRE+编译、运行等命令工具

- 运行java程序的最小的环境为JRE
- 开发java程序的最小的环境为JRE

1.3变量命名规则：

- 只能包含字母、数字、_和$符，并且不能以数字开头
- 严格区分大小写
- 不能使用关键字
- 驼峰命名法

1.4变量初始化及使用

- 当变量作为作为类成员使用时，Java才确保给定其初始值，防止程序运行时错误
  （成员变量在使用之前如果没有初始化，jvm就会帮我们初始化，）
- 方法中基本类型的所有变量在使用之前要保证是经过初始化的

```java
/*int b;
		b=3.14;//编译错误，不能赋值与不匹配的类型
		System.out.print(b);*/		
 /*int c;
		System.out.print(c);//编译错误，使用前必须赋值*/
```

<<<<<<< HEAD
#### 2.基本数据类型

(数据存储是以“字节”（Byte）为单位，数据传输大多是以“位”（bit，又名“比特”）为单位，一个位就代表一个0或1（即二进制），每8个位（bit，简写为b）组成一个字节（Byte，简写为B），是最小一级的信息单位 )

字节是二进制数据的单位。一个字节通常8位长

| 序号 | 数据类型 | 位数          | 字节 | 默认值 |
| ---- | -------- | ------------- | ---- | ------ |
| 1    | byte     | 8(1个字节8位) | 1    | 0      |
| 2    | boolean  | 8             | 1    | false  |
| 3    | char     | 16            | 2    | 空     |
| 4    | short    | 16            | 2    | 0      |
| 5    | int      | 32            | 4    | 0      |
| 6    | float    | 32            | 4    | 0.0    |
| 7    | long     | 64            | 8    | 0      |
| 8    | double   | 64            | 8    | 0.0    |

- 整数直接量默认为int型，但不能超范围，超范围则编译错误
- 两个整数相除，结果还是整数，小数位无条件舍弃
- 整数运算时超出范围会发生溢出，溢出是需要避免的
- 浮点数运算时，有可能会出现舍入误差，所以精确场合不建议使用
- 采用Unicode编码，每个字符都对应一个码
- 表现的形式是char字符，但实质上是int码
- 数据类型间的转换:
  1. 自动类型转换:从小类型转到大类型
  2. 强转类型转换:从大类型转到小类型  ，(要转换成的数据类型)变量，强转有可能会溢出或丢失精度
- 整数直接量可以直接赋值给byte,short,char，但不能超范围
- byte、short、char型数据参与运算时，先一律转换为int再运算
- boolean只有2个值：true、false,可以用1bit来存储，但具体大小没有明确规定。JVM会在编译时期将boolean类型的数据转化为int,使用1来表示true,0来表示false。JVM支持boolean数组，但是是通过读写byte数组来实现的。

#### 3.运算符

3.1算术运算符:+-*/%,++,--
3.2关系运算符:>,<,>=,<=,==,!=
3.3逻辑运算符:&&,||,!(双与，提高效率 &&  & )
3.4赋值运算符:=,+=,-=,*=,/=,%=
3.5字符串连接运算符:+
3.6三目/条件运算符:boolean?数1:数2

参与运算：(++a),(a++)：     ++在前面先自增再运算，++在后面先运算再自增
a前面有加号的加了再运算，前面没有加号的先运算再加

#### 4.数组

- 创建一位数组

```java
        int[] arr1 = {100,200,300,400,500};
        int[] arr2 = new int[5];
        arr2[0] = 100;
        arr2[1] = 200;
        arr2[2] = 300;
        arr2[3] = 400;
        arr2[4] = 500;
```

- 创建二位数组

```java
        String[][] str1 = {{"java","html"},{"css","javascript"}};
        String[][] str2 = new String[2][2];
        str2[0][0] = "java";
        str2[0][1] = "html";
        str2[1][0] = "css";
        str2[1][1] = "javascript";
```
#### 5.包装类型

基本类型都有对应的包装类型，基本类型与其对应的包装类型之间的赋值使用自动装箱与拆箱完成。

```
Integer x=2;//装箱 调用了Integer.valueOf(2)
int y=x; //拆箱 调用了 x.intValue()
```

#### 6.缓存池

new Integer(123) 与 Interger.valueOf(123)区别在于：

- new Integer(123)每次都会新建一个对象；

- Integer.valueOf(123) 会使用缓存池中的对象，多次调用会取同一个对象引用。

  ```java
  Integer x = new Integer(123);
  Integer y = new Integer(123);
  System.out.println(x==y);//false
  Integer z = Integer.valueOf(123);
  Integer k = Integer.valueOf(123);//true
  ```

  valueOf()方法的实现比较简单，就是先判断是否在缓存池中，如果在的话就直接返回缓存池的内容。

  ```java
  public static Integer valueOf(int i){
  	if (i>=IntegerCache.low && i <=IntergerCache.high)
  		return IntegerCache.cache[i+(-IntegerCache.low)];
  	return new Integer(i);
  }
  ```

   在 Java 8 中，Integer 缓存池的大小默认为 -128~127。 

  ```java
  static final int low = -128;
  static final int high;
  static final Integer cache[];
  
  static {
      // high value may be configured by property
      int h = 127;
      String integerCacheHighPropValue =
          sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
      if (integerCacheHighPropValue != null) {
          try {
              int i = parseInt(integerCacheHighPropValue);
              i = Math.max(i, 127);
              // Maximum array size is Integer.MAX_VALUE
              h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
          } catch( NumberFormatException nfe) {
              // If the property cannot be parsed into an int, ignore it.
          }
      }
      high = h;
  
      cache = new Integer[(high - low) + 1];
      int j = low;
      for(int k = 0; k < cache.length; k++)
          cache[k] = new Integer(j++);
      // range [-128, 127] must be interned (JLS7 5.1.7)
      assert IntegerCache.high >= 127;
  }
  ```
  

编译器会在自动装箱过程中调用valueOf()方法，因此多个值相同且值在缓存池范围内的Integer实例使用自动装箱来创建，那么就会引用相同的对象。

```java
  Integer m=123;
  Integer n=123;
  System.out.println(m==n);//true
```

基本类型对应的缓冲池如下：

- boolean values true and false

- all byte values

- short values between -128 and 127

- int values between -128 and 127

- char in the range \u0000 to \u007F

在使用这些基本类型对应的包装类型时，如果该数值范围在缓冲池范围内，就可以直接使用缓冲池中的对象。

在 jdk 1.8 所有的数值类缓冲池中，Integer 的缓冲池 IntegerCache 很特殊，这个缓冲池的下界是 - 128，上界默认是 127，但是这个上界是可调的，在启动 jvm 的时候，通过 -XX:AutoBoxCacheMax=<size> 来指定这个缓冲池的大小，该选项在 JVM 初始化的时候会设定一个名为 java.lang.IntegerCache.high 系统属性，然后 IntegerCache 初始化的时候就会读取该系统属性来决定上界。

#### 7.引用数据类型String

string 被申明为final,因此它不可继承.(Integer等包装类也不能被继承)

value 数组被声明为 final，这意味着 value 数组初始化之后就不能再引用其它数组。并且 String 内部没有改变 value 数组的方法，因此可以保证 String 不可变。 

#### 8.for循环

- 1.格式：for(初始化语句1;条件判断语句2;循环体执行之后的语句4){循环体3}
  2.执行流程1 —>2—>3—>4 —>2—>3—>4—>2false(结束)

- 增强for循环:for(数据类型 变量名：数组或者集合名){}

- 求和思想

  ```java
  int sum=0;
  for(int i=1;i<=100;i++){
  sum+=i
  }
  System.out.println(sum);
  ```

- while格式:
  初始化语句1
  while(条件判断语句2){循环体3;循环体之后的语句4;}
  执行顺序：和for是一样；1—>2—>3—>4—>2—>3—>4—>2false(结束)

- do while格式：
  初始化语句1
  do{循环体3;循环体之后的语句4;}while(条件判断语句2);
  特点：do whlie至少会执行一次循环体

- 循环控制语句
  continue //跳出本次循环，继续下次循环
  break //跳出全部循环

- 嵌套循环

  ```java
  for(int i=1;i<=4;i++){
       for(int j=1;j<=5;j++){
            System.out.print("*");
       } 
    System.out.println();
  }
  ```

- 条件控制语句
  格式1：if(){}
  格式2：if()else{}
  格式3：if()else if(){}else if(){}else{}
  格式4：if()if()if()else{}//和格式3区别：主要满足条件就进if，不存在互斥

  ```
  eg:
  ```

- switch格式：
  switch(值)值的类型:byte、short、int、char、String、枚举
  switch什么时候结束，遇到break和}
  break穿透：没有遇到break,不会再次进行case匹配

  ```java
  switch(值){
      case 值1:
          语句;
          break;
      case 值1:
          语句;
          break;
      default:
          语句;
     		break; 
      }
  ```

- 遍历数组
- 冒泡排序
- 打印等边三角形











