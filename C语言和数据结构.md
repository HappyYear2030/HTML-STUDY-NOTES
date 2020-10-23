# C语言&数据结构

```
·动态内存分配所使用的三个函数：
--malloc(),calloc(),realloc().不过在堆中申请的内存空间不会像在栈中存储的局部变量一样，函数调用完会自动释放内存，需要我们手动释放——free()函数。
```

##  1.malloc ()

```
(void*)malloc(size_t size)
1).malloc()函数会向堆中申请一片连续可用的内存空间.
2).若申请成功,返回指向这片内存空间的指针 ,若失败 ,则会返回NULL, 所以我们在用malloc()函数开辟动态内存之后, 一定要判断函数返回值是否为NULL.
3).返回值的类型为void*型, malloc()函数并不知道连续开辟的size个字节是存储什么类型数据的 ,所以需要我们自行决定,
方法是在malloc()前加强制转 ,转化成我们所需类型,如: (int*)malloc(sizeof(int)*n).
4).如果size为0, 此行为是未定义的, 会发生未知错误, 取决于编译器.
5).malloc函数只能反回第一个字节的地址所以必须加类型强制转换(elemtype*).
·例子：
int *p = NULL;
int n = 0;
scanf("%d", &n);
p = (int*)malloc(sizeof(int) * n);//不太懂这个*n
if(p != NULL){
    //....需要进行的操作
}
这时就相当于创建了一个数组 p[n] ,这个n的值并不需要像定义一个普通数组一样必须是常量, 可以使程序运行时得出的, 或是用户输入的。
```

<a herf="C:\Users\周志豪\Desktop\studio-gzs\project-1\new-1\picture\malloc.jpg">malloc截图</a>
=======
![malloc截图](\C:\Users\周志豪\Desktop\studio-gzs\project-1\new-1\picture\malloc.jpg)

# C语言位运算

## 1、位运算是指按二进制进行的运算。在系统软件中，常常需要处理二进制位的问题。C语言提供了6个位操作运算符。这些运算符只能用于整型操作数，即只能用于带符号或无符号的char,short,int与long类型。

## 2、C语言运算符含义详解：

```
1>.
   & 按位与----如果两个相应的二进制位都为1，则该位的结果值为1，否则为0

2>.
   | 按位或----两个相应的二进制位中只要有一个为1，该位的结果值为1

3>.
   ^ 按位异或---若参加运算的两个二进制位值相同则为0，否则为1

4>.
   ~ 取反------~是一元运算符，用来对一个二进制数按位取反，即将0变1，将1变0

5>.
   << 左移------用来将一个数的各二进制位全部左移N位，右补0

6>.
   >> 右移------将一个数的各二进制位右移N位，移到右端的低位被舍弃，对于无符号数，                 高位补0
```

# C语言逻辑运算符

## 1.&& (逻辑与)    | | (逻辑或)

````
1) && (逻辑与)：(三种)

① 当逻辑与左边为false(假)，则不再进行逻辑与右边的判断，结果为false(假)

② 当逻辑与左边为true(真)则进行右边判断，右边为false(假)，结果为false(假)

③ 当逻辑与左边为true(真)则进行右边判断，右边也为true(真)，则结果为true(真)


2) || (逻辑或)：(三种)

① 当逻辑或左边为false(假)，继续逻辑或右边的判断，如果也为false(假)，结果为false(假)

② 当逻辑或左边为false(假)，继续逻辑或右边的判断，如果为true(真)，结果为true(真)

③ 当逻辑或左边为true(真)，则不再进行逻辑或右边的判断，结果为true(真)
````

# 单链表的冒泡排序
```设置三个指针tail，p，cur；p和tail用于控制外循环的次数，cur用于内循环。

1. 排序开始前遍历一次单链表将tail指向尾结点的指针域，即NULL。cur和p均指向头结点。
2. 比较cur->data与cur->next->data的大小，若前者大于后者则交换；否则不交换，之后cur指针右移，继续比较cur->data与cur->next->data的大小，直至cur->next==tail。
3. 一次循环之后，将tail指向cur的位置，即相当于tail前移。将cur重新指向头结点，重复步骤2。
4. 直至p->next==tail结束整个循环。

  由于需要被冒泡排序的链表不一定十分杂乱无序，有可能经过s少量几次循环后就会有序，不需要经过大量的循环，所以为了减少循环次数，设置一个变量flag，flag初始值为0，若在某一次循环中有元素与元素间的交换，flag变为1，如果没有元素的交换，证明这次循环单链表已经有序，flag不变，依旧为0。没经历一次循环判断flag的大小是否为0，若为0，直接跳出整个循环。
```

