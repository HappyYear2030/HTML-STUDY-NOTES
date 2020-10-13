

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

```
//我决定不用动态内存分配了
//就直接100个字节最简单
//
char* __dashujia(char* data_1, char* data_2) {
	char data_num[1000] = { 0 };

	char datalist_1[1000] = { 0 }, datalist_2[1000] = { 0 };
	int data_1_length = 0, data_2_length = 0, data_lengthmax = 0;
	int i;
	for (i = 0; data_1[i]; i++)
		data_1_length = i + 1; 
	//printf("%d\n", data_1_length);
	for (i = 0; data_2[i]; i++)
		data_2_length = i + 1;
	//printf("%d\n", data_2_length);
	data_lengthmax = __max(data_1_length, data_2_length);
	//printf("%d\n", data_lengthmax);
	//初始化为‘0’不然相加时有一个字符串里的元素为空就加不了
	memset(datalist_1, '0', data_lengthmax);
	memset(datalist_2, '0', data_lengthmax);
	for (i = 0; i < data_1_length; i++) {
		datalist_1[i] = data_1[data_1_length - 1 - i];
	}
	for (i = 0; i < data_2_length; i++) {
		datalist_2[i] = data_2[data_2_length - 1 - i];
	}
	//printf("%s\n%s\n", datalist_2, datalist_1);
	//printf("%s\n", datalist_1);

	for (i = 0; i < data_lengthmax; i++) {
		
		if (data_num[i] == '1') {
			data_num[i] = datalist_1[i] + datalist_2[i] - '0' + 1;
		}
		else
		{
			data_num[i] = datalist_1[i] + datalist_2[i] - '0';
		}

		if (data_num[i] > '9') {
			data_num[i] -= 10;
			data_num[i + 1] = '1';
		}

	}
	//printf("%s", data_num);
	if (data_num[data_lengthmax] == '1') {
		for (i = 1; i < (data_lengthmax+1)/2 ; i++) {
			char m;
			m = data_num[data_lengthmax - i];
			data_num[data_lengthmax - i] = data_num[i];
			data_num[i] = m;
		}
	}
	else
	{
		for (i = 1; i < data_lengthmax/2; i++) {
			char m;
			m = data_num[data_lengthmax - i -1];
			data_num[data_lengthmax - i - 1] = data_num[i];
			data_num[i] = m;

		}
	}
	//printf("%s", data_num);

	return data_num;
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

##### free释放非动态存储空间

- 在我完成顺序表的作业时，由于我```free```了线性表```L```而不是```L.elem``` , 导致了这个错误

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

无符号整型输出用```%u``` 其最大值4294967295

#### 2020.10.5

对于一个数据的定义需要指定两种属性----数据类型和存储类别。未声明存储类别为```auto```型。

```
auto int a;自动变量/动态局部（一般我们用的是这个）
static int a;静态局部变量（作用域仍然只有函数内但生存期为整个程序，函数调用后其值保留）
register int a;寄存器变量，存储在CPU寄存器中，可以节省时间，一般用不到。
extern a;扩展全局变量的作用域
static int a;此全局静态变量不能被 extern 察觉
```



##### 递归算法三部曲

- 找变化：递归运算中变化的量

  对数组实现运算的时候，数组名是不变的，我们可以给函数多加一个参数，以变化。

- 找重复：函数体部分

- 找边界：递归终止的条件，即出口

##### 斐波那契数列

```
//暴力求，每个分支都算。频度是an(斐波那契第N项)
int feibonaqie_baoli(int n) {
	if (n == 1 || n == 2)return 1;
	return feibonaqie_baoli(n - 1) + feibonaqie_baoli(n - 2);

}
f(n)
|       \
|        \
f(n-1)   f(n-2)
|     \     |     \
|      \    |      \
f(n-2)  ```  ```     ```
|
|
​```
|
|
f(1||2)
关于演算顺序是先纵后横。（我觉得以后的赵夕朝应该懂这句话的意思，如今的zxz就不多解释了）

//利用性质简单加法，频度是n-2
int feibonaqie(int a, int b, int n) {
	if (n < 3) return b;
	return feibonaqie(b, a + b, --n);
}
int __feibonaqie(int n) {
	return feibonaqie(1, 1, n);
}
```

#### 2020.10.6

字符数组用```scanf```输入时其空格的作用是作多个字符串输入的空格

```
scanf("%s%s%s%s", str1, str2, str3) 
输入 how are you?
则输出 how are you?
若scanf("%s", str1)
输入 how are you?
则输出 how
```

```
//汉诺塔游戏 
//输入层数 最小为三 后三个参数为起始位置、终止位置、桥梁位置
int hannuota(int censhu, char qishi, char zhongzhi, char qiao) {
	
	if (censhu <= 1) return 1;
	static int i = 0;

	hannuota(censhu - 1, qishi, qiao, zhongzhi);
	if (censhu == 2) {
		printf("(%d)from(%c)to(%c)\n", 1, qishi, qiao);
		i++;
	}
	
	printf("(%d)from(%c)to(%c)\n", censhu, qishi, zhongzhi);
	i++;

	hannuota(censhu - 1, qiao, zhongzhi, qishi);
	if (censhu == 2) {
		printf("(%d)from(%c)to(%c)\n", 1, qiao, zhongzhi);
		i++;
	}

	return i;
}

```



#### 2020.10.7

虽然我最近没有学习，但是没有关夕。冲冲冲

```memset```是对前n个字节起作用

```
int main() {

	typedef struct book {
		int a;
		char b;
		double m;

	}book;

	book a = { 2, '5', 10.00 };
	
	memset(&a, 0, 7);
	printf("%d\n", sizeof(book));
	printf("%d %c %lf", a.a, a.b, a.m);
	
	return 0;




}
```

运行结果如下：

![@T3165X@NTD`73ZG07@AIV](小小夕朝图库\@T3165X@NTD`73ZG07@AIV.png)

其中char还因为对齐有了4个字节。

#### 2020.10.9

函数返回地址时，在主函数里仍然可以通过指针访问。

#### 2020.10.12

##### 二分查找

```
binary [数]二进制的、二态的 
binary_search 二分查找
count 伯爵、指望、数数、总数...
```

```
//binary_search
int binary_search(int key, int a[], int n) {
	int low, high, mid, count = 0, count1 = 0;
	low = 0;
	high = n - 1;
	while (low<high)
	{
		count++;
		mid = (low + high) / 2;
		if (key < a[mid])
			high = mid - 1;
		else if(key>a[mid])
		{
			low = mid + 1;
		}
		else if (key == a[mid]) {
			printf("查找成功！\n 查找%d次！a[%d] = %d", count, mid, key);
			count1++;
			break;
		}
	}
	if (count1 == 0)
		printf("查找失败！");
	return 0;

}


//二分查找  仅对有序数组生效
status __erfenchazhao(int shuzu[], int zhi, int left, int right) {
	static int count;//静态局部变量
	count++;
	int mid = (left + right) / 2;
	if (left > right) return OK;
	if (zhi < shuzu[mid])
		right = mid - 1;
	if (zhi > shuzu[mid])
		left = mid + 1;
	if (zhi == shuzu[mid]) {
		printf("查找成功！\n%d位置为%d", zhi, mid);
		return OK;//结束退出语句
	}
	__erfenchazhao(shuzu, zhi, left, right);
	
	return OK;
}
```

