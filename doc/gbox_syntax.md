# Gbox 语法参考手册

## 目录

- [Gbox 语法参考手册](#gbox-语法参考手册)
  - [目录](#目录)
  - [基础语法](#基础语法)
    - [注释](#注释)
  - [变量](#变量)
    - [基础类型 {#基础类型}](#基础类型-基础类型)
    - [特殊表示法](#特殊表示法)
      - [颜色表示](#颜色表示)
      - [ID 和函数特殊写法](#id-和函数特殊写法)
    - [变量声明与初始化](#变量声明与初始化)
    - [数组和字典](#数组和字典)
      - [普通数组](#普通数组)
      - [VID 数组](#vid-数组)
      - [字典数组](#字典数组)
    - [变量生命周期](#变量生命周期)
      - [普通类型（非 obj 对象类型）](#普通类型非-obj-对象类型)
      - [对象类型（obj）](#对象类型obj)
  - [预处理指令](#预处理指令)
    - [常量定义](#常量定义)
    - [条件编译](#条件编译)
    - [常量定义的替代方案](#常量定义的替代方案)
  - [枚举类型](#枚举类型)
    - [枚举定义](#枚举定义)
    - [枚举注释属性](#枚举注释属性)
    - [枚举访问](#枚举访问)
    - [枚举变量](#枚举变量)
    - [枚举在函数和控制流中的应用](#枚举在函数和控制流中的应用)
  - [函数](#函数)
    - [函数定义](#函数定义)
    - [函数调用](#函数调用)
  - [条件控制](#条件控制)
    - [if 语句](#if-语句)
    - [switch 语句](#switch-语句)
  - [循环语句](#循环语句)
    - [for循环](#for循环)
    - [while循环](#while循环)
    - [do-while循环](#do-while循环)
    - [循环控制](#循环控制)
  - [类和对象](#类和对象)
    - [类定义和继承](#类定义和继承)
    - [对象初始化和函数执行顺序](#对象初始化和函数执行顺序)
      - [函数执行顺序规则](#函数执行顺序规则)
    - [成员变量命名规范](#成员变量命名规范)
    - [对象实例化](#对象实例化)
      - [1. 使用 new 关键字（推荐）](#1-使用-new-关键字推荐)
      - [2. 使用类名直接声明（仅函数外）](#2-使用类名直接声明仅函数外)
      - [3. 使用动态创建](#3-使用动态创建)
    - [对象变量赋值](#对象变量赋值)
    - [对象成员访问](#对象成员访问)
  - [样式（Style）](#样式style)
    - [样式定义](#样式定义)
    - [类型化样式](#类型化样式)
    - [样式继承](#样式继承)
  - [定时器和微线程](#定时器和微线程)
    - [定时器](#定时器)
      - [SetTimer](#settimer)
      - [KillTimer](#killtimer)
      - [IsTimer](#istimer)
    - [微线程](#微线程)
      - [StartTask](#starttask)
      - [Wait](#wait)
      - [WaitMs](#waitms)
    - [任务管理](#任务管理)
      - [IsTaskPtr](#istaskptr)
      - [RemoveHoldTask](#removeholdtask)
      - [完整示例](#完整示例)
  - [异常处理](#异常处理)
    - [异常捕获](#异常捕获)
    - [异常抛出](#异常抛出)
  - [命名空间与作用域](#命名空间与作用域)
    - [命名空间函数调用](#命名空间函数调用)
    - [类与对象](#类与对象)
      - [静态变量和函数](#静态变量和函数)
      - [对象引用](#对象引用)
  - [Gbox执行机制和入口点](#gbox执行机制和入口点)
    - [面向对象的执行模型](#面向对象的执行模型)
    - [代码执行位置](#代码执行位置)
    - [正确的初始化模式](#正确的初始化模式)
  - [键盘和输入处理](#键盘和输入处理)
    - [键盘状态查询函数](#键盘状态查询函数)
    - [键盘事件回调函数](#键盘事件回调函数)
    - [组合使用示例](#组合使用示例)
    - [键盘和鼠标常量](#键盘和鼠标常量)
      - [鼠标按钮常量 (GTK\_)](#鼠标按钮常量-gtk_)
      - [键盘虚拟键常量 (GVK\_)](#键盘虚拟键常量-gvk_)
      - [控制键状态标志 (GVKBIT\_)](#控制键状态标志-gvkbit_)
    - [键盘常量使用示例](#键盘常量使用示例)
  - [对象显示和隐藏](#对象显示和隐藏)
    - [注意事项](#注意事项)

## 基础语法

### 注释

Gbox 支持两种类型的注释：

```gbox
// 单行注释

/*
多行注释
可以跨越多行
*/
```

## 变量

### 基础类型 {#基础类型}

Gbox 提供以下基础数据类型：

| 类型    | 描述                       |
|---------|----------------------------|
| int     | 32位整数                   |
| int64   | 64位整数                   |
| float   | 浮点数                     |
| string  | 字符串                     |
| bool    | 布尔值（同 int）           |
| vec2    | 2D向量                     |
| vec3    | 3D向量                     |
| vec4    | 4D向量                     |
| obj     | 对象引用                   |
| strid   | 字符串ID                   |
| var     | 变量类型，可存储任意类型数据 |

### 特殊表示法

#### 颜色表示

颜色值（int 类型）可以使用十六进制或 rgb# 格式表示，通常包含 alpha 通道：

```gbox
// 十六进制表示
int color1 = 0xff00ff00;  // ARGB 格式：透明度, 红, 绿, 蓝

// rgb# 格式
int color2 = rgb#ff00ff;  // RGB 格式：红, 绿, 蓝
```

#### ID 和函数特殊写法

```gbox
// id# 自动将字符串转换为 int
int id = id#something;  // 等同于 "something".strid

// fun# 类似 id#，但引擎内部有特殊检查
int funcId = fun#someFunction;
```

### 变量声明与初始化

在 Gbox 中变量声明可以带有或不带有初始值。

```gbox
// 声明变量并赋初值
int a = 10;
float f = 3.14;
string s = "Hello";

// 声明变量不赋初值，将使用默认值
int b;     // 默认值为0
float g;   // 默认值为0.0
string t;  // 默认值为""
```

注意事项：
- 变量声明和初始化必须在一行内完成
- 可以在一行中声明多个相同类型的变量
- var类型必须使用nil初始化，而不是空括号`()`

```gbox
// 正确的var初始化方式
var v1 = nil;      // 正确
var v2;            // 正确，默认为nil

// 错误的var初始化方式
// var v3 = ();    // 错误，不能使用空括号初始化
```

### 数组和字典

Gbox 中的数组和字典都是 `var` 类型，可以嵌套。

#### 普通数组

Gbox 中可以使用多种方式创建和操作数组：

```gbox
// 创建数组
var arr1 = (1, 2, 3, 4, 5);
var arr2 = ("a", "b", "c");
var arr3 = nil;   // 空数组，而不是 var arr3 = ()

// 访问数组元素
var first = arr1[0];  // 数组索引从0开始
var last = arr1[arr1.size - 1];  // 使用size属性获取数组大小

// 添加元素
arr3 = nil;            // 确保arr3是一个空数组
arr3.append(10);       // 在数组末尾添加元素
arr3.append(20, 30);   // 可以一次添加多个元素

// 删除元素
arr3.remove(0);        // 删除索引为0的元素

// 循环遍历数组
for(int i = 0; i < arr1.size; i++) {
    ?(i + ": " + arr1[i]);
}
```

注意：Gbox中数组大小通过`.size`属性获取，而不是`.len()`方法。

#### VID 数组

VID 数组使用 ID 作为键：

```gbox
var v;
// 注意: vset 第一个参数可以是字符串或 int，但最终都会被转换为 int
v.vset("a", 100);  // 相当于: v.vset("a".strid, 100)
v.vset("b", 232);  // 相当于: v.vset("b".strid, 232)

//vid数组是一个一维的结构,自动把字符串转为int.也可以直接传入int
?v;  // 输出: (id##400EB2BF, 232, id##7DC63D68, 100)

```

#### 字典数组

字典可以使用字符串作为键：

```gbox
var vdic;
vdic.svSet("a", 100);
vdic.svSet("b", 99);
//实际上创建了一个二维数组:(("a",100),("b",99))

// 获取值
int a = vdic.svVal("a", 0);  // 第二个参数是默认值

// 另一种获取方式
int b;
if(vdic.svGet("b", b)) {
    ?b;  // 如果键存在，输出对应值
}
```

### 变量生命周期

#### 普通类型（非 obj 对象类型）

- 成员变量的生命周期与对象实例相同
- 函数内的局部变量生命周期与函数相同

#### 对象类型（obj）

- 生命周期跟随父对象
- 需要手动释放对象：
  ```gbox
  p.DelThis();      // 效率更高，但如果 p 对象无效会报错
  SafeDelObj(p);    // 更安全，p 对象无效时不会报错
  ```

## 预处理指令

Gbox 支持一些预处理指令，用于在代码编译前进行替换和条件编译。

### 常量定义

**注意：** Gbox 不支持 `const` 关键字定义常量。相应地，可以使用 `#define` 定义常量：

```gbox
#define SCREEN_WIDTH 800
#define SCREEN_HEIGHT 600
#define APP_NAME "My Game"

// 使用常量
void InitWindow() {
    SetWindowSize(SCREEN_WIDTH, SCREEN_HEIGHT);
    SetWindowTitle(APP_NAME);
}
```

`#define` 也可以不带值，用于条件编译：

```gbox
#define DEBUG  // 定义一个标记，不带值
```

### 条件编译

可以使用 `#ifdef`、`#else`、`#endif` 进行条件编译：

```gbox
#define DEBUG

void LogMessage(string msg) {
    #ifdef DEBUG
        ?msg;  // 在调试模式下输出消息
    #else
        // 在非调试模式下不做任何事
    #endif
}
```

完整的条件编译指令包括：

```gbox
#ifdef 标识符     // 如果标识符已定义，则编译下面的代码
#ifndef 标识符    // 如果标识符未定义，则编译下面的代码
#else            // 条件不满足时的替代分支
#endif           // 结束条件编译块
```

### 常量定义的替代方案

除了 `#define`，还可以使用枚举定义常量：

```gbox
enum Constants
{
    SCREEN_WIDTH = 800,
    SCREEN_HEIGHT = 600,
    MAX_PLAYERS = 4
};

// 使用枚举常量
void InitWindow() {
    SetWindowSize(Constants.SCREEN_WIDTH, Constants.SCREEN_HEIGHT);
}
```

对于字符串常量，只能使用 `#define`，因为枚举只能存储整数值。

## 枚举类型

枚举是一种命名整数常量的方式，在Gbox中支持创建自定义枚举类型。

### 枚举定义

使用 `enum` 关键字定义枚举类型：

```gbox
enum 枚举名
{
    成员1 = 值1,
    成员2,  // 如果不指定值，会自动递增
    成员3 = 新值
};
```

例如：

```gbox
enum MyTestENUM
{
    A = 120,
    B,       // 值为121，自动递增
    C = 80
};
```

### 枚举注释属性

枚举和枚举成员可以附加特殊注释属性，使用 `//@属性名=值` 格式：

```gbox
enum TestENUM
{
    //@name=asdjkk   // 为成员A添加name属性
    //@pos=ymdef     // 为成员A添加pos属性
    A = 1,
    B = 5,
    C = 9
};

//@mem=test def     // 为枚举变量添加mem属性
enum MyTestENUM m_HH;
```

这些注释属性可以用于系统内部处理或自定义功能。

### 枚举访问

通过 `枚举名.成员名` 的方式访问枚举值：

```gbox
?MyTestENUM.A;     // 输出120
int value = TestENUM.B;  // value = 5
```

枚举值可以参与算术运算：

```gbox
int result = 2 + MyTestENUM.A * 2;  // result = 2 + 120 * 2 = 242
```

### 枚举变量

可以声明枚举类型的变量：

```gbox
enum MyTestENUM m_nEnumVar;  // 声明一个MyTestENUM类型的变量
```

枚举值可以赋给整数变量：

```gbox
int m_nA = MyTestENUM.C;  // m_nA = 80
```

### 枚举在函数和控制流中的应用

枚举可以用作函数参数类型：

```gbox
void Test(enum MyTestENUM a)
{
    enum MyTestENUM bb;  // 局部变量
    // ...
}
```

在switch语句中使用枚举值：

```gbox
switch(a) {
    case MyTestENUM.C:
        ?"ok c";
        break;
    default:
        ?a;
        break;
}
```

枚举信息可以通过系统帮助函数获取：

```gbox
var list;
syshelp::GetClassInfo(list, "$ENUM", "TestENUM;GSYNTAX_CHAR");
```

系统内置枚举也可作为命名空间使用：

```gbox
?GSYNTAX_CHAR.EXTCHAR;  // 访问系统枚举
```

## 函数

### 函数定义

函数可以有返回值和参数，参数可以有默认值：

```gbox
// 无返回值，无参数
void print() {
    ?"打印函数";
}

// 有返回值，有参数，带默认参数
int add_ten(int a, int b = 10) {
    return a + b;
}
```

### 函数调用

直接调用函数：

```gbox
print();
int result = add_ten(100, 2);  // 结果为 102
int result2 = add_ten(100);    // 使用默认参数，结果为 110
```

调用对象的方法：

```gbox
GObjShape m_pA;
m_pA.SetColor(0xffff0000);
```

## 条件控制

### if 语句

条件在小括号内，代码块使用大括号（单行可省略大括号）：

```gbox
void print(int a) {
    // 单行语句可省略大括号
    if(a > 10) ?"a 比 10 大";
    else ?"a 没有 10 大";

    // 嵌套 if
    if(a > 10) {
        if(a < 100) {
            ?"a 比 10 大，但比 100 小";
        }
    }
    
    // 使用逻辑运算符
    if(a > 10 && a < 100) ?"a 比 10 大，但比 100 小";
}
```

### switch 语句

```gbox
void print(int a) {
    switch(a) {
        case 0:
            ?"值为 0";
            break;
        case 1:
            ?"值为 1";
            break;
        default:
            ?"其他值";
            break;
    }
}
```

## 循环语句

Gbox支持以下循环结构：

### for循环

基本for循环语法，用于固定次数迭代:

```
for(初始化; 条件; 增量) {
    // 循环体
}
```

示例:
```
// 正确的循环用法
for(int i = 0; i < 10; i++) {
    print(i);
}

// 迭代数组
var myArray = (1, 2, 3, 4, 5);
for(int i = 0; i < myArray.size; i++) {
    print(myArray[i]);
}
```

注意事项:
- 循环变量必须在循环前声明，不能在for语句内首次声明变量
- Gbox不支持C++风格的foreach或范围for循环

### while循环

当条件为真时执行循环:

```
while(条件) {
    // 循环体
}
```

### do-while循环

至少执行一次，然后在条件为真时继续循环:

```
do {
    // 循环体
} while(条件);
```

### 循环控制

- `break` - 立即退出最内层循环
- `continue` - 跳过当前迭代，继续下一次迭代

## 类和对象

### 类定义和继承

类必须继承自一个 Gbox 脚本可用类，`GObj` 是脚本基础类：

```gbox
// 基本类定义
class A : GObj {
    int m_nA = 10;
    
    int Add(int b) {
        m_nA += b;
        return m_nA;
    }
    
    void Print() {
        ?m_nA;
    }
}

// 继承自内置类
class B : GObjShape {
    // 类定义中可以直接调用父类方法
    SetColor(0xffff0000);
}

// 继承自自定义类
class C : A {
    // 可以重写父类成员变量
    m_nA = 100;
}
```

### 对象初始化和函数执行顺序

在Gbox中，对象的创建和初始化遵循特定的执行顺序：

```gbox
class GTest : GObj {
    // 构造函数（与类同名）
    void GTest(string s) {
        ?"构造函数:", s;
    }
    
    // 特殊生命周期函数，对象创建后自动调用
    void OnCreate() {
        ?"OnCreate";
    }
    
    // 常规初始化方法，需要手动调用
    void Init() {
        ?"Init被手动调用";
    }
    
    void foo() {
        ?"foo";
    }
    
    void foo2() {
        ?"foo2";
    }
    
    // 类内直接调用的函数会首先执行
    foo();  // 直接调用
}

// 创建对象实例
obj m_pTest = new GTest("abc");
// Init()不会自动调用，需要手动调用
m_pTest.Init();
m_pTest.foo2();  // 外部调用方法
```

以上代码的执行顺序为：
1. `"foo"` - 首先执行类内直接调用的函数
2. `"OnCreate"` - 然后是OnCreate生命周期函数
3. `"构造函数: abc"` - 接着是构造函数
4. `"Init被手动调用"` - 然后是手动调用的Init方法（只有明确调用才会执行）
5. `"foo2"` - 最后是外部对对象方法的调用

#### 函数执行顺序规则

1. **类内直接调用的函数**：在类定义中直接调用的函数会最先执行
2. **OnCreate函数**：特殊的生命周期函数，在对象创建后自动调用
3. **构造函数**：与类同名的函数，在OnCreate之后执行
4. **Init函数**：通常用于初始化的公共方法，但不会自动调用，需要明确调用
5. **外部方法调用**：创建完成后，外部代码对对象方法的调用

**注意**：虽然Init()是常见的初始化方法名称，但它并不特殊，不会被Gbox引擎自动调用。它只是一个约定俗成的公共方法，需要在对象创建后手动调用。

### 成员变量命名规范
所有类的成员变量必须以 `m_` + 类型标记开头：
同时，类外面的变量，其实等同于g_pDeskTop的成员变量,所以也要遵循此规则

| 类型           | 前缀    | 示例       |
|----------------|---------|------------|
| int            | m_n     | m_nCount   |
| string         | m_s     | m_sName    |
| float          | m_f     | m_fScale   |
| obj            | m_p     | m_pShape   |
| var (数组)     | m_sz    | m_szItems  |
| var (其他类型) | m_v     | m_vData    |
| vec2/3/4       | m_v     | m_vPos     |
| int64          | m_N     | m_NId      |
| bool           | m_b     | m_bVisible |

### 对象实例化

Gbox中有三种主要方式创建对象实例：

#### 1. 使用 new 关键字（推荐）

可以在函数内或函数外使用。**注意：所有对象类型变量都应使用`obj`关键字声明，而不是类名。**

```gbox
// 创建实例并赋值给变量
obj m_pShape = new GObjShape;  // 正确
// GObjShape m_pShape = new GObjShape;  // 错误！不要这样做

void foo() {
    obj p = new GObj;  // 正确
    p.SetShow(0);
}
```

#### 2. 使用类名直接声明（仅函数外）

这种方式只能在函数外使用，是一种特殊的简写语法：

```gbox
// 直接用类名创建实例 - 仅在函数外有效
GObjShape m_pA;  // 类似于 obj m_pA = new GObjShape;

// $ 会自动生成变量名，通常用于不需要手动调用的实例
GObjShape $;

// 可以使用冒号链式调用方法
GObjShape m_pB : SetPos(100, 100) : SetSize(50, 50) : SetColor(0xff00ff00);
```

#### 3. 使用动态创建

通过字符串类名创建对象，可在函数内或函数外使用：

```gbox
void foo() {
    // 通过类名字符串创建
    obj p = NewObj("GObjShape", this);
    
    // 通过变量中的类名创建
    string s = "GObj";
    obj p2 = NewObj(s, this);
}
```

### 对象变量赋值

当需要将一个对象赋值给另一个变量时，接收变量也必须使用`obj`类型：

```gbox
GObjShape m_pPlayer;  // 在函数外创建实例

void SomeFunction() {
    // 正确的赋值方式
    obj player = m_pPlayer;
    
    // 错误的赋值方式
    // GObjShape player = m_pPlayer;  // 错误！不要这样做
    
    player.SetPos(100, 100);
}
```

### 对象成员访问

使用点号访问对象的成员变量和方法：

```gbox
obj shape = new GObjShape;
shape.SetPos(100, 100);
shape.SetColor(0xffff0000);

// 访问成员变量
float x = shape.m_vPos.x;
float y = shape.m_vPos.y;
```

## 样式（Style）

样式是一种代码复用机制，允许多个类共享相同的代码。

### 样式定义

基本样式定义：

```gbox
style AddStyle {
    int Add(int a, int b) {
        return a + b;
    }
}
```

### 类型化样式

如果样式需要引用特定类的变量或方法，需要通过 `<>` 指定类型：

```gbox
style<GObjShape> PrintStyle {
    // 这是 GObjShape 的方法，需要在样式中指定 <GObjShape>
    SetColor(rgb#ff00ff00);
    
    void Print() {
        ?"hello";
    }
}
```

### 样式继承

类可以继承多个样式（用逗号分隔），但只能继承一个类（必须是第一个）：

```gbox
// 继承类 GObjShape 和两个样式 AddStyle、PrintStyle
class A : GObjShape, AddStyle, PrintStyle {
    void TestMethods() {
        ?Add(10, 20);  // 输出 30（来自 AddStyle）
        Print();       // 输出 hello（来自 PrintStyle）
    }
}
```

## 定时器和微线程

Gbox提供了定时器和微线程功能，用于处理定时任务和异步操作。

### 定时器

定时器用于以固定时间间隔执行函数，或在指定延迟后执行函数。

#### SetTimer

创建定时器，可以重复执行或指定执行次数：

```gbox
// 语法: SetTimer(延迟秒数, 函数名, 参数, 执行次数)
// 参数说明:
// - 延迟秒数: float类型，每次执行的间隔时间
// - 函数名: string类型或strid类型，要执行的函数名
// - 参数: 可选，传递给定时器函数的参数，默认为null
// - 执行次数: 可选，int类型，定时器执行的次数，0或不填表示无限循环

// 每隔1秒调用一次foo_timer_loop函数
SetTimer(1, "foo_timer_loop");

// 3.2秒后调用一次foo_timer_3函数，且仅调用3次
SetTimer(3.2, "foo_timer_3", nil, 3);
```

#### KillTimer

终止指定名称的定时器：

```gbox
// 语法: KillTimer(函数名)
// 参数说明:
// - 函数名: string类型或strid类型，要终止的定时器函数名，不填则终止所有定时器

// 终止foo_timer_loop定时器
KillTimer("foo_timer_loop");

// 终止所有定时器
KillTimer();
```

#### IsTimer

检查指定名称的定时器是否存在：

```gbox
// 检查foo_timer_loop定时器是否存在
bool exists = IsTimer("foo_timer_loop");
```

### 微线程

微线程允许异步执行代码，而不会阻塞主线程。

#### StartTask

创建并启动一个微线程：

```gbox
// 语法: StartTask(函数名, 参数, 结束回调函数)
// 参数说明:
// - 函数名: string类型或strid类型，要在微线程中执行的函数名
// - 参数: 可选，传递给微线程函数的参数，默认为null
// - 结束回调函数: 可选，微线程结束后调用的函数名

// 启动微线程执行foo_wait_kill函数
obj m_pTask = StartTask("foo_wait_kill");

// 带参数启动微线程
obj m_pTask = StartTask("foo_func", "参数值");

// 带结束回调的微线程
obj m_pTask = StartTask("foo_func", nil, "on_task_completed");
```

#### Wait

在微线程中暂停执行指定的秒数：

```gbox
// 语法: Wait(秒数, 等待标识)
// 参数说明:
// - 秒数: float类型，等待的秒数
// - 等待标识: 可选，标识此等待的名称，可用于提前结束等待

// 暂停1.5秒
void foo_wait() {
    ?"开始等待";
    Wait(1.5);  // 在微线程中暂停1.5秒
    ?"等待结束";
}

// 使用等待标识
void foo_wait2() {
    ?"开始等待";
    Wait(5, "my_wait");  // 等待5秒，标识为"my_wait"
    ?"等待结束";
}
```

#### WaitMs

以毫秒为单位暂停微线程：

```gbox
// 暂停500毫秒
WaitMs(500);

// 暂停500毫秒，带标识
WaitMs(500, "my_wait_ms");
```

### 任务管理

#### IsTaskPtr

检查对象是否为有效的任务指针：

```gbox
// 检查m_pTask是否为有效的任务指针
if(IsTaskPtr(m_pTask)) {
    ?"m_pTask是一个有效的任务";
}
```

#### RemoveHoldTask

终止指定的微线程任务：

```gbox
// 终止m_pTask微线程
if(IsTaskPtr(m_pTask)) {
    RemoveHoldTask(m_pTask);
}
```

#### 完整示例

以下是定时器和微线程的综合使用示例：

```gbox
// 定时器函数，每秒调用一次
void foo_timer_loop() {
    ?"foo_timer_loop";
}

// 设置定时器，每秒调用一次
SetTimer(1, "foo_timer_loop");

// 微线程函数
void foo_wait_kill() {
    ?"foo_wait_kill 1";
    Wait(20);
    // 由于微线程可能被提前终止，此行可能不会执行
    ?"foo_wait_kill 2";
}

// 启动微线程
obj m_pTask = StartTask("foo_wait_kill");
?"微线程已启动", IsTaskPtr(m_pTask);

// 主线程函数
void test() {
    Wait(10);  // 在主线程中调用会阻塞主线程
    
    // 10秒后终止定时器
    KillTimer("foo_timer_loop");
    
    // 终止微线程
    if(IsTaskPtr(m_pTask)) {
        RemoveHoldTask(m_pTask);
    }
}

// 执行测试
test();
```

## 异常处理

### 异常捕获

使用 `catch` 块捕获异常：

```gbox
void foo() {
    test_abort();
    catch {
        ?_errinfo;    // 错误 ID 和错误字符串
        ?_err;        // 只有错误 ID
        ?_erragv;     // 只有错误字符串
    }
}
```

### 异常抛出

使用 `Abort` 方法抛出异常：

```gbox
void test_abort() {
    ?"a";
    Abort(1, "something wrong");  // 抛出异常，后续代码不会执行
    ?"b";  // 不会执行
}

// 调用上述函数并捕获异常
void run_test() {
    test_abort();
    catch {
        ?_errinfo;  // 输出: user Abort;_err=1;_erragv="something wrong"
    }
}
```

## 命名空间与作用域

### 命名空间函数调用

Gbox中命名空间函数调用有两种形式：

1. **单冒号前缀命名空间**：以单冒号开头的命名空间（如`:fixcal`, `:math`, `:task`）中的函数必须直接调用，不能使用命名空间前缀

```
// 这些函数必须直接调用，不能带命名空间
rand(100);           // 正确，而不是 :math.rand(100)
AddDelayMS(500, callback);  // 正确，而不是 :task.AddDelayMS(500, callback)
clamp(value, min, max);     // 正确，而不是 :fixcal.clamp(value, min, max)
```

2. **双冒号命名空间**：其他命名空间中的函数必须使用双冒号（`::`）来调用

```
// 这些函数必须带上命名空间
ease::Ani(obj, "x", 100, 1000);   // 必须包含ease::前缀
file::SaveText("path.txt", content);  // 必须包含file::前缀
```

### 类与对象

Gbox 支持面向对象编程，可以定义类、创建对象、继承等操作。

```gbox
// 定义一个简单的类
class MyClass {
    // 成员变量
    int m_nValue = 0;
    string m_strName = "Default";
    
    // 成员函数
    void SetValue(int value) {
        m_nValue = value;
    }
    
    int GetValue() {
        return m_nValue;
    }
}

// 创建对象
obj myObj = new MyClass();
myObj.SetValue(10);
?(myObj.GetValue());  // 输出: 10
```

#### 静态变量和函数

类可以包含静态成员和静态方法，使用`static`关键字声明。静态成员属于类本身，而不是类的实例。

```gbox
class GameManager {
    // 静态变量
    static int s_nScore = 0;
    static int s_nHighScore = 100;
    
    // 静态函数
    static void AddScore(int value) {
        GameManager::s_nScore += value;
        // 也可以直接使用 s_nScore += value;
        
        if(GameManager::s_nScore > GameManager::s_nHighScore) {
            GameManager::s_nHighScore = GameManager::s_nScore;
        }
    }
    
    static int GetHighScore() {
        return GameManager::s_nHighScore;
    }
    
    // 普通成员函数
    void ResetGame() {
        GameManager::s_nScore = 0;
    }
}

// 访问静态成员和方法（使用::语法）
GameManager::AddScore(50);
?(GameManager::s_nScore);  // 输出: 50

// 通过对象调用静态方法（可行但不推荐）
obj manager = new GameManager();
manager.AddScore(25);  // 有效，但最好使用 GameManager::AddScore(25)

// 错误：不能通过对象访问静态变量
// ?(manager.s_nScore);  // 错误! 需要使用 GameManager::s_nScore
```

注意事项：
1. 静态变量和函数使用`::`操作符从类外部访问
2. 类内部可以直接访问静态成员，无需`::`操作符
3. 静态方法可以通过对象调用，但最好通过类名调用
4. 静态方法不能访问非静态成员变量

#### 对象引用

不同对象之间可以通过以下方式互相引用和调用：

```gbox
// 父对象引用：使用pid访问父对象
void SomeMethod() {
    pid.SomeParentMethod();  // 调用父对象的方法
    var parentValue = pid.m_nParentValue;  // 访问父对象的变量
}

// 顶级对象：g_pDeskTop是顶级根对象
g_pDeskTop.SomeGlobalMethod();  // 调用顶级对象的方法

// 其他对象引用：通过变量访问
obj m_pPlayer;  // 保存对象引用
m_pPlayer.Move();  // 调用引用对象的方法
```

## Gbox执行机制和入口点

### 面向对象的执行模型

Gbox是完全面向对象的引擎，**没有类似C/C++的main函数**作为入口点。理解这一点对于正确编写Gbox代码至关重要：

```gbox
// 这段代码直接写在最外层，会立即执行
// 相当于在g_pDeskTop对象内部执行
InitGame();  // 这会直接调用InitGame函数

// 下面的代码不会自动执行，需要手动调用main()
void main() {  // 这不是入口点，只是一个普通函数
    InitGame();
}
```

### 代码执行位置

1. **最外层代码**：
   - 直接写在脚本最外层的代码会立即执行
   - 这些代码实际上是在顶层对象`g_pDeskTop`的上下文中运行
   - 可以直接调用全局函数和访问全局变量

2. **OnCreate函数**：
   - 在顶层写的OnCreate会在脚本加载时自动调用
   - 等同于直接写在最外层的代码
   ```gbox
   void OnCreate() {
       InitGame();  // 会自动执行
   }
   ```

3. **main函数**：
   - Gbox中的main函数**不是**自动执行的入口点
   - 它只是一个常规函数，需要显式调用才会执行
   ```gbox
   void main() {
       // 这段代码不会自动执行
       InitGame();
   }
   
   // 需要手动调用才会执行main
   main();
   ```

### 正确的初始化模式

```gbox
// 1. 直接在最外层执行初始化（推荐）
InitGame();

// 2. 在OnCreate中执行初始化（也有效）
void OnCreate() {
    InitGame();
}

// 3. 错误方式：仅定义main函数但不调用
void main() {  // 这不会自动执行！
    InitGame();
}
```

理解Gbox的这种执行模式对于正确初始化游戏和避免常见错误至关重要。 

## 键盘和输入处理

Gbox提供了多种方式处理键盘输入，适用于不同的场景：

### 键盘状态查询函数

```gbox
// 检查按键是否被按下（持续按住时返回true）
if(keyboard.IsKeyDown(KEY_SPACE)) {
    // 适用于需要持续响应的输入，如角色移动
}

// 检查按键是否刚被按下（只在按下瞬间返回true）
if(keyboard.IsKeyPressed(KEY_ENTER)) {
    // 适用于需要触发一次的操作，如菜单选择
}
```

### 键盘事件回调函数

推荐的键盘输入处理方式是通过回调函数：

```gbox
// 按键按下事件 - 在g_pDeskTop对象的上下文中定义
void OnKeyDown(int key) {
    switch(key) {
        case KEY_SPACE:
            // 处理空格键按下事件
            break;
        case KEY_UP:
            // 处理上方向键按下事件
            break;
    }
}

// 按键释放事件 - 在g_pDeskTop对象的上下文中定义
void OnKeyUp(int key) {
    switch(key) {
        case KEY_UP:
            // 处理上方向键释放事件
            break;
    }
}
```

### 组合使用示例

对于游戏角色移动这类需要持续响应的输入，可以组合使用：

```gbox
// 玩家类
class GPlayer : GObj {
    // 移动方向控制变量
    bool m_bUp = false;
    bool m_bDown = false;
    
    void Update() {
        vec2 velocity = (0, 0);
        
        // 基于方向变量更新速度
        if(m_bUp) velocity.y -= 5;
        if(m_bDown) velocity.y += 5;
        
        // 更新位置
        m_vPos.x += velocity.x;
        m_vPos.y += velocity.y;
    }
    
    // 设置移动方向
    void SetDirection(int key, bool pressed) {
        switch(key) {
            case KEY_UP:
                m_bUp = pressed;
                break;
            case KEY_DOWN:
                m_bDown = pressed;
                break;
        }
    }
}

// 全局按键处理函数（在g_pDeskTop上下文中）
void OnKeyDown(int key) {
    // 方向键 - A设置玩家移动方向
    if(m_pPlayer) {
        m_pPlayer.SetDirection(key, true);
    }
}

void OnKeyUp(int key) {
    // 方向键释放 - 停止移动
    if(m_pPlayer) {
        m_pPlayer.SetDirection(key, false);
    }
}
```

### 键盘和鼠标常量

Gbox提供了完整的键盘和鼠标按键常量定义，用于输入处理。

#### 鼠标按钮常量 (GTK_)

```gbox
#define GTK_LBUTTON    0x1    // 鼠标左键
#define GTK_RBUTTON    0x2    // 鼠标右键
#define GTK_CANCEL     0x3    // 取消操作
```

#### 键盘虚拟键常量 (GVK_)

```gbox
// 特殊键
#define GVK_BACK       0x8    // 退格键
#define GVK_TAB        0x9    // Tab键
#define GVK_CLEAR      0xC    // Clear键
#define GVK_RETURN     0xD    // 回车键
#define GVK_SHIFT      0x10   // Shift键
#define GVK_CTRL       0x11   // Ctrl键
#define GVK_ALT        0x12   // Alt键
#define GVK_PAUSE      0x13   // Pause键
#define GVK_CAPITAL    0x14   // Caps Lock键
#define GVK_ESCAPE     0x1B   // Esc键
#define GVK_SPACE      0x20   // 空格键

// 方向和编辑键
#define GVK_PAGEUP     0x21   // Page Up键
#define GVK_PAGEDN     0x22   // Page Down键
#define GVK_END        0x23   // End键
#define GVK_HOME       0x24   // Home键
#define GVK_LEFT       0x25   // 左方向键
#define GVK_UP         0x26   // 上方向键
#define GVK_RIGHT      0x27   // 右方向键
#define GVK_DOWN       0x28   // 下方向键
#define GVK_SELECT     0x29   // Select键
#define GVK_PRINT      0x2A   // Print键
#define GVK_EXECUTE    0x2B   // Execute键
#define GVK_SNAPSHOT   0x2C   // Print Screen键
#define GVK_INSERT     0x2D   // Insert键
#define GVK_DELETE     0x2E   // Delete键
#define GVK_HELP       0x2F   // Help键

// 字母键
#define GVK_A          0x41   // A键
#define GVK_B          0x42   // B键
#define GVK_C          0x43   // C键
// ... 其他字母键 ...
#define GVK_Z          0x5A   // Z键

// 数字键
#define GVK_0          48     // 0键
#define GVK_1          49     // 1键
#define GVK_2          50     // 2键
// ... 其他数字键 ...
#define GVK_9          57     // 9键
#define GVK_SUB        189    // 减号键 '-'
#define GVK_EQ         187    // 等号键 '='

// 功能键
#define GVK_F1         0x70   // F1键
#define GVK_F2         0x71   // F2键
// ... 其他功能键 ...
#define GVK_F20        0x83   // F20键

// 其他键
#define GVK_LWIN       0x5B   // 左Windows键
#define GVK_RWIN       0x5C   // 右Windows键
#define GVK_APPS       0x5D   // 应用程序键
#define GVK_NUMLOCK    0x90   // Num Lock键
#define GVK_SCROLL     0x91   // Scroll Lock键

// 小键盘数字键
#define GVK_NUMPAD0    0x60   // 小键盘0
#define GVK_NUMPAD1    0x61   // 小键盘1
// ... 其他小键盘数字键 ...
#define GVK_NUMPAD9    0x69   // 小键盘9
```

#### 控制键状态标志 (GVKBIT_)

```gbox
#define GVKBIT_SHIFT   0x1    // Shift键状态标志
#define GVKBIT_CTRL    0x2    // Ctrl键状态标志
#define GVKBIT_ALT     0x4    // Alt键状态标志
```

### 键盘常量使用示例

```gbox
void OnKeyDown(int key) {
    // 使用键盘常量
    switch(key) {
        case GVK_W:
        case GVK_UP:
            m_pPlayer.SetDirection("up", true);
            break;
            
        case GVK_S:
        case GVK_DOWN:
            m_pPlayer.SetDirection("down", true);
            break;
            
        case GVK_ESCAPE:
            PauseGame();
            break;
            
        case GVK_SPACE:
            PlayerJump();
            break;
    }
}

// 检查组合键
void CheckKeyCombination() {
    // 检查Ctrl+S组合键
    if(keyboard.IsKeyDown(GVK_CTRL) && keyboard.IsKeyPressed(GVK_S)) {
        SaveGame();
    }
} 
```

## 对象显示和隐藏

Gbox提供了对象显示和隐藏的功能，主要通过`SetShow`函数实现：

```gbox
// 显示对象
obj.SetShow(true); // 或 obj.SetShow(1);

// 隐藏对象
obj.SetShow(false); // 或 obj.SetShow(0);
```

### 注意事项

- **不要使用`SetVisible`**：这个函数在Gbox API中不存在。正确的函数是`SetShow`。
- 对象继承自`GObjShow`类都可以使用`SetShow`方法控制显示状态。
- 可以通过对象的`m_nShow`属性检查当前显示状态。

```gbox
// 示例：根据游戏状态切换UI元素显示
void ChangeGameState(int state) {
    switch(state) {
        case STATE_MENU:
            m_pMenuText.SetShow(true);
            m_pGameText.SetShow(false);
            break;
            
        case STATE_GAME:
            m_pMenuText.SetShow(false);
            m_pGameText.SetShow(true);
            break;
    }
}
```

一些对象可能有额外的显示控制方法，例如`GObjSheet`类的`HideAllLine`方法，具体请参考相关类的API文档。 