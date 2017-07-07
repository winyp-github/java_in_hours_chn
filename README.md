# Java编程一天入门

## 一 准备编程 (建议时间: 20分钟. 如果卡住,请在代码库开issue, 下同)
编程就是让计算机做你想让它做的事.

编程语言是工具,就像锤子,应该拿上手就可以用.

为了编写第一个Java程序,必需一个Java开发套件(JDK),以及一个写程序的文本编辑工具.
本文的代码足够简单,集成开发环境的用处不大,任何文本编辑器都可以(推荐工具待定).

安装Oracle JDK后, 打开命令行窗口,运行javac和java,不报错"command not found",即为成功,可以继续. (待续:常见问题与解决)

扩展资料: 解释器与编译器的区别, JDK(Oracle JDK, OpenJDK), IDE(Eclipse, NetBeans, IntelliJ等等)

## 二 写第一个程序 (建议时间: 20分钟)

新建文本文件,命名为"问好.java".输入最简单的一个Java程序:

```
class 问好 {
  public static void main (String[] 参数) {
    // 待续: 要让它做的事
  }
}
```

这个程序定义了一个类(class),名叫"问好",文件名一般与类名相同. 这个类就是一个程序. 里面的main是程序入口. 注意所有的大括号都需要配对. 双斜杠"//"之后的是注释,是为读代码的人方便理解写的,不影响编译运行.
"参数"很扎眼吧,不用急,第四讲就知道它做什么了.

这个程序可以编译运行(见"手把手"部分),但运行后没有任何输出.因为这个程序是个空架子,没有任何可以看到的运行结果.下面就让它做点事.

```
class 问好 {
  public static void main (String[] 参数) {
    // 要让它做的事
    System.out.println("吃了么");
  }
}
```

加上的这行代码将打印一行字,内容是"吃了么".

试试编译运行,将看到命令行下输出:
```
吃了么
```

试试改字符串的内容,再编译运行.恭喜! 你已经可以写出无数个不同的Java程序了.
再试试加一行相同的代码,输出结果变了吗? 恭喜! 你已经可以写出无限长的Java程序了.

### 手把手:
在命令行下编译运行
在程序文件的目录下,运行下面的命令:
```
$ javac 问好.java
```
此命令将程序文件编译生成.class文件,在这个目录下多了一个"问好.class"文件
```
$ java 问好
```
此命令寻找并运行叫"问好"的类

## 三 Java的现状 (建议时间: 10分钟)
在更进一步之前,最好了解现在Java都用来做什么.

优点:
- 开源: Oracle JDK是开源的, 另有一个社区维护的版本OpenJDK.
- 程序员用户群很大,可以用的成熟的经过时间检验的库很多.

用途:
- 很大一部分网络服务
- 大多数安卓手机应用
- 少量游戏和桌面应用
- 一些企业内部用Java Applet做可以嵌入网页的在线工具. 注: Chrome浏览器已不支持Java Applet,原因之一是安全性

扩展资料: Apache Maven, Java Applet

## 四 用Java算术 (建议时间: 40分钟)

新建文件"四则运算.java"
```
class 四则运算 {
  public static void main (String[] 参数) {
    System.out.println(1+2);
  }
}
```
编译运行后,果然输出3. 再试试学过的四则运算吧,加减乘除运算符分别是+-*/.
还有括号也可以用. 注: 如果算式中所有的数都是整数,那么每步运算都会取整
恭喜! 你已经可以用Java程序完成数学运算了.

那么其他的运算呢?
新建文件"根号.java"
```
class 根号 {
  public static void main (String[] 参数) {
    System.out.println(Math.sqrt(4));
  }
}
```
既然命名是"根号",看起来告诉程序的值是4,那么如果程序写的正确,自然应该输出4开根号,就是2
编译运行后, 果然打印出了2.0. Math.sqrt是Java中开根号的方法.
应该不用啰嗦了,试试把4改成其他的数,看看结果如何?
现在,你可能已经觉得程序的"回答"太"精简"和生硬了,那么人性化一些吧:
```
class 根号 {
  public static void main (String[] 参数) {
    System.out.println("4的平方根是" + Math.sqrt(4));
  }
}
```
输出听起来顺耳些了,但是如果想要把4改成其他数,就需要改程序的两个地方,这种麻烦可要不得! 可以把4先存到一个变量里,然后在两处引用同一个变量:
```
class 根号 {
  public static void main (String[] 参数) {
    int 数 = 4;
    System.out.println(数 + "的平方根是" + Math.sqrt(数));
  }
}
```
这样只要改一处程序了.不过,为了改一个参数,还是要改程序,再编译再运行,这种麻烦可要不得! "参数"终于派上用场了.
```
class 根号 {
  public static void main (String[] 参数) {
    int 数 = Integer.parseInt(参数[0]);
    System.out.println(数 + "的平方根是" + Math.sqrt(数));
  }
}
```
"参数[0]"是"参数"数组的第一个值. Integer.parseInt是Java把字符串转换成整数的方法.
现在代码里没有了输入值,该怎样告诉程序需要给什么数开根号呢?
在运行程序时,命令后加上一个"参数":
```
$ java 根号 4
```
如果忘了在运行时加参数, 这个程序会打印一个异常报告: java.lang.ArrayIndexOutOfBoundsException
意思是:数组是空的,却要取第一个值,没辙.

试试多加几个参数吧, 参数[1]是"参数"数组第二个值,以此类推.
恭喜! 你的程序不用修改代码就可以接受不同的外部输入了.

Math是Java自带标准库中的数学类,包含很多有用的方法.详细请查阅JDK文档. 标准库还有很多有用的类.
比如随机数很有用,聊天机器人少不了它.
新建"随机数生成器.java":
```
class 随机数生成器 {
  public static void main (String[] 参数) {
    java.util.Random 生成器 = new java.util.Random();
    System.out.println("来一个随机数:" + 生成器.nextInt());
  }
}
```
java.util.Random是随机数类的全路径, java.util是它所在的包. 没有全路径Java就找不到这个类了.
为什么Math和Integer没有这样的前缀呢? 因为他们在java.lang包里,是"亲生"的,不用包名Java也能找到这些类.
"生成器"是随机数类的一个"个体". 用new关键词来产生. 一个现实的比方: "人"是一个类型, 你我都是同样类型的不同个体.
nextInt是产生一个随机数的方法. 为什么Math.sqrt和Integer.parseInt不用new出一个个体呢? 留个悬念吧.
这样重复类的全名看着真累, 下面用import来开头导入这个类路径, 之后就不用再重复了:
```
import java.util.Random;

class 随机数生成器 {
  public static void main (String[] 参数) {
    Random 生成器 = new Random();
    System.out.println("来一个随机数:" + 生成器.nextInt());
  }
}
```

扩展资料: 数组, 异常, 方法, JDK文档