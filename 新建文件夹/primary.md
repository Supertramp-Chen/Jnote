# GitHub

## 使用Git/GitHub/Markdown进行项目协作，团队协作 (与开发者进行对话)

```java
/*
    团队协作的开发流程

    clone操作（把远端的代码复制一份到本地）

    打开项目后，fist右上角maven 刷新一下项目 避免idea没有识别项目里的内容
*/
```

## git分支

```java
/*
    一个项目由多人进行开发，若其都在一个分支上开发 在一个分支上写代码 项目会变得混乱不堪

    每个分支代表一份独立的不同的代码库本

    idea——git master(当前这代码处于master这个分支上)    切换分支
*/
```

## git commit/push

```java
/*
    修改代码

    git的仓库就是一个项目的最小单位

    fork（把这个仓库在自己的仓库中复制一份，为了修改代码，clone自己的项目可修改 在别人的仓库中没有权限）fork后原来的仓库更新和自己fork到本地的没有关系

    GitHub上的仓库你clone一份到自己本地了 , 修复

    commit : 把当前对代码的变更（XXX.java）提交到本地仓库

    push : 把当前本地仓库的变更全部一次性的推到远端去  

    new pull request （请求项目代码拥有者把你的代码合并到他们的代码中去）, commits

*/
```

## markdown

```java
/*
    GitHub上任何可以输入东西的地方

    可以用非常简单的语法写出很好的文章的一种写作方法 标记语言

    # 标题
    - [] 列表
    - [x]

    **加粗**

     _倾斜_ 

    > 引用
     
    `行内代码`

    这是[谷歌的首页][hyyps://www.google.com]
*/
```

## github

```java
/*
可以把仓库看成一棵树

可以看到仓库详细的历史
*/
```




# 生产力工具

## maven 自动化构建工具

```java
/*
    maven只定义了个生命周期，每个插件可以把自己的工作绑定在上面

    当你执行相应阶段的时候，maven会把前面的阶段都执行一遍（从最开始） 顺便在每个阶段上执行相应的插件目标

    一个阶段上可以绑定若干个目标，执行的顺序取决于你声明的顺序
*/
```

## idea快捷键

```java
/*
    缩写
        psvm
        sout
        soutv
        fori

    万用键 - alt+enter

    search everywhere - 双shift

    查看定义 declaration - ctrl+E（click）

    导航键 navigate - back/forward - ctrl+alt+左右

    查看文件 navigate - file   -    

    ⾼级查找：Find in Path 

    快速⽣成：Generate 

    格式化：Reformat Code 

    优化导⼊语句：Optimize imports

    谁调⽤了这个⽅法：Call Hierarchy 

    所有的实现类：Implementation 

    ⽂件⼤纲：File Structure 

    下⼀处错误：Next Highlighted Error 

    ⾼级重命名（all）：Rename 

    调试器快捷键：F5/F6/F7/F8
*/
```

## git相关操作

```java
/*
    查找背锅侠：Annotate/Blame 
    查看当前⽂件的历史版本 
    ⾼级筛选⽅式查找commit记录 
    显示差异：show diff 
    Open in GitHub
*/
```

## 调试器


    bug 虫子
    debug 除虫
    debugger 调试器

    理解程序执行过程
    理解JVM内部构造
    非常方便检查任何时间点JVM的内部状态

    在任何你需要调试的时间都可以把它变为调试模式

    条件断点

    点一个断点 再debug后 程序会全速运行到该断点

    step over 执行一行
    step into 执行语句 可跟踪到最精细的语句执行
    step out

    JVM 
        堆heap 所有对象都再堆中分配
        栈 线程（方法栈，后进先出，main方法在最底部，一条线程对应一个方法栈，随后出栈 方法被销毁[栈帧 stack frame，一个栈帧被销毁后里面的局部变量即被销毁]，移交控制权）

    跳转到源代码





# java程序基本结构

## 跨平台性、字节码


    强类型，静态编译语言
    
        在内存中的每一块数据都要和一种类型相绑定

        把java code转换为byte code的过程为编译compile，在compile过程任何的错误都会被检查出来，过不了这一关java code就不能变为byte code，就不能在各个平台上运行
        编译器为我们提供最大的安全保障



    跨平台性

        操作系统
        
            软件和硬件打交道的一个中介，机器码对换的桥梁


        不同操作系统由不同的语言，开发一个软件想让不同的操作系统看懂（需要用多个操作系统的语言去编写）


        想让软件和不同的操作系统对话

            方式一：用不同操作系统的语言开发软件和它交互

        or

        JVM 虚拟机

            提供一些外部接口，在操作系统提供API（对话的一种语言，一种编程接口，每个操作系统有自己的语言API），JVM提供另外一种接口 所有人只需要实现这一层接口 JVM会帮你去和操作系统的接口打交道
            （在不同的国家找到懂英语的人，现在只需写一本书，交给JVM，JVM看懂后 告诉不同国家的人怎么做）

            要实现跨平台的性能，只需开发一种中间层的专用语言（English），让JVM把他翻译成对应的API调用就可以

            称中间的语言为bytecode（字节码）



        字节

            计算机中操作一个元素or内存的最小单位（八个框框，00000000 - 00000001）

        字节码

            java为了实现跨平台性，在每个平台上实现JVM，为JVM开发一种统一标准化语言 字节码（由一个一个字节组成）


        绝大多数服务器运行的是Linux操作系统（在widows上开发，写完代码，拿到Linux的服务器上运行 可以没有障碍的运行，因为java提供JVM 中间层的虚拟）


