# LeetCode 每日一题4.10 二维数组中的查找问题

## 一、C++ 二维数组

### 1、初始化

~~~c++
vector<vector<int>>m = {{1,2,3},{4,5,8},{5,9,16}};
//用大括号初始化
~~~

### 2、矩阵大小

~~~c++
//访问矩阵行数：第一层数组储存行向量
matrix.size();
//访问矩阵列数
matrix[0].size();
~~~

## 二、算法

### 1、将图旋转45度，用二叉树查找

### 2、从右上角开始查找

跟我的思路其实比较像了，不过我的是从左上角开始找，不能一下排除一行或者一列

==注意：要考虑空矩阵的情况，空矩阵直接返回false==

**基本思路**

- 从右上角开始查找，如果等于，返回true，否则：
- 如果当前位置元素大于target，则该列下面的所有元素都不用再查找了（因为一定也大于target），向左走
- 如果当前位置元素小于target，则该列下面有可能有相等元素，向下走
- 重复上述过程，直到达到边界（返回false）或找到目标（返回true）

~~~c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if (matrix.size()==0) return 0;
        int x=0,y=matrix[0].size()-1;
        while(x<matrix.size()&&y>=0)		//这里循环结束条件要额外注意：例如一个3x3的矩阵，size是3
        {																//所以x，y取值范围是0-2，y判断条件包含0，x判断条件不包含3
            if(matrix[x][y]==target) return true;
            if(matrix[x][y]>target) y--;
            else x++;
        }
        return false;
    }
};
~~~

