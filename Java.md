# JavaSE

## 简介

### 三个名词

JDK：Java开发者工具，在JRE基础上添加了很多工具，包含JRE

JRE：Java运行时环境，有它就可以运行程序，但是要开发程序必须要有JDK

JVM：Java虚拟机，属于JRE，在电脑上模拟了一个小cpu，等于一个小的虚拟机，用它才能实现Java的跨平台

> Write once,run anywhere

### 安装

1. `https://www.oracle.com/java/technologies/javase-downloads.html`下载JDK
2. 直接安装
3. （*可能不用）添加环境变量
   1. 进入`Java`目录
   2. `bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre`生成jre文件夹
   3. 新建系统变量![image-20210307115419394](https://s2.loli.net/2021/12/05/KIgS9Dm8haRxcFi.png)
   4. 新建PATH变量![image-20210307115459215](https://s2.loli.net/2021/12/05/NVHFIj6wyUhR7td.png)
4. 安装目录内`bin`目录存放各种 `.exe`文件，用于运行Java文件
5. `include`目录引用了一些`c`的头文件
6. `lib`目录放了一些Java的库文件
7. `lib`里面还有个`src.zip`存放Java的所有类源代码

### 卸载

1. 删除Java安装目录
2. 删除JAVA_HOME环境变量
3. 删除PATH内有关JAVA的目录
4. `java -version`查看Java版本信息，检查是否删除成功

### 编译型&解释型

**Java语言是结合了编译语言和解释语言**

`.java`文件通过编译器（Javac）预编译变成了`.class`文件，这种`.class`文件介于机器码和Java源代码之间（字节码）

当`.class`文件运行的时候会走到JVM虚拟机的类装载器中，对其中的字节码进行校验，看看写的对不对

如果都是对的，就把这个代码交给解释器，解释完后给操作系统平台

## 简单的开始

### 默认类创建时所需

```java
public class Hello{
    public static void main(String[] args){
        System.out.println("Hello,World!");
    }
}
```

> 在IDEA中，只需要输入`psvm`就可以快速创建`main`方法
>
> 而输入`i.sout`就可以直接`System.out.println(i)`

### 执行第一个Java程序

```cmd
javac Hello.java # 编译Java文件
java Hello # 执行Java的class文件，但注意不要加后缀class
```

![image-20210307115814933](https://s2.loli.net/2021/12/05/2GNvK4YMJatLAdy.png)

### Warning

1. Java大小写敏感
2. 尽量使用英文
3. 文件名和类名必须保证一致，并且首字母大写
4. 符号不能使用中文

### 在IDEA中新建一个空项目

1. 文件→新建→项目，并在弹出页面中选择**空项目**
2. 文件→新建→新模块，选择Java模块并设置名字
3. 文件→项目结构，在项目一栏中的SDK中选择自己的Java版本，并在项目语言级别中同样选择自己的Java版本
4. 在创建好的新模块下的`src`目录中创建一个Java类文件
5. 愉快的编写代码

> IDEA优化&有趣的代码注释

### 类型和运算

- `//`单行注释

- `/*   */`多行注释

- `/**   */`文档注释，内部可以通过`@`加内容

- 数据类型（Java是一种强类型语言，所有变量都应该先定义后才能使用）

  - 在定义的时候必须直接定义内容

  - `byte/short/int/long`都是整数类型，`long`类型后面要加一个`L`

    - 整数类型前`0b`表示二进制，`0`是八进制，`0x`是十六进制

    - 数字之间可以加下划线，不影响输出

    - ```java
      int i = 10_0000_0000
      int j = 20
      long total = i * j
      ```

      如果输出会发现输出了一个负数，实际上`i*j`作为`int`计算完之后再进行转换

      ```java
      long total = i * (long)j
      ```

      这样就可以正确输出

    - 除了`long`类型，其他整数类型相互运算结果都是`int`类型

  - `float/double`则是浮点类型，`float`类型后面要加`F`

    - **不要使用浮点数进行比较**
    - 银行业务可以用别的类，反正不要用浮点

  - `char`是字符型，可以包含一个字符

    - `’\u0x‘`表示unicode的一个编码

  - `boolean`是布尔类型

  - `String`**不是关键字**，因为它以大写开头，其实是一个类，不属于基本数据类型

    - 拼接字符串直接`+`

  - 所有的关键字的如果大写首字母就变成一个类，可以看到这个关键字的基本信息

  - 在前面使用`([基本类型])`可以强制类型转换，但是当类型从低容量转换到高容量时，自动就可以转换了，布尔类型不能转换

- 变量类型

  - 实例变量，在某个方法外，等于是一个类的属性，不初始化内容就是默认值（`0/0.0/\u0000/false/null`）

  - 局部变量，一定要有初始值，在某个方法内

  - 类变量，在变量前加`static`修饰符，不是类的属性了，而是这个类当中的全局变量

    > 加了修饰符之后会对后面的变量产生一定的效果，修饰符不分前后

  - `final` 加在原本变量之前来定义一个常量，常量建议全部大写字母+下划线

- 运算符和`C`语言都一样

- `Math.pow([数字],[几次])`幂运算

### 包机制

包实际上就是一个文件夹

一般使用公司的域名倒置作为包的名称（com.baidu.www）

如上所示创建一个包之后，会发现递归创建了三个文件夹，我们把所需的各个网站内容分别装在不同的文件夹中

在类的最上边要明示包名

```java
package com.baidu.www;
```

正因如此，`src`目录下第一个文件夹往往是`com`

`Ctrl + [点击包名]`可以跳转到某个包的路径

在某个Java文件中要使用别的包的内容，且用的内容存在歧义（如好多个包中都有`Date`这个方法），就需要使用`import`进行导包

且`import`导入的包不能和本文件的类名称相同

> - 阿里巴巴开发手册

### JavaDoc

#### 概要

JavaDoc是用来生成自己的API文档的，需要使用文档注释

注释中的参数信息

- `@author [作者名]`
- `@version [版本号]`
- `@since [需要最早使用的jdk版本]`
- `@param [参数名]`
- `@return [返回值情况]`
- `@throws [异常抛出情况]`

要给某个类做注释就要加在那个类**上面**

#### 生成自己的JavaDoc文档

之后在命令行内可以查看某个Java文件的JavaDoc

```bash
javadoc -encoding UTF-8 -charset UTF-8 [.java文件名]
```

之后会出现一个`index.html`，进入后会出现该类的详细文档说明

### 流程控制

#### 利用Scanner对象实现人机交互

```java 
Scanner scanner = new Scanner(System.in);
// 创建一个scanner对象，使用System.in接收用户的输入，并封装成scanner对象
// 可以通过new Scanner(System.in)然后按Alt + Enter快速生成对象
if (scanner.hasNext()){
    // 如果用户还有输入，就使用next方法接收
    String str = scanner.next();  // 使用scanner接收用户的输入
    // nextLine()也可以接收，可以忽略输入时候的空格
}
// 所有IO流的类如果不关闭就会一直占用资源，用完scanner就要关掉
scanner.close();
```

事实上上述代码的判断语句可以删除，依旧可以输入一个内容，但是一般来说要经过一个判断来判定用户是否输入了正确的类型

```java
Scanner scanner = new Scanner(System.in);
if (scanner.hasNextInt()){
    int i = scanner.nextInt();
    System.out.println(i);
}
else {
    System.out.println("请输入整数");
}
scanner.close();
```

#### 各种基本结构

**顺序结构**就是Java代码正常情况下从上往下依次执行

**判断结构**就是`if/else`或`switch/case`语句，和`C`语言没啥区别

> 注意`case`穿透现象，当某一个`case`判断成功后，没有`break`的情况时，会把后面每一个`case`内容都执行一遍
>
> > `JDK7`之后，`case`语句支持字符串的判定了，我们可以通过项目管理里查找到编译后的`.class`文件
> >
> > ![image-20210309180041704](https://s2.loli.net/2021/12/05/9pEiHo4ehSVmcnG.png)
> >
> > 将`.class`文件直接拷到`.java`文件的目录内，通过`IDEA`打开，可以获得`.class`文件的反编译代码
> >
> > 会发现`case`语句处理字符串时，使用了其中的`.hashCode`方法生成哈希值来判定
> >
> > ![image-20210309181447344](https://s2.loli.net/2021/12/05/fvFsT9jKaAoI7qN.png)

**循环结构**也和`C`语言没什么不同，就是`while/do..while/for`语句

> 通过`fori`快速生成一个递增循环
>
> 通过`100.for`来快速生成一个循环100次的`for`语句，而`100.forr`可以快速生成一个递减循环
>
> `break`和`contiune`也和`C`语言一样

- 增强型`For`循环，实际上和`python`中的`for`循环差不多

  ```java
  int[] numbers = {1,2,3,4};
  for (int x:numbers){
      // == for x in numbers
      // 循环语句
  }
  // 可以直接通过numbers.for来快速生成一个进阶for循环
  ```

- 循环体中标签的使用

  ```java
  outer:for (int i = 0; i<10; i++){
      for (int j = 0; j<10; j++){
          continue outer;
          // 跳转到第一个for循环
      }
  }
  ```

### 方法

方法的基本格式

```java
public static void main(String[] args){
    return [返回值]
}
// [修饰符] [返回类型] [方法名([参数类型] [参数名])]{}
```

方法约等于函数，因为Java面向对象所以函数的模式被淡化了

#### 方法重载

只需要方法的参数不同，方法可以用同一个名字，编译器会自动识别用哪一个方法，这就是方法重载

```java
public class Demo3 {
    public static void main(String[] args) {
        int i = max(10,20);
        double j = max(10,20);
        System.out.print(i+" "+j);
    }

    public static int max(int a, int b){
        return a>b?a:b;
    }
    public static double max(double a, double b){
        return a>b?a:b;
    }
}

```

#### 命令行传参

当我们在命令行使用`java [文件名]` 执行某一个`class`文件时，可以在后面加若干个参数，会根据空格作为分割通过字符串的方式传递给`main`方法的`args`字符串数组

```java
// 输出args数组内的内容
public class Demo4 {
    public static void main(String[] args) {
        int j = 0;
        for (String i:args){
            j++;
            System.out.println(j+""+i);
        }
    }
}
```

#### 可变传参

在某个形参定义时类型的后面加`...`可以传递任意参数，等于`python`中的`*args`

事实上就是把某个类型变成了一个数组，传递的参数变成了数组中的值

```java
public class Demo5 {
    public static void main(String[] args) {
        test(1,2,3,4,5);
    }
    public static void test(int... i){
        for (int j:i){
            System.out.println(j);
        }
    }
}
```

注意可变传参的参数必须在形参的最后一个

### 数组

数组可以用两种方式定义

```java
int[] nums1;
int num2[];  // 不推荐
num1 = new int[10]  // 定义数组长度，每个元素赋默认值0
```

可以通过`.length`方法获取数据长度

事实上，Java通过堆和栈的共同作用来定义一个数组

![image-20210310180005509](https://s2.loli.net/2021/12/05/5B6RQdj14ClmMEP.png "关于堆和栈的理解")

会发现命名在栈中完成，开辟空间在堆中完成，赋值就在堆中的空间中执行

同时，通过`new`创建的变量属于动态初始化，直接在变量后`= [值]`叫做静态初始化，动态初始化包含默认初始化

```java
Man[] mans = {new Man(1,1), new Man(2,2)};  // 静态初始化,Man时另一个文件中的一个类，本质就是创建+初始化
int[] int1 = new int[10];  // 动态初始化，每个元素赋默认值
```

#### Arrays类

`Arrays`类是系统封装的一个用于操作数组的类

- `sort`对数组进行排序
- `toString`变成带中括号的字符串
- `fill(*,[起始],[结束],[填充内容])`将指定内容填充数组的每一个元素
- 其他的方法建议通过帮助文档查看

#### 稀疏数组

有些时候某个数组的大多数元素的值都是默认值0，反而占用大量空间，这时候就可以用我们的稀疏数组

比如棋盘的内容，我们就可以用另一个简单的$3*n$二维数组来保存

- `a[0]`保存这个棋盘的大小`a[1/2/3]`分别是行、列、元素个数
- 从`a[1]`开始，每一行保存元素所在位置和所在位置的值

### 面向对象编程(OOP)

#### 方法的调用

当在某一个方法前面加`static`就将一个方法变成静态方法，在别的程序中可以直接通过`[类名].[方法名]`来调用

不加`static`的方法就是非静态方法，必须先通过`new`实例化一个对象，再通过这个对象调用其中的方法

`static`方法是和类一起加载的，而非静态方法是类的实例化，在类创建完之后加载，因此不能在`static`方法中调用另一个不是`static`修饰的方法

#### 构造器

类中的构造器也称为构造方法，是在进行创建对象的时候必须要调用的，他有两个特点

- 必须和类的名字相同
- 必须没有返回类型，也不能写viod

就算我们只单纯定义一个类，编译的时候也会自动创建一个构造器

相当于`python`中的`__init__`方法

如果要给构造器传递参数，就要用有参构造，不过注意如果定义了有参构造，无参构造必须显示

```java
public class Test {
    String name;
    public Test() {
        // 有参构造必须创建一个空的无参构造
    }
    public Test(String name){   // 有参构造
        this.name = name;  // this等于python中的self
    }
}
```

有参构造的方法也可以同名但是参数不同，系统会自动识别

`Alt+insert`可以自动生成无参/有参构造器

#### 封装

程序设计要追求**“高内聚，低耦合”**，类的内部数据操作细节自己完成，不允许外部干涉，仅暴露少量方法提供给外部使用

通常，应禁止直接访问一个对象中数据的实际表示，而应通过操作接口来访问，这称为**信息隐藏**

要实现属性私有，就要使用`private`修饰符，外部想要访问到某个私有属性，我们可以提供一个`get`方法

![image-20210310205049211](https://s2.loli.net/2021/12/05/3vqnjNwSJ6bAYMG.png)

如图，系统会自动生成一个`get`方法，里面自动`return`了私有属性`name`

外部想要设置某一个属性，同样如图设定一个`set`方法

```java
public class Test {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

`Alt+insert`可以自动生成`get/set`方法

通过`get/set`方法可以有效规避不法分子乱定义属性，我们只需要在`get/set`方法内判断并抛出异常

#### 继承

在某一个类名后`extends [父类]`就可以继承一个父类，注意Java没有多继承

使用`super`代替`this`可以访问父类的方法/属性

子类不能继承父类的私有属性/方法，甚至使用`super`也不行

在子类的界面中按下`Ctrl+H`可以看到继承完整树

事实上，和`python`相同，在Java中，所有的类都默认继承`object`类

同时注意子类的无参构造中会自动执行父类的无参构造，隐藏了`super()`这一行代码

使用`super/this()`可以直接执行构造器方法，不过必须放在方法的第一行（所以两个方法不能同时调用）

![image-20210311182200630](https://s2.loli.net/2021/12/05/JEvoQmO8rKBGnNh.png)

上图可以发现，存在继承关系时，子类可以重写父类的方法，不过注意

- 重写的方法名必须相同
- 重写的餐宿列表必须相同（不然就是重载）
- 重写时修饰符可以扩大但不能缩小（`public>protected>default（默认）>privite`）
- 抛出的异常可以被缩小但不能被扩大
- `static`方法属于类不属于生成的对象，不能被重写
- `final`方法无法改变也不能重写，甚至不能有子类
- `private`方法也不能重写

#### 多态

看上图，`new`后面是指向，前面的是引用类型

```java
B b = new A();
// [引用] [对象名] = new [类型名]
```

一个对象的指向是确定的，但是引用类型不确定，父类的引用可以指向子类

子类重写的父类的方法，上述代码执行子类的方法

父类的引用不能调用非重写子类的方法，也就是能执行的方法看左边的引用，但执行效果需要看右边

如果强行要让父类类型执行子类方法，需要强制类型转换`((A)b).test`

要看某个类是否是另一个类的子类，需要用`instanceof`关键字

```java
// Object > String
// Object > Test
Test test = new Test();
Object object = test;  // 可以直接转换为父类
System.out.println(object instanceof Test);  // True
System.out.println(object instanceof Object);  // True
System.out.println(object instanceof String);  // False
System.out.println(test instanceof String);  // 会报错，他们俩没有半毛钱关系
```

子类虽然能直接转换为父类，但是可能丢失一些方法，父类转子类用强制转换，才能调用子类未重写的方法

#### Static关键字详解

![image-20210311193138594](https://s2.loli.net/2021/12/05/C8Z37Jy2HTz6hnF.png "创建一个类时各方法的执行顺序")

可以发现`static`方法永远位于第一个执行，和类一起加载，然后通过`main`方法新建一个类后，先执行匿名代码块（成员变量）内容，再执行构造方法

通过静态导入包，可以快捷直接访问某个包内的方法

```java
package com.mine.oopdemo;
import static java.lang.Math.random;

public class Demo2 {
    public static void main(String[] args) {
        System.out.println(random());
    }
}
```

#### 抽象类

![image-20210311205410993](https://s2.loli.net/2021/12/05/HS6e98cBGbm4lFu.png)

抽象类由于单继承的局限性，用到的情况不是很多，不过还是要注意

- 抽象类不能被`new`出来，只能靠子类去实现它

- 抽象类里可以写普通方法，但是抽象方法不能写在普通类中

#### 接口

接口什么都没有，自己甚至无法写方法，比抽象类还要抽象，是专业的约束

面对大的项目的时候，我们要学会面向接口编程，由架构师整理出大的框架再由码农进行方法设计

接口就是规范，像法律一样，定义好了之后大家都要遵守

![image-20210311213956059](https://s2.loli.net/2021/12/05/zg4JVtkG7OwrlKj.png "不同的图标样式")

```java
// 接口定义

// interface定义的关键字就是接口，接口都需要有实现类
public interface Demo5 {
    // 接口定义的属性都是常量，默认public static final
    int AGE = 100;
    // 接口中的所有定义其实都是抽象的，默认public abstract
    void add(String name);
    void delete(String name);
    void update(String name);
    void query(String name);
}
```

```java
// 实现类

// 接口的实现类一般名字以Impl结尾
// 类可以实现接口，通过implements关键字，可以通过逗号分隔用来继承多个接口
// 实现了接口中的类，就需要重写接口中的方法
public class Demo5Impl implements Demo5{

    @Override
    public void add(String name) {

    }

    @Override
    public void delete(String name) {

    }

    @Override
    public void update(String name) {

    }

    @Override
    public void query(String name) {

    }

}
```

#### 内部类

```java
public class Demo6 {
    private int id;
    public void out(){
        System.out.println("外部类的方法");
    }
    
    public class Inner{
        public void in(){
            // 内部类可以获得外部类的私有属性/方法
            System.out.println(id);
        }
    }
    
    // 另外方法中也可以定义一个类，叫做局部内部类

    public static void main(String[] args) {
        Demo6 demo6 = new Demo6();
        Inner inner = demo6.new Inner();  // 如何定义一个内部类
    }
}
```

### 异常机制

当程序运行中出现了编译之外的错误，程序就会自动抛出异常

异常可以分为三类

- 检查性异常，用户错误或问题引起的异常，程序员无法预见，在编译时无法被简单的忽略，比如打开不存在的文件
- 运行时异常，可能被程序员避免，可以在编译时被忽略，比如递归调用
- 错误（ERROR），不是异常，时脱离程序员控制的问题，在代码中通常被忽略，比如栈溢出

Java中可以把异常当作一个对象来处理，制定了一个异常体系结构，并定义了一个基类`java.lang.Throwable`作为所有异常的超类

其中又分为两个大类，错误（Error）和异常（Exception）

![img](https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3365527833,3762210150&fm=26&gp=0.jpg)

另外，`Error`类对象是由Java虚拟机生成并抛出，大多数错误与代码编写者所执行的操作无关，这些异常发生的时候，Java虚拟机（JVM）就直接终止了

`RuntimeException`属于运行时异常，程序应该从逻辑角度尽可能避免这些异常的发生

```java
public class Demo1 {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;
        if (b == 0){
            throw new ArithmeticException();  // 主动抛出异常，一般存在某个方法中无法处理某个异常
        }
        try {  // try监控区域
            System.out.println(a/b);
        }catch (ArithmeticException e){  // 捕获异常，括号里是想要捕获的异常类型（最高时Throwable）
            // 增加
            System.out.println("div 0");
        }catch (Exception e){  // 大类的异常必须在小类异常的后边
            System.out.println("Exception");
        }finally {  // 处理善后工作
            System.out.println("finally");
        }
        // finally 可以不要，之后学习中可以用来释放占用的资源
    }
}
```

选中一行代码`Ctrl+Alt+T`可以快速生成包裹代码

另外，用户可以自定义异常类，只需要继承`Exception`类即可

```java
// 异常类

public class Demo2 extends Exception{
    // 传递数字>10就抛出异常
    private int detail;
    public Demo2(int a){
        this.detail = a;
    }

    @Override
    public String toString() {  // 直接通过alt+insert快速创建，打印异常信息
        return "Demo2{" +
                "detail=" + detail +
                '}';
    }

}
```

```java
// 抛出自定义异常

public class Demo3 {
    public static void main(String[] args) throws Demo2{
        int a = 11;
        if (a>10){
            throw new Demo2(a);  // 抛出
        }
       
    }
}
```

## I/O流

### 流

流就是内存和存储设备传输数据的通道

#### 分类

输入流就是将存储设备中的内容读入到内存中，输出流相反

字节流以字节为单位，可以读写所有的数据，字符流只能读写文本数据

节点流是具有实际传输数据的读写功能，过滤流就是在节点流的基础上增强功能

#### 字节流

`InputStream`和`OutputStream`是所有`I/O`流的超类，提供了一般子类的方法

下面以文件字节输入/输出流示例

##### FileInputStream

```java
public class Demo1 {
    public static void main(String[] args) throws IOException {
        // 创建文件输入流，并指定路径
        FileInputStream input = new FileInputStream("D://test.txt");// 可能没有这个文件，抛出异常
        // 1. 单个字节读入
        int len;
        while ((len=input.read())!=-1){
            System.out.print((char)len);
        }
        // 2. 多个字节读入
        byte[] buf = new byte[4];
        int count = input.read(buf);  // 将文件中读到的buf长度内容放在buf数组中
        System.out.println(new String(buf));
        System.out.println(count);
        // 3. 最优结合（因为不能够创建一个过大的数组）
        byte[] buf = new byte[1024];  // 缓冲区，每次接收1kb内容
        int count=0;
        while ((count=input.read(buf))!=-1) System.out.print(new String(buf,0,count));
        // 关闭
        input.close();
    }
}
```

##### FileOutputStream

```java
public class Demo2 {
    public static void main(String[] args) throws IOException {
        FileOutputStream os = new FileOutputStream("test.txt",true);  // 布尔为真代表追加内容
        // 追加内容同样会创建文件
        os.write(97);  // a的ASCII码，输出仍为a
        os.write('b');
        os.write('\n');
        String s="hello";
        os.write(s.getBytes());  // 传入字节数组
    }
}
```

##### 字节缓冲流

缓冲流即`BufferInputStream/BufferOutputStream`

本身文件输入输出流是不带缓冲的，单独使用文件字节流效率不高（容量太小）

缓冲流通过单独创建一个缓冲区，当主数据缓冲区内有可以直接获得

可以用于提高I/O的效率，减少访问磁盘的次数

数据存储在缓冲区内，通过`flush`将缓冲区内的内容写入文件中

```java
public class Demo3 {
    public static void main(String[] args) throws IOException {
        // 创建BufferInputStream
        FileInputStream is = new FileInputStream("test.txt");
        BufferedInputStream bufIs = new BufferedInputStream(is);  // 说明这个缓冲流是为了增强is的
        // 从缓冲区读取
        // int data=0;
        // while ((data=bufIs.read())!=-1) System.out.println();  // 利用BufferedInputStream自带的缓冲区
        // 也可以自己创建一个缓冲区并传入
        int count;
        byte[] buffer = new byte[1024];
        while ((count=bufIs.read(buffer))!=-1) System.out.print(new String(buffer,0,count));

        // 关闭只需要关闭缓冲流
        bufIs.close();
    }
}
```

```java
public class Demo4 {
    public static void main(String[] args) throws IOException {
        FileOutputStream os = new FileOutputStream("test.txt");
        BufferedOutputStream bufOs = new BufferedOutputStream(os);
        for (int i = 0; i < 10; i++) {
            bufOs.write("hello\n".getBytes());  // 写入8K缓冲区，先不写入文件
            // 直到缓冲区满了自动写入文件
            // bufOs.flush();  // 也可手动每次刷新到硬盘
        }
        bufOs.close();  // 关闭的时候会自动执行flush()操作
    }
}
```

#### 对象流

对象流增强了缓冲区功能和8种基本数据类型和字符串功能

同时通过流传输**对象**的过程称为<a name="序列化">序列化</a>和反序列化

```java
// 想要序列化一个对象，必须实现Serializable接口，但这个接口没有任何的方法（标记接口）
class Test1 implements Serializable {
    // 序列化版本号ID，可以保证序列化的类和反序列化的类是同一个类
    // 反序列化的时候UID会与文件中的UID比对，不一样就抛出异常
    @Serial
    private static final long serialVersionUID = 100L;

    private String name;
    private int age;
    private transient int test1;  // 用transient（瞬间的）修饰不会被序列化
    private static int test2;  // 静态属性也不会被序列化

    public Test1(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 一个类正确的定义方式
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Test1{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

public class Demo5 {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        // 实现把一个对象写在硬盘上，序列化操作
        FileOutputStream fos = new FileOutputStream("test.bin");
        ObjectOutputStream oos = new ObjectOutputStream(fos);
        Test1 test = new Test1("test", 1);
        oos.writeObject(test);
        oos.close();
        // 读取文件重构对象，反序列化操作
        FileInputStream fis = new FileInputStream("test.bin");
        ObjectInputStream ois = new ObjectInputStream(fis);
        Test1 t = (Test1) ois.readObject();  // 强转为Test1类型
        // 如果文件内有多个对象继续读就能获得第二个对象
        ois.close();  // 关闭的时候也会关闭文件流
        System.out.println("Done");
        System.out.println(t.toString());
    }
}
```

注意要求序列化类中的对象属性（假设某个属性的类型是一个类的话）也要实现`Serializable`接口

#### 字符编码

- ISO-8859-1 收录除ASCII外，还包括西欧、希腊语、泰语、阿拉伯语、希伯来语对应的文字符号（一字符）
- UTF-8 针对Unicode码表的可变长度字符编码
- GB2312 简体中文
- GBK 简体中文、GB2312扩充（ANSI在中国即是GBK）
- BIG5 台湾、繁体中文

注意当编码方式和解码方式不一致的时候会出现乱码

#### 字符流

我们可以通过记事本的另存为查看当前记事本记录的代码格式

```java
public class Demo6 {
    public static void main(String[] args) throws IOException {
        // 当文件中存在中文时，要用字符流读取和写入
        FileWriter fileWriter = new FileWriter("test.txt");
        for (int i = 0; i < 10; i++) {
            fileWriter.write("你好\n");
        }
        fileWriter.close();

        FileReader fr = new FileReader("test.txt");  // FileReader继承FileInputStream
        int data=0;
        while ((data=fr.read())!=-1){  // 读取一个字符不再是一个字节
            System.out.print((char) data);
        }
    }
}
```

#### 字符缓冲流

```java
public class Demo7 {
    public static void main(String[] args) throws IOException {
        // BufferedReader
        FileReader fileReader = new FileReader("test.txt");
        BufferedReader br = new BufferedReader(fileReader);
        // 第一种方法
//        char[] buf = new char[1024];
//        int count = 0;
//        while ((count=br.read(buf))!=-1)
//            System.out.println(new String(buf,0,count));
//        br.close();
        // 第二种方法（readLine()）
        String line = null;
        while ((line=br.readLine())!=null)
            System.out.println(line);
        br.close();

        FileWriter fileWriter = new FileWriter("test.txt");
        BufferedWriter bw = new BufferedWriter(fileWriter);
        for (int i = 0; i < 10; i++) {
            bw.write("你好！");
            bw.newLine();  // 写入一个换行符（如果是windows就是\r\n，linux是\n）
        }
        bw.close();
    }
}
```

#### 打印流

打印流可以在写入文件时原样写入

```java
public class Demo8 {
    public static void main(String[] args) throws FileNotFoundException {
        PrintWriter pw = new PrintWriter("test.txt");
        pw.println(1);
        pw.println(true);
        pw.print(1.1);
        pw.print('a');
        pw.close();
    }
}
```

#### 转换流

转换流可以将字节流转换为字符流，并且可以设置字符的编码方式

```java
public class Demo9 {
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("test.txt");
        InputStreamReader inputStreamReader = new InputStreamReader(fis, StandardCharsets.UTF_8);
        int data=0;
        while ((data= inputStreamReader.read())!=-1){
            System.out.print((char) data);
        }
    }
}
```

### 文件类（File）

File代表物理盘符中的一个文件或者一个文件夹

我们可以通过内部的方法访问文件的各个属性或创建文件

```java
public class Demo1 {
    static File file = new File("test.txt");  // 现在只是创建了一个文件对象，可以并没有文件

    public static void main(String[] args) throws IOException {
        separator();
        information();
        check();
        directoryOpen();
    }

    // 1. 文件分隔符
    public static void separator(){
        System.out.println("路径分隔符"+ File.pathSeparator);  // ';'
        System.out.println("名称分隔符"+ File.separator);  // '\'
    }

    // 2. 文件创建/删除
    public static void fileOpen() throws IOException {
        if (!file.exists()) {  // 也是用来判断文件是否存在
            boolean b = file.createNewFile();
            System.out.println("创建结果：" + b);  // 文件已经存在就返回false，否则创建一个新文件并返回true
        }
        boolean b = file.delete();  // 直接删除，返回方式和上面创建文件同理
        System.out.println("删除结果："+ b);
        file.deleteOnExit();  // 利用jvm在程序结束后删除文件
    }

    // 3. 获取文件信息
    public static void information(){
        System.out.println("文件的绝对路径：" + file.getAbsolutePath());
        System.out.println("定义时的路径：" + file.getPath());
        System.out.println("获取文件名称："+ file.getName());
        System.out.println("获取父目录："+ file.getParent());
        System.out.println("获取文件长度："+ file.length());
        System.out.println("文件的创建时间："+ new Date(file.lastModified()).toString());
    }

    // 4. 判断文件属性
    public static void check(){
        System.out.println("是否可写："+ file.canWrite());
        System.out.println("是否是文件："+ file.isFile());
        System.out.println("是否隐藏："+ file.isHidden());
    }

    // 5. 目录操作
    public static void directoryOpen(){
        // 创建文件夹
        File dir = new File("a\\b");  // dir指向最后一个目录
        if (!dir.exists())
            System.out.println("创建结果：" + dir.mkdirs());
        System.out.println("删除结果："+dir.delete());  // 删除的必须是空目录，同时只能删除最底层目录b
        dir.deleteOnExit();  // 同
        // 获取目录信息和判断和文件相同
        String[] files = dir.list();  // 返回目录下所有文件名称，是字符串数组
        if (files != null) {
            for (String s : files) {
                System.out.println(s);
            }
        }
    }
}
```

### 文件过滤器接口（FileFilter）

当调用`File`类中的`listFiles()`方法时，支持传入`FileFileter`接口的接口实现类，对获取的文件进行过滤，只有满足条件的文件才可以出现在`listFiles()`的返回值中

```java
public class Demo2 {
    public static void main(String[] args) {
        File file = new File("a\\b");
        File[] files = file.listFiles(pathname -> pathname.getName().endsWith(".jpg"));  // Lambda表达式
        assert files != null;
        for (File file1 : files) {
            System.out.println(file1.getName());
        }
    }
}
```

### 递归遍历文件夹

```java
public class Demo3 {
    public static void main(String[] args) {
        listDir(new File("a"));
    }

    public static void listDir(File dir){
        File[] files = dir.listFiles();
        System.out.println(dir.getAbsolutePath());
        if (files!=null && files.length>0){
            for (File file : files) {
                if (file.isDirectory()) listDir(file);
                else System.out.println(file.getAbsolutePath());
            }
        }
        // 同理也可以递归删除文件夹
    }
}
```

### Properties集合

相当于字典类型，存储的属性名和属性值都是字符串类型，存储内容和流有关，没有泛型

```java
public class Demo1 {
    public static void main(String[] args) throws IOException {
        Properties properties = new Properties();
        properties.setProperty("name","test");
        System.out.println(properties.toString());
        Set<String> proNames = properties.stringPropertyNames();
        for (String pro : proNames) {
            System.out.println(pro+"->"+properties.getProperty(pro));
        }
        // 通过打印流打印集合内容
        PrintWriter pw = new PrintWriter("test.txt");
        properties.list(pw);  // 传入一个打印流对象
        pw.close();
        // 通过文件输出流保存集合信息
        FileOutputStream fos = new FileOutputStream("test.txt");
        properties.store(fos,"comments");
        fos.close();
        // 通过输入流加载之前保存的集合信息
        Properties pro1 = new Properties();
        FileInputStream fis = new FileInputStream("test.txt");
        pro1.load(fis);
        fis.close();
        System.out.println(pro1.toString());
    }
}
```

## GUI编程

### AWT

包含了很多的类和接口

![image-20210314171920071](https://s2.loli.net/2021/12/05/MK7gHT1heNjuvwS.png)

#### 窗口（Frame）

```java
package com.GUI.test1;

import java.awt.*;

public class Demo2 {
    public static void main(String[] args) {
        MyFrame myFrame1 = new MyFrame(100, 100, 200, 200);
        MyFrame myFrame2 = new MyFrame(100, 300, 200, 200);
        MyFrame myFrame3 = new MyFrame(300, 100, 200, 200);
    }
}

class MyFrame extends Frame{
    static int id=0;  // 可能存在多个窗口，我们需要一个计数器
    public MyFrame(int x,int y, int w, int h){
        super("MyFrame "+ ++id);
        setVisible(true);  // 可见性
        setBounds(x,y,w,h);  // 快捷窗口大小
        setBackground(Color.pink);
    }
}
```

#### 面板（Panel）

面板是在容器里面的，可以看成一个空间，但是不能单独存在

面板的方法大多和窗口`Frame`一模一样（布局，大小等）

内容应该全部放在面板中执行，因为窗口是唯一的

```java
public class Demo3 {
    public static void main(String[] args) {
        Frame frame = new MyFrame(100,100,1000,500);
        Panel panel = new Panel();
        frame.setLayout(null);  // 设置布局
        panel.setBounds(100,100,100,100);
        panel.setBackground(new Color(127, 255, 152));
        frame.add(panel);
    }
}
```

#### 监听

Java内置了`WindowListener`监听器，但是直接使用的话会需要重写很多方法

```java
new WindowListener() {
    @Override
    public void windowOpened(WindowEvent e) {
        
    }

    @Override
    public void windowClosing(WindowEvent e) {

    }

    @Override
    public void windowClosed(WindowEvent e) {

    }

    @Override
    public void windowIconified(WindowEvent e) {

    }

    @Override
    public void windowDeiconified(WindowEvent e) {

    }

    @Override
    public void windowActivated(WindowEvent e) {

    }

    @Override
    public void windowDeactivated(WindowEvent e) {

    }
}
```

因此我们可以使用适配器模式快速添加想要的监听效果

```java
frame.addWindowListener(new WindowAdapter() {  // 适配器模式，是WindowListener的一个子类
    @Override
    public void windowClosing(WindowEvent e) {
        System.exit(0);
        super.windowClosing(e);
    }
});  // 监听事件（窗口关闭：System.exit(0)）
```

然而，`WindowListener`只能监听窗口动作，要监听别的事件需要`ActionListener`

同时我们可以通过判断一个元素的`ActionCommand`来通过同一个监听类执行不同按钮的不同命令

```java
public class Demo7 {
    public static void main(String[] args) {
        Frame frame = new Frame();
        Button button = new Button("test");
        button.setActionCommand("start");  // 设定命令，如果没写的话就默认Label值
        frame.setBounds(100,100,500,500);
        // 因为addActionListener()需要一个ActionListener，所以我们需要构造一个ActionListener
        MyActionListener myActionListener = new MyActionListener();
        button.addActionListener(myActionListener);
        frame.add(button,BorderLayout.CENTER);
        frame.setVisible(true);
        closeWindow(frame);  // 关闭窗口
    }

    private static void closeWindow(Frame frame){
        WindowAdapterIMPL windowAdapterIMPL = new WindowAdapterIMPL();
        frame.addWindowListener(windowAdapterIMPL);
    }
}

// 事件监听
class MyActionListener implements ActionListener{
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println(e.getActionCommand());  // 获得之前设置的命令动作名
    }
}

class WindowAdapterIMPL extends WindowAdapter{
    @Override
    public void windowClosing(WindowEvent e) {
        System.exit(0);
        // 也可以通过setVisible(false);隐藏窗口，但是不关闭进程
        super.windowClosing(e);
    }
}
```

#### 布局管理器

会发现上述代码中我们使用了一个布局管理器

```java
frame.setLayout(null);  // 设置布局
```

事实上，该方法还提供了很多种布局

- 流式布局

  ```java
  public class Demo4 {
      public static void main(String[] args) {
          MyFrame myFrame = new MyFrame(100,100,500,500);
          Button button = new Button("hi");
          button.setSize(200,200);
          myFrame.setLayout(new FlowLayout(FlowLayout.LEFT/*默认是CENTER*/));  // 流式布局
          myFrame.add(button);  // 尽管设定了200的大小，实际显示的大小还是按字数多少来
      }
  }
  ```

  从左到右排，排满了之后换下一行

  ![image-20210314185605795](https://s2.loli.net/2021/12/05/UKl1gdANDGqrT9O.png)

- 东西南北中

  ```java
  public class Demo5 {
      public static void main(String[] args) {
          MyFrame myFrame = new MyFrame(100,100,500,500);
          Button test1 = new Button("test");
          Button test2 = new Button("test");
          test1.setSize(200,100);
          myFrame.setLayout(new BorderLayout());
          myFrame.add(test1,BorderLayout.CENTER);
          myFrame.add(test2,BorderLayout.SOUTH);
      }
  }
  ```

  按钮会铺满整个屏幕

  ![image-20210314190317907](https://s2.loli.net/2021/12/05/pEw6tkg5r7nFqxK.png)

- 表格布局（Grid）

  ```java
  public class Demo6 {
      public static void main(String[] args) {
          MyFrame myFrame = new MyFrame(100, 100, 500, 500);
          Button test1 = new Button("test1");
          Button test2 = new Button("test2");
          Button test3 = new Button("test3");
          Button test4 = new Button("test4");
          Button test5 = new Button("test5");
          myFrame.setLayout(new GridLayout(3,2));  // 建立一个三行两列的表格
          myFrame.add(test1);
          myFrame.add(test2);
          myFrame.add(test3);
          myFrame.add(test4);
          myFrame.add(test5);
  
          myFrame.pack();  // 可以自动的选择最优秀的布局，是一个Java函数，使用后窗口变小了
      }
  }
  ```

  ![image-20210314191046586](https://s2.loli.net/2021/12/05/FlIijACQOMYB68V.png)

事实上，单个布局无论是哪一个都十分难看，所以实际开发中大多使用嵌套的方式进行布局

可以面板套面板，并在最后一层中添加按钮

#### 输入框（TextFIeld）

```java
public class Demo1 {
    public static void main(String[] args) {
        new MyFrame();
    }
}

class MyFrame extends Frame{
    public MyFrame() throws HeadlessException {
        TextField textField = new TextField();
        add(textField);
        setBounds(200,200,500,500);
        ActionListenerIMPL actionListenerIMPL = new ActionListenerIMPL();
        // 按下 enter 就会触发这个输入框的事件
        textField.addActionListener(actionListenerIMPL);
        textField.setEchoChar('*');  // 将输入的字母变成*
        setVisible(true);
        closeWindow(this);
    }

    private static void closeWindow(Frame frame){
        frame.addWindowListener(new WindowAdapterEXT());
    }
}

class ActionListenerIMPL implements ActionListener{
    @Override
    public void actionPerformed(ActionEvent e) {
        TextField content = (TextField) e.getSource();  // 会发现这是一个object类，可以强制类型转化
        System.out.println(content.getText());
        content.setText("");  // 按下回车后清空内容
    }
}

class WindowAdapterEXT extends WindowAdapter {
    @Override
    public void windowClosing(WindowEvent e) {
        System.exit(0);
        super.windowClosing(e);
    }
}
```

#### 组合和内部类

`oop`原则，组合大于继承

```java
class A extends B{}  // 继承
class A{
    public B b;  // 组合，在A类中私有B（用B类型定义b）
}
```

让我们开发一个计算器

```java
public class Demo2 {
    public static void main(String[] args) {
        new Calculator().loadFrame();
    }
}

class Calculator extends Frame {
    TextField num1, num2, num3;
    public void loadFrame(){
        num1 = new TextField(10);
        num2 = new TextField(10);
        num3 = new TextField(20);
        Button button = new Button("=");
        button.addActionListener(new MyCalculatorListener(this));
        Label label = new Label("+");  // 是一个标签，可以显示文字
        setLayout(new FlowLayout());
        setBounds(100,100,500,500);
        add(num1);
        add(label);
        add(num2);
        add(button);
        add(num3);
        setVisible(true);
        closeWindow(this);
    }

    private static void closeWindow(Frame frame){
        frame.addWindowListener(new WindowAdapterEXT());
    }

}

class MyCalculatorListener implements ActionListener{
    // 在一个类中组合另外一个类！可以使用这个类的所有属性和方法！
    Calculator calculator;

    public MyCalculatorListener(Calculator calculator) {
        this.calculator = calculator;
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        int n1 = Integer.parseInt(calculator.num1.getText());
        int n2 = Integer.parseInt(calculator.num2.getText());
        calculator.num3.setText(""+(n1+n2));
        calculator.num1.setText("");
        calculator.num2.setText("");
    }
}
```

```java
// 或者直接使用内部类，一步搞定，甚至不需要组合
// 直接复制到类Calculator内
private class MyCalculatorListener implements ActionListener{

    @Override
    public void actionPerformed(ActionEvent e) {
        int n1 = Integer.parseInt(num1.getText());
        int n2 = Integer.parseInt(num2.getText());
        num3.setText(""+(n1+n2));
        num1.setText("");
        num2.setText("");
    }
}
```

#### 画笔（Paint）

```java
public class Demo3 {
    public static void main(String[] args) {
        new MyPaint().loadFrame();
    }
}

class MyPaint extends Frame{

    public void loadFrame(){
        setBounds(200,200,500,500);
        setVisible(true);
        closeWindow();
    }

    private void closeWindow(){
        this.addWindowListener(new WindowAdapterEXT());
    }

    // 画笔
    @Override
    public void paint(Graphics g) {
        // 画笔，需要有颜色，画笔可以画画
        g.setColor(Color.red);
        g.fillOval(100,100,100,100);  // 实心的圆
        // g.drawOval(); 是空心的
    }
}
```

#### 监听鼠标事件

让我们实现用鼠标在窗口中画点

```java
public class Demo4 {
    public static void main(String[] args) {
        new MouseTest("Test");
    }
}

class MouseTest extends Frame{

    static ArrayList<Point> points;

    public MouseTest(String title) throws HeadlessException {
        super(title);
        setBounds(200,200,300,400);
        points = new ArrayList<>();
        setVisible(true);
        this.addMouseListener(new MyMouseListener());  // 会发现这个和窗口监听一样是一个接口，要重写很多类
        this.addWindowListener(new WindowAdapterEXT());
    }

    @Override
    public void paint(Graphics g) {
        Iterator<?> iterator;  // 迭代器
        iterator = points.iterator();
        while (iterator.hasNext()){
            Point next = (Point) iterator.next();
            g.setColor(Color.blue);
            g.fillOval(next.x,next.y,20,20);
        }
    }

    // 适配器模式
    private class MyMouseListener extends MouseAdapter {
        @Override
        public void mousePressed(MouseEvent e) {
            // 让我们点击的时候能够在界面上产生一个点
            // 这个点就是鼠标的点，e就是鼠标
            points.add(e.getPoint());
            // 每次点击鼠标都要重画一遍
            repaint();  // 调用父类方法
        }
    }
}
```

#### 监听键盘监听

```java
public class Demo5 {
    public static void main(String[] args) {
        new KeyTest();
    }
}

class KeyTest extends Frame{
    public KeyTest() throws HeadlessException {
        setBounds(100,100,500,500);
        setVisible(true);

        this.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                int keycode = e.getKeyCode();
                System.out.println(keycode);
                if (keycode==KeyEvent.VK_W){
                    System.out.println("W键");
                }
            }
        });
        
        addWindowListener(new WindowAdapterEXT());
    }
}
```

### Swing

`AWT`比`Swing`更底层，类似于一个框架，`Swing`在`AWT`的基础上可以实现更多的功能

#### 建立一个窗口和标签

```java
public class Demo1 {
    // init() 初始化
    public void init(){
        JFrame frame = new JFrame("这是一个JFrame窗口");
        frame.setVisible(true);
        frame.setBounds(100,100,300,300);
        // 设置文字 JLabel
        JLabel jLabel = new JLabel("Hello");
        frame.add(jLabel);
        // 文本居中
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);  // 水平对齐+常量居中
        // 设置背景色
        // 获得一个容器，容器里面的颜色才是他自己的颜色
        // 所有元素放在容器中，同时容器不需要被add进JFrame窗口中
        Container contentPane = frame.getContentPane();
        contentPane.setBackground(Color.yellow);
        // 关闭事件
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);  // 高级的关闭方法
    }

    public static void main(String[] args) {
        // 建立一个窗口
        new Demo1().init();
    }
}
```

#### 弹窗

```java
// 主窗口
public class Demo2 extends JFrame {

    public Demo2() throws HeadlessException {
        this.setVisible(true);  // 涉及两个窗口，必须要用this
        this.setBounds(100,100,700,500);
        // 容器
        Container contentPane = this.getContentPane();
        contentPane.setLayout(null);  // 绝对定位

        JButton jButton = new JButton("点击弹出一个对话框");
        jButton.setBounds(30,30,200,50);
        contentPane.add(jButton);
        // 点击按钮的时候弹出一个弹窗
        jButton.addActionListener(e -> new DialogEXT());
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new Demo2();
    }
}

// 弹窗
class DialogEXT extends JDialog{
    public DialogEXT() {
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        // 注意默认状态下弹窗就有关闭事件，可以不设定

        Container contentPane = this.getContentPane();
        contentPane.setLayout(null);
        JLabel label = new JLabel("Hello");
        label.setBounds(100,100,200,200);
        label.setHorizontalAlignment(SwingConstants.CENTER);
        label.setOpaque(true);  // 想给标签设定颜色就得先把透明度调了
        label.setBackground(Color.black);
        contentPane.add(label);
    }
}
```

#### 图标

```java
// 同时继承类和图标接口
public class Demo3 extends JFrame implements Icon {

    private int width;
    private int height;

    public Demo3() throws HeadlessException {
    }

    public void init(){
        Demo3 demo3 = new Demo3(15,15);  // 定义一个图标
        // 图标放在标签上，也可以放在按钮上
        JLabel icon = new JLabel("icon", demo3, SwingConstants.CENTER);
        Container contentPane = getContentPane();
        contentPane.add(icon);
        contentPane.setVisible(true);
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public Demo3(int width, int height) throws HeadlessException {
        this.width = width;
        this.height = height;
    }

    public static void main(String[] args) {
        new Demo3().init();
    }

    // 重写三个接口方法
    @Override
    public void paintIcon(Component c, Graphics g, int x, int y) {
        g.fillOval(x,y,width,height);
    }

    @Override
    public int getIconWidth() {
        return this.width;
    }

    @Override
    public int getIconHeight() {
        return this.height;
    }
}
```

#### 图片

```java
public class Demo4 extends JFrame {

    public Demo4() throws HeadlessException {
        JLabel label = new JLabel("ImageIcon");
        URL url = Demo4.class.getResource("test.jpg");  // 获取当前这个类的下面图片资源，返回的url是一个绝对路径
        ImageIcon imageIcon = new ImageIcon(url);  // 利用图片对象保存url
        label.setIcon(imageIcon);
        label.setHorizontalAlignment(SwingConstants.CENTER);
        Container contentPane = this.getContentPane();
        contentPane.add(label);
        setVisible(true);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        setBounds(100,100,400,400);
    }

    public static void main(String[] args) {
        new Demo4();
    }
}
```

#### 面板

```java
public class Demo5 extends JFrame {

    public Demo5() throws HeadlessException {
        Container contentPane = this.getContentPane();
        contentPane.setLayout(new GridLayout(2,1,10,10));  // 表格布局，后面参数代表元素之间间距
        JPanel jPanel = new JPanel(new GridLayout(1,3,10,10));
        jPanel.add(new JButton("1"));
        jPanel.add(new JButton("1"));
        jPanel.add(new JButton("1"));
        contentPane.add(jPanel);
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new Demo5();
    }
    
}
```

#### 滚动条

```java
public class Demo6 extends JFrame{

    public Demo6() throws HeadlessException {
        Container contentPane = getContentPane();
        
        // 文本域，支持换行
        JTextArea jTextArea = new JTextArea(20,50);
        jTextArea.setText("Hello");

        // Scroll面板
        JScrollPane jScrollPane = new JScrollPane(jTextArea);
        contentPane.add(jScrollPane);
        setVisible(true);
        setBounds(100,100,200,200);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new Demo6();
    }
}
```

![image-20210319001948117](https://s2.loli.net/2021/12/05/2FqeYHLOVcp41ER.png "滚动条")

#### 按钮

- 图片按钮

  ```java
  public class Demo7 extends JFrame {
      public Demo7() throws HeadlessException {
          Container contentPane = this.getContentPane();
          URL resource = Demo7.class.getResource("test.jpg");
          ImageIcon imageIcon = new ImageIcon(resource);
          contentPane.setLayout(null);  // 利用绝对定位防止按钮占满整个屏幕
  
          JButton jButton = new JButton();
          jButton.setIcon(imageIcon);
          jButton.setToolTipText("鼠标放上时弹出的提示文本");
          jButton.setText("按钮文本");
          jButton.setBounds(100,100,600,300);
          jButton.setHorizontalAlignment(SwingConstants.CENTER);
          contentPane.add(jButton);
          this.setVisible(true);
          this.setBounds(100,100,1000,500);
          this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo7();
      }
  }
  ```

  ![image-20210319091410202](https://s2.loli.net/2021/12/05/HeRCTDQWBUlMGny.png "图片按钮")

- 单选按钮

  ```java
  public class Demo8 extends JFrame {
      public Demo8() throws HeadlessException {
          Container contentPane = getContentPane();
          contentPane.setLayout(new FlowLayout());
  
          JRadioButton jB1 = new JRadioButton("1");
          JRadioButton jB2 = new JRadioButton("2");
          JRadioButton jB3 = new JRadioButton("3");
  
          // 由于单选框只能选一个，要对以上单选框打组
          ButtonGroup buttonGroup = new ButtonGroup();
          buttonGroup.add(jB1);
          buttonGroup.add(jB2);
          buttonGroup.add(jB3);
  
          contentPane.add(jB1);  // 注意不能直接添加一个组
          contentPane.add(jB2);
          contentPane.add(jB3);
  
          this.setVisible(true);
          this.setBounds(100,100,300,300);
          this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo8();
      }
  }
  ```

- 多选框

  将单选框改成`JCheckBox`即可，同时注意不需要打组了

#### 列表

- 下拉框

  ```java
  public class Demo9 extends JFrame {
  
      public Demo9() throws HeadlessException {
          Container contentPane = getContentPane();
          JPanel jPanel = new JPanel();  // 一般都会放在一个面板中
          jPanel.setBounds(50,50,100,10);
  
          JComboBox<Object> objectJComboBox = new JComboBox<>();
          objectJComboBox.addItem("hello");
          objectJComboBox.addItem("hi");
          objectJComboBox.addItem("good");
  
          jPanel.add(objectJComboBox);
          contentPane.add(jPanel);
  
          setVisible(true);
          setBounds(100,100,200,200);
          setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo9();
      }
  }
  ```

- 列表框

  ```java
  public class Demo10 extends JFrame {
  
      public Demo10() throws HeadlessException {
          Container contentPane = getContentPane();
  
          String[] contents = {"1","2","3"};
          JList<Object> objectJList = new JList<>(contents);
  
          contentPane.add(objectJList);
  
          setVisible(true);
          setBounds(100,100,200,200);
          setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo10();
      }
  }
  ```

#### 文本框

```java
public class Demo11 extends JFrame {

    public Demo11() throws HeadlessException {
        Container contentPane = getContentPane();
        contentPane.setLayout(new GridLayout(3,1));

        // 文本框
        JTextField textField = new JTextField("文本框");

        // 密码框
        JPasswordField passwordField = new JPasswordField("密码框");

        // 文本域
        JTextArea textArea = new JTextArea("文本域");

        contentPane.add(textField);
        contentPane.add(passwordField);
        contentPane.add(textArea);

        setVisible(true);
        setBounds(100,100,1000,500);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }

    public static void main(String[] args) {
        new Demo11();
    }
}
```

![image-20210319095630633](https://s2.loli.net/2021/12/05/AiND51PuT6H4yVv.png)

注意到文本框和密码框默认都是居中，且无法换行，文本域顶格

### 贪吃蛇

制作一个贪吃蛇，我们首先需要对其中的界面进行分析

- 一个窗口
- 一个面板用来承载所有元素
- 一个画笔画出元素
- 图片素材

然后我们要制订完成的步骤

1. 画上总体的界面
2. 绘制小蛇
3. 使小蛇随时间运动
4. 使小蛇随键盘转弯
5. 放置食物
6. 失败判定

对于每一个步骤，我们都可以对其进行机械化操作

1. 定义数据
2. 画上去
3. 监听事件（键盘，事件）

## 多线程初步

### 简介

在操作系统中运行的程序就是进程，一个进程可以有多个线程，比如一个视频可以同时听声音，看图像，看弹幕等等，多线程就是一台机器同时完成多个任务

进程等于是一个保护伞，各种各样的线程在进程内跑，线程是`CPU`调度和执行的单位

我们知道程序执行的时候会先执行`main()`函数，这就说明`main()`函数是程序的主线程

除了主线程之外，还有一个`gc()`线程主要负责垃圾回收

事实上，一个`CPU`还是只能执行一个代码，所以我们模拟多线程就是使`CPU`迅速切换执行代码

在一个进程中，如果开辟了多个线程，线程的运行由调度器安排调度，调度器是与操作系统紧密相关的，先后顺序不能人为干预

对同一份资源进行操作时，会存在资源抢夺的问题，需要加入并发控制

> 不能让资源被同时抢夺，让抢夺资源的线程排好队一个一个来

### 线程创建

创建线程有两种方法

- 继承`Thread`类方法

  ```java
  // 创建线程方式1，继承
  public class Demo1 extends Thread{
      @Override
      public void run() {
          // run方法线程体
          for (int i = 0; i < 5; i++) {
              System.out.println("Looking..."+i);
          }
      }
  
      public static void main(String[] args) {
          // main线程，主线程
          // 创建一个线程对象
          Demo1 demo1 = new Demo1();
          // 调用start()方法开启线程
          demo1.start();
          for (int i = 0; i < 5; i++) {
              System.out.println("Studying..."+i);
          }
      }
  }
  ```

  ![image-20210321165300770](https://s2.loli.net/2021/12/05/zcljsOe2gaWSKCH.png "多线程执行模式")

  如果不使用`start`方法而是直接使用`run()`调用就不会进行多线程操作了

### 尝试用多线程下载网图

网络上下载`commons-io.jar`复制后粘贴到项目中新建的`lib`目录下，并且右击添加到库

![image-20210403192636438](https://s2.loli.net/2021/12/05/P8eOvSAI1wl9Guf.png "添加库")

```java
public class Demo2 extends Thread{
    private String url;
    private String name;

    public Demo2(String url, String name){
        this.url = url;
        this.name = name;
    }

    @Override
    public void run() {
        WebDownloader webDownloader = new WebDownloader();
        webDownloader.downloader(url, name);
        System.out.println("下载的文件名为:"+name);
    }

    public static void main(String[] args) {
        Demo2 j1 = new Demo2("https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2458053954,3888878830&fm=26&gp=0.jpg", "1.jpg");
        Demo2 j2 = new Demo2("https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2458053954,3888878830&fm=26&gp=0.jpg", "2.jpg");
        Demo2 j3 = new Demo2("https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2458053954,3888878830&fm=26&gp=0.jpg", "3.jpg");

        j1.start();
        j2.start();
        j3.start();
    }
}

class WebDownloader{
    public void downloader(String url, String name){
        try {
            FileUtils.copyURLToFile(new URL(url),new File(name));  // 把一个url变成一个文件
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("IO异常,downloader方法出现问题");
        }
    }
}
```

### 实现Runnable接口

和`Thread`类整体差不多，但是是一个接口

```java
public class Demo3 implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Looking..."+i);
        }
    }

    public static void main(String[] args) {
        // 创建runnable接口的实现类对象
        Demo3 demo3 = new Demo3();
        // 创建线程对象，通过线程对象来开启我们的线程（代理）
        Thread thread = new Thread(demo3);
        thread.start();
        for (int i = 0; i < 5; i++) {
            System.out.println("Studying..."+i);
        }
    }
}
```

事实上`Thread`类也实现了`Runnable`接口，推荐使用`Runnable`，因为Java要避免单继承的局限性

### 多个线程运行同一操作

```java
public class Demo4 implements Runnable{

    private int ticketNum = 10;

    @Override
    public void run() {
        while (ticketNum > 0) {
            System.out.println(Thread.currentThread().getName() + "-->拿到了第" + ticketNum-- + "张票");
        }
    }

    public static void main(String[] args) {
        Demo4 tickets = new Demo4();
        new Thread(tickets,"1").start();
        new Thread(tickets,"2").start();
        new Thread(tickets,"3").start();
    }
}
```

![image-20210403201546436](https://s2.loli.net/2021/12/05/hGpM2DkZH5En3ru.png "拿票模拟")

事实上，当多个线程操作同一个资源的情况下，线程不安全了，数据紊乱

比如可能遇到某两个人拿到了同一张票的情况（上图无体现，但可以看出数据顺序出现问题）

这就涉及到并发的问题

### 代理

静态代理模式，就是代理对象和真实对象都实现同一个接口

代理对象要代理真实角色，同时代理对象可以实现很多真实角色实现不了的事情，而真实对象只需要专注于做自己的事情

以上一部分代码为例，`Thread`就是代理对象，我们实现的接口类就是真实对象

我们先通过接口实现一个对象，再用代理对象`Thread`传入真实对象，通过`Thread`类的方法来实现真实对象本身实现不了的操作

真实对象就是我们个人，代理对象就是专门做某件事的公司，我们个人也可以做这件事，但是好麻烦，于是我们把这件事交给公司来专业方便的实现

### Lambda表达式

`Lambda`表达式实际上简化了我们的表达式

#### 使用原因

- 避免匿名内部类定义过多
- 可以让一些代码看上去更加简洁
- 去掉了一堆没有意义的代码，只留下核心的逻辑

#### 函数式接口

任何接口，如果只包含唯一一个抽象方法，那么他就是一个函数式接口

```java
// 官方定义的Runnable接口
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface {@code Runnable} is used
     * to create a thread, starting the thread causes the object's
     * {@code run} method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method {@code run} is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```

对于函数式接口，我们可以 通过`Lambda`表达式来创建该接口的对象

#### 怎么演化的

```java
// 1.这是一个函数式接口
interface TestInterface{
    void test();
}

// 2.这是一个平常的实现类
class TestInterface1 implements TestInterface{
    @Override
    public void test() {
        System.out.println("实现类");
    }
}

public class Demo5 {
    
    // 3.这是一个静态内部类
    static class TestInterface2 implements TestInterface{
        @Override
        public void test() {
            System.out.println("静态内部类");
        }
    }

    public static void main(String[] args) {
        TestInterface test;
        test = new TestInterface1();
        test.test();
        test = new TestInterface2();
        test.test();
        
        // 4.这是一个局部内部类

        class TestInterface3 implements TestInterface{
            @Override
            public void test() {
                System.out.println("局部内部类");
            }
        }
        test = new TestInterface3();
        test.test();
        
        // 5.是一个匿名内部类，没有类的名称，必须借助接口或者父类
        test = new TestInterface(){
            @Override
            public void test() {
                System.out.println("匿名内部类");
            }
        };
        test.test();
        
        // 6.这是利用lambda表达式
        test = ()-> System.out.println("lambda表达式");
        test.test();
    }
}
```

由上述可以看出`lambda`表达式对于代码的简化，不过注意到首先要保证`test`是一个函数式接口类型

如果接口类存在参数，就把`()`改成一个参数名称即可

> 如：`test = a->sout("hi "+ a);`
>
> 注意到甚至不需要定义a的类型，前提是接口当中已经定义了a

### 线程状态

![image-20210407163233804](https://s2.loli.net/2021/12/05/LznEwQY8F4ItXTS.png)

#### 线程停止

- 不推荐使用JDK使用的`stop()`、`destory()`方法
- 推荐让线程自己停下来，例如利用次数
- 建议使用一个标志位进行终止变量，当`flag=false`时，终止线程运行

```java
public class Demo6 implements Runnable{

    private boolean flag = true;

    @Override
    public void run() {
        int i = 0;
        while (flag){
            System.out.println("run...Thread"+i++);
        }
    }

    public void stop(){
        this.flag = false;
    }

    public static void main(String[] args) {
        Demo6 demo6 = new Demo6();
        new Thread(demo6).start();
        for (int i = 0; i < 1000; i++) {
            System.out.println("main"+i);
            if (i==900){
                // 调用stop方法切换标志位，让线程停止
                demo6.stop();
                System.out.println("线程停止");
            }
        }
    }
}
```

#### 线程休眠

利用`sleep()`方法令线程进行休眠，模拟网络延时，放大问题的发生性

同时记住每一个对象都有一把锁，`sleep()`不会释放锁

```java
// 获取系统当前时间
public class Demo7 {
    public static void main(String[] args) {
        while (true) {
            try {
                Date date = new Date(System.currentTimeMillis());
                Thread.sleep(1000);
                System.out.println(new SimpleDateFormat("HH:mm:ss").format(date));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### 线程礼让

- 礼让线程，让当前正在执行的线程暂停，但不阻塞
- 让线程从运行状态转为就绪状态
- 继而让`cpu`重新调度，但是注意礼让不一定成功，看`cpu`心情

```java
public class Demo8 {
    static class MyYield implements Runnable{

        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName()+" 线程开始执行");
            // if (Thread.currentThread().getName().equals("a")) Thread.yield();  // 礼让
            System.out.println(Thread.currentThread().getName()+" 线程停止执行");
        }
    }

    public static void main(String[] args) {
        MyYield myYield = new MyYield();
        new Thread(myYield,"a").start();
        new Thread(myYield,"b").start();
    }
}
```

#### 线程合并

通过`join`合并进程，待此线程执行完之后再执行其他线程，执行`join`线程时其他线程阻塞（插队）

```java
public class Demo9 implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("插入线程 " + i);
        }
    }

    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            System.out.println("主线程 " + i);
            if (i == 50){
                Thread thread = new Thread(new Demo9());
                thread.start();
                try {
                    thread.join();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

#### 查看线程状态

通过`Thread.State`查看线程状态

- `NEW` 线程尚未启动
- `RUNNABLE`线程处于就绪状态
- `BLOCKED`线程被阻塞并正在等待监视器锁定
- `WAITING`该线程正在等待另一个线程执行
- `TIMED_WAITING`等待另一个线程执行动作达到指定等待时间（`sleep`）
- `TERMINATED`已退出的线程

#### 线程优先级

Java提供一个线程调度器来监控程序中启动后进入就绪状态的所有线程，线程调度器按照优先级决定应该先调度那个线程来执行

线程的优先级用数字表示，范围从1~10，其中

- `Thread.MIN_PRIORITY = 1`
- `Thread.MAX_PRIORITY = 10`
- `Thread.NORM_PRIORITY = 5`

同时我们可以通过`getPriority()`和`setPriority(int x)`来改变或获取优先级

优先级高的只是大概率先执行，权重比较大，事实上小概率也会让优先级低的先执行

#### 守护线程

线程分为用户线程和守护线程

虚拟机必须确保用户线程执行完毕（`main()`）

但是虚拟机不用等待守护线程执行完毕（`gc()`）

守护线程可以在后台记录操作日志，监控内存，垃圾回收等等

```java
public class Demo10 {
    public static void main(String[] args) {
        Daemons daemons = new Daemons();
        Users users = new Users();

        Thread thread1 = new Thread(new Daemons());
        Thread thread2 = new Thread(new Users());

        thread1.setDaemon(true);  // 默认false表示用户线程

        thread1.start();
        thread2.start();
    }
}

class Daemons implements Runnable{
    @Override
    public void run() {
        while (true) System.out.println("守护线程");
    }
}

class Users implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("用户线程");
        }
    }
}
```

### 线程同步

线程同步就是同一个对象被多个线程操作

但是如同之前编的代码一样，当同一个资源多个人都想使用的时候，这个资源可能会被重复使用

因此，处理多线程问题时，多个线程访问同一对象，并且某些线程还想修改这个对象，这时我们需要线程同步，线程同步就是一种等待机制，多个需要同时访问此对象的线程进入这个**对象的等待池**形成队列，等待前面的线程使用完毕，下一个线程再使用

#### 锁

面对线程同步时，必须使用**队列+锁**的机制

为了保证数据在方法中被访问时的正确性，在访问中加入了锁机制（synchronized）

当一个线程获得对象的排他锁，独占资源，其他线程必须等待，使用后释放锁即可，同时注意

- 当一个线程持有锁会导致其他所有需要锁的线程挂起
- 在多线程的竞争下，加锁，释放锁会导致比较多的上下文切换和调度延时，引起性能问题
- 如果一个优先级高的线程等待一个优先级低的线程释放锁，会导致优先级倒置，引起性能问题

线程同步一定会损失性能，但是保证了安全性

通过对方法加入`synchronized`关键字控制对对象的访问，每个对象对应一把锁，每个`synchronized`方法都必须获得调用该方法的对象的锁才能执行，否则线程阻塞

注意，若将一个大的方法申明为`synchronized`将会影响效率

所以一般来说，我们会使用`synchronized(Obj){}`块

- 其中`Obj`是一个监视器，可以是任何对象，但是推荐使用共享资源作为同步监视器
- 同步方法中无需指定同步监视器，因为同步方法的同步监视器就是`this`这个对象本身

```java
public class Demo1 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                synchronized (list){
                    list.add(Thread.currentThread().getName());  // 对list加锁
                }
            }).start();
        }
        System.out.println(list.size());
    }
}
// 该程序可能还出现并不会显示完所有内容，其实是因为list线程和主线程一起在跑，可能主线程跑完了list线程还没跑完但程序直接结束了，因为start()之后并不会马上执行某线程
// 只需要在结尾休眠一会即可
```

多个线程进行同一操作，就在同一操作中添加锁

#### JUC并发包

JUC是别人写好的专门用来做并发编程的包，可以省去加锁过程

可以把上述代码的`List<>`改成`CopyOnWriteArrayList<>`安全列表

#### 死锁

多个线程各自占有一些共享资源，并且互相等待其他线程占有的资源才能运行

但是如果遇到两个线程互相在等待对方释放资源，都停止执行就会发生死锁现象

重点是一个锁还没执行完就想要获得另一个锁

```java
public class Demo2 {
    public static void main(String[] args) {
        DeadLock test1 = new DeadLock(0, "test1");
        DeadLock test2 = new DeadLock(1, "test2");
        new Thread(test1).start();
        new Thread(test2).start();
    }
}

class Lock1 {}
class Lock2 {}

class DeadLock implements Runnable{

    // 保证需要的资源只有一份
    static Lock1 lock1 = new Lock1();
    static Lock2 lock2 = new Lock2();

    int o;
    String name;

    public DeadLock(int o, String name) {
        this.o = o;
        this.name = name;
    }

    @Override
    public void run() {
        try {
            deadLock();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    private void deadLock() throws InterruptedException{
        if (this.o == 0){
            synchronized (lock1){
                System.out.println(this.name + " acquire lock1");
                Thread.sleep(1000);
                synchronized (lock2){
                    System.out.println(this.name + " acquire lock2");
                }
            }
        }
        else {
            synchronized (lock2){
                System.out.println(this.name + " acquire lock2");
                Thread.sleep(1000);
                synchronized (lock1){
                    System.out.println(this.name + " acquire lock1");
                }
            }
        }
    }

}
```

#### Lock锁

`Lock`接口存在于`java.util.concurrent.locks`中，提供了对共享资源的独占访问

- `ReentrantLock`类实现了`Lock`接口，拥有与`synchronized`相同的并发性和内存语义
- 同时可以显式加锁，释放锁

```java
public class Demo3 implements Runnable{

    int tickets = 10;
    // 定义Lock锁，推荐的定义方法
    private final ReentrantLock lock = new ReentrantLock();

    @Override
    public void run(){
        while (true){
            try {
                lock.lock();  // 加锁
                if (tickets > 0) {
                    System.out.println(tickets--);
                } else {
                    break;
                }
            }finally {
                lock.unlock();  // 解锁
            }
        }
    }

    public static void main(String[] args) {
        Demo3 demo3 = new Demo3();

        new Thread(demo3).start();
        new Thread(demo3).start();
        new Thread(demo3).start();
    }
}
```

`synchronized`和`Lock`对比

- `Lock`是显性锁（手动开启和关闭锁），`synchronized`是隐性锁，出了自动域自动释放

- `Lock`只有代码块锁，`synchronized`有代码块锁和方法锁
- `Lock`锁性能更好，并且具有更好的扩展性（提供有更多的子类）
- 优先使用顺序
  - `Lock`>同步代码块（已经进入方法体，分配了相应资源）>同步方法（在方法体外）

### 线程协作

可以看作生产者和消费者模型，首先由生产者生产东西，生产中消费者处于等待状态

生产完成后通知消费者，消费者消费东西，让生产者等待，往复循环

```java
// 管程法

public class Demo4 {
    public static void main(String[] args) {
        SynContainer container = new SynContainer();

        new Producer(container).start();
        new Consumer(container).start();
    }
}

// 生产者
class Producer extends Thread {
    SynContainer container;

    public Producer(SynContainer container) {
        this.container = container;
    }
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            container.push(new Product(i));
            System.out.println("生产了 " + i);
        }
    }
}

// 消费者
class Consumer extends Thread{
    SynContainer container;

    public Consumer(SynContainer container) {
        this.container = container;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("消费了 "+container.pop().id);
        }
    }
}

// 产品
class Product{
    int id;

    public Product(int id) {
        this.id = id;
    }
}

// 缓冲区
class SynContainer{
    // 需要一个容器大小
    Product[] products = new Product[10];
    int count = 0;

    // 生产者放入产品
    public synchronized void push(Product product){
        while (count == products.length){
            // 生产等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        // 没有满，丢入商品
        products[count] = product;
        count++;
        // notifyAll就是通知wait的方法不用等待了
        this.notifyAll();
    }

    public synchronized Product pop(){
        while (count==0){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        count--;
        this.notifyAll();
        return products[count];
    }
}
```

```java
// 信号灯法，等于为1的管程法
public class Demo5 {
    public static void main(String[] args) {
        TV tv = new TV();
        new Player(tv).start();
        new Watcher(tv).start();
    }
}

class Player extends Thread{
    TV tv;

    public Player(TV tv) {
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            this.tv.play("节目 "+i);
        }
    }
}

class Watcher extends Thread{
    TV tv;

    public Watcher(TV tv) {
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            this.tv.watch();
        }
    }
}

class TV{
    String voice;
    boolean flag = true;

    public synchronized void play(String voice){
        if (!flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        System.out.println("表演 "+voice);
        this.notifyAll();
        this.voice = voice;
        this.flag = !this.flag;
    }

    public synchronized void watch(){
        if (flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("观看 "+voice);
        this.notifyAll();
        this.flag = !this.flag;
    }
}
```

### 线程池

经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能影响很大

我们可以提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中，可以避免频繁创建和销毁线程，实现重复使用

- 可以提高响应速度
- 降低资源消耗
- 便于线程管理
  - `corePoolSize` 核心池的大小
  - `maximumPoolSize` 最大线程数
  - `keepAliveTime` 线程没有任务时最多保持多长时间后终止

```java
public class Demo6 {

    static class MyThread implements Runnable{

        @Override
        public void run() {
            for (int i = 0; i < 100; i++) {
                System.out.println(Thread.currentThread().getName()+i);
            }
        }
    }

    public static void main(String[] args) {
        // 创建服务，创建线程池，参数为线程池大小
        ExecutorService service = Executors.newFixedThreadPool(10);
        service.execute(new MyThread());
        service.execute(new MyThread());
    }
}
```

## 网络编程

网络编程主要针对的是传输层内容（TCP，UDP）

Java中网络编程相关类都封装在`java.net`包中

### IP

`cmd`中`ipconfig`获得的都是我们的局域网ip，公网ip是看不到的

公网（互联网）-私网（局域网）

- 192.168.xx.xx 一般都是局域网，专门给组织内部使用的

```java
public class Demo1 {
    public static void main(String[] args) {
        try {
            // 发现这个类没有构造方法，不能new出来
            InetAddress inetAddress;
            inetAddress = InetAddress.getByName("127.0.0.1");
            System.out.println(inetAddress);
            inetAddress = InetAddress.getByName("localhost");
            System.out.println(inetAddress);
            inetAddress = InetAddress.getLocalHost();
            System.out.println(inetAddress);
            // 三种方法获得本机ip
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }
}
```

### 端口

端口表示的是计算机中一个程序的进程，不同的进程有不同的端口号

端口分为TCP端口和UDP端口，每一协议都有65535个端口

端口分类：

- 公有端口 0~1023（尽量不要占用）
  - HTTP : 80
  - HTTPS : 443
  - FTP : 21
  - Telent : 23
- 程序注册端口 1024~49151，主要给用户或者程序使用
  - Tomcat : 8080
  - MySQL : 3306
  - Oracle : 1521
- 动态，私有端口 49152~65535（也尽量不要用）

CMD中通过`netstat -ano`查看所有端口，通过`tasklist`查看所有进程（任务管理器也可）

```java
// 存放一个ip+端口
public class Demo2 {
    public static void main(String[] args) {
        InetSocketAddress inetSocketAddress = new InetSocketAddress("127.0.0.1", 8080);
        System.out.println(inetSocketAddress);
    }
}
```

### 通信协议

网络通信协议非常的复杂，我们需要对他进行分层

TCP/IP协议簇，实际上是一组协议

- TCP: 用户传输协议
- UCP: 用户数据报协议
- IP: 网络互联协议

TCP协议可以看作打电话，运用了**三次握手 四次分手**两者进行连接比较稳定，分为客户端为服务端，传输完成自动释放连接，效率比较低

UDP协议相当于发短信，不连接不稳定，客户端和服务端没有明确的界限，不管有没有准备好，都可以发给你，效率高（DDOS: 洪水攻击）

### TCP实现传输数据

```java
// 服务端
public class ServerTest {
    public static void main(String[] args) throws IOException {
        // 服务器应该有一个地址
        ServerSocket serverSocket = new ServerSocket(9999); // 网络编程也叫做套接字编程
        // 监听 等待客户端连接
        Socket socket = serverSocket.accept();
        // 读取客户端消息
        InputStream is = socket.getInputStream();
        // 管道流 让输入流通过管道接一下再输出
        ByteArrayOutputStream pipeOs = new ByteArrayOutputStream();
        byte[] bytes = new byte[1024];
        int len;
        while ((len=is.read(bytes))!=-1){
            pipeOs.write(bytes,0,len);
        }
        System.out.println(pipeOs.toString());
        // 通知客户端已经接收完毕
        OutputStream os = socket.getOutputStream();
        os.write("done".getBytes(StandardCharsets.UTF_8));
        // 关闭资源
        pipeOs.close();
        is.close();
        socket.close();
        serverSocket.close();
    }
}

// 客户端
public class ClientTest {
    public static void main(String[] args) throws IOException {
        // 要知道服务器的地址
        InetAddress byName = InetAddress.getByName("127.0.0.1");
        int port = 9999;
        Socket socket = new Socket(byName, port);
        // 发送消息 IO流
        OutputStream os = socket.getOutputStream();
        os.write("hi".getBytes(StandardCharsets.UTF_8));
        // 通知服务器已经结束
        socket.shutdownOutput();
        // 确认服务器接收完毕，断开连接
        InputStream inputStream = socket.getInputStream();
        // 接收服务器发来的确认数据
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
        byte[] bytes = new byte[1024];
        int len;
        while ((len=inputStream.read(bytes))!=-1)
            byteArrayOutputStream.write(bytes,0,len);
        System.out.println(byteArrayOutputStream.toString());
        // 关闭服务
        byteArrayOutputStream.close();
        inputStream.close();
        os.close();
        socket.close();
    }
}
```

### 文件上传

将上述代码的`Byte`改成`File`即可

同时注意在客户端上传文件时要先使用`FileInputStream`导入文件内容

```java
FileInputStream fileInputStream = new FileInputStream(new File("test.jpg"));
byte[] buffer = new byte[1024];
int len1;
while ((len1=fileInputStream.read(buffer))!=-1){
    os.write(buffer,0,len1);  // 输出文件
}
```

### Tomcat

 `Tomcat`即是一种`B/S`架构，是我们本地通过浏览器与`Tomcat`服务器进行通信

### UDP

`UDP`发送数据不需要连接服务器，只需要知道对方的地址

```java
// 发送端
public class UDPClientTest {
    public static void main(String[] args) throws Exception {
        // 建立一个Socket，随机指定一个端口
        DatagramSocket socket = new DatagramSocket();
        // 建立一个包
        String msg = "Hello";
        // 发送给谁
        InetAddress localhost = InetAddress.getByName("127.0.0.1");
        int port = 9999;
        // 数据，数据的长度，发送给谁
        DatagramPacket packet = new DatagramPacket(msg.getBytes(), 0, msg.getBytes().length, localhost, port);
        // 发送包
        socket.send(packet);
        socket.close();
    }
  
// 接收端    
public class UDPServerTest {
    // 其实这并不是服务端，哪一边都可以直接发送数据
    public static void main(String[] args) throws Exception {
        // 开放端口
        DatagramSocket socket = new DatagramSocket(9999);
        // 接收数据包
        byte[] bytes = new byte[1024];
        DatagramPacket datagramPacket = new DatagramPacket(bytes, 0, bytes.length);
        socket.receive(datagramPacket);  // 阻塞接收
        System.out.println(datagramPacket.getPort());
        System.out.println(new String(datagramPacket.getData(),0,datagramPacket.getLength()));
    }
}
```

#### 基于多线程UDP在线会话

```java
// 发送端
public class UDPSendTest implements Runnable {
    DatagramSocket socket;
    BufferedReader reader;

    int myPort;
    String toIP;
    int toPort;

    public UDPSendTest(int myPort, String toIP, int toPort) throws SocketException {
        this.myPort = myPort;
        this.toIP = toIP;
        this.toPort = toPort;

        this.socket = new DatagramSocket(myPort);
        this.reader = new BufferedReader(new InputStreamReader(System.in));
    }

    @Override
    public void run(){
        while (true){
            String s = null;
            try {
                s = this.reader.readLine();
            } catch (IOException e) {
                e.printStackTrace();
            }
            assert s != null;
            byte[] bytes = s.getBytes();
            DatagramPacket packet = new DatagramPacket(bytes, 0, bytes.length, new InetSocketAddress(this.toIP, this.toPort));
            try {
                this.socket.send(packet);
            } catch (IOException e) {
                e.printStackTrace();
            }
            if (s.equals("Done")) break;
        }
        this.socket.close();
    }
}
```

```java
// 接收端
public class UDPReceiveTest implements Runnable{
    DatagramSocket socket;
    int port;

    public UDPReceiveTest(int port) throws SocketException {
        this.port = port;
        this.socket = new DatagramSocket(this.port);
    }

    @Override
    public void run() {
        while (true){
            byte[] bytes = new byte[1024];
            DatagramPacket datagramPacket = new DatagramPacket(bytes,0,bytes.length);
            try {
                this.socket.receive(datagramPacket);
            } catch (IOException e) {
                e.printStackTrace();
            }
            String s = new String(datagramPacket.getData(), 0, datagramPacket.getData().length).trim();
            System.out.println("From "+datagramPacket.getPort()+": "+s);
            if (s.equals("Done")){
                break;
            }
        }
        socket.close();

    }
}
```

```java
// 用户端
public class UDPUser1 {
    public static void main(String[] args) throws SocketException {
        // 开启两个线程
        new Thread(new UDPSendTest(7777,"localhost",9999)).start();
        new Thread(new UDPReceiveTest(8888)).start();
    }
}

public class UDPUser2 {
    public static void main(String[] args) throws SocketException {
        // 开启两个线程
        new Thread(new UDPSendTest(6666,"localhost",8888)).start();
        new Thread(new UDPReceiveTest(9999)).start();
    }
}
```

## 注解和反射

注解和反射是所有框架的底层，是其底层实现的机制

### 注解

#### 什么是注解

- 注解和注释都可以给人看，但是注解还可以给程序解释，给程序读取

  > 注解是`Annotation` 而注释是`comment`


- 注解是以`@注解名`在代码中存在的，还可以添加一些参数值
- 注解可以附加在包，类，方法，属性等内容上，相当于给他们添加了额外的辅助信息，我们可以通过反射机制编程实现对这些元数据的访问
- 注解还可以起到检查注解内容的作用

#### 内置注解

- `@Override`只适用于修饰方法，表示重写注解

- `@Deprecated`可以用于修饰方法，属性，类，表示不鼓励使用这样的元素，通常是有更好的选择

- `@SuppressWarning`用来抑制编译时的警告信息，需要添加一个参数才可以使用

  > 一个变量未使用就会有警告，标黄也是警告，可以在前添加`@SuppressWarning`来镇压全部警告

#### 元注解(meta-annotation)

元注解的作用就是负责注解其他注解，Java定义了4个标准的元注解类型，他们被用来提供对其他注解类型做说明

- `@Target`用于描述注解的使用范围（被描述的注解可以用在什么地方）

- `@Retention`表示需要在什么级别保存该注释信息，用于描述注解的生命周期

  > `SOURCE` < `CLASS` < `RUNTIME`，一般都是用`RUNTIME`（运行时有效）

- `@Document`说明该注解将被包含在javadoc中

- `@Inherited`说明子类可以继承父类中的该注解

#### 自定义注解

`@interface`用来声明一个注解，格式：`public @interface [注解名]{[定义内容]}`，其中的每一个看似的方法实际上时声明了一个配置参数，方法的名称就是参数的名称，返回值类型就是参数的类型

> 注意返回值只能是基本类型，Class，String，enum

可以通过`default`来声明参数的默认值

如果只有一个参数成员，一般参数名为`value`

注解的元素必须要有值，我们定义注解元素时，经常使用空字符串或0作为默认值

```java
public class Demo1{
    @MyAnnotation(test = {"test"})
    public void test(){
        
    }
}

// 定义一个注解
@Target({ElementType.METHOD,ElementType.TYPE})  // 定义只能在方法和类上使用，当只有一个方法时可以省略value = 
// 同时注意，当且仅当只有一个方法且方法名为value时可以省略value = 
@Retention(value = RetentionPolicy.RUNTIME)  // 表示在所有地方都有效(RUNTIME)
@interface MyAnnotation{
    // 注解的参数：参数类型+参数名();
    // 可以默认为空
    String name() default "";
    int age() default -1;  // 如果默认值为-1表示不存在
    String[] test();
}
```

### 反射

Java作为一个静态语言，反射为其提供了动态性

反射是一个大概念，通过反射获取注解信息只是它的其中一个用处

#### 静态/动态语言

动态语言就是一类在运行的时候可以改变其结构的语言，例如添加新的函数，对象，甚至可以引进代码，已有的函数可以被删除或进行其他结构变化，即运行时代码可以改变自身结构

静态语言与之相反，Java不是动态语言，但是具有一定的动态性，即反射，我们可以利用反射机制获得蕾丝动态语言的特性，可以在编程的时候更加灵活

#### Reflection

`Reflection（反射）`是Java被视为动态语言的关键，其允许程序在执行期间借助`Reflection API`取得任何类内部信息，并能直接操作任意对象的内部属性及方法

```java
Class c = Class.forName("java.lang.String");  // 加载一个类的方式
```

![image-20210513195524986](https://s2.loli.net/2021/12/05/dFIhVg4LevTo98b.png "正常创建对象和通过反射加载类区别")

加载完类之后，在对内存的方法区中就产生一个Class类型的对象（一个类只有一个Class对象），这个对象包含了完整的类的结构信息，我们可以通过这个对象看到**类的结构**

![image-20210513201611638](https://s2.loli.net/2021/12/05/IV5n8blUAuotMyj.png "反射就是逆着来")

#### 应用

反射机制都是在程序运行中

- 判断对象所属的类
- 构造一个类的对象
- 判断一个类所具有的成员变量和方法
- 获取泛型信息
- 运行时处理注解
- 生成动态代理

#### 缺点

对性能有影响，使用反射是一种解释操作，通过JVM满足我们的要求，这类操作总是慢于直接执行相同的操作

#### Class类

Class类是我们创建的所有类的源头，对于每一个类而言，JRE都为其保留了一个不变的Class类型对象，一个Class对象包含了特定某个结构的有关信息

- Class本身也是一个类
- Class对象只能由系统建立对象
- 一个加载的类在JVM中只会有一个Class实例
- 一个Class对象对应的是一个加载到JVM中的一个`.class`文件
- 每个类的实例都会记得自己是由哪个Class实例所生成的
- 通过Class可以完整地得到一个类中的所有被加载的结构
- Class类是Reflection的根源，针对任何想要动态加载、运行的类，唯有先获得相应的Class对象

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        // 通过反射获取类的class对象

        // 方式1：通过forName获得
        Class<?> c1 = Class.forName("com.mine.test1.User1");
        // 方式2：通过对象获得
        User user = new User1();
        Class<? extends User> c2 = user.getClass();
        // 方式3：通过类名.class获得
        Class<User1> c3 = User1.class;
        
        System.out.println(c1.hashCode());
        System.out.println(c2.hashCode());
        System.out.println(c3.hashCode());  // 返回值都相同！因为一个类型只有一个Class对象！
    }
}

class User {
    String name;

    public User() {
    }

    public User(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}

class User1 extends User {
    public User1() {
        this.name = "1";
    }
}

class User2 extends User {
    public User2() {
        this.name = "2";
    }
}
```

> 注意几乎所有的类型都有Class对象（万物皆对象）
>
> ```java
> public class Demo3 {
>  public static void main(String[] args) {
>      Class c1 = Object.class;
>      Class c2 = Comparable.class;
>      Class c3 = String[].class;
>      Class c4 = Override.class;
>      Class c5 = void.class;
>      Class c6 = Class.class;
>  }
> }
> ```
>
> ![image-20210513204619661](https://s2.loli.net/2021/12/05/UNrLIX2GZ9TeBgR.png "各种类型的class对象")

#### 内存分析一个类的加载过程

![image-20210513205046416](https://s2.loli.net/2021/12/05/aBZg3KVnEFo5kX6.png)

![image-20210513212628543](https://s2.loli.net/2021/12/05/82bT5gjlRusvke6.png)

![image-20210513212651085](https://s2.loli.net/2021/12/05/34pn6vdJj9Fx1Xy.png "jvm文字描述")

![image-20210729225308727](https://s2.loli.net/2021/12/05/5QJUDA1NjCh9nuz.png "jvm运行思路整理图")

##### 类的主动引用

类的主动引用一定会发生类的初始化

- 当虚拟机启动，先初始化main方法所在的类
- new一个类的对象
- 调用类的静态非常量成员和静态方法
- 对类进行反射调用
- 初始化某个类该类的父类未被初始化

##### 类的被动引用

不会发生类的初始化

- 当访问一个静态域时，只有真正声明这个域的类才会被初始化。如：通过子类引用父类的静态变量
- 通过数组定义类的引用
- 引用静态常量（常量在链接阶段就存入调用类的常量池中了）

```java
public class Demo4 {
    public static void main(String[] args) {
        System.out.println("Main Loading...");
        // 1. 主动引用
        Son son = new Son();
        Class<Son> sonClass = Son.class;
        // 2. 被动引用
        System.out.print(String.valueOf(Son.b));  // 只有父类被加载
        Son[] array = new Son[5];
        System.out.print(String.valueOf(Son.M));

    }
}

class Father {
    static int b = 2;
    static {
        System.out.println("Father Loading...");
    }
}

class Son extends Father{
    static {
        System.out.println("Son Loading...");
    }
    static final int M = 1;
}
```

#### 类加载器

##### 作用

- 将`.class`文件字节码内容加载到内存中

- 在堆中形成一个Class对象，作为方法区中类数据访问入口

详情可以见“jvm运行思路整理图”

##### 分类

| 名称                                      | 加载的类              | 说明                            |
| ----------------------------------------- | --------------------- | ------------------------------- |
| Bootstrap ClassLoader（启动类加载器）     | JAVA_HOME/jre/lib     | 无法直接访问                    |
| Extension ClassLoader(拓展类加载器)       | JAVA_HOME/jre/lib/ext | 上级为Bootstrap，**显示为null** |
| Application ClassLoader(应用程序类加载器) | classpath             | 上级为Extension                 |
| 自定义类加载器                            | 自定义                | 上级为Application               |

有关部分可以访问[Nyima]([https://nyimac.gitee.io/2020/07/03/JVM%E5%AD%A6%E4%B9%A0/])的jvm笔记总结博客

##### 使用

```java
public class Demo5 {
    public static void main(String[] args) {
        // 获取应用程序类加载器(ApplicationClassLoader)也叫系统类加载器(SystemClassLoader)
        ClassLoader appClassLoader = ClassLoader.getSystemClassLoader();
        // 获取扩展类加载器(Extension ClassLoader)
        ClassLoader extClassLoader = appClassLoader.getParent();
        // 获取启动类加载器(Bootstrap ClassLoader)
        ClassLoader bootClassLoader = extClassLoader.getParent();

        System.out.println(appClassLoader);  // jdk.internal.loader.ClassLoaders$AppClassLoader@2f0e140b
        System.out.println(extClassLoader);  // jdk.internal.loader.ClassLoaders$PlatformClassLoader@16b98e56
        System.out.println(bootClassLoader);  // null
    }
}
```

#### 创建运行时类的对象

##### 获得了Class后的相关方法获取

```java
public class Demo6 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException {
        // 获取类
        Class<?> aClass = Class.forName("com.mine.test1.TestClassLoader");

        // 获得类的信息
        System.out.println(aClass.getName());  // 包名+类名
        System.out.println(aClass.getSimpleName());  // 类名

        Field[] fields1 = aClass.getFields();  // 只能找到public属性，但是也可以找到父类的公共方法
        Field[] fields2 = aClass.getDeclaredFields();  // 所有声明了的属性，但是无法获得父类的方法
        aClass.getField("attr2");  // 已知某个属性
        for (Field field : fields2) {
            System.out.println(field);
        }  // 要这样输出
        // 获得方法的方式也于此雷同，只是变成了getMethod()和getDeclareMethod()，注意传参的时候第二项是返回值
        // 类似的还有getConstructor()可以获得类的构造器，指定构造器参数就是传入参数
    }
}

class TestFather {
    public int attr;
}

class TestClassLoader extends TestFather{
    private int attr1;
    public int attr2;
    protected int attr3;

    private void mat1(){}
    public void mat2(){}
    protected void mat3(){}
}
```

##### 利用反射获得对象/方法属性使用

```java
public class Demo7 {
    public static void main(String[] args) throws Exception {
        Class<?> aClass = Class.forName("com.mine.test1.TestClassLoader");
        // 利用反射构造一个对象
        // aClass.newInstance();  // 只能调用类的无参构造器来创建一个对象，不建议使用（因为如果没有无参构造就会报错
        // 指定构造方法（推荐）
        Constructor<?> constructor = aClass.getDeclaredConstructor(int.class);

        TestClassLoader instance = (TestClassLoader) constructor.newInstance(1);
        // 给这个构造器传入一个参数（可以看作new TestClassLoader(1))
        // 同时由于我们知道这个类的名称，所以可以将其返回值强转为我们指定的类

        System.out.println(instance);  // 注意应在类中加上toString方法，不然打印出来地址

        // 通过反射调用方法

        // 方法一
        Method setAttr1 = aClass.getDeclaredMethod("setAttr1", int.class);// 想要调用先要获取
        setAttr1.invoke(instance,1);  // 调用获取到的方法的invoke方法，传入谁想调用它（对象）和调用的参数
        // 方法二
        int attr1 = instance.getAttr1();  // 获取刚刚配置的值，直接通过对象调用


        System.out.println(attr1);

        // 通过反射修改属性
        Field attr11 = aClass.getDeclaredField("attr1");
        attr11.setAccessible(true);  // 如果修改的是私有属性可能会报错，关闭安全检测
        attr11.set(instance,1);  // 通常不能直接访问私有属性
        System.out.println(instance.getAttr1());
    }
}

class TestClassLoader extends TestFather{

    public TestClassLoader(int attr1) {
        this.attr1 = attr1;
    }

    private int attr1;

    public int getAttr1() {
        return attr1;
    }
    public void setAttr1(int attr1) {
        this.attr1 = attr1;
    }

    @Override
    public String toString() {
        return "TestClassLoader{" + "attr1=" + attr1 + '}';
    }
}
```

##### 获取泛型信息

- `ParameterizedType` 表示一种参数化类型，比如`Collection<String>`（也就是泛型）
- `GenericArrayType` 表示一种元素类型是参数化类型或者类型变量的数组类型
- `TypeVariable` 是各种类型变量的公共父接口
- `WildcardType` 代表一种通配符类型的表达式

以上各种类型都代表不饿能被归一到Class类中的类型但是又和原始类型齐名的类型

```java
public class Demo8 {
    public List<String> test01(Map<String,String> map, List<String> list) {
        return null;
    }

    public static void main(String[] args) throws NoSuchMethodException {
        Class<Demo8> c1 = Demo8.class;  // 反射获得Class
        Method met = c1.getDeclaredMethod("test01", Map.class, List.class);  // 获得其中的方法

        Type[] parameterTypes = met.getGenericParameterTypes();  // 获得该方法的参数类型信息，返回值为数组
        Type returnType = met.getGenericReturnType();  // 获得方法的返回类型信息

        // 获得泛型参数当中的每个参数类型
        for (Type parameterType : parameterTypes) {
            System.out.println("#" + parameterType);
            if (parameterType instanceof ParameterizedType) {  // 如果获得的类型是一个参数化类型（泛型）
                Type[] actualTypeArguments = ((ParameterizedType) parameterType).getActualTypeArguments();
                // 这样才能获得泛型里面包含的每个真实类型，存在数组里
                for (Type actualTypeArgument : actualTypeArguments) {
                    System.out.println(actualTypeArgument);  // 再将每个类型输出
                }
            }
        }

        //获得泛型返回值当中的每个参数类型，返回值只有一个
        if (returnType instanceof ParameterizedType) {
            Type[] actualTypeArguments = ((ParameterizedType) returnType).getActualTypeArguments();
            for (Type actualTypeArgument : actualTypeArguments) {
                System.out.println(actualTypeArgument);
            }
        }
    }
}
```

##### 获取注解信息

以下是通过<a name="ORM">某个类映射到数据库中一个表的示例</a>

![image-20210805103122811](https://s2.loli.net/2021/12/05/x1GfyLZ6cODizh5.png)

```java
public class Demo9 {
    public static void main(String[] args) throws NoSuchFieldException {
        Class<Demo9_1> c = Demo9_1.class;  // 还是先获得一个类（不是对象哦）

        // 通过反射获得所有类注解
        for (Annotation annotation : c.getAnnotations()) {
            System.out.println(annotation);
        }

        // 获得所有属性的所有注解
        for (Field declaredField : c.getDeclaredFields()) {
            for (Annotation declaredAnnotation : declaredField.getDeclaredAnnotations()) {
                System.out.println(declaredAnnotation);
            }
        }

        // 获得某个属性的某个注解的值
        Field id = c.getDeclaredField("id");  // 获得c这个对象的id属性
        TestInter2 a = id.getAnnotation(TestInter2.class);  // 寻找id中的某个注解
        System.out.println(a.s1() + " " + a.s2() + " " + a.i());  // 指定输出该注解的某个值
    }
}

@TestInter1("db_Demo")  // 注解了一下，并设定了名称
class Demo9_1{
    @TestInter2(s1="id",s2="int",i=8)
    private int id;
    @TestInter2(s1="age",s2="int",i=3)
    private int age;
    @Override
    public String toString() {
        return "Demo9_1{" +
                "id=" + id +
                ", age=" + age +
                '}';
    }
}

// 创建一个自定义类名注解
@Target(ElementType.TYPE)  // 作用域：类
@Retention(RetentionPolicy.RUNTIME)  // 作用时间：运行时
@interface TestInter1{
    String value();
}

@Target(ElementType.FIELD)  // 作用域：类
@Retention(RetentionPolicy.RUNTIME)  // 作用时间：运行时
@interface TestInter2{
    String s1();  // 在表中的列名
    String s2();  // 在这一列中存储什么类型的数据
    int i();  // 长度是多少
}
```

## JUC并发

JUC即指`java.util.concurrent`这个包，里面包括并发的功能，之前学过的`Callable`和`Lock`锁都在这个包里面

### 相关背景

#### 多线程初步遇到的问题

- `Thread`只是一个普通的线程类，`Runnable`接口没有返回值，相较于`Callable`效率较低
- 在业务当中之前学过的普通线程使用较少

#### 线程和进程

进程是一个程序的集合，一个进程往往包含多个线程，Java默认只包含`main`和`GC`两个线程

**例：**写文档的时候，就有键盘输入线程和自动保存线程等等

Java本身并没有权利开启线程，想要开启线程，即操作硬件，只能通过本地方法(`native`)

#### 并发和并行

- 并发：多线程操作同一个资源，一核CPU模拟出来多条线程，快速交替进行

- 并行：多个人一起行走，CPU多核，多个线程可以同时执行

>如何查看CPU的核数
>
>```java
>public class Demo1 {
>public static void main(String[] args) {
>   // 获取CPU的核数（CPU密集型，IO密集型）
>   System.out.println(Runtime.getRuntime().availableProcessors());
>}
>}
>```

并发编程的本质就是充分利用CPU的资源

#### 线程的状态

通过`Thread.state`查看线程的状态目录

```java
public enum State {
    // 新生
    NEW,
    // 运行
    RUNNABLE,
    // 阻塞
    BLOCKED,
    // 等待，死等
    WAITING,
    // 超时等待，一段时间就不等了
    TIMED_WAITING,
    // 终止
    TERMINATED;
}
```

#### wait/sleep区别

- `wait`来自`Object`，会释放锁，必须在同步代码块中使用，必须得有一个人让你等
- `sleep`在`Thread`里，抱着锁睡觉，不会释放锁，可以在任何地方睡觉

### Lock锁

#### Synchronized锁方法

传统`Synchronized`就是一个排队的过程，见下代码

```java
public class Demo2 {
    public static void main(String[] args) {
        // 并发：多个线程操作同一个资源类，把资源类丢入线程
        Demo2_1 t = new Demo2_1();
        // Runnable是@FunctionalInterface函数式接口，应该用lambda表达式
        // 即new Thread(()->{ }).start();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"A").start();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"B").start();
        // 以上的代码就是对一个资源类解耦的过程
    }
}

// 资源类 OOP，如果在这里实现了接口，这个类就成了单独的线程类，这个类就不干净了，耦合性太大
// 耦合性即资源类只干自己的事，不和外边主方法里的线程掺杂在一起
class Demo2_1{
    // 属性、方法
    private int i = 20;
    public void test(){
        if (i>0){
            System.out.println(Thread.currentThread().getName()+" consume "+(i--));
        }
    }
}
```

#### 实现类

![image-20210805115619090](https://s2.loli.net/2021/12/05/9IofsOxyjul35VT.png)

- 公平锁：十分公平，先来后到，一定要排队
- 非公平锁：可以插队，后面的线程可以先执行，`Synchronized`也是非公平锁

要用Lock锁，就得在方法内部先加锁，再在catch块中执行语句，再解锁

![image-20210805124126737](https://s2.loli.net/2021/12/05/HvW7J4XY2szZqmi.png)

```java
public class Demo3 {
    public static void main(String[] args) {
        Demo3_1 t = new Demo3_1();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"A").start();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"B").start();
    }
}

// lock使用  1、new一个可重入锁 2、l.lock()加锁 3、finally+unlock()解锁
class Demo3_1{
    private int i = 20;

    // 创建一个可重入锁对象
    Lock l = new ReentrantLock();  // 传入参数true的话就是公平锁，不然默认非公平锁

    public void test(){
        l.lock();  // 加锁
        try {
            if (i>0){
                System.out.println(Thread.currentThread().getName()+" consume "+(i--));
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            l.unlock();  // 解锁
        }
    }
}
```

#### 两个锁的区别

- `Synchronized`是Java内置的一个关键字，`Lock`是一个类
- `Synchronized`无法判断锁的状态，而`Lock`可以判断是否获取到了锁
- `Synchronized`会自动释放锁，A线程执行完了就自动释放
- `Synchronized`一个线程获得了锁，尽管堵塞了，另一个线程也会一直等，`Lock`锁就不一定会等（通过`lock.trylock`可以尝试获取锁，让堵塞的线程可以有机会释放锁）
- 他们都是可重入锁，不可以中断，非公平锁（`Lock`可以自己设置）
- `Synchronized`适合锁少量的代码同步问题，`Lock`适合锁大量的同步代码

#### 锁的含义

重要的就是解决生产者消费者问题，让程序知道当前需要操作的内容

实操时常考题：单例模式，排序算法，**生产者消费者问题**。死锁

##### Synchronized版（多线程中提到过）

`Synchronized`版围绕着`wait`和`notify`进行

```java
public class Demo4 {
    public static void main(String[] args) {
        Demo4_1 demo4_1 = new Demo4_1();
        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo4_1.inc();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"A").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo4_1.dec();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"B").start();
    }
}

class Demo4_1{
    private int num = 0;
    public synchronized void inc() throws InterruptedException {
        // 加锁三步q
        if (num!=0) this.wait();  // 1.判断等待
        num++;  // 2.功能
        System.out.println(Thread.currentThread().getName());
        this.notifyAll();  // 3.通知 其他所有线程加完了，解除其他线程的wait操作
    }
    public synchronized void dec() throws InterruptedException {
        if (num==0) this.wait();
        num--;
        System.out.println(Thread.currentThread().getName());
        this.notifyAll();
    }
}
```

**注意**：这样的程序并不安全，当创建大于两个线程的时候还是会不安全，因为运用了`if`判断，当等待被唤醒时无论当前状态如何都会跳出`if`进入接下来的语句，解决方法就是把`if`改成`while`即可

![image-20210809120241653](https://s2.loli.net/2021/12/05/QBSynxM6Yt1p7rF.png)

##### JUC版

JUC将传统的`wait`和`notify`替换为了`Condition`中的`await`和`signal`

通过`Condition`可以实现线程的任意的顺序进行

```java
public class Demo5 {
    public static void main(String[] args) {
        Demo5_1 demo5_1 = new Demo5_1();
        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo5_1.inc();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"A").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo5_1.dec();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"B").start();
    }
}

class Demo5_1{
    private int num = 0;
    private final Lock lock = new ReentrantLock();
    private final Condition condition1 = lock.newCondition();
    private final Condition condition2 = lock.newCondition();  // 两个方法两个监视器，通过监视器来判断当前执行的是哪个方法

    public void inc() throws InterruptedException {
        lock.lock();
        try {
            // 判断+功能+通知
            while (num==1){
                condition1.await();
            }
            System.out.println(Thread.currentThread().getName());
            num++;
            condition2.signal();  // 唤醒指定的人
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
    public void dec() throws InterruptedException {
        lock.lock();
        try {
            // 判断+功能+通知
           while (num==0){
                condition2.await();
            }
            System.out.println(Thread.currentThread().getName());
            num--;
            condition1.signal();  // 唤醒指定的人
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}
```

##### 八个锁的现象

可以深刻理解锁到底是什么！

>  注意，下面的延迟用的都是`TimeUnit.SECONDS.sleep`这个方法，因为这是JUC包里面的方法

1. 对于外部两个线程争同一个锁，谁先拿到锁谁先执行
2. 拿到锁的线程无论方法内部是否延迟，都必须执行完
3. 普通方法的线程不受加锁方法内部延迟的影响
4. 创建两个实现类是两把不同的锁，执行顺序没有要求
5. 静态方法上锁实际上锁的是类Class模板（唯一），就算是两个对象也无所谓，类锁只有一把
6. 然而如果是静态方法和普通方法被对象调用（不管是不是同一个对象），由于一个是类锁一个是方法锁，所以有两把锁，操作结果同4

~~八个现象只有六点不是常识吗？~~

### 集合类不安全

```java
// list is unsafe
public class Demo6 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();  // ArrayList不安全
        for (int i = 0; i < 100; i++) {
            new Thread(()->{
                list.add(UUID.randomUUID().toString().substring(0,5));
                System.out.println(list);
            }, String.valueOf(i)).start();
        }
    }
}
// Exception in thread "92" Exception in thread "89" java.util.ConcurrentModificationException 报错
```

**解决方法**

1. 把`ArrayList`改成`Vector`就不会报错，因为`Vector`默认线程安全（源码中有`Synchronized`加锁）

2. 利用`Collections`工具类内置方法实现

   ```java
   List<String> list = Collections.synchronizedList(new ArrayList<>());
   ```

3. 然而上面这个工具类并不在JUC里面，还可以用JUC内的`CopyOnWriteArrayList<>()`类

   ```java
   List<String> list1 = new CopyOnWriteArrayList<>();
   ```

   > CopyOnWrite 写入时复制，简称COW，是计算机设计领域的一种优化策略
   >
   > 当有多个线程调用的时候，对于相同的资源，在读取的时候是固定的但是写入的时候避免覆盖（会造成数据问题）
   >
   > 这也就是读写分离

第三种方法比起前两种，优势在于使用的是`Lock`锁完成（因为位于JUC下），同时运用读写分离，效率更高

### 未完待续……

# JavaEE

## JavaWeb

### 基本概念

web开发就是网页开发，表示我们可以从网上拿到一些东西

web分为静态web和动态web

- 静态web就是像html，css等，提供给所有人看的数据不会发生变化
- 动态web就是每个人在不同的时间不同的地点看到的信息各不相同（比如淘宝每日推荐等）

在Java中，动态web资源开发的技术统称为JavaWeb

像`xxx.html`这样的web资源，经过打包，统一地放在某一个文件夹下，这个文件夹可以供浏览器访问，那么这个程序就是web应用程序，通常一个web应用程序由多部分组成，包括：

- html，css，js
- jsp，servlet
- Java程序
- jar包
- 配置文件（Properties）

web应用程序编写完毕后，若想提供给外界访问，需要一个服务器来支持

#### 静态web

静态web的服务器需要有一个`web Service`将用户给的`Request`请求进行分析，将需要的内容`Response`返回

这些静态web都存在很多缺点，比如无法和数据库交互，大多都只通过JavaScript架构，缺少个性化

![image-20210825221446078](https://s2.loli.net/2021/12/05/qmhZPDSrxA6HQOL.png "静态web架构")

#### 动态web

页面会动态展示，因此服务器端的架构和静态web有所不同

![image-20210825222223734](https://s2.loli.net/2021/12/05/jEphuG7y1l9fgZO.png "动态web架构")

`WebServer Plugin`内置一些插件，会过滤一些有害请求，同时除了处理静态资源的一路，新增了动态资源的处理，处理之后同样交给`WebServer`

动态web也有缺点，假如服务器的动态web资源出现了错误，我们需要重新编写我们的后台程序，并重新发布（停机维护）

### web服务器相关技术

如上，所有的服务器都需要`WebServer`，同时`WebServer`有很多种类可以选择：

- ASP（Active Server Pages）
  - 微软公司开发，是国内最早流行的服务器页面
  - 在一个HTML中嵌入VB的脚本，ASP+DOM
  - ASP开发，因为在HTML里嵌入，十分繁杂混乱，基本上每一个页面都有几千行代码
  - ASP也可以用C#作为开发语言，用于进行微软的IIS开发
- PHP
  - PHP开发速度很快，功能很强大，跨平台，代码很简单
  - 但是无法承载大访问量的情况，具有局限性
  - 由于中国大部分网站都是小网站，使PHP很火爆
- JSP（本质就是Servlet）
  - 它是sun公司主推的B/S架构，基于Java语言（大部分大公司组件都是用Java写的）
  - 可以承载三高（高并发 高性能 高可用）问题带来的影响
  - 语法很像ASP，可以让原本学ASP的人快速上手JSP

而web服务器就是用于接收用户的请求并返回响应，包括IIS，**Tomcat**等

### Tomcat

#### 简介

[Tomcat](https://baike.baidu.com/item/tomcat/255751) 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。因为Tomcat 技术先进、性能稳定，而且免费，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

#### 安装

![image-20210825225616843](https://s2.loli.net/2021/12/05/1tvCMRFoc9IfrVS.png "官网")

![image-20210825230237703](https://s2.loli.net/2021/12/05/a6uGpU2K9xg3H8z.png "内部文件结构")

![image-20210825230412871](https://s2.loli.net/2021/12/05/UDyulFCrnqz7Sik.png "启动")

> 提示出现**org.apache.catalina.LifecycleException: 协议处理程序初始化失败**错误！
>
> ```shell
> 26-Aug-2021 00:37:54.080 严重 [main] org.apache.catalina.util.LifecycleBase.handleSubClassException 初始化组件[Connector
> [HTTP/1.1-8080]]失败。
> org.apache.catalina.LifecycleException: 协议处理程序初始化失败
>        at org.apache.catalina.connector.Connector.initInternal(Connector.java:1054)
>        at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:136)
>        at org.apache.catalina.core.StandardService.initInternal(StandardService.java:556)
>        at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:136)
>        at org.apache.catalina.core.StandardServer.initInternal(StandardServer.java:1042)
>        at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:136)
>        at org.apache.catalina.startup.Catalina.load(Catalina.java:747)
>        at org.apache.catalina.startup.Catalina.load(Catalina.java:769)
>        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
>        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:64)
>        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:
> 43)
>        at java.base/java.lang.reflect.Method.invoke(Method.java:564)
>        at org.apache.catalina.startup.Bootstrap.load(Bootstrap.java:305)
>        at org.apache.catalina.startup.Bootstrap.main(Bootstrap.java:475)
> Caused by: java.net.BindException: Address already in use: bind
>        at java.base/sun.nio.ch.Net.bind0(Native Method)
>        at java.base/sun.nio.ch.Net.bind(Net.java:550)
>        at java.base/sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:249)
>        at org.apache.tomcat.util.net.NioEndpoint.initServerSocket(NioEndpoint.java:242)
>        at org.apache.tomcat.util.net.NioEndpoint.bind(NioEndpoint.java:197)
>        at org.apache.tomcat.util.net.AbstractEndpoint.bindWithCleanup(AbstractEndpoint.java:1179)
>        at org.apache.tomcat.util.net.AbstractEndpoint.init(AbstractEndpoint.java:1192)
>        at org.apache.coyote.AbstractProtocol.init(AbstractProtocol.java:580)
>        at org.apache.coyote.http11.AbstractHttp11Protocol.init(AbstractHttp11Protocol.java:82)
>        at org.apache.catalina.connector.Connector.initInternal(Connector.java:1051)
> ```
>
> 通过`netstat -aon|findstr "8080"`找到占用我们8080端口的进程
>
> 然后记住占用的进程PID，在任务管理器-详细信息里面删掉他即可

> 如果出现闪退问题，可以在`startup.bat`文件末尾加上`pause`命令让程序执行完毕后暂停

![image-20210826010251191](https://s2.loli.net/2021/12/05/1ngUreRmispNtSz.png)

成功！

#### 配置

服务器核心配置文件就是`conf/server.xml`，其中可以配置系统的端口号，主机的名称，默认网站应用存放的位置等

> 改主机名称的时候不能只改配置文件里的内容，还需要改系统配置文件
>
> 1. ![image-20210826122520245](https://s2.loli.net/2021/12/05/Bb3V7O5SXK812Zn.png)
>    将此处的localhost改成自定义名称
> 2. `C:\Windows\System32\drivers\etc\hosts`在后面加上`127.0.0.1 [自定义的名称]`	![image-20210826122819666](https://s2.loli.net/2021/12/05/YUXrp29CamqtusE.png)

网站是如何访问的？

1. 输入一个域名+回车，意味着客户端发起了一个请求
2. 首先这个请求交给Windows的配置文件（hosts），检查是否有这个域名的映射
   - 有的话直接返回ip地址
   - 没有的话去DNS服务器寻找该域名对应的ip地址

3. 访问查询到的ip(OSI)

#### 发布一个自己的网站

将自己写的网站，放到服务器（Tomcat）中指定的web应用文件夹（webapps）下，即可通过浏览器（localhost:8080/[自定义文件夹]）访问

> 注意Tomcat默认情况会自动先进入ROOT文件夹内的（根目录）

注意，`webapps`里面一个目录就代表一个网站！网页默认会自动选择目录中的`index.html`内容进行优先展示

#### 部署网站的方式

部署项目的方式（目前有一个D盘下的hello.html需要部署到Tomcat）

1. 直接部署：

   将项目放到 webapps目录下即可。`/hello`:项目的访问路径即<a name="虚拟目录">虚拟目录</a>

   > 当项目十分多的时候，复制起来十分麻烦

2. 优化部署：

   将项目打成一个war包，再将war包放置到 webapps目录下，war包会自动解压缩成网站目录

   > 依旧涉及到复制操作，并不方便

3. 配置文件部署：

   在`conf/ server.xml`文件的`<Host>`标签体中配置`<Context docbase=D: \hello path=/hehe"/>`其中`docbase`为项目存放的路径，`path`为虚拟目录

   > 然而在配置文件中直接修改是十分危险的，这种方式也不建议

4. **热部署方式部署**：

   在 `conf\Catalina \localhost`创建任意名称的`.xml`文件。在文件中编写
   `<Context docbase="D: \hello/>`其中虚拟目录就是`.xml`文件的名称

   > 好处不仅是安全可靠，同时可以在Tomcat运行时修改文件内容而不用重启Tomcat服务

#### Http

Http全称超文本传输协议，是一个简单的请求-响应协议，他通常运行在TCP之上

超文本就是包括图片，音乐，视频，地图等在内的文件形式

Http分为`HTTP/1.0`和`HTTP/1.1(目前)`，前者客户端与web服务器链接后，只能获得一个web资源，然后立即断开连接，后者就是在先前的基础上可以获得多个资源（节省流量）

##### 请求/响应

- 请求：

  ![image-20210827113955393](https://s2.loli.net/2021/12/05/SkwNBq8ufmjOZRc.png)

  其中常用的有两种请求方式，分别是GET和POST

  - GET：请求能够携带的参数比较少，大小有限制，会在浏览器的URL中显示数据内容，不安全，但是比较搞高效

  - POST：请求携带的参数没有限制，大小没有限制，安全，但不高效

  - 但是鉴于目前的网络速度，高效的要求实际上差别不大，大多使用POST更加好

    > <img src="https://s2.loli.net/2021/12/05/T7XVtvOpS2bBRPA.png" alt="image-20210827120643139" style="zoom: 50%;" />

  而后的请求头内还有此次请求更加详细的请求信息

  ![image-20210827121430856](https://s2.loli.net/2021/12/05/a4Bcjk3WKdgJEXq.png)

  其中重要的参数有：

  - `Accept`告诉服务器自己这边支持的数据类型
  - `Accept-Encoding`声明自己支持的编码类型（gzip：接收用gzip压缩的输出）
  - `Accept-Language`声明自己浏览器的语言环境
  - `Connection`请求完成后事断开还是链继续连接
  - 等等

- 响应头：

  ![image-20210827114434878](https://s2.loli.net/2021/12/05/GNQ1PWxe4s9dMOZ.png)

  除了展示出来的响应头信息，还有些其他的内容

  - `Refresh`告诉客户端多久刷新一次
  - `Location`让网页重新定位

##### 状态码

整体印象可以看这个[http.cat](https://http.cat/)

常见的状态码比如：

- 200 OK，请求响应成功
- 3**，请求重定向
- 404，找不到资源
- 502，网关错误

### Maven

在Javaweb的开发中，需要使用大量的jar包，需要手动导入

如何能够让一个东西能够自动帮我们导入这些jar包，这就需要使用Maven（项目架构构建管理工具）

核心思想：约定大于配置。因为Maven会规定好你应该如何编写我们的Java代码，我们必须按照这个来

#### 安装

[官网](https://maven.apache.org/)直接下载解压即可

![image-20210827131108640](https://s2.loli.net/2021/12/05/ShNmzke1L4PDdJp.png)

其中Maven的配置文件为`apache-maven-3.8.2\conf\settings.xml`

#### 配置环境变量

在系统变量中，配置`M2_HOME`和`MAVEN_HOME`两个变量

![image-20210827133348943](https://s2.loli.net/2021/12/05/ch6s2rEiQp4uLNI.png)

并在环境变量Path中加上bin目录的地址

![image-20210827134055700](https://s2.loli.net/2021/12/05/CE5JaefwQdqpFAs.png)

启动cmd查看是否安装成功

![image-20210827133939909](https://s2.loli.net/2021/12/05/kY78uzRIMOm5rvn.png  "完成截图")

#### 添加镜像

由于国内访问国外的网站比较慢，我们可以给Maven添加阿里云镜像

访问[阿里云Maven镜像官网](https://developer.aliyun.com/mvn/guide)复制镜像配置信息

![image-20210827135112700](https://s2.loli.net/2021/12/05/ELJW572oVz8M4aG.png)

复制内容粘贴至[配置文件](apache-maven-3.8.2\conf\settings.xml)内的Mirrors内

```xml
  <mirrors>
      
    <mirror>
      <id>maven-default-http-blocker</id>
      <mirrorOf>external:http:*</mirrorOf>
      <name>Pseudo repository to mirror external repositories initially using HTTP.</name>
      <url>http://0.0.0.0/</url>
      <blocked>true</blocked>
    </mirror>

    <mirror>
      <id>aliyunmaven</id>
      <mirrorOf>*</mirrorOf>
      <name>aliyun public</name>
      <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
    
  </mirrors>
```

#### 建立本地仓库

本地仓库使得我们可以不用每一次都从网上下载内容

在Maven环境中新建一个repo文件夹作为本地仓库，并在配置文件中添加地址

![image-20210827140414087](https://s2.loli.net/2021/12/05/cmike1xKMgr9NWt.png)

```xml
<!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
  <localRepository>D:\PROGRAM\EXE\Environment\apache-maven-3.8.2\maven-repo</localRepository>
```

至此，Maven相关的文件配置工作完成

#### 在IDEA中创建原生Maven项目

创建项目之前，先在设置里修改我们的Maven路径

![image-20210827142702312](https://s2.loli.net/2021/12/05/GRvBO18EafdspZJ.png)

![image-20210827144028279](https://s2.loli.net/2021/12/05/ScjoWN5vqh4xEzk.png)

然后创建一个Maven项目

![image-20210827141203898](https://s2.loli.net/2021/12/05/x37uCXHgPjAoDRe.png)

> 会发现原型下面的内容非常的干净，有两个kotlin相关模板的也和我们javaweb的开发无关
>
> 当我们本地项目创建完之后会自动构建出很多模板，到时候再创建一遍即可

勾选从原型创建可以使用Maven的模板

![image-20210827141847849](https://s2.loli.net/2021/12/05/hgUXrkcOE5IGHxK.png)

> 图片错了，jav改成gav（坐标）

创建好Maven项目后会看到系统正在下一堆文件，慢慢等他下完就行

![image-20210827142506751](https://s2.loli.net/2021/12/05/TV1mnjaJgAKSFQ8.png)

然后可以在之前我们建的仓库中看看是不是有东西了

![image-20210827142933972](https://s2.loli.net/2021/12/05/uah6vyEgLfoG5nz.png)

#### 创建Maven时勾选模板

上述原生项目创建完毕后，我们再次新建一个Maven项目，会发现多了很多原型（模板）

![image-20210827145701602](https://s2.loli.net/2021/12/05/3TCgos9JtWacMFx.png)

选择模板后一路确定

![image-20210827150131448](https://s2.loli.net/2021/12/05/yw2Xo7eJYHc5mZi.png)

又会开始下一堆东西，慢慢等即可

#### 项目结构

原生的Maven项目十分干净，结构十分明了

![image-20210827144828402](https://s2.loli.net/2021/12/05/1Yl38fsTwdAyVvD.png)

通过web模板创建的Maven目录有些不一样

![image-20210827150413631](https://s2.loli.net/2021/12/05/6FJ3x9GgmoZtCIf.png)

为了让两者看上去差不多，可以手动<a name='创建源目录'>创建一下这里没有的目录</a>

> 会发现原生的Maven项目红红绿绿的文件夹比较多，事实上我们也可以创建这些文件夹
>
> 右击目录更改标记
>
> ![image-20210827150726407](https://s2.loli.net/2021/12/05/W4UXq2bm6yPTCeO.png)

当然现在的版本比较智能，当我们在main目录下创建目录时，会提示是否使用Maven原生目录

![image-20210827150912571](https://s2.loli.net/2021/12/05/x2AIEPVhcgfFXCq.png)

勾上就行了

#### 创建原生Maven文件添加web框架

在创建好的原生Maven模块处右键-添加框架支持并选择第一个选项即可，这样创建出来的web框架更加完整

![image-20210901191400088](https://s2.loli.net/2021/12/05/nTAZRLyHg8ujxKq.png)

![image-20210901191442251](https://s2.loli.net/2021/12/05/2dV6ULNRtD3GBZl.png)

#### 在Maven项目中添加Tomcat配置

![image-20210827152907144](https://s2.loli.net/2021/12/05/AgSYrKlcNUWs3i7.png)

然后就会出现Tomcat的配置页面

![image-20210827153419526](https://s2.loli.net/2021/12/05/wKysmBhFGUDxClT.png)

![image-20210827153552231](https://s2.loli.net/2021/12/05/tmQ6uZSKvAHqOFL.png)

 配置完成后还是会出现警告，我们点击部署-添加来添加一个工件

![image-20210827153745487](https://s2.loli.net/2021/12/05/72s6nmXF3pAyw4f.png)

点第一个即可

![image-20210827153814270](https://s2.loli.net/2021/12/05/yfmQdAs9OtMiLoK.png)

因为我们访问一个网站需要指定一个文件夹的名字（如Tomcat下的webapps文件夹），所以必须要创建一个工件

![image-20210827154654956](https://s2.loli.net/2021/12/05/xR9wnTs4D1K2YQh.png)

这个过程就叫做虚拟路径映射

之后只需要点击Tomcat旁边的绿色小三角即可启动Tomcat

![image-20210827154906676](https://s2.loli.net/2021/12/05/zC6HhdXRgLfAv9y.png)

之后会弹出`Helloworld`的网页，实际上就是项目文件中`index.jsp`内的内容（因为浏览器会自动去寻找网站下的`index`打头的文件)

启动过后，我们会发现项目结构中出现了一个`target`目录，里面就是我们构建出来的内容，然而我们可能发现Hello world的网页地址栏内容并不是`target`目录内的网站名，事实上是经过了虚拟路径映射（存疑）

> 虚拟目录映射，就是将web应用交给web服务器管理，然后就可以通过web服务器访问到这个资源。假设现在有一个专门用于发布新闻的web应用news，其位于c盘下，那么，如果配置tomcat，使得当我们访问tomcat服务器时会访问到news里的资源。
>
> 方式一、tomcat的自动映射，将news应用直接放在 tomcat主目录/webapps/，便可直接访问:`http://localhost:8080/news/index.html`
>
> 方式二、很多情况下，在实际的部署中，有可能web应用与tomcat服务器不在同一盘符下，即web应用没办法直接放在webapps目录下，这时就需要建立虚拟目录映射

![image-20210827234856030](https://s2.loli.net/2021/12/05/mwH3ufkgoziVE6P.png)

> 以下为个人猜想：
>
> 如图，此处`target`目录即为目标需要运行网站，程序启动之后在Tomcat下目录中建立相应文件夹，同时使`target`目录和图中`MVNTest_war`目录形成连接，即`MVNTest_war`目录为`target`目录的映射，使得浏览器能够正常读取`index.jsp`主页文件

此双击Maven侧边栏的clear命令，程序会自动清理target目录，这也说明target是一个临时性的目录，用于存放运行时的缓存临时复制文件，在程序结束以后可以被随意清理

#### Maven侧边栏内容

![image-20210827163543169](https://s2.loli.net/2021/12/05/OpVMA8Yyi7IvGEQ.png)

#### pom文件

`pom.xml`是Maven的核心配置文件，存放了Maven的相关信息

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--Maven版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!--创建Maven时配置的GAV-->
  <groupId>com.test</groupId>
  <artifactId>MVNTest</artifactId>
  <version>1.0-SNAPSHOT</version>
  
  <!--项目的打包方式，
      Java应用通常用jar包
      JavaWeb应用通常用war包-->
  <packaging>war</packaging>

  <!--名称及范例，无关紧要-->
  <name>MVNTest Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <!--配置-->
  <properties>
    <!--项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--编码版本-->
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <!--项目依赖-->
  <dependencies>
    <!--具体依赖的jar包配置文件，删除之后Maven会自动更新lib目录（存放程序需要的jar包）下的内容-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <!--项目构建用的东西-->
  <build>
    <finalName>MVNTest</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

其中的项目依赖十分强大，我们可以随便在[Maven仓库](https://mvnrepository.com/)中搜一个依赖（这个web模板中是`junit`），直接粘贴进这里面的`dependencies`标签里

![image-20210828001735499](https://s2.loli.net/2021/12/05/VQTWI6F8fd9ryEs.png)

Maven不仅会自动导入所需jar包，甚至会智能导入这个jar包需要依赖的所有jar包（侧边栏可看）

![image-20210828001855185](https://s2.loli.net/2021/12/05/RYwZHy3V7ubzdTQ.png)

也可以在左边项目结构的外部库里看

![image-20210828002041517](https://s2.loli.net/2021/12/05/E2L7cQpvUHtA1wb.png)

同时由于Maven对约定的要求非常严格，之后我们可以会遇到我们自己写的配置文件无法被导出或者生效的问题，此时我们可以在pom的`build`标签中配置一下`resource`节点，使我们的配置文件可以被<a name="build导出问题">导出</a>

```xml
  <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <!--使Java目录下不只能够存放.java文件
					如果没有这一条可能会出现某些后缀的无法被导出-->
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```

#### Junit

会发现自动创建web模板的时候系统会默认给你导一个Junit的包，事实上Junit就是单元化测试包，导入这个包之后不用写main方法，直接在需要执行的**方法**前面加上`@Test`就可以直接执行某个方法

### Servlet

Servlet是sun公司开发动态web的一门技术，实际上就是一接口，当我们需要使用Servlet的时候，只需要编写一个类实现Servlet接口并把开发好的Java类部署到web服务器中即可

所以我们把实现了Servlet接口的**Java程序**叫做Servlet

#### 准备工作

首先我们需要创建一个普通的Maven项目，并删除其中的src目录，这样的工程就是我们的主工程

之后我们只需要在该项目中新建Module即可

之后我们可以预先将Servlet学习中需要的所有依赖导入（仓库直接搜索即可）

![image-20210828135143340](https://s2.loli.net/2021/12/05/WFcZ3ndvm5arlHC.png)

```xml
<dependencies>
    
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.1</version>
        <scope>provided</scope>
    </dependency>

    <!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
        <scope>provided</scope>
    </dependency>


</dependencies>
```

> 导入包的时候可能会遇到的问题：
>
> 1. 程序包的位置报红，就在侧边栏手动刷新一下，Maven会自动导入包
>
> 2. 还是报红，就去本地仓库中找一找相对应文件位置的jar包是否存在，比如上面的包
>
>    ![image-20210828140506569](https://s2.loli.net/2021/12/05/L2PFgu8jS59kHnZ.png)
>
>    如果不存在就在Maven仓库中手动下包，手动导入，导入路径和图示一致即可（注意改文件夹名）
>
> 3. 如果还有问题，可以在项目结构中有问题描述，根据要求解决问题
>
>    ![image-20210828140832878](https://s2.loli.net/2021/12/05/xpTyeBuY6RHj8zf.png)

接下来我们要建一个Servlet项目，由于Servlet是外部项目，现在我们需要从原型创建

![image-20210828144953216](https://s2.loli.net/2021/12/05/MxgQ6S8e9nip3qT.png)

下一步的时候发现有一个父项项目

![image-20210828145117148](https://s2.loli.net/2021/12/05/5P3ydmEOjZxqRQ1.png)

之后我们会发现项目结构中原本的项目下出现了新的子项目

![image-20210828151151759](https://s2.loli.net/2021/12/05/6H3jABuCM2Jft8y.png)

如果没出现parent标签就按照如图自己加一个即可

然后我们更改一下`src/main/webapp/WEB-INF/web.xml`的版本信息，默认的xml版本（2.3）过老，我们可以去Tomcat里把所有的东西直接复制过来，去掉那些没什么用的东西来直接更换

```xml
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                      https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
  version="5.0"
  metadata-complete="true">

</web-app>
```

> 可以看到Tomcat 10里面用了5.0版本的xml

紧接着和之前一样[创建Maven源目录](#创建源目录)

然后在Java的目录下创建一个正常的Java普通类文件，现在只需要实现Servlet接口即可

#### 继承实现类HttpServlet

Sun公司对Servlet接口提供了两个实现类，分别是`HttpServlet`和`GenericServlet`，而前者又是继承后者的，所以我们这里直接**继承**`HttpServlet`即可

查看源码，会发现`HttpServlet`实现了`Servlet`接口中的`service`方法，而这个方法存在`req`和`resp`两个参数，这两个参数也就是我们能够操作请求从而实现动态web的核心

```java
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String method = req.getMethod();
    long lastModified;
    if (method.equals("GET")) {
        lastModified = this.getLastModified(req);
        if (lastModified == -1L) {
            this.doGet(req, resp);
        } else {
            long ifModifiedSince = req.getDateHeader("If-Modified-Since");
            if (ifModifiedSince < lastModified) {
                this.maybeSetLastModified(resp, lastModified);
                this.doGet(req, resp);
            } else {
                resp.setStatus(304);
            }
        }
    } else if (method.equals("HEAD")) {
        lastModified = this.getLastModified(req);
        this.maybeSetLastModified(resp, lastModified);
        this.doHead(req, resp);
    } else if (method.equals("POST")) {
        this.doPost(req, resp);
    } else if (method.equals("PUT")) {
        this.doPut(req, resp);
    } else if (method.equals("DELETE")) {
        this.doDelete(req, resp);
    } else if (method.equals("OPTIONS")) {
        this.doOptions(req, resp);
    } else if (method.equals("TRACE")) {
        this.doTrace(req, resp);
    } else {
        String errMsg = lStrings.getString("http.method_not_implemented");
        Object[] errArgs = new Object[]{method};
        errMsg = MessageFormat.format(errMsg, errArgs);
        resp.sendError(501, errMsg);
    }

}
```

看出来这个实现在请求方式不同时执行不同的方法，这意味着我们可以重写这些方法达到个性化操作的目的

```java
public class Demo1 extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        PrintWriter writer = resp.getWriter();  // 响应流
        writer.print("Hello World!");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);    // 由于get和post只是请求实现的不同方式，可以相互调用，业务逻辑都一样
    }
}
```

#### 编写Servlet映射

因为我们写的是Java程序，但是要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务中注册我们写的Servlet，还需要给他一个浏览器能够访问的路径

这同样是在`web.xml`里面配置

```xml
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                      https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
         version="5.0"
         metadata-complete="true">

    <!--注册Servlet-->
    <servlet>
        <servlet-name>Demo1</servlet-name>
        <servlet-class>com.test.servlet.Demo1</servlet-class>  <!--Servlet文件地址-->
    </servlet>
    <!--Servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>Demo1</servlet-name>   <!--name标签要相对应（但是可以和Servlet文件不一样）-->
        <url-pattern>/hello</url-pattern>  <!--现在我们只需要在前端请求一个/hello，就会走Servlet-->
    </servlet-mapping>
</web-app>
```

然后我们需要和之前一样[配置Tomcat](#在Maven项目中添加Tomcat配置)，此处我们设置应用程序上下文为D1

#### 启动测试

点击运行，会先出现默认的`index.jsp`里面的内容，然后我们在地址栏后加上`/hello`，页面成功的运行了我们提供的Servlet文件

![image-20210828170358921](https://s2.loli.net/2021/12/05/bSjepcyhirUBmlu.png)

然而也有可能会出现500错误的问题

![image-20210828233406219](https://s2.loli.net/2021/12/05/zK38lxB2iCdWypP.png)

原因是Tomcat10内置的Servlet用的是`jakarta`这个名称底下的jar包，而我们pom中的Servlet用的是`javax`底下的jar包，因此当你写的Servlet传入Tomcat的时候，它判定不出来这是个Servlet（包名不一致）

![image-20210828235030485](https://s2.loli.net/2021/12/05/c1y9fh6WIBTl4Xa.png)

遇到这种情况，解决方法也很简单，打开pom，再导入一个`jakarta`依赖即可

```xml
<!--Tomcat10 Servlet依赖-->
<!--jsp的依赖-->
<dependency>
  <groupId>jakarta.servlet.jsp</groupId>
  <artifactId>jakarta.servlet.jsp-api</artifactId>
  <version>3.0.0</version>
  <scope>provided</scope>
</dependency>
<!--jar包的依赖-->
<dependency>
  <groupId>jakarta.servlet</groupId>
  <artifactId>jakarta.servlet-api</artifactId>
  <version>5.0.0</version>
  <scope>provided</scope>
</dependency>
```

注意改完之后我们的Servlet里面的头部包名也要改

![image-20210829110039528](https://s2.loli.net/2021/12/06/j9oUFMOqZLJWaRr.png)

最终成功结果

#### 工作原理

第一次按下启动按钮的时候，先后发生了这些事（仅个人见解）

1. IDEA将我们写的Servlet编译成`.class`文件，同时与进行打包封装成target目录，之后部署到Tomcat目录下，使得Tomcat目录下拥有我们的网站目录

2. IDEA启动Tomcat，同时调用浏览器给`localhost:8080/D1`发送了一个请求

3. Tomcat启动之后就一直在监听8080端口，接收到请求后，其中的web服务器会产生请求头/体和响应头/体，web服务器根据这个响应收集资源`index.jsp`到浏览器

4. 当我们在浏览器后加上`/hello`时，web服务器在`web.xml`里找到了`\hello`内容，但是发现它用了`<servlet>`标签修饰了，意味着他是一个Servlet资源，因此带着请求和响应去目标的Servlet程序

5. Servlet会将请求封装成req参数，我们对req信息进行判断，然后将结果交给resp参数返回，之后resp会解耦重新变成响应交给web服务器，web服务器根据这个响应去寻找相应其他资源丢还浏览器

   > 正常的Java程序Tomcat并不能执行，必须要满足它提供的规范的Java程序才能被执行，而在Java中，一个规范实际上就是一个接口，而Tomcat能执行的就只有实现了Servlet接口的Java程序

   - 其中Servlet根据提供的接口出发，先执行构造方法，然后执行`init()`方法，接着执行`service()`方法

     > ```Java
     > public interface Servlet {
     > void init(ServletConfig var1) throws ServletException;
     > 
     > ServletConfig getServletConfig();
     > 
     > void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;
     > 
     > String getServletInfo();
     > 
     > void destroy();
     > }
     > ```

附上正规说明的Tomcat执行图

![preview](https://pic2.zhimg.com/v2-ce6e39bb02e3c6a2f4eb1e5afaa6e4e6_r.jpg?source=1940ef5c "附图")

#### Mapping

注意到我们在`web.xml`里面曾经加过`<servlet-mapping>`标签

```xml
<servlet-mapping>
    <servlet-name>Demo1</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

其中`url-pattern`即为Servlet匹配虚拟路径（**不是虚拟目录**），其中的路径可以使用通配符`*`，但注意不能用`?`，而且只存在三种情况：

1. `/*`表示默认路径，无论敲什么都匹配（优先级比较低，会先匹配之前有的明确虚拟路径，而且会顶替掉任何直接输入的文件）

   因此最好使用`/`而不是`/*`

2. `/xxx/*`指定通用映射路径（匹配前缀），只要指定路径xxx就一定会进行映射到指定Servlet

3. `*.xxx`表示匹配后缀，只要最后包含`.xxx`就一定会映射到指定Servlet

> `/*`和`/`的区别：
>
> - `< url-pattern>/</url-pattern>  `会匹配到`/login`这样的路径型url，不会匹配到模式为`*.jsp`这样的后缀型url。
>
> - `< url-pattern>/*</url-pattern> `会匹配所有url：路径型的和后缀型的url(包括`/login`,`*.jsp`,`*.js`和*.html等)。

#### 第二个项目

在项目中再新建一个项目，注意，建立新项目的时候要更改Tomcat配置元件

![image-20210829154134738](https://s2.loli.net/2021/12/06/MrQbzodeBpfYxED.png)

如果不新建元件Tomcat还会将这次的项目和之前的项目一起打包在一个文件里，那就糟糕了

顺便把上一个工程元件给删掉，否则每次启动时都要部署两个项目，也不方便

#### ServletContext对象

ServletContext就是上下文环境，web服务器在启动的时候会为每一个web程序都创建一个ServletContext对象，由于它是由web服务器创建的，因此凌驾于所有Servlet之上，它代表了当前的web应用，它也有很多作用

- 共享数据：比如我在一个Servlet中保存的数据，想要在另一个Servlet中拿到，就需要用到ServletContext

  ```java
  public class Demo1 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext sc = this.getServletContext();
          String s = "你好";  // 某个数据
          sc.setAttribute("s",s);  // 将一个数据保存在Servlet中，名字为s
      }
  }
  
  public class Demo2 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext sc = this.getServletContext();
          String s = (String) sc.getAttribute("s");// 两个Servlet共用一个ServletContext，那边设定完这边就可以取
  
          resp.setContentType("text/html");
          resp.setCharacterEncoding("utf-8");  // 让响应回去不要乱码
          resp.getWriter().print(s);
      }
  }
  ```

  设置`web.xml`之后只需要在浏览器中先访问Demo1后访问Demo2即可

- 请求转发：请求转发并不是重定向，状态码并不会报3xx，因为地址栏路径不变

  ```Java
  public class Demo3 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext sc = req.getServletContext();
          sc.getRequestDispatcher("/2").forward(req,resp);
      }
  }
  ```

  <img src="https://s2.loli.net/2021/12/06/91pQbNevAcUMko6.png" alt="image-20210829232016726" style="zoom: 60%;" />

  <img src="https://s2.loli.net/2021/12/06/MkpC2yh4Ls5NGH6.png" alt="image-20210829234335333" style="zoom: 67%;" />

- 读取资源文件（需要用到Properties类）：

  - 创建一个`.properties`文件，将其放置在`resource`资源文件夹中，重启Tomcat

    会发现资源类文件存放在`target/classes/db.properties`中，说明它默认路径是`classpath`(即在classes目录下)

  - ```java
    public class Demo4 extends HttpServlet {
        @Override
        protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
            InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");
            Properties prop = new Properties();
            prop.load(is);
            String usn = prop.getProperty("usn");
            String pwd = prop.getProperty("pwd");
            resp.getWriter().print(usn+":"+pwd);
        }
    }
    ```

#### HttpServletResponse

当web服务器接收到客户端的http请求，针对这个请求，服务端会创建一个代表请求的HttpServletRequest对象和一个代表响应的HttpServletResponse对象，分别代表客户端请求内容和响应信息

应用：

1. 向浏览器输出信息

2. 下载文件：

   - 关于Content-Disposition：

     在常规的 HTTP 应答中，`Content-Disposition` 响应头指示回复的内容该以何种形式展示，是以**内联**的形式（即网页或者页面的一部分），还是以**附件**的形式下载并保存到本地。

     而在 HTTP 场景中，第一个参数或者是 `inline`（默认值，表示回复中的消息体会以页面的一部分或者整个页面的形式展示），或者是 `attachment`（意味着消息体应该被下载到本地；大多数浏览器会呈现一个“保存为”的对话框，将 `filename` 的值预填为下载后的文件名，假如它存在的话）。

     ```java
     Content-Disposition: inline
     Content-Disposition: attachment
     Content-Disposition: attachment; filename="filename.jpg"
     ```

   - ```java
     public class Demo5 extends HttpServlet {
         @Override
         protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
             // 1.获取下载文件的路径
             String rp = this.getServletContext().getRealPath("/WEB-INF/classes/1.png");  // 注意路径，跟上面的代码一样，最终文件存放位置就是这个
             // 2.获取下载文件的文件名
             String ss = rp.substring(rp.lastIndexOf("\\") + 1);  // 高级用法，检测最后一个\
             // 3.设置文件头，使浏览器能够支持下载我们需要的内容
             resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(ss, StandardCharsets.UTF_8));
             // 第一个参数为属性名，后一个参数为下载方式（attachment是以附件形式下载）最后一项是文件名
             // 4.获取下载文件的输入流
             FileInputStream is = new FileInputStream(rp);
             // 5.创建缓冲区
             int len;
             byte[] buf = new byte[1024];
             // 6.获取OutputStream对象
             ServletOutputStream os = resp.getOutputStream();
             // 7.将FileOutputStream写入到buf缓冲区
             while ((len=is.read(buf))>0)
                 os.write(buf,0,len);
             // 8.关闭内容
             is.close();
             os.close();
         }
     }
     ```

     > 注意到，`getRealPath()`并没有检错功能，要是你的相对路径写错了那就是写错了，他还是会傻瓜一样把一个没有的文件的绝对路径返回给你
     >
     > 在程序中，相对路径的根目录就是你的网站目录，即放在webapps底下的目录

   - 也可以把上一个获取资源类的Servlet改一下实现

     ```java
     public class Demo4 extends HttpServlet {
         @Override
         protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
             InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/1.png");  //这个也是文件的一个路径
             resp.setHeader("Content-Disposition","attachment;filename=1.png");
             int len;
             byte[] buf = new byte[1024];
             ServletOutputStream os = resp.getOutputStream();
             while ((len=is.read(buf))>0)
                 os.write(buf,0,len);
         }
     }
     ```

   - 如果文件名为中文，下载的时候无法被显示，此时需要修改响应头的文件名称格式

     ```java
     resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(ss, StandardCharsets.UTF_8));
     ```

3. 验证码功能：

   ```java
   public class Demo6 extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
           // 浏览器5秒刷新
           resp.setHeader("refresh","5");
           // 在内存中创建一个图片
           BufferedImage bi = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
           // 得到图片
           Graphics2D g = (Graphics2D) bi.getGraphics();
           // 设置图片的背景颜色
           g.setBackground(Color.WHITE);
           g.setColor(Color.BLUE);
           g.setFont(new Font("Consolas",Font.BOLD,20));
           g.drawString(radNum(),0,20);
   
           // 告诉浏览器这个请求用图片方式打开
           resp.setContentType("image/jpg");
           // 网站存在缓存，我们要不让他缓存
           resp.setDateHeader("expires",-1);
           resp.setHeader("Cache-Control","no-cache");
           resp.setHeader("Pragma","no-cache");  // 不缓存
   
           // 将图片写给浏览器
           ImageIO.write(bi,"jpg",resp.getOutputStream());
       }
   
       // 生成四位随机数
       private String radNum(){
           Random random = new Random();
           String s = random.nextInt(9999) + "";
           s = "0".repeat(Math.max(0, 4 - s.length())) + s;  // 这种更巧妙
           // 下面这种方式也可
           // StringBuffer sb = new StringBuffer();
           // for (int i = 4 - s.length(); i > 0; i--) {
           //    sb.append("0");
           //}
           //s = sb.toString() + s;
           return s;
       }
   }
   ```

   > ![20180411092400746](https://s2.loli.net/2021/12/04/4NDcrRGI2mq3S6i.png)

4. **重定向**

   一个web资源收到客户端请求，会通知客户端访问另外一个web资源的过程叫做重定向（用户登录）

   ```java
   public class Demo7 extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           resp.sendRedirect("/2/6");  // 会跳到localhost:8080/2/6的地方，注意不能直接输/6
       }
   }
   ```

#### HttpServletRequest

`Request`和`Responce`是对应关系，那边`set`到的意味着这边都可以`get`到，请求中的所有信息都被封装到`HttpServletRequest`中

下面是一个应用了获得请求信息和请求转发的示例

```java
public class Demo7 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 获得请求信息
        String usn = req.getParameter("username");
        String pwd = req.getParameter("password");
        String[] ckb = req.getParameterValues("checkbox");
        resp.setContentType("text/html");
        resp.getWriter().print(usn+"\n"+pwd+"\n");
        System.out.println(Arrays.toString(ckb));
        // 请求转发
        req.getRequestDispatcher("/jumpWeb.jsp").forward(req,resp);
    }
}
```

```jsp
<%--jumpWeb.jsp--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>success</title>
</head>
<body>
<p>username : ${pageContext.request.getParameter("username")}</p>
<p>password : ${pageContext.request.getParameter("password")}</p>
<p>checkbox : ${pageContext.request.getParameterValues("checkbox")}</p>
</body>
</html>
```

```jsp
<%--index.jsp--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Test</title>
</head>
<body>

<div style="width: auto;height: auto;text-align: center">
    <h1>Login</h1>
    <%--${pageContext.request.contextPath}代表当前的项目--%>
    <form action="${pageContext.request.contextPath}/7" method="get">
        <label>
            username:
            <input type="text" name="username">
        </label><br>
        <label>
            password:
            <input type="password" name="password">
        </label><br>
        checkbox:
        <input type="checkbox" name="checkbox" value="1">
        <input type="checkbox" name="checkbox" value="2">
        <input type="checkbox" name="checkbox" value="3">
        <input type="checkbox" name="checkbox" value="4">
        <input type="checkbox" name="checkbox" value="5"><br>
        <input type="submit">
    </form>
</div>

</body>
</html>
```

### Cookie

会话：就是用户打开一个浏览器，访问web资源，关闭浏览器的过程

有状态会话：客户端访问某一个曾经访问过的服务端且服务端知道的过程

而如何记录一个客户端访问过服务端，就需要服务端对第一次会话进行保存

保存会话的两种方式，分别就是cookie和session（分别代表客户端技术和服务端技术）

#### 为客户端设置一个cookie

```java
public class Demo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html");
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        PrintWriter out = resp.getWriter();

        // 服务端从客户端获取Cookie
        Cookie[] cookies = req.getCookies();
        // 判断Cookie是否为空，如果为空意味着第一次访问
        if (cookies!=null){
            // 如果存在就遍历cookie取出自己想要的数据
            out.write("你上一次访问的时间：");
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals("time")) {  // 有key就有value
                    long l = Long.parseLong(cookie.getValue());  // 时间戳
                    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
                    out.write(sdf.format(new Date(l)));
                }
            }
        }else{
            out.write("第一次访问");
        }
        // 服务端给客户端响应一个Cookie
        Cookie cookie = new Cookie("time",System.currentTimeMillis()+"");  // 存一个信息在cookie里
        resp.addCookie(cookie);

    }
}
```

其中在审查元素的Application里可以看到每一个cookie的信息，并可以对cookie进行删除

![image-20210831143502193](https://s2.loli.net/2021/12/06/xnuDrqm5jdpi84Z.png)

然而这样的代码当我们关闭浏览器再启动的时候先前的cookie不会被保存（默认），只需在27行后加上`cookie.setMaxAge(24*60*60);`即可

正由于由于cookie可以设置有效期的原因，导致cookie并不安全，我本地某一个文件夹中，然而现在随着技术的发展，cookie的形式已经渐渐被淘汰了，取而代之的是session

同时Cookie还存在一些别的问题：

- 一个Cookie只能保存一个信息
- 一个web站点可以个浏览器发送多个cookie，最多存放20个cookie
- Cookie大小有限制，一般在4kb左右
- 浏览器有300个cookie上限

### Session

当你通过浏览器访问一个网站时，服务器会给每一个用户都创建一个session对象，一个Session对象独占一个浏览器，只要浏览器没有关闭就一直存在，所以在用户登录之后可以带着自己的用户信息访问整个网站

#### 保存用户的信息/注销用户

```java
public class Demo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        // 得到Session
        HttpSession session = req.getSession();
        session.setAttribute("name","123");
        // 获取session的id
        String id = session.getId();
        // 判断session是不是新创建
        if (session.isNew()){
            resp.getWriter().write("Login done!id="+id);
        }else{
            resp.getWriter().write("your id="+id);
        }
    }
}
```

```java
public class Demo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        // 得到别的Servlet中配置的session属性
        HttpSession session = req.getSession();
        String name = (String) session.getAttribute("name");
        resp.getWriter().write(name);
        session.removeAttribute("name");  // 删除Session属性
        session.invalidate();  // 会删除当前SessionID
    }
}
```

根据代码可以发现，Session同样实现了之前需要ServletContext才能实现的内容，即实现两个Servlet之间实现数据传输，同时通过抓包可以发现，Session的实现在Cookie中保存了ID值

![image-20210831215016885](https://s2.loli.net/2021/12/06/WltjNxSwRF5boZa.png)

#### 原理

一个**浏览器**对应一个Session，同时虽然我们是在`req`参数中拿到的Session，但是这并不意味着Session是客户端创建的，相反，客户端只保留了Session的ID

sessionid是一个会话的key，浏览器第一次访问服务器会在服务器端生成一个session，有一个sessionid和它对应。tomcat生成的sessionid叫做jsessionid。

session在访问tomcat**服务器**HttpServletRequest的getSession(true)的时候**创建**，tomcat的ManagerBase类提供创建sessionid的方法：**随机数+时间+jvmid**；

存储在服务器的内存中，tomcat的StandardManager类将session**存储在内存中**，也可以持久化到file，数据库，memcache，redis等。**客户端只保存sessionid到cookie**中，而不会保存session，session销毁只能通过invalidate或超时，关掉浏览器并不会关闭session。

那么Session在何时创建呢？当然还是在服务器端程序运行的过程中创建的，不同语言实现的应用程序有不同创建Session的方法，而在Java中是通过调用HttpServletRequest的getSession方法（使用true作为参数）创建的。在创建了Session的同时，服务器会为该Session生成唯一的Session id，而这个Session id在随后的请求中会被用来重新获得已经创建的Session；在Session被创建之后，就可以调用Session相关的方法往Session中增加内容了，**而这些内容只会保存在服务器中，发到客户端的只有Session id；当客户端再次发送请求的时候，会将这个Session id带上，服务器接受到请求之后就会依据Session id找到相应的Session**，从而再次使用之。

#### 失效

1. 服务器会把长时间没有活动的Session从服务器内存中清除，此时Session便失效。Tomcat中Session的默认失效时间为20分钟，并不是随着浏览器的关闭消失！

2. 调用Session的invalidate方法。

```java
HttpSession session = request.getSession();
session.invalidate();  // 注销该request的所有session
```

3. session的过期时间是从：从session不活动的时候开始计算，如果session一直活动，session就总不会过期。从该Session未被访问,开始计时; 一旦Session被访问,计时清0;

4. 设置session的失效时间

   - web.xml中

     ```xml
     <session-config>
         <!--分钟为单位-->
         <session-timeout>30</session-timeout>
     </session-config>
     ```

   - 在程序中手动设置

     ```java	
     request.getSession().setMaxInactiveInterval(-1);  // 永不过期，秒为单位
     ```

   - tomcat也可以修改session过期时间，在server.xml中定义context时采用如下定义：

     ```xml
     <Context path="/livsorder" 
     docBase="/home/httpd/html/livsorder" 　　defaultSessionTimeOut="3600" 
     isWARExpanded="true" 　　
     isWARValidated="false" isInvokerEnabled="true" 　　isWorkDirPersistent="false"/>
     ```

Session和ServletContext的主要区别就是是否能够获取共有资源，Sessio对于资源的处理是个性化的，随着浏览器的不同（用户的不同）而存储不同内容，ServletContext则所有资源共用，每个人访问到的都是相同的内容

### JSP

JSP目前来说已经用的越来越少了，但是仍旧需要进行了解和掌握

最大的特点就是和HTML非常像，同时不同于HTML只能提供静态数据，JSP页面中可以嵌入JAVA代码，提供动态数据

启动Tomcat后，在Appdata目录下的IDEA的路径下，会发现一个`index_jsp.java`的文件，打开来再细研究还能发现他最终继承于Servlet，因此可以说，jsp最终会转变成一个Servlet文件

在JSP中，Java代码要用`<% %>`包裹起来即可直接使用

学习JSP的过程当中，需要导入三个包

```xml
<!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>javax.servlet.jsp-api</artifactId>
    <version>2.3.3</version>
</dependency>

<!-- https://mvnrepository.com/artifact/javax.servlet/jstl -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/taglibs/standard -->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

#### 语法

- `<%=[Java代码]%>`正常的Java代码嵌入，同时省略了`out.println()`，

- `<%[Java代码]%>`可以写多行代码，不过要自己手动输出

- `out.print`手动在浏览器输出html代码（等于`resp.getWriter().print()`）

- `<%![声明]>`声明某个方法，变量（本质上和前面一个没什么区别）

- `<%----%>`注释

- `<%@[属性]%>`浏览器属性相关

  - `page`页面信息，包括自动刷新，导包，页面编码，及设置错误页面等 

  - `include`提取公共页面，就是网站中所有的网页都有的头部和尾部

    > 但一般会这样用`<jsp:include page='...'/>`，两种方式区别不大
    >
    > 前者将两个页面合二为一，后者是在Servlet中通过静态代码块拼接页面（还是两个页面）

  - `taglib`自定义标签形式

#### 九大内置对象

九大内置对象分别对应着Servlet中的九个对象

- out（JspWriter）：等同与response.getWriter()，用来向客户端发送文本数据；
- config（ServletConfig）：对应“真身”中的ServletConfig；

- page（当前JSP的真身类型）：当前JSP页面的“this”，即当前对象；
- pageContext（PageContext）：页面上下文对象，它是最后一个没讲的域对象；
- exception（Throwable）：只有在错误页面中可以使用这个对象；
- request（HttpServletRequest）：即HttpServletRequest类的对象；
- response（HttpServletResponse）：即HttpServletResponse类的对象；
- application（ServletContext）：即ServletContext类的对象；
- session（HttpSession）：即HttpSession类的对象，不是每个JSP页面中都可以使用，如果在某个JSP页面中设置<%@page session=”false”%>，说明这个页面不能使用session。

#### 四大作用域

会发现pageContext、request、session、application四个对象好多方法都基本一样，说明他们的结构是差不多的，这时候就需要理解他们的作用域问题

```jsp
  <%
    pageContext.setAttribute("1","1");  // 默认只在当前页面有效
    request.setAttribute("2","2");  // 在同一请求中有效
    session.setAttribute("3","3");  // 在一次会话中有效
    application.setAttribute("4","4");  // 在服务器关闭后才失效
    // 这四个作用域层层递进，逐级变高
  %>
```

什么状态需要用什么作用域十分重要，同时注意pageContext和request可以通过请求转发和页面转发在另外一个页面中取到

#### JSP标签/JSTL标签/EL表达式

jsp标签一般用于页面（pageContext）的处理，标准格式为`<jsp:[内容]></jsp:[内容]>`

EL表达式可以获取数据、执行运算、获取Web开发的常用对象，格式为`${[内容]}`

jstl标签库则集合了jsp应用的很多功能，用以弥补HTML标签的不足，格式为`<c:[内容]></c:[内容]>`

> 注意在jsp文件头部加上`<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`才可以使用jstl标签库（你妈的Tomcat10根本不行，`jakarta.servlet`就没有jstl包，估计给淘汰了）
>
> 如果是Tomcat9报错可以直接将jstl包和standard包导到`Tomcat/lib`目录下，重启项目即可

```jsp
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
  <form action="index.jsp" method="get">
    <input type="text" name="username" value="${param.username}">
    <input type="submit">
  </form>
  <c:if test="${param.username=='admin'}">
    <c:out value="ur admin,welcome"/>
  </c:if>
  <c:out value="hello+${param.username}"/>
  </body>
</html>
```

然后发现确实还不如Java代码好用，干，什么神秘jstl，狗都不用

#### JavaBean

JavaBean就是实体类，有特定的写法：

- 必须要有一个无参构造
- 属性必须私有化
- 必须有对应的get/set

一般用来和数据库的字段做映射（[ORM](#ORM)）

一般来说实体类的文件夹可以叫`pojo/entity`等，比较正规

```jsp
3<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%--
等价于 Bean bean = new Bean();
bean.getName("123");
...
--%>
<jsp:useBean id="bean" class="com.pojo.Bean" scope="request"/>
<jsp:setProperty name="bean" property="name" value="123"/>
<jsp:setProperty name="bean" property="age" value="1"/>
<jsp:setProperty name="bean" property="gender" value="true"/>

<jsp:getProperty name="bean" property="name"/>
<jsp:getProperty name="bean" property="age"/>
<jsp:getProperty name="bean" property="gender"/>
</body>
</html>
```

```java
public class Bean {
    private String name;
    private int age;
    private boolean gender;

    public Bean() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public boolean isGender() {
        return gender;
    }

    public void setGender(boolean gender) {
        this.gender = gender;
    }

    @Override
    public String toString() {
        return "Bean{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", gender=" + gender +
                '}';
    }
}
```

### MVC三层架构

直到微服务之前都是用这一个架构开发

MVC就是模型（Model/实体类），视图（View/jsp页面），控制器（Controller/Servlet跳转页面）

早期没有MVC架构的时候，用户直接访问控制层，控制层就可以直接操作数据库

![image-20210902005453923](https://s2.loli.net/2021/12/06/sZvCBIHrKg2i75Q.png)

> 然而这样的结构，Servlet直接通过CRUD来操作数据库，使得程序十分臃肿，因为在小小的Servlet中需要处理请求，响应，视图跳转，处理JDBC，处理业务代码，处理逻辑代码等等等等

于是逐渐演变为如今的MVC三层架构，其中的各个部分负责的内容及相互关联情况见下图

![image-20210902003641029](https://s2.loli.net/2021/12/06/zBgiNHW9moLU2rF.png)

Model：

- 业务处理：业务处理（Service）
- 数据持久层：CRUD（Dao）

View：

- 展示数据
- 提供链接发起Servlet请求（a，form，img…）

Controller（Servlet）

- 接受用户的请求：（req：请求参数、Session信息）
- 交给业务层处理对应的代码
- 控制视图跳转

### Filter

过滤器就是用来过滤网站的数据，可以减少很多代码的重复写入

过滤器存在于web服务器和后台资源之间，可以负责过滤掉浏览器的一些垃圾请求，以及进行共用参数初始化

首先也需要先创建一个Java文件，实现Filter接口即可创建一个过滤器

```java
public class Encoding implements Filter {

    // 初始化
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("starting...");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        servletResponse.setContentType("text/html;charset=utf-8");
        filterChain.doFilter(servletRequest,servletResponse);
        // 必须通过Chain调用自己，用以让我们的请求继续走，不然程序运行到这就停住了
    }

    // 销毁
    @Override
    public void destroy() {
        System.out.println("end...");
    }
}
```

然后同样要和Servlet一样配置文件

```xml
<filter>
    <filter-name>filter1</filter-name>
    <filter-class>com.filter.Encoding</filter-class>
</filter>
<filter-mapping>
    <filter-name>filter1</filter-name>
    <url-pattern>/*</url-pattern>
    <!--作用域为所有网页-->
</filter-mapping>
```

#### Listener

监听器在java中和Filter十分相似，同时在运用中其实并不是很常见，同时java中存在着非常多的监听器，其功能都大差不差

比如我们可以运用SessionLisener来监听Session的创建事件，来判断当前网站的在线人数

#### 拦截请求

利用过滤器实现拦截请求功能，涉及到各个界面的转换

前端展示：

- 主页面/登录页面（`index.jsp`）

  ```jsp
  <html>
    <head>
      <title>$Title$</title>
    </head>
    <body>
    <form action="${pageContext.request.contextPath}/1" method="get">
      <input type="text" name="username" value="${param.username}">
      <input type="submit">
    </form>
    </body>
  </html>
  ```

- 被拦截页面（`sys/main.jsp`）

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>主页</title>
  </head>
  <body>
  <h1>成功进入主页</h1>
  <a href="${pageContext.request.contextPath}/2">注销</a>
  </body>
  </html>
  ```

后端服务：

- 登录判断Servlet（`4/1`）

  ```java
  public class Demo01 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          String username = req.getParameter("username");
          if (username.equals("admin")){  // 登录成功
              req.getSession().setAttribute("USER",req.getSession().getId());
              resp.sendRedirect("/4/sys/main.jsp");
          }else{
              resp.sendRedirect("/4");
          }
      }
  }
  ```

- 注销判断Servlet（`4/2`）

  ```java
  public class Demo02 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          req.getSession().removeAttribute("USER");
          resp.sendRedirect("/4");
      }
  }
  ```

- 拦截页面访问过滤器

  ```java
  public class SysFilter implements Filter {
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
          Filter.super.init(filterConfig);
      }
  
      @Override
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain filterChain) throws IOException, ServletException {
          HttpServletRequest req = (HttpServletRequest) request;
          HttpServletResponse resp = (HttpServletResponse) response;  // 强转为Http型的才能操作Session
  
          Object user = req.getSession().getAttribute("USER");
          if (user==null) resp.sendRedirect("/4");
          filterChain.doFilter(request, response);
      }
  
      @Override
      public void destroy() {
          Filter.super.destroy();
      }
  }
  ```

这样便可以完成一个简单的跳转登录专属界面的操作

### JDBC

JDBC就是Java到数据库的连接件，负责将各种类型的数据库的数据和web项目进行连接

#### MySQL连接

安装过程[详见](https://www.jb51.net/article/218236.htm)，同时下载[Navicat](https://www.navicat.com.cn/download/navicat-premium)并进行[破解](https://www.jb51.net/database/712269.html)（略），并进行连接

![image-20210903143811296](https://s2.loli.net/2021/12/06/Hg1KwEGLjIlmFvX.png "完成截图")

接着在IDEA中连接数据库，点击侧边栏后点击加号，配置连接参数

![image-20210903153725135](https://s2.loli.net/2021/12/06/gtnb4uRlEfOQTMP.png)

数据库没加载出来就上面的小圆圈刷新多点几遍

添加依赖

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.26</version>
</dependency>
```

设置中设置中MySQL的方言

![image-20210905155440023](https://s2.loli.net/2021/12/06/jTCupSHw8mdMN7P.png)

#### 获取数据

```java
public class TestJDBC {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        String url = "jdbc:mysql://localhost:3306/demo?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";
        // 1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        // 2.获取数据库的连接
        Connection connection = DriverManager.getConnection(url, username, password);
        // 3.向数据库发送SQL的对象Statement
        Statement statement = connection.createStatement();
        // 4.编写SQL
        String sql = "select * from users";
        // 5.执行SQL，返回结果集（每一条记录）
        ResultSet resultSet = statement.executeQuery(sql);
        // 遍历记录
        while (resultSet.next()){
            System.out.println("id="+resultSet.getObject("id"));
            System.out.println("name="+resultSet.getObject("name"));
            System.out.println("password="+resultSet.getObject("password"));
        }
        // 6.关闭连接，释放资源（先开的后关）
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```

其中的六个步骤就是JDBC的固定步骤，其中仅有第四步需要脑子体现个性化

其中的3-5步也可以写成

```java
PreparedStatement preparedStatement = connection.prepareStatement(sql);
preparedStatement.executeQuery();
```

使用预编译直接获得想要的内容

注意增删改都是`statement.executeUpdate`，查是`statement.executeQuery`

#### 事务

事务遵循[ACID](https://baike.baidu.com/item/acid/10738)原则，用来保证数据传输或者其他的安全，同时事务有四个状态：

- 开启事务
- 事务提交（`commit()`）
- 事务回滚（`rollback()`）
- 关闭事务

下面程序模拟了事务在实际中的重要性

```java
public class TestJDBC02 {
    public static void main(String[] args) throws Exception{
        Connection connection = null;
        try {
            String url = "jdbc:mysql://localhost:3306/demo?useUnicode=true&characterEncoding=utf-8";
            String username = "root";
            String password = "123456";
            // 加载驱动
            Class.forName("com.mysql.cj.jdbc.Driver");
            // 获取数据库的连接
            connection = DriverManager.getConnection(url, username, password);
            // 通知数据库开启事务，false开启
            connection.setAutoCommit(false);
            String sql = "update users set money = money-100 where id = 1;";
            connection.prepareStatement(sql).executeUpdate();
            // int i = 1/0;
            sql = "update users set money = money+100 where id = 2;";
            connection.prepareStatement(sql).executeUpdate();
            connection.commit();  // 两条语句都成功了才提交语句
        } catch (Exception e) {
            assert connection != null;
            connection.rollback();
            e.printStackTrace();
        }finally {
            assert connection != null;
            connection.close();
        }
    }
}
```

## SSM框架

### Mybatis

Mybatis简单来说就是简化了JDBC的操作，是一款优秀的持久层框架（DAO），目前可以在Github中寻找

> 持久化就是将我们的数据在持久状态和瞬时状态转换的过程，比如我们吃的东西吃不完了就要放冰箱，数据不用了放内存也会丢，要做持久化存储
>
> 而持久层就是完成持久化工作的代码块，与之并列的是服务层（Service）和控制层（Controller），其中各个层与层之间的界限非常明显，体现了分工模块化的思想

学习Mybatis，[官方文档](https://mybatis.org/mybatis-3/zh/)非常重要

#### 简单流程

1. 创建mysql数据表

   ```sql
   CREATE DATABASE `mybatis`;
   USE `mybatis`;
   CREATE TABLE `user`(
   	`id` INT(20) NOT NULL,
   	`name` VARCHAR(30) DEFAULT NULL,
   	`pwd` VARCHAR(30) DEFAULT NULL,
   	PRIMARY KEY(id)
   )ENGINE=INNODB DEFAULT CHARSET=utf8;
   
   INSERT INTO `user`(`id`,`name`,`pwd`) VALUES
   (1,'用户1','1234'),
   (2,'用户2','1234'),
   (3,'用户3','1234');
   ```

2. 新建一个Maven普通的父项目，添加依赖

   ```xml
   <!--导入依赖-->
   <dependencies>
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>8.0.26</version>
       </dependency>
   
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.7</version>
       </dependency>
       
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.13.2</version>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

3. 在父项目中创建子模块

4. 编写mybatis工具类

   > 每个基于 MyBatis 的应用都是以一个 SqlSessionFactory 的实例为核心的。SqlSessionFactory 的实例可以通过 SqlSessionFactoryBuilder 获得。而 SqlSessionFactoryBuilder 则可以从 XML 配置文件或一个预先配置的 Configuration 实例来构建出 SqlSessionFactory 实例。

   ```java
   // 工具类
   // sqlSessionFactory --> sqlSession 工厂模式
   public class MybatisUtils {
       // 获取sqlSessionFactory对象
       private static SqlSessionFactory sqlSessionFactory;
       static {
           try {
               String resource = "mybatis-config.xml";
               InputStream inputStream = null;
               inputStream = Resources.getResourceAsStream(resource);
               sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   
       // 获取sqlSession实例，sqlSession无论是方法还是用法都非常像之前JDBC里面的Connection
       public static SqlSession getSqlSession () {
           return sqlSessionFactory.openSession();
       }
   }
   ```

   ![image-20210905104949398](https://s2.loli.net/2021/12/06/fAGJ76q1l98atpm.png)

5. 在`pojo`目录下编写<a name="User">实体类</a>

   ```java
   public class User {
       private int id;
       private String name;
       private String pwd;
   
       public User() {
       }
   
       public User(int id, String name, String pwd) {
           this.id = id;
           this.name = name;
           this.pwd = pwd;
       }
   
       public int getId() {
           return id;
       }
   
       public void setId(int id) {
           this.id = id;
       }
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public String getPwd() {
           return pwd;
       }
   
       public void setPwd(String pwd) {
           this.pwd = pwd;
       }
   
       @Override
       public String toString() {
           return "User{" +
                   "id=" + id +
                   ", name='" + name + '\'' +
                   ", pwd='" + pwd + '\'' +
                   '}';
       }
   }
   ```

6. 在`dao`目录下创建Dao接口，并且设置xml配置文件实现接口

   ```java
   public interface UserMapper {  // 注意实体类以Mapper结尾
       List<User> getUserList();
   }
   ```

   ```xml
   <?xml version="1.0" encoding="GBK" ?> <!--注意此处用GBK编码！-->
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <!--名称空间绑定唯一一个接口，这里等于是实现了这个接口-->
   <mapper namespace="com.test.dao.UserMapper">
       <!--select标签代表的就是查询语句，id对应方法名，resultType就是返回结果的类型，内容就是sql语句-->
       <select id="getUserList" resultType="com.test.pojo.User">
           select *from mybatis.user;
       </select>
   </mapper>
   ```

7. 在resources文件夹下创建`mybatis-config.xml`配置文件，接着编写Mybatis核心配置文件

   ```xml
   <?xml version="1.0" encoding="GBK" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <!--核心配置文件-->
   <configuration>
   
       <environments default="development">
           <environment id="development">
               <transactionManager type="JDBC"/>
               <dataSource type="POOLED">
                   <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                   <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                   <property name="username" value="root"/>
                   <property name="password" value="123456"/>
               </dataSource>
           </environment>
       </environments>
       <!--每一个Mapper.xml都要在Mybatis配置文件中注册-->
       <mappers>
           <mapper resource="com/test/dao/UserMapper.xml"/>
       </mappers>
   </configuration>
   ```

8. Junit测试内容

   ```java
   public class UserDaoTest {
       @Test
       public void test(){
           // 获得SqlSession对象
           SqlSession sqlSession = MybatisUtils.getSqlSession();
           // 执行SQL
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           for (User user : mapper.getUserList()) {
               System.out.println(user);
           }
           // 关闭SqlSession
           sqlSession.close();
       }
   }
   ```

   > 注意到我们自己编写的`.xml`文件（除了`pom.xml`）如果头部 为`UTF-8`且内部含有中文注释一律会报错，这就非常弱智，解决办法就是改为`UTF8`或者删除所有注释
   >
   > 同时记得要在`pom.xml`中[允许](#build导出问题)构建项目的时候把`*.xml`一起打包，不然这些配置文件会被忽略，不过也可以选择把`*Mapper.xml`放到resource文件夹下，就不需要更改pom文件了
   >
   > ![image-20210919135647274](https://s2.loli.net/2021/12/06/VnWqBgN529xCFPZ.png)
   >
   > > 可以看出这样的文件结构也更加美观，注意在resources目录中创建目录是，目录之间要用`/`分割，同时创建的目录结构必须和java目录下Mapper目录结构相同（如图中`com.test.mapper`）

   所有事情完成之后的项目结构（`Dao`和`Mapper`可以互换）

   ![image-20210905143842411](https://s2.loli.net/2021/12/06/yq86nXLBYMWTeao.png)

> 有时候我们可能忘记Mybatis这些工作流程，导致自己在配置环境的时候丢三落四，这时候就可以安装一个Mybatis Plugin的插件，他会提示我们Mapper里面的接口方法是否有配置文件匹配（匹配不到就会报错），以及通过可视化箭头快速跳转配置文件实现方法等，方便我们的Mybatis操作
>
> ![image-20210919145340629](https://s2.loli.net/2021/12/06/KZRUk5NLhsWCJ3m.png)

#### CRUD

现在我们只需要对两个Mapper文件和测试文件进行操作，其他的内容一律可以放着不用管了

- 接口

  ```java
  public interface UserMapper {
      // 查询所有用户
      List<User> getUserList();
      // 根据ID查询用户（带参数范例）
      User getUserById(int id);
      // 插入一个新用户（多个参数+insert标签）
      int addUser(User user);
      // 修改用户
      int updateUser(User user);
      // 删除用户
      int delUser(int id);
  }
  ```

- `.xml`配置文件

  ```xml
  <!--名称空间绑定唯一一个接口，这里等于是实现了这个接口-->
  <mapper namespace="com.test.mapper.UserMapper">
      <!--select标签代表的就是查询语句，id对应方法名，resultType就是返回结果的类型，内容就是sql语句-->
      <select id="getUserList" resultType="com.test.pojo.User">
          select *from mybatis.user;
      </select>
      <!--注意传参方式及使用参数内容形式-->
      <select id="getUserById" resultType="com.test.pojo.User" parameterType="int">
          select *from mybatis.user where id = #{id};
      </select>
      <!--insert标签没有resultType选项-->
      <insert id="addUser" parameterType="com.test.pojo.User" >
          insert into mybatis.user (id, name, pwd) values (#{id},#{name},#{pwd})
      </insert>
      <!--下面语句执行成功返回1，未执行或执行失败返回0（不会报错）-->
      <update id="updateUser" parameterType="com.test.pojo.User" >
          update mybatis.user
          set pwd = #{pwd}
          where id = #{id};
      </update>
      <delete id="delUser" parameterType="int">
          delete
          from mybatis.user
          where id=#{id};
      </delete>
  </mapper>
  ```

- 测试文件

  ```java
  public class UserDaoTest {
      // 获得SqlSession对象
      SqlSession sqlSession = MybatisUtils.getSqlSession();
      // 执行SQL
      UserMapper mapper = sqlSession.getMapper(UserMapper.class);
      @Test
      public void testM1(){
          for (User user : mapper.getUserList()) {
              System.out.println(user);
          }
          // 关闭SqlSession
          sqlSession.close();
      }
  
      @Test
      public void testM2(){
          User userById = mapper.getUserById(5);
          System.out.println(userById);
  
          sqlSession.close();
      }
  
      // 注意！增删改需要提交事务！不然根本插不进去！
      @Test
      public void testM3(){
          int i = mapper.addUser(new User(5, "用户5", "12345"));
          System.out.println(i);
          // 提交事务！
          sqlSession.commit();
          this.testM2();
          sqlSession.close();
      }
  
      @Test
      public void testM4(){
          int i = mapper.updateUser(new User(4, "用户4", "1234567"));
          System.out.println(i);
          sqlSession.commit();
          this.testM2();
          sqlSession.close();
      }
  
      @Test
      public void testM5(){
          int i = mapper.delUser(5);
          System.out.println(i);
          sqlSession.commit();
          this.testM2();
          sqlSession.close();
      }
  }
  ```

#### Map查询

当我们创建User对象的时候可能User有几百个属性，这样在我们创建用户的时候就要传一堆参数，这时候就需要用到Map

比如现在添加了一个`updateMUser`方法

```xml
<update id="updateMUser" parameterType="Map">
    update mybatis.user
    set pwd = #{setPwd}
    where id = #{setId};
</update>
```

```java
@Test
public void testM6(){
    Map<String, Object> map = new HashMap<String,Object>();
    map.put("setPwd","123456");
    map.put("setId",4);
    int i = mapper.updateMUser(map);
    System.out.println(i);
    sqlSession.commit();
    this.testM2();
    sqlSession.close();
}
```

这样即可完成相同的操作，甚至不用用到实体类，这样也很好的解决了多个传参的问题

同时利用`%`通配符作为参数传入还可以进行模糊搜索

#### 配置解析

MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息。 配置文档的顶层结构如下：

- properties（属性）
- settings（设置）
- typeAliases（类型别名）
- typeHandlers（类型处理器）
- objectFactory（对象工厂）
- plugins（插件）
- environments（环境配置）
- environment（环境变量）
- transactionManager（事务管理器）
- dataSource（数据源）
- databaseIdProvider（数据库厂商标识）
- mappers（映射器）

##### 环境配置（environments）

MyBatis 可以配置成适应多种环境，这种机制有助于将 SQL 映射应用于多种数据库之中， 现实情况下有多种理由需要这么做。不过**尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

看上面的`environments`内容，我们可以发现主要由两部分组成

- 第一个是**事务管理器（transactionManager）** ，其中规定了使用JDBC的内容

- 第二个是**数据源（dataSource）**，其中**POOLED**属性代表这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间。同时支持自定义更多属性

  > - `poolMaximumActiveConnections` – 在任意时间可存在的活动（正在使用）连接数量，默认值：10
  > - `poolMaximumIdleConnections` – 任意时间可能存在的空闲连接数。
  > - `poolMaximumCheckoutTime` – 在被强制返回之前，池中连接被检出（checked out）时间，默认值：20000 毫秒（即 20 秒）
  > - `poolTimeToWait` – 这是一个底层设置，如果获取连接花费了相当长的时间，连接池会打印状态日志并重新尝试获取一个连接（避免在误配置的情况下一直失败且不打印日志），默认值：20000 毫秒（即 20 秒）。
  > - `poolMaximumLocalBadConnectionTolerance` – 这是一个关于坏连接容忍度的底层设置， 作用于每一个尝试从缓存池获取连接的线程。 如果这个线程获取到的是一个坏的连接，那么这个数据源允许这个线程尝试重新获取一个新的连接，但是这个重新尝试的次数不应该超过 `poolMaximumIdleConnections` 与 `poolMaximumLocalBadConnectionTolerance` 之和。 默认值：3（新增于 3.4.5）
  > - `poolPingQuery` – 发送到数据库的侦测查询，用来检验连接是否正常工作并准备接受请求。默认是“NO PING QUERY SET”，这会导致多数数据库驱动出错时返回恰当的错误消息。
  > - `poolPingEnabled` – 是否启用侦测查询。若开启，需要设置 `poolPingQuery` 属性为一个可执行的 SQL 语句（最好是一个速度非常快的 SQL 语句），默认值：false。
  > - `poolPingConnectionsNotUsedFor` – 配置 poolPingQuery 的频率。可以被设置为和数据库连接超时时间一样，来避免不必要的侦测，默认值：0（即所有连接每一时刻都被侦测 — 当然仅当 poolPingEnabled 为 true 时适用）。

##### 属性（properties）

我们可以通过该属性来实现引用配置文件，注意在xml中所有的标签都有其固定的位置

![image-20210905201011162](https://s2.loli.net/2021/12/06/PJDixkTElV5vIyc.png)

其顺序就和上边例举时一样，其中属性必须放在第一个标签位置上

引入了外部配置文件之后，环境内的参数可以直接引用配置文件内的变量

```properties
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=UTF-8
username=root
password=123456
```

```xml
<!--引入外部配置文件同时优先使用外部文件的内容-->
<properties resource="db.properties"/>

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

##### 类型别名（typeAliases）

当我们对某一个实体类定义一个别名，使得在项目中的任何位置都可以使用别名来代替完整包名

```xml
<typeAliases>
  	<typeAlias alias="Author" type="domain.blog.Author"/>
    <package name="domain.blog"/>
</typeAliases>
```

如图为该标签的两种用法，其中第二种用法可以通过在实体类前加注解实现自定义别名

```java
@Alias("author")
public class Author {
    ...
}
```

注意第二种方法建议别名使用小写

##### 设置（settings）

这是 MyBatis 中极为重要的调整设置，它们会改变 MyBatis 的运行时行为，但不需要全部掌握

唯一需要知道的就是<a name="日志设置">打印日志</a>

| logImpl | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。 | SLF4J \| LOG4J \| LOG4J2 \| JDK_LOGGING \| COMMONS_LOGGING \| STDOUT_LOGGING \| NO_LOGGING | 未设置 |
| :------ | ----------------------------------------------------- | :----------------------------------------------------------: | ------ |

##### 映射器（mappers）

之前已经使用过，Mybatis提供了四种方式来实现Mapper的映射

```xml
<!-- 1.使用相对于类路径的资源引用 -->
<mappers>
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
  <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
<!-- 2.使用完全限定资源定位符（URL） -->
<mappers>
  <mapper url="file:///var/mappers/AuthorMapper.xml"/>
  <mapper url="file:///var/mappers/BlogMapper.xml"/>
  <mapper url="file:///var/mappers/PostMapper.xml"/>
</mappers>
<!-- 3.使用映射器接口实现类的完全限定类名 -->
<mappers>
  <mapper class="org.mybatis.builder.AuthorMapper"/>
  <mapper class="org.mybatis.builder.BlogMapper"/>
  <mapper class="org.mybatis.builder.PostMapper"/>
</mappers>
<!-- 4.将包内的映射器接口实现全部注册为映射器 -->
<mappers>
  <package name="org.mybatis.builder"/>
</mappers>
```

第三种方式是通过接口来寻找xml配置文件，但是当我们配置文件的文件名和接口类名不一样，或者两者不在同一个包下的时候，程序无法寻找到需要的配置文件

同时第四种方法同样要求配置文件名和接口类名相同，不然也找不到

同时还要注意通过第一和第二种方式的时候使用`/`来分隔目录和类

#### 生命周期和作用域

当程序开始执行时，建造器（SqlSessionFactoryBuilder）读取`mybatis-config.xml`文件，根据配置建造工厂（SqlSessionFactory），之后工厂通过执行器制造一个个SqlSession，每一个SqlSession可以得到一个SqlMapper，通过Mapper来调用我们创建的一个个方法

- 由于建造器只负责根据配置创建工厂，因此在整个程序中完全可以只作为局部变量出现（工具类）
- 工厂可以看作和数据库的连接池，因为程序需要他不断地提供资源给SqlSession，因此他必须在整个程序中一直存在，跟随程序的结束而结束，且全局仅有一个变量
- SqlSession就是连接到连接池的一个请求，工厂接收到请求给予相应的响应，同时他不是线程安全导致不能被共享，最好将其放入每个需要使用的方法中，随着某个要求的实现而结束，即每次收到一个HTTP请求，就打开一个SqlSession，响应之后及时关闭

#### ResultMap结果集映射

当我们的实体类属性和数据库中的字段名不一致的时候，就需要使用到ResultMap

比如我们将上面的[User](#User)实体类的pwd改为password，之后我们的Mapper会去寻找数据库中和实体类中字段相同的属性（password），然而并没有找到（数据库中只有pwd），就会返回空

```xml
<resultMap id="UserMap" type="user">
    <!--column就是数据库中的字段，property就是实体类中的属性，其中两者相同的属性可以不写-->
    <result column="pwd" property="password"/>
</resultMap>
```

其实就是告诉程序实体类中的什么属性等于数据库中的哪个字段名，同时数据库中总是用`_`来分割单词（由于数据库不区分大小写），而实体类中往往使用驼峰命名法，两者的不一致可以用结果集映射来统一

然而这只是非常简单的情况现实中往往不是这么简单

```xml
<!-- 非常复杂的语句 -->
<select id="selectBlogDetails" resultMap="detailedBlogResultMap">
  select
       B.id as blog_id,
       B.title as blog_title,
       B.author_id as blog_author_id,
       A.id as author_id,
       A.username as author_username,
       A.password as author_password,
       A.email as author_email,
       A.bio as author_bio,
       A.favourite_section as author_favourite_section,
       P.id as post_id,
       P.blog_id as post_blog_id,
       P.author_id as post_author_id,
       P.created_on as post_created_on,
       P.section as post_section,
       P.subject as post_subject,
       P.draft as draft,
       P.body as post_body,
       C.id as comment_id,
       C.post_id as comment_post_id,
       C.name as comment_name,
       C.comment as comment_text,
       T.id as tag_id,
       T.name as tag_name
  from Blog B
       left outer join Author A on B.author_id = A.id
       left outer join Post P on B.id = P.blog_id
       left outer join Comment C on P.id = C.post_id
       left outer join Post_Tag PT on PT.post_id = P.id
       left outer join Tag T on PT.tag_id = T.id
  where B.id = #{id}
</select>
```

这样的查询显得非常头痛，因此我们要使用结果集映射中的其他标签

```xml
<!-- 非常复杂的结果映射 -->
<resultMap id="detailedBlogResultMap" type="Blog">
  <constructor>
    <idArg column="blog_id" javaType="int"/>
  </constructor>
  <result property="title" column="blog_title"/>
  <association property="author" javaType="Author">
    <id property="id" column="author_id"/>
    <result property="username" column="author_username"/>
    <result property="password" column="author_password"/>
    <result property="email" column="author_email"/>
    <result property="bio" column="author_bio"/>
    <result property="favouriteSection" column="author_favourite_section"/>
  </association>
  <collection property="posts" ofType="Post">
    <id property="id" column="post_id"/>
    <result property="subject" column="post_subject"/>
    <association property="author" javaType="Author"/>
    <collection property="comments" ofType="Comment">
      <id property="id" column="comment_id"/>
    </collection>
    <collection property="tags" ofType="Tag" >
      <id property="id" column="tag_id"/>
    </collection>
    <discriminator javaType="int" column="draft">
      <case value="1" resultType="DraftPost"/>
    </discriminator>
  </collection>
</resultMap>
```

看上去非常的复杂，实际上是我们没有意识到为什么会那么复杂，这就需要先理解数据表与表之间的多对一/一对多的关系，并且从简单的问题出发，引申到复杂问题的解决

多对一就是很多学生**关联**着一个老师，一对多就是一个老师**集合**很多学生

看起来没什么区别，实际上对应着数据表于表之间的关系，不妨让我们先创建一个关系表

```sql
CREATE TABLE `teacher` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO teacher(`id`, `name`) VALUES (1, 'teacher');

CREATE TABLE `student` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  `tid` INT(10) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fktid` (`tid`),
  CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (1, 's1', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (2, 's2', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (3, 's3', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (4, 's4', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (5, 's5', 1);
```

其中每一个学生必须对应着唯一一个老师，而每一个老师可以拥有很多学生，也可以没有学生，其中查询某一个学生及他的老师就是多对一查询，查询某一个老师和他所有的学生就是一对多查询

> 这两张表出现了外键，但是在目前，外键的使用是越来越少了

##### 多对一（association标签）

接下来我们要创建两个实体类，为了多对一查询，我们在Student实体类中添加Teacher属性

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Student {
    private int id;
    private String name;
    private Teacher teacher;
}
```

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Teacher {
    private int id;
    private String name;
}
```

```java
SqlSession sqlSession = MybatisUtils.getSqlSession();
StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
for (Student student : mapper.listStu()) {
    System.out.println(student);
}
```

以上为测试类和实体类

- 通过配置文件执行和以前一样的操作，在前面的步骤和之前一样的情况下，确实能够输出每一个学生的信息，但是会发现其中的teacher字段为空，原因就是当Student实体类的一个属性为另一个Teacher类的时候，程序不知道应该在这个teacher属性里放什么内容

  ```xml
  <mapper namespace="com.test.mapper.StudentMapper">
      <select id="listStu" resultType="student">
          select * from mybatis.student;
      </select>
  </mapper>
  ```

- 换一种方式，可以用sql代码实现，但是他的问题是无法放进xml配置文件中，因为在我们对两张表取了别名之后，每个字段的名称都改了（t.id，s.id），何况id值查出来就有两个，程序不知道到底把student表里的id值放到Student实体类的id属性还是其中的teacher属性里的teacher.id属性中~（尽管我们能立马理解，但是程序比较笨）~

  ```sql
  select *
  from student s,teacher t
  where s.tid=t.id;
  ```

面对上面两种方式都会出现的问题，就需要万能的结果集映射

- 按照查询嵌套处理（从第一种方式出发）

  ```xml
  <!--查询嵌套-->
  <select id="listStuQ" resultMap="StuATea1">
      select * from mybatis.student;
  </select>
  <resultMap id="StuATea1" type="student">
      <!--复杂的属性单独处理
              其中对象:association
              集合:collection-->
      <association property="teacher" column="tid" select="getTeacher"/>
  </resultMap>
  <select id="getTeacher" resultType="teacher">
      select * from mybatis.teacher where id=#{id}
  </select>
  ```

  > 注意此处`getTeacher`选择中似乎并没有传入参数，实际上系统会默认将`association`下的`column`标签传入，且后面sql语句中的`#{id}`中的id可以被换成任何变量值，无论写什么都是对应着该项tid的值，说到底是系统对参数值的智能匹配

  查询嵌套的本质就是在模糊查询（`select * from mybatis.student`）的基础上对无法识别的内含实体类进行额外处理，优点在于不需要为每个数据表的每一项定制别名，但是缺点在于结构层次不明显，由于需要额外再写一条查询，当数据表结构复杂时难以进行阅读维护

- 按照结果嵌套处理（从第二种方式出发）

  ```xml
  <!--结果嵌套-->
  <select id="listStuR" resultMap="StuATea2">
      select s.id as sid,s.name as sn,t.name as tn,t.id as rid
      from mybatis.student s,mybatis.teacher t
      where s.tid=t.id;
  </select>
  <resultMap id="StuATea2" type="Student">
      <result property="id" column="sid"/>
      <result property="name" column="sn"/>
      <association property="teacher" javaType="teacher">
          <result property="name" column="tn"/>
          <result property="id" column="rid"/>
      </association>
  </resultMap>
  ```

  > 注意到其中给student表中的id字段取了sid的别名，那么等于最后查出来呈现的表中同样是以sid为列，因此在做结果集匹配的时候也需要用别名映射

  结果嵌套本质是从最终的sql语句出发，通过结果集解释每一个名称在数据表中的位置，相对来说更符合惯性思维容易理解，且呈现的内容上更加有层次感，但是注意这种方法必须给每一张表的每一个字段添加别名（其中`s.id as sid`中的as可以省略），否则之后的结果集映射无法找到内容

两种解决方式的思路不同但是最终是殊途同归，代表着`association`标签的两种用法，不过最重要先决条件是两张表存在互相联系的外键，且需要查询的内容（`Student`）和内含的实体类（`Teacher teacher`）是多对一的关系

##### 一对多（collection标签）

将上面的实体类稍加修改，创建Teacher类的students属性，从Teacher查询Student，就实现了一对多的查询

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Teacher {
    private int id;
    private String name;
    private List<Student> students;
}
```

- 根据查询嵌套处理

  ```xml
  <mapper namespace="com.test.mapper.TeacherMapper">
      <select id="listTeaQ" resultMap="TeaAStu1">
          select * from mybatis.teacher;
      </select>
      <resultMap id="TeaAStu1" type="teacher">
          <result property="id" column="id"/>
          <!--上一行不能省略，不然后面一行代码会自动仅将数据表id列作为与student表关联的工具而不会作用于teacher实体类的属性
              造成的结果就是id输出为0-->
          <collection property="students" column="id" ofType="student" select="getStu"/>
          <!--虽然数据表中不存在students列，但是与student的关联关系与id有关，column属性就填有关联的字段-->
      </resultMap>
      <select id="getStu" resultType="student">
          select * from mybatis.student where tid=#{id}; # 同样这个id想填啥就填啥
      </select>
  </mapper>
  ```

  其中的`ofType`代表泛型`List`内的内容类型，如果用`javaType`就是`ArrayList`

- 根据结果嵌套处理

  ```xml
  <select id="listTeaR" resultMap="TeaAStu2">
      select t.id rid,t.name tn,s.id sid,s.name sn
      from mybatis.student s,mybatis.teacher t
      where s.tid=t.id;
  </select>
  <resultMap id="TeaAStu2" type="teacher">
      <result property="id" column="rid"/>
      <result property="name" column="tn"/>
      <collection property="students" ofType="student">
          <result property="id" column="sid"/>
          <result property="name" column="sn"/>
      </collection>
  </resultMap>
  ```

可以看出无论是多对一还是一对多只要理解了内容就都不难，举一反三即可，重要的还是理解每一种方法的核心思想

#### 日志

日志就是当我们的程序出现错误的时候，我们想知道究竟哪里错了，这时候就需要日志

之前在配置解析中也有[提到过](#日志设置)，默认是不输出日志的（NO_LOGGING），而我们实际上只用在配置文件中设置中设定日志类型，之后就可以在程序中输出日志

- STDOUT_LOGGING 标准的日志输出，我们可以直接用，配置进去就行了

  ```xml
  <settings>
      <setting name="logImpl" value="STDOUT_LOGGING"/>
  </settings>
  ```

- LOG4J 是一个强大的日志组件，需要额外导包

  1. ```xml
     <dependency>
         <groupId>org.apache.logging.log4j</groupId>
         <artifactId>log4j-core</artifactId>
         <version>2.14.1</version>
     </dependency>
     ```

  2. 在`resource`目录下创建`log4j.properties`配置文件

     ```properties
     #将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
     log4j.rootLogger=DEBUG,console,file
     
     #控制台输出的相关设置
     log4j.appender.console = org.apache.log4j.ConsoleAppender
     log4j.appender.console.Target = System.out
     log4j.appender.console.Threshold=DEBUG
     log4j.appender.console.layout = org.apache.log4j.PatternLayout
     log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
     
     #文件输出的相关设置
     log4j.appender.file = org.apache.log4j.RollingFileAppender
     log4j.appender.file.File=./log/log.log
     log4j.appender.file.MaxFileSize=10mb
     log4j.appender.file.Threshold=DEBUG
     log4j.appender.file.layout=org.apache.log4j.PatternLayout
     log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
     
     #日志输出级别
     log4j.logger.org.mybatis=DEBUG
     log4j.logger.java.sql=DEBUG
     log4j.logger.java.sql.Statement=DEBUG
     log4j.logger.java.sql.ResultSet=DEBUG
     log4j.logger.java.sql.PreparedStatement=DEBUG
     ```

  3. 之后启动某个测试项目就会生成log文件

     ```log
     [DEBUG][21-09-06][org.apache.ibatis.logging.LogFactory]Logging initialized using 'class org.apache.ibatis.logging.log4j.Log4jImpl' adapter.
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]Class not found: org.jboss.vfs.VFS
     [DEBUG][21-09-06][org.apache.ibatis.io.JBoss6VFS]JBoss 6 VFS API is not available in this environment.
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]Class not found: org.jboss.vfs.VirtualFile
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]VFS implementation org.apache.ibatis.io.JBoss6VFS is not valid in this environment.
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]Using VFS adapter org.apache.ibatis.io.DefaultVFS
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Find JAR URL: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Not a JAR: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Reader entry: User.class
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Listing file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Find JAR URL: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo/User.class
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Not a JAR: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo/User.class
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Reader entry: ����
     ```

     前面的[DEBUG]表示调试级别，代表每个步骤的正常调试运行，目前输出的DEBUG级别都是Mybatis内部设置好的，如果我们需要自定义级别，可以在Java文件中编写代码

  4. 设置日志信息

     ```java
     @Test
     public void testLog(){
         logger.info("info level");
         logger.debug("debug level");
         logger.error("error level");
     }
     ```

     ```log
     [INFO][21-09-06][mapper.UserDaoTest]info level
     [DEBUG][21-09-06][mapper.UserDaoTest]debug level
     [ERROR][21-09-06][mapper.UserDaoTest]error level
     ```

  5. 之后我们要习惯使用log而不是sout打印输出！

#### 分页

分页的目的就是减少数据的处理量，正常通过sql的limit就可以实现，代码为`SELECT * from user limit 0,2`即可，查询从第一个人开始的往后两个人（不是0-2三个人）

知道分页原理之后，我们就可以通过编写mapper的方式来执行分页sql语句

```xml
<select id="getUserByLimit" parameterType="map" resultMap="UserMap">
    select * from mybatis.user limit #{startIndex},#{pageSize}
</select>
```

```java
@Test
public void testLimit(){
    HashMap<String, Integer> map = new HashMap<>();
    map.put("startIndex",1);
    map.put("pageSize",2);
    System.out.println(mapper.getUserByLimit(map));
    sqlSession.close();
}
```

#### 使用注解开发

对于映射器类来说，还有另一种方法来完成语句映射。 它们映射的语句可以不用 XML 来配置，而可以使用 Java 注解来配置。比如， XML 配置文件可以被替换成如下的配置：

```java
package org.mybatis.example;
public interface BlogMapper {
  @Select("SELECT * FROM blog WHERE id = #{id}")
  Blog selectBlog(int id);
}
```

注意之后需要在配置文件中修改mapper成类名注册的方式

```xml
<mappers>
    <mapper class="com.test.mapper.UserMapper"/>
</mappers>
```

然而这样的注解开发十分局限，比如无法实现之前描述过的实体类和数据项名称不一致的问题，因此注解只用于非常简单的情况

同时因为利用注解进行CRUD，必然无法进行提交操作，这时候回去看看当时创建SqlSession的时候，可以发现`sqlSessionFactory.openSession()`是可以传参的，传入true的时候创建出来的SqlSession可以自动提交

而且注解可以实现多参数的查询，之前引入map操作实际上并不正规，正规的多参写法应该在参数前加上`@param`标签

```java
// 注解多参数查询
@Update("update mybatis.user set pwd = #{psw} where id = #{id};")
int anUpdateUser(@Param("id")int id,@Param("psw") String pwd);
```

看上去确实比之前的方法清爽很多

这样参数的注解之后也可以在xml文件中进行相同配置而不需要`parameterType`参数

```java
int anUpdateUser(@Param("id")int id,@Param("pwd") String pwd);
```

```xml
<update id="anUpdateUser" >
    update mybatis.user set pwd = #{pwd} where id = #{id};
</update>
```

#### Lombok

总之就是简化getter和setter的操作，让代码更加简单，~~但相应的争议也很大（但他妈的用就完了）~~

先在setting内把Lombok的插件装上，然后要去maven导包

```xml
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
    <scope>provided</scope>
</dependency>
```

之后我们的实体类就可以使用Lombok来简单实现

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private String password;
}
```

~~操，这寄吧太简单了吧，他妈我爱爆~~

![image-20210906180613693](https://s2.loli.net/2021/12/06/XfjBT28UbDiIgqO.png "项目结构")

#### 动态SQL

动态SQL就是根据不同的条件生成不同的SQL语句，他是Mybatis的一个强大特性

```sql
CREATE TABLE `blog`(
`id` VARCHAR(50) NOT NULL COMMENT '博客id',
`title` VARCHAR(100) NOT NULL COMMENT '博客标题',
`author` VARCHAR(30) NOT NULL COMMENT '博客作者',
`create_time` DATETIME NOT NULL COMMENT '创建时间',
`views` INT(30) NOT NULL COMMENT '浏览量'
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

先创建一个空表

注意到其中`create_time`中存在下划线，而在实体类中我们需要的是驼峰命名法，这时候就需要设置配置文件中的配置信息

![image-20210919123301490](https://s2.loli.net/2021/12/06/zDOnVZmoMwg7S2t.png)

```java
// 实体类
@Data
public class Blog {
    private String id;
    private String title;
    private String author;
    private Date createTime;
    private int views;
}
```

```xml
<mapper namespace="com.test.mapper.BlogMapper">
    <insert id="addBlog" parameterType="blog">
        insert into mybatis.blog (id, title, author, create_time, views)
        values (#{id}, #{title}, #{author}, #{createTime}, #{views});
    </insert>
</mapper>
```

```java
// 工具类
public class IDUtils {
    public static String getID(){
        return UUID.randomUUID().toString().replaceAll("-","");
    }
}
```

```java
// 测试类
public class DSTest {
    @Test
    public void test(){
        SqlSession session = MybatisUtils.getSqlSession();
        BlogMapper mapper = session.getMapper(BlogMapper.class);
        Blog blog = new Blog();
        blog.setId(IDUtils.getID());
        blog.setTitle("1");
        blog.setAuthor("a");
        blog.setViews(9999);
        blog.setCreateTime(new Date());
        mapper.addBlog(blog);
        session.commit();
    }
}
```

以上仅是常规的配置工作

##### if/where标签

```xml
<select id="queryBlogIF" parameterType="map" resultType="blog">
    select *
    from mybatis.blog
    <where>
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>
```

这样就可以在不传入任何参数的时候返回所有值，而在传入拥有`title`或`author`的键值时返回查找到的相应值，注意到*其中的where元素只会在子元素返回任何内容的情况下才插入 “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，where元素也会将它们去除（摘自[帮助文档](https://mybatis.org/mybatis-3/zh/dynamic-sql.html)）*，十分方便

##### choose/when/otherwise语句

当我们只需要多个条件中的选择一个使用时，使用`choose`语句，它有点像 Java 中的 switch 语句

```xml
<select id="queryBlogChoose" resultType="blog">
    select *
    from mybatis.blog
    <where>
        <choose>
            <when test="title != null">
                title = #{title};
            </when>
            <when test="author != null">
                author = #{author}
            </when>
            <otherwise>
                views = #{views}
            </otherwise>
        </choose>
    </where>
</select>
```

会发现比如说传入了title和author，那么程序在判断第一个when的时候就成立，直接跳出choose标签，返回title匹配的字段而不会再判断下面的操作，而if标签每一条都会被判断，取判断结果的交集

##### set标签

set应用在update语句中，代替其中的set语句，同样也会帮我们去除语句**结尾**无用的`,`符号

```xml
<update id="setBlog">
    update mybatis.blog
    <set>
        <if test="title != null">
            title = #{title},
        </if>
        <if test="author != null">
            author = #{author},
        </if>
    </set>
    where id = #{id};
</update>
```

替代后sql语句

```sql
update mybatis.blog SET title = ?, author = ? where id = ?;
Parameters: 4(String), c(String), 99515fc9708d49b9919f484cf53e7a41(String)
```

##### SQL片段

当我们实际应用中可能会出现多个重复使用的SQL语句，使用SQL片段可以将他们提取出来方便复用

```
<sql id="pdTAA">
    <if test="title != null">
        title = #{title},
    </if>
    <if test="author != null">
        author = #{author}
    </if>
</sql>

<update id="setBlog">
    update mybatis.blog
    <set>
        <include refid="pdTAA"/>
    </set>
    where id = #{id};
</update>
```

比如把上面的代码改成这样，也可以正常执行，最好只内含if语句，不然可能无法实现最高程度复用

##### foreach标签

直接用帮助手册上的例子：

```xml
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
```

这语句就是foreach最基础的做法，其中collection代表一个集合，即外部的传入参数名（比如我们向上面一样用map传入，就需要一个list的键值，类型就为`Arraylist`），这个集合内的每一个元素值就是item（整型，字符串都可），其中元素下标即为index，同时拼接的字符串规则在第二行，表示以`(`起始，以`)`结尾，每一个item之间用`,`相连

比如我们传入参数为`{1,2,3}`这个集合，则最后拼接出来的SQL语句为

```sql
SELECT *
  FROM POST P
  WHERE ID in (1,2,3)
```

#### 缓存

缓存就是让一次查询的结果，暂存在一个可以直接取到的地方，当我们需要再次查询相同数据的时候，直接走缓存即可，免去了走数据库的麻烦，同时也可以解决高并发系统的性能问题

同时在实际应用中，查操作往往远远多于写操作，而对于经常查询并且基本不会改变的数据我们就需要使用缓存使得读写速度加快

Mybatis有非常强大的查询缓存特性，可以非常方便地定制和配置缓存，缓存可以极大的提升查询效率

其中默认定义了两级缓存

- 在默认情况下仅有一级缓存开启，它是SqlSession（即我们工具类里创建的）级别的缓存，也称为本地缓存

- 二级缓存需要手动开启和配置，它是基于namespace级别的缓存
- 同时我们还可以通过实现Cache接口来自定义二级缓存

##### 一级缓存

使用这样的测试代码

```java
@Test
public void test4(){
    Blog blog1 = mapper.queryBlog("1");
    System.out.println(blog1);
    System.out.println("---------------------------");
    Blog blog2 = mapper.queryBlog("1");
    System.out.println(blog2);
    System.out.println(blog1==blog2);
    session.close();
}
```

```log
Checking to see if class com.test.mapper.BlogMapper matches criteria [is assignable to Object]
Opening JDBC Connection
Created connection 443713699.
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
---------------------------
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
true
Closing JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@1a7288a3]
Returned connection 443713699 to pool.
```

通过输出日志可以很明显发现，其中的SQL语句只运行了一次，这就代表着第二次对于相同数据的查询并没有重新连接数据库，同时我们还可以发现对于同样的查询数据，他们不仅内容相同，地址也一样，意味着两个数据是从同一个缓存中取出的

> 注意到当取出不同数据或执行增删改的操作的时候，都会刷新缓存，为了使查询到的内容能够时刻保持最新（虽然有时候可能是更新二号用户但是一号用户的缓存也会更新）

除此之外，我们还可以手动清除缓存

```java
@Test
public void test4(){
    Blog blog1 = mapper.queryBlog("1");
    System.out.println(blog1);
    session.clearCache();  // 手动清理缓存
    System.out.println("---------------------------");
    Blog blog2 = mapper.queryBlog("1");
    System.out.println(blog2);
    System.out.println(blog1==blog2);
    session.close();
}
```

```log
Opening JDBC Connection
Created connection 1614133563.
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
---------------------------
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
false
Closing JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@6035b93b]
Returned connection 1614133563 to pool.
```

可以发现使用了不同的缓存区，最后判断结果为false

所以，一级缓存是默认开启的，而且也关闭不掉，只在一次Session中有效（即在开启->关闭过程中开启），意味着不同的用户会开启不同的缓存（作用域太低），从而导致一级缓存在实际中并不能起到很好的优化效果

##### 二级缓存

当我们需要使用全局缓存时，只需要在设置中开启全局缓存（虽然默认就是true），`mapper.xml`中加一个`<cache/>`即可，当然我们也可以通过参数来制定策略

> 注意不加参数的时候因为不存在策略，因此会报错（NotSerializableException），原因是实体类没有[序列化](#序列化)，只需要实体类实现Serializable接口即可，序列化的目的就是有一个规定的的格式使得对象在被序列化（变成字节码）之后能够正常从一级缓存写入到二级缓存中

二级缓存的存在可以让**被关闭**的一级缓存内容被转移到二级缓存，相对应一个`mapper`（mapper作用域比session高，session是去加载一个mapper，并不是创建了一个mapper）对应一个缓存

同时我们也可以在每一条查询内部设置缓存属性，支持个性化的定制缓存策略

```xml
<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
```

这个更高级的配置创建了一个 FIFO（[first in first out]先进先出策略） 缓存，每隔 60 秒刷新，最多可以存储结果对象或列表的 512 个引用，而且返回的对象被认为是只读的，因此对它们进行修改可能会在不同线程中的调用者产生冲突。

```log
Opening JDBC Connection
Created connection 1618984457.
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
---------------------------
Cache Hit Ratio [com.test.mapper.BlogMapper]: 0.0
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
true
```

下面是原理图

![image-20210919201333857](https://s2.loli.net/2021/12/06/szu5HwcKFBmbJpk.png)

##### 自定义缓存（Ehcache）

EhCache 是一个纯Java的进程内缓存框架，具有快速、精干等特点，是Hibernate中默认的CacheProvider

因为在mybatis中用的比较少，这里稍微就提一下

先导包，注意要导mybatis的包，然后在mapper配置文件中添加缓存

```xml
<cache type="com.domain.something.MyCustomCache"/>  <!--这里使用官方文档给出的-->
```

然后配置`ehcache.xml`文件，同样和log4j差不多，网上下一个配置文件，放到resorce文件夹中即可

```xml
<?xml version=1.0 encoding=UTF-8 ?>
<ehcache xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance
         xsi:noNamespaceSchemaLocation=http://ehcache.org/ehcache.xsd
         updateCheck=false>

    <diskStore path=./tmpdir/Tmp_EhCache/>

    <defaultCache
            eternal=false
            maxElementsInMemory=10000
            overflowToDisk=false
            diskPersistent=false
            timeToIdleSeconds=1800
            timeToLiveSeconds=259200
            memoryStoreEvictionPolicy=LRU/>

    <cache
            name=cloud_user
            eternal=false
            maxElementsInMemory=5000
            overflowToDisk=false
            diskPersistent=false
            timeToIdleSeconds=1800
            timeToLiveSeconds=1800
            memoryStoreEvictionPolicy=LRU/>
</ehcache>
```

当然这个不是很重要，今后要学的redis更加牛逼，和spring的配合也更加好！

### Spring

#### 简介

广义上的Spring是一个无比巨大的项目，是一个大杂烩，整合了现有的框架，可能我们一辈子都学不完，我们需要学的只是其中的一个小部分，狭义中的Spring即指Spring Framework，我们所说的SSM框架即指Spring(Framework)、SpringMVC和Mybatis

在2002年的时候推出了Spring框架原型（Interface21），在2004年的时候正式发布了1.0版本，开发者Rod Johnson是一个搞音乐的，Spring框架是针对简化服务器的开发而制作的

它具有一些特点：

- Spring虽然叫做框架，但是实际上也可以看作一个容器
- Spring是一个轻量级的，非入侵式的框架
- 其中有两个核心理念，分别是控制反转（IoC）和面向切面编程（AOP）
- 具有特别优秀的事务处理能力，同时基本上可以整合目前市面上所有的框架

Spring七大模块组成

![20170713150400373](https://s2.loli.net/2021/12/07/iupzQWB7hoy3kFn.png)

#### 第一个程序

1. 第一步还是创建Maven项目并导包，注意要导的是[Spring Web MVC](https://mvnrepository.com/artifact/org.springframework/spring-webmvc)这个包

   ```xml
   <dependency>
       <groupId>org.springframework</groupId>
       <artifactId>spring-webmvc</artifactId>
       <version>5.3.10</version>
   </dependency>
   ```

2. 在java目录下创建`com.test.pojo`目录，并创建实体类`hello.java`，其中比如有一个str的属性

   ```java
   @Data
   public class Hello {
       private String str;
   }
   ```

   > 这里使用了[Lombok](#Lombok)的注解简化操作，手动的话一定要注意添加set方法

3. 在resource文件夹下创建`bean.xml`文件，加上相关头部信息，并在内部对我们刚刚创建的实体类进行属性编辑操作

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <!--使用Spring创建对象（Bean）-->
       <bean id="hello" class="com.test.pojo.Hello">
           <property name="str" value="Spring"/>
       </bean>
   
   </beans>
   ```

   如果把这行配置文件翻译成我们之前的语言，`id`即为创建的对象名（变量名），`class`就是`new`的对象，每一条`property`就是一个属性信息，包括了`name`属性名和`value`属性值

   > idea甚至贴心的可以自动创建Spring配置的头部文件
   >
   > <img src="https://s2.loli.net/2021/12/06/JfkpSZ1jDGCwoyb.png" alt="image-20210921163032772" style="zoom: 47%;" />

4. 在测试类中创建<a name="应用程序上下文">Spring上下文对象</a>（容器），这也是我们程序中唯一一个new对象

   ```java
   public class MTest {
       @Test
       public void test(){
           // 获取Spring的上下文对象
           ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
           // 我们的对象都在context容器中管理，我们要使用的时候直接从里面取即可
           Hello hello = (Hello) context.getBean("hello");
           System.out.println(hello.toString());
       }
   }
   ```

5. 程序结果为`Hello(str=Spring)`

如果把上面的例子带入的话，程序员不用修改程序，由于配置文件中附带了无论是Dao层还是Service层的所有的注册信息，如今只需要将配置文件交给用户，用户直接通过修改配置文件来达到获取自己需要的东西的效果

> 可能会说这他妈和修改代码有什么区别啊，实际上配置文件是灵活的，代码是需要编译+运行的，修改配置文件能够快速的达到不同的效果，无论是调试还是最终的个性化内容都十分方便
>
> 这即是控制反转（IoC）的理念，接下来我们会逐步理解IoC

#### 配置文件

Spring配置文件中，标签实际上并没有多少，常用的而且有用的就更加少了~（当然是在我们目前阶段）~

- `Alias`给我们的某个bean的id取一个别名

  ```xml
  <alias name="hello" alias="hello2"/>
  ```

- `bean`内大多数属性前面都了解过了，还有一些属性实际上也并不重要

  - `name`也是别名，还可以取多个别名，别名之间在`“”`内用`,`或者空格或者分号分隔都可（听说还有更多分隔符），这直接把`Alias`给干掉了
  - `scope`作用域，常用的有单例模式（singleton）和原型模式（prototype）
    - 单例模式，程序启动时创建，并在之后通过容器get时会永远只用同一个对象
    - 原型模式，与单例模式相反，每次get时都会重新创建一个新的对象（比较占内存)

- `import`一般用于团队开发使用，可以将多个配置文件导入合并为一个，比如有两个`bean.xml`，这时候就可以在其中一个配置文件中通过`import`导入另一个配置文件，这样在引用的时候就可以只引用整合起来的一个即可

#### 控制反转（IoC）

##### 理念推导

在没有出现IoC的时候，我们会先写一个Dao层接口（比如UserDao，里面有一个抽象方法get()），然后在Dao层中创建了几个实现类（比如MySQLUserImpl和OracleUserImpl，其中实现了get()接口，分别用来从不同的数据库中查询用户信息），同时由于Dao层不像用户开放，用户想要查询到自己的信息，我们就要创建一个业务层接口（比如UserService，同样提供了get接口），然后再创几个实现类（UserServiceImpl，里面创建了一个私有的UserDao类型对象属性userDao，并保存着一个new出来的MySQLUserImpl对象，同时实现get()方法，直接调用刚刚new出来的对象的方法即可），于是用户想要使用的时候就可以自己new一个业务层实现类，然后调用实现类的方法

![image-20210921150934356](https://s2.loli.net/2021/12/06/6KErLd5ZzfqCh94.png)

看似好像没有问题，但是当某一天我们需要从另一个数据库中搜索用户的信息时，我们必须对业务层中new代码进行修改（比如变成new OracleUserImpl），虽然后面的代码不用改变，但是当我们拥有很多个Dao层的实现类，并且业务层又存在多个new的时候，对于每一条代码的修改就显得非常麻烦

这时候就需要我们对业务层的内容进行修改，比如说加一个带参数的set()方法，当用户创建出业务层实现类对象后，通过调用set方法并传入自己外部new出来的持久层对象，指定自己想要去哪个数据库查询信息，而业务层中的set()方法直接将传入的对象赋值给自己的私有的属性，从而实现对用户要求的满足

这样的将主动权从业务层到用户的更改模式就是早期的**控制反转**思想

看似好像非常简单，但是一旦放到实际的应用中，我们或许并不能清楚的说出相关原理

##### 创建对象方式

通过测试的方式，我们可以粗略的探究Spring的运行原理

- 首先默认使用无参构造创建的对象，如果实体类中用有参构造覆盖了无参构造，那么运行时就会报错

- 当然Spring也是提供了三种方式来便于我们进行有参构造的初始化

  1. 利用下标进行有参构造，有参构造内第一个参数就是下标0，以此类推

     ``` xml
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg index="0" value="7500000"/>
         <constructor-arg index="1" value="42"/>
     </bean>
     ```

  2. ~~利用类型进行有参构造（不建议）~~

     ```xml
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg type="int" value="7500000"/>
         <constructor-arg type="java.lang.String" value="42"/>
     </bean>
     ```

  3. 利用参数名进行有参构造

     ```xml
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg name="years" value="7500000"/>
         <constructor-arg name="ultimateAnswer" value="42"/>
     </bean>
     ```

- 无论我们想不想要某个bean，在程序启动的时候都已经被实例化了，等着我们去取

##### 依赖注入（DI）

依赖注入是Spring进行控制反转的主要手段，分别有构造器注入，**Set注入**和拓展方式注入

其中的依赖就是bean对象的创建依赖于容器，注入则是bean对象中的所有属性，由容器来注入

- 构造器注入就是之前我们尝试过的有参构造的初始化操作

- Set方式注入是一个非常重要的注入方式，也是DI的本质注入方式

  1. 创建拥有不同类型属性的实体类

     ```java
     @Data
     public class BeanF {
         private String s;
         private BeanS beanS;  // 另外一个自定义类，有一个字符串属性s
         private String[] ss;
         private List<String> l;
         private Map<String,String> m;
         private Properties p;
     }
     ```

  2. 对不同的属性进行注入

     ```xml
     <bean id="beanS" class="com.test.pojo.BeanS"/>
     
     <bean id="beanF" class="com.test.pojo.BeanF">
         <!--1.普通注入-->
         <property name="s" value="1"/>
         <!--2.bean注入-->
         <property name="beanS" ref="beanS"/>
         <!--3.数组注入-->
         <property name="ss">
             <array>
                 <value>a</value>
                 <value>b</value>
                 <value>c</value>
             </array>
         </property>
         <!--4.list集合-->
         <property name="l">
             <list>
                 <value>a</value>
                 <value>b</value>
             </list>
         </property>
         <!--5.map索引-->
         <property name="m">
             <map>
                 <entry key="a" value="1"/>
                 <entry key="b" value="2"/>
             </map>
         </property>
         <!--6.资源类-->
         <property name="p">
             <props>
                 <prop key="a">1</prop>
                 <prop key="b">2</prop>
             </props>
         </property>
     </bean>
     ```

- 拓展注入方式

  当内置的标签内容不能满足我们的要求时，我们可以导入外部的命名空间包，从而获得我们想要的内容

  首先先在配置文件 头部添加p标签网络地址，p标签实际上就是让属性值的快速注入

  ```xml
  xmlns:p="http://www.springframework.org/schema/p"
  ```

  ```xml
  <bean id="beanF" class="com.test.pojo.BeanF" p:s="1" p:beanS-ref="beanS">
  ```

  这样就相当于set注入时例子的第一、二种方式

  与此类似的是c命名空间，代表着的是构造器注入，同样要导入头部文件地址（上面p改成c即可）

  ```xml
  <bean id="beanF" class="com.test.pojo.BeanF" c:s="1" c:_1-ref="beanS">
  ```

  可以看出两者十分类似，代表着通常的两种注入

#### 自动装配

上面我们都是通过手动设置每一个Bean的属性，事实上Spring还支持属性的隐性的自动装配

原理就是Spring会在上下文中自动寻找，并自动给Bean装配属性

比如我们先搭一个父亲拥有两个孩子的环境

```java
@Data
public class Fat {
    private String n;
    private Son son;
    private Dau daughter;
}
```

配置文件也要搞好

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="son" class="com.test.pojo.Son"/>
    <bean id="daughter" class="com.test.pojo.Dau"/>

    <bean id="father" class="com.test.pojo.Fat">
        <property name="n" value="lyb"/>
        <property name="son" ref="son"/>
        <property name="daughter" ref="daughter"/>
    </bean>

</beans>
```

然后我们其实会发现，设置父亲的两个孩子的配置代码似乎是多余的，因为不用说我们也知道两个属性肯定是儿子和女儿

##### 利用配置文件自动装配

于是我们就可以使用bean的自动装配属性

```xml
<bean id="father" class="com.test.pojo.Fat" autowire="byName">
    <property name="n" value="lyb"/>
</bean>
```

会发现也达成了效果，不过有个非常重要的点，这个`byName`属性只会查找和自己对象的属性变量名一样的`beanid`

比如说我的父亲有`Dau daughter`的属性，这时候程序就会在配置文件中寻找是否有id（即变量名）为daughter的bean，有的话就给父亲对象默认加一个`<property name="daughter" ref="daughter"/>`的标签

与此类似的还有`byType`，引用上一个例子，他则会去寻找配置文件中是否有class为Dau的bean，操作相同

`byName`不能解决名字不相同和名字相同但类型不相同的情况，而`byType`则不能解决存在多个相同类型属性和配置文件对同一个实体类创建多个实例化类的情况

##### 注解实现自动装配

事实上，对于到底使用注解还是xml配置，官方文档里有这么一句话

==**The long answer is that each approach has its pros and cons, and, usually, it is up to the developer to decide which strategy suits them better. **==

意思就是各有利弊，但是显然通过注解配置相对来说更为方便

想要使用注解开发，我们要先导入约束，并且配置注解的支持

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```

通过之前的学习，可以看出导入了一个`context`的命名空间，里面的`annotation-config`为我们提供了注解的支持

现在我们使用自动装配也变得十分简单，只需要在`Fat`类的需要自动装配属性前加上`@Autowired`即可

而我们的配置文件就可以变得十分简单

```xml
<bean id="son" class="com.test.pojo.Son"/>
<bean id="daughter1" class="com.test.pojo.Dau"/>

<bean id="father" class="com.test.pojo.Fat"/>
```

```java
@Data
public class Fat {
    private String n;
    @Autowired
    private Son son;
    @Autowired
    private Dau daughter;
}
```

其中注解会默认先匹配`byTye`如果存在类型相同的就使用`byName`，非常智能

实在还是无法自动匹配，就在`@Autowired`注解下加一个`@Qualifier(value = "son")`可以手动指定`beanid`

#### 利用注解配置

上面我们稍微讲了一下自动装配的注解方式，实际上Spring的注解是非常强大的

同时由于配置文件一般需要配置一些核心内容，对于像是bean中注入属性之类往往跟倾向于用注解

同时在Spring4之后，使用注解开发必须导入AOP的包，并导入context的约束

同时我们可能会发现，使用注解之后甚至不需要set方法了，因为注解是通过反射获得类的所有信息，不需要set就能访问到私有属性

```java
@Data
@Component  // 相当于之前的在配置文件中<bean id="user" class.../>这样
// 注意@Component往往专属于实体类层，在dao层往往使用@Repository，controller层和service层往往会使用@Controller和@Service
// 这四个注解名称不一样但是功能完全相同，都是将一个类交由Spring托管
@Scope("singleton")  // 相当于之前设置scope属性
public class User {

    @Value("a")  // 相当于之前的<property name="s" value="a"/>
    private String s;
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!--指定要扫描的包，这个包底下的所有Spring注解都会生效-->
    <context:component-scan base-package="com.test"/>
    <context:annotation-config/>

</beans>
```

#### 使用JavaConfig配置

如果使用基于Java容器配置的方法来配置，就可以完全摆脱xml配置文件，全权交给Java来做配置

在Spring4之后，JavaConfig变成了推荐的配置方式，因为他对比于xml更加灵活

一共有两种方式为一个实体类创建配置：

- 通过`@Bean`实现

  - 在实体类中通过注解添加该类的属性值

    ```java
    @Data
    public class User02 {
        @Value("a")
        private String s;
    }
    ```

  - 创建一个Java的配置文件类（官网推荐`AppConfig.java`）

    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public User02 user(){
            return new User02();
        }
    }
    ```

  - 这时候就可以将`AppConfig`看作之前的xml配置文件，`@Bean`注解就是`bean`标签，`user()`方法即为配置文件中的`id`，而`return`返回的内容即为配置文件中的`class`属性

    因此上述类可以化为xml配置文件`<bean id="user" class="com.test.pojo.User02"/>`

  - 于是乎我们可以在测试类中导入这个Java类配置文件

    ```java
    public class MTest {
        @Test
        public void test(){
            AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            Object user = context.getBean("user");
            System.out.println("user = " + user);
        }
    }
    ```

    与之前通过`ClassPathXmlApplicationContext`创建容器不同，现在由于没有xml配置文件，我们要使用JavaConfig注解方式`AnnotationConfigApplicationContext`获得应用程序上下文，可以看出`getBean`里面根据对应关系写的便是方法名，用法与先前类似

- 通过`@Conponent`&`@ComponentScan`实现

  - 在利用注解配置时，我们注意到当一个实体类拥有`@Component`注解且被Spring扫描到后，该类就可以自主的成为一个Bean，现在我们想要的就是把原本在xml中做的扫描操作搬到现在的JavaConfig中来

  - 同样先创建实体类，注意要给他标上`Component`注解

    ```java
    @Data
    @Component
    public class User01 {
        @Value("a")
        private String s;
    }
    ```

  - 创建JavaConfig配置文件

    ```java
    @Configuration
    @ComponentScan("com.test.pojo")
    public class AppConfig {
    }
    ```

    可以发配置文件中可以什么都没有，只需要加上`@ComponentScan`注解并指定正确的包名即可

  - 添加测试类

    ```java
    public class MTest {
        @Test
        public void test(){
            AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            User01 bean = context.getBean(User01.class);
            System.out.println("bean = " + bean);
        }
    }
    ```

- 注意到上述的代码有一个神秘的`@Configuration`注解，这个注解实际上是`@Component`注解的子注解，意味着它和`@Component`注解拥有一样的功能，也就是可以被Spring扫描功能扫到

- 而在上述代码中我们事实上并没有使用`@Configuration`的功能，因为我们通过传参的形式使得`AnnotationConfigApplicationContext`精准识别到了我们的JavaConfig文件，然而当我们拥有多个JavaConfig时，我们可以通过添加`@Configuration`注解在测试类中扫包获得JavaConfig

  ```java
  AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
  context.scan("com.test.config");  // 获取该目录下的所有带@Component及子注解的文件
  context.refresh();  // 注意refresh不能省略，为了将扫到的包能够更新到上下文
  ```

#### 面向切面编程（AOP）

代理模式就是SpringAOP的底层，想要了解AOP就必须了解代理模式

##### 静态代理

静态代理的角色分配及实现

- 抽象角色：一般会用接口或者抽象类解决（租房子）

  ```java
  public interface Rent {
      public void rent();
  }
  ```

- 真实角色：被代理的角色（房东）

  ```java
  public class Host implements Rent{
      @Override
      public void rent() {
          System.out.println("rent");
      }
  }
  ```

- 代理角色：代理真实角色，并且在代理之后做一些附属操作（中介）

  ```java
  public class Proxy implements Rent{
      private Host host;
  
      public Proxy() {
      }
  
      public Proxy(Host host) {
          this.host = host;
      }
  
      @Override
      public void rent() {
          // 在这里添加附属操作
          host.rent();
      }
  }
  ```

- 客户：访问代理对象的人（我）

  ```java
  public class Client {
      public static void main(String[] args) {
          Host host = new Host();
          Proxy proxy = new Proxy(host);
          proxy.rent();
      }
  }
  ```

其中的注意点是无论是中介还是房东实现的都是租房子的接口，同时我们需要将指定的房东信息交给中介，其中中介还可以在`rent()`方法中内联一些其他操作（比如给**我们**看价格，跟**我们**交涉等）

这样就可以保证房东的纯粹性，同时又满足了客户的要求，如果没有中介存在，当我们需要特定需求时就需要频繁修改房东的代码，而这种修改代码的行为破坏了原有稳定的房东类结构，是开发中的大忌

这种一个中介绑定一个房东的模式就叫做静态代理，当然正由于他的一对一特性，当存在多个房东时就需要多个中介，久而久之还是会使得类太多而显得臃肿，这时候就出现了动态代理

同时代理模式还可以从另一个角度理解，当我们已经形成了标准的纵向基础开发层次（dao、service、controller、前端等），却缺乏完整的应用体系时，通过代理模式，我们可以面向基础层次中的某一层，在不改动其基础代码的前提下横向拓展其功能，这就是最重要的AOP思想，也就是面向切面编程

![image-20210923124348208](https://s2.loli.net/2021/12/06/w3OFREuXLagMVkZ.png)

##### 动态代理

上面我们已经引出了动态代理的概念，事实上，动态代理和静态代理在角色分工上相同，但是代理类时动态生成的，不是我们直接写好的

动态代理可以分为两大类，分别是基于接口的动态代理和基于类的动态代理

- 基于接口–JDK动态代理
- 基于类–cglib
- 还可以通过Java字节码实现（但是不适配于Tomcat）

了解动态代理需要知道反射和两个类，分别是`Proxy`和`InvocationHandler`，这些都是JavaSE反射包的类

当我们的Host和Rent文件都不变时，通过实现`InvocationHandler`接口建造一个动态代理工厂，它可以根据我们的需求生成不同的代理对象，对不同的真实对象进行代理

```java
@Data
public class DynamicProxy implements InvocationHandler {
    private Object target;

    public Object getProxy(){
        // 三个参数分别是获取代理类所使用的构造器，代理类需要实现的接口，代理类调用方法时调用谁的invoke方法
        return Proxy.newProxyInstance(this.getClass().getClassLoader(), target.getClass().getInterfaces(),this);
    }
    // 每当我们通过代理类调用一个方法时，就会走这个invoke方法（反射调用），如proxy.rent()时
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 动态代理的本质就是使用反射机制实现
        return method.invoke(target, args);
    }
}
```

对于invoke方法的使用及反射处理可以参考[前面章节](#反射)，下面通过客户调用动态代理工厂生成指定代理对象

```java
public class Client {
    public static void main(String[] args) {
        // 真实角色
        Host host = new Host();
        // 代理角色：利用代理类的处理程序生成一个代理角色，实现Rent接口
        DynamicProxy dynamicProxy = new DynamicProxy();
        dynamicProxy.setTarget(host);  // 生成的代理类要代理真实角色
        // 生成代理类相当于之前写好的静态代理类
        Rent proxy = (Rent) dynamicProxy.getProxy();
        proxy.rent();
    }
}
```

##### 走进AOP

在软件业，AOP为Aspect Oriented Programming的缩写，意为：面向切面编程，通过预编译方式和运行期间动态代理实现程序功能的统一维护的一种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![20181225093750237](https://s2.loli.net/2021/12/06/Ceg8wjPd6YHoMTc.png)

其中需要了解一些专有名词

- 切面(Aspect): 横切关注点(跨越应用程序多个模块的功能)被模块化的特殊对象；
- 通知(Advice): 切面必须要完成的工作；
- 目标(Target): 被通知的对象；
- 代理(Proxy): 向目标对象应用通知之后创建的对象；
- 连接点（Joinpoint）：程序执行的某个特定位置：如类某个方法调用前、调用后、方法抛出异常后等。连接点由两个信息确定：方法表示的程序执行点；相对点表示的方位。例如 ArithmethicCalculator#add() 方法执行前的连接点，执行点为 ArithmethicCalculator#add()； 方位为该方法执行前的位置；
- 切点（pointcut）：每个类都拥有多个连接点：例如 ArithmethicCalculator 的所有方法实际上都是连接点，即连接点是程序类中客观存在的事务。AOP 通过切点定位到特定的连接点。类比：连接点相当于数据库中的记录，切点相当于查询条件。切点和连接点不是一对一的关系，一个切点匹配多个连接点，切点通过 org.springframework.aop.Pointcut 接口进行描述，它使用类和方法作为连接点的查询条件。

当然这些概念实际上听也听不懂，我们在接下来的项目中在实践中理解

##### 简单实现

首先我们要导一个依赖包

```xml
    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.7</version>
            <scope>runtime</scope>
        </dependency>
    </dependencies>
```

创建服务层接口和实现类

```java
public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void select();
}
```

```java
@Service("service")  // 取个别名，初始名为userServiceImpl太长了
public class UserServiceImpl implements UserService{
    @Override
    public void add() {
        System.out.println("add");
    }

    @Override
    public void delete() {
        System.out.println("delete");
    }

    @Override
    public void update() {
        System.out.println("update");
    }

    @Override
    public void select() {
        System.out.println("select");
    }
}
```

接下来我们在不更改上面两个文件的前提下插入一些我们自己的方法（比如添加日志）

以下提供三种方式实现

1. 使用SpringAPI接口

   ```java
   @Component
   public class BeforeLog implements MethodBeforeAdvice {  // 这个接口专门在方法前使用
       @Override
       public void before(Method method, Object[] args, Object target) throws Throwable {
           System.out.println("BeforeLog.before");
       }
   }
   ```

   ```java
   @Component
   public class AfterLog implements AfterReturningAdvice {  // 这个接口在方法运行完之后使用
       // 可以拿到返回值
       @Override
       public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
           System.out.println("AfterLog.afterReturning & return result:" + returnValue);
       }
   }
   ```

   接着我们怎么将这两个日志方法切进服务类中的某一个方法中执行呢？

   这时候就需要配置文件发力

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:context="http://www.springframework.org/schema/context"
   xmlns:aop="http://www.springframework.org/schema/aop"
   xsi:schemaLocation="http://www.springframework.org/schema/beans
   https://www.springframework.org/schema/beans/spring-beans.xsd
   http://www.springframework.org/schema/context
   https://www.springframework.org/schema/context/spring-context.xsd
   http://www.springframework.org/schema/aop
   https://www.springframework.org/schema/aop/spring-aop.xsd">
   
   <context:component-scan base-package="com.test"/>
   <context:annotation-config/>
   
   <!--配置AOP-->
   <aop:config>
       <!--切入点: expression 表达式:execution(要执行的位置 格式：修饰词 返回值 列名 方法名 参数)-->
       <aop:pointcut id="pointCut" expression="execution(* com.test.service.UserServiceImpl.*(..))"/>
       <!--这就代表着将某一个类插入到UserServiceImpl的所有方法中，同时不管方法有什么参数（(..)）-->
       <aop:advisor advice-ref="beforeLog" pointcut-ref="pointCut"/>
       <aop:advisor advice-ref="afterLog" pointcut-ref="pointCut"/>
       <!--将我们写好的两个类插入方法-->
   </aop:config>
   
   </beans>
   ```

   记得加上头部信息，不然无法识别aop标标签

   测试类

   ```java
   @Test
   public void test1(){
       ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
       // 动态代理的是一个接口
       UserService service = context.getBean("service", UserService.class);
       service.add();
   }
   ```

2. 自定义类实现

   先随便写一个类，里面定义一些要切入的方法

   ```java
   @Component
   public class Customize {
       public void before(){
           System.out.println("Customize.before");
       }
   
       public void after(){
           System.out.println("Customize.after");
       }
   }
   ```

   然后同样通过配置文件自定义切入位置和切入方法

   ```xml
   <aop:config>
       <aop:aspect ref="customize">
           <!--定义切入点-->
           <aop:pointcut id="point" expression="execution(* com.test.service.UserServiceImpl.*(..))"/>
           <!--定义自定义类中的方法操作位置-->
           <aop:before method="before" pointcut-ref="point"/>
           <aop:after method="after" pointcut-ref="point"/>
       </aop:aspect>
   </aop:config>
   ```

   这种方法相对来说简单，但是功能不如前一种强大（前一种利用反射可以拿到方法的信息）

3. 纯注解实现AOP

   创建配置类

   ```java
   @Aspect  // 标注这个类是一个切面
   @EnableAspectJAutoProxy  // 想要让Aspect注解生效就要加这个注解
   @Component
   public class AnnotationMethod {
       @Pointcut("execution(* com.test.service.UserServiceImpl.*(..))")
       public void pc(){}
   
       @Before("pc()")
       public void before(){
           System.out.println("AnnotationMethod.before");
       }
   
       @After("pc()")
       public void after(){
           System.out.println("AnnotationMethod.after");
       }
   
       @Around("pc()")  // 了解一下Around注解
       public Object around(ProceedingJoinPoint pjp) throws Throwable {
           // 自动在执行方法之前卡住，先执行前部分代码
           Signature signature = pjp.getSignature();
           System.out.println("signature = " + signature);
           System.out.println("AnnotationMethod.around before");
           // 执行完之后会等待一个继续执行方法的指令
           Object proceed = pjp.proceed();// 执行之前的before方法及add方法内容，返回一个Object内容（但我不知道这个Object有什么用）
   // 执行完后目标方法后并发的执行后面的代码和after代码
           System.out.println("AnnotationMethod.around after");
           return proceed;
       }
   }
   ```

   直接写测试类

   ```java
   @Test
   public void test2(){
       AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
       context.scan("com.test");
       context.refresh();
       UserService service = context.getBean("service", UserService.class);
       service.add();
   }
   ```

#### 整合Mybatis

整合需要好多包，除了之前导入的webmvc包以外，还需要

```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.7</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.6</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.3.10</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.26</version>
    </dependency>
</dependencies>
```

接下来那一个流程走一遍

- 配置文件

  ```xml
  <?xml version="1.0" encoding="GBK" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  
  <configuration>
  
      <properties resource="db.properties"/>
  
      <settings>
          <setting name="logImpl" value="STDOUT_LOGGING"/>
          <setting name="mapUnderscoreToCamelCase" value="true"/>
      </settings>
  
      <typeAliases>
          <package name="com.test.pojo"/>
      </typeAliases>
  
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
  
      <mappers>
          <package name="com.test.mapper"/>
      </mappers>
  </configuration>
  ```

- 资源文件

  ```properties
  driver=com.mysql.cj.jdbc.Driver
  url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=UTF-8
  username=root
  password=123456
  ```

- 实体类

  ```java
  @Data
  public class User {
      private int id;
      private String name;
      private String pwd;
  }
  ```

- Mapper

  ```java
  public interface UserMapper {
      @Select("select * from mybatis.user")
      public List<User> selectUser();
  }
  ```

- 测试类

  ```java
  public class MTest {
  
      @Test
      public void test() throws IOException {
          InputStream in = Resources.getResourceAsStream("mybatis-config.xml");
          SqlSessionFactory build = new SqlSessionFactoryBuilder().build(in);
          SqlSession session = build.openSession(true);
          UserMapper mapper = session.getMapper(UserMapper.class);
          for (User user : mapper.selectUser()) {
              System.out.println(user);
          }
      }
  
  }
  ```

这样看起来其实也还是挺简单的，看看这文件结构也挺清晰

![image-20210925175326270](https://s2.loli.net/2021/12/06/BNyr5p8nPWCe3wG.png)

然后就让我们正式进入`Mybatis-Spring`中

##### 原始方法

为了实现Spring代理数据源，我们需要通过bean的方式替代mybatis中的环境配置信息

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop 
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <context:property-placeholder location="db.properties"/>
    <!--DataSource：使用Spring的数据源替换Mybatis配置-->
    <bean id="datasource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
    </bean>

</beans>
```

既然这边已经设定了数据源，另一边的环境信息就可以删掉了

```xml
<!--这些都可以删了-->
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

接着在Spring中创建一个SQLSession工厂，来制造sqlsession

然后我们甚至可以顺便把mybatis-config配置文件中的所有标签都移过来

```xml
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="datasource"/>
        <!--绑定Mybatis配置文件-->
        <property name="mapperLocations" value="com/test/mapper/*"/>
        <property name="typeAliases" value="com.test.pojo.User"/>
    </bean>
```

当然这样并不能解耦配置文件，看着也挺烦的，最好还是在其中引用一下mybatis的配置文件，mybatis相关配置文件还是在相应xml中配置

```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="datasource"/>
    <property name="configLocation" value="mybatis-config.xml"/>
</bean>
```

现在我们有了工厂，下一步就是制造SqlSession

这时候就需要介绍Spring的一个Template（模板）习惯，很多的类在Spring内部都成了一个个`xxxTemplate`，实际上他和原本的类别无二致，我们不需要额外学习别的内容，`SqlSessionTemplate`就是一个例子

```xml
<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
    <!--使用构造器注入参数，创建一个SqlSession需要一个工厂，把工厂传进去即可-->
    <constructor-arg ref="sqlSessionFactory"/>
</bean>
```

到此为止，我们其实已经获得了一个SqlSession了（Spring中叫SqlSessionTemplate），接着我们要怎么用这个SqlSession呢，还是通过测试类中的context上下文调用吗？

事实上我们可以再创建一个Mapper类，通过定义方法的方式之后从外部调用方法

```java
@Data
public class UserMapperImpl implements UserMapper{

    // 现在使用SqlSessionTemplate来执行
    private SqlSessionTemplate sqlSession;

    @Override
    public List<User> selectUser() {
        // 从之前的通过测试类配置，到现在整合到一个类中实现
        return sqlSession.getMapper(UserMapper.class).selectUser();
    }
}
```

记得要在Spring中注册Bean

```xml
<bean id="userMaaper" class="com.test.mapper.UserMapperImpl">
    <property name="sqlSession" ref="sqlSession"/>
</bean>
```

终于大功告成，让我们在测试类中测试一下效果

```java
public class MTest {

    @Test
    public void test(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        UserMapper userMapper = context.getBean("userMapper", UserMapper.class);
        for (User user : userMapper.selectUser()) {
            System.out.println("user = " + user);
        }
    }

}
```

> 发现报了一个错，`com.mysql.jdbc.exceptions.jdbc4.MySQLNonTransientConnectionException: Public Key Retrieval is not allowed`
>
> 上网查了一下有些说`db.properties`的url没写对，加个`allowPublicKeyRetrieval=true`之后变成了`Access denied for user 'lenovo'@'localhost' (using password: YES)`这个错误，看来是数据库什么用户信息搞错了，后来发现`username`和`password`是jdbc还不xml里面的两个关键字，编译的时候不会被识别为调用资源类的信息，所以我们只需要把名字改一改即可
>
> ```properties
> driver=com.mysql.cj.jdbc.Driver
> url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=UTF-8
> a.username=root
> a.password=123456
> ```
>
> 记得Spring配置文件里也要改哦

##### 终极简化使用SqlSession

```java
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper {
    @Override
    public List<User> selectUser() {
        return getSqlSession().getMapper(UserMapper.class).selectUser();
    }
}
```

这时候在配置文件中直接给他注入一个SqlSessionFactory即可

```xml
<bean id="impl2" class="com.test.mapper.UserMapperImpl2">
    <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
</bean>
```

这样直接省略了配置文件中的两步获得SqlSession和类中的一个私有SqlSession方法，获得工厂后直接可以使用，还是比较方便的

#### 声明式事务

[事务](#事务)内容之前提到过，这里就不再提了

*MyBatis-Spring 允许 MyBatis 参与到 Spring 的事务管理中。而不是给 MyBatis 创建一个新的专用事务管理器，MyBatis-Spring 借助了 Spring 中的 `DataSourceTransactionManager` 来实现事务管理*

在Spring中，事务可以通过AOP的方式织入某个程序中，使得在执行指定方法的时候开启/关闭事务

首先要更改Spring配置文件的头部信息，引入事务标签包

```xml
xmlns:tx="http://www.springframework.org/schema/tx"
```

然后在配置文件中配置声明式事务及配置事务通知

配置声明式事务之后，就会在该数据源中建立事务管理系统，当我们需要给数据源传输数据时会经过这个系统判别是否需要创建及提交事务

```xml
<!--配置声明式事务-->
<bean class="org.springframework.jdbc.datasource.DataSourceTransactionManager" id="transactionManager">
    <property name="dataSource" ref="datasource"/>
</bean>
<!--配置事务通知-->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <!--想给哪些方法配置事务-->
    <!--配置事务的传播特性-->
    <tx:attributes>
        <tx:method name="delete" propagation="REQUIRED"/>
        <tx:method name="insert" propagation="REQUIRED"/>
        <!--所有方法则用"*"代替方法名-->
    </tx:attributes>
</tx:advice>
```

> 事务通知类型有七种，默认就是REQUIRED
>
> *REQUIRED：支持当前事务，如果当前没有事务，就新建一个事务。这是最常见的选择。* 
>
> *SUPPORTS：支持当前事务，如果当前没有事务，就以非事务方式执行。* 
>
> *MANDATORY：支持当前事务，如果当前没有事务，就抛出异常。* 
>
> *REQUIRES_NEW：新建事务，如果当前存在事务，把当前事务挂起。* 
>
> *NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。* 
>
> *NEVER：以非事务方式执行，如果当前存在事务，则抛出异常。* 
>
> *NESTED：支持当前事务，如果当前事务存在，则执行一个嵌套事务，如果当前没有事务，就新建一个事务。*

同时在Mapper增加增删事务操作

```java
@Component
public interface UserMapper {
    @Select("select * from mybatis.user")
    public List<User> selectUser();
    @Delete("delete from mybatis.user where id=#{id}")
    public int delete(int id);
    @Insert("insert into mybatis.user (id, name, pwd) values (#{id}, #{name}, #{pwd})")
    public int insert(User user);
}
```

从上可以看出，`tx:method`标签应与mapper中需要创建事务的方法一一对应

之后结合AOP方式切入事务内容

```xml
    <!--结合AOP-->
    <!--配置事务切入-->
<!--    <bean class="com.test.mapper.UserMapper"/>-->
    <!--注意这里必须要导入接口类，因为我们的sql代码注解是编写在接口上的，不然Spring无法识别方法-->
    <aop:config>
        <aop:pointcut id="pc" expression="execution(* com.test.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="pc"/>
    </aop:config>
```

这样就可以实现事务的自动提交及回滚

### SpringMVC

MVC架构之前有所提及，就是模型（Model），视图（View），控制器（Controller）的简写，是一种设计规范

注意到最典型的MVC就是JavaBean+JSP+servlet的模式，分别对应着上面的三层结构

#### 回顾Servlet+Tomcat

创建普通Maven父项目，删除src目录，导入公共依赖

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.1</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>

    <!--Tomcat10 Servlet依赖-->
    <!--jsp的依赖-->
    <dependency>
        <groupId>jakarta.servlet.jsp</groupId>
        <artifactId>jakarta.servlet.jsp-api</artifactId>
        <version>3.0.0</version>
        <scope>provided</scope>
    </dependency>
    <!--jar包的依赖-->
    <dependency>
        <groupId>jakarta.servlet</groupId>
        <artifactId>jakarta.servlet-api</artifactId>
        <version>5.0.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

创建web子项目，注意先创建一个普通项目再通过添加框架支持添加web框架

![image-20210928121437118](https://s2.loli.net/2021/12/06/6QxlvpZEAGktK8R.png "项目结构")

如图最终效果应该是在web目录上有一个蓝色小点点，Tomcat就是通过它来确认是否为web项目

之后让我们创建一个简单的由主页传参给Sevlet并返回到指定页面的小项目

- 让我们从Servlet开始（Controller）

  ```java
  public class Demo1 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          // 获取前端参数
          String method = req.getParameter("method");
          if (method.equals("add")){
              req.getSession().setAttribute("msg","add");
          }
  
          // 调用业务层
          req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,resp);
      }
  }
  ```

  之后记得再web.xml中注册内容

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
           version="5.0">
  
      <servlet>
          <servlet-name>demo01</servlet-name>
          <servlet-class>com.test.Demo1</servlet-class>
      </servlet>
      <servlet-mapping>
          <servlet-name>demo01</servlet-name>
          <url-pattern>/1</url-pattern>
      </servlet-mapping>
  
      <session-config>
          <session-timeout>15</session-timeout>
      </session-config>
  
      <welcome-file-list>
          <welcome-file>index.jsp</welcome-file>
      </welcome-file-list>
  
  </web-app>
  ```

- 然后我们在`/WEB-INF/jsp/test.jsp`下开始设计返回目标的jsp（View）

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
      ${msg}
  </body>
  </html>
  ```

- 之后是请求页面（index.jsp）

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
    <head>
      <title>$Title$</title>
    </head>
    <body>
      <form action="1" method="get">
        <label>
          <input type="text" name="method">
        </label>
        <input type="submit">
      </form>
    </body>
  </html>
  ```

- 然后配置Tomcat环境和建立应用程序上下文，启动项目，在地址栏输入`http://localhost:8080/1?method=add`或者在表单填入add再提交即可看到我们的test.jsp页面

搞清楚这些底层的内容之后，我们就开始正式的进入SpringMVC的学习中

#### 简单入门

SpringMVC有这些特点

- 轻量级，简单易学
- 高效，基于请求和响应的MVC框架
- 和Spring兼容性好，无缝结合
- 约定大于配置
- 功能强大（RESTful，数据验证，格式化，本地化，主题）
- 简介灵活

Spring的web框架围绕着DispatcherServlet设计，它可以理解为一个管理各种Servlet的调度器，它将请求分发到不同的处理器，同时它的本质也是一个Servlet

进入SpringMVC之后，注解就大于配置了，任何情况下都最好使用注解进行各种控制

口说无凭，不如先通过自己的操作动手搭建一个SpringMVC环境

1. 配置`web.xml`内容

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
            version="5.0">
   
       <servlet>
           <servlet-name>springmvc</servlet-name>
           <!--导入DispatcherServlet，用它来管理我们的Servlet-->
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
           <!--为DispatcherServlet关联一个配置文件-->
           <init-param>
               <param-name>contextConfigLocation</param-name>
               <!--于是下一步我们需要创建一个配置文件
                   注意：classpath指的就是resource目录-->
               <param-value>classpath:springmvc-servlet.xml</param-value>
           </init-param>
           <load-on-startup>1</load-on-startup>
       </servlet>
       <!--使得DispatcherServlet对所有页面生效（类似过滤器？）-->
       <servlet-mapping>
           <servlet-name>springmvc</servlet-name>
           <url-pattern>/</url-pattern>
       </servlet-mapping>
   
   </web-app>
   ```

2. 由于上面导入了某xml，所以下一步是在resource目录下配置Spring的配置文件`springmvc-servlet.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
       <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
   
       <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="resolver">
           <!--前缀，因为我们请求的路径将不会是一个完整的路径-->
           <property name="prefix" value="/WEB-INF/jsp/"/>
           <!--后缀，程序会自动给我们的名字拼接上这个前后缀-->
           <property name="suffix" value=".jsp"/>
       </bean>
   
       <!--Handler-->
       <bean id="/t" class="com.test.controller.CDemo1"/>
   
   </beans>
   ```

3. 然后我们的配置工作暂告一段落，接下来我们需要创建控制类，实现Controller接口

   ```java
   public class CDemo1 implements Controller {
       @Override
       public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) {
           // ModelAndView模型和视图
           ModelAndView mv = new ModelAndView();
           // 封装对象啊那个，放在ModelAndView中
           mv.addObject("msg","Demo1");
           // 封装要跳转的视图，同样放在ModelAndView中
           mv.setViewName("test");  // /WEB-INF/jsp/test.jsp
           return mv;
       }
   }
   ```

4. 最后在把上一个项目的jsp文件拿过来即可，最终呈现的文件效果如图

   ![image-20210928162159966](https://s2.loli.net/2021/12/06/vZCytWxRUgF59q8.png)

> 由于我们是在Maven空项目中添加的框架支持，实际上并不算是完全的web项目，因此项目结构中并没有lib目录，Tomcat也无法从我们的lib目录中寻找到我们依赖的包（包括Springwebmvc等），无法正确识别我们的请求，因此在我们启动项目发送请求后会报404错误，这时候就需要我们手动创建lib目录并导包
>
> 先打开项目结构，选择工件
>
> ![image-20210928163823440](https://s2.loli.net/2021/12/06/qPi1Aw5IgLb6aGc.png)

接着启动项目，请求`http://localhost:8080/t`查看是否正常跳转到damo1

![image-20210928164129520](https://s2.loli.net/2021/12/06/gpX4wmORW8GLNJM.png)



#### 原理分析

在完成了这个项目之后，我们来通过一张图清晰的了解SpringMVC的工作原理

![image-20210928133253545](https://s2.loli.net/2021/12/06/AeOHjF6wGUtzR9X.png)

如图当一个用户发送请求时（比如说`/t`），请求会交给前端控制器（DispatcherServlet，即`web.xml`中编写的内容），之后前端控制器会向他自己绑定的配置文件中（springmvc-servlet.xml）通过HandlerMapping（Spring配置文件中设定的bean）查询需要的处理器（Handler）信息并返回结果，然后查到了我们创建的控制类处理器（CDemo1），于是通过HandlerAdapter（也是Spring配置文件中创建的bean）去执行控制类，在控制类中我们对请求进行了简单的处理（比如携带msg键值，设置视图名字为demo1），之后返回给前端控制器一个ModelAndView（mv），前端控制器再根据ViewResolver（Spring配置文件中的bean）对返回来的ModelAndView进行装饰（比如加上前缀后缀），并渲染成响应数据返回给用户

但是这样开发还是比较麻烦，每编写一个控制类都需要去Spring当中注册一个bean，一点都不智能，这时候就需要强大的注解功能出马

#### 注解实现

在原有的配置文件中，我们只需要修改Spring配置文件中的内容，为该SpringMVC项目添加注解支持

```xml
<context:component-scan base-package="com.test.controller"/>
<mvc:default-servlet-handler/>
<mvc:annotation-driven/>
```

第一个标签前面使用过，是扫包标签

第二个标签代表着启用mvc默认的Servlet构建Handler程序，意味着像是css、js等静态资源请求不会将其交给前端控制器，避免了直接请求静态资源导致的找不到内容

> 如果交给前端控制器，他又会去匹配配置文件中的处理器（Handler），然而我们并没有配置直接请求静态资源的处理器，但是这个静态资源又是确实存在的，于是当然会找不到内容

第三个标签表示启动支持mvc注解驱动，其中自动配置了之前的HandlerMapping和HandlerAdapter

因此之前配置的两个bean都可以删去了！

之后我们修改对应的控制类内容，实现利用注解开发

```java
@Controller
public class Demo1 {
    @RequestMapping("/t")  // 请求/t的时候走这个控制器
    public String test(Model model){
        // 封装数据
        model.addAttribute("msg","Demo1!");
        return "test";  // 返回的字符串就是转发到的jsp文件名字
    }
}
```

你可能不相信，但是确实这样就已经可以运行了

会发现现在的控制类中被传入了Model来植入携带信息，而用返回值携带View视图名字，等于说在之前的图中的前端控制器和处理器之间被中间又被`annotation-driven`又加了一层，用以使ModelAndView拆分成Model和View模块再只将Model传到我们的控制类中，实现了进一步的解耦

#### 数据处理

前端传参的时候我们后端需要对请求的参数进行接收和处理，这时候就需要在控制类中添加参数接收内容

```java
@Controller
public class Demo2 {
    @RequestMapping("/add")
    public String test1(int a, int b, Model model){  // 前端给我们传的参数必须跟这里参数保持一致
        int res = a + b;
        model.addAttribute("msg","结果："+res);
        return "test";
    }
}
```

之后通过`/add?a=1&b=2`来传参，a和b的值就会被传到我们的控制类

![image-20210929192220523](https://s2.loli.net/2021/12/06/LsuGD2fX4UjMyaV.png)

如果不想让前端和我们的参数名保持一致，就需要`@RequestParam`注解

```java
 @Controller
 public class Demo2 {
     @GetMapping("/t2")
     public String test1(@RequestParam("a1") int a,@RequestParam("b1") int b, Model model){ 
         int res = a + b;
         model.addAttribute("msg","结果："+res);
         return "test";
     }
 }
```

这时候就需要`/add?a1=1&b1=2`传参，但是并没有什么意义

实际开发中，前端传过来的往往不是某一个参数而是一个对象，这时候我们就需要创建实体类接收

比如我们有一个User对象

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
}
```

如果把实体类作为参数，当前端传参的时候就需要对每一个参数都分别传送，Spring会将其打包成对象

```java
@Controller
public class Demo4 {
    @GetMapping("/t4")
    public String test(User user, Model model){
        model.addAttribute("msg",user.getId()+" "+user.getName());
        return "test";
    }
}
```

这时候就需要这样传入参数`http://localhost:8080/t4?id=1&name=1`

不过注意到，并不建议这样进行传参，因为这样就无法运用Restful风格和别名简化传参

会发现当传入数据不太多时，直接

#### RestFul风格

Restful风格就是一个URL显示的风格形式，将地址栏中的比如`?`、`=`等乱七八糟的符号删去，全部变成`/`分隔，现在几乎所有的网站上都在使用

![image-20210929185910968](https://s2.loli.net/2021/12/06/x43d2Bo9vPybWSg.png)

传统的方式操作资源只能通过`GET`或`POST`方式通过请求不同的资源来获得不同的内容

而RestFul风格的重心是以对统一资源不同的请求方式来获得不同的内容效果

想使用RestFul风格，就只需要在上面的基础上修改`RestMapping`并增添`@PathVariable`注解即可

```java
@RequestMapping(value = "/add/{a}/{b}",method = RequestMethod.DELETE)
public String test1(@PathVariable int a,@PathVariable int b, Model model){}
```

> ```java
> @RequestMapping("/add/${a}/${b}")
> ```
>
> 直接这样修改RestMapping好像也可以，不知道是不是IDEA优化了还是这就是jQuery的某一种方式

之后就可以直接在地址栏输入`/add/1/2`即可对a，b参数赋值

这只是最基础的内容，要实现不同方式请求获得不同内容，就需要给ResultMapping加上请求类型

```java
@RequestMapping(value = "/add/${a}/${b}",method = RequestMethod.DELETE)
```

这样之后我们如果还跟之前一样输入地址，就会报405错误，因为默认的请求方法是GET，而本程序不支持

```java
@DeleteMapping("/add/{a}/{b}")
```

当然这样也可以，算是另一种方式

RestFul风格可以让URL变得更加简洁、高效和安全，别人不再知道传入的参数在服务器里到底是什么东西

#### 结果跳转方式

正常的Servlet转发和重定向必须得通过req和resp的方法实现，在Spring中可以被简化，在return中可以通过前缀实现转发和重定向

其中在拥有视图解析器的情况下，转发并不需要加前缀，而如果想要重定向就在前面加上`redirect:`即可

```java
@Controller
public class Demo3 {
    @RequestMapping("/t3")
    public String test(){
        return "redirect:/index.jsp";
    }
}
```

> 事实上如果我们把Spring配置文件中的所有东西都删掉，只留一个扫包标签，即没有视图解析器和HandlerMapping等等，这时候我们依然可以在控制类中通过前缀+全路径`return "forward:/WEB-INF/jsp/test.jsp";`的返回值实现转发

==注意重定向不能重定向到WEB-INF目录，因为他是隐藏的==

#### 乱码问题

当我们在前端提交一个中文参数的请求时，在转发的时候在Java层面上就会出现乱码，也就是根本无法把中文参数传到后端

![image-20211003163821782](https://s2.loli.net/2021/12/06/pJi9ErgqQeNB1Hk.png)

![image-20211003163840065](https://s2.loli.net/2021/12/06/PU8xOCtMRy4fsI2.png)

这时候就需要通过过滤器劫持前端发到后端的请求，进行utf-8编码后再传到后端

```java
public class EncodingF implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

做完之后记得在`web.xml`中添加过滤器依赖

```xml
<filter-mapping>
    <filter-name>encoding</filter-name>
    <url-pattern>/t5</url-pattern>
</filter-mapping>
<filter>
    <filter-name>encoding</filter-name>
    <filter-class>com.test.filter.EncodingF</filter-class>
</filter>
```

同时注意到get方法在Tomcat中会自动解决乱码，所以此处模拟时的post提交非常重要，这样才能看出是否解决乱码问题

当然这是我们自己写的乱码，事实上SpringMVC也给我们提供了一个写好了的乱码过滤器，此时我们只需要在`web.xml`中，直接配置即可

> 同时还需要注意一下，乱码过滤器在`web.xml`中作用域如果要是所有网页就应该写`/*`而不是`/`，因为`/`不过滤`.jsp`一类的文件请求，当展示页面的时候过滤器不生效（详见[过滤器](#Filter)）

#### 后端解析JSON

在讲JavaScript的时候我们[提到了](#JSON对象)JSON是一个什么东西，我们学习了怎么在前端把数据存储为JSON格式，现在我们则需要学习怎么在后端解析前端发来的JSON内容

当然因为JSON只是一个字符串，常理来说我们也可自己写一个对象转换JSON的方法，但是没必要，很多人已经帮我们写好了，常见的有 Jackson，Fastjson，gson等等

这里使用gson演示，这些工具实际上都大同小异

首先导入Gson依赖

```xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.8</version>
</dependency>
```

> 注意之后加载项目之前务必要在项目结构中那个将gson的包丢进去，不然会报`NoClassDefFoundError`的错

之后编写控制类，并创建Gson对象调用方法即可

```java
@Controller  // 这里改成RestController也可以实现下面ResponseBody一样的效果，只是作用域是一个类
public class Demo6 {
    @GetMapping(value = "/t6",produces = "text/html;charset=utf-8") // 设置传输给生成的文件的编码格式
    @ResponseBody  // 加上这个注解下面的方法就不会走视图解析器，也就不会请求转发给test.jsp
    // 而是会直接返回一个字符串到网页上（生成一个html文件然后在body里面直接插入返回内容，就是这么暴力）
    public String json(){
        User user = new User(1, "测试");
        Gson gson = new Gson();
        return gson.toJson(user);
    }
}
```

Gson相关方法还有比如说将JSON转换为对象等等， 功能还是挺强大的

#### Ajax

*AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。*

*AJAX 不是新的编程语言，而是一种使用现有标准的新方法。*

*AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。*

*AJAX 不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行。*

Ajax实际上就是一个弹窗，不熟悉的话我们的HTML也有一个iframe标签，利用它可以简单的了解弹窗效果

下面是用纯HTML做的页内弹窗，实现弹窗内显示我们需要访问的网站

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script>
        function g(){
            let value = document.getElementById("url").value;
            document.getElementById("iframe1").src=value;
        }
    </script>
</head>
<body>
<div>
    <p>请输入地址：</p>
    <p>
        <input type="text" id="url">
        <input type="button" value="提交" onclick="g()">
    </p>
</div>

<div>
    <iframe id="iframe1" style="width: 50%;height: auto"></iframe>
</div>
</body>
</html>
```

当然这并不是真正的Ajax，Ajax的核心是XHR（XMLHttpRequest），在原生Javascript中，我们要通过创建一个XHR对象来实现Ajax，然而现在有很多种简便的方法，其中jQuery提供了多个与Ajax有关的方法

下面是前端利用了jQuery的post方法（内含一个Ajax请求）来实现请求后台数据并展示

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script
            src="https://code.jquery.com/jquery-3.6.0.js"
            integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk="
            crossorigin="anonymous"></script>
    <script>
        function a(){
            $.post("${pageContext.request.contextPath}/ajax",function (data){
                let html="";
                for (let i = 0; i < data.length; i++) {
                    html += "<tr>"
                        +"<td>"+data[i].id+ "</td>"
                        +"<td>"+data[i].name+ "</td>"
                        +"<td>"+data[i].age+ "</td>"
                        +"</tr>"
                }  // 这里使用了非常复杂的字符串拼接操作，等到学到vue了以后就会被简化
                $("#context").html(html);
            })
        }
    </script>
</head>
<body>
    <label>
        <input type="button" id="btn" onclick="a()" value="显示内容">
    </label>
<table>
    <tr>
        <td>id</td>
        <td>name</td>
        <td>age</td>
    </tr>
    <tbody id="context">
    </tbody>
</table>
</body>
</html>
```

前端的繁琐使得我们后端变得十分简便，只需要无脑给前端传参数即可

```java
@RequestMapping("/ajax")
@ResponseBody  // 注意不要不小心带视图解析器了，只是单纯的返回数据即可
public List<User> test1(){
    User test1 = new User(1, "test1", 1);
    User test2 = new User(2, "test2", 2);
    User test3 = new User(3, "test3", 3);
    List<User> users = new ArrayList<>();
    users.add(test1);
    users.add(test2);
    users.add(test3);
    return users;
}
```

其中User类也十分简单

```java
@Data
@AllArgsConstructor
public class User {
    private int id;
    private String name;
    private int age;
}
```

如此就可以不刷新页面实现展示不同内容的功能

可以看出，Ajax把大部分内容都交给了前端，前后端仅通过XHR沟通，同时也避免了频繁刷新页面和设计过多不同页面的困扰

#### 拦截器

拦截器是AOP思想的具体应用，横切进某个具体方法中进行拦截，同时它只会拦街访问的控制器方法，如果访问的是jsp/html/css/image/js等静态资源则不会进行拦截（就算你在配置文件中写`/**`，这也体现了它运行在SpringMVC层上的特点）

SpringMVC提供了独有拦截器的功能，想要实现拦截器，只需要实现其中的`HandlerInterceptor`接口即可

> 在前面学习过滤器的时候我们使用过滤器实现了[拦截功能](#拦截请求)，虽然这个拦截器不是由web端执行，但是思路上面都是大差不差

该接口有三个需要实现方法（当然也可以不实现），分别对应着在方法前拦截，方法后拦截及清理的功能

```java
public class MInterceptor implements HandlerInterceptor {
    @Override
    // 这里return true就代表放行，执行下一个拦截器，相当于过滤器中clain.forward();
    // 请求前拦截
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("MInterceptor.preHandle");
        return true;
    }

    // 请求后拦截
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("MInterceptor.postHandle");
    }

    // 清理内容
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("MInterceptor.afterCompletion");
    }
}
```

由于拦截器是SpringMVC提供的，所以接下来要在`ApplicationContext.xml`而不是`web.xml`里面配置，意味着不是让Tomcat拦截而是SpringMVC，这也正体现了Spring独有的AOP思想

```xml
<mvc:interceptors>
    <mvc:interceptor>
        <mvc:mapping path="/**"/> <!--**代表这个请求下面的所有请求，*只代表当前文件夹下的某个请求-->
        <bean class="com.test.config.MInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
```

一般来说，最重要的是第一个请求前拦截（毕竟你方法都执行完了也没必要拦截了），在方法执行之前判断是否能让这个方法执行（返回值），后两个一半是作为日志或者其他无关紧要的内容

同时接口内还有req和resp参数，可以在拦截之后让用户跳转到其他页面（登陆页面等）

由于之前写过，此处就不再赘述了，详细可以看前面的[Filter](#Filter)内容

#### 文件传输

需要进行文件传输，首先要导入文件上传和下载的包

```xml
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.2</version>
</dependency>
```

> 我们使用的文件上传的手段是通过Apache的一个文件上传组件来实现，上面的导入包及下面的前端表单配置内容都是这个文件上传包的要求所致

需要在前端传输文件，需要在表单中的`enctype`属性指定为`multipart/form-data`属性

```xml
<form action="${pageContext.request.contextPath}/file" enctype="multipart/form-data" method="post">
  <input type="file" name="file">
  <input type="submit" value="submit">
</form>
```

接下来我们要利用SpringMVC给我们的文件上传的支持，因此需要在配置文件中创建bean

```xml
<bean class="org.springframework.web.multipart.commons.CommonsMultipartResolver" id="multipartResolver">
    <property name="defaultEncoding" value="utf-8"/>
    <property name="maxUploadSize" value="10485760"/>
    <property name="maxInMemorySize" value="40960"/>
</bean>
```

下一步就是编写Controller内容

```java
@PostMapping("/file")
@ResponseBody
public String upload(@RequestParam("file") CommonsMultipartFile file, HttpServletRequest req)
        throws IllegalStateException, IOException {
    String path=req.getServletContext().getRealPath("/upload");  // 创建文件放置目录
    File realPath = new File(path);  // 将字符串存储为一种地址格式
    if (!realPath.exists()){  // 判断目录是否存在，不存在就创建一个
        realPath.mkdir();
    }
    file.transferTo(new File(realPath+"/"+file.getOriginalFilename()));
    // 调用Spring提供的文件类方法，快速将目标文件存储于指定目录
    return "success";
}
```

同时这些文件上传的操作只需要理解但不需要记忆，哪天需要用到了直接上网搜索复制即可

相比较与上传文件的繁琐，下载文件只需要在a标签中添加文件的所在位置即可，浏览器会自动下载内容

### SSM整合

三个模块基本都讲解完毕，接下来就可以运用SSM框架开发了

#### 准备工作

网站实际上就是一系列围绕数据库做的工作，所以一切要从创建数据库开始

```sql
CREATE DATABASE `ssmbuild`;
USE `ssmbuild`;
CREATE TABLE `books`(
                        `bookID` INT NOT NULL AUTO_INCREMENT COMMENT '书id',
                        `bookName` VARCHAR(100) NOT NULL COMMENT '书名',
                        `bookCounts` INT NOT NULL COMMENT '数量',
                        `detail` VARCHAR(200) NOT NULL COMMENT '描述',
                        KEY `bookID`(`bookID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `books`(`bookID`,`bookName`,`bookCounts`,`detail`)VALUES
                                                                  (1,'Java',1,'从入门到放弃'),
                                                                  (2,'MySQL',10,'从删库到跑路'),
                                                                  (3,'Linux',5,'从进门到进牢');
```

下一步当然是导入依赖

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.26</version>
    </dependency>
    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP</artifactId>
        <version>5.0.0</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.6</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.10</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.3.10</version>
    </dependency>

</dependencies>
```

然后连接数据库，建立层级包，创建配置文件，最终效果如图

![image-20211003203335687](https://s2.loli.net/2021/12/06/My5VxO4ziwBhAtg.png)

#### Mybatis层

Mybatis要做的内容是十分简单，即创建实体类，mapper内容，mybatis配置文件及业务层调用

- 实体类

  ```java
  @Data
  @AllArgsConstructor
  @NoArgsConstructor
  public class Books {
      private int bookID;
      private String bookName;
      private int bookCounts;
      private String detail;
  }
  ```

- Mapper接口及sql实现

  ```java
  public interface BookMapper {
      int addBook(Books books);
      int delBookByID(int id);
      int updBook(Books books);
      Books queBookByID(int id);
      List<Books> queBooks();
  }
  
  ```

  ```xml
  <?xml version="1.0" encoding="GBK" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <mapper namespace="com.test.mapper.BookMapper">
      <insert id="addBook" parameterType="books">
          insert into ssmbuild.books (bookID, bookName, bookCounts, detail)
          values (#{bookID},#{bookName},#{bookCounts},#{detail});
      </insert>
      <delete id="delBookByID" parameterType="_int">
          delete
          from ssmbuild.books
          where bookID = #{id};
      </delete>
      <update id="updBook" parameterType="books">
          update ssmbuild.books
          set bookName = #{bookName},bookCounts=#{bookCounts},detail=#{detail}
          where bookID=#{b};
      </update>
      <select id="queBookByID" resultType="books">
          select *
          from ssmbuild.books where bookID=#{id};
      </select>
      <select id="queBooks" resultType="books">
          select *
          from ssmbuild.books;
      </select>
  </mapper>
  ```

- 业务层接口及实现

  ```java
  public interface BookService {
      int addBook(Books books);
      int delBookByID(int id);
      int updBook(Books books);
      Books queBookByID(int id);
      List<Books> queBooks();
  }
  ```

  ```java
  @Data
  public class BookServiceImpl implements BookService{
  
      // 业务层就需要调用dao层，目的就是组合dao
      private BookMapper bookMapper;
  
      @Override
      public int addBook(Books books) {
          return bookMapper.addBook(books);
      }
  
      @Override
      public int delBookByID(int id) {
          return bookMapper.delBookByID(id);
      }
  
      @Override
      public int updBook(Books books) {
          return bookMapper.updBook(books);
      }
  
      @Override
      public Books queBookByID(int id) {
          return bookMapper.queBookByID(id);
      }
  
      @Override
      public List<Books> queBooks() {
          return bookMapper.queBooks();
      }
  }
  ```

  看似似乎业务层和dao层没有什么区别，实际上业务层将会连接Spring并通过Spring注入来传参，而dao层只由业务层调用并传参，既保证安全，有避免耦合

- 配置文件

  ```xml
  <?xml version="1.0" encoding="GBK" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
          
  <configuration>
  
      <properties resource="db.properties"/>
  
      <settings>
          <setting name="logImpl" value="STDOUT_LOGGING"/>
          <setting name="mapUnderscoreToCamelCase" value="true"/>
      </settings>
      
      <typeAliases>
          <package name="com.test.pojo"/>
      </typeAliases>
      
      <mappers>
          <package name="com.test.mapper"/>
      </mappers>
  </configuration>
  ```

  当然还有资源类，此处省略

#### Spring层

Spring层的重点就是整合项目中的各层内容，即对各种内容编写配置文件，在我们的项目中即配置Dao层（连接数据库）和Service层（被web项目调用）

由于我们要对不同的层配置不同的文件，因此为了分工明确且解耦，我们需要创建多个Spring配置文件，并且将它们添加到同一个上下文当中，保证各个配置文件能够相互引用beanid，如图所示，一般来说创建Spring配置文件之后会自动提示配置上下文

![image-20211004154102035](https://s2.loli.net/2021/12/06/M4DcI98gzplaACW.png)

当然也可以通过`import`标签在一个配置文件中引入另一个，但是配置在同一个上下文既安全又高效

- Dao层配置文件（`spring-dao.xml`）

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/aop 
          https://www.springframework.org/schema/aop/spring-aop.xsd">
  
      <!--关联数据库配置文件-->
      <context:property-placeholder location="classpath:db.properties"/>
      <!--连接池-->
      <bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource">
          <property name="driverClassName" value="${jdbc.driver}"/>
          <property name="jdbcUrl" value="${jdbc.url}"/>
          <property name="username" value="${jdbc.username}"/>
          <property name="password" value="${jdbc.password}"/>
      </bean>
      <!--SqlSessionFactory-->
      <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
          <property name="dataSource" ref="dataSource"/>
          <!--绑定Mybatis配置文件-->
          <property name="configLocation" value="classpath:mybatis-config.xml"/>
      </bean>
      <!--配置dao接口扫描包，动态实现Dao接口可以注入到Spring容器中-->
      <!--通俗来讲就是省去了原先的创建SqlSession类的过程
          现在由Spring自动根据Mapper生成SqlSession，变得更加简单！-->
      <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
          <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
          <property name="basePackage" value="com.test.mapper"/>
      </bean>
  
  </beans>
  ```

  注意到在获取SqlSession方面采用了更加简便的自动生成的方法，避免了创建多个实现类的繁琐

- Service层（`spring-service.xml`）

  ```xml
  <!--Service层内容，头部内容省去-->
  <!--扫包-->
  <context:component-scan base-package="com.test.service"/>
  <!--将所有业务类注入到Spring，此处使用注解形式-->
  <!--声明式事务配置-->
  <bean class="org.springframework.jdbc.datasource.DataSourceTransactionManager" id="transactionManager">
      <property name="dataSource" ref="dataSource"/>
  </bean>
  
  <!--AOP事务支持，这个项目中用不到-->
  ```

#### SpringMVC层

SpringMVC的功能就是操作web项目，在前面搞了那么多配置文件之后，我们发现实际上我们的项目还不是一个web项目，所以第一步我们就要添加web框架支持（右击项目->添加框架支持->web应用程序）

- 首先要先配置`web.xml`

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
           version="5.0">
  
      <!--DispatchServlet-->
      <servlet>
          <servlet-name>springmvc</servlet-name>
          <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
          <init-param>
              <param-name>contextConfigLocation</param-name>
              <!--注意注意，此处引用的是总的配置文件而并不是spring-mvc.xml，因为我们是在Service层配置文件中注册的bean，到时候Controller调用的是Service层的bean-->
              <param-value>classpath:ApplicationContext.xml</param-value>
          </init-param>
          <load-on-startup>1</load-on-startup>
      </servlet>
      <servlet-mapping>
          <servlet-name>springmvc</servlet-name>
          <url-pattern>/</url-pattern>
      </servlet-mapping>
  
      <filter-mapping>
          <filter-name>encoding</filter-name>
          <url-pattern>/*</url-pattern>
      </filter-mapping>
      <filter>
          <filter-name>encoding</filter-name>
          <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
          <init-param>
              <param-name>encoding</param-name>
              <param-value>utf-8</param-value>
          </init-param>
      </filter>
  
      <session-config>
          <session-timeout>15</session-timeout>
      </session-config>
  
  </web-app>
  ```

- 下一步是配置创建并配置`spring-mvc.xml`，同样要记得把它添加到上下文

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop" xmlns:mvc="http://www.springframework.org/schema/mvc"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/aop 
          https://www.springframework.org/schema/aop/spring-aop.xsd http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd">
  
      <!--注解驱动-->
      <mvc:annotation-driven/>
      <!--静态资源过滤-->
      <mvc:default-servlet-handler/>
      <!--扫描包-->
      <context:component-scan base-package="com.test.controller"/>
      <!--视图解析器-->
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
          <property name="prefix" value="/WEB-INF/jsp/"/>
          <property name="suffix" value=".jsp"/>
      </bean>
  
  </beans>
  ```

最后，为了稳妥起见，在总的`ApplicationContext.xml`中导入需要使用所有的xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop 
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <import resource="spring-dao.xml"/>
    <import resource="spring-service.xml"/>
    <import resource="spring-mvc.xml"/>
    
</beans>
```

至此，所有的配置工作就完成啦！可以看出来总的来说还是比较繁琐的。。。

下面是项目完成以后的总项目结构图

![image-20211004162620447](https://s2.loli.net/2021/12/06/sSeTEtUcWu52i1F.png)

如果感觉摸不着头脑，不如看看下面这个图，详细说明了各个配置文件及功能体系连接

![查看源图像](https://pic4.zhimg.com/v2-55b2dac916e70e9bb9a4452868220983_r.jpg)

#### 测试方法

接下来我们要做的就是连接Controller层和jsp目录，同时通过Controller层调用Service层实现内容跳转展示

在这之前不如让我们先写一个最简单的小程序来测试一下我们上面的一大堆配置到底有没有问题

```java
@Controller
@RequestMapping("/book")
public class BookController {
    // Controller层调用Service层
    @Autowired
    private BookService bookService;

    // 查询全部数据并返回到页面
    @GetMapping("/all")
    public String list(Model model){
        List<Books> books = bookService.queBooks();
        model.addAttribute("list",books);
        return "all";
    }
}
```

相对应我们要建立一个jsp文件，并且在`index.jsp`中实现跳转

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
    <h3>
      <a href="${pageContext.request.contextPath}/book/all">所有书籍</a>
    </h3>
  </body>
</html>
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>所有书</title>
</head>
<body>
    进入成功
</body>
</html>
```

如果出现问题，我们可以进行Junit单元测试，例如

```java
public class TestM {
    @Test
    public void test(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        BookService bookServiceImpl = context.getBean("BookServiceImpl", BookService.class);
        for (Books queBook : bookServiceImpl.queBooks()) {
            System.out.println(queBook);
        }

    }
}
```

以此来检查dao层及service层有没有问题

最终成功结果如下，点击所有书籍之后跳转成功

![image-20211004172010887](https://s2.loli.net/2021/12/06/dLPO8Qarvuym4EA.png)

#### CRUD操作

前面我们已经测试到让查询页面跳转成功，我们现在来完善它

我们已经将书籍列表传给了这个页面，如今我们只需要将其取出并展示即可

此处我们使用BootStrap样式来展示页面，可以百度一个cdn导入

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>所有书</title>
    <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <%--BootStrap栅格系统--%>
    <div class="container">
        <div class="row clearfix">
            <div class="col-md-12 column">
                <div class="page-header">
                    <h1>
                        <small>书籍列表--显示书籍</small>
                    </h1>
                </div>
            </div>
        </div>
        <div class="row clearfix">
            <div class="col-md-12 column">
                <table class="table table-hover table-striped">
                    <thead>
                    <tr>
                        <th>书籍编号</th>
                        <th>书籍名称</th>
                        <th>书籍数量</th>
                        <th>书记详情</th>
                    </tr>
                    </thead>
                    <tbody>
                    <c:forEach var="book" items="${list}">
                        <tr>
                            <td>${book.bookID}</td>
                            <td>${book.bookName}</td>
                            <td>${book.bookCounts}</td>
                            <td>${book.detail}</td>
                        </tr>
                    </c:forEach>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

</body>
</html>
```

查询效果，确实好看不少了

![image-20211004174455640](https://s2.loli.net/2021/12/06/AcurFRCE1nhtL8I.png)

接下来的操作即都是照猫画虎，十分简单，我们简单的贴上源码

- Controller层，为所有资源统一定向和提供Servlet

  ```java
  @Controller
  @RequestMapping("/book")
  public class BookController {
      // Controller层调用Service层
      @Autowired
      private BookService bookService;
  
      // 查询全部数据并返回到页面
      @GetMapping("/all")
      public String list(Model model){
          List<Books> books = bookService.queBooks();
          model.addAttribute("list",books);
          return "all";
      }
  
      @GetMapping("/pageShow/add")
      public String addShow(){
          return "add";
      }
      @GetMapping("/pageShow/update/{id}")
      public String updateShow(@PathVariable int id, Model model){
          Books books = bookService.queBookByID(id);
          model.addAttribute("RBook",books);
          System.out.println(model.getAttribute("RBook"));
          return "update";
      }
  
      @PostMapping("/add")
      public String add(Books books){
          System.out.println("BookController.add");
          bookService.addBook(books);
          return "redirect:/book/all";
      }
      @PostMapping("/update")
      public String update(Books books){
          bookService.updBook(books);
          return "redirect:/book/all";
      }
      @GetMapping("/delete/{id}")
      public String delete(@PathVariable int id){
          bookService.delBookByID(id);
          return "redirect:/book/all";
      }
  }
  ```

- View层接收Servlet传输数据内容并展示

  - `all.jsp`

    ```jsp
    <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>所有书</title>
        <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
        <%--BootStrap栅格系统--%>
        <div class="container">
            <div class="row clearfix">
                <div class="col-md-12 column">
                    <div class="page-header">
                        <h1>
                            <small>书籍列表--显示书籍</small>
                        </h1>
                    </div>
                </div>
    
                <div class="row">
                    <div class="col-md-4 column">
                        <a type="button" class="btn btn-default" href="${pageContext.request.contextPath}/book/pageShow/add">新增书籍</a>
                    </div>
                </div>
    
            </div>
            <div class="row clearfix">
                <div class="col-md-12 column">
                    <table class="table table-hover table-striped">
                        <thead>
                        <tr>
                            <th>书籍编号</th>
                            <th>书籍名称</th>
                            <th>书籍数量</th>
                            <th>书籍详情</th>
                        </tr>
                        </thead>
                        <tbody>
                        <c:forEach var="book" items="${list}">
                            <tr>
                                <td>${book.bookID}</td>
                                <td>${book.bookName}</td>
                                <td>${book.bookCounts}</td>
                                <td>${book.detail}</td>
                                <th>
                                    <a href="${pageContext.request.contextPath}/book/pageShow/update/${book.bookID}">修改</a>
                                    &nbsp; | &nbsp;
                                    <a href="${pageContext.request.contextPath}/book/delete/${book.bookID}">删除</a>
                                </th>
                            </tr>
                        </c:forEach>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    
    </body>
    </html>
    ```

  - `add.jsp`

    ```jsp
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
        <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
    <div class="container">
        <div class="row clearfix">
            <div class="col-md-12 column">
                <div class="page-header">
                    <h1>
                        <small>书籍列表--新增书籍</small>
                    </h1>
                </div>
            </div>
        </div>
    
        <form action="${pageContext.request.contextPath}/book/add" method="post">
            <div class="form-group">
                <label>
                    <p>书名</p>
                    <input type="text" class="form-control" name="bookName" required>
                </label>
                <label>
                    <p>数量</p>
                    <input type="text" class="form-control" name="bookCounts" required>
                </label>
                <label>
                    <p>备注</p>
                    <input type="text" class="form-control" name="detail" required>
                </label>
            </div>
            <button type="submit" class="btn btn-default">Submit</button>
        </form>
    </div>
    
    </body>
    </html>
    ```

  - `update.jsp`

    ```jsp
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
        <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
    <div class="container">
        <div class="row clearfix">
            <div class="col-md-12 column">
                <div class="page-header">
                    <h1>
                        <small>书籍列表--修改书籍</small>
                    </h1>
                </div>
            </div>
        </div>
    
        <form action="${pageContext.request.contextPath}/book/update" method="post">
            <div class="form-group">
                <input type="hidden" name="bookID" value="${RBook.bookID}">
                <label>
                    <p>书名</p>
                    <input type="text" class="form-control" name="bookName" value="${RBook.bookName}" required>
                </label>
                <label>
                    <p>数量</p>
                    <input type="text" class="form-control" name="bookCounts" value="${RBook.bookCounts}" required>
                </label>
                <label>
                    <p>备注</p>
                    <input type="text" class="form-control" name="detail" value="${RBook.detail}" required>
                </label>
            </div>
            <button type="submit" class="btn btn-default">Submit</button>
        </form>
    </div>
    
    </body>
    </html>
    ```

会发现比起配置，内容的实现要简单的多，在拥有了框架搭建后的基础上，功能的实现显得是那么简单

接下来贴上耗费了我一个下午时间总结的这个项目中整个SSM框架的[运行流程图](http://assets.processon.com/chart_image/614c05b7f346fb69b168b1ca.png)（看不清就点这个链接）

<img src="https://s2.loli.net/2021/12/06/rJfAEv2wsIzhmeR.png" alt="未命名文件 (1)"  />

## SpringBoot

SpringBoot框架的目的就是简化Spring的开发，是一个Spring的顶级项目，在目前以微服务为潮流的当下，SpringBoot能够大大降低开发成本，增加开发速度，成为了大多数人的首选

> 其中**微服务**就是将一个系统按业务划分成多个子系统，每个子系统都是完整的，可独立运行的，子系统间的交互可通过HTTP协议进行通信（也可以采用消息队列来通信，如RoocketMQ，Kafaka等）。

Spring最大的缺点就是配置繁琐，包括了Spring里的xml里面的配置和Maven项目中的pom文件配置，既要保证导入依赖的版本相同，又要保证创建的bean的正确性，一来二去，形成了代码轻量但配置重量的一种头重脚轻的感觉

SpringBoot解决了Spring的缺点，它在运行时**自动配置**了各种原本需要一个个在`ApplicationContext.xml`中所需要需要配置的内容，同时采用了**起步依赖**的思想，它打包了更多的具有相同功能的不同包，使得我们不需要再依靠Maven来管理我们的jar包，更进一步的是，SpringBoot还提供了许多**辅助功能**，如嵌入式服务器，安全配置等，我们再也不用再配置Tomcat环境了

因此SpringBoot提供了一种快速开发Spring项目的方式，而不是对Spring功能上的增强

### 简单的项目

1. 首先我们还是要先创建一个Maven项目，并在pom.xml中导入依赖

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>com.example</groupId>
       <artifactId>myproject</artifactId>
       <version>0.0.1-SNAPSHOT</version>
   
       <!--springboot工程需要继承的父工程-->
       <parent>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-parent</artifactId>
           <version>2.5.5</version>
       </parent>
   
       <dependencies>
           <!--web开发的起步依赖-->
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-web</artifactId>
           </dependency>
       </dependencies>
   
       <build>
           <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

   注意到导入的方式与之前有所不同，继承了SpringBoot的父工程之后，我们仅仅需要导入一个依赖即可

2. 定义Controller类

   ```java
   @RestController
   public class Hello {
       @RequestMapping("/")
       public String hello(){
           return "hello Spring";
       }
   }
   ```

3. 编写引导类（注意在必须在根目录下创建引导类）

   ```java
   @SpringBootApplication
   public class HelloApplication {
       public static void main(String[] args) {
           SpringApplication.run(HelloApplication.class,args);
       }
   }
   ```

4. 启动测试

   直接按下main方法旁边的启动按钮即可直接启动项目，接着控制台会弹出一段启动成功的提示

   ![image-20211010154907059](https://s2.loli.net/2021/12/06/gUiRn9Fsjeqh1ML.png)

   看到这里，我们会发现SpringBoot内置的Tomcat服务器已经启动，当我们打开浏览器访问8080端口时，就可以访问到我们自定义的界面了

   ![image-20211010155115311](https://s2.loli.net/2021/12/06/yk1dRcseIiBFz7X.png)

最终项目结构如下

![image-20211010155154318](https://s2.loli.net/2021/12/06/b67crGFLO1NzKtS.png)

> 注意引导类位置，绝对不能放在任何别的目录下（涉及到Spring扫包机制）

可以说是已经简单到批爆了，而这就是SpringBoot项目的最简化方式！真的爽！

经过代码的编写，现在我们总结一下，可以发现几个特点

1. SpringBoot不再使用以前的war打包方式，由于通过main方法启动项目，因此创建项目时使用jar打包
2. SpringBoot引导类时项目的入口，运行main方法就可以启动项目
3. 使用SpringBoot和Spring构建的项目业务代码编写方式完全一样

这时候就有人要问了，万一还是觉得这种方法麻烦那怎么办呢？事实上，IDEA提供了一整套的SpringBoot项目构建方案，一步到位，谁用谁知道

![image-20211010160103550](https://s2.loli.net/2021/12/06/xNjbCvcgu4iGwnL.png)

接着直接用鼠标点击想要导入的依赖即可，经典的面向鼠标编程！

![image-20211010160525254](https://s2.loli.net/2021/12/06/jJKE2V8XSdNWhDn.png)

再看看生成出来的项目结构，哇塞，该创建的不该创建的都给我们创建出来了，可谓是懒人一步到位

![image-20211010160648854](https://s2.loli.net/2021/12/06/pzLAsdJ5yrRfH7c.png)

请记住这个项目结构，接下来的学习中会不断的用到其中的内容！

### 运行原理

我们肯定会好奇，到底是什么操作可以让我们只需要简单的开始一个main方法就能够执行程序，接下来让我们从依赖和主程序方面来初步认识SpringBoot

#### 起步依赖

起步依赖，即在最简单的pom文件中引入的一个父工程和一个依赖，这些依赖的功能需要我们一个个分析

- `spring-boot-starter-parent`父工程

  我们点进这个父工程，发现它又继承了`spring-boot-dependencies`父工程，我们再往里面点，发现了密密麻麻一大堆的配置信息，通过标签锁定，我们看到了整体上来看分为两大类

  - `<properties>`标签下定义的一大堆版本号
  - `<dependencies>`标签下定义的一大堆依赖位置及引用前文版本号
  - `<dependencyManagement>`通过这个标签锁定所有版本号，使得子项目配置时**不需要再引入版本号**

  ![image-20211010162518589](https://s2.loli.net/2021/12/06/IwB8DkYaECfVspU.png)

  可以看到我们之后引入的依赖也可以在里面找到，但是我们在引入时并没有指定版本信息

  综上我们可以得出结论，`spring-boot-starter-parent`父工程为我们贴心的配置了它认为我们会用到的各种依赖的版本信息，同时这些版本都是经过精挑细选使得任意两两之间都能够完美适配，免去了我们在创建Spring项目时不知道导入什么版本的依赖的问题

- `spring-boot-starter-web`依赖

  点进这个依赖，抛开头部信息不谈，我们看到了许多熟悉的身影

  ```xml
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
      <version>2.5.5</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-json</artifactId>
      <version>2.5.5</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.5.5</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.3.10</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.10</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>
  ```

  可以说都是老熟人了，其中就非常简洁的集合了我们web开发需要用到的几个框架，同时注意在SpringBoot中凡是带有`starter`的包都代表着一个开发场景，里面包含了所需启动该功能的所有依赖

  现在我们只需要依赖这个包，就可以间接的依赖上其中依赖的所有内容，注意

#### 自动配置

在探究自动配置之前，我们需要了解到其实引导类中`SpringApplication.run`这个方法是会返回当前IoC容器的（就是Spring中学习过的通过配置文件创建出来的[应用程序上下文](#应用程序上下文)），其中包含了当前项目中自动或我们手动注册的所有组件（即bean）

```java
public static void main(String[] args) {
    ConfigurableApplicationContext run = SpringApplication.run(Demo01Application.class, args);
    String[] beanDefinitionNames = run.getBeanDefinitionNames();
    for (String beanDefinitionName : beanDefinitionNames) {
        System.out.println(beanDefinitionName);
    }
}
```

可以在打印出来的组件中搜索定义下来的beanid

![image-20211012150348730](https://s2.loli.net/2021/12/06/jIUE4zZevCOVSFP.png)

如图可以轻松搜索到我们之前尝试运行时注册的bean

> 注意到其中还有很多名称为全类名的bean，这些bean实际上是通过@import注解导入的

通过打印下来这个容器，我们可以在里面找到很多熟悉的面孔，例如`DispatcherServlet`（SpringMVC核心前端控制器）、`CharacterEncodingFilter`（乱码过滤器）等等，正是SprignBoot自动帮助我们配置好了这些web开发的场景，才使得我们能够正常、简便的使用其中的各种功能

包括自动配置中还为我们配置了默认的自动扫描包机制，会自动扫描和引导类同级的所有包内容里面的组件

这些所有的配置功能，都在`spring-boot-autoconfigure`这个依赖中

![image-20211012152710735](https://s2.loli.net/2021/12/06/hG7oO6SFigQ2WXb.png)

其实就是相同名称的这个包

![image-20211012153040715](https://s2.loli.net/2021/12/06/ivat59fp8h7Mnyw.png)

除了web场景，里面配置了所有的SpringBoot支持的场景自动配置信息，只不过我们只导入了web应用场景，别的内容将不会生效（体现了自动配置的按需加载）

#### @SpringBootApplication

只需要为引导类添加上这个标签，即可以通过执行main方法来启动SpringBoot，显而易见，整个SpringBoot最核心的部分就是这个注解了，而理解了这个注解，等于理解了SpringBoot的运行模式

点进去，发现它是一个合成注解，内含了一些我们认识或者不认识的注解

- `@SpringBootConfiguration`即SpringBoot的配置，里面包含了`@Configuration`，表明它修饰的这个引导类从根本来说也是一个Spring组件（Bean）

- `@EnableAutoConfiguration`使该组件能够自动配置，也是其中最重要的一个注解

  - 内含了一个`@AutoConfigurationPackage`自动配置包注解，这个注解里面又导入了一个注册选择器（`Registrar.class`），选择器代表一个类，这个类里面有一个核心方法

    ```java
    public void registerBeanDefinitions(AnnotationMetadata metadata, BeanDefinitionRegistry registry) {
        AutoConfigurationPackages.register(registry, (String[])(new AutoConfigurationPackages.PackageImports(metadata)).getPackageNames().toArray(new String[0]));
    )
    ```

    方法通过传入的`metadata`参数获取到自动配置包注解注解到的类（即我们的引导类）的详细信息，并通过调用`(new AutoConfigurationPackages.PackageImports(metadata)).getPackageNames().toArray(new String[0])`获取到引导类所属包名，并把这个包底下的所有组件注册到容器中来

  - 同时也导入了一个配置自动导入选择器（`AutoConfigurationImportSelector.class`）这个类里面也有一个核心方法

    ```java
    public String[] selectImports(AnnotationMetadata annotationMetadata) {
        if (!this.isEnabled(annotationMetadata)) {
            return NO_IMPORTS;
        } else {
            AutoConfigurationImportSelector.AutoConfigurationEntry autoConfigurationEntry = this.getAutoConfigurationEntry(annotationMetadata);
            return StringUtils.toStringArray(autoConfigurationEntry.getConfigurations());
        }
    }
    ```

    这个方法的返回值同样也就是我们需要导入的包名构成的字符串数组，而这个数组怎么来的，我们就要去看`getAutoConfigurationEntry`这个方法

    ```java
    protected AutoConfigurationImportSelector.AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata) {
        if (!this.isEnabled(annotationMetadata)) {
            return EMPTY_ENTRY;
        } else {
            AnnotationAttributes attributes = this.getAttributes(annotationMetadata);
            List<String> configurations = this.getCandidateConfigurations(annotationMetadata, attributes);
            configurations = this.removeDuplicates(configurations);
            Set<String> exclusions = this.getExclusions(annotationMetadata, attributes);
            this.checkExcludedClasses(configurations, exclusions);
            configurations.removeAll(exclusions);
            configurations = this.getConfigurationClassFilter().filter(configurations);
            this.fireAutoConfigurationImportEvents(configurations, exclusions);
            return new AutoConfigurationImportSelector.AutoConfigurationEntry(configurations, exclusions);
        }
    }
    ```

    - 可以看出这个方法通过两个方法获得了`configurations`和`exclusions`两个字符串集合，并对其做了一些元素筛选操作，然后返回，我们想知道这两个集合里面到底有什么，就需要进入这个方法里面看看

    ```java
    protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
        List<String> configurations = SpringFactoriesLoader.loadFactoryNames(this.getSpringFactoriesLoaderFactoryClass(), this.getBeanClassLoader());
        Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you are using a custom packaging, make sure that file is correct.");
        return configurations;
    }
    ```

    - 进到`getCandidateConfigurations`这个方法，发现没什么东西，我们得再进一层

    - 这时候已经不在上述对象内了，跳到了`SpringFactoriesLoader`这个对象中

      ```java
      public static List<String> loadFactoryNames(Class<?> factoryType, @Nullable ClassLoader classLoader) {
          ClassLoader classLoaderToUse = classLoader;
          if (classLoader == null) {
              classLoaderToUse = SpringFactoriesLoader.class.getClassLoader();
          }
      
          String factoryTypeName = factoryType.getName();
          return (List)loadSpringFactories(classLoaderToUse).getOrDefault(factoryTypeName, Collections.emptyList());
      }
      ```

      这个方法也没什么东西，只是给返回的调用的方法准备了所需要的参数

      ```java
      private static Map<String, List<String>> loadSpringFactories(ClassLoader classLoader) {
          Map<String, List<String>> result = (Map)cache.get(classLoader);
          if (result != null) {
              return result;
          } else {
              HashMap result = new HashMap();
      
              try {
                  Enumeration urls = classLoader.getResources("META-INF/spring.factories");
      
                  while(urls.hasMoreElements()) {
                      URL url = (URL)urls.nextElement();
                      UrlResource resource = new UrlResource(url);
                      Properties properties = PropertiesLoaderUtils.loadProperties(resource);
                      Iterator var6 = properties.entrySet().iterator();
      
                      while(var6.hasNext()) {
                          Entry<?, ?> entry = (Entry)var6.next();
                          String factoryTypeName = ((String)entry.getKey()).trim();
                          String[] factoryImplementationNames = StringUtils.commaDelimitedListToStringArray((String)entry.getValue());
                          String[] var10 = factoryImplementationNames;
                          int var11 = factoryImplementationNames.length;
      
                          for(int var12 = 0; var12 < var11; ++var12) {
                              String factoryImplementationName = var10[var12];
                              ((List)result.computeIfAbsent(factoryTypeName, (key) -> {
                                  return new ArrayList();
                              })).add(factoryImplementationName.trim());
                          }
                      }
                  }
      
                  result.replaceAll((factoryType, implementations) -> {
                      return (List)implementations.stream().distinct().collect(Collectors.collectingAndThen(Collectors.toList(), Collections::unmodifiableList));
                  });
                  cache.put(classLoader, result);
                  return result;
              } catch (IOException var14) {
                  throw new IllegalArgumentException("Unable to load factories from location [META-INF/spring.factories]", var14);
              }
          }
      }
      ```

      进到这个方法，我们总算找到了头，让我们细细品味一下，首先它似乎从`"META-INF/spring.factories"`这个工厂里面拿到了什么东西，这个文件在哪呢？实际上哪里都有，他会自动的扫描当前系统中所有这个位置中的文件，比如核心包`spring-boot-autoconfigure-2.5.5.jar`里面就有

      ![image-20211013001125706](https://s2.loli.net/2021/12/06/eGFwOM7ZgtykYsN.png)

      这里面稍微瞄一眼，密密麻麻全是包名，代表了SpringBoot全环境需要的所有包内容，而这个工厂也就获得了这个里面所有包的名称然后将其返回（默认全部加载）

  - 会发现分析到最后，居然是加载了所有的包，但是真的加载了所有的包吗，回到`getAutoConfigurationEntry`这个方法，我们发现之后对`configurations`这个变量做了过滤操作，即`this.getConfigurationClassFilter().filter(configurations);`而这个过滤操作滤除了大多数用不到的配置包，这也就是SpringBoot最重要的按需加载功能

  - 什么是按需加载，SpringBoot怎么识别我们是否需要一个配置包，我们不妨在`spring-boot-autoconfigure`里随便点进一个包里面

    ![image-20211013164856537](https://s2.loli.net/2021/12/06/zksFLZrhX23NBwO.png)

    会发现几乎每一个包里面的类都会由一个`@Conditionxxxx`注解修饰，而这个注解的含义就是能够判断其括号内的条件是否满足，当不满足条件的时候就不会加载它修饰的类内容，因此我们在pom文件中不导入的配置内容当执行到此的时候也判断不到我们需要这个类，也就不加载了

    > 我们可以通过在配置文件中添加`debug: true`来在启动时查看日志信息，里面会有生效类和未生效类的列举

到此为止，我们初步的了解了当我们启动main方法的时候发生的一系列事情，也让我们认识到了SpringBoot最重要的两大特性，即自动按需配置和起步依赖的大致工作原理，为之后的学习提供方便

### 配置

SpringBoot虽然尽可能的少配置，但是并不代表着不配置，接下来就要重点讲解一下其中配置文件配置问题

首先由于SpringBoot约定大于配置的要求，很多配置都有默认值，如果我们想用自己的配置替换默认配置的话，就可以使用核心文件`application.properties`或者`application.yml/yaml`进行配置

> 是不是似曾相识？其实就是在自动生成SpringBoot项目时自动创建的配置文件

而归根结底，配置文件的用处就是将一系列数据和一个个Bean绑定在一起

比如我们想要定义Tomcat的启动端口为8081，那么我们可以采用下面两种方式

- `application.properties`

  ```properties
  server.port=8081
  ```

- `application.yml/yaml`

  ```yaml
  server:
    port: 8081
  ```

> 会发现启动测试的时候会出现Spring的一个图标，事实上我们也可以自定义启动时出现的图像，只需要直接在和配置文件的同级的目录下创建`banner.txt`的文件并写入我们自定义内容即可

同时注意`properties>yml>yaml`，其中`properties`会最后加载，在配置了相同属性时，他的优先级最高

`.properties`资源类我们的都很熟悉，采用键值对的形式来配置内容，所以我们重点介绍`.yaml`配置文件形式

#### YAML

YAML 是 "YAML Ain't a Markup Language"（YAML 不是一种标记语言）的递归缩写（还挺好玩？），准确来说它是一种直观的能够被电脑识别的数据序列化格式，并且容易被人类阅读，容易和脚本语言交互，比xml更简洁

YAML比起一般资源文件多了不同配置之间的层级关系，又比起xml文件更加易于编写，因此受到大众欢迎

注意点

- 大小写敏感
- 数据值前边必须有空格（但不限于一个），作为分隔符
- 使用缩进表示层级关系
- 缩进的每一个空格就代表一个层级，相同层级之间元素左侧对齐即可
- 使用`#`进行注释

基本语法

- 对象（Map）

  ```yaml
  person:
  	name: 1  # 层级写法
  person: {name: 1}  # 行内写法
  ```

- 数组

  ```yaml
  address:
  	- 1
  	- 2  # 层级写法
  address: [1,2]  # 行内写法
  ```

- 纯量（常量）

  ```yaml
  msg1: '1/n2'  # 单引号忽略转义字符
  msg2: "1/n2"  # 双引号识别转义字符
  ```

- 参数引用

  ```yaml
  name: 1
  person:
  	name: ${name}  # 引用上面的name值
  ```

#### 读取配置内容

当我们在`application.yaml`配置文件中配置内容之后，我们可以在控制类中通过三种方式取到配置值

假设有这样一个配置文件

```yaml
name: 123

person:
  name: 123
  age: 123
```

在控制类及实体类中，我们可以这样拿到值

```java
@RestController
public class Demo1 {
    @Value("${name}")  // Field注入，不推荐通过这种方式注入
    private String s;

    private final Environment env;  // 将所有的自定义内容注入到一个对象

    private final Person person;

    // @Autowired 当类中仅有一个构造器方法时（无参构造也不行），可以省略Autowired，因此可以搭配Lombok使用
    // Spring4.x中，推荐使用构造器注入方式
    public Demo1(Environment env, Person person) {
        this.env = env;
        this.person = person;
    }

    @RequestMapping("/")
    public String test(){
        System.out.println(s);
        System.out.println(env.getProperty("name"));
        System.out.println(person);
        return "test";
    }
}
```

其中实体类Person内属性名必须保证与配置文件内一致

```java
@Data
@Component
@ConfigurationProperties(prefix = "person")  // 这里指定在配置文件中类名前缀
public class Person {
    private String name;
    private int age;
}
```

> 注意到在添加`@ConfigurationProperties`注解时，系统会提示我们需要配置一下配置文件进程支持
>
> 此时我们在pom文件中添加依赖
>
> ```xml
> <dependency>
> <groupId>org.springframework.boot</groupId>
> <artifactId>spring-boot-configuration-processor</artifactId>
> <optional>true</optional>
> </dependency>
> ```
>
> 之后重新运行一遍SpringBoot进程，会发现当我们在配置文件中输入时会自动提示前缀名对应的属性
>
> ![image-20211010201049781](https://s2.loli.net/2021/12/06/XNq62oUkRS1Gyne.png)
>
> 不过当然我们不导入这个依赖其实也是可以的，只是不会智能提示罢了

除了正常的玩法，yaml配置文件甚至可以做一些正常配置文件想都不敢想的事情

```yaml
name: 123  # 正常赋值
# test: name
person:
  age: ${random.int(10)} # 获得十以内随机数
  name: ${test:null}  # 获取配置文件中test的值，如果没有test这个值就赋值null
```

可以发现比起`.properties`配置文件，`.yaml`更加灵活和方便

除了在`classpath`下直接建立配置文件之外，SpringBoot还支持在其他位置创建配置文件`application.yml`

![image-20211016154812496](https://s2.loli.net/2021/12/06/wYfercdbDHT7m65.png)

之后SpringBoot会根据优先级顺序读取配置内容，优先级高的文件配置会覆盖优先级低的

#### 多环境配置

在SpringBoot中，我们可以根据不同环境配置不同的配置文件，从而方便的切换各种环境

首先我们先创建多个配置文件，注意一定要以`appliacation`开头，不然不会生效

![image-20211016155750250](https://s2.loli.net/2021/12/06/8mrubWnXgHq1D3I.png)

如图，此时我们只需要在主配置文件中配置如下内容即可

```yaml
spring:
  profiles:
    active: dev  # 这里就填短横杠后面内容
```

这样就可以实现多环境配置，同时注意主配置的内容还是会生效的

但是这样可能还是很麻烦，事实上yaml提供了更加强大的多文档模块内容，我们只需要在模块之间加上`---`即可

```yaml
spring:
  profiles:
    active: dev  # 这里就填短横杠后面内容

---
server:
  port: 8082

spring:
  config:
    activate:
      on-profile: test
---
server:
  port: 8083  # 相当于之前的多文件
  
spring:
  config:
    activate:
      on-profile: dev
```

但是这样耦合性高，在配置多的时候还是建议多文件清晰明了

#### AutoConfiguration和Properties文件

。。。

### 添加静态资源

在之前的学习中，我们好像发现SpringBoot好像没有WEB-INF之类的目录，那我们的web开发应该如何进行呢

在SSM框架中，与静态资源交互的是SpringMVC，顺着这个思路，我们去寻找一下在SpringBoot中集成的SpringMVC内容

![image-20211016193743726](https://s2.loli.net/2021/12/06/edLvunzV6KBQSJM.png)

不出所料，我们找到了自动配置静态资源的类，接着我们慢慢看他的方法，发现了一个`addResourceHandlers`方法

```java
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {
        logger.debug("Default resource handling disabled");
    } else {
        this.addResourceHandler(registry, "/webjars/**", "classpath:/META-INF/resources/webjars/");
        this.addResourceHandler(registry, this.mvcProperties.getStaticPathPattern(), (registration) -> {
            registration.addResourceLocations(this.resourceProperties.getStaticLocations());
            if (this.servletContext != null) {
                ServletContextResource resource = new ServletContextResource(this.servletContext, "/");
                registration.addResourceLocations(new Resource[]{resource});
            }

        });
    }
}
```

可以看到里面有一个if语句，判断我们是否在配置文件中指定了文件位置，如果没有指定，就加载他默认的文件位置里的内容

那么它默认的文件位置在哪里呢，这时候我们看到else语句，里面调用了`addResourceHandler`方法两次，明显是从不同的两个地方去读取一些资源文件，第一个地方很明显是某个叫做`/META-INF/resources/webjars/`的目录，我们先不管他，第二条if语句的第三个参数是一个Lambda表达式，里面有一个`getStaticLocations`方法，同时一看调用方法的类，我们一下子懂了，肯定是某一个默认自动配置好的资源内容

为了证明，我们点进去看看，很明显这是一个Getter方法，获得了资源类私有的`staticLocations`属性，翻翻翻，我们看到了这个Resource类里面的构造方法

```java
public static class Resources {
    private static final String[] CLASSPATH_RESOURCE_LOCATIONS = new String[]{"classpath:/META-INF/resources/", "classpath:/resources/", "classpath:/static/", "classpath:/public/"};
    private String[] staticLocations;
    private boolean addMappings;
    private boolean customized;
    private final WebProperties.Resources.Chain chain;
    private final WebProperties.Resources.Cache cache;

    public Resources() {
        this.staticLocations = CLASSPATH_RESOURCE_LOCATIONS;
        this.addMappings = true;
        this.customized = false;
        this.chain = new WebProperties.Resources.Chain();
        this.cache = new WebProperties.Resources.Cache();
    }
```

这下我们知道了，在自动装配阶段，SpringMVC会自动扫描如此代码中`CLASSPATH_RESOURCE_LOCATIONS`内 的内容，也就是说，今后我们的静态资源只需要放在这四个目录下，都可以在项目启动时被扫描到

![image-20211016200852426](https://s2.loli.net/2021/12/06/wXlpvQVDnjU2Guk.png)

同时我们还可以在里面找到一个`welcomePageHandlerMapping`方法

```java
@Bean
public WelcomePageHandlerMapping welcomePageHandlerMapping(ApplicationContext applicationContext, FormattingConversionService mvcConversionService, ResourceUrlProvider mvcResourceUrlProvider) {
    WelcomePageHandlerMapping welcomePageHandlerMapping = new WelcomePageHandlerMapping(new TemplateAvailabilityProviders(applicationContext), applicationContext, this.getWelcomePage(), this.mvcProperties.getStaticPathPattern());
    welcomePageHandlerMapping.setInterceptors(this.getInterceptors(mvcConversionService, mvcResourceUrlProvider));
    welcomePageHandlerMapping.setCorsConfigurations(this.getCorsConfigurations());
    return welcomePageHandlerMapping;
}
```

看第一个方法调用的参数，调用了一个`getStaticPathPattern`方法，我们点点点，发现其中的`staticPathPattern`属性其实就是代表着`/**`，意味着我们只需要访问`/`程序就会自动把我们跳转到欢迎页面

从哪里调用呢，我们再找找找，发现下面有一个`getIndexHtml`方法

```java
private Resource getIndexHtml(Resource location) {
    try {
        Resource resource = location.createRelative("index.html");
        if (resource.exists() && resource.getURL() != null) {
            return resource;
        }
    } catch (Exception var3) {
    }

    return null;
}
```

`Resource`这个类我们很熟啊，不就是存放静态资源的类吗，因此我们只需要在存放静态资源的地方创建一个`index.html`文件，在应用启动的时候就会自动为我们展示欢迎界面

### thymeleaf模板引擎

模板引擎（这里特指用于Web开发的模板引擎）是为了使用户界面与业务数据（内容）分离而产生的，它可以生成特定格式的文档，用于网站的模板引擎就会生成一个标准的html文档，不懂的可以看下图

![image-20211016210337659](https://s2.loli.net/2021/12/06/oPHYFCdW8xT3Azh.png)

可以发现我们把数据和模板丢进模板引擎，他就能造出我们需要的前端文件用于展示，还是挺方便的

#### 准备工作

使用模板引擎第一步还是要导入依赖，当然我们创建项目的话直接点一下就可以了

![image-20211016210702755](https://s2.loli.net/2021/12/06/i9pXanqvKjEc7Ph.png)

当然由于不需要指定版本号，我们完全可以直接在pom文件中手动加上依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

此时我们再启动SpringBoot会发现报了一个WARN问题

```log
2021-10-16 21:12:14.219  WARN 17100 --- [           main] ion$DefaultTemplateResolverConfiguration : Cannot find template location: classpath:/templates/ (please add some templates or check your Thymeleaf configuration)
```

为什么会报这个错误呢，这时候就需要我们去找源码了

![image-20211016212102341](https://s2.loli.net/2021/12/06/STMkaWmiXb8OdBl.png)

又是自动配置的包下面，我们发现了熟悉的身影，我们知道，想要了解他的默认自动配置内容，就得去`Propeties`类里面找

```java
@ConfigurationProperties(
    prefix = "spring.thymeleaf"
)
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING;
    public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
    private boolean checkTemplate = true;
    private boolean checkTemplateLocation = true;
    private String prefix = "classpath:/templates/";
    private String suffix = ".html";
    private String mode = "HTML";
    private Charset encoding;
    private boolean cache;
    private Integer templateResolverOrder;
    private String[] viewNames;
    private String[] excludedViewNames;
    private boolean enableSpringElCompiler;
    private boolean renderHiddenMarkersBeforeCheckboxes;
    private boolean enabled;
    private final ThymeleafProperties.Servlet servlet;
    private final ThymeleafProperties.Reactive reactive;

    public ThymeleafProperties() {
        this.encoding = DEFAULT_ENCODING;
        this.cache = true;
        this.renderHiddenMarkersBeforeCheckboxes = false;
        this.enabled = true;
        this.servlet = new ThymeleafProperties.Servlet();
        this.reactive = new ThymeleafProperties.Reactive();
    }
```

这可不就来了吗，我们脑补一下就知道在自动配置类里面规定了当我们Controller层调用时，他会去`templates`目录下找到后缀为`.html`的内容，这不就是一个盗版的视图解析器嘛，还是比较好理解的

> SpringBoot的Template目录和我们之前的WEB-INF目录差不多，用户是不能从外部直接访问的，必须在我们内部通过转发得到

当然thymeleaf还是比视图解析器要强大多了，接下来我们看看他到底怎么用

#### 简单语法

```java
@Controller
public class Demo1 {
    @RequestMapping("/")
    public String test(Model model){
        model.addAttribute("msg","<h1>test</h1>");
        model.addAttribute("list", Arrays.asList(1,2));
        return "test";
    }
}
```

Controller和SpringMVC一点都没有区别，由于thymeleaf是请求转发到`.html`页面，因此我们要在Template里面新建一个`test.html`

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div th:text="${msg}"></div>
    <div th:utext="${msg}"></div> <!--不转译-->
    <div th:each="var:${list}" th:text="${var}"></div>
    <div th:each="var:${list}">[[${var}]]</div>  <!--行内格式，不推荐-->
</body>
</html>
```

如上代码，想要使用thymeleaf，只需要在头部引用到他的命名空间约束，之后在几乎任何标签属性前加上`th:`即可，然后后面就可以像jsp一样快乐的使用表达式了，下面是显示效果

![image-20211017170406575](https://s2.loli.net/2021/12/06/mfg7oxUl5JZSLKj.png)

实际上thymeleaf就是用一堆标签来代替了jsp的一系列功能，使得我们能在html页面中动态的制定一些内容

接下来的学习中我们会在应用中慢慢的接触其他的语法

### 整合数据库

对于数据访问层，无论是否是关系性数据库，SpringBoot底层都是采用SpringData的方式进行统一管理

其中SpringData也是一个和SpringBoot齐名的知名项目

首先先创建一个项目

![image-20211017194910834](https://s2.loli.net/2021/12/06/m9jYAoF1ElutXPR.png)

之后直接在`application.yml`里面编写数据库连接信息即可

```yml
spring:
  datasource:
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=uft-8
```

然后在测试类里面添加数据源，通过自动装配，就可以自动将数据库的信息注入到该数据源中

```java
@SpringBootTest
class Demo03ApplicationTests {

    @Autowired
    DataSource dataSource;

    @Test
    void contextLoads() {
        System.out.println(dataSource.getClass());
    }

}
```

最后输出结果可以看出SpringBoot默认的数据源是Hikari，之前也介绍过

之后我们就可以通过SpringBoot自动注入好的JDBCTemplate来执行SQL语句进行查找数据内容

```java
@Data
@AllArgsConstructor
@RestController
public class JDBCController {
    private final JdbcTemplate jdbcTemplate;  // 注意这里只有一个有参构造，会自动装配属性

    @GetMapping("/")
    public List<Map<String,Object>> userList(){  // 万能的Map传值，可以不需要实体类了
        String sql = "select * from mybatis.user";
        return jdbcTemplate.queryForList(sql);
    }
}

```

> 注意再次之前要导入web包

### 整合Druid

Druid可以说是功能最强大的数据池了，利用它我们在获取数据的同时还可以非常方便的对数据请求进行监控

首先还是要导入Druid依赖，同样选择`starter`导入，这样在项目启动时会自动配置bean，省去我们的一些配置操作

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.2.5</version>
</dependency>
```

现在在别的内容不变的情况下，其实我们项目已经在使用druid数据源了，当然我们还需要了解它的强大功能

```yml
spring:
  datasource:
    # 这里不用配在druid下也可以正常使用Druid作为数据源
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8
    druid:
      # 由于使用了starter，这里的配置内容会默认在项目启动时自动配置
      # druid 数据源专有配置
      # 初始化大小，最小，最大
      initialSize: 5
      minIdle: 5
      maxActive: 200
      # 配置获取连接等待超时的时间
      maxWait: 60000
      # 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒
      timeBetweenEvictionRunsMillis: 60000
      # 配置一个连接在池中最小生存的时间，单位是毫秒
      minEvictableIdleTimeMillis: 300000
      # 用来检测连接是否有效的sql，要求是一个查询语句
      validationQuery: SELECT 1 FROM DUAL
      # 建议配置为true，不影响性能，并且保证安全性。申请连接的时候检测，如果空闲时间大于timeBetweenEvictionRunsMillis，执行validationQuery检测连接是否有效。
      testWhileIdle: true
      # 申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能
      testOnBorrow: false
      # 归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。
      testOnReturn: false
      # 是否缓存preparedStatement，也就是PSCache。PSCache对支持游标的数据库性能提升巨大，比如说oracle。在mysql下建议关闭。
      poolPreparedStatements: true
      # 要启用PSCache，必须配置大于0，当大于0时，poolPreparedStatements自动触发修改为true。
      max-pool-prepared-statement-per-connection-size: 50

      #配置监控统计拦截的filters，stat:监控统计、log4j：日志记录、wall：防御sql注入
      #如果允许时报错  java.lang.ClassNotFoundException: org.apache.log4j.Priority
      #则导入 log4j 依赖即可，Maven 地址：https://mvnrepository.com/artifact/log4j/log4j
      filters: stat,wall
      # 合并多个DruidDataSource的监控数据
      useGlobalDataSourceStat: true
      # 通过connectProperties属性来打开mergeSql功能；慢SQL记录
      connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500
```

当然上面的这些配置内容其实是个数据源都能做到，现在扩展一些Druid特有内容，比如开启自带的后台监控功能

由于使用了`starter`，我们直接在配置文件后加上开启统计视图的Servlet功能，并配置一些信息即可

```yml
stat-view-servlet:
  enabled: true
  login-username: admin
  login-password: 123456
  allow: 127.0.0.1
  url-pattern: /druid/*
```

这么简单代码感觉都不用解释，完全就是字面意思罢了

同样的通过配置文件中还可以配很多其他的东西，比如说过滤器功能

```yml
web-stat-filter:
  enabled: true
  url-pattern: /*
  # 这些请求不计入统计
  exclusions: /druid/*,*.js,*.gif
```

开启项目，测试，在地址栏输入`http://localhost:8080/druid`，就会自动跳转到Druid配置好的后台中

![image-20211019133905185](https://s2.loli.net/2021/12/06/AsXgD3bx7R8aGlu.png)

使用我们之前配置好的账户（admin）和密码（123456），登陆以后就可以看到内部强大的监控功能

![image-20211019134104245](https://s2.loli.net/2021/12/06/zPnbBj34ec17GCp.png)

还是非常强大的

### 整合Mybatis

跟着SpringBoot的思路，我们需要使用Mybatis，肯定要导入什么什么`-starter`的包才行

![image-20211019140821645](https://s2.loli.net/2021/12/06/FTbdMjwGgStkL5r.png)

直接选中即可

作为一个新项目，首先我们还是要先连接数据库

```yml
spring:
  datasource:
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8
```

接着创建一个实体类用于存储从数据库接收过来的信息

```java
@Data
public class User {
    private int id;
    private String name;
    private String pwd;
}
```

作为一个Mybatis项目，mapper是必不可少的，所以接下来创建一个mapper接口

```java
@Mapper  // 表示这是一个mybatis的mapper类，里面包含了@Component类注解
public interface UserMapper {
    @Select("select * from mybatis.user")
    List<User> queryUser();
}
```

你可能很惊讶，但是事实上现在已经整合mybatis成功了，接下来我们测一下有没有地方写错

创建一个控制类

```java
@Data
@AllArgsConstructor
@RestController
public class UserController {
    private UserMapper userMapper;
    @GetMapping("/")
    public List<User> test(){
        return userMapper.queryUser();
    }
}
```

会发现只要我们想偷懒，甚至连一个`.xml`文件都不需要创建，直接就可以成功运行

而对于一些复杂sql语句，我们其实也是可以引入`xxxmapper.xml`文件的，只需要在`.yaml`配置文件里配一下即可

比如我们在resource目录下创建了`mapper/userMapper.xml`文件

```xml
<?xml version="1.0" encoding="GBK" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.test.mapper.UserMapper">
    <select id="queryUser" resultType="user">
        select *
        from mybatis.user;
    </select>
</mapper>
```

这时候我们只需要在`.yaml`中配置如下内容即可实现相同功能

```yaml
mybatis:
  mapper-locations: classpath:mapper/*.xml
  type-aliases-package: com.test.pojo
```

同样的，原本我们在`mybatis-config.xml`里写的内容其实都可以直接配置在`.yaml`中，或者通过

```yaml
mybatis:
  config-location:
```

的方式定位到某个配置文件

### 安全防护

之前我们学习了利用过滤器或者拦截器实现对不同特征的请求进行不同的操作分分流，实际上当前有非常多的框架自动为我们实现了这些麻烦的功能，我们只需要引入这些框架内容就可以轻松为自己的项目建立安全防护

这些框架共同的特点就是认证和授权功能，给每个用户分配不同的权限

其中最著名的就是**Shiro**和**SpringSecurity**

#### SpringSecurity

SpringSecurity也是Spring全家桶里面的一个项目，特点是和Spring的契合度极高，但是使用稍微复杂

- 首先还是要先创建一个新项目，导入这些依赖

  ![image-20211020134447315](https://s2.loli.net/2021/12/06/FilkSHeOr1GLpCd.png)

- 环境准备，在开始测试之前，我们需要进行现实环境的简单模拟

  ![image-20211020134053792](https://s2.loli.net/2021/12/06/riTmvkwdfIFM4AW.png)

- 接下来的第一步就是创建控制类，利用thymeleaf模板引擎，使得我们能够访问到`.html`文件

  ```java
  @Controller
  public class Router {
      @RequestMapping("/lv/{a1}")
      public String lv(@PathVariable("a1")int a1){
          return "views/lv"+a1 +"/1";
      }
  }
  ```

  > 这时候我们可以选择在pom文件中将SpringSecurity相关依赖给注掉然后测试一下基础环境的搭建情况，当然如果没有注掉Security的依赖的话，无论我们访问什么内容都会给跳转到Security自带的登录页面，看上去我们似乎没有办法通过控制类访问`.html`资源
  >
  > <img src="https://s2.loli.net/2021/12/06/mWRs3lndX2qLFyJ.png" alt="image-20211020135124296" style="zoom:50%;" />

- 上面发生的情况实际上是由于SpringSecurity的默认配置自动的拦截了所有请求，使得没有人拥有权限能够访问到我们设置好的内容，这意味着想要自定义不同用户的不同权限，我们只需要重写它提供的默认方法即可，

  因此我们创建一个控制类，继承SpringSecurity提供的`WebSecurityConfigurerAdapter`方法

  ```java
  // AOP
  @EnableWebSecurity
  // 链式编程，只需要一直.就完了
  public class SecurityConfig extends WebSecurityConfigurerAdapter {
  
      // 定制授权功能
      @Override
      protected void configure(HttpSecurity http) throws Exception {
          // 首页所有人可以访问，功能页只有有权限的人可以访问
          http.authorizeRequests()
                  .antMatchers("/").permitAll()
                  .antMatchers("/lv/1/**").hasRole("lv1")
                  .antMatchers("/lv/2/**").hasRole("lv2");
          // 没有权限默认会跳转到登录页（/login)，需要开启登录页面
          http.formLogin();
          // 可以通过.loginPage("/tologin").loginProcessingUrl("/login");定制登录页，一旦指定了它提供的页面就没用了
          // 其中第一个/tologin指的是Controller里面对应的请求转发页面，后一个/login指的是登录页html页面中表单的转发请求
          // 注销，开启注销页面（/logout）
          http.logout().logoutSuccessUrl("/");  // 注销成功跳到首页
          // 开启记住我功能，保存在cookie中，关闭浏览器依旧可以保存登陆状态
          http.rememberMe();  // 默认保存两周
      }
  
      // 定制认证功能
      @Override
      protected void configure(AuthenticationManagerBuilder auth) throws Exception {
          // 实际开发中一般从数据库中获取认证，这里先用从内存获取认证来演示
          auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                  .withUser("admin1").password(new BCryptPasswordEncoder().encode("123456")).roles("lv1").and()
                  .withUser("admin2").password(new BCryptPasswordEncoder().encode("123456")).roles("lv2");
          // 注意密码必须要编码格式，不然不仅会报错而且很容易被别人破译，不安全
      }
  }
  ```

- 接着我们就可以通过我们设定的认证方式访问到不同的页面了，同时这个认证的内容是保存在session中的，意味着在一次会话中我们都可以用这一身份进行浏览内容

可以看出这个SpringSecurity的核心方法都是一种新奇的链式编程的方式，同时采用了AOP的思想，相当于一个智能化的过滤器，对客户端发起的各种请求都进行拦截和判断，只用符合设定的条件的内容才给予放行

#### Shiro

Shiro是Apache的一个强大且易于使用的Java安全框架，可以执行认证、授权、密码学和会话管理。利用Shiro简单易懂的API，你可以快速、轻松地保护任何应用程序--从最小的移动应用程序到最大的网络和企业应用程序。

这意味着不仅是JavaEE项目，甚至是JavaSE项目也可以使用Shiro作为安全验证

想要在SpringBoot中集成Shiro，由于不是Spring官方的框架，没办法一键导入，我们只能在创建好的项目中添加Shiro启动器依赖

首先我们要了解到Shiro的核心是三层核心组件，分别是Subject, SecurityManager 和 Realms.

- Subject：即“当前操作用户”。但是，在Shiro中，Subject这一概念并不仅仅指人，也可以是第三方进程、后台帐户（Daemon Account）或其他类似事物。它仅仅意味着“当前跟软件交互的东西”。Subject代表了当前用户的安全操作，SecurityManager则管理所有用户的安全操作。
- SecurityManager：它是Shiro框架的核心，Shiro通过SecurityManager来管理内部组件实例，并通过它来提供安全管理的各种服务。
- Realm： Realm充当了Shiro与应用安全数据间的“桥梁”或者“连接器”。也就是说，当对用户执行认证（登录）和授权（访问控制）验证时，Shiro会从应用配置的Realm中查找用户及其权限信息。

多说无益，还是之前同样的项目，相同的味道，让我们再次尝试对不同的用户进行拦截

这次我们采用从数据库中取出用户名和密码，所以还需要[整合Mybatis](#整合Mybatis)

- Mapper

  ```java
  @Mapper
  public interface UserMapper {
      @Select("select * from mybatis.user where name=#{name}")
      public User queryUserByName(String name);
  }
  ```

- 接下来创建我们自己的Realm类，实现对不同用户的认证和授权

  ```java
  @Configuration
  @Scope("prototype")  // 不知道是否是要加多例的注解。。。因为正常代码中这个类时使用时临时new出来的
  @RequiredArgsConstructor
  public class UserRealm extends AuthorizingRealm {
  
      // 通过连接数据库查找账号密码信息
      final UserMapper userMapper;
  
      @Override
      // 当我们的login界面一点提交，就会被这个方法劫持内容，它默认就规定了第一项是用户名第二项是密码
      // 用户名可以通过getPrincipal获得，但是传入的密码我们也获取不到，所以必须通过返回值来交给shiro判断
      protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
          System.out.println("认证");
          User user = userMapper.queryUserByName((String) token.getPrincipal());  // 获取用户登录名
          if (user==null) {
              return null;
          }
          // 这样就可以在完全不知道密码的情况下完成登录，但是还是可以加密（MD5盐值加密）
          // 这个方法实际上就是将认证到的详细内容（也就是登录页面被封装好的token）包装好传给认证信息类，其中第二个参数会与传进来的pwd比对，不一致会抛出异常
          return new SimpleAuthenticationInfo(user.getName(),user.getPwd(),getName());
      }
  
      @Override
      // 当我们想要访问某个在配置文件中经perm修饰的路径时（此项目为/lv/2），会被此方法拦截并获取到该用户的信息（该信息应由认证方法返回传入）
      // PrincipalCollection即为信息的载体，它安全的接收了Object中的有关用户信息的内容（即上个方法中返回的第一个参数）
      protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
          System.out.println("授权");
          SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();
          // 给指定用户添加2权限
          // getPrimaryPrincipal获取到的实际上就是认证信息类里面第一个参数的内容
          if (principalCollection.getPrimaryPrincipal().equals("用户1")) {
              info.addStringPermission("2");  // 一般来说数据库中会有一个权限表，用来判断哪个用户有哪个权限
          }
          return info;
      }
  
  }
  ```

- 然后我们创建Shiro的配置组件，集成有关权限控制的所有信息

  ```java
  @Configuration
  @RequiredArgsConstructor
  public class ShiroConfig {
  
      // 从IoC池中获取我们配置的realm对象
      private final UserRealm realm;
  
      @Bean
      public ShiroFilterFactoryBean getShiroFilterFactoryBean(){
          // 将realm传入defaultWebSecurityManager
          DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
          securityManager.setRealm(realm);
          // ShiroFilterFactoryBean，整合SecurityManager，同时包含了对于权限的控制信息（即过滤条件）
          ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
          bean.setSecurityManager(securityManager);
          // 为指定页面设定权限
          Map<String,String> map = new LinkedHashMap<>();
          map.put("/lv/1","authc");  // authc：需要认证才可访问
          map.put("/lv/2","perms[2]");  // perms：必须是认证了并拥有2这个权限的用户才能访问
          bean.setFilterChainDefinitionMap(map);
          // 自定义登录页面，不过Shiro没有内置的登录页面，所以我们必须指定页面
          bean.setLoginUrl("/toLogin");
          return bean;
      }
  }
  
  ```

之后启动项目，我们就可以实现和之前几乎相同的效果了

### Swagger

Swagger是比较流行的API框架，也就是一个RestFulAPI文档在线自动生成工具，可以保证API文档与API定义同步更新，同时支持多种语言（Java，PHP等）

#### 简单环境

我们需要在项目中使用Swagger，千篇一律的要从导入jar包开始

Swagger在3.0之后变得更加简单，现在我们只需要导入这个依赖

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>
```

然后启动项目，访问`http://localhost:8080/swagger-ui/`，接着最简单的Swagger页面就展示出来了

![image-20211025000652190](https://s2.loli.net/2021/12/06/5pmkY67Z39bWiAB.png)

这也就是SpringBoot的好处，其实，所有的事情都是在AutoConfig文件里做的，就像其他starter做的事情一样。从源码中，我们发现swagger和ui组件默认都是开启的

当然只有这么一个简单的页面显然是不够的，所以我们需要对其进行配置

#### API内容配置

我们访问的上面这个页面究竟会显示什么东西实际上是由一个叫做`Docket`的对象bean控制的，如果我们需要自定义显示内容，只需要自己创建一个Docket的bean即可

创建一个bean，在SpringBoot中，仅有`@Configuration`加`@Bean`的模式了

```java
@Configuration
public class SwaggerConf{
    @Bean
    // 配置了Swagger的bean实例（即这里的Docket），我们所有的对Swagger的配置都可以往这个Docket里面丢
    public Docket createRestApi() {
        // OAS_30代表我们使用的是Swagger3.0+版本，如果用2.0+就是SWAGGER_2
        // 同样是链式编程，想要配置什么值直接一直.就可以了
        return new Docket(DocumentationType.OAS_30)
            	.pathMapping("/")  // 给
                .enable(true)  // 是否启动swagger，可以通过外部开发环境传值
                .apiInfo(new ApiInfo("Swagger标题",  // 配置在API页面上显示信息的内容（没啥用）
                        "Swagger描述",
                        "版本号",
                        "服务网站",
                        new Contact("作者信息","作者网站url","作者邮箱email"),
                        "证书",
                        "许可证网站",
                        new ArrayList<>()))
                // 选择哪些接口作为swagger的doc发布（从select开始到build结束）
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.test.controller"))  // 配置要扫描接口的方式
                // any()表示扫描全部，none()表示都不扫描，basePackage()指定包扫描，还有两个是扫描特定的注解
                .paths(PathSelectors.any())  // 过滤什么路径
                .build()  // 工厂模式
                .groupName("group1");  // 给每一个Docket分组，需要另一个组就在这里再加一个即可
    }
}
```

这么一通操作，最后我们显示的页面是这样的

![image-20211026152546778](https://s2.loli.net/2021/12/06/h3OVcluCv4U7ipZ.png)

会发现这个route（即controller类名）里面已经将我们的`/test`路径内容识别进来了，如果之前在参数中的`.RequestHandlerSelectors`配的是any，则还会出现`model`和`error`的内容（虽然里面没东西）

#### 输出注解&调试

比如我们存在一个用户的实体类，此时我们如果在实体类中加一些注释

```java
@Data
@ApiModel("用户")
public class User {
    @ApiModelProperty("用户名")
    private String username;
    @ApiModelProperty("密码")
    private String password;
}
```

然后我们重新创建一个控制路径，同样也添加一些注释，而且尝试返回到User值

```java
@PostMapping("/user/{username}/{password}")
@ApiOperation("user请求")
public User user(@ApiParam("输入用户名")@PathVariable("username")String username,
                 @ApiParam("输入密码")@PathVariable("password") String password){
    User user = new User();
    user.setUsername(username);
    user.setPassword(password);
    return user;
}
```

此时我们再次启动项目，打开route内部的内容，就可以发现自己写的注释显示在特定的位置中

![image-20211026162620991](https://s2.loli.net/2021/12/06/eyLbE8ofMrgJ63K.png)

从这就能看出，swagger可以对每一个人编写的接口（控制类）进行调试，同时输出调试信息，在团队开发中及最后调试中用处非常大

### 任务管理

#### 异步任务

当我们的某个服务操作需要耗费一定时间时，为了不让用户等待太久，我们可以选择先提前响应内容，将耗时任务放到另一个线程中慢慢执行，从而提升用户体验

比如有这么一个服务类和控制类

```java
@Service
public class DelayService {
    public void delay(){
        System.out.println("数据正在处理...");
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```java
@Controller
public class AsyncController {

    @Autowired
    DelayService delayService;

    @ResponseBody
    @GetMapping("/")
    public String test(){
        delayService.delay();
        return "OK";
    }
}
```

正常情况下，由于控制类需要等待三秒才能给出响应，因此在执行return之前浏览器就会转三秒的圈圈，用户看着圈圈只能干跺脚，因此我们可以在服务类的耗时方法上加上`@Async`标签，并在main方法内开启异步功能

```java
@Service
public class DelayService {
    @Async
    public void delay(){
        System.out.println("数据正在处理...");
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```java
@EnableAsync
@SpringBootApplication
public class Demo08Application {

    public static void main(String[] args) {
        SpringApplication.run(Demo08Application.class, args);
    }

}
```

即可直接秒加载

#### 邮件任务

想要发邮件也很简单，我们直接先导一个包

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

之后进行邮箱的配置，告诉它我们要用什么邮箱进行发送

当然在此之前我们得先获取到我们邮箱的账号密码信息，其中的密码并不是我们登陆密码，一般的邮箱页面会给我们一个专用密码供我们使用（比如qq就可以通过设置里打开smtp服务获取专用密码）

以下是配置文件

```yaml
spring:
  mail:
    username: qys.chillyblaze@gmail.com
    password: # 这里要填的是通过设置的专用密码，一般邮箱会进行两步验证之类
    host: smtp.gmail.com
    properties:
      mail.smtp.ssl.enable: true
```

之后我们就可以直接发送邮件了，比如我们可以在测试类中试一下

```java
@SpringBootTest
class Demo08ApplicationTests {

    @Autowired
    JavaMailSenderImpl mailSender;

    @Test
    void contextLoads() {
        final SimpleMailMessage message = new SimpleMailMessage();
        message.setSubject("主题测试");
        message.setText("文本测试");
        message.setTo("qys.chillyblaze@gmail.com");  // smtp发送
        message.setFrom("qys.chillyblaze@gmail.com");  // pop接收
        mailSender.send(message);
    }

}
```

SpringBoot好就好在提供了一系列的配置工具，我们不费吹灰之力就可以直接实现邮件发送

当然还有复杂邮件发送，此处不提

#### 定时任务

比如有时候会设定几点钟更新，几点钟日志输出，这些都需要利用定时任务功能

SpringBoot的Spring框架为我们提供了函数式接口来进行定时任务操作，我们不需要导包就可以直接使用

它和异步任务很类似，我们也是要在启动类上开启服务并且在方法上注解即可

```java
@SpringBootApplication
@EnableScheduling
public class Demo08Application {

    public static void main(String[] args) {
        SpringApplication.run(Demo08Application.class, args);
    }

}
```

```java
@Service
public class ScheduledService {
    // 秒 分 时 日 月 周几，*表示任意，?表示不确定
    // 异步执行，不需要管他，同时注意这里代表的是每分钟的第二秒执行，而不是每两秒执行一次
    @Scheduled(cron = "2 * * * * *")
    public void hello(){
        // 希望在特定的时候执行
        System.out.println("ScheduledService.hello");
    }
}
```

可以发现这里使用了cron表达式，如果不会写的话网上也有生成器可以使用

![image-20211026181101571](https://s2.loli.net/2021/12/06/GKNgRDL5xU1oZFu.png)

可以看出语法还是比较强大的，只需要这样简单的配置，当我们启动项目的时候就能够定时执行了

## MybatisPlus

MyBatis-Plus是一个MyBatis的增强工具，在 MyBatis 的基础上只做增强不做改变，为简化开发、提高效率而生。

### 初始化工作

1. 先创建一个用户表为了接下来使用，并插入一些数据

   ```sql
   CREATE DATABASE `mybatis_plus`;
   USE `mybatis_plus`；
   CREATE TABLE `user`(
   	`id` BIGINT(20) NOT NULL COMMENT '主键id',-- 由于mybatisplus默认给定的id值生成的比较大，因此需要使用bigint
   	`name` VARCHAR(30) DEFAULT NULL COMMENT '姓名',
   	`age` int(11) DEFAULT NULL COMMENT '年龄',
   	`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
   	PRIMARY KEY (`id`)
   ) ENGINE=INNODB DEFAULT CHARSET=utf8;
   
   INSERT INTO `user` (id,name,age,email) VALUES
   (1,'Jone',18,'test1@test.com'),
   (2,'Jack',20,'test2@test.com'),
   (3,'Tom',20,'test3@test.com'),
   (4,'Sandy',21,'test4@test.com'),
   (5,'Billy',24,'test5@test.com');
   ```

2. 创建springboot工程添加依赖

   ```xml
       <dependencies>
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter</artifactId>
           </dependency>
   
           <dependency>
               <groupId>org.projectlombok</groupId>
               <artifactId>lombok</artifactId>
               <optional>true</optional>
           </dependency>
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-test</artifactId>
               <scope>test</scope>
           </dependency>
   <!--        mysql驱动-->
           <dependency>
               <groupId>mysql</groupId>
               <artifactId>mysql-connector-java</artifactId>
               <version>8.0.28</version>
           </dependency>
   <!--        mybatis-plus启动器依赖-->
           <dependency>
               <groupId>com.baomidou</groupId>
               <artifactId>mybatis-plus-boot-starter</artifactId>
               <version>3.5.1</version>
           </dependency>
       </dependencies>
   ```

3. 编写配置文件添加数据源

   ```yaml
   spring:
     # 配置数据源信息
     datasource:
       type: com.zaxxer.hikari.HikariDataSource
       driver-class-name: com.mysql.cj.jdbc.Driver  # mysql驱动为8版本用这个，5版本不需要加cj
       url: jdbc:mysql://172.17.0.2:3306/mybatis_plus?characterEncoding=utf-8&useSSL=false&serverTimezone=GMT%2B8
       hikari:
         username: root
         password: 123456
   ```

4. 编写实体类

   ```java
   @Data
   public class User {
       private Long id;
       private String name;
       private Integer age;
       private String email;
   }
   ```

5. 创建Mapper接口继承MybatisPlus提供的父类，这个父类中编写了一大堆已经封装好的方法，只要继承之后就可以直接使用，因此我们自己的Mapper里面啥都不用写，指定一下泛型类型为我们的实体类即可

   ```java
   // 继承了这个接口那我们的Mapper里面也有它的方法了
   @Mapper
   public interface UserMapper extends BaseMapper<User> {
   }
   ```

6. 主程序扫描mapper目录

   ```java
   @SpringBootApplication
   // 扫描mapper接口的包
   @MapperScan("com/example/mybatisplustest/mapper")
   public class MybatisPlusTestApplication {
   
       public static void main(String[] args) {
           SpringApplication.run(MybatisPlusTestApplication.class, args);
       }
   
   }
   ```

7. 编写测试类测试结果

   ```java
   @SpringBootTest
   class MybatisPlusTestApplicationTests {
   
       @Autowired
       private UserMapper userMapper; 
   
       @Test
       void contextLoads() {
          userMapper.selectList(null).forEach(System.out::println);
       }
   
   }
   ```

8. ![image-20220408172825472](https://s2.loli.net/2022/04/08/A9qCgDFXabiKRp2.png)

> 如果我们想要查看mybatisplus给我们自动生成的SQL语句，我们只需要在配置文件中添加如下代码即可
>
> ```yaml
> mybatis-plus:
>   configuration:
>     log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
> ```

可以发现当包括实体类和内部属性和数据库中的内容严格对应的时候，基础的操作和正常集成SpringBoot并没有什么差别，目前来看，MybatisPlus只是为我们省去了在mapper中手写简单SQL语句的困扰，但是它的优势还远不于此

### BaseMapper

可以发现，我们的mapper只需要继承一下这个接口即可，而我们如果点进这个接口，就会发现里面内置了一大堆方法供我们使用

对其中主要的方法进行一个测试

```java
// 插入
@Test
void insertTest() {
    User user = new User();
    user.setName("Mike");
    user.setAge(22);
    user.setEmail("test6@test.com");
    int result = userMapper.insert(user);  // 返回值为布尔值，1为成功，0为失败
    System.out.println("result = " + result);
    System.out.println("user.getId() = " + user.getId());  // 可以发现mybatis在BaseMapper里面自动通过雪花算法给我们生成了一个id
    // result = 1
    // user.getId() = 1512367928111190017
}

// 删除
@Test
void deleteTest() {
    // 通过id删除，注意加L
    System.out.println(userMapper.deleteById(1512367928111190017L));
    // userMapper.deleteBatchIds()这个方法则是传入一个id的list删除
    // 通过map删除
    HashMap<String, Object> map = new HashMap<>();
    map.put("name", "Mike");
    map.put("age", 22);  // 且关系，必须两个都满足 DELETE FROM user WHERE name = ? AND age = ?
    System.out.println(userMapper.deleteByMap(map));
}

// 更改
@Test
void updateTest(){
    User user = new User();
    user.setId(1512371169733574658L);
    user.setName("Mike1");
    user.setEmail("Mike@test.com");
    System.out.println(userMapper.updateById(user));
}
```

可以发现大部分方法都已经演示出来了，剩下来的方法我们如果进到源代码中看，会发现其中的参数都为一个奇形怪状的东西，这也就是条件构造器，接下来的内容中会详细介绍

![image-20220408181446763](https://s2.loli.net/2022/04/08/cSv691PnKTBLH5Q.png)

### 自定义功能

同时我们会发现在配置文件的编写中，mybatisplus默认会读取我们类路径下的mapper目录下的`*.xml`配置文件作为自定义的mapper配置，这也体现了它只作增强不做改变的原则

![image-20220408221524095](https://s2.loli.net/2022/04/08/hPbsovzWYiUkMEx.png)

于是我们找到类路径，自己创建目录文件并编写mapper配置

![image-20220408221726296](https://s2.loli.net/2022/04/08/A1Zxw8gqVtNlvap.png)

- `UserMapper.xml`

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <mapper namespace="com.example.mybatisplustest.mapper.UserMapper">
      <!--Map<String,Object> selectMapById(Long id)-->
      <select id="selectMapById" resultType="map">
          select id,name,age,email from user where id=#{id}
      </select>
  </mapper>
  ```

- `UserMapper.java`

  ```java
  @Mapper
  public interface UserMapper extends BaseMapper<User> {
  
      Map<String,Object> selectMapById(Long id);
  
  }
  ```

- 测试类

  ```java
  @Test
  void selectTest(){
      Map<String, Object> map = userMapper.selectMapById(1L);
      System.out.println(map);
  }
  ```

功能也能够正常运行

### 通用Service接口

除了通用的Mapper接口，MybatisPlus还提供了丰富的Service接口，同时也为了避免混淆，功能差不多的接口名和Mapper中的接口名也特意做了区分，比如通用Mapper接口使用`select`而通用Service则使用`get`作为获得数据的前缀，可谓是十分的人性

```java
@SpringBootTest
public class ServiceTest {
    @Autowired
    private UserService userService;

    @Test
    void testGetCount() {
        // 通过内置的方法查询数据库表中的总记录数 SELECT COUNT( * ) FROM user
        long count = userService.count();
        System.out.println("count = " + count);
    }

    @Test
    void testInsertMore() {
        // 集合中的每一个对象都是一条记录
        ArrayList<User> users = new ArrayList<>();
        for (int i = 1; i < 10; i++) {
            User user = new User();
            user.setName("lyb"+i);
            user.setAge(20+i);
            user.setEmail("lyb"+i+"@test.com");
            users.add(user);
        }
        // INSERT INTO user ( id, name, age, email ) VALUES ( ?, ?, ?, ? )
        // 说明也是通过复数次单词添加进行批量添加
        userService.saveBatch(users);
    }
}
```

可以发现还是十分方便的

### 自定义表/列名

之前我们提到过，当我们没有指定表名的时候，MybatisPlus会自动去寻找和实体类名字一致的表进行查询，但是显示情况是我们的实体类名字可能并不和表名一致，因此我们可以使用`@TableName`指定真实表名或者全局添加配置项指定表的指定前缀

比如我现在将user表改为t_user，直接重新运行程序肯定会报错

此时我们可以在配置中

```yaml
mybatis-plus:
  global-config:
    db-config:
      table-prefix: t_
```

或者在实体类中

```java
@Data
@TableName("t_user")
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
}
```

与之同理的是表中的列名，当我们的主键不是id字段时，我们可以同理给字段添加`@TableId`注解

```java
@Data
public class User {
	@TableId
    private Long uid;
    private String name;
    private Integer age;
    private String email;
}
```

而遇到更复杂的情况，比如数据库中主键叫`uid`，但实体类我就想用`id`作为属性，同时在数据表中还好死不死的设置了自动递增，意味着我们不需要通过随机算法自己给每一条记录添加id，此时我们就可以设置`@TableId`的注解属性

```java
@Data
public class User {
    @TableId(value = "uid",type = IdType.AUTO)  // 自动递增
    private Long id;
    private String name;
    private Integer age;
    private String email;
}
```

对于`id`编写的策略，我们也可以通过在配置文件中和指定表名一样指定全局的`id`插入策略，用法和之前差不多

```yaml
mybatis-plus:
  global-config:
    db-config:
      id-type: auto
```

同时我们如果在添加记录的时候手动指定了id，那么怎么指定id的策略都没有用了

如果属性名和字段名不一致的话，还可以使用`@TableField`在实体类中指定真实字段名

> 同时注意到MybatisPlus默认将我们数据表中的下划线变成是实体类中的驼峰，还是比较方便的

### 逻辑删除

因为数据库操作`delete`指令是危险的，意味着一旦删除记录就永远无法恢复，因此我们面对某些未来可能需要恢复的记录中，需要一个进行假删除的操作，使得某条记录在之后的查询结果中不显示，但是在数据库中我们却可以看到这条记录的情况，也就是所谓的逻辑删除

在此之前，我们需要在数据表中添加某一个字段，比如叫做`is_deleted`，值设置为整型就行，接着我们在实体类中添加该属性，在之前加上`@TableLogic`注解即可

```java
@Data
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
    @TableLogic
    private Integer isLogic;
}
```

此时我们若我们在项目中的任何地方进行`delete`操作，事实上MybatisPlus只会将数据表中的逻辑值变为`1`而不是直接删除记录，等于是变相进行了一个修改的操作，以下是执行的SQL语句

```sql
UPDATE user SET is_delete=1 WHERE name = ? AND age = ? AND is_delete=0
```

### 条件构造器（Wrapper）

条件构造器就是为了能根据个性化条件进行查找指定记录，我们只需要封装一个`Wrapper`构造器，传入支持查询的方法即可

事实上我们目前看到的Wrapper类型只是一个顶层接口，我们需要根据自己使用的不同查询方法引用继承自这个接口的不同子类进行封装，再传入指定方法

#### QueryWrapper

```java
@SpringBootTest
public class WrapperTest {
    @Autowired
    private UserMapper mapper;

    @Test
    void test01(){
        // 查询用户名包含a，年龄在20-30之间，邮箱信息不为null的用户信息，以降序输出
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        wrapper.like("name","a")
                .between("age",20,30)  // 双闭区间
                .isNotNull("email")
                .orderByDesc("id");
        // SELECT id,name,age,email,is_delete FROM user WHERE is_delete=0 AND (name LIKE ? AND age BETWEEN ? AND ? AND email IS NOT NULL) ORDER BY id DESC
        List<User> users = mapper.selectList(wrapper);
        users.forEach(System.out::println);
    }

    @Test
    void test02(){
        // 查询用户名包含a，年龄大于20，或id小于3的用户进行修改
        // UPDATE user SET age=? WHERE is_delete=0 AND (name LIKE ? AND age > ? OR id < ?)
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        wrapper.like("name","a")
                .gt("age",20)
                .or()  // 默认都是用and连接，我们如果需要不同逻辑就需要自己定义
                .lt("id",3);
        User user = new User();
        user.setAge(30);  // 设置几条属性就改几条属性
        mapper.update(user,wrapper);
    }
}
```

通过给定的各种方法可以实现多种不同的个性化查询操作，对于更复杂的语句查询，这时候我们就可以借助Lambda表达式帮忙了，因为我们知道，Lambda表达式在程序中会优先执行，从而实现一个局部带括号的效果

```java
@Test
void test03(){
    // 查询用户名包含a的同时（年龄大于30，或id小于3）的用户
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    wrapper.like("name","a")
            .and(i->i.gt("age",20).or().lt("id",3));
    // 虽然看上去和前一条差不多，但是这条语句不再会查询到第一条记录了，因为name中包含a的优先级更高
    // SELECT id,name,age,email,is_delete FROM user WHERE is_delete=0 AND (name LIKE ? AND (age > ? OR id < ?))
    mapper.selectList(wrapper).forEach(System.out::println);  
}
```

![image-20220409104842735](https://s2.loli.net/2022/04/09/ZmF7waViQcyJbtH.png)

当然我们也不能过度使用这个条件构造器，实在比较麻烦的SQL语句建议还是创建mapper文件单独编写，不然Service层内容会显得十分臃肿

#### UpdateWrapper

当我们涉及到对数据内容进行修改的时候，我们可以进一步使用更加简便的UpdateWrapper，来避免人为手动再创建一次User对象的麻烦

```java
@Test
void test04() {
    UpdateWrapper<User> wrapper = new UpdateWrapper<>();
    wrapper.like("name","a")
            .set("age",22);
    mapper.update(null,wrapper);
}
```

#### LambdaQueryWrapper

Java8提供了方法引用的概念，也算是Lambda表达式的进一步增强，用法是通过`[类名]::[方法]`来引用方法

> `Math::max`等效于`(a, b)->Math.max(a, b)`
>
> `String::startWith`等效于`(s1, s2)->s1.startWith(s2)`
>
> `System.out::println`等效于`n->System.out.println(n)`
>
> 上面我们在`forEach`方法中就曾经引用过

而一旦我们在MybatisPlus中引用了`LambdaQueryWrapper`这个类来创建我们的Wrapper，意味着我们就不需要在方法内容中一个个敲字段名了，我们只用直接引用实体类方法即可

```java
@Test
void test05(){
    LambdaQueryWrapper<User> wrapper = new LambdaQueryWrapper<>();
    wrapper.select(User::getName,User::getId);
    // SELECT name FROM user WHERE is_delete=0
    mapper.selectMaps(wrapper).forEach(System.out::println);
}
```

可以有效的避免我们的字段写错

### 插件

MybatisPlus为我们提供了大量可以开箱即用的插件内容，仅需要我们简单的创建一个配置类，并自己组装需要用到的插件内容，之后将其丢给Spring作为bean即可

#### 分页

MybatisPlus本身为我们提供了分页插件，我们如果需要使用它，只需要创建一个配置类把一个分页插件Bean丢到Spring里面去就行

```java
package com.example.mybatisplustest.config;

@Configuration
public class MyBatisPlusConfig {
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor(DbType.MYSQL));
        return interceptor;
    }
}
```

接下来项目启动时IoC容器中就会多出来一个分页拦截器了，同时注意这个插件是以类似横切的方式进行对将要交给数据库的SQL语句进行添加分页指令的，因此我们不需要修改已经封装好的SQL语句，只需要在调用mapper的时候额外增添一个`Page<V>`参数即可

```java
@SpringBootTest
public class PluginTest {
    @Autowired
    private UserMapper userMapper;
    @Test
    void test01() {
        Page<User> page = new Page<>(1,3);  // 第一个参数是页码，不再是limit下的两个参数
        userMapper.selectPage(page,null);
        System.out.println("page = " + page);  // 输出Page对象，里面的方法可以查看当前页的属性
    }
}
```

对于我们自己创建的个性化分页方法，同样我们不需要在配置文件`mapper.xml`	里面写任何有关分页的内容，只需要在mapper接口中的参数里增加一个Page参数接收Page对象，其他的就交给拦截器做了

#### 乐观锁

当我们需要修改某一条数据库的记录时，常规的方式是先通过查询语句对数据库中某条记录进行查询，接着再调用update语句，对数据库中的数据进行更新，但是这会存在一个问题，当我们查询到了数据的同时，数据库被更新了，但我们并不知道，于是造成了并发的问题

此时我们需要一个属性对每一次的记录更新做出记录，而在我们需要更新记录的时候，首先先查询本次更改记录是不是最新的，如果在这期间记录被人修改，那么就拒绝本次的更新操作

为了实现这个想法，我们需要在数据库中添加一个version字段，接着我们学着分页插件的样子，同样给输出的拦截器添加乐观锁插件类，再在实体类中给version字段添加`@version`标签即可

```java
@Configuration
public class MyBatisPlusConfig {
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new OptimisticLockerInnerInterceptor());
        return interceptor;
    }
}
```

```java
@Data
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
    @TableLogic
    private Integer isDelete;
    @Version
    private Integer version;
}
```

```java
@Test
void test02() {
    // 第一个人查询数据
    User user1 = userMapper.selectById(1L);

    // 第二个人查询并修改数据
    User user2 = userMapper.selectById(1L);  // 注意必须通过查询+更新的方式才能迭代乐观锁，如果直接新new一个user类传进去更新并不会有效果
    user2.setAge(40);
    System.out.println(userMapper.updateById(user2));

    // 第一个人修改数据
    user1.setAge(user1.getAge()-10);  // 原意是让他的年龄在当前情况下-10，也就是40-10=30，但是此时我们拿到的数据user.age=30还未更新
    System.out.println(userMapper.updateById(user1));  // 由于设置了版本验证，因此更新操作被拒绝
}
```

#### MybatisX

他是一个IDEA的插件，但是也是MybatisPlus作者开发的，我们只需要在IDEA的插件商城里面下载一下，之后重启就行

1. mapper接口也映射文件自动匹配，重启项目之后，我们发现我们的mapper接口变成了一个小鸟，与之对应的mapper映射文件也变成了小鸟

   ![image-20220409160119702](https://s2.loli.net/2022/04/09/axGpI9Poiwbf53g.png)

   而在文件内，也提供了一个小鸟图标便于我们两个文件之间匹配跳转

   ![image-20220409160335457](https://s2.loli.net/2022/04/09/F3Rj7SaqoUwW8sZ.png)

2. 代码生成器，我们需要通过IDEA内置的数据库模块连接上我们的数据库

   ![image-20220409163036817](../../.config/Typora/typora-user-images/image-20220409163036817.png)

   ![image-20220409162601840](https://s2.loli.net/2022/04/09/JZMzLfERq75OtdF.png)

   ![image-20220409162630255](https://s2.loli.net/2022/04/09/HvGF4YlXc3Jjwot.png)配置下来一点Finish就自动生成从实体类到service了

   ![image-20220409163133714](https://s2.loli.net/2022/04/09/LtbEepRj3Uad7x6.png)

3. 快速创建CRUD，现在我们如果在mapper接口中想要自己创建一个个性化mapper，我们一打字，便会提示我们一大堆乱七八糟的东西，比如我们现在想要根据所得name和age进行查找用户，我们只需要这样写

   ![image-20220409164102433](../../.config/Typora/typora-user-images/image-20220409164102433.png)

   接着直接一个`Alt+Enter`选择生成代码即可，然后我们就会发现不仅是mapper接口，甚至映射文件都给你写好了，直接用就行，简直无敌，而且这玩意写的SQL语句比你写的都要好，我就是个废物

## SpringCloud

SpringCloud并不是一个框架，而是一个集成了各种乱七八糟组件的解决方案，提供了一套微服务架构所需的功能

### 内置API调用

1. 在启动类内创建Bean返回`new RestTemplate()`
2. 在Service层注入`RestTemplate`对象
3. 调用其`getForObject(url,class)`方法发请求并获得返回对象

问题：

- 无法负载均衡
- 开闭问题

### Eureka

统一注册分发微服务，心跳监控服务状态

1. `pom.xml`引入Eureka服务依赖

2. 所有需要注册到Eureka的服务都需要`application.yml`编写配置内容`eureka.client.service-url.defaultZone=http://[ip]:[port]/eureka`配置地址信息（别忘了`server.port`和`spring.application.name`）

   > Eureka会把自己也注册到自己上，所以他自己也要配这个

3. Eureka服务端微服务的启动类上添加`@EnableEurekaServer`注解

4. 在启动类的`RestTemplate`上添加`@LoadBalanced`负载均衡

5. Eureka会根据微服务的`spring.application.name`作为服务名归类每个微服务，因此`getForObject(url,class)`的`url`的`ip`直接写服务名

### Ribbon

Eureka内部调用了Ribbon，同样是一个SpringCloud组件，`@LoadBalanced`就是Ribbon的注解，是我们发请求会先给Ribbon，Ribbon去请求Eureka然后返回结果根据负载均衡策略选一个请求后返回给服务

重写负载均衡策略只需要在启动类内添加Bean重写IRule，返回某一个策略（比如`RandomRule()`），或者在配置文件内添加`[服务名].ribbon.NFLoadBalancerRuleClassName`配置项可以指定服务名的请求负载均衡策略

Ribbon默认懒加载，服务启动的时候不会去拉取请求服务信息，直到第一次请求的时候Ribbon才去获取服务列表记录在缓存中，可以通过`ribbon.eager-load.enabled=true`使服务启动的时候就加载（饥饿加载），通过`ribbon.eager-load.clients=[服务名]`指定饥饿加载的服务名

### Nacos

#### Nacos部署

1. 去仓库[下载](https://github.com/alibaba/nacos)
2. 解压后去`conf/application.properties`调端口
3. `startup.sh -m standalone`单机启动
4. 访问Nacos控制台，登录账号密码默认都是nacos

#### 注册到Nacos

1. `pom.xml`引入`com.alibaba.cloud`和`nacos`依赖
2. 配置文件配`spring.cloud.nacos.server-addr=[ip]:[port]`
3. `spring.cloud.nacos.discovery.cluster-name=[集群名称]`配置集群信息
4. 负载均衡还是Ribbon所以之前Eureka的内容可以不用动，也可以配一下`[服务名].ribbon.NFLoadBalancerRuleClassName=com.alibaba.cloud.nacos.ribbon.NacosRule`使用Nacos负载均衡策略，他会优先使用和自己集群名称一致的服务请求，然后根据控制台配置的权重分配请求（默认都是1）
5. 还可以配命名空间`spring.cloud.nacos.discovery.namespace=[ip]`，不同命名空间的服务不可见

Nacos会把服务的更改信息主动推送给注册的服务，我们也可以设置`spring.cloud.nacos.discovery.ephemeral=false`把服务转成非临时实例，然后Nacos就会主动检测其健康状态而不靠服务给Nacos发心跳，就算服务停了也不会从Nacos里面剔除

#### 统一管理配置

1. 在Nacos控制台`配置列表->+->Data ID->[服务名]-[环境].[后缀]->配置内容`编写配置
2. 项目内建立`bootstrap.yml`配置Nacos地址，服务名，服务环境，Nacos配置后缀`spring.cloud.nacos.config.file-extension`然后删去`application.yml`中相同的配置
3. 重启项目可通过`@Value`注解拿到配置信息，还可以在类上添加`@RefreshScope`实现热更新（在Nacos控制台的修改即时反应），或者新建一个配置类`@ConfigurationProperties`自动装配配置项，默认自动热更新

#### Nacos集群

1. `conf/cluster.conf.example`后的`.example`删去，在其中添加集群中每一个`[ip].port`

2. `application.properties`配置数据库信息`spring.datasource.platform`和`db.*`

3. 复制三份直接`startup.sh`

4. 配置Nginx，访问Nacos自动负载均衡

   ```conf
   upstream nacos {
   	server [ip]:[port];
   	server [ip]:[port];
   	server [ip]:[port];
   }
   server {
   	listen	80;
   	server_name	localhost;
   	location /nacos {
   		proxy_pass	http://nacos;
   	}
   }
   ```

### Feign

1. `pom.xml`添加Feign依赖
2. 启动类上加`@EnableFeignClients`注解
3. 新建类并添加`@FeignClients("[服务名]")`注解
4. 在方法上添加`@RequestMapping`注解用法和Controller一样
5. 在Service注入`@FeignClient`标注类，调用请求方法即可

Feign默认不支持连接池，可以添加`Httpclient`依赖，然后添加`feign.httpclient.enabled=true`设置开启，包括连接池配置（最大连接数等）

### Gateway

1. 添加gateway依赖
2. 配置网关端口和名称，并注册到配置中心（Nacos，Eureka）
3. 配置`spring.cloud.gateway.routes.id/uri/predicates/filters`四个，其中`uri`可以把`http`改成`lb`表示负载均衡，`predicates`是匹配[断言工厂](https://cloud.spring.io/spring-cloud-gateway/reference/html/#gateway-request-predicates-factories)数组，包括匹配路径`Path=/xx/**`等，`filters`是[过滤器](https://cloud.spring.io/spring-cloud-gateway/reference/html/#gatewayfilter-factories)，可以对请求做处理鉴权等
4. 如果默认过滤器不满足需求，也可以自己重写`GlobalFilter.filter`方法，接受参数第一个是`ServerWebExchange`上下文和`GatewayFilterChain`放行器，通过注解`@Order`控制过滤器优先级，`[放行器].filter(上下文)`放行
5. 通过配置`spring.cloud.gateway.globalcors`控制跨域处理

### RabbitMQ

队列结构，异步暂存收发消息，AMQP是程序传递消息标准

1. `docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq`，15672是管理端口，5672是通信端口
2. 访问管理端口，默认用户名和密码`guest`（可以通过`-e RABBITMQ_DEFAULT_USER/RABBITMQ_DEFAULT_PASS`设置）
3. 引入springAMQP依赖
4. 配置`spring.rabbitmq`设置服务端配置，ip地址，端口号（5672），用户名密码，虚拟主机
5. 创建Bean`QueueBuilder.build()`创建队列
6. 注入`RabbitTemplate`往特定队列发消息
7. 新建类方法注解`@RabbitListener(queues = "[队列名]")`收消息

默认消息预取，可以通过`spring.rabbitmq.listener.simple.prefetch`设置预取上限，交换机需要绑定队列使用，使用`BindingBuilder.bind`绑定，如果要发对象消息尽量转成json（导入Jackson依赖之后在启动类注入新Bean`messageConverter`返回`Jackson2JsonMessageConverter()`）

- 简单工作队列只涉及队列，一个队列内的消息无法被多次获取
- Fanout Exchange把消息分发给连接的每一个队列
- Direct Exchange分发给RoutingKey一致的队列，监听端需要`@RabbitListener(bindings=@QueueBinding())`设置`key`表明监听标签
- Topic Exchange分发给多个单词的RoutingKey，`key`中间以`.`分割，支持通配符`#`多个单词`*`一个单词

#### 消息可靠性

- 生产者确认，交换机收到之后返回一个确认`ack`，到了队列之后返回一个成功`publish-confirm`，没到队列返回`publish-return`和失败原因，返回确认情况应该带上消息id，需要配置下面这些

  ```yaml
  spring:
  	rabbitmq:
  		publisher-confirm-type: correlated  # 异步回调
  		publisher-returns: true  # 开启失败信息返回
  		template:
  			mandatory: true  # 队列失败调用回调returnCallback
  ```

  `returnCallback`可以用`RabbitMQ.setReturnCallback`设置，确认的`Callback`我们则可以通过`CorrelationData.getFuture().addCallback()`设置回调函数在消息发送的时候追加到参数即可

- 消息持久化，RabbitMQ是内存应用，因此重启队列信息和交换机都没了，我们可以在创建队列和交换机和消息的时候携带需要持久化参数或者比如`QueueBuilder.durable().build()`即可实现持久化
- 消费者确认，接收到消息之后给RabbitMQ发一个`ack`他才会删除消息，Spring默认监听`Listener`即处理过程中是否抛出异常，有异常就不返回`ack`，但是可能出现一直重试，我们可以通过`spring.rabbitmq.listener.simple.prefetch/retry`设置本地重试或者创建`RepublishMessageRecoverer`把错误消息专门发到一个错误交换机

#### 死信交换机

消费者无法处理（返回`nack`），超时未消费，消息队列溢出之后的头消息称为死信，除了在代码内实现异常交换机投递，队列也可以通过设置属性`dead-letter-exchange=[交换机名]`绑定一个死信交换机用于处理死信

我们可以给队列或者消息设置TTL超时时间并绑定死信交换机（`deadLetterExchange`），超时之后就会进入死信交换机，从而实现消息延迟投递，比如用户下单取消，会议预定等

#### 惰性队列

消息太多内存不够用可以在创建队列的时候使用`lazy()`指定为惰性队列，则消息会直接写入磁盘而不是内存，取的时候也是去磁盘取，普通队列会在内存达到占用40%的时候才去写入磁盘，写入磁盘的过程不允许消息传入

#### MQ集群

分为分片和主从集群，集群内通过主机名识别和通信，但是集群的对象是队列而不是服务器因此只要多个MQ联通之后我们只需要创建队列时设置队列应该分片还是复制（主从）

1. 先开一个MQ然后`docker exec -it mq cat /var/lib/rabbitmq/.erlang.cookie`拿到一个cookie，集群内的MQ必须相同cookie才能通信

2. 集群需要事先写好配置文件和集群信息`rabbitmq.conf`

   ```conf
   listeners.tcp.default = 5672
   cluster_formation.peer_discovery_backend = rabbit_peer_discovery_classic_config
   cluster_formation.classic_config.nodes.[集群编号] = rabbit@[主机名]  # 多个
   ```

3. 启动容器的时候把cookie挂到`/var/lib/rabbitmq/.erlang.cookie`，配置文件挂到`/etc/rabbitmq/rabbitmq.conf`，并且指定`--hostname [主机名]`必须和设定的保持一致，由于RabbitMQ用的是主机名进行通信，因此如果服务器不在同一个机器下需要配置`/etc/hosts`把主机名和IP进行映射，之后访问任意一台服务器测试集群连通性

4. 在项目中配置`spring.rabbitmq.addresses`指定服务地址，多个地址用逗号分隔

5. 默认是分片集群，如果要创建主从队列我们在创建的时候加上`quorum()`即可

   > 上面是仲裁队列，要创建一般镜像队列则需要进入任意一个控制台编写`rabbitmqctl set_policy "[策略名称]" "[策略正则]" '{"ha-mode":[策略],"ha-params":[主从数量],"ha-sync-mode":"automatic"}'`策略正则比如`^test\.`那么就会在集群内对于`test`开头的队列创建指定数量的镜像或者是主从，其中策略可以用`exactly`，详细可以看[官网](https://www.rabbitmq.com/ha.html)

### ElasticSearch

用于搜索，拷贝自数据库，倒排索引，一张表是一个索引，表里的数据结构是映射，每一条记录是文档，可以用MQ和数据库实现同步

#### ES部署

1. `docker run --name es -d -e ES_JAVA_OPTS="-Xms512m -Xmx512m" -e "discovery.type=single-node" -v es-data:/usr/share/elasticsearch/data -v es-plugins:/usr/share/elasticsearch/plugins -p 9200:9200 -p 9300:9300 elasticsearch`，其中9200是用户搜索通信端口，9300是es集群互联通信端口
2. 启动成功之后访问9200可以得到默认返回的一条json，可视化监视es工作和管理可以再部署一个kibana`docker run -d --name kibana -e ELASTICSEARCH_HOSTS=http://[es ip]:9200 -p 5601:5601 kibana`接着访问5601看看是否连接上

#### DSL语法

只介绍一部分，大部分去[官网查](https://www.elastic.co/guide/en/elasticsearch/reference/8.6/index.html)

- `GET /_analyze`分词

  - 下载[IK分词器](https://github.com/medcl/elasticsearch-analysis-ik)，解压后传到plugins目录下重启ES，可以修改其中的`config/IKAnalyzer.cfg.xml`定位扩展和停用额外分词字典
  - `text`需要分词的文本
  - `analyzer`分词器名（`ik_smart`，`ik_max_word`）
- `PUT /[索引库名]`新建索引库映射

  - `mappings.properties`内是映射，`type`数据类型，`text`会被分词，`keyword`不会分词，`object`可以内含另外`properties`，其余差不多（`long`，`boolean`等），定义需要被搜索的类型时需要指定分词器
  - `/_mapping`新增字段，里面直接`properties`就行
  - `DELETE`，`GET`控制的都是索引库映射
- `POST /[索引库名]/_doc/[id]`新建文档

  - 根据映射约束添加字段，`GET/DELETE`同理
  - `PUT`如果指定的id已经存在就会删掉再增，`POST`则会报错
  - 每写一次文档都会更新一下版本
- `POST /[索引库名]/_update/[id]`局部更新，id不存在报错
- `GET /[索引库名]/_search`查询匹配结果，根据条件返回不同若干文档

  - `query`筛选范围，只例举部分，可查看[文档](https://www.elastic.co/guide/en/elasticsearch/reference/8.6/query-dsl.html)

    - `match`模糊查询
    - `range`值范围，包括比如`gte/lte`等
    - `term`精确查询
    - `geo_distance`以某一点为圆心`distance`为半径圆内所有文档，`geo_bounding_box`则是指定`top_left`和`bottom_right`方形区域内所有文档

    - `function_score`根据查询条件算分，里面嵌套`query`查询条件，`functions`数组包含过滤条件`filter`和额外分值`weight`以及`boost_mode`额外分的增加方式（默认加法）

    - `bool`满足或不满足若干指定条件的文档，包含`must/must_not/should/filter`其中filter和must一样，但是不参与算分
  - 除了`query`之外还有`sort`用于排序，`from`控制起始位置，`size`控制一页大小，`highlight`高亮（周围包围`<em>`标签，与常规筛选文档分离），具体看帮助文档
  - `aggs`聚合搜索，包括桶聚合（计数），度量聚合（最值均值），结果会和原本文档分开返回
    - `brandAgg`桶聚合，内用`terms`指定字段和值和聚合返回的数量`size`
    - `scoreAgg`度量聚合，内用`stats`指定字段和值，返回包含最大最小值均值和累计值，可和桶聚合嵌套使用，可以获得某个品牌价格的最值等

#### RestClient

1. 引入`elasticsearch-rest-high-level-client`依赖，必要修改ES版本`<elasticsearch.version>`，或者装一个和默认一致的ES
2. 初始化一个`new RestHighLevelClient(RestClient.builder(HttpHost.create("http://[ip]:[port]")))`和ES连接
3. 发请求前`client.indices().[操作方法]`，里面有所有的操作索引库的方法按照要求构建请求即可，如果文档操作则可以`client`直接点出来，条件查询则需要`SearchRequest`类，通过`source()`方法链式拼接所有条件后`client.search`
4. 发完请求获取的原始内容是一个长json，为了从中分离出我们需要的信息，我们可以先用请求工具模拟发一个请求，然后通过`response.getxxx()`找找有没有自己需要的字段，没有的话可以直接`.get("[字段名]")`强行抽取字段

#### 自动补全

下载[拼音分词器](https://github.com/medcl/elasticsearch-analysis-pinyin)，同样解压之后放到plugin里面，分词器指定`pinyin`即可

由于拼音分词器只能单个拼音分开，正常应该先IK分词之后再用拼音分词器，并且把分词结果保留拼音和词语两种形式才适合用于自动补全，因此我们需要自定义分词器，需要在创建索引库的时候带上`settings`字段，如下

```json
PUT /test
{
    "settings": {
        "analysis": {
            "analyzer":{
                "my_analyzer": {
                    "tokenizer": "ik_max_word",
                    "filter": "py"
                }
            },
            "filter": {
                "py": {
                    "type": "pinyin",
                    "keep_full_pinyin": false,
                    "keep_joined_full_pinyin": true,
                    "keep_original": true,
                    "limit_first_letter_length": 16,
                    "remove_duplicated_term": true,
                    "none_chinese_pinyin_tokenize": false
                }
            }
		}
    }
}
```

同时需要注意文档存储时混合使用IK和拼音分词器，搜索的时候只用IK即可，因此创建索引库的时候还应该指明

```json
"mappings": {
    "properties": {
        "name": {
            "type": "text",
            "analyzer": "my_analyzer",
            "search_analyzer": "ik_smart"
        }
    }
}
```

#### ES集群

1. 在上面的基础上改一下部分环境配置`docker run --name es -d -e ES_JAVA_OPTS="-Xms512m -Xmx512m" -e "discovery.seedhosts=[ip1],[ip2]" -e "cluster.name=[集群名称]" -e "cluster.initial_master_nodes=[ip1],[包括自己]" -v es-data:/usr/share/elasticsearch/data -v es-plugins:/usr/share/elasticsearch/plugins -p 9200:9200 elasticsearch`，`discovery.seedhosts`是其他两个ES的位置，`cluster.name`是集群名称，`cluster.initial_master_nodes`是可以参与选举成为主节点的ES，由于默认用9300内部通信因此不需要暴露出来，其余几个ES把暴露端口改一改就行了
2. 安装一个cerebro代替kibana管理ES集群，里面随便输入一个节点就行
3. 在创建索引库的时候定义`settings.number_of_shards/number_of_replicas`可以指定分片数量和副本数量

为了防止脑裂，集群数量最好是奇数，插入数据的时候会根据文档的id来分配数据应该被存到哪个分片，因此索引库创建之后分片数量不能修改，节点坏了之后其他节点会把坏了的节点数据迁移到其他节点，好了之后再还原

### Sentinel

雪崩就是上游机器阻塞了下游爆一堆，常用解决策略有超时处理，舱壁模式，熔断降级

Sentinel用信号量隔离，基于慢调用比例或异常比例熔断降级，支持QPS和调用关系的限流及慢启动和匀速排队，

- 把jar包[下过来](https://github.com/alibaba/Sentinel)直接启动，可以用`-Dserver.port`设定端口等，详细看[wiki](https://github.com/alibaba/Sentinel/wiki)，默认sentinel账号密码
- 项目内引入`spring-cloud-starter-alibaba-sentinel`
- 配置Sentinel地址`spring.cloud.sentinel.transport.dashboard`，如果使用了Feign则还需要配`feign.sentinel.enabled`并
- 启动项目后对任意Controller发一次请求才会在Sentinel控制面板上显示监控信息，默认Sentinel只监控Controller方法
- 接收请求的限流规则直接在Sentinel控制台配配配就行了，发送请求的限流规则（比如整合Feign，用户请求的接口调用了其他微服务接口的情况）则需要手动实现`FallbackFactory`然后在`@FeignClient`注解上指明`FallbackFactory`
- 由于大部分含Sentinel的微服务都是网关转发过来的，因此网关在转发请求的时候可以携带一些身份认证，之后在Sentinel里面配置通过的授权规则，避免不法分子滥用接口
- 想要自定义异常处理，则需要实现`BlockExceptionHandler`里面的`handle`方法通过判断`BlockExceptinon`的类型来分别进行异常处理
- 如果想要保存Sentinel的配置到Nacos那得自己改动源代码，解压之后找到`sentinel-dashboard`添加`sentinel-datasource-nacos`依赖，`然后找src.test.java...rule.nacos`复制到`main.java..rule`里面并在配置文件内添加`nacos.addr`，同时修改`...controller.v2.FlowControllerV2`类更改两处`@Qualifier("flowRuleNacosProvider/Publisher")`，修改`webapp.app.scripts.directives.sidebar.sidebar.html`解开`流控规则-NACOS`标签注解打包，接着在自己的项目里也引入依赖`sentinel-datasource-nacos`，配置`spring.cloud.sentinel.datasource.flow.nacos`确定Nacos地址，还是比较麻烦的

### Seata

处理分布式事务，原子性，一致性，隔离性，持久性（ACID）

#### Seata部署

1. 下载压缩包解压

2. `conf/registry.conf`服务注册和配置

3. Seata会将分布式事务内容记录到数据库，因此要在配置中心（比如Nacos）添加配置文件`seataServer.properties`添加数据库依赖

   ```properties
   # 数据存储方式，db代表数据库
   store.mode=db
   store.db.datasource=druid
   store.db.dbType=mysql
   store.db.driverClassName=com.mysql.jdbc.Driver
   store.db.url=jdbc:mysql://127.0.0.1:3306/seata?useUnicode=true&rewriteBatchedStatements=true
   store.db.user=root
   store.db.password=123
   store.db.minConn=5
   store.db.maxConn=30
   store.db.globalTable=global_table
   store.db.branchTable=branch_table
   store.db.queryLimit=100
   store.db.lockTable=lock_table
   store.db.maxWait=5000
   # 事务、日志等配置
   server.recovery.committingRetryPeriod=1000
   server.recovery.asynCommittingRetryPeriod=1000
   server.recovery.rollbackingRetryPeriod=1000
   server.recovery.timeoutRetryPeriod=1000
   server.maxCommitRetryTimeout=-1
   server.maxRollbackRetryTimeout=-1
   server.rollbackRetryTimeoutUnlockEnable=false
   server.undo.logSaveDays=7
   server.undo.logDeletePeriod=86400000
   
   # 客户端与服务端传输方式
   transport.serialization=seata
   transport.compressor=none
   # 关闭metrics功能，提高性能
   metrics.enabled=false
   metrics.registryType=compact
   metrics.exporterList=prometheus
   metrics.exporterPrometheusPort=9898
   ```

4. 新建库Seata（和配置保持一致），然后建表

   ```sql
   SET NAMES utf8mb4;
   SET FOREIGN_KEY_CHECKS = 0;
   
   -- ----------------------------
   -- 分支事务表
   -- ----------------------------
   DROP TABLE IF EXISTS `branch_table`;
   CREATE TABLE `branch_table`  (
     `branch_id` bigint(20) NOT NULL,
     `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
     `transaction_id` bigint(20) NULL DEFAULT NULL,
     `resource_group_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `resource_id` varchar(256) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `branch_type` varchar(8) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `status` tinyint(4) NULL DEFAULT NULL,
     `client_id` varchar(64) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `gmt_create` datetime(6) NULL DEFAULT NULL,
     `gmt_modified` datetime(6) NULL DEFAULT NULL,
     PRIMARY KEY (`branch_id`) USING BTREE,
     INDEX `idx_xid`(`xid`) USING BTREE
   ) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Compact;
   
   -- ----------------------------
   -- 全局事务表
   -- ----------------------------
   DROP TABLE IF EXISTS `global_table`;
   CREATE TABLE `global_table`  (
     `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
     `transaction_id` bigint(20) NULL DEFAULT NULL,
     `status` tinyint(4) NOT NULL,
     `application_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `transaction_service_group` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `transaction_name` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `timeout` int(11) NULL DEFAULT NULL,
     `begin_time` bigint(20) NULL DEFAULT NULL,
     `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
     `gmt_create` datetime NULL DEFAULT NULL,
     `gmt_modified` datetime NULL DEFAULT NULL,
     PRIMARY KEY (`xid`) USING BTREE,
     INDEX `idx_gmt_modified_status`(`gmt_modified`, `status`) USING BTREE,
     INDEX `idx_transaction_id`(`transaction_id`) USING BTREE
   ) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Compact;
   
   SET FOREIGN_KEY_CHECKS = 1;
   ```

5. 运行`seata-server.sh`启动服务

6. 项目内引入依赖`seata-spring-boot-starter`，如果版本不够需要手动调一下

7. 配置`seata.registry.nacos`下的Nacos配置，地址，命名空间，服务名称，组

8. 配置`seata.tx-service-group`事务组，然后配置`service.vgroup-mapping.seata-demo`设置集群名称

9. 设置`seata.data-source-proxy-mode`设置解决方案名称（XA，AT，TCC，SAGA）

10. 给发起全局事务的入口方法（Service）添加`@GlobalTransactional`注解

#### Seata架构

- RM用于控制每一个和数据库交互的微服务（Service中的调用方法）
- TM用于向TC发起全局事务请求和调用RM（Service）
- TC用于管理整个分布式事务状态和服务配置（启动的服务器）

#### 解决方案

- CAP定理

  - 一致性（Consistency），数据备份及时完成同步
  - 可用性（Availability），访问任意节点都要即时反馈
  - 分区容错（Partition Tolerance），在出现错误时维持一致性和可用性的平衡

  > ES是高一致低可用（CP），每一个节点坏了就不管他上面的同步了

- BASE理论

  - 基本可用（Basically Available），出现故障时保证部分可用
  - 软状态（Soft State），允许出现临时不一致状态
  - Eventually Consistent（最终一致性），软状态结束之后必须数据一致

- XA模式，所有事务执行完不提交，所有微服务事务都没错之后再统一提交，但是占用锁，低可用

- AT模式，直接提交并保存快照，失败之后恢复快照，但是单纯保存快照可能产生脏写因此还是占用锁，只不过这个锁Seata管理而不是数据库（较多使用）

- TCC模式，直接尝试提交并保存反向更新方法和此条事务的相关信息（全局事务ID，事务三种状态（尝试提交，确认，回滚），事务操作内容），适用于数字类加减更新，无法自动完成必须手动配置反向更新操作详细内容，自己写的时候还需要考虑幂等，空回滚，业务悬挂等健壮性

  ![img](https://s2.loli.net/2023/02/08/17sEDtz6e8l3RMQ.png)

  > 之后实现接口方法控制尝试提交，确认提交和回滚

- SAGA模式，在TCC基础上删掉了保存事务信息的过程，只进行提交和回滚，没有事务隔离性

### Redis

停机后Redis不保存数据，并发能力有限，一个Redis宕机了就寄了

#### 持久化

- RDB，每一段时间拷贝一整个Redis内容到文件中，默认在正常停机之后执行，在`redis.conf`里面配置`save [探测时间] [修改数量]`控制RDB执行频率，可以配多个
- AOF，每一段时间在文件后追加修改内容，文件比较大，需要配置`appendfsync always/everysec`，嫌文件太大了可以用`auto-aof-rewrite-min-size 64mb`在超过之后自动整理

#### 集群

在配置里加上`slaveof [master-ip] [master-port]`即可实现主从，主从全量同步（第一次）用RDB方式保证基本一致，用LOG保证完全一致，增量同步则根据从里面的偏移量（offset）控制差多少同步差的内容，偏移量差太多了就全量，默认主写从读，从节点没有写入权限

额外加一层Redis哨兵监控主节点是否可用，不可用之后所有哨兵投票出一个从节点替换主节点，我们直接找哨兵要主从节点地址，用`redis-sentinel`启动一个哨兵，其配置文件可以看[官网](https://redis.io/docs/management/sentinel/)，Sentinel配置只需要指定主节点地址即可

由于要用RDB因此单点Redis内存不要分太大，于是就可以进行分片，集群内多个主节点互相监控就不需要Sentinel了，同时每一个主节点还可以有多个从节点保证可用，改一下配置文件

```conf
port 6379
# 开启集群功能
cluster-enabled yes
# 集群的配置文件名称，不需要我们创建，由redis自己维护
cluster-config-file /tmp/6379/nodes.conf
# 节点心跳失败的超时时间
cluster-node-timeout 5000
# 持久化文件存放目录
dir /tmp/6379
# 绑定地址
bind 0.0.0.0
# 让redis后台运行
daemonize yes
# 注册的实例ip
replica-announce-ip 192.168.150.101
# 保护模式
protected-mode no
# 数据库数量
databases 1
# 日志
logfile /tmp/6379/run.log
```

然后执行`redis-cli --cluster create --cluster-replicas [每一个主节点多少个从节点] [多个ip:port]`即可，注意后面的IP个数应该能被前面的数字加一整除

分片通过哈希计算插槽，分到固定的分片，每一个分片享有固定数量插槽，我们可以在在设置键的时候把同类键值加上`{}`统一字段控制被分配到同一个分片，如果想新加一个分片，则可以在新开的Redis上`redis-cli --cluster reshard [ip:port]`根据提示分片

1. 引入`spring-boot-starter-data-redis`

2. 配置`spring.redis.sentinel.nodes/master`配置Sentinel集群地址和主节点名称，如果是分片集群则直接配`spring.redis.cluster.nodes`所有节点即可

3. 注入读写分离配置（RedisTemplate底层用的是Lettuce）

   ```java
   @Bean
   public LettuceClientConfigurationBuilderCustomizer configurationBuilderCustomizer(){
       return configBuilder -> configBuilder.readFrom(ReadFrom.REPLICA_PREFERRED);
   }
   ```

### Caffeine

用于内部缓存，随每一个微服务启停产生和消失，近似一个NoSQL数据库

- 引入springcloud之后默认已经引入直接使用就行
- `Caffeine.newBuilder().build()`创建一个缓存对象
- 通过build出来的这个对象`.put`方法记录键值，`.get`获取键值，包括设置缓存上限和有效时间等，自己试一试也容易

### OpenResty

就是Nginx+Lua，加了Lua之后可以作为请求分发使用，要用Lua得添加模块依赖

```conf
lua_package_path "/usr/local/openresty/lualib/?.lua;;";
lua_package_path "/usr/local/openresty/lualib/?.so;;";
```

之后转发请求规则可以这么写

```conf
server {
	location /api/item {
		default_type application/json;
		# 响应结果由指定文件控制
		content_by_lua_file lua/item.lua;
	}
}
```

在OpenResty里面，Lua函数库大部分都可以在`ngx`里面找到（不需要导入），在微服务中，我们用Nginx进行请求分发和本地缓存，本地缓存没有则转发请求到Redis再没有再请求Tomcat，这个过程中主要的几个函数有以下几个

- `ngx.log(ngx.ERR,content)`打印到日志

- `ngx.location.capture(path,param)`发起一个请求并获取结果
- `ngx.shared.item_cache:set(key,value,timeout)`存入本地缓存，注意在此之前需要在`nginx.conf`中添加`lua_shared_dict item_cache [容量]`来设置本地缓存容量
- `require('resty.redis'):new()`创建一个Redis对象，之后使用`:connect`获取Redis连接，用`:set_timeouts`等方法设置连接配置，和go一样调用函数的过程中可以用例如`ok,err = redis:connect(ip,port)`进行错误处理
- `ngx.say([返回内容])`返回给发送者内容（一般是JSON）
- `require('cjson').encode/decode`序列化和反序列化JSON

### Canal

缓存同步的策略一般有设置有效期（时效性差），同步双写（代码侵入），异步通知（MQ，权衡后的结果）三种方式

监听数据库Log文件在数据进行变动之后

1. 开启数据库主从，MySQL在`conf/my.cnf`中添加启用日志`log-bin=[log文件位置和名称]`和启用日志的数据库`binlog-do-db=[数据库名]`

2. Canal用docker启动还是有点麻烦的，可以写一个docker-compose文件

   ```yaml
   version: '3'
   
   services:
     canal-server:
       image: canal/canal-server:v1.1.4
       container_name: canal-server
       restart: unless-stopped
       network_mode: host
       ports: 
         - 11111:11111
       environment:
         - canal.auto.scan=false
         - canal.instance.master.address=127.0.0.1:3306
         - canal.instance.dbUsername=canal
         - canal.instance.dbPassword=canal
         - canal.instance.filter.regex=.*\\..*
         - canal.destinations=test
         - canal.instance.connectionCharset=UTF-8
         - canal.instance.tsdb.enable=true
       volumes:
         - /root/canal/test/log/:/home/admin/canal-server/logs/
   ```

3. 引入`canal-spring-boot-starter`，配置`canal.destination`集群名称和`canal.server`地址和端口

4. 编写实现类实现`EntryHandler<[表实体类]>`接口并添加`@CanalTable([监听表名])`，实现`insert/update/delete`方法即可

5. 还需要在实体类中加`@id`注解到属性标注主键，添加`@Transient`注解到不属于表中的属性

