
    批量修改变量名    ctrl+shift+A

    查看一个类all方法 ctrl+Alt+F
    
    debug时快速标记某一行 ctrl+shift+P
    
    类的继承结构与关系图  ctrl+H


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

```java
//idea快捷键的使用
import java.util.*;

class user{
}
public class 快捷键使用 {
    public static void main(String[] args){
        //1、自动导包，自动删包 创建一个对象时 需要把对象所在的类导到我们的类当中(setting中)
        Map aa = new HashMap();//idea自动导入包，删除包

        //2、if的自动补全
        boolean flag = true;
        if (flag) {//flag.if

        }
        if (!flag) {//flag.else

        }
        //3、for/while循环
        for (int i = 0; i < ; i++) {//打fori

        }
        while (flag) {//flag.while

        }
        //4、var（更加方便去创建对象）
        user user = new user();//new出来个对象（）直接 .var
        //6、sout 输出
        System.out.println("hello world");//"hello world".sout
        System.out.println("hell");
        //7、try 异常
        try {
            int num = 10/0;//int num=10/0 直接 .try
        } catch (Exception e) {
            e.printStackTrace();
        }
        //8、List各种操作（其实就是遍历）
        List<Integer> list = Arrays.asList(1,2,4,5,6);
        for (Integer integer : list) {//直接list.for
            System.out.println(integer);
        }
        for (int i = 0; i < list.size(); i++) {//直接list.fori

        }
        for (int i = list.size() - 1; i >= 0; i--) {//方向输出 list.forr

        }
        //list使用迭代，获取它的迭代器
        Iterator<Integer> iterator = list.iterator();//list.iterator.var
        while (iterator.hasNext()) {//iterator.hasnext.while
            System.out.println(iterator.next());//.sout
        }
        //9、快速生成getSet方法，Alt+Insert/鼠标右键 Generate，按shift键可多选
        //10、psvm快速生成启动类
        //11、ctrl+D 复制该行代码至下一行
        //12、ctrl+Y 删除该行代码
        //13、多行注释 ：ctrl+/ 这个是多行代码 分行注释，每行一个注释符号
		//ctrl+shift+/ 这个是多行代码注释在一个块里，只在开头和结尾有注释符号
        //取消注释同理
    }
    public int text(){
        //5、return
        return 10;//打10.return
    }
}
``` 