#### 尽可能使用 const
- 如果 const 出现在星号左边，表示被指物是常量；如果出现在右边，表示指针自身是常量；如果出现在两边，表示两者都是常量。
- 如果被指物是常量，const 在类型之前或之后都一样。
    void f1 (const Widget* pw); // f1 获得一个指向常量的 Widget 对象
    void f2 (Widget const * pw); // f2 相同
- STL 迭代器是以指针塑造出来的。
    T× const；// 表明迭代器不能指向不同的东西，但所指的值是可以改变的。
    const T×；// 所指的东西不可被改动。

    std::vector<int> vec;
    ...
    const std::vector<int>::iterator iter = vec.begin();// iter 的作用像个 T× const
    *iter = 10;  //可以改变 iter 所指物。
    ++iter;  // 错误，iter是const
    std::vector<int>::const_iterator = cIter = vec.begin();// cIter 的作用像个 const T×
    ×cIter = 10;  // 错误，×cIter 是 const
    ++cIter；    // 正确。

总结：
- 将某些东西声明为 const 可帮助编译器侦测出错误用法。
。。。
