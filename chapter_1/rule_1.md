#### 把 C++ 看成多个语言的集合
支持多种编程范式:
- 过程
- 面向对象
- 函数式
- 泛型
- 元编程
四种语言:
- C. 语言块,语句,预处理,内置数据类型,数组,指针.
- 面向对象 C++. 类,包括构造函数,析构函数;封装,继承,多态,动态绑定等等.
- Template C++. 模版元编程.
- STL. template程序库,包含容器,迭代器,算法和函数对象.

高效:
C: pass-by-value比pass-by-reference高效
面向对象,template: pass-by-reference-const更好
STL:是用c指针pass构造出来的,所以pass-by-value更好
