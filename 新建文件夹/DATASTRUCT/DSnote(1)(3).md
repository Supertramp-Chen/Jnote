# 数构

# 概述


  逻辑结构 即大脑里有该东西 用图能画出来即可 且不考虑计算机如何存储

      线性结构
      
          (数组，链表存储)
          
          栈和队列是特殊的线性结构
      
      
      非线性结构
          
          树
          图
          
          


          
  物理结构 如何把这种逻辑的东西保存到计算机里面


      如何在计算机里用直线形的内存来表示现实中的问题



  数据结构研究数据的存储问题（个体的存储 + 个体和个体之间关系的存储）

  算法研究数据的操作问题

  算法依附于存储数据的方式（不同的存储方式对它执行的操作也不一样）



  衡量算法的标准

  ​	时间复杂度：核心代码执行的次数


  数据存储就分两种结构

  ​	线性存储

  ​	非线性存储


# 线性结构

  ## 线性存储 

    ### 概述


      把所有节点（类似于数组元素，单独的事物、个体）用一根直线穿起来


      结构体变量不可以加减乘除 但可以相互赋值


      无论一个变量有多大，它的地址只用第一个字节的地址表示（占4个字节）


    ### typedef



      为已有的数据类型起个名字，两个等价 都可以用

      ```c++
      typedef int zhan;//为int多取个名字，int等价于zhan
      zhan i;//等价于int i
      typedef struct student{
          int i;
          string name[100];
      }ST;
      struct student aa;
      ST aa;
      typedef struct student{
          int i;
          string name[100];
      } * PST，ST;//PST等价于 struct student * 类型，s到*整体是个类型，ST等价于struct student
      ```

    ### 数组

      pArr -> pBase //表示pArr这个结构体变量所指向的结构体中的pBase这个成员

      pArr -> pBase = （int *）malloc(seizeof(int) * length)//分配了多个字节，把第一个字节的地址分配给pBase，pBase是整型 正好指向前4个字节，pBase指向第一个元素 pBase+1指向第二个元素


      ```c++
      #include <stdio.h>
      #include <stdlib.h>
      #include <malloc.h>
      struct Arr{
        int * pBase;
        int len;
        int cnt;
      }*PST,ST;
      void init_arr();
      bool is_full();
      bool is_empty();
      bool append_arr();
      bool insert_arr();
      bool delete_arr();
      void sort_arr();
      void show_arr();
      void inversion();
      int main(void){
        int devalue;
        struct Arr arr;
        init_arr(&arr,10);
        append_arr(&arr,1);
        append_arr(&arr,2);
        append_arr(&arr,3);
        append_arr(&arr,4);
        show_arr(&arr);
        insert_arr(&arr,1,123);
        show_arr(&arr);
        delete_arr(&arr,2,&devalue);
        show_arr(&arr);
        inversion(&arr);
        show_arr(&arr);
        sort_arr(&arr);
        show_arr(&arr);
      }
      void init_arr(struct Arr * array,int length){//初始化
        array->pBase = (int *)malloc(sizeof(int) * length);
        array->len = length;
        array->cnt = 0;
      }
      bool append_arr(struct Arr * array,int value){//在数组末尾添加元素
        if (is_full(array))//先判断数组是否满了
          return false;
        else{
          array->pBase[array->cnt] = value;
          array->cnt ++;//数组有效长度需加1
          printf("successful append\n");
          return true;
        }
      }
      bool insert_arr(struct Arr * array,int pos,int value){//在数组红任意位置的后面插入元素，一次only插入一个
        if ( is_full(array) )//先判断数组是否满了
          return false;
        while (pos>0 & pos<=array->cnt){//限定元素插入的位置
          for (int i=array->cnt-1;i>pos-1;i--){//插入之前先进行插入位置之后的元素集体后移一位
          array->pBase[i+1] = array->pBase[i];
          }
          array->pBase[pos] = value;//插入元素赋值
          array->cnt ++;//数组有效值+1
          return true;
        }
      }
      bool delete_arr(struct Arr * array,int pos,int * devalue){//删除数组中任意位置的元素
        if ( is_empty(array) )//判断数组是否为空
          return false;
        if (pos<1 || pos>array->cnt)//限制删除数组元素的位置
          return false;
        *devalue = array->pBase[pos-1];//摘出删除的元素
        for (int i=pos-1;i<array->cnt-1;++i){//删除元素后面的数组元素集体前移一位
          array->pBase[i] = array->pBase[i+1];
        }
        array->pBase[array->cnt-1] = 0;//最后一位赋值0，可忽略，因为输出数组内容时在cnt截至
        array->cnt --;//数组有效长度-1
        printf("successful delete\nthe number you delete is %d\n",*devalue);
        return true;
      }
      bool is_full(struct Arr * array){//判断数组是否满了
        if (array->cnt == array->len)
          return true;
        else
          return false;
      }
      bool is_empty(struct Arr * array){//判断数组是否为空
        if (array->cnt == 0)
          return true;
        else
          return false;
      }
      void sort_arr(struct Arr * array){//失败，后补
        int t;
        for(int i=0;i<array->cnt-1;++i){
          if (array->pBase[i] > array->pBase[i+1]){
            t = array->pBase[i];
            array->pBase[i] = array->pBase[i+1];
            array->pBase[i+1] = t;
          }
        }
      }
      void show_arr(struct Arr * array){//输出数组内元素
        if (is_empty(array))//先判断数组是否为空
          exit(-1);
        else
          for (int i=0;i<array->cnt;++i){
            printf("%d ", array->pBase[i]);
          }
          printf("\n");
      }
      void inversion(struct Arr * array){//进行数组颠覆操作
        int t,i=0,j=array->cnt-1;
        while (i<j){//i<j 保证无论数组内元素个数是奇数还是偶数皆可
          t = array->pBase[i];
          array->pBase[i] = array->pBase[j];
          array->pBase[j] = t;
          ++i;
          --j;
        }
      }
      ```



  ## 离散存储



    离散 不连续的意思（某个点到某个点之间的间距是可以被计算出来的，若连续则无数）



   ### 链表


   #### 定义

    n个节点离散分配

    彼此通过指针相连

    每个节点只有一个前驱节点，每个节点只有一个后续节点

    首节点没有前驱节点，尾节点没有后续节点





    专业术语：

    ​	首节点：第一个有效节点（存放有效数据的节点）

    ​	尾节点：最后一个有效节点

    ​	头节点：

    ​		头节点数据类型和首节点类型一样

    ​		第一个有效节点之前的那个节点

    ​		头节点不存放有效数据

    ​		加头节点的目的为方便对链表的操作

    ​	头指针：指向头节点的指针变量

    ​	尾指针：指向尾节点的指针变量



   #### 通过函数处理链表 接受的参数



    首节点可以通过头节点找到，尾节点也可



    只需要头节点即可

    通过头指针可以推算出列表的其他所有信息




   #### 表示链表节点的数据类型


    结构体变量中的成员指向和该结构体变量数据类型一样的变量

    整体分两部分：数据域和 指针域（指向和它本身数据类型一样但是是另外一个节点）

    ```c++
    typedef struct Node{
        int date;//数据域
        struct struct Node * pNext;//指针域
    } Node,*PNode;
    ```


   #### 链表的分类



    单链表

    双链表：

    ​	每一个节点有两个指针域

    ​	左边指针域指向前面，右边指针域指向后面



    循环链表：

    ​	能通过任何一个节点找到其他所有节点

    ​	最后一个节点的指针域又指向前面的

    非循环链表



   #### 非单循环链表插入和删除节点



    有一个链表，一个指针p指向某个节点（前后可有），q指向另外 i 一个节点

    现需把q指向的节点插入到p指向的节点后面

    ```c++
    r=p->pNext;//先把p指向的节点后面的节点的地址保存
    p->pNext=q;//先使p指向的节点的指针域指向q
    q->pNext=r;//再使q指向的节点的指针域指向p指向的节点后面的节点

    q->pNext=p->pNext;//先使q指向的节点的指针域指向p指向的节点的后面的节点
    p->pNext=q;//再使p指向的节点指向q
    ```



    ```c++
    r=p->pNext;
    p->pNext=p->pNext->pNext;
    free(r);//删除r指向节点所占的内存 手动释放，不会导致内存泄露（only C and C++）
    ```





   #### 链表的操作



    算法：
      狭义的算法和数据的存储方式密切相关（狭义，从内部的真正实现上，本质）
      广义的算法和数据的存储方式无关  （外表）
      泛型：(一种假象，内部已经编好了)
        利用某种技术使得：不同的存储方式，执行的操作一样

      可以在一个函数分配内存，在另外一个函数去使用内存（跨函数调用内存问题）（only动态内存，函数调用完后静态的内存没了，动态的还有）

      

    ```c++
    #include <stdio.h>
    #include <malloc.h>
    #include <stdlib.h>
    typedef struct Node{
        int date;
        struct Node * pNext;
    }NODE,* PNODE;
    PNODE create_list();
    void traverse_list(PNODE pHead);
    bool is_empty(PNODE pHead);
    int length_list(PNODE pHead);
    void sort_list(PNODE pHead);
    bool insert_list(PNODE pHead,int pos,int val);
    bool delete_list(PNODE pHead,int pos);
    int main(void){
        PNODE pHead = create_list();
        traverse_list(pHead);
        sort_list(pHead);
        traverse_list(pHead);
        insert_list(pHead,3,20);
        traverse_list(pHead);
        delete_list(pHead,3);
        traverse_list(pHead);
        return 0;
    }
    PNODE create_list(){//返回头指针，创建头指针，指向链表尾节点的指针pTail，指向新节点的指针，通过pTail->pNext = PNew 创建链表
        int len,value;
        PNODE pHead = (PNODE)malloc(sizeof(NODE));//动态内存分配创建头指针
        if (pHead == NULL){//确保动态内存分配成功
            printf("fail");
            exit(-1);
        }
        PNODE pTail = pHead;//该指针指向链表最后一个节点
        pTail->pNext = NULL;
        printf("number is ");
        scanf("%d",&len);
        //PNODE pNew = (PNODE)malloc(sizeof(NODE));//若在循环外面进行动态内存分配pNew指针，则导致致循环结束始终只有一个pNew
        for (int i=0;i<len;++i){
            printf("number %d =",i+1);
            scanf("%d",&value);
            PNODE pNew = (PNODE)malloc(sizeof(NODE));//该指针指向新的节点
            if (pNew == NULL){//确保动态内存分配成
              printf("fail");
              exit(-1);
            }
            pNew->date = value;
            pTail->pNext = pNew;
            pTail = pNew;
            pTail->pNext = NULL;
        }
        return pHead;
    }
    void traverse_list(PNODE pHead){//创建一个始终指向链表尾节点的指针
        PNODE p = pHead->pNext;
        while(p != NULL){
            printf("%d ",p->date);
            p = p->pNext;
        }
        printf("\n");
    }
    bool is_empty(PNODE pHead){
        if(pHead->pNext = NULL)
            return true;
        else
            return false;
    }
    int length_list(PNODE pHead){//与travel函数实现类似
        int len=0;
        PNODE p = pHead->pNext;
        while(p != NULL){
            ++len;
            p = p->pNext;
        }
        return len;
    }
    void sort_list(PNODE pHead){
    /*
        数组中的排序
        for(i=0;i<len-1;++i){//把数组中的第一个元素和其后面所有元素依次进行比较，再拿第二个与后面依次进行比较，随之结束
            for(j=i+1;j<len;++j){//j变，i不变
                if(a[i]<a[j]){
                    t = a[i];
                    a[i] = a[j];
                    a[j] = t;
                }
            }
        {//链表和数组比，链表不连续，但都属于线性结构，内部不一样，但从逻辑上讲他们的算法一样
    */
        int i,j,t;
        PNODE ip,jp;
        int len = length_list(pHead);
        for(i=0,ip=pHead->pNext;i<len-1;++i,ip=ip->pNext){
            for(j=i+1,jp=ip->pNext;j<len;++j,jp=jp->pNext){
                if(ip->date > jp->date){
                    t = ip->date;
                    ip->date = jp->date;
                    jp->date = t;
                }
            }
        }
    }
    bool insert_list(PNODE pHead,int pos,int val){//在pos位置的后面插入值为val的元素
        int i=0;
        PNODE p = pHead;
        while(p!=NULL && i<pos){//确保pos的值不大于链表的有效节点数，且其余正常时使得i=pos，并且确保pos值的正常
            p = p->pNext;
            ++i;//使得p指向的有效节点为第i个有效节点
        }
        if (i>pos || p==NULL)//pos值大于链表有效节点数or pos值的正常性
            return false;
        PNODE pNew = (PNODE)malloc(sizeof(NODE));
        if (pNew == NULL){
            printf("fail");
            exit(-1);
        }
        pNew->date = val;
        pNew->pNext = p->pNext;//先让pos节点的后面的节点前面为要插入的节点
        p->pNext = pNew;
        /*先让pos节点的后面为要插入的节点
        PNODE t = p->pNext;
        p->pNext = pNew;
        pNew->pNext = t;
        */
        return true;
    }
    bool delete_list(PNODE pHead,int pos){//与insert函数方法类似
        int i=0;
        PNODE p = pHead;
        while(p!=NULL && i<pos-1){
        ++i;
        p = p->pNext;
        }
        if(p==NULL || i>pos-1)
            return false;
        PNODE t = p->pNext;
        p->pNext = p->pNext->pNext;
        free(t);
        t = NULL;
        return true;
    }
    ```



  ## 线性结构的应用


   ### 栈



    定义：

    ​	一种可以实现先进后出的存储结构

    ​	类似于箱子

    ​	先放进去的最后取出来



    分类：

    ​	静态栈

    ​	动态栈



    ​	内存可以分为静态内存（栈内分配，操作系统分配，压栈方式）和动态内存（堆内分配，手动分配，排序方式）

    ​	栈and堆表示分配数据的方式



    算法：

    ​	出栈	

    ​	入栈



    ```c++
    #include <stdio.h>
    #include <malloc.h>
    #include <stdlib.h>
    typedef struct node{//链表节点的模型
      int date;
      struct node * pnext;
    }node,* pnode;
    typedef struct stack{//栈的模型，从下开始往上为受限链表,相当于两个指针分别指向链表的上下两端
      pnode ptop;
      pnode pbottom;//pbottom为头指针
    }stack,* pstack;
    void init(pstack ps);//使生成一个空栈
    void push(pstack ps,int value);
    bool is_empty(pstack ps);
    bool pop(pstack ps,int *value);
    bool clear(pstack ps);
    void traverse(pstack ps);
    int main(){
      stack op;//创建一个栈（其中值为垃圾值）
      int delete_value;//删除的元素的值
      init(&op);
      push(&op,2);
      push(&op,4);
      push(&op,5);
      traverse(&op);
      pop(&op,&delete_value);
      traverse(&op);
      clear(&op);
      traverse(&op);
    }
    void init (pstack ps){//对栈进行初始化，动态分配一个链表节点（头指针），使ptop和pbottom指向它，使栈中存放的不是垃圾值
      ps->pbottom = (pnode)malloc(sizeof(node));//因为是动态内存分配的，所以该函数调用完后该内存不会被自动释放
      if(ps->ptop == NULL){
        printf("fail");
        exit(-1);
      }
      ps->ptop = ps->pbottom;
      ps->ptop->pnext = NULL;//头指针内不存放有效数据
    }
    void push(pstack ps,int value){//压栈，动态分配一个链表节点pnew，pnew指向ptop所指向的节点，再让ptop再指向pnew
      pnode pnew = (pnode)malloc(sizeof(node));
      pnew->date = value;
      pnew->pnext = ps->ptop;
      ps->ptop = pnew;
    }
    bool is_empty(pstack ps){
      if(ps->ptop == ps->pbottom)
        return true;
      else 
        return false;
    }
    bool pop(pstack ps,int *value){//出栈，先把栈顶节点保存至r，使ptop指向r->pnext 再free（r），如此防止内存泄漏
      if(is_empty(ps)){//先判断该栈是否为空栈
        printf("fail\n");
        return false;
      }
      else{
        pnode r = ps->ptop;
        *value = r->date;
        ps->ptop = r->pnext;//若直接让ptop指向ptop下面的节点，将使得找不到出栈的节点，造成内存泄漏
        free(r);
        r = NULL;
        return true;
      }
    }
    bool clear(pstack ps){//对栈进行清空，双指针r t，循环(t始终在r下面，free(r)，r=t)
      if(is_empty(ps)){
        printf("fail");
        return false;
      }
      else{
        pnode r = ps->ptop;
        while(r != ps->pbottom){
          pnode t = r->pnext;
          free(r);
          r = NULL;
          r = t;
        }
        ps->ptop = ps->pbottom;
        return true;
      }
    }
    void traverse(pstack ps){//遍历栈，引入一个指针r，r由ptop遍历至pbottom，ptop和pbottom不动
      if(is_empty(ps))
        printf("empty!!\n");
      else{
        pnode r = ps->ptop;
        while(r != ps->pbottom){
          printf("%d ",r->date);
          r = r->pnext;
        }
        printf("\n");
      }
    }
    ```





   ### 队列



    定义：一种可以实现 先进先出 的存储结构（先放进去的先出来 ）类似于排队去买票 

      头出(f) 尾增(r)

      只允许一端插入元素
      只允许另一端把元素删除 
      （栈只允许在一端进行插入删除操作）



    分类



      链式队列：用链表实现

    ​    内部是链表，对链表进行的操作和限制 使其变成队列


      静态队列：用数组实现（把数组的一些功能砍掉）

    ​    静态队列必须是 循环队列
    ​    



   #### 循环队列的几个问题


    ​1.静态队列为什么必须是循环队列 
    ​        按照一般数组的算法来操作时
    ​        
    ​          f端删除一个元素后永远无法往上移 
    ​          删除，增加，f r都是往上移（只能加） 如此会造成空间浪费
    ​          r永远指向的是当前队列的下一个位置

    ​          如若变成循环的，如此加到末尾再加就能到头部去
    ​          所以必须是循环队列 



    2.循环队列需要几个参数来确定，及参数的含义
          
            需要2个参数来确定
            且2个参数不同场合下有不同的含义

    ​        front rear
    ​        
    ​        队列初始化
    ​          front 和 rear 都是0
    ​          
    ​        队列非空
    ​          front代表队列第一个元素
    ​          rear代表队列最后一个有效元素的下一个元素
    ​        
    ​        
    ​        队列空
    ​          front和rear值相等，但不一定为0
    ​    
    ​
    ​    

      出队，入队（压栈，出栈）


      front（出队，删）  

      rear（入队，头指针，增）



    3.入队、出队的伪算法

      将值存入 r 代表的位置

      r = (r+1) % 数组的长度//(n-1)%n == n-1 ， 此为循环队列 防止溢出


      f = (f+1) % 数组的长度


    4.判断队列是否为空、判断队列是否已满

      f可大于r  f可小于r  f可等于r

      f == r

      两种方式

        多增加一个标识参数(有效长度)

        少用一个元素(常用)

          if((r+1)%r == f)
            满
          else
            不满


   #### 队列的应用

      所有和时间有关的操作都有队列的影子

    ```c++
    #include<stdio.h>
    #include<malloc.h>
    typedef struct Queue{
        int *pBase;
        int front;//front代表队列第一个元素
        int rear;//rear代表队列最后一个有效元素的下一个元素
    } QUEUE;
    void init_queue(QUEUE *pQ);
    bool full_queue(QUEUE *pQ);
    bool en_queue(QUEUE *pQ, int val);
    int traverse_queue(QUEUE *pQ);
    bool out_queue(QUEUE *pQ, int *pVal);
    bool empty_queue(QUEUE *pQ);
    int main(){
        // QUEUE Q;
        // int delVal;
        // init_queue(&Q);
        // en_queue(&Q, 1);
        // en_queue(&Q, 2);
        // en_queue(&Q, 3);
        // en_queue(&Q, 4);
        // traverse_queue(&Q);
        // out_queue(&Q, &delVal);
        // printf("\n删除的元素为 %d\n", delVal);
        // traverse_queue(&Q);
    }
    void init_queue(QUEUE *pQ){
        pQ->pBase = (int *)malloc(sizeof(int) * 6);
        pQ->front = pQ->rear = 0;
    }
    bool full_queue(QUEUE *pQ){
        if((pQ->rear+1)%6 == pQ->front)
            return true;
        else
            return false;
    }
    bool en_queue(QUEUE *pQ, int val){
        if(full_queue(pQ))
            return false;
        else{
            pQ->pBase[pQ->rear] = val;
            pQ->rear = (pQ->rear + 1) % 6;
            return true;
        }
    }
    int traverse_queue(QUEUE *pQ){//创建一个r 使其遍历
        int r = pQ->front;
        while(r != pQ->rear){
            printf("%d ", pQ->pBase[r]);
            r = (r + 1) % 6;
        }
    }
    bool out_queue(QUEUE *pQ, int *pVal){
        if(empty_queue(pQ))
            return false;
        else{
            *pVal = pQ->pBase[pQ->front];
            pQ->front = (pQ->front + 1) % 6;
            return true;
        }
    }
    bool empty_queue(QUEUE *pQ){
        if(pQ->rear == pQ->front)
            return true;
        else
            return false;   
    }
    ```


