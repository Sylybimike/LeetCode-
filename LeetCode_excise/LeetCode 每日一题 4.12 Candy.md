# LeetCode 每日一题 4.12 Candy

## 一、vector的初始化：全为1

~~~c++
vector<int> vec1(ex.size(),1);
//传入两个参数，第一个是数组的长度，第二个是数组的元素
~~~

## 二、计算数组中所有元素的和

~~~c++
accumulate(vec1.begin(),vec1.end(),org);
//首指针，尾指针，累加的初始值（一般为0）
~~~



## 三、解法

思路就是贪心算法

- 先左遍历，让他满足左规则
- 右遍历，满足右规则

做法

1. 左遍历：如果当前元素大于它左边的元素，将自身的candy置为左侧元素candy+1
2. 右遍历：如果当前元素小于它左边的元素，且当前元素的candys量不少于它左边元素的candys，将左边元素的candys置为自身的candys+1

~~~
class Solution {
public:
    int candy(vector<int>& ratings) {
        vector<int> candys(ratings.size(),1);
        for(int i =1;i<ratings.size();i++){
            if(ratings[i-1]<ratings[i]) candys[i]=candys[i-1]+1;
        }
        for(int j=ratings.size()-1;j>0;j--){
            if(ratings[j]<ratings[j-1]&&candys[j]>=candys[j-1]) candys[j-1]=candys[j]+1;
        }
        return accumulate(candys.begin(),candys.end(),0);
    }
};
~~~

