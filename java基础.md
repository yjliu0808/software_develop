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

### 一、数据类型

#### 基本类型

(数据存储是以“字节”（Byte）为单位，数据传输大多是以“位”（bit，又名“比特”）为单位，一个位就代表一个0或1（即二进制），每8个位（bit，简写为b）组成一个字节（Byte，简写为B），是最小一级的信息单位 )

- byte/8

- char/16

- short/16

- int/32

- float/32

- long/64

- double/64

- boolean/~

  boolean只有2个值：true、false,可以用1bit来存储，但具体大小没有明确规定。JVM会在编译时期将boolean类型的数据转化为int,使用1来表示true,0来表示false。JVM支持boolean数组，但是是通过读写byte数组来实现的。

#### 包装类型

基本类型都有对应的包装类型，基本类型与其对应的包装类型之间的赋值使用自动装箱与拆箱完成。

```
Integer x=2;//装箱 调用了Integer.valueOf(2)
int y=x; //拆箱 调用了 x.intValue()
```

#### 缓存池

new Integer(123) 与 Interger.valueOf(123)区别在于：

- new Integer(123)每次都会新建一个对象；

- Integer.valueOf(123) 会使用缓存池中的对象，多次调用会取同一个对象引用。

  ```
  Integer x = new Integer(123);
  Integer y = new Integer(123);
  System.out.println(x==y);//false
  Integer z = Integer.valueOf(123);
  Integer k = Integer.valueOf(123);//true
  ```

  valueOf()方法的实现比较简单，就是先判断是否在缓存池中，如果在的话就直接返回缓存池的内容。

  ```
  public static Integer valueOf(int i){
  	if (i>=IntegerCache.low && i <=IntergerCache.high)
  		return IntegerCache.cache[i+(-IntegerCache.low)];
  	return new Integer(i);
  }
  ```

   在 Java 8 中，Integer 缓存池的大小默认为 -128~127。 

  ```
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

  ```
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

### 二、String

#### 概述

string 被申明为final,因此它不可继承.(Integer等包装类也不能被继承)

 value 数组被声明为 final，这意味着 value 数组初始化之后就不能再引用其它数组。并且 String 内部没有改变 value 数组的方法，因此可以保证 String 不可变。 





