# LeetCodes每日一题4.5 合并两个有序数组

## 1、条件表达式的简化运用：

~~~C++
Y=a&&b ? A:B;
//当a&&b为真时，Y=A，否则为Y=B
//用此简化if - else语句
~~~

## 2、算法

- 很常见的一种思路是创建一个新数组，用双指针遍历给定的两个数组，再把新数组赋值给nums1

- 缺点：时间复杂度高，感觉空间复杂度也挺高的，需要一个新数组的空间



实现方法：从后往前遍历

1. 比较nums1的最后一位和nums2的最后一位
2. 如果nums1的最后一位大，将nums1的最后一位赋值给nums1数组最大处（m+n-1）
3. 如果nums2的最后一位大，将nums2的最后一位赋值给nums1数组最大处
4. 循环跳出条件：n<0 **当n=-1时意味着数组2已经被清空，退出**
5. ==m=0是可能的，此时仍需要进行赋值操作==



## 3、解法

~~~c++
class Solution {
    public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i =m--+--n;
        while(n>=0) {
            nums1[i--] = m>=0 && nums2[n]<nums1[m]?  nums1[m--]:nums2[n--];
        }   
    }
};
~~~

