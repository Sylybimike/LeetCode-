# LeetCode 每日一题 4.11 分发饼干

# 一、数组的排序操作

~~~c++
vector<int> test={3,4,1,2};
sort(test.begin(),test.end());
//sort的参数是两个指针，分别是数组的头部和尾部，第三个参数可以传一个函数作为比较规则，默认从小到大
~~~

## 二、解法

思路：

- 饥饿度最低的孩子优先度最高（因为把饥饿度高的喂饱了可能就没有饼干了）
- 给饥饿度最低的孩子喂能满足条件的饼干中最小的一个
- 直到饼干无了，返回孩子数量

实现：

- 先将两个数组排序（sort）
- 如果当前指向的饼干大小大于孩子的饥饿度，喂给他，两个指针都向右移动
- 如果当前指向的饼干大小小于等于孩子的饥饿度，说明饼干不够大，饼干指针向右移动，孩子指针不动

~~~c++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        if (s.size()==0){return 0;}
        sort(g.begin(),g.end());
        sort(s.begin(),s.end());
        int child = 0;
        int cookie = 0;
        while (child<g.size()&&cookie<s.size()){
            if(g[child]<=s[cookie]) child++;
            cookie++;
        }
        return child;
    }
};

~~~

