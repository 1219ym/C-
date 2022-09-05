#### 1，命名空间将全局作用域分成不同的部分

#### 2，不同命名空间中的标识符可以同名而不会发生冲突

#### 3，命名空间可以发生嵌套

#### 4，全局作用域也默认命名空间

### 语法

```c++
namespace Name
{
    /*******/
    namespace Internal
    {
        /******/
    }
    /******/
}
```

#### c++命名空间的使用

```c++
/*、
1，使用整个命名空间 using namespace name
2，使用命名空间中的变量 using name::variable
3，使用默认命名空间中的变量： ::variable
*/
```

```c++
#include <stdio.h>
#include <iostream>
namespace First 
{
	int i = 0;
}
 
namespace Second
{
	int i = 1;
 
	namespace Internal //嵌套命名空间
	{
		struct P  //嵌套命名空间
		{
			int x;
			int y;
		};
	}
}
 
int main()
{
	using namespace First; //使用整个命名空间
	using Second::Internal::P;  //使用嵌套的命名空间
 
	printf("First::i = %d\n", i);
	printf("Second::i = %d\n", Second::i);  //使用命名空间中的变量
 
	P p = { 2, 3 };
 
	printf("p.x = %d\n", p.x);
	printf("p.y = %d\n", p.y);
 
	system("pause");
	return 0;
}
```



#### using 指令

​	可以使用 using namespace 指令避免使用名称空间前置，该指令告诉编译器后续代码正在使用指定命名空间中的名称

#### std的命名空间

​	下列代码可以引用 cout 不预先添加命名空间（库里有的不需添加）

```c++
#include <iostream>
using std::cout;
 
int main () {
   cout << "std::endl is used with std!" << std::endl;
   
   return 0;
}
```

 