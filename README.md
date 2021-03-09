
# 2.1 基本内置类型 · c++

```text
bool，char
wchar_t，char16_t，char32_t
short，int，long
long long
float，double，long double
[-128, 127]
[0, 255] 8bit
[0, 65535] 16bit
[-32768, 32767] print 32768 == -32768
[0, 4294967295] 32bit
(int)4294967296 == 0
(int)4294967295 == -1
(int)4294967294 == -2
[-2147483648, 2147483647]
(int)2147483648 == -2147483648
```

c++标准规定了最小尺寸

* bool : 未定义，只能用sizeof\(bool\)来判断
* char : 8
* wchar\__t、chat16\_t、short、int : 16_
* char32\_t、long : 32
* long long : 64
* float : 32，6位有效数字，通常是7位
* double：64，10位有效数字，通常16位
* long double : 96或128，10位有效数字，常用于特殊硬件

符号

* bool、wchar_t、char16\_t、char32\_t 无符号_
* unsigned int == unsigned
* char 是由编译器决定是unsigned char 还是 signed char
* char、signed char、unsigned char 三种

**如何选择类型？**

* 明确知道是正、用 unsigned
* int 或者 long long
* 算数表达式不要用 char 或者 bool，因为 char 的符号是编译器决定的
* 浮点数：double
  * 有些机器上 double 比 float 快
  * long double 运行时消耗大

类型转换convert

```text
unsigned char c = -1; 
signed char c = 256; 
```

* 浮点型 = 整型，整型空间如果超过了浮点型的容量，精度会损失
* 无符号 = 超出范围，初始值对无符号类型表示数值总数取模后的余数，\(-1 + 256\) % 256
* 有符号 = 超出范围，未定义undefined，可能继续工作、可能崩溃、可能生成垃圾数据
* 算数表达式，倾向于，统一成无符号数，所以表达式里有unsigned，int 会变成unsigned

> **避免无法预知和依赖环境的行为!!!**

整型浮点型字面值常量 literal

* 十进制带符号，类型是int, long, long long中最小的
* 8和16进制不一定，类型是int, unsigned int, long, unsigned long, long long, unsigned long long 中最小的
* short没有字面值
* 严格的说，十进制都是unsigned的，负号不在字面值内，取负而已
* double，3.14E0 0. 0e0 .001

字符型

* 字符串末尾'\0'，长度+1
* 不能用%s 打印 char
* '22' : 0x3232 不通过
* 'text' : 0x74657374 == 1952805748
* c = 'abcd'; %c 只显示 d

```text
cout << "this is a test, this "
        "is a new line" << end; 
```

转义符

| 换行符 \n | tab 建 \t | 报警 \a |
| :--- | :--- | :--- |
| 纵向制表符 \v | 回车 \r | 退格符 \b |

泛化转义序列

| \7 响铃 | \12 换行符 | \40 空格 |
| :--- | :--- | :--- |
| \0 空字符 | \115 字符 M | \x4d 字符 M |

* 如果反斜杠后边跟着8进制超过3个，只有前3个数字构成转义
  * \1234 表示2个字符，8进制123对应的字符和字符4
* \x1234 表示16进制，所有数字都会用，这里会超出范围可能会报错，表2.2，p37
* 尽量用大写 L，因为小写 l 跟1很接近

