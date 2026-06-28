# Java期末复习讲义

> 目标：30-40 分钟内讲清 Java 基础概念、基础语法、基本数据类型与常见考点
> 本讲义不展开：类与对象设计、继承、多态、接口、异常等内容


## 1. Java 基本概念（历年选择题高频）

### 1.1 Java 的三层结构

- JVM：执行字节码的虚拟机。
- JRE：JVM + 运行 Java 程序所需的核心类库。
- JDK：JRE + 编译工具（`javac`）与开发工具。
**JDK = JRE + 开发工具；JRE = JVM + Java类库；JVM 只负责运行字节码(.class)**，**包含层级：JDK ⊃ JRE ⊃ JVM**

#### 1.2 JVM（Java Virtual Machine，Java虚拟机）
**只负责运行程序，最小单元**
- 作用：解析 `.class` 字节码文件，翻译成当前操作系统（Windows/Linux/Mac）能识别的机器码，实现**一次编译、到处运行(跨平台)**
- 特点：**不包含类库、编译工具**，不同系统有专属JVM（win版、linux版）
- 职责：内存管理、垃圾回收GC、字节码解释执行

#### 1.3 JRE（Java Runtime Environment，Java运行环境）
**运行Java程序必备，没有编译功能**
$$\boldsymbol{JRE = JVM + 核心类库(rt.jar等)}$$
- JVM：负责执行代码
- Java基础类库：`String、ArrayList、IO、集合`等系统自带API
- 使用场景：**只运行别人写好的Java程序（jar/exe），不需要写代码**，服务器部署项目只装JRE即可

#### 1.4 JDK（Java Development Kit，Java开发工具包）
**Java程序员开发用的全套环境**
$$\boldsymbol{JDK = JRE + 开发工具包}$$
- 内置JRE：能运行程序
- 开发工具：
  - `javac`：编译.java源码 → .class字节码
  - `java`：运行class程序
  - jar打包、jdb调试、jps/jmap等JVM排查工具
- 使用场景：**写代码、编译、调试Java项目必须安装JDK**

# 快速区分使用场景
1. 只想运行Java游戏/软件 → 装 **JRE**
2. 写Java代码、开发项目 → 装 **JDK**
3. JVM不能单独安装，JRE/JDK自带JVM


#### 1.5 编译与运行流程

- 源码：`.java` → 编译：`javac` → 字节码：`.class` → 运行：`java`。
- “一次编译，到处运行”：依赖 JVM 的跨平台特性。

#### 1.6 其他Java常考的一些特点
- java提供了自动分配和回收内存空间
- Java 语言不使用指针,而是引用
- 健壮性：严格的类型检查，编译期就能发现大量错误
- 支持多线程

## 2. Java 程序最小结构（不考虑package,import）

> Java 程序必须放在类中。这里仅作为语法要求说明，不展开类与对象知识。

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Java");
    }
}
```

- 文件名必须与 `public class` 类名一致（如 `Main.java`）。
- 所有的 Java 程序由 `public static void main(String[] args)` 方法开始执行,public和static是修饰符可以交换位置
- 一个源文件中只能有一个 public 类,内部类不受这个限制！
- 一个类可以有多个main方法（重载）

## 3. 基本语法与关键字速查

### 3.1 注释

- 单行注释：`//`
- 多行注释：`/* ... */`
- 文档注释：`/** ... */`

### 3.2 标识符规则

- 由字母、数字、`_`、`$` 组成，不能以数字开头。(这里和c语言略有不同，可以使用`$`，但不推荐)
- 区分大小写，不能是关键字。
- 命名习惯：类名首字母大写，变量/方法小驼峰。

### 3.3 Java 核心关键字详解表