```
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct {

    int m;

} jihe;

typedef struct set {

    jihe data;//这是我们的数据类型所以要用jihe
    struct set* next;//这是我们的节点类型，所以要用set，下次一定取个好名字，害，裂开了
} set;

void initial_linklist(set* *L) {

    (*L) = (set*)malloc(sizeof(set));
    (*L)->next = NULL;
}


//创建链表(前插法)
int Create_linklist1(set* L) {
    int a, b;
    printf("请定义A集合的元素个数：|A|=");
    scanf("%d", &a);
    if (!a)return 0;//判断是否为空表
    set* p;
    for (b = 1; a > 0; a--, b++) {
        printf("第%d个元素为：", b);
        p = (set*)malloc(sizeof(set));
        scanf("%d", &(p->data.m));
        p->next = L->next;//有点问题 现在没了，喵喵喵
        L->next = p;
    }
    return b;
}


//创建链表(尾插法)
int Create_linklist2(set* L) {
    set* p, * q;
    int a, b;
    p = (set*)malloc(sizeof(set));
    q = L;
    printf("请定义B集合的元素个数：|B|=");
    scanf("%d", &a);
    if (!a)return 0;//判断是否为空表

    for (b = 1; a > 0; a--, b++) {
        p = (set*)malloc(sizeof(set));
        printf("第%d个元素为：", b);
        scanf("%d", &(p->data.m));
        p->next = NULL;
        q->next = p;
        q = p;
    }
    return b;
}


//用来输出结构体成员（此处结构体只有一个成员，所以其他场合并不适用）
void output(set L) {
    set* p;
    p = L.next;
    while (p) {
        printf("%d ", p->data.m);
        p = p->next;
    }

}


//这是一个给集合元素排序的函数（链表的冒泡），希望不要bug      555，QAQ，枯了
void order(set* L) {//L用来存放 结构体数组 的首地址

    if (L->next == NULL)return 0;

    set* tail, * p,*cur;
    cur = L;
    p = L->next;//L->next相当于a1的地址
    tail = L->next;
    int a;

    while (tail->next != NULL) {

        tail = tail->next;
    }

    while (p != tail) {
        p = L->next;

        while (p != tail) {
            if (p->data.m > p->next->data.m) {
                a = p->data.m;
                p->data.m = p->next->data.m;
                p->next->data.m = a;
                cur = p;
                p = p->next;
            }
            else {
                cur = p;
                p = p->next;
            }
        }
        tail = cur;
    }

}

void Collection_merger(set* LA, set* LB) {
    set* tail = LA;

    while (tail->next != NULL) {

        tail = tail->next;
    }
    tail->next = LB->next;

    order(LA);
}

void exchange(set* L) {}

void main() {


    set *LA = NULL;
    set *LB = { 0 };


    initial_linklist(&LA);
    initial_linklist(&LB);


    Create_linklist1(LA);
    Create_linklist2(LB);


    printf("\n集合A={ ");
    output(*LA);
    printf("}");


    printf("\n集合B={ ");
    output(*LB);
    printf("}");


    order(LA);
    printf("\n排序后集合A={ ");
    output(*LA);
    printf("}");


    order(LB);
    printf("\n排序后集合B={ ");
    output(*LB);
    printf("}");


    Collection_merger(LA, LB);
    printf("\nA集合,B集合 合并为集合C={ ");
    output(*LA);
    printf("}");
}
```




```
//这是一个给集合元素排序的函数（链表的冒泡），希望不要bug      555，QAQ，枯了
void order(set* L) {//L用来存放 结构体数组 的首地址

    if (L->next == NULL)return 0;

    set* tail, * p,*cur;//cur用来存放p的上一个节点的地址，以便于tail的移动
    cur = L;
    p = L->next;//L->next相当于a1的地址
    tail = L->next;
    int a;

    while (tail->next != NULL) {

        tail = tail->next;
    }//将tail移动到尾节点

    while (p != tail) {/*外层循环*/
        p = L->next;

        while (p != tail) {/*内层循环（这个理解起来没问题）*/
            if (p->data.m > p->next->data.m) {
                a = p->data.m;
                p->data.m = p->next->data.m;
                p->next->data.m = a;
                cur = p;
                p = p->next;
            }
            else {
                cur = p;
                p = p->next;
            }
        }
        tail = cur;
    }

}
//纪念一下这个快乐的时刻，喵喵喵！
```



# 链表

```
1，初始化链表头部指针需要用二级指针或者一级指针的引用。

2，销毁链表需要用到二级指针或者一级指针的引用。

3，插入、删除、遍历、清空结点用一级指针即可。
```

