# Segment Tree
## 用来解决什么问题
给定一个长度为 n 的序列，需要频繁地求其中某个区间的最值，以及更新某个区间的所有值, 
可以logn求区间最大，最小， rangeSum等

<img src="../assets/segment_tree.png" width="300" />

## 常用method
1. 单点修改 (logn) update(index, value)
2. 区间修改(这里需要用到lazy propogation来优化到logn, 完全不在面试 范围)
3. 区间查询(logn 区间求和，求区间最大值，求区间最小值，区间最小公倍 数，区间最大公因数) rangeSum(i, j) 一般为[i, j]

## 实现
- tree指针实现的线段树
- zkw线段树

## 
一般求rangeSum可以考虑用Binary Index Tree或者preFix sum解决