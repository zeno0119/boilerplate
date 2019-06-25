---
title: ダイクストラ法組んでみた
tag: C/C++
date: 2019-06-25
---

# ダイクストラ法を利用した最良優先探索アルゴリズムを組んでみた
## ダイクストラ法って何？
スタート地点から目標地点までの最短距離を求めるアルゴリズム
## 何がいいの？
最適化すれば線形時間で最短距離を調べることができる $O(n)$
## どんなアルゴリズム？
ノード間のコストと経路間のコストを足し合わせて最小値だけを残していく
## 実装下アルゴリズム(C)
```C
#pragma once

#include <math.h>

struct Node {
    int id;
    int cost;
};

struct Path {
    int id1;
    int id2;
    int cost;
};

void dikstra(struct Node node[], struct Path path[], int nNode, int nPath){
    printf("%d\n", nNode);
    int prev = -1;
    node[0].cost = 0;
    printf("%d", node[0].id);
    for(int i = 0;;){
        int minCost = 10000;
        int next = 0;
        for(int j = 0;j < nPath;j++){
            if((node[i].id == path[j].id1 || node[i].id == path[j].id2) && (prev != path[j].id2 && prev != path[j].id1)){
                int to = ((path[j].id1 == node[i].id) ? path[j].id2 : path[j].id1);
                node[to].cost = (int)fmin(node[to].cost, path[j].cost + node[i].cost);
                if(minCost > node[to].cost){
                    minCost = node[to].cost;
                    next = to;
                }
            }
        }
        prev = node[i].id;
        i = next;
        printf(" - %d", next);
        if(node[next].id == nNode - 1)break;
    }
}
```
これを適当にmain関数に突っ込んであげると経路が表示できる