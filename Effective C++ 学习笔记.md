# Effective C++ 学习笔记

## 一、构造函数和析构函数

1、虚函数技巧：在base类中采用虚函数，子类继承它可以实现重写

~~~c++
class Father {
  public:
    virtual void getData();
  private:
  ...
}

void Father::getData(){	//这里声明不需要加关键字vitural
  do someding...
}

class Son:public Father{
  public:
  ...
    virtual void getData();
  private:
  ...
}
~~~

利用虚函数，编译器会根据对象的类型自动选择执行base类或者子类的函数

~~~c++
Father* createFather() {
    return new Son;
}
int main() {
    Father* son0 = createFather();//见下方条例2
    son0->getData();
		//调用Son类的getData()
    Son son1;
    son1.getData();
    //调用Son类的getData()
}
~~~

2、使用工厂模式生产指向父类指针指向子类

~~~c++
Father * createFather()
{
  return new Father;	//此处调用默认构造函数
}
~~~

3、成员函数有虚函数时，析构函数声明为virtual

问题：在上例中如果使用detele son0 使用的是父类指针进行内存释放，会导致调用父类的析构函数，从而导致子类的部分成员不能被释放，内存泄露

修改方法：给父类的析构函数加virtual关键字

==当一个类不打算被当作父类时，不应该有virtual的析构函数，也不用该有virtual的成员函数，会导致内存占用==

==换句话来说，只有当一个类拥有virtual成员函数时才使用virtual析构函数==

4、抽象类

抽象类一定会被当作父类使用并被继承，该抽象类不能被实例化，在成员函数和析构函数中，都要采用纯虚函数(pure virtual)

~~~c++
class Father {
  public:
    virtual void getData();
  virtual ~Father() = 0;				//成为纯虚函数
  private:
  	virtual ...
}
//此时必须要为虚函数提供一份定义
Father::~Father(){}
~~~

5、构造函数的行为顺序*：不要在构造函数和析构函数中调用虚函数*

~~~c++
Father::Father() :age(21){
    getData();
}
//即使创造的是子类对象，也会先调用base类的构造函数，且getDate是父类版本
~~~

说明了构造函数的顺序：先调用父类的构造函数构造base类，在此基础上调用子类的构造函数

==注意顺序，先调用父类，再调用子类，注意避免使用虚函数，从而导致我们不想要的结果==

析构函数顺序：先调用子类的析构函数，再调用父类的析构函数

## 二、static、const

1、static关键字：

- local static：在函数内定义的static对象，只被初始化一次，后续再次调用函数时，使用的仍然是这个对象
- non-local static：修饰全局变量时，表示该变量只能被此文件使用，其他文件不允许使用

2、