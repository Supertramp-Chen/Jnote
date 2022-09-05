# java特点

        没有内存管理的问题
        不释放导致内存泄漏，即内存越用越少
        java中会自动释放垃圾内存

        跨平台
            在A机器上编译运行的代码可直接转到B机器上，且结果一样



        用户写出一个高级语言程序，通过编译器转化成一个可执行程序，在操作系统的控制下由硬件来执行 



## 注释

    //
    /**/
    /** */ 将注解变为说明文档

## 标识符

    变量名

## 数据类型

    基本数据类型

        数值型

            一个常量整数默认为int类型，数字过大 必须在末尾加L 否则报错

            实数默认为double类型，若希望为float类型 则末尾加f（F）
            double不可赋给float

        字符型
        布尔型
    


    引用数据类型

        类
        接口
        数组




    输出控制符

    没有%ld %lf，float double 皆%f







    字符常量

        java中字符and字符串用Unicode编码表示，Unicode编码中一个字符占两个字节(一个字节放不下，一个字节存放的范围无法把世界上通用的字符放进去)

        'a' -> 97

        '/u0030' Unicode编码下0030对应的字符

        
        不同类型变量占几个字节是固定的（跨平台）





    数据类型的转换



        低的，小字节可转换为高的

        高转换为低会导致丢失数据

        ```java
            int i=1;
            byte b=10;
            b=(byte)i;//强制类型转换，此处没有改变i 只是转换出了一个临时的值赋给b
        ```


## 运算符

    算数运算符+

        数值相加

        字符串的连接 "123"+"abc"    "123abc"

        非字符串转换为字符串 "x"+123    "x123"



        'a'+1 //非字符串和1相加 就把两个值加起来
        ""+'a'+1


## 位运算符





# 面向对象三大特点，封装 继承 多态

# 面向过程思想

        自顶而下的设计模式

        先写个main方法，把程序分为三步，每一步用一个函数实现，如果某一步复杂再分解

        以算法为核心，这个问题怎么解决，必须一步步事先知道，用函数一步步设计出来

        把大问题化解为若干个小问题求解

        函数是划分程序的基本单位，函数是面向过程的思想，每一个步骤最终用一个函数去代替


     优点

        符合人类思想

     缺点

        先定义好变量，然后单独定义好函数，两个是分开的，函数不一定是为这个变量单独而设计的，数据也不一定要通过这个函数操作，可以直接操作 安全性低，数据和函数严格讲是一个整体，但在面向过程里是分开的

        程序是否正确 最终依赖于最下面的子函数的实现，依赖于实现细节，一个有问题很可能导致整个程序崩溃

        现实中的问题很难一开始就知道它是分几步解决





# 面向对象思想

        一个问题可能很复杂，解决这个问题

        先把这个问题的一个个部分模拟出来，整个问题也是由这一个个部分和部分之间的关系组成

        现实世界的问题无论多么复杂也是由个体和个体间的关系组成

        把个体模拟出来，最终整个问题也可以解决




    面向对象能更好的模拟现实

    任何一个事物都可以通过两个方面确定

        静态的一些属性
        动态的可执行的操作


    ```c++
    /*
    C中数据和数据的操作是分离的，没有有机的组合在一起
    如此导致可以任意修改abc的值，且能把任意垃圾数据发送给函数
    但是在JAVA中，ZC这个函数只能被三角形这个事物调用
    */
    #include<stdio.h>
    int ZC(int m,int n,int k);
    int main(){
        int a=3;
        int b=3;
        int c=3;
        printf("%d",ZC(a1,b1,c1));
    }
    int ZC(int m,int n,int k){
        return m+n+k;
    }
    ```




    ```c++
        struct Triangle{//C中的结构体只允许有属性 不允许有操作
            int id;
            char sex;
            float score;
        }
    ```

    ```java
        //构造出模型，但没有创建出事物
        class Triangle{//class类似C中struct，但其有事物可执行的操作
            int a;
            int b;
            int c;

            int ZC(){//该函数可直接访问a b c变量，因为函数和属性是一个有机整体
                return a+b+c;
            }
            void sleep(){

            }
        }

        //依据模型创建事物
        public class A{
            public static void main(String[] args){
                /*
                int * p = (int *)malloc(sizeof(int));
                A * q = (A*)malloc(sizeof(A));//怎么生成一个A事物，通过malloc这个函数分配A这种类型所占的字节数，再把它的地址发给q，通过q就能找到A这个事物
                */
                Triangle s = new Triangle();//Triangle * a = (Triangle *)malloc(sizeof(Trianlge)) ,左静右动
                s.a = 3;
                s.b = 3;
                s.c = 3;
                System.out.printf("%d",s.ZC());//大工具里套了个小工具，小工具里套了个函数，实际上本身是个类 类里面的一个属性 属性本身是个对象 里面又套用方法
            }
        }

    ```

