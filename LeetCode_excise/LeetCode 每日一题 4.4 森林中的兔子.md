# LeetCode 每日一题4.4森林中的兔子

## 1、哈希表

1. 哈希函数：将键值对的键通过一定规则转化为数组下标，将键值对放入该数组中
2. 哈希冲突：两个不同的键值对，通过哈希函数得到相同的结果
3. 哈希冲突解决办法：拉链表、开放定制法……
4. 封装类的使用：unordered_map

~~~C++
//class unordered_map
//创建
unordered_map<int,int> item;

//初始化:可以用={(a,b)}初始化
//可以通过遍历另一个数组初始化：
for(auto m :count){item[m]++;}

//迭代器：指针
auto ptr = item.begin();

//最牛逼的功能：find,给出键值k，返回指向该Entry的指针
iterator find ( const key_type& k );
unordered_map<string,double>::const_iterator got = myrecipe.find ("coffee");
cout<<got.second()<<endl;		//second访问键值对中的值

//https://blog.csdn.net/lizhengze1117/article/details/96728468
~~~

## 2、向上取整算法

~~~C++
void ceil(float n) //返回不小于n的最小整数（即向上取整）
void floor(float n)//向下取整
~~~

$$
Math: \\
[\frac x y]=\frac{x+y-1}{y}=\frac{x+y}{y+1}
$$



