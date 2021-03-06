---
title: lint109-triangle
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


# problem
[lint109-triangle](http://www.lintcode.com/en/problem/triangle/)

# solution
## 解法1,自上而下递归法
```
    int minimumTotal(vector<vector<int> > &triangle) {
        // write your code here
        if (triangle.empty())
            return 0;
        return dfs(triangle, 0, 0);
    }
    int dfs(vector<vector<int> > &triangle, int i, int j)
    {
        if (i == triangle.size() - 1)//最后一行;
            return triangle[i][j];
        int left = dfs(triangle, i + 1, j);
        int right = dfs(triangle, i + 1, j+1);
        return left < right ? triangle[i][j] + left : triangle[i][j] + right;  
    }
```
### analysis

因为递归导致重复计算，所以会导致超时，可以通过使用缓存数组来减少计算量，通过率53%,total runtime 1211ms

## 解法2, 递归+辅助空间
```
    int minimumTotal(vector<vector<int> > &triangle) {
        // write your code here
        if (triangle.empty())
            return 0;
        vector<vector<int> > nums;
        for (int i = 0; i < triangle.size() - 1; i++)
            nums.push_back(vector<int>(triangle[i].size(), INT_MIN) );
        return dfs(triangle, 0, 0, nums);
    }
    int dfs(vector<vector<int> > &triangle, int i, int j,vector<vector<int> > &nums)
    {
        if (i == triangle.size() - 1)//最后一行;
            return triangle[i][j];
        if (nums[i][j] ！= INT_MIN) return nums[i][j];
        int left = dfs(triangle, i + 1, j, nums);
        int right = dfs(triangle, i + 1, j+1, nums);
        nums[i][j] = left < right ? triangle[i][j] + left : triangle[i][j] + right;  
        return nums[i][j];
    }
```
### analysis
会通过计算。

## 解法3.用循环就能通过
```
    int minimumTotal(vector<vector<int> > &triangle) {
        // write your code here
        if (triangle.empty())
            return 0;
        vector<vector<int> > nums;
        for (int i = 0; i < triangle.size() ; i++)
            nums.push_back(vector<int>(triangle[i].size(), 0) );
        for (int i = 0; i < nums[nums.size()-1].size(); i++)
            nums[nums.size()-1][i] = triangle[nums.size()-1][i];
        //从下往上算一遍;
        for (int i = triangle.size()-2; i >= 0;i --)
        {
            for (int j = 0; j < nums[i].size(); j ++)
                nums[i][j] = nums[i+1][j] < nums[i+1][j+1]?nums[i+1][j]+triangle[i][j]:nums[i+1][j+1]+triangle[i][j];
        }
        return nums[0][0];
    }
```

### analysis
但是依然是全部遍历后打结果，不太智能. 




