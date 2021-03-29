---
title: 高次方程问题总结
date: 2016-11-30T10:36:00.000Z
summary: 形如a^b=c(mod m)的方程有关问题求解(a，b，c在int范围内)
draft: false
featured: false
authors:
  - 阿威
tags:
  - 数论
image:
  filename: ""
  focal_point: ""
  preview_only: false
---
形如a^b=c(mod m)的方程有关问题求解(a，b，c在int范围内)

 1.已知a,b,m求c。
     快速幂 复杂度logb；
     若x较大且b>=m,可以用欧拉定理（指数循环节）来降次

 2.已知a,c,m,求b (可能无解)
     BSGS+hash

~~3.已知b,c,m,求a(可能无解)~~
   ~~求原根+指标+Baby-step+Hash+解模方程+欧拉函数+...(m必须是素数)~~

~~4.已知a,b,c,求某区间范围内的m(可能无解)~~
  ~~不会~~