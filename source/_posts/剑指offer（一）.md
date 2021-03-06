---
title: 剑指offer（一） #标题
categories: 剑指offer #分类，可多个；若单个去掉括号
tags: [查找, 替换空格, 打印链表] #标签，可多个；若单个去掉括号
mathjax: true #是否引用公式
kewords: #本文关键词
description: #本文描述，若为空就自动全文前150字)
copyright: true #是否需要版权申明，默认有
reward: true #是否需要打赏，默认有
toc: true #是否需要目录，默认有
password: #是否加密，为空不加密
date: 2018-1-29 16:09:02 #日期
---


# 二维数组中的查找
在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

算法思想：
1. 由于数组从左到右，从上到下都是递增，可以从右上角或者左下角开始查找，这里从右上角开始查找
2. 定义数组array，行i，列j，目标target。
3. 若`array[i][j]`==target,那恭喜你找到目标；
4. 若`array[i][j]`>target,那向左去找目标--j；
5. 否则，`array[i][j]`小于target,那向下寻找目标++i；


```C++
class Solution{
public:
    bool Find(int target,vector<vector<int> > array){
        if(array.size()!=0)
        {
              int i=0;
              int j=array[0].size()-1;
              while(i< array.size()&& j>= 0)
              {
                  if(array[i][j]== target)
                        return true;
                  else if(array[i][j]>target)
                        --j;
                  else
                        ++i;
               }
        }
    return false;
    }
};
```

# 替换空格
请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy

算法思想：
1. 定义字符串下标i（i=0开始），定义空格bankNum,遍历字符串并计算空格个数；
2. 总字符串=原始字符串下标+1+2*bankNum；
3. 末尾字符串下标=totalNum-1，也就是我们说的放置位置；
4. 总体来说：从后向前遍历字符串，如果遇到空格，就加%20；没有空格，就将原字符串的最后一个字符赋给新字符串

```C++
class Solution{
public:
    void replaceSpaca(char *str,int length)
    {
        int bankNum=0;
        int i=0;
        for(;str[i]!='\0';++i)
        if(str[i]==' ')
        ++bankNum;
    }
    int totalNum=i+1+2*bankNum;
    int pos=totalNum-1;
    for(;i>=0;--i)
    {
        if(str[i]==' ')
        {
            str[pos--]='0';
            str[pos--]='2';
            str[pos--]='%';
        }
        else
            str[pos--]=str[i];
    };

    

}
```

# 打印链表
输入一个链表，从尾到头打印链表每个节点的值。

```python
class Solution:
    def printListFromTailToHead(self,listNode):
        l=[]
        head = listNode
        while head:
            l.insert(0,head.val)
            head=head.next
        return 1
```

# 二分查找

```python
def search2(a,m):
    low=0
    high=len(a)-1
    while(low<=high):
        mid=(low+high)/2
        midval=a[mid]

        if midval<m:
            low=mid+1
        else if midval>m:
            high=mid-1
        else 
            return mid
    return -1

    if __name__=="__main__"
       a=[1,2,3,4,5,6,7,8,9]
       m=5
       result=search2(a,m)
       print result
```
下面这个程序就会陷入无限循环while中
```C++
#include<studio.h>
int bsearch(int a[],int n,int v)
{
    int left, middle, right;
    left=0, right=n-1;
    while(left<=right)
    {
        middle=left+(right-left)/2;
        if(a[middle]>v)
        {
        right=middle
        }
        else if(a[middle]<v)
        {
        left=middle
        }
        else
        return middle;  
    }
    return -1;
}
```
以下是正确写法
```C++
public static int binarySearch(int[] a,int n,int x)
{
    if(n>0 && x>=a[0])
    {
        int left=0,right=n-1;
        while(left<right)
        {
            int middle=left+(right-left)/2;
            if(x<a[middle])
            right=middle-1;
            else 
            left=middle;
        }
        if(x==a[left])
        return left;
    }
    return -1;
}
```
# 重建二叉树
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
```
# -*- coding:utf-8 -*-
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        # write code here
        if len(pre) == 0:
            return None
        root = TreeNode(pre[0])
        pos = tin.index(pre[0])
        root.left = self.reConstructBinaryTree( pre[1:1+pos], tin[:pos])
        root.right = self.reConstructBinaryTree( pre[pos+1:], tin[pos+1:])
        return root
```