# 递归
    

    一个函数直接or间接调用自己(自己调别人，让别人调自己)
    
    
 ## 为什么一个函数能自己调用自己

    
    调用自己or调用别人，在计算机看来没有任何区别


       一个函数运行时调用另一个函数之前，系统做的三件事：(实参发送过去，下一个语句地址发送过去，为n分配空间 转移控制权限)
            
            
                将所有实际参数，返回地址(调用完之后紧接着要执行的下一个语句的地址，确保程序能接起来)等信息传递给被调函数保存
            
                为被调函数的局部变量分配存储空间
            
                将控制转移到被调函数的入口
            



      从被调函数返回主函数前，系统做的三件事：(保存返回值n， 释放all形参 局部变量，根据保存的地址执行下一个语句)
    
            
                保存被调函数的返回结果(为返回值n产生一份拷贝)
    
                释放被调函数所占的存储空间(静)

                依照被调函数保存的返回地址将控制转移到调用函数    
                
    

      当前运行的函数永远在栈顶的位置，a调用b就把b里all局部变量 形参 压入栈中，在栈顶队b函数进行处理 ，处理完把b函数出栈
            
            
            
            
            
            
 ##  递归需满足的三个条件
    
    
        递归需有一个明确的终止条件
    
        该函数所处理的数据规模必须在递降(规模n的解决 借助于n-1的解决，要解决n的问题 解决n-1的问题即可，要解决n-1的问题 解决n-2的问题即可)
    
        这个转化必须是可解的(一个问题是否可以用递归解决 是数学问题)
        
    
    
 ##  循环和递归
    
    

        理论上all循环都可以转化成递归，但用递归可以解决的问题不一定用循环可以解决
        
        
            
        递归
        
            易于理解
            
            速度慢(函调函)
            
            存储空间大(浪费空间的大)(函调函)



            
        循环
        
            不易理解
            
            速度快
            
            存储空间小(几乎不浪费空间)

    
    
 ## 递归实例  
    
    阶乘的递归实现
    
    int f(int n){
        if(n==1)
            return 1;
        else
            return n*f(n-1);
    }
    

  
    1+...+100的递归实现
    
    int f(n){
        if(n==1)
            return 1;
        else
            return n+f(n-1);
    }
    



    汉诺塔
    
      伪算法

        如果是一个盘子
        
            直接把该盘子从A移到C
        
        否则
        
            把A上的n-1个盘子借助C移到B
            直接把A上的第n个盘子移到C
            把B上的n-1个盘子借助A移到C
            
                    
  ```c++
    #include<stdio.h>
    #include<iostream>
    using namespace std;
    int a = 0;
    void towerofHanoi(int n, char A, char B, char C) {//把A上的n个盘子 借助B 从A移到C上
        if (n == 1) {
            ++a;
            printf("第%d步：把编号为%d的盘子 从%c移到%c上 \n", a, n, A, C);//换成%c 是由于移动过程中A和B的角色会互换
        }
        else{
            towerofHanoi(n - 1, A, C, B);
            ++a;
            printf("第%d步: 把编号为%d的盘子 从%c移到%c上 \n",a, n, A, C);
            towerofHanoi(n - 1, B, A, C);
        }
    }
    int main() {
        int n;
        char A = 'A', B = 'B', C = 'C';
        cin >> n;
        towerofHanoi(n, A, B, C);
    }
  ```       
    
 ##  递归的应用
    
        树和森林是以递归的方式定义
        树和图的很多算法是用递归实现
        很多数学公式是以递归的方式定义
  

