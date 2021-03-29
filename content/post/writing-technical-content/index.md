---
summary: 给定n、k，求自然数的k次幂的和，结果对2^32取模。
authors:
  - 阿威
math: true
date: 2016-11-29T16:00:00.000Z
diagram: true
highlight: true
title: light oj 1132【矩阵快速幂】/【伯努利数】
tags:
  - 矩阵快速幂
image:
  placement: 3
  caption: ""
---
题目：http://vjudge.net/problem/LightOJ-1132

做快速幂专题做到的题

题意：给定n、k，求自然数的k次幂的和，结果对2^32取模。

分析：
    令S(n)=1^k+2^k+...+n^k

有两种做法，看到n^k，想到xiongmao之前说的沈阳的题，通项里有i^4,两题构造方式一样。

由二项式定理，(n+1)^k展开C(k,0)*n^k+C(k,1)*n^(k-1)+...+C(k,k)*n^0，可知(n+1)^k能由

n^k,n^(k-1)...,n^0推出，那么列数为1的矩阵就是$ \begin{pmatrix}n^k\n^{k-1}\n^{k-2}\...\n^0\S(n-1)\end{pmatrix}$  我们就可以构造一个(k+2)*(k+2)的矩阵$\qquad \begin{pmatrix}C(k,0)&C(k,1)&...&C(k,k)&0 \0&C(k-1,0)&...&C(k-1,k-1)&0\0&0&C(k-2,0)&C(k-2,k-2)&0\.&.&.&.&.\.&.&.&.&.\.&.&.&.&.\0&0&...&C(0,0)&0\C(k,0)&C(k,1)&...&C(k,k)&0\end{pmatrix}$, 组合数可以打表预处理。

 ~~第二种~~

//前置技能：伯努利数(https://zh.wikipedia.org/wiki/%E4%BC%AF%E5%8A%AA%E5%88%A9%E6%95%B0)**\***逆元不可求 //待证

// $B*0=1,且C*{n+1}^0*B0+C{n+1}^1*B*1+...C*{n+1}^n*B_n=0$;

//那么，$B*n=\frac{-1}{n+1}*\sum*{i=0}^{n-1}C_{n+1}^i*B_i\qquad$

//$S(n)=\frac{1}{k+1}*\sum{i=1}^{k+1}C{k+1}^i*B_{k+1-i}*(n+1)^i$

//可以预处理逆元

mod为2^32 不是素数 预处理不可求逆元 伯努利数似乎不可行