# 类和对象


    类

        模型，把一类事物相同的静态属性和动态可执行的操作组合在一起的一个概念

        抽象的，可模拟一类事物（现实中存在也可，可只存在于我们的大脑）



    对象

        用类这个模型造出的具体的事物


    类如果是汽车的设计图，一辆辆真正的汽车就是对象




# 内存分配问题


    很多程序的语法最终最核心的问题

        是否分配内存

        内存怎么分配

        内存怎么释放

        通过什么方式可以使用这块内存





    内存本质上就是线性的一维空间，但是我们需要把内存模拟出不同的区域 把不同的区域当作不同的东西来使用

    无论是堆内存还是栈内存 本质上都是同一个物理意义上的内存，只不过把它单独模拟出来

    ```java
    class A{
        int i;//静态分配的，i就代表事物本身，动态分配不可能之间代表它，是把其地址赋给一个变量 通过变量代表它
        int j;
    }
    class Test{
        public static void main(String[] args){
            A aa = new A();
                //new A()在堆中动态分配一块区域，被当作A对象
                //aa本身的内存是在栈中分配的
                //堆中内存的地址赋给了aa
                //aa指向堆中的内存，aa代表堆中的内存
                //c语言中(*aa).i , JAVA中aa.i
                //aa.i代表aa这个静态指针变量所指向的动态内存中的A对象的i个这个成员
                //aa本身没有i这个成员，aa本身只存放了地址 只占4个字节，保存第一个字节的地址
        }
    }
    ```


# 程序执行过程


    程序本来是在硬盘上的，CPU不能之间访问硬盘上的程序，先把A.java这个程序通过操作系统放到内存上
    操作系统会对A.java进行分析解读，最终把代码至少划分为4个区域

        heap（new出来的东西）可跨函数使用
        stack（局部变量）不可跨函数使用
        data segment（静态变量，字符串常量）
        code segment（操作）

        java中heap区动态分配的内存不需要程序员手动释放，其会自动释放

# 访问控制符

    黑匣子，把事物内部的很多复杂的东西屏蔽掉，只提供一些按钮，通过按钮进行操作（如电视机 遥控器的开机 关机 换台 按钮）

    对于类中的属性，通过类提供的按钮进行操作

    在类数据成员前面加上一些访问控制符，对数据进行保护



    public

    protected

    private


    在一个类的内部，访问控制符的透明的，访问控制符是针对类外部访问而言的


# 构造函数

    定义的同时对它赋值or定义的同时已经有了确切的值

    构造函数：构造这个事物的时候被调用 自动执行

    若自己定义了构造函数 则不默认提供无参的构造函数


    如果是一个局部变量，没有对他赋值 则是垃圾值，不初始化不能使用
    一个对象创建时 会对其中各种类型的成员变量自动进行初始化，数值型为0 boolean为false


# 函数的重载

    几个函数的功能类型 
    
    统一可以用一样的名字 
    
    函数形参列表不一样（个数 数据类型 顺序）
    
    若只是返回值不一样 其他一样 则不行
    
    通过实参列表确定出具体调用哪个函数


# this指针

```java
    /*
    类只对他的属性分配空间，n个对象共用一个方法
    aa1和aa2共用一个show方法，如何知道哪个是哪个
    哪一个对象调用show方法，他会把对象的地址赋给this指针 
    this代表当前正在调用show方法的对象
    */
    public class A{
        private int i;
        public A(int i){
            this.i=i;//this代表当前时刻正在创建的对象
        }
        //非静的方法中有this指针
        public void show(){//A*this
            System.out.printf("i=%d",this.i);//(*this).i
        }
    }
    public class Test{
        public static void main(String[] args){
            A aa1=new AA(10);
            A aa2=new AA(20);
            aa1.show();//aa1
        }
    } 

```
    


# static