# 非线性结构

 ## 树

  ### 树定义

   有且只有一个称为根的节点
   有若干个互不相交的子树，这些子树本身也是一棵树


   树由节点和根组成
   每个节点只有一个父节点，但可以有多个子节点
   但根节点没有父节点


   专业术语

     节点（表示一个具体的事物） 父节点（最上面和它紧挨着的点） 子节点（它下面all节点）
     子孙 堂兄弟



     深度（整个层数，分几层）
      
       从根节点到最底层节点的层数为深度
       根节点是第一层

     叶子节点：

      没有子节点的节点

     非终端节点：

       即非叶子节点

     度：

      子节点的个数



  ### 树分类

   一般树：

    任意一个节点的子节点个数都不受限制

   
   二叉树：

    任意一个节点的子节点个数最多两个，且子节点顺序不可更改

    分类：

      一般二叉树

      满二叉树：

        在不增加树的层数的前提下，无法再多添加一个节点

      完全二叉树：

        只是删除了满二叉树最底层最右边的连续若干个节点所形成的二叉树


   森林：

    n个互不相交的树的集合


  ### 树的存储

      若计算机内有个硬件设备，每一层比每一层更多，类似于树的结构 则不需要学树的存储问题，硬件已有 直接放即可

      但实际内存只是一个线性一维的东西，要把树的关系放到这里面去

      现实中有层次关系的事物要保存在直线型的物理设备上

      解决把非线 —— 线的问题




   #### 二叉树的存储：

      连续存储（完全二叉树） 一般二叉树要用数组来存储必须先转化成完全二叉树

        存储的时候不能只存有效节点，如果只存有效节点 无论以哪种方式，转换成的一定是以线性的来存（先 中 后），即无法倒推出树原来的样子

        非线 —— 线 （但内存又是线性的）

        用三种规则（先 中 后）把树转换成一种线性结构



          完全二叉树的优点：

           知道节点数 就能知道该二叉树有几层

           知道一个节点，就能知道该节点的父节点与子节点
           查找某个节点的父节点和子节点（判断有没有子节点）速度很快


           缺点：

            耗内存



      链式存储


   #### 一般树的存储

    双亲表示法
      求父节点方便

    孩子表示法
      求子节点方便

    双亲孩子表示法
      求父子节点都方便

    二叉树表示法
      把一个普通树转化成二叉树来存储
      具体转换方法：
        设法保证任意一个节点的
          左指针域指向它的第一个孩子
          右指针域指向它的下一个兄弟
        满足此条件即能把普通树转换成二叉树

        一个普通树转换成的二叉树一定没有右子树


   #### 森林的存储

    先把森林转换成二叉树 再存储二叉树

      别的树作为兄弟

  ### 树的操作

    二叉树操作


      遍历

        先序遍历（先访问根节点）：
          先访问根节点
          再先序访问左子树
          再先序访问右子树    

        中序遍历（中间访问根节点）：
          中序遍历左子树
          再访问根节点
          再中序遍历右子树

        后序遍历（最后访问根节点）：
          先中序遍历左子树
          再中序遍历右子树
          再访问根节点




      已知两种遍历序列求原始二叉树

        通过先序和中序 or 中序和后序 可以还原出原始的二叉树
        但通过先序和后序无法还原出原始二叉树

        只有通过先序和中序 or 中序和后序 才可以唯一确定一个二叉树



       eg：

        先序：ABDGHCEFI
        中序：GDHBAECIF
        求后序:CHDBEIFCA


        中序：BDCEAFHG
        后序：DECBHGFA
        求先序：ABCDEFGH





  ### 树的应用

      树是数据库中数据组织的一种重要形式
      操作系统子父进程的关系本身就是一棵树
      面向对象语言中类的继承关系本身就是一棵树
      赫夫曼树





