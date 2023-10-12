# 程序设计基础 上机5 指针的应用
一、实验目的及要求

1、深刻理解和区分普通变量和指针变量、地址的概念。

2、正确使用指针变量、指针数组、字符串指针和二级指针编写程序。

3、掌握指针的基本运算。

4、掌握如何通过指针类型的变量访问某个变量或数组元素的值。

二、实验设备（环境）及要求

1、CodeBlocks集成开发环境

2、PTA程序设计类实验辅助教学平台www.pintia.cn

三、实验内容与步骤

1、字符串逆序

（1）题目

 编写函数`int strreverse(char *str1, char *str2)`，对输入的字符串str2，将其逆序放入字符串str1中，其返回值为str1的长度。

（2）源代码

 ```c
 #include<stdio.h>
 #include<string.h>
 int strreverse(char* str1, char* str2) {
 	for (int i = strlen(str2)-1,j=0; i > -1; i--,j++)
 		str1[j] = str2[i];
 	return strlen(str2);
 }
 
 int main(void) {
 	char a[10];
 	gets(a);
 	char b[10] = { '\0' };
 	int c=strreverse(b, a);
 	printf("%s\n%d",b, c);
 	return 0;
 }
 ```

（3）运行结果截屏

 

2、指针实现数的查找

（1）题目

 编写函数int find(int *p,int n,int x)，在指针p所指的数组中查找整型数x，如果x在数组中，则该函数返回1，否则返回0。n为数组的大小。

（2）源代码

 ```c
 #include<stdio.h>
 int find(int* p, int n, int x) {
 	int i = 0;
 	for ( i = 0; i < n; i++)
 		if (*(p+i)==x)
 			return 1;
 	return 0;
 }
 
 int main(void) {
 	int a[50], n;
 	scanf("%d", &n);
 	for (int i = 0; i < n; i++)
 		scanf(" %d", &a[i]);
 	int* p = a;
 	int c;
 	scanf("%d", &c);
 	c = find(p,n,c);
 	printf("%d", c);
 	return 0;
 }
 ```

（3）运行结果截屏

 

3、查找奥运五环色的位置

（1）题目

 奥运五环的5种颜色的英文单词按一定顺序排列{"red", "blue", "yellow", "green", "black" }，定义指针数组并初始化，输入任意一个颜色的英文单词，从已有颜色中查找并输出该颜色的位置值，若没有找到，则输出"Not Found"。

（2）源代码

 ```c
 #include<stdio.h>
 #include<string.h>
 
 int main(void) {
 	char* p[5] = { "red", "blue", "yellow", "green", "black" };
 	char a[10];
 	gets(a);
 	int flag = 0;
 	for (int i = 0; i < 5; i++)
 	{
 		if (strcmp(p[i],a)==0) {
 			printf("%d\n", i + 1);
 			flag = 1;
 		}
 	}
 	if (flag==0)
 		printf("Not Found");
 	return 0;
 }
 ```

（3）运行结果截屏

 

4、求多个学生的课程平均分

（1）题目

假设有M门课程N个学生（此处假设M为3，N为4），要求编程求各门课程的平均分，并查找M门课程均不及格的学生的成绩。用指针来实现。
其中求每门课程的平均分的函数为：`void average (float(*p)[N]) `。
查找M门课程均不及格的学生成绩的函数为：`void search (float(*p)[N])`

（2）源代码

```c
#include<stdio.h>
#define M 3
#define N 4
/*计算并打印每门课程的平均成绩*/
void average(float(*p)[N])		/*p为行指针*/
{
	float sum = 0;
	for (int i = 0; i < M; i++)
	{
		sum = 0;
		for (int j = 0; j < N; j++)
			sum += *(*(p + i) + j);
		printf("%d course average is %.1f\n", i + 1, sum / 4);
	}
}

/*查找各门课程不及格的学生及其成绩*/
void search(float(*p)[N])        /*p为行指针*/
{

	for (int i = 0; i < N; i++)
	{
		float sum = 0;
		for (int j = 0; j < M; j++)
		{
			
			sum += p[j][i];
		}
		if (sum / 3 < 60)
		{
				printf("%d course %d student score is %.2f\n", 1, i+1, p[0][i]);
				printf("%d course %d student score is %.2f\n", 2, 1+i, p[1][i]);
				printf("%d course %d student score is %.2f\n", 3, 1+i, p[2][i]);
		}
		
	}

}
int main(void)
{
	float score[M][N];
	int i, j;
	for (i = 0; i < M; i++)
	{
		for (j = 0; j < N; j++)
			scanf("%f", &score[i][j]);
	}
	average(score);   //调用average函数打印每门课平均成绩
	search(score);   //调用search函数查找各门课程不及格的学生及其成绩
	return 0;
}
```

（3）运行结果截屏
