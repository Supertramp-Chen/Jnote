# Collection

## Collection的体系结构

    
[集合框架体系图,collection在继承链的位置](../png/集合框架.png)


    collection 这个接口代表一组东西

    Map是两种


    <> 泛型
    
        List<Integer>

            加了一个泛型，表面List的类型是Integer 声明新的类型


## List


    List 有顺序、有序的一个一个的元素


    
    最常⽤的ArrayList

        本质上就是⼀个数组


    List如何实现动态扩容

        创建⼀个更⼤的空间，然后把原先的所有元素拷⻉过去


```java
    
    Collection<Integer> c = new LinkedHashSet();
    List<Integer> list = new ArrayList<>(c);
    //等价于
    List<Integer> list2 = new ArrayList<>();
    list2.addAll(c);
    //等价于
    List<Integer> list3 = new ArrayList<>();
    for (Integer i : c) {
        list3.add(i);
    }

```


# Set

    无序，不能包含重复元素

```java
//用hashset对list去重
List<Integer> list = new ArrayList<>();
        list.add(2);
        list.add(3);
        list.add(3);
        list.add(3);

        Set<Integer> set = new HashSet<>(list);
```



    判断重复：equals⽅法



## java世界⾥第⼆重要的约定：hashCode

        判断一个object是不是重复的

            类似于百家姓查找，查找效率提高

[示意图](png/hashcode.png)


            先把它映射成一个int值，把他均匀分布到hash桶里面

            一个新的object有没有重复，算它的hashcode，去对应hashcode桶里面找（Object为all类的父类）

            哈希算法为一个单向映射（不能反过来） 对象出现的情况比整数多的多

[示意图](png/hashc.png)


        同⼀个对象 返回同 hashCode

        两个对象 equals返回true 则同 hashCode

        两个对象不等，也可能返回相同的hashCode(张三、张二)




# Map

    键不能重复，值可以重复（微信ID映射到微信名）


    keyset和map背后是同一组数据，一个变 另外一个也会变


key不能重复 即返回set
value可     即返回collection


```java
//entrySet分别打印键和值
for (Map.Entry<String, String> entry : map.entrySet()) {
    entry.getKey;
    entry.getValue
}

containsKey()/containsValue()
keySet()/values()/entrySet()
```


## HashMap

    hashmap的key的set就是hashset

    计算key的hashcode丢到对应的hash桶   
    把相同的hashcode的对象分到一个桶里

    

    HashMap的扩容

        怎么面对一个满了的hashmap

            创建一个更大的hashmap，把原先的东西copy过来


    HashMap的线程不安全性

        hashmap在多线程环境下扩容（重新调整大小）的时候有可能变成一个死循环的链表

        用ConcurrentHashMap

    HashMap在Java 7+后的改变：链表->红⿊树

        不同的对象因为hashcode相同被放在同一桶里面，hashmap就退化成了链表，性能恶化

        所以该情况下 链表变为红黑树

[示意图](png/set性能恶化.png)

    HashMap和HashSet本质上是⼀种东⻄

# 有序集合TreeSet/TreeMap

    HashSet LinkedHashSet TreeSet

[3 set区别示意图](png/3%20set.png)

    插入后发生一些特殊变化、翻转，使其顺序不变 左小右大




    使⽤Comparable约定，认为排序相等的元素相等


        如果一个对象实现comparable约定，就可以对它进行排序



[原理1](png/原理1.png)
[原理2](png/原理2.png)
[原理3](png/原理3.png)
[原理4](png/原理4.png)


    左小右大

    插入后发生一些特殊变化、翻转，使其顺序不变 左小右大



# Collections⼯具⽅法集合

    eg类为List 其方法存放在Lists类

    • emptySet(): 等返回⼀个⽅便的空集合
    • synchronizedCollection: 将⼀个集合变成线程安全的
    • unmodifiableCollection: 将⼀个集合变成不可变的（也可以
    使⽤Guava的Immutable）



# Collection的其他实现

• Queue/Deque
• Vector/Stack
• LinkedList
• ConcurrentHashMap
• PriorityQueue


# Guava

• 不要重复发明轮⼦！尽量使⽤经过实战检验的类库
• Lists/Sets/Maps
• ImmutableMap/ImmutableSet
• Multiset/Multimap
• BiMap