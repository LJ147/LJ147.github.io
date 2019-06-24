---
title: leetcode 每周练习(1)
tags:
  - LeetCode
  - 刷题
  - 并查集
date: 2019-06-02 14:49:58
updated: 2019-06-02 14:49:58
categories: 算法
description: 整理、汇总

---

LeetCode 练习

<!-- more -->



# 1. LeetCode 721 账户合并

链接：https://leetcode-cn.com/problems/accounts-merge/

分析：需要用到并查集，记住就好了。

解法1：



``` c++
class Solution {    
public:
    vector<int> par; 
    vector<int> rank;  
    
    int find(int x){
       if(x == par[x]){
           return x;
       }else{
           return par[x] = find(par[x]);
       }
    }

    void merge(int x,int y){
        x = find(x);
        y = find(y);
        if(x == y) return ;
        if(rank[x] == rank[y]) rank[x]++;  
        if(rank[x] > rank[y]) par[y] = x;   
        else par[x] = y;                     
    }
    
    vector<vector<string>> accountsMerge(vector<vector<string>>& accounts) {
        vector<vector<string>> reaccounts;  
        int n = accounts.size();
        if (!n) {
            return reaccounts;
        }
        for (int i = 0; i < n; i++){
            par.push_back(i);
            rank.push_back(1);
        }
        map<string,int> m;  
        for (int i = 1; i < accounts[0].size(); i++){
            m[accounts[0][i]] = 0;
        }
        for(int i = 1;i < n;i++){
            for(int j = 1;j < accounts[i].size();j++){
                if(m.find(accounts[i][j]) != m.end()){
                    merge(m[accounts[i][j]],i); 
                }else{
                    m[accounts[i][j]] = i;
                }
            }
        }
       
        map<int, vector<string>> man;   //姓名+邮箱的 账户集合
        for (auto &it:m){    //遍历邮箱和行号的 映射集合
            int k = find(it.second);
            if (man.find(k) == man.end()){   //没有该账户时才新增账户
                man[k].push_back(accounts[k][0]);
            }
            man[k].push_back(it.first); //添加邮箱到集合
        }
        for(auto & it:man) {
            reaccounts.push_back(it.second);   
        }
        return reaccounts;
    }
};
```



时间复杂度：

空间复杂度：