```java
/*
某一个属性前加static意味该属性就不是某一个对象的了，n个对象共用同一个属性i
static属性i属于类本身，没有对象 可以通过类名的方式直接访问类内部的static属性or方法，也属于类对象
静不能访问非静，非静可以访问静
*/
class A {
    private static int i = 10;
    public static int j = 100;

    public A() {
    }

    public A(int i) {
        this.i = i;
    }

    public void show() {
        System.out.printf("%d\n", this.i);
    }
    public static void show1() {
        System.out.printf("此为静态方法\n");
    }
    public void show2(){
        show1();
    }
}
public class Test{
    public static void main(String[] args){
        A aa1=new A(20);
        A aa2=new A();
        aa1.show();
        aa2.show();
        System.out.printf("%d\n",A.j);
        System.out.printf("%d\n",aa1.j);
        A.show1();
        aa1.show2();
    }
}
```

## 统计一个类前前后后造出了多少个对象

```java
/*
    通过static 统计一个类前前后后造出了多少个对象
 */

class A{
    private int i;
    private static int sum=0;
    public A(){
        sum+=1;
    }
    public A(int i){
        this.i=i;
        ++sum;
    }
    public static int show(){
        return sum;
    }
}
class Test{
    public static void main(String[] args){
        A aa1=new A();
        A aa2=new A();
        A aa3=new A();
        A aa4=new A();
        A aa5=new A();
        A aa6=new A();
        System.out.printf("该类共创建了%d个对象",A.show());
    }
}
```

## 使得一个类只能创建一个对象
```java
/*
使得一个类只能创建一个对象
类里面的属性既可以是个普通的变量也可以是个对象
 */
class A{
    private int i=99;
    private static A aa=new A();//在类内部，private是透明的
    private A(){}//加private使得不能以new方式创建对象
    public static A getAa(){//因为不能new方式创建对象，所以需加static
        return aa;
    }
}
class Test{
    public static void main(String[] args){
        A aa1=A.getAa();
        A aa2=A.getAa();
        if(aa1==aa2)
            System.out.printf("一个类只能创建一个对象");
    }
}

```



# 继承

    extends

    私有成员无法被继承

    物理上已经被继承过来，但逻辑上程序员不能去访问它 因此继承需慎重，否则会浪费内存

    通过子类对象名只能访问从父类继承过来的非私 内and外




    继承的原则

        b是一个a吗，是则让b为a的子类    

        java中的继承反映的是现实中一般到特殊 具体的关系


    java只支持单继承

        一个类只能有一个父类


    

    子类访问父类成员的三种方式

        在子类内部访问

        子类对象名方式访问

        子类类名方式访问


## super

```java
/*
父类的构造函数无法被继承
一个类里面一定会有构造函数（不写默认）
创建对象一定会调用构造方法，调一个
 */
class A{
    private int i;
    public A(int i){
        this.i = i;
    }
}
class B  extends A{
    private int j;
    public B(int i,int j){
        //每一个子类构造方法的第一条语句 都是隐含的调用super()
        //super放第一条
        super(i);
        this.j = j;
    }
}
class Test{
    public static void main(String[] args){

    }
}
```


# 重写父类方法 

```java
/*
不能说方法的重写，我们从A里面继承了A类的方法 然后又重新定义了自己的方法，两个方法同名 同参 同返回值 只是函数体不一样（B有两个，可以解释为什么B类中若返回值不一样则报错）

在重写，super.父类方法 可调用父类的没有被重写的方法
为保证多态在任何情况下都可实现
重写的时候权限不能过低
子类中不允许出现和父类方法 同名同参不同返回值的函数（函数重载问题 子类有两个函数 一个继承而来 一个自己添加定义 会不知道要调哪个函数）
 */
class Human{
    private String name;
    private int age;
    public Human(){}
    public Human(String name,int age){
        this.name=name;
        this.age=age;
    }
    public void setName(String name){
        this.name=name;
    }
    public void setAge(int age){
        this.age=age;
    }
    public String getInfor(){
        return age + "," + name;
    }
}
class Student extends Human{
    private String school;
    public Student(){}
    public Student(String name,int age,String school){
        super(name, age);
        this.school=school;
    }
    public void setSchool(String school){
        this.school=school;
    }
    public String getInfor(){
        return super.getInfor() + "," + school;
    }
}
public class Test {
    public static void main(String[] args){
        Student aa = new Student("ww",12,"qq");
        System.out.printf(aa.getInfor());
    }
}
```


# 多态

