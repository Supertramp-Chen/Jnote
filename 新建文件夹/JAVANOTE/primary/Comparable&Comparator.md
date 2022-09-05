# Comparable 内部比较器

    Comparable排序接口，若一个类实现了Comparable 说明他支持排序

    实现了Comparable接口的类的对象 数组or列表 可通过Collections.sort或Arrays.sort进行自动排序


    该接口只有一个方法

    约定，比较此对象与指定对象的顺序

        如果是以自然顺序排序（从小到大）

            当 a<b 返回 负数
                >       正数
                =       0

        想从大到小排 则把约定反过来


    Predicate
        给定一个元素返回Boolean


    comparaTo方法

        a.comparaTo(b); // a - b

    需要修改源码


[题目](https://github.com/hcsp/sort-by-multiple-fields/pull/240)
```java
//按照其约定
//先排x 再排y
public int compareTo(Point o) {
        if (x < o.x) {
            return -1;
        }
        else if (x > o.x) {
            return 1;
        }
        else if (y < o.y) {
            return -1;
        }
        else if (y > o.y) {
            return 1;
        }
        else {
            return 0;
        }
    }
```

# Comparator 外部比较器