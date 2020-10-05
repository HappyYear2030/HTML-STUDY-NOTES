#### 2020.9.30

![R4@$K310F$SNRLM45DCT](小小夕朝图库\R4@$K310F$SNRLM45DCT.png)

```
#define max(a, b) (((a)?(b)) > (a):(b))
头文件 ：#include<stdlib.h>
```

宏定义 可以像上式一样定义函数计算，大概。

我感觉是因为左边```max(a, b)```命名了右边, 右边```(((a)?(b))>(a):(b))```是个值<br/>

仍然符合宏定义的标准。

 #### 2020.10.1

字符数组与单独设置字符指针再```malloc```分配效果一样，可以通过```p[i] 或 *(p+i)``` 的形式拿出值,可以用```strcpy```。

但是```sizeof``` 只能算字符数组的长度，指针仍然只有4个长度。

验证代码如下：

```
char a[100] = "313163163231651", b[100] = "6563215646156";


	char* p;
	p = (char*)malloc(100);
	strcpy(p, "123456789");
	printf("%s  %d\n", p, sizeof(a));
	int i;
	for (i = 0; i < sizeof(p); i++) {
		printf("%c %c ", *(p+i), p[i]);
	}
```

[]:我觉得能用是因为字符数组名就是个指针

[]:```sizeof```算形参只能的形参的长度，比如形参是指针，实参是个数组。

[]:```malloc```分配空间之后就有了指针地址

------

**赋值给空字符串的时候记得给结尾NULL **   ```%s```就会喵喵喵。

##### 大数相加代码

```
//大数加减 1.1版本
//头文件 <malloc.h> <stdlib.h>
char* dashuxiangjia_11(char a[], char b[]) {
	
	int zifuchangdu_1(char a[]) {
	int i;
	for (i = 0; *(a + i); i++);
		return i;
    }
	
	//先求长度 试验无问题
	int length_1 = zifuchangdu_1(a), length_2 = zifuchangdu_1(b);
	int length_max = __max(length_1, length_2);

	//以实验 可以给字符指针分配初始空间 并给值
	char* p1, * p1_1, * p1_2;
	p1 = (char*)malloc(length_max + 1);
	p1_1 = (char*)malloc(length_1 + 1);
	p1_2 = (char*)malloc(length_2 + 1);

	//反序
	//经试验 %s时将多输出 因为末尾不是空
	int i;
	for (i = 0; i < length_1; i++) {
		p1_1[i] = a[length_1 - 1 - i];
	}
	for (i = 0; i < length_2; i++) {
		p1_2[i] = b[length_2 - 1 - i];
	}
	p1_1[length_1] = NULL;
	p1_2[length_2] = NULL;
	//printf("--------------------------\n%s -%s\n-----------------------", p1_1, p1_2);

	//现在应该没问题了 开始实现加法
	p1[0] = NULL;//避免第一次判断出 '1'
	p1[length_max] = NULL;
	for (i = 0; i < length_max; i++) {//不需要循环加一次

		if (p1[length_max] == '1')continue;

		if (p1[i] == '1')p1[i] = p1_1[i] + p1_2[i] - '0' + 1;//进位
		else p1[i] = p1_1[i] + p1_2[i] - '0';

		if (p1[i] > '9') {
			p1[i] -= 10;
			p1[i + 1] = '1';
		}
	}
	if (p1[length_max] == NULL);
	if (p1[length_max] == '1') p1[length_max + 1] = NULL;//字符串收尾

	//printf("\n%s\n", p1);


	//順序再回来应该就可以了
	
	if (p1[length_max] == NULL) {

		int j = length_max;
		for (i = 0; i < j; i++, j--) {
			char mmm;
			mmm = p1[j - 1];
			p1[j - 1] = p1[i];
			p1[i] = mmm;

		}
	}
	if (p1[length_max + 1] == NULL) {

		int j = length_max;
		for (i = 0; i < j; i++, j--) {
			char mmm;
			mmm = p1[j];
			p1[j] = p1[i];
			p1[i] = mmm;

		}
	}

	//printf("最终试验\n------%s-------\n", p1);//大功告成 哈哈哈

	//printf("%d %d %d", length_1, length_2, length_max);

	return p1;
}
```

------



![UAASWDMY64OPHTBI](小小夕朝图库\UAASWDMY64OPHTBI.png)

[未加载](https://blog.csdn.net/fidoliang/article/details/105340095)```wntdll.pdb```

可能是内存泄漏。

##### 关于内存泄漏

动态内存分配结尾不像数组结尾会给NULL。。。

```strcpy```会给结尾空

###### 动态内存分配初始化不成功，却使用了它

- 在内存使用时检查指针是否为NULL

- Always use **memset** along with malloc, or always use calloc.
```
# include <string.h>
void *memset(void *s, int c, unsigned long n);(memory set)
将指针变量 s 所指向的前 n 字节的内存单元用一个“整数” c 替换，注意 c 是 int 型。s 是 void* 型的指针变量，所以它可以为任何类型的数据进行初始化。
# stdlib.h或malloc.h
void *calloc(unsigned n,unsigned size)；
在内存的动态存储区中分配n个长度为size的连续空间，函数返回一个指向分配起始地址的指针；如果分配不成功，返回NULL。
# string.h
void *memcpy(void *dest, const void *src, size_t n);
从src的开始位置拷贝n个字节的数据到dest。如果dest存在数据，将会被覆盖。memcpy函数的返回值是dest的指针。
```

- '\0' = 0

###### 尚未初始化就引用

- 给初始值

###### 内存分配成功并且已经初始化，但操作越过了内存的边界

- 例如在使用数组时经常发生下标“多1”或者“少1”的操作。特别是在for循环语句中，循环次数很容易搞错，导致数组操作越界。

###### 忘记了释放内存，造成内存泄露

- 记得```free```

###### [相关链接](https://blog.csdn.net/qq_32319583/article/details/53641469) 

------

#### 2020.10.2

#### 2020.10.3

```strcmp
# <string.h>
strcmp()函数有两个参数，即要比较的两个字符串。strcmp()函数对两个字符串进行大小写敏感的(case-sensitiVe)和字典式的(lexicographic)比较，并返回下列值之一：
----------------------------------------------------
    返  回  值         意  义
----------------------------------------------------
    <0               第一个字符串小于第二个字符串
     0               两个字符串相等    ·
    >0               第一个字符串大于第二个字符串
----------------------------------------------------

在上例中，当比较str_1(即“abc”)和str_2(即“abc”)时，strcmp()函数的返回值为0。然而，当比较str_1(即"abc")和str_3(即"ABC")时，strcmp()函数返回一个大于0的值，因为按ASCII顺序字符串“ABC”小于“abc”。

strcmp()函数有许多变体，它们的基本功能是相同的，都是比较两个字符串，但其它地方稍有差别。下表列出了C语言提供的与strcmp()函数类似的一些函数：   
-----------------------------------------------------------------
    函  数  名                   作  用
-----------------------------------------------------------------
    strcmp()         对两个字符串进行大小写敏感的比较
    strcmpi()        对两个字符串进行大小写不敏感的比较
    stricmp()        同strcmpi()
    strncmp()        对两个字符串的一部分进行大小写敏感的比较
    strnicmp()       对两个字符串的一部分进行大小写不敏感的比较
-----------------------------------------------------------------
在前面的例子中，如果用strcmpi()函数代替strcmp()函数，则程序将认为字符串“ABC”等于“abc”。
```

#### 2020.10.4

无符号整型输出用```%d```

