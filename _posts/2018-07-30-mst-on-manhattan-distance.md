---
id: 239
title: MST on Manhattan distance
date: 2018-07-30T17:13:23+00:00
author: YoungHun Roh
layout: post
guid: http://13.124.96.114/?p=239
permalink: /2018/07/30/mst-on-manhattan-distance/
hestia_layout_select:
  - default
categories:
  - Misc
  - PS / CP
---
<img class="ls_lazyimg aligncenter" alt="Octants" src="http://community.topcoder.com/i/education/lineSweep/octants.png" file="http://community.topcoder.com/i/education/lineSweep/octants.png" lazyloadindexed="1" lazyloadpass="1" width="315" height="315" border="0" />

한 점에서 8방향으로 가장 가까운것을 찾아, 그 간선들만 고려하면 된다.

증명은 아직 안했다.

만약 찾은 간선들로만 트리를 만들 수 있다면 그 트리가 최소 가중치라는 것은 쉽게 보일 수 있다.

그러나 찾은 간선들로 모든 정점들이 connected라는 것은 잘 모르겠다.

코드:

<pre class="brush: cpp; title: ; notranslate" title="">#include &lt;bits/stdc++.h&gt;
using namespace std;
typedef long long ll;
typedef pair&lt;int, int&gt; pii;
const int MX=250010, inf=2e9;

struct pt{
    int x, y, idx;
    void flip_x(){ swap(x,y); }
    void flip_h(){ x=-x; }
    void flip_v(){ y=-y; }
    int operator ^ (const pt &p) const {
        return (abs(x-p.x) + abs(y-p.y))/2;
    }
} P[MX];
int n;

struct edge{
    int u, v, c;
    bool operator &lt; (const edge &e) const {
        return c&lt;e.c;
    }
};
vector&lt;edge&gt; E;

void add_edge(int a, int b){
    E.push_back({a,b,P[a]^P[b]});
}

int mn(pii tree[], int r){
    pii p={inf, -1};
    for(; 0&lt;r; r-=r&(-r)) p=min(p, tree[r]);
    return p.second;
}
void upt(pii tree[], int x, pii p){
    for(; 0&lt;x && x&lt;=n; x+=x&(-x)) tree[x]=min(tree[x], p); } void solve(){ int idx[MX]; iota(idx, idx+n+1, 0); sort(idx+1, idx+n+1, [](int a, int b){ if(P[a].y==P[b].y) return P[a].x&gt;P[b].x;
        return P[a].y&gt;P[b].y;
    });
    vector&lt;int&gt; comp;
    for(int i=1; i&lt;=n; i++) comp.push_back(P[i].y-P[i].x);
    sort(comp.begin(), comp.end());
    comp.resize(unique(comp.begin(), comp.end())-comp.begin());

    pii tree[MX];
    for(int i=1; i&lt;=n; i++) tree[i]={inf, -1};

    for(int i=1; i&lt;=n; i++){ int v=idx[i]; int r=lower_bound(comp.begin(), comp.end(), P[v].y-P[v].x)-comp.begin()+1; int u=mn(tree, r); if(u&gt;0) add_edge(v, u);
        upt(tree, r, pii(P[v].x+P[v].y, v));
    }

}

void flip_h(){
    for(int i=1; i&lt;=n; i++) P[i].flip_h();
}
void flip_v(){
    for(int i=1; i&lt;=n; i++) P[i].flip_v();
}
void flip_x(){
    for(int i=1; i&lt;=n; i++) P[i].flip_x();
}

int U[MX], sz[MX];
int find(int x){
    return x==U[x] ? x : U[x]=find(U[x]);
}
void unite(int x, int y){
    sz[find(x)]+=sz[find(y)];
    U[find(y)]=find(x);
}

void mst(){
    iota(U, U+n+1, 0);
    fill(sz+1, sz+n+1, 1);
    sort(E.begin(), E.end());
    
    ll ans=0;

    for(edge &e:E){
        int x=e.u, y=e.v; ll c=e.c;
        if(find(x)==find(y)) continue;
        ans+=c*sz[find(x)]*sz[find(y)];
        unite(x,y);
    }
    cout&lt;&lt;ans; } int main(){ ios::sync_with_stdio(0); cin.tie(0); cin&gt;&gt;n;
    for(int i=1; i&lt;=n; i++){ cin&gt;&gt;P[i].x&gt;&gt;P[i].y; P[i].idx=i;
    }

    solve(); flip_x();
    solve(); flip_v();
    solve(); flip_x();
    solve(); flip_h();
    solve(); flip_x();
    solve(); flip_v();
    solve(); flip_x();
    solve(); flip_h();
    
    mst();

    return 0;
}
</pre>

&nbsp;