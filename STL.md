#### vector( #include  < vector >)

​	vector的它能够像容器一样存放各种类型的对象，简单地说，vector是一个能够存放任意类型（包括结构体）的动态数 组，能够增加和压缩数据

``` c++
vector<Type>v;  //创建动态数组
vector<int>v[131]; //一维长度为131，二维为动态大小的数组
vector<vector<Type>>v; //一维二维都是动态大小数组
struct rec{....} => vector<rec>v; //结构体的动态数组
Type v[index]; //利用[]来访问v中第index的元素
vector<int>v(int n,int elem); //开辟大小为n，并初始化为elem；
vector<int>v(10,0);//开辟大小为10，并初始化为0；
vector<int>v(10);//开辟大小为10的空间；
v.push_back(item);//在v的最后添加item；
v.pop——back(item);//将v的最后元素删去
v.resize(int n);//为v重新开辟大小为n的空间，并初始化为0；
v.resize(10);//为v开辟大小为10的空间，并初始化为0
v.front();//返回v最前面的元素(返回首元素的引用)
v.back();//返回v最后面的元素（返回尾元素的引用）
v.size();//返回v的元素的个数  
v.clear();//清空v中的元素；
v.empty();//判断v是否为空，返回的是bool值；
v.begin();//返回首迭代器，指向第一个元素（相当于指针）<=>v[0];
v.end();//返回尾迭代器，指向最后一个元素的下一个位置， <=>*--v.end() = v.back() = v[v.size()-1]
v.insert(iterator it,Type x); //向迭代器指向元素前增加元素x
v.erase(iterator it);//删除迭代器所指向的元素
v.erase(pos1,pos2)//删除[pos1,pos2)区间中迭代器相对应的元素
v.insert(v.begin()+3,666);//在v[3]前增加一个元素666；
v.erase(v.begin()+3);//删除v[3];
//遍历方法
for(int i=0;i<v.size();++i) v[i];
for(auto x:v) i;
for(vector<int>::it = v.begin();it != v.end();it++) *it;
```

##### 	关于迭代器

​	迭代器就像STL容器的“指针”，可以用星号*操作符解除引用。

```c++
vector<int>::iterator it = v.begin(    );//其中it相当于指针
cout<<*it<<endl;//*it代表v[0]的值
it++;
cout<<*it<<endl;//此时*it代表v[1]的值；
```

​	vector的迭代器是“随机访问迭代器”，可以把vector的迭代器与一个整数相加减，其行为和指针的移动类似。可以把vector的两个迭代器相减，其结果也和指针相减类似，得到两个迭代器对应下标之间的距离。

#### 队列和栈（#include < queue >    #include < stack >）

##### 队列

​	queue只能在容器的末尾添加新元素，只能从头部移除元素。(先进先出) stack 只能在栈顶插入元素，也只能在栈顶取出元素（先进后出）

​	头文件queue主要包括循环队列queue和优先队列priority_queue两个容器。

```c++
//queue创建方法
queue<Type>q //创建一个存放数据类型为Type（也可为结构体）的队列q
q.push(item);//在q最后添加一个为Type类型的item；
q.pop();//使q最前面的元素出队，不获取该元素
q.front();//获取队列最前面的元素
q.back();//获取队尾元素
q.size();//返回q中元素的个数
q.empty();//判断队列q是否为空，返回bool值
```

##### 优先队列

```c++
priority_queue //出队顺序与插入顺序无关，与数据优先级有关，本质是堆
priority_queue<Type,container,functional>q;
/*
type是数据类型
Container是存放数据的容器，默认用的是vector
Functional是排序顺序
*/
//大跟堆
priority_queue<int>a;//基础类型，默认是大根堆
<=>prioity_queue<int,vector<int>,less<int>>q;
//小根堆
priority_queue<int,vector<int>,greater<int>>q;
q.push(item);//在q中添加一个元素；
q.top();//返回最大元素（大根堆）//最小值（小根堆）
q.pop();//使最大元素（大根堆）//最小值（小根堆）出队
q.size();//返回q的元素个数
q.empty();//判断队列是否为空
//pair 比较
priority_queue<pair<int,int>>q//先比较第一个，如果第一个相等再比较第二个（第一个 int 为frist，第二个 int 为second）
/*
priority_queue中的存在元素，如果是结构体这样无法比较的类型，必须重载运算符，相当于先使得优先队列中的元素进行比较再建立q
*/
struct Rec{
    int x,y;
    bool operator<(const&Rec t)const{
        return x<t.x
    }
}//大根堆重载小于号，小根堆重载大于号
<=>
struct Rec{
	int x,y;
    bool operator<(Rec a,Rec b){
        return a.x<b.x;
    }
}
```

##### 栈

