#### 尽量以 const, enum, inline 替换 #define
如：
    #define ASPECT_RATIO 1.653
替换为：
    const double AspectRatio = 1.653;
有两个优点：
1. 出错时，能显示地显示变量名；
2. 预处理器盲目地将 ASPECT_RATIO 替换为 1.653，代码所占存储空间更大。


#### 特殊情况
1. 定义常量指针
常量定义通常放在头文件中，便于共享。
如：定义一个常量 char×-based 字符串
    const char* const authorName = "Scott Meyers";
string 对象通常比 char×-based 更好
    const std::string authorName("Scott Meyers");
2. class 专属常量
将常量作用域限制于 class，并且只有一份实体
    class GamePlayer {
    private:
        static const int NumTurns = 5;
        int scores[NumTurns];
        ...
    };
对于 class 中 静态的整数类型，上面只是 NumTurns 的声明，C++要求所有东西都要提供定义式。
    const int GamePlayer::NumTurns;
而 #define 无法提供封装性。

使用 enum hack，可当成静态的int类型使用
class GamePlayer {
private:
    enum { NumTurns = 5 };
    int scores[NumTurns];
    ...
};
有两个特点：
- 比较像 #define
- enum 是模板元编程的基础
常见的 #define 误用情况是实现宏的时候
    #define  CALL_WITH_MAX(a,b) f((a) > (b) ? (a) : (b))
    int a = 5, b = 0;
    CALL_WITH_MAX(++a, b);    // a 被累加两次
    CALL_WITH_MAX(++a, b+10); // a 被累加一次
可利用 template inline 方法替代宏，避免出现错误
template<typename T>
inline void callWithMax(const T& a, const T& b)
{
    f(a > b ? a : b);
}
// 由于不知道 T 是什么，所以采用 pass by reference-to-const
// a 和 b 较大的数，调用 f 函数。
