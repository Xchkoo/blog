title: "[匈牙利算法-最小覆盖点]POJ3041题解"
description: "[匈牙利算法-最小覆盖点]POJ3041题解"
categories: 
  - ['图论', '匈牙利算法']
tags: ['图论','匈牙利算法','最小覆盖点','题解']
---

```
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
###参考博客