```java
/*
子类对象可以直接赋给父类引用
父类对象在任何情况下都不能赋给子类引用（只有在父类引用已经指向一个子类对象时，可通过强制类型转换 把父类引用转换为子类引用）

多态：
    如果把子类的引用赋值给父类的引用，这时候通过父类的引用调用方法 变成调用子类的方法  
    
    有一个刺激，不同的对象对这个刺激有不同的反映（上课铃声响起时，不同班级的同学去往不同的班级）

    通过父类的引用只能调用子类从父类继承过来的成员，不能调用子类特有的
 */
class A{
    public void f(){
        System.out.printf("AAAA\n");
    }
}
class B extends A{
    public void f(){
        System.out.printf("BBBB\n");
    }
    public void g(){//但aa不能调用子类特有的方法
        System.out.printf("GGG\n");
    }
}
class Test{
    public static void main(String[] args){
        A aa = new A();
        B bb = new B();
        aa.f();
        aa=bb;//子类可以当父类看，但父类不能当子类看
        //同样一行代码做不同的事情
        //父类的引用根据当前指向的是父类的还是子类的 自动调用其方法
        aa.f();//等价于C中(*aa).f
    }
}
```

## eg

```java
/*
无论当前时刻有多少子类对象，都可以把他们全部输出（代码不需要改变）
之后若把类族进行扩充，代码照样不需要改变
 */
class A{
    public void f(){
        System.out.println("AAAA");
    }
}
class B extends A{
    public void f(){
        System.out.println("BBB");
    }
}
class C extends B{
    public void f(){
        System.out.println("CCCC");
    }
}
class Test{
    public static void g(A aa){//在一个类的某个方法内部定义的形参，只能在本类的方法内生效
        aa.f();
    }

    public static void main(String[] args) {
        A a = new A();
        B b = new B();
        C c = new C();
        g(a);
        g(b);
        g(c);
    }
}
```

```java
/*
如何把一个父类的引用转换为子类的引用
即实现 bb=aa
使得通过父类的引用可以调用子类特有的方法
 */
/*
double x = 6.666;
int i = (int)x;//如此x的值没有改变，只是产生了个临时值赋给i
 */
class A{
    public void f(){
        System.out.println("AAA");
    }
}
class B extends A{
    public void f() {
        System.out.println("BBB");
    }
    public void g(){
        System.out.println("GGG");
    }
}
class Test{
    public static void main(String[] args) {
        A aa = new A();
        B bb = new B();
        //bb=(B)aa;//编译没错，运行出错，aa本身指向的是父类的对象
        A aa2 = new B();
        bb=(B)aa2;//aa2已经指向子类对象
        ((B) aa2).g();//使得通过父类的引用可以调用子类特有的方法
        bb.g();
    }
}
```

# 抽象类、final

```java
/*
抽象类作为一个类族最顶层的父类，用最顶层的类表示该类族所有事物的共性，最底层的类表示现实中的具体事物
把满足事物的特点都用方法来实现，具体如何实现不用管，下面进行逐步的分解 最后变成一个有实际意义的实际类的时候再进行实现
 */
//有抽象方法的类一定是抽象类
abstract class A{
    abstract public void f();//没有方法体的方法为抽象方法，末尾加分号，前加abstract
}
//抽象类不一定有抽象方法
abstract class Aa{
    public void g(){

    }
}
class B extends A{
    public void f(){
        System.out.println("BBB");
    }
}
class Test{
    public static void main(String[] args) {
        //可以定义一个抽象类的引用，但不能定义一个抽象类的对象
        //抽象类实现多态
        A aa;
        //A aa = new A();
        A aa2=new B();
        aa2.f();
    }
}
```

```java
final class A{//final修饰类，该类不能被继承
    //定义时赋值
    final public int i=9;//final修饰属性，该属性必须被赋值，且只能被赋一次值
//    public f(){//error
//        i=0;
//    }
    //构造函数赋值
    final public int j;
    public A(){
        j=0;
    }
    final public void f(){//final修饰方法，该方法可以被继承，但不能被重写
        System.out.println("AAA");
    }
}
class B {
    final public void f(){//final修饰方法，该方法可以被继承，但不能被重写
        System.out.println("BBB");
    }
}
//class C extends B{
//    public void f(){
//        System.out.println("CCC");
//    }
//}

```

# 接口



# 异常

# ToString()

# equals

# String类

# printf、println

# 数组

# 线程

# 字节流

# 缓冲流

# 泛型