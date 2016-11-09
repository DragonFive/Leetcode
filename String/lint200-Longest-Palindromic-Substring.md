---
title: lint200-Longest-Palindromic-Substring
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---

# 题目来源 

## 相似题目


# 解法 

## 寻找最长公共字串 
```cpp
    string longestPalindrome(string& s) {
        // Write your code here
        if (s.empty())
            return s;
        string t = s;
        std::reverse(t.begin(), t.end());
        int len = s.length();
        vector<vector<int> > lenVec =  vector<vector<int> >(len + 1, vector<int>(len + 1, 0));
        for (int i = 0; i < len; i++)
            for (int j = 0; j < len; j++)
                if (s[i] == t[j])
                    lenVec[i + 1][j + 1] = lenVec[i][j] + 1;
        int maxLen = 0, endIdx = 0;
        for (int i = 0; i <= len; i++)
            for (int j = 0; j <= len; j++)
                if (lenVec[i][j] > maxLen)
                {
                    maxLen = lenVec[i][j];
                    endIdx = i - 1;
                }    
        return s.substr(endIdx - maxLen + 1, maxLen);                    
    }
```


## 