int *j = malloc(13)\\左静右动


  ### 链式二叉树遍历程序（静态）

   ```C++
    #include<stdio.h>
    #include<malloc.h>
    typedef struct tree {//树的一个节点包含 左边的指向左子树的左指针域 中间的数据域 右边的指向右子树的右指针域
        char date;
        struct tree* pLeft;
        struct tree* pRight;
    }T, * pT;
    pT creatTree();
    void proshow(pT pA);//先序
    void midshow(pT pA);//中序 后序同理
    void postshow(pT pA);
    int main() {
        pT a = creatTree();
        proshow(a);
        return 0;
    }
    pT creatTree() {//必须动态创建一个二叉树
        pT pA = (pT)malloc(sizeof(T));//动态创建出二叉树的一个节点的内存空间并把该内存的地址赋给pA
        pT pB = (pT)malloc(sizeof(T));
        pT pC = (pT)malloc(sizeof(T));
        pT pD = (pT)malloc(sizeof(T));
        pT pE = (pT)malloc(sizeof(T));
        pT pF = (pT)malloc(sizeof(T));
        pT pG = (pT)malloc(sizeof(T));
        pA->date = 'A';
        pB->date = 'B';
        pC->date = 'C';
        pD->date = 'D';
        pE->date = 'E';
        pF->date = 'F';
        pG->date = 'G';
        pA->pLeft = pB;
        pA->pRight = pD;
        pB->pLeft = NULL;
        pB->pRight = pC;
        pC->pLeft = NULL;
        pC->pRight = NULL;
        pD->pLeft = pE;
        pD->pRight = pF;
        pE->pLeft = NULL;
        pE->pRight = NULL;
        pF->pLeft = NULL;
        pF->pRight = pG;
        pG->pLeft = NULL;
        pG->pRight = NULL;
        return pA;
    }
  void proshow(pT pA) {//递归问题
      if(pA != NULL) {
          printf("%c ", pA->date);
          proshow(pA->pLeft);
          proshow(pA->pRight);
      }
      /*
        先访问根节点
        再先序遍历左子树
        再先序遍历右子树
      */
  }
   ```


