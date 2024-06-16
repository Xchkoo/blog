---
title: "[归并排序]luogu-P1908逆序对 题解"
date: 2021-02-04 17:04:40 
categories: 
  - ['排序', '归并排序']
tags: ['排序','归并排序','luogu-P1908 逆序对','题解','Mergesort']
---
### ！！！如果无法显示模板效果，请刷新网页一下！！！
## ( מּ,_מּ)！$\color{darkviolet}{归并排序}$

#### 1. 归并排序简介
> 归并排序（Merge Sort）是建立在归并操作上的一种有效，稳定的排序算法，$\color{red}{该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。}$将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路归并。<p align="right">————百度百科</p>

| 复杂度 |  |
| :-------: | :------------------: |
| 时间复杂度 | $\mathcal{O}(nlogn)$ |
| 空间复杂度 | $\mathcal{T}(n)$ |


![原理图解](mergesort.webp)

归并排序简要概括一下就是————两个步骤：二分 -> 合并(排序的重要步骤)

#### 2. 归并排序原理

##### 1. 二分
正如简介所言，归并排序函数`void msort(int b,int e)`是一个递归函数。
``` cpp
        if(b == e)
		return;
    int mid=(b+e)/2,i=b,j=mid+1,k=b;
    msort(b,mid),msort(mid+1,e);
    //理解递归只需知道你设计这个递归函数的功能，中间的递归过程就不用管了。
```
这一步进行递归二分数组直到不可再分 即b(begin)指针和e(end)指针指向同一位置。

2. 合并
``` cpp
 while(i <= mid&&j <= e)
    	if(o[i]<=o[j])
    		tem[k++]=o[i++];
    	else
    		tem[k++]=o[j++];

```
i,j是指向左数组和右数组的开头的指针
在合并时我们遵守一个原则：将左边的和右边的元素比较，谁小谁先进数组。
逻辑上分为：
$\color{green}{1. i < j 且 a[i] < a[j]时 我们将i指向的元素保存至临时数组tem中。}$
$\color{green}{2. i < j 且 a[i] > a[j]时 我们将j指向的元素保存至临时数组tem中。}$

可是这样轮次放置，可能会出现一边的数组先轮完了，这就是第2、3个while，轮完就意味着不需要再比较了，可以直接放入。
$\color{green}{3. i <= mid 的情况 就直接tem[k++]=o[i++];}$
$\color{green}{   j <= e 的情况   tem[k++]=o[j++];}$
``` cpp
    while(i<=mid)
    	tem[k++]=o[i++];
    while(j<=e)
    	tem[k++]=o[j++];
```
别忘了我们的数组是放在临时数组里的，结束时要放回主数组，毕竟接下来还要递归。
``` cpp
    for(int l=b;l<=e;l++)
    	o[l]=tem[l];
```


#### 3. [原题](https://www.luogu.com.cn/problem/P1908)&AC代码

解题思路:
逆序对就是$1，2，3，4，5$这样顺的数组中出了一个二五仔（如 ${1，2，3，5，4}$ 的情况 ${5，4}$ 就算一组逆序对）,那么二五仔的数量就是我们在归并时else的情况的集合。
``` cpp
while(i <= mid&&j <= e)
    	if(o[i]<=o[j])
    		tem[k++]=o[i++];
    	else
    		tem[k++]=o[j++],ans+=mid-i+1;
```
所以，逆序对的数量实际上就是我们将数组归并排序时发生交换的元素数量。
只要在归并排序的源码上加上计算ans的步骤就行了。

$\color{red}{AC代码}$：
``` cpp Xchkoo-p1908-code https://Xchkoo.top/ Xchkoo
/*
 * © Copyright 2021 Xchkoo All rights reserved.
 * Author: Xchkoo
 * Date: 2021-02-04 5:40
 * LISENSE: CC v4.0 BY-SA https://creativecommons.org/licenses/by-sa/4.0/deed.zh
 * Remark: Thanks for viewing XD
 * Welcome to my blog -> Xchkoo.top 
 */
#include<iostream>
#define N 500010
using namespace std;
int n;
int o[N];//Main
int tem[N];//Temporary
long long ans;

void msort(int b,int e)// b = begin e = end
{
    if(b == e)
	    return;
    int mid=(b+e)/2,i=b,j=mid+1,k=b;
    msort(b,mid),msort(mid+1,e);
    while(i <= mid&&j <= e)
    	if(o[i]<=o[j])
    		tem[k++]=o[i++];
    	else
    		tem[k++]=o[j++],ans+=mid-i+1;//count answer
    while(i<=mid)
    	tem[k++]=o[i++];
    while(j<=e)
    	tem[k++]=o[j++];
    for(int l=b;l<=e;l++)
    	o[l]=tem[l];
}           

int main()
{
    ios::sync_with_stdio(false);
    cin >> n;
    for(int i=1;i<=n;i++){
        cin >> o[i];
    }
    msort(1,n);
    cout << ans;
    return 0;
}
```