## 基本单元 类、基本结构 包


    类的类名和文件名相同，不同的包下面可以有同名的类，包的结构和目录的结构完全对应

    类
        类名和文件名相同
        java最基本结构， 每个类都处在一个包中（包是什么取决于类所在的目录结构）

    包

        
        类的名字是个简单字符串，为了避免重名 用包来区分它
        
        防止一些有异议的单词，在同一个JVM中运行的时候怎么去避免冲突

        区分同名，但不同类

    


    

    在JVM中没有类这个东西，有的是权限定类名（full qualified name）

    JVM所做的一切工作被设计成 按照类的名字去寻找这个类 然后执行类中的代码

public class com.github.hcsp.home{//在JVM虚拟机看来程序中只存在这种长的名字,防止命名冲突
    //JVM允许在不引起歧义的情况 通过先import 再写简单的，但JVM按照完整的去理解它
    com.github.hcsp.pet1.Cat cat1;
    com.github.hcsp.pet2.Cat cat2;
}



引用第三方包


    必须告JVM它类在哪里能找到
    JVM只会按照程序中的东西去找相关的类

    把类的依赖库放到项目中

    用java.lang下面的东西都可以不import直接使用


## 方法、static


    局部变量 作用域局限于包围它的第一对 {} 被看到 被访问


## 对象、构造器、成员变量


    不引起歧义的情况下可省略this

    空指针异常

        if（x == null）
        
        通过if判断把空指针的情况规避掉

public class Cat{
    private String name;//成员变量 和对象相绑定，静态成员变量则不和任何对象相绑定
}



        静态变量虽然不和任何的对象（实例）绑定，在类外部访问时需用类名去限制它

        可以直接被访问，调用，全局共享的变量、方法

    实例方法、成员变量

        和对象紧密绑定在一起的一块内存单元 存储空间
    
    无论多么复杂的Java代码都是通过六个基本结构组成的


## 对象和引用


    引用就是地址 地址就是引用（reference）

    内存

        具体表现就是电脑里安装的一块内存条

        JVM占据一块内存存储各种各样的东西

        java中所有的对象都是地址
        


```java
//所有对象都是地址
package com.javade.pe1;

public class Cat {
    public String name;
}
```

```java
package com.javade.pe1;

public class Home {
    Cat cat;
}
```

```java
package com.javade.pe1;

public class Copy {
    public static Home deepCopy(Home home){//deep
        //在内存中，先是动态分配了Home的对象 其内含cat，newhome本身只是存放了其地址
        //再动态分配Cat的对象 newCat存放其地址
        //Home对象中含cat，把newCat赋值给它后，Home中的cat即存放了Cat对象 即其指向了Cat对象
        //Cat对象中含name，其也是存放String的地址，newCat.name=“www” 即把字符串的地址赋值给name
        //即形成链，Home - Cat - name
        Home newHome = new Home();//只存放了个地址指向庞大无比内存空间的具体数据
        Cat newCat = new Cat();
        String newName = null;
        newHome.cat = newCat;//地址的赋值
        newCat.name = newName;
        return newHome;
    }

    public static void main(String[] args) {
        Home home = new Home();//home只是个对象，里面有cat变量
        Cat cat = new Cat();
        cat.name = "wwww";//wwww 在内存中占据一定的空间，它有个地址
        deepCopy(home);
    }
}
```

## 传值和传引用

```java
/*
    java中含两种数据类型



        原生数据类型

            int，double...


            int i = 100；

                在内存中开创一块单元存放100这个数据，这个数据就是变量本身
        
                声明这个变量就是数据本身


        找到对应的类就算引用数据类型

        引用数据类型（对象）

            Stirng

            Cat C = new Cat();

                声明这个变量只是地址，这个地址指向数据本身

*/
class Cat{
    public String name;
}
class A{
    public static void addOne(int i){
        i+=1;
    }
    public static void renameCat(Cat cat){
        cat.name = "www";
    }
    public static void main(String[] args){//main是整个java的入口，在main调用之前是什么都没有的，每次调用一个方法的时候 java都会在内存中的某个地方为它提供全新的执行环境
    //同样是重新开辟了一块存储空间，由于一个数据就是变量本身，一个变量只是地址
    //传值
        //调用main方法时，内存中会为main分配Main.main空间，i在其内
        //调用addOne方法是，内存中会另外为addOne方法分配空间，i只是把值传给addOne中的i
        int i = 0;
        addOne(i);


    //传引用
        //若如此，在main中的cat只是存放了cat对象的地址，内存为cat对象分配的空间不在main中
        //即 renameCat中接受的也只是cat对象的地址
        //只是把地址复制过去，真正的数据是共享同一份
        Cat cat = new Cat();
        renameCat(cat);
    }
}
```

