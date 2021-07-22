# LeetCode 每日一题 435 去除不重复区间

## 一、牛逼的sort函数和lambda表达式

~~~c++
template <class RandomAccessIterator, class Compare>
void sort (RandomAccessIterator first, RandomAccessIterator last, Compare comp);
//分别传入排序的起点和终点，默认升序，这个上次做题用过
//第三个参数是比较规则，一般写一个返回值为bool的函数传进来
//这里使用lambda表达式
[](vector<int> &a,vector<int> &b){
  return a[1]<b[1];
}
//第一个大括号传入=时，可以按值使用lambda所在类的所有局部变量，一般就用它
//第二个小括号传入参数，可以穿引用/非饮用
~~~

## 二、解法

贪心算法：

![image-20210413225829095](/Users/apple/Library/Application Support/typora-user-images/image-20210413225829095.png)

1. 进行按右边界增序排列
2. 贪心思路：选择右边界尽可能小的区间，以便给后续序列留有空间==（求至少删除多少个，那么保留的序列尽可能多）==
3. 在此基础上，筛选重复序列并删掉
   - 设置第一个比较数：intervals[0] [1]，并且从第二个区间开始比较
   - 比较当前区间左端点是否小于比较数，如果是说明重合了，删掉不要，计数器++
   - 如果不是，更新比较数为当前比较数的右边界，并更新当前区间

~~~c++
class Solution {
        public:
        int eraseOverlapIntervals(vector<vector<int>>& intervals) {
            if(intervals.empty()) return 0;	//排除异常数据，很重要
            sort(intervals.begin(),intervals.end(),[](vector<int> &a,vector<int> &b){
                return a[1]<b[1];						//lambda表达式
            });
            int del=0;
            int prev = intervals[0][1];
            for(int i=1;i<intervals.size();i++){
                if(prev>intervals[i][0]) del++;
                else prev=intervals[i][1];
            }
            return  del;
        }
};
~~~