# 排序和查找

  ## 排序和查找的关系

    排序是查找的前提

    排序十分重要

  ## 排序

    冒泡:

      循环遍历一次可将一个max（min）排到末尾

      ```C++
      void sort(int *a,int n){
        for (int i=0; i < n; ++i) {
        for (int j = 0; j < n -1 - i; ++j) {
            if (a[j] > a[j + 1]) {
              t = a[j + 1];
              a[j + 1] = a[j];
              a[j] = t;
            }
          }
        }
      }
      ```


      插入：

        后面的一个元素往前面的元素中插入，保证后面的那个元素加上前面的所有元素都有序

      选择：

        从当前所有元素中选择出一个min与第一个元素交换
        再从除第一个元素之外的元素中选择一个次min与第二个元素交换
        依次....

      归并排序：

        先两个两个排，在四个四个....


      快速排序：

        ```c++
        #include<stdio.h>
          void quickSort(int* a, int L, int R);
          int findPos(int* a, int L, int R);
          int main() {
              int a[6] = { 120, -10, 234, 4, 4, 4 };
              quickSort(a, 0, 5);
              for (int i = 0; i < 6;++i) 
                  printf("%d ", a[i]);
              return 0;
          }
          void quickSort(int* a, int L, int R) {//递归,该函数功能为将数组a中从L到R元素进行排序
              int pos;
              if (L < R) {
                  pos = findPos(a, L, R);//将第一个元素的位置找到，并保证该元素左边元素都小于其，右边都大于其
                  quickSort(a, L, pos - 1);//把左边的元素进行排序
                  quickSort(a, pos + 1, R);//把右边的元素进行排序
              }
          }
          int findPos(int* a, int L, int R) {//调用该函数找到第一个元素的位置 并移动，并值得该元素左边都是小于其，右边都大于其 但无序
              int val = a[L];
              while (L < R) {
                  while(L<R && a[R] >= val)//右边的元素大于等于其 则移动
                      R--;
                  a[L] = a[R];//右边的元素小于其 则赋值
                  while (L<R && a[L] <= val)
                      L++;
                  a[R] = a[L];
              }
              a[L] = val;
              return L;
          }
        ```



# 再次讨论什么是数据结构

  数据结构是研究数据的存储和操作的学问

  数据的存储分为：

    个体的存储

    个体关系的存储

    从某个角度而言，数据的存储最核心即为个体关系的存储，个体的存储可忽略不计


# 再次讨论什么是泛型

  同一种逻辑结构，无论该逻辑结构物理存储是什么样子，我们都可以对他执行相同的操作