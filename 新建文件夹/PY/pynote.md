
print()

    数字可直接传入print后的括号内
    文本需用单引号or双引号括住(单双一样)

    每次使用print打印信息时，print都会在最后添加一个换行符


注释

    python使用 # 作为单行注释符号

每一句的代码占一行，代码通过缩进区分代码之间的层次



# for循环

    for 变量 in 集合:
        语句

    range函数的结果是一个整数列表
    range(a,b)会生成a至b-1这些数字，不包括b


    print("sum=%d"%(sum))


# 集合的概念和创建

    集合是python中的内置数据结构，一个无序的集，存储不重复的元素，基本的不可变的数据类型


    创建集合

    a = set()#创建空集合用set,若用{}则会默认创建字典
    b = {1,2,'qw'}

    print集合时 不会包括重复的元素，将重复函数归一化

    集合是无序的，不能用索引的方式访问，可用遍历的方式访问


    可把字符串 列表 元组 字典 转换为集合 
    d = 
    test = set(d)#字典转换为集合后，value会被忽略

    nums = {1,2,3}
    nums.add(4)
    nums.remove(1)



    集合之间可进行运算

    交 & a.intersection(b)
    并 | a.union(b)
    差 - a-b a.difference(b)
    


    编写程序求两个班级的重名学生



# 字典的创建和概念


    映射

        把不同的水果放在不同的箱子，水果和箱子就有了相互映射的关系
        映射即元素间的相互对应关系


    字典即表示这种映射关系的结构

    dict = {key1:value1,key2:value2}#左侧为字典名，key代表映射的键 value代表映射的值

    print(dict)
    print(dict[key])#单独访问字典中的某个key

    name = {}
    name = dict()

    在字典中添加键值对

        dictname[key] = value
        name[key] = value

        if 'key' in name:

    已知水果价格和购买水果数量，计算需要支付的总金额













































python 是解释形语言，开发中没有编译这个环节，写完后直接运行即可



# 标识符（怎么命名变量）

    标识符即是定义变量的名称

    字母 数字 下划线

    第一个字符不能是数字

    不能和保留字相同(python系统中有的)



# 注释

    # 单行

    """ """  ''' ''' 多行


# 六大数据类型

    Number数值类型(int float complex boolean)

        a = 3

    String字符串类型

        ""
        ''
        ''' '''


    List列表类型

        a = []
    
    Tuple元组类型

        a=()

    Set集合类型

        a={}

    Dict字典类型

        a = {'ww':99}


    可变：

        List[] Dict{} Set{} 

        可修改内容，地址不改变

    不可变：(地址会改变)

        String Number Tuple()



# 循环

    for i in range():


    for i in 'qwewqe'


    a = 3
    print("a=",a)



# 运算符

    // 整除

    /  带小数的除法

    %  取余

    ** 次方

    *  (若是字符串*2，写两遍字符串)


# 字符串

    定义

        "" '' ''''''

    截取

        a = "qwe"
        print(a[0:2])#不包括2

        print(a[:])

        print(a[:-1])

        print(a[::2])#2为长度

    连接

        +

        a.count("xx")#xx出现的次数

        a.startwith("n")#是否以n开头
        a.endwith("n")

        a.lower()#全转换为小写
        a.upper()#全转换为大写

        a.repalce("q","b")



# 列表

    a = []

    把其他类型转换为列表类型

    a = list()




    删除 

        del a
        a.remove()
        a.pop()#下标



    增加

        a.append()
        a.insert(2,"")
        a.extend(list2)


# 字典

    dic.get('键名')


    dic = {'w':'qw'}
    for i in dic：
        print(i)#默认为key

    for k,v in dic.items():
        print(k,v)


# 函数

    def fw(str):

        return 


    不可变类型(string,num,tuple)作为参数时，在该函数内修改该参数不改变原函数中该参数的值

    可变类型(list,dict,set)会改变


    lambda

    we = lambda arg : arg+1

