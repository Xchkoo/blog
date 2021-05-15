---
title: "[匈牙利算法-最小覆盖点]POJ3041题解"
description: "匈牙利算法-最小覆盖点"
categories: 
  - ['图论', '匈牙利算法']
tags: ['图论','匈牙利算法','最小覆盖点','题解']
date: 2021-01-16 14:20:13
---
## 最小点覆盖
#### <font color=red size=3>例题</font>: [POJ3041](http://poj.org/problem?id=3041)
#### <font color=red size=3>理解</font>： 有图G{U,V}，求删去最小点可删去所有边的步骤即求最小点覆盖的过程

------

##### 二分图最大匹配的<font color=red size=3>König定理</font>及其证明(过于困难)->见[http://www.matrix67.com/blog/archives/116]

------

##### 结论版<font color=red size=5> König定理</font> :

1. 由X侧匹配失败的一点回溯所有边（可见图） 并给走过的点打上标记
2. X侧未打标记的点和X对侧打标记的点集就是最小点覆盖

![post1-img1](post1-img1.jpg)
------


### **代码:**
```cpp
#include<cstdio>
#include<cstring>
using namespace std;
const int maxn=500+10;

struct Max_Match
{
    int n;
    bool g[maxn][maxn];
    bool vis[maxn];
    int left[maxn];

    void init(int n)
    {
        this->n=n;
        memset(g,0,sizeof(g));
        memset(left,-1,sizeof(left));
    }

    bool match(int u)
    {
        for(int v=1;v<=n;v++)if(g[u][v] && !vis[v])
        {
            vis[v]=true;
            if(left[v]==-1 || match(left[v]))
            {
                left[v]=u;
                return true;
            }
        }
        return false;
    }

    int solve()
    {
        int ans=0;
        for(int i=1;i<=n;i++)
        {
            memset(vis,0,sizeof(vis));
            if(match(i)) ans++;
        }
        return ans;
    }
}MM;

int main()
{
    int n,k;
    scanf("%d%d",&n,&k);
    MM.init(n);
    while(k--)
    {
        int u,v;
        scanf("%d%d",&u,&v);
        MM.g[u][v]=true;
    }
    printf("%d\n",MM.solve());
    return 0;
}
```

------

##### [参考博客](https://zhuanlan.zhihu.com/p/96229700)