| 关键字        | 类型         | 作用范围/修饰目标          | 核心特点与作用                                                                                                                                     |
| ------------- | ------------ | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **public**    | 访问修饰符   | 类、方法、变量             | 1. 公开权限，所有类均可访问<br>2. 跨包、同类、子类、无关类都能调用<br>3. 程序入口 `main` 必须用 public                                             |
| **private**   | 访问修饰符   | 方法、变量、内部类         | 1. 私有权限，**仅当前类内部可访问**<br>2. 子类、外包、同类包其他类都无法访问<br>3. 封装核心关键字，保证数据安全                                    |
| **protected** | 访问修饰符   | 方法、变量                 | 1. 受保护权限<br>2. 同类、同包、**子类（无论是否同包）** 可访问<br>3. 不同包的无关类不能访问                                                       |
| **default**   | 访问修饰符   | 类、方法、变量             | 1. **不写任何修饰符就是 default**<br>2. 包访问权限：仅**同类 + 同包类**可访问<br>3. 不同包（含子类）都无法访问                                     |
| **static**    | 非访问修饰符 | 变量、方法、代码块、内部类 | 1. 静态成员，属于**类**，不属于对象<br>2. 优先于对象加载，可直接通过**类名调用**<br>3. 静态方法不能直接访问非静态成员<br>4. 静态变量全类共享一份   |
| **final**     | 非访问修饰符 | 类、方法、变量             | 1. **最终的、不可改变的**<br>2. 修饰类：类不能被继承<br>3. 修饰方法：方法不能被重写<br>4. 修饰变量：变量变为常量，只能赋值一次                     |
| **abstract**  | 非访问修饰符 | 类、方法                   | 1. **抽象的**<br>2. 修饰方法：只有声明，没有方法体<br>3. 修饰类：包含抽象方法，**不能实例化**<br>4. 子类必须重写所有抽象方法，否则子类也要是抽象类 |

---

#### 访问权限从小到大排序
- private  <  default  <  protected  <  public

## 4. 基本数据类型

### 4.1 八种基本类型

| 类型    | 位数 | 取值范围（大致） | 备注             |
| ------- | ---- | ---------------- | ---------------- |
| byte    | 8    | -128 ~ 127       | 小整型           |
| short   | 16   | -3e4 ~ 3e4       | 小整型           |
| int     | 32   | -2^31 ~ 2^31-1   | 默认整型         |
| long    | 64   | -9e18 ~ 9e18     | 末尾加 `L`       |
| float   | 32   | 单精度           | 末尾加 `F`       |
| double  | 64   | 双精度           | 默认浮点         |
| char    | 16   | Unicode 字符     | **2 字节，常考** |
| boolean | 1    | true/false       | 不能用 0/1       |
。
### 4.2 Java自动类型转换
整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。

转换从低级到高级：
> 低  ------------------------------------> 高
> `byte,short,char` —> `int` —> `long` —> `float` —> `double`

## 数据类型转换规则
1. 不能对`boolean`类型进行类型转换。
2. 不能把对象类型转换成不相关类的对象。
3. 在把容量大的类型转换为容量小的类型时必须使用**强制类型转换**。
4. 转换过程中可能导致溢出或损失精度

## 5. 运算符与表达式

### 5.1 运算符分类

- 算术：`+ - * / %`
- 关系：`> >= < <= == !=`
- 逻辑：`&& || !`
- 位运算：`& | ^ ~ << >> >>>`
- 三目：`条件 ? 表达式1 : 表达式2`

### 5.2 易混点

- `++i` 与 `i++`：前者先加后用，后者先用后加。

## 6. 流程控制

### 6.1 if / else

```java
int score = 85;
if (score >= 90) {
    System.out.println("A");
} else if (score >= 60) {
    System.out.println("B");
} else {
    System.out.println("C");
}
```

### 6.2 switch

- 可用类型：`byte/short/char/int/String`。
- 注意 `break`，否则会贯穿执行。

### 6.3 循环

- `for` 适合已知次数，`while` 适合未知次数。
- `do...while` 至少执行一次。

## 7. 数组基础
### 7.1 声明与初始化
```java
// 1. 声明（此时只是引用变量，未分配空间）
int[] arr1;
int arr1[];//其实也可以，但是一般不这样

// 2. 动态初始化（指定长度，元素为默认值）
arr1 = new int[5];          // [0, 0, 0, 0, 0]

// 3. 静态初始化（编译器自动推导长度）
int[] arr2 = new int[]{1, 2, 3, 4, 5};
int[] arr3 = {1, 2, 3, 4, 5};   // 简写形式，只能在声明时使用

// 动态初始化：3行4列
int[][] matrix = new int[3][4];

// 静态初始化
int[][] matrix2 = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```
### 7.2 Arrays
```java
import java.util.Arrays;

public class Test {
    public static void main(String[] args) {
        int[] arr = {3,1,4,2};

        // 1. 打印数组（直接打印数组会输出地址，用Arrays才会输出内容）
        System.out.println(Arrays.toString(arr)); // [3, 1, 4, 2]

        // 2. 数组排序
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr)); // [1, 2, 3, 4]

        // 3. 数组查找
        int index = Arrays.binarySearch(arr, 3); // 找元素3的下标
        System.out.println(index); // 2

        // 4. 数组复制
        int[] newArr = Arrays.copyOf(arr, arr.length);
    }
}
```

