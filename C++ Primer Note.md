# C++ Primer

### chap01
+ 可以使用`while (std::cin>>value)`来读取所有输入

### chap02
+ 如果给一个无符号整数超过它表示范围的值，将会得到一个对无符号数总数取模的余数，如果对一个有符号整数做同样的操作，结果是未定义的
+ 混用无符号数和有符号数时，有符号数会自动转换为无符号数，如果有符号数的值是负的，那么结果很有可能是错误的
+ C++11全面引入列表初始化，列表初始化过程中，如果可能造成信息丢失，那么编译器将报错
+ 嵌套作用域中已经存在变量覆盖全局作用域变量时，可以用`::reused`语法获取全局变量
+ 引用即别名，一旦与变量绑定就不能改变，所以引用必须初始化
+ C++11中，定义了`nullptr`作为空指针字面量
+ `void*`指针因为指向的数据类型未知，所以功能受限
+ 指向指针的引用 `int *p,int *&r=p`,其中`r`就是指针`p`的引用
+ 类型别名 `using SI = Sale_Item;`
+ 使用`constexpr`来让编译器确定变量值是否是常量表达式

### chap03

##### string
+ 直接初始化 and 拷贝初始化

``` C++
string s1 //默认是空串
string s2(s1) // s2是s1的副本
string s3 = s1
string s4("value")
string s5 = "value"
string s6(n, 'c')
```

##### vector
+ 初始化

``` c++
vector<T> v1
vector<T> v2(v1)
vector<T> v3(n, val)
vector<T> v4(n)
vector<T> v4{a,b,c,...}
vector<T> v5={a,b,c,...}
```

+ 不允许通过下标来添加元素



### const
`const` 用于声明变量是不可以改变的，因此必须初始化，由编译器进行全局替换
默认情况下,`const`是只在文件内有效的，如果希望`const`在多个文件中有效，需要使用`extern`关键字，无论是声明还是定义都需要添加该关键字

###### 常量引用
对于`const`限定的常量，只可以用常量引用来绑定
```C++
const int ci=1024;
const int &r1=ci; //常见形式
```
上面的代码中，无论是ci还是r都是不可改变的
```C++
int a=1;
const int &r1=a;
```
这份代码也是合法的，a是可变的，并且这种变化会反应在r1上，`const`唯一的限定是不可以通过r1来改变a的值

常量引用初始化时不要求类型一致，只需要可以表达式可以转换为常量引用的类型

同上，对于`const`限定的常量，只能用常量指针来指向
常量指针不可以用来改变指向的对象

`const int *const curErr=&errNumb`表示指针curErr是一个指向常量的指针（虽然实际上该常量可以通过其他方式改变），不可以用来改变errNumb的值，同时它作为一个对象，是不可以改变的，换言之，它必须始终指向errNumb  
读取该指针类型时，可以从左往右  
`const int *const pip`  
pip首先是一个常量，其次是一个指针，指向的是一个const int  
左边的`const`是底层const，右边的`const`是顶层const  
拷贝对象时，顶层const和底层const有明显区别，如下  
```C++
const int *p=a;
int *p2=p;//error!
```
p2是无限制指针，而p具有底层const，拷入拷出时，两个对象必须具有同样的底层const资格，或者两者可以互相转换