```c++
stack<Type>s;//建立一个存放数据类型为Type（可以为结构体）的栈
s.push(item);//在栈顶添加一个类型为Type的item
s.pop();//使栈顶的元素出栈
s.top();//获取栈顶元素
s.empty();//判断栈是否为空
s.size();//获取栈中的元素个数
```

#### 双向队列 （#include < deque >）

​	双端队列是支持在两端高效插入和删除元素的连续性存储空间，它就像 queue 和 vector 的结合，与 vector 相比，deque在头部增删元素仅需要O(1)的时间；与 queue 相比，deque可以像数组一样支持随机访问（迭代器也和vector一样，支持运算）

```c++
deque<Type>dq;//创建一个存放Type数据类型的双端队列
deque<Type>dq(10,5);//构造10个值为5的双端队列
Type dq[index];//访问dq中第index的元素
dq.begin()/end();//返回头尾迭代器
dq.front()/back();//获取头尾元素的值
dq.push_back(item)/pop_back();//从队尾进队和出队
dq.push_front(item)/pop_front();//从队头进队和出队
dq.clear();//清空dq中的元素
dq,size();//获取dq中元素个数
dq.empty();//判断dq是否为空
dq.resize(n,elem(可有可无));//重新指定容器长度为n,用 elem 填充（如果没有，则初始化为0）
deque<int>dq(begin,end);//利用迭代器构建双端队列
deque<int>dq(arr,arr+sizeof(arr)/sizeof(arr[0]));//利用数组构建双端队列
```

#### set (用相应的头文件，内部红黑树)

​	集合set是一种包含对象的容器，可以快速地查询元素是否在集合中，set中所有元素是有序的，且只能出现一次，因为set中的元素是有序的，所以存储的元素必须定义过<运算符（因此如果想在set中存放struct的话必须手动重载<运算符，和优先队列一样）

```c++
//与set类似
multiest //元素有序可以出现多次
unordered_set//元素无序只能出现一次
unordered_multiestl//元素无序可以出现多次
//建立方法
set<type>s;<=>set<int,less<int>>s;//结构体必须重载小于号，默认升序
set<int,greater<int>>s;//这是降序，结构体必须重载大于号
//遍历方法
for(auto i:s) i;
s.insert(item);//在s中插入一个元素
s.clear();//清空s；
s.empty();//判断s是否为空
s.size();//返回s中元素个数
s.find(item);//在s中查找一个元素并返回相应的迭代器，找不到则返回是s.end();
s.count(item);//返回s中item的个数
s.erase(item);//删去s中item，入迭代器也可删去迭代器
s.erase(pos1,pos2)//删除[pos1,pos2)区间中迭代器相对应的元素。
s.end();//返回尾迭代器，*--s.end()是指集合中最大的元素
s.begin();//返回尾迭代器，*s.begin()是指集合中最小的元素
s.lower_bound(item);//返回大于等于item的元素迭代器，找不到返回s.end();
s.upper_bound(item);//返回大于item的元素迭代器，找不到返回s.end();
/*
set和multiset的迭代器称为“双向访问迭代器”，不支持“随机访问”，支持星号*解除引用，仅支持++和--两个与算术相关的操作。

设it是一个迭代器，例如set<int>::iterator it;

若把it ++，则it会指向“下一个”元素。这里的“下一个”元素是指在元素从小到大排序的结果中，排在it下一名的元素。同理，若把it --，则it将会指向排在“上一个”的元素。
如果是unordered_set/map等不支持迭代器++和--；
*/
```

####  map(用相应的头文件，内部红黑树）

​	map是按照特定顺序存储由key和value，map中元素按照key进行排序，每个key都是唯一的，并对应着一个value，value可以重复（遇到无法比较的，也要定义小于号）

```c++
//与map相似
unordered_map(哈希表)，区别在于不是按照顺序排序
//遍历方法
for(auto i:mp)
cout << i.first << ' ' << i.second << endl;
//建立方法
map<key_type, value_type> name;
unordered_map<key_type, value_type>
size/empty/clear/begin/end()//均与set类似。
mp.count(key)//在 mp 中查找 key 的数量，因为 map中 key 唯⼀，所以只会返回 0 或 1 O(logn)
mp.find(key)//在 mp 中查找⼀个 key 并返回其 iterator，找不到的话返回 s.end() O(logn)
mp[key]//返回 mp 中 key 对应的 value。如果key 不存在，则返回 value 类型的默认构造器(defaultconstructor)所构造的值，并该键值对插⼊到 mp 中O(logn)
mp[key] = xxx//如果 mp 中找不到对应的 key 则将键值对 (key: xxx) 插⼊到 mp 中，如果存在 key 则将这个 key 对应的值改变为 xxx O(logn)
insert()/ erase()//与set类似，但是参数是pair<Type,Type>;
lower_bound()/upper_bound()//与set类似
```

#### pair

```c++
pair<int, int>
first, 第一个元素
second, 第二个元素
支持比较运算，以first为第一关键字，以second为第二关键字
```