### 7.3 ArrayList

```java
import java.util.ArrayList;

// 创建（泛型，只能存对象类型；基本类型需用包装类）
ArrayList<String> list = new ArrayList<>();
ArrayList<Integer> nums = new ArrayList<>(100);  // 指定初始容量，避免频繁扩容

// 增删改查
list.add("Java");
list.add("Python");
list.add(1, "C++");          // 在索引 1 处插入
list.set(0, "Go");           // 修改索引 0
list.remove(1);              // 删除索引 1
list.remove("Go");           // 删除指定对象（需重写 equals）

String first = list.get(0);  // 读取
int size = list.size();      // 元素个数（注意不是 length）
boolean exists = list.contains("Java");

// 清空
list.clear();
boolean empty = list.isEmpty();

// 遍历方式
// 1. 普通 for
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

// 2. 迭代器（遍历时安全删除）
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    String s = it.next();
    if (s.equals("Java")) {
        it.remove();  // 正确：用迭代器的 remove
    }
}

```

## 8. 字符串基础


```java
// 创建 String 对象
String str1 = "Hello Java";  // 直接赋值
String str2 = new String("Hello Java");  // 构造方法创建（新对象）

// 获取长度
int len = str1.length();  

// 按索引获取字符
char ch = str1.charAt(0);  // 获取索引0的字符：'H'

// 字符串拼接
String concatStr = str1.concat(" World");  // 拼接："Hello Java World"
String addStr = str1 + "!!!";  // 最常用拼接方式

// 分割字符串
String str = "a,b,c,d";
String[] splitArray = str.split(",");  // 按逗号分割，返回数组：["a","b","c","d"]

// 遍历字符串
for (int i = 0; i < str1.length(); i++) {
    System.out.println(str1.charAt(i));
}
```

## 9. 输入输出


```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);//System.in是标准输入流，System.out是标准输出流，in和out是System类中的静态变量

        int n = sc.nextInt();
        long l = sc.nextLong();
        double d = sc.nextDouble();
        String s = sc.next();          // 读单词
        String line = sc.nextLine();    // 读整行

        System.out.println("输出内容");//换行
        System.out.printf("%.2f\n", d);//不换行

    }
}
```

```java

import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    public static void main(String[] args) throws Exception {
        int n = Integer.parseInt(br.readLine());
        double d = Double.parseDouble(br.readLine());

        String[] arr = br.readLine().split(" ");
        int a = Integer.parseInt(arr[0]);
        int b = Integer.parseInt(arr[1]);

        bw.write("Hello\n");
        bw.flush();
    }
}

```

## 10. Java构造方法

- 与类名相同：构造方法的名称必须与类名完全一致。
- 没有返回类型：构造方法没有返回类型声明，即使是 void 也不写。这使得它与普通方法区分开来。
- 自动调用：每次使用 new 创建对象时，构造方法会自动调用，以初始化对象的属性和状态。
- 不能直接调用：构造方法只能通过 new 关键字在创建对象时调用，不能像普通方法那样直接调用。
- 默认构造方法：如果没有定义任何构造方法，Java 会提供一个无参的默认构造方法。但一旦定义了任何其他构造方法，Java 不再提供默认构造方法。
- this 关键字的使用：在构造方法中可以使用 this 来引用当前对象的属性、方法
- 不能被继承，但可以被调用：构造方法不能被子类继承，但子类可以使用 super() 来调用父类的构造方法，以便初始化继承的属性。

## 11. 常用的库
1. java.lang,自动导入,包括String,System,Integer等包装类,Trownable等异常类
2. java.util,集合工具类ArrayList,Scanner,Iterator
3. java.io,输入输出流,BufferedReader,BufferedWriter,FileReader,FileWriter
4. java.awt,java.swing,图形界面


