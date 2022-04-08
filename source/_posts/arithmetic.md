---
title: arithmetic
date: 2022-04-06 15:25:39
tags: 学无止境
---

## 算法

### MiniMax (极小化极大算法)

查询出最坏的情况下最好的那个结果
1、[CSDN MiniMax 讲解](https://blog.csdn.net/zkybeck_ck/article/details/45644471)

#### Alpha-Beta剪枝算法

删除 MiniMax 算法中不影响结局的中间节点
对 MiniMax 树进行中序遍历

>alpha 为下限，初始为 -inif
>beta 为上限,初始为 +inif

1、在 MiniMax 算法树中，每一个 min 节点修改 beta 值，每一个 max 节点修改 alpha 值
2、当某个节点出现 alpha >= beta 时，该节点剩下的子节点可以忽略不计
