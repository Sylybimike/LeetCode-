# LeetCode 每日一题 4.6 删除数组中重复元素

==双指针啦== 

## 一、双指针应用

对于数组问题，指针是抽象的，很多时候用int类型访问下标，也算是指针，效率更高

## 二、解法

~~~c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()==0) return 0;
        int p=0;
        int q=1;
        while(q!=nums.size()){
            if(nums[p]==nums[q]) {q++;continue;}
            else {
                nums[p+1]=nums[q];
                p++;q++;
            }
        }
        return p+1;
    }
};

//优化方向：如果nums[p]!=nums[q],q-p=1，不需要进行替换，因为此时相当于原地替换自己
~~~

**另一个版本 更巧妙**

~~~~c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()==0) return 0;
        int p=0;
        for(int j=1;j<nums.size();j++)	//每次执行完for的判断都会给j++，此处j是快指针
        {
          if(nums[p]!=nums[j]){
            p++;												//“先给p向后挪一位，再赋值”，比“赋值给p的后一位，p++”更通畅
            nums[p]=nums[j];
          }															//如果没进if说明相等，此时应该将快指针向后移，也就是j++
        }
        return p+1;
    }
};
~~~~

