# IOException

    在return的语句之外，为方法提供另外一个出口
    异常的抛出过程就是方法的另外一个出口

    IOException代表 预期之内的异常


    正常情况下从方法的入口开始执行直到return
    但在这个过程中可能碰到不计其数的异常情况

    如果没有try异常将击穿all栈帧
    这时候丢出一个异常的时候 
    会忽略throw下面的all代码，并且把这个异常顺着方法栈一直往上抛
    若没有方法抓住该异常 则一直抛 直到击穿all栈帧 , 线程则终止


```java
    try{
        b();//尝试做这样一件事情 看异常有没有发生，有才执行catch
    }
    catch{
        //处理异常
        //在log里打印异常
        //返回对应的对异常的处理
    }
    //无论什么情况下 finally都会执行
    finally{
        //执行资源的清理工作
    }
```


    JDK7+ : try - with - resources
    
        原来try不能独立存在
        try()声明在()里的东西会自动被close 可以这样的写的时候idea会提示


# throw/throws


    throw是个语句，声明自己要抛出一个异常，可以被丢出来的 throwable

    throws 只是有可能

        如在方法后声明throws Exception这样一个语句 
        声明可能会对此丢出一个Exception异常
        
        在其他方法中调用一个可能会丢出Exception异常的方法

            要么声明自己也可能丢出Exception异常

            要么try catch


# java的异常体系

方法后面声明

    Throwable 可以抛出的东西（有毒，任何调用它的方法都会被传染）

        Exception - checked execption（受检异常，有毒） 预料之内可能出现的异常IOException，能恢复的异常

            RuntimeException（运行时异常，五毒）意料之外的，出现则是bug，不应该出现的，不需要处理它 不需要声明

        Error（错误，五毒）不能恢复的异常



catch的级联和合并

    按照不同的类型处理
    根据抛出异常的具体类型做不同的处理  

```java
    //从小到大的顺序排,按照类的继承体系
    try{
        throwCheckedException();
    } catch (NullPointerException e){
        System.out.prinln("no found");
    } catch (RuntimeException e){
        System.out.prinln("文件到达末尾");
    } catch (Exception e){
        e.printStackTeace();
    } catch (Throwable t){

    }//同可合并
```


# Stacktrace



    栈轨迹（排查问题最重要的信息）
    异常链


```java
import java.sql.SQLException;

public class Main {
    public static void main(String[] args) throws Exception {
        aa();
    }

    private static void aa() throws Exception {
        processUserData();
    }
    private static class UserAlreadyExistException extends RuntimeException{
        public UserAlreadyExistException(String message,Throwable cause) {
            super(message, cause);
        }
    }
    private static void processUserData() throws Exception {
        Integer userId = 1;
        try {//tyr catch处理的时候在外面包了一层,多了一个cause by
            inserIntoDatabase();
        } catch (SQLException e){
            throw new UserAlreadyExistException("插入id为"+userId+"时出错",e);
        }
    }

    private static void inserIntoDatabase() throws Exception {
        throw new SQLException("重复的键值");
    }
}

```


# 异常的抛出原则

    能用if/else的不用异常

    尽早抛出异常（碰到异常的时候 必须决定也不要处理它 不能处理则要立刻抛出）

    异常要准确（准确表达正在发生的事情） 带有详细信息

    抛出异常比悄悄执行错误的逻辑强的多

# 异常的处理原则

    本方法是否有责任处理这个异常
        不要处理不归自己管的异常

    本方法是否有能力处理这个异常（无法处理就抛出）

    不是万分必要 不要忽略异常

# JDK内置异常