# 数据类型

## 数据在内存中如何存储

```java
/*
    在计算机中 所有的数据都是以字节的形式存储，二进制

    类型不同以不同的方式去表示

    字节

        最小单位

        字节即一个格子，其分成8个小格子

    ASCII

        最常用的字符的对照表

        如字符”今“

            在内存中 有一个内存单元以二进制的形式存储了20170这个数字

            但我们看到这个内存数据的时候，把它解释成 汉字字符 今
*/
class A{
    private int i = 1;//在内存中某个地方开辟出4个byte _ _ _ _(00000001)
    i+=1;//_ _ _ _(00000010)
}
/*
如String i="www";
在内存中分配两块空间
一块存储字符串www（此块内存本质为二进制数，依照字符对应的ASCII码值为对应的二进制数）
另外一块仅存储 存储字符串数据的内存空间的地址
*/
```

## 数据类型

```java
/*
    原生数据类型

        byte （8bit，最高位是符号位）_(0) _ _ _ _ _ _ _

            -127 —— 128
        
        int

            21亿

        float、double
        
            浮点数代表小数在计算机中的近似的表示

            浮点数只能比较大小不能比较相等    
*/
float i;
        if(Math.abs(i-0.0) < 0.000001){
            //i和0相等
        }


/*
    字面量

        long number = 1L;
        float number = 1f;
        double number = 1d;
        0x
        0b100110;//java7之后才有

        表示类型
*/



public class Copy {
    public static void main(String[] args) {
        byte i = Byte.MAX_VALUE;
        System.out.println("i = " + i);
        i = (byte) (1+i);//溢出，强行超过它的范围后就到头重来
        System.out.println("i = " + i);
    }
}
```

## 类型转换、类型提升

```java
/*
    低精度转换为高精度直接转换（字节少——多）
    int j;
    byte i=（byte）i;//强制转换 损失一定的数据

    int / int 结果还是整数（经过了截断
    
    若类型不同，需要把所有的值都提升到最高的精度 进行计算，最后的结果也是最高的精度


    字符进行运算的时候，完全等价于它对应的ASCII

        char a = '1';//等价于char a = 49



    char i = '1';
    i = i+1;//error int占4个字节 高于char，转换为int类型，i又是char类型，故错误
    i = (char)(i+1);//1在内存中的实际表示是数字49，加以为50

    int、 String、void  在JVM中都有对应的内存表示
*/
```

## 基本数据类型对应的装箱类型


    Integer i = 5;//Integer i = new Integer(5)


    任何一个原生数据类型都有和它对应的装箱类型

        int i=100;//100这个数据就按照二进制存储在i的4个byte中

    区别是不是对象看有没有和它对应的类

    自动装箱、自动拆箱

        需要一个int的时候可以丢给它一个Interger
        需要一个Integer可以丢给它一个int

        会自动


        int i = 100;
        Integer integer = i;//Integer integer = new Integer(i)
        list<Integer> list = new ArrayList<>();//容器类不接受原生数据类型
        list.add(1);

        boolean 只能有两种状态
        Boolean 可以有三种状态

        String i="123"

            内存中分配3个byte，第一个byte依照字符1对应的ASCII 以二进制存储数据

        int i = 123;

            内存中分配4个byte，依照123对应的二进制存储


        当需要一个int的时候 总可以用Integer类型去赋值给它（会自动完成装箱、拆箱）

        Integer i = null;
        int a = i;//若为null，对null拆箱会造成空指针异常


## null 、 equals

```java
/*
    int i = 1;//在内存中分配4ge连续的byte，以1对应的二进制数 存储数据1
    int j = 1;
    if(i==j){}

    Integer i = 1;Integer i = new Integer(1)
    Integer j = 1;//在内存中分配两块空间，j仅存储地址
    if(i==j){}


    ==

        运算符，比较二者是否相同

    equals()

        i和j指向的对象中的数据是不是相等

    Integer i = 1;
    Integer j = 1;
    if(i==j){//true

    }


    Integer c = 1;//Integer本身是不可变的
    c = c + 1;//c本身的数据没有改变，创建了一个新的对象
*/
```


# 运算系统

基本运算符

    同与同为同


# 控制流

```java
/*

*/
```