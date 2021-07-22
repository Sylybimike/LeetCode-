# DFS 广度优先搜索

## 1、代码结构（四叉树遍历）

~~~c++
auto main_function(vector<vector<int>>grid){
  for(int i = 0;i<grid.size();i++){
    for(int j = 0;j<grid[0].size();j++){
      if(判断当前点是否满足条件){
        dfs(...);
        附加语句，用于统计或维护最大值
      }
    }
  }
}

auto dfs(...){
  if(当前点不满足条件){
    return;
  }
 	grid[r][c] = 0;//标记当前点已经走过，有两种实现方式，一种是另设数组book标记走过的路，另一种是把当前节点涂成另一个无关值
  //下面四个方向尝试。有两种方式实现
  //一、
  for(int k=0;k<3;++k){
    x = r + direction[k];
    y = c + direction[k+1];
    if(不越界){
      dfs(...)//递归子节点，注意dfs的参数中一定要用能表示「下一层」这样关系的参数
    }
  }
  //二、采用这种方法时，越界条件放在第一个if判断
  dfs(r+1,c,..);
  dfs(r,c+1,..);
  dfs(r-1,c,..);
  dfs(r,c-1,..);
}
~~~

## 2、例题

**#200.岛屿数量 #695.岛屿的最大面积 #547.省份数量**



# 回溯法：深度优先搜索的特例

## 1、代码框架

~~~c++
class Solution {
public:
  //回溯函数
    void back_tracking(vector<int>& nums,int level,vector<vector<int>>& ans){
        if(递归到最后一层){	
            将答案记录下来
            return;
        }
        
        for(int i=level;i<nums.size();i++){
            做决定：交换，加入队列等
            递归调用下一层
            撤销决定：交换回来，退出队列等
        }
    }
	//主函数
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;
        int level = 0;
        back_tracking(nums,level,ans);
        return ans;
    }
};
~~~

## 2、适用范围：排列组合问题、选择问题

==不适用于求最值的问题==

## 3、时间复杂度：比较高

递归算法的时间复杂度取决于递归事件本身✖️调用递归的次数，循环O(N)，递归调用（满树）O(N!)

则整体为O(N!N)

## 4、例题

**#46全排列问题（两种思路，交换并改变原数组和建立新数组记录）**

**#51N皇后问题**

