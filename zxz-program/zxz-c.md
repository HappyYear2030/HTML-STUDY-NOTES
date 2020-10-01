#### 2020.9.30

![R4@$K310F$SNRLM45DCT](小小夕朝图库\R4@$K310F$SNRLM45DCT.png)

```
#define max(a, b) (((a)?(b)) > (a):(b))
头文件 ：#include<stdlib.h>
```

宏定义 可以像上式一样定义函数计算，大概。



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



