# LeetCode 每日一题 4.9 数组中的重复数字

## 一、vector的初始化

~~~c++
vector<int> count ={1,2,3,4,5}	
//用大括号初始化
~~~

## 二、解法

### 1、时间复杂度O（N），空间复杂的O（N）

~~~c++
//借用桶排序的思想，用一个数组记录每个数字出现的次数，超过1的就输出
//优化一下：在每次记录数字出现时，先判断它是不是已经出现过一次了，如果是直接返回，后面的步骤无需进行
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        vector<int> count(nums.size());
        for(int i=0;i<nums.size();i++) {
            if (count[nums[i]]>0) return nums[i];
            count[nums[i]]++;
        }
        return -1;
    }
};
~~~

### 2、时间复杂度O（NlogN），空间复杂的O（1）

~~~java
//原地排序，不需要花费额外的空间

//对每一位，找所需求的对象
class Solution {
    public int findRepeatNumber(int[] nums) {
        int temp;
        for(int i=0;i<nums.length;i++){
            while (nums[i]!=i){										//对每一位进行匹配
                if(nums[i]==nums[nums[i]]){				//看看nums[i]应该去的位置处是否已经匹配
                    return nums[i];								//如果匹配证明出现过两次，是重复数字
                }					
                temp=nums[i];						//如果不匹配，交换当前位置的数字，和它应该去的位置上的数字
                nums[i]=nums[temp];
                nums[temp]=temp;
            }
        }
        return -1;
    }
}

~~~

