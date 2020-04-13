# LeetCode 523

## 题目描述
给定一个包含非负数的数组和一个目标整数 k，编写一个函数来判断该数组是否含有连续的子数组，其大小至少为 2，总和为 k 的倍数，即总和为 n*k，其中 n 也是一个整数。

示例 1:

输入: [23,2,4,6,7], k = 6
输出: True
解释: [2,4] 是一个大小为 2 的子数组，并且和为 6。
示例 2:

输入: [23,2,6,4,7], k = 6
输出: True
解释: [23,2,6,4,7]是大小为 5 的子数组，并且和为 42。

## 思路解析
重要的降低时间复杂度，常规暴力算法一般都能想到。主要思路是hash,前缀和以及模相等。如示例1,前缀和数组为[0,23,25,29,35,42],其中mod(25,6)==mod(29,6)。注意k==0以及一些边界处理。

## 代码
```
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        
        if (k==0) {
            
            for (int i = 1; i < nums.size(); ++i) {
                if (nums[i] == 0&& nums[i-1] == 0) return true; 
            }
            
            return false;
        }
        
        map<int,int> sum_index_map;
        int sum = 0;
        sum_index_map.insert(pair<int,int>(0,-1));
        
        for (int i = 0; i < nums.size(); ++i) {
            
            sum += nums[i];
            sum = sum%k;
           
            map<int,int>::iterator iter = sum_index_map.find(sum);
            if(iter != sum_index_map.end()) {
                    if (i-iter->second > 1) return true;
                }
             
            else
            {
                sum_index_map.insert(pair<int,int>(sum,i));
            }
        }
        
        return false;
    }
};
```