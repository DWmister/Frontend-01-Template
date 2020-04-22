# 编程语言通识

### 语言按语法的分类

- 非形式语言
  - 中文、英文、阿拉伯。。。
- 形式语言
  - 0型	无限制文法     ?::=?
  - 1型	上下文相关文法     ?<A>?::=?<B>?
  - 2型	上下文无关文法     <A>::=?
  - 3型	正则文法    <A>::=<A>?

### BNF(巴科斯范式) 计算机和语言之间

BNF(Backus-Naur Form)是描述编程语言的文法。巴科斯范式是一种用于表示上下文无关文法的语言，上下文无关文法描述了一类形式语言。

自然语言存在不同程度的二义性。这种模糊、不确定的方式无法精确定义一门程序设计语言。必须设计一种准确无误地描述程序设计语言的语法结构，这种严谨、简洁、易读的形式规则描述的语言结构模型称为文法。

BNF规定是推导规则(产生式)的集合，写为：

`符号 ::= <使用符号的表达式>`

这里的 <符号> 是非终结符，而表达式由一个符号序列，或用指示选择的竖杠 '|' 分隔的多个符号序列构成，每个符号序列整体都是左端的符号的一种可能的替代。从未在左端出现的符号叫做终结符。



补充：

`**`是右结合运算，例如：`2**2**3 === 256 === 2**8 ！== 4**3`

`/*等大部分`是左结合的运算，例如：`9/3/3 === 1 === 3/3 !== 9/1`

### 图灵完备性

- 命令式
  - goto实现
  - if和while实现
- 声明式
  - 递归实现

### 动态与静态

- 动态
  - 在用户设备/服务器
  - 产品实际运行时
  - Runtime
- 静态
  - 程序员设备
  - 产品开发时
  - Compiletime

### 类型系统

- 动态类型与静态类型
- 强类型与弱类型
  - 弱类型：类型检查不严格，允许隐式类型转换
  - 强类型：类型一旦确定就不能被转化
- 复合类型
  - 结构体：比如对象
  - 函数签名：比如(T1,T2) => T3
- 子类型
  - 逆变：能用Function<child>的地方，都能用Function<parent>
  - 协变：能用Array<parent>的地方，都能用Array<child>

语言类型举例：

js/php: 动态弱类型

ts/c++/c: 静态弱类型

python: 动态强类型

java/c#: 静态强类型

ts其实就是在js的基础上套了一个静态的类型系统

### 一般命令式编程语言

- Atom(原子，最小单位)
  - Identifier
  - Literal
- Expression(表达式)
  - Atom
  - Operator
  - Punctuator(符号)
- Statement(语句)
  - Expression
  - Keyword
  - Punctuator
- Structure(结构化)
  - Function
  - Class
  - Process
  - Namespace
- Program(程序)
  - Program
  - Module
  - Package
  - Library





## 词法，类型

### Unicode(字符集，字符的集合)

每个字符都对应一个码点，比如a对应的是97。

现在存在的字符都要兼容ASCII字符(一共128个)

```js
// 获取128个ASCII字符
for (let i = 0; i < 128; i ++){
    console.log(String.fromCharCode(i))
}
// https://www.fileformat.info/info/unicode/block/basic_latin/list.htm
```

### InputElement

- WhiteSpace(空格)
  - <tab> \t
  - <VT> \v 垂直制表符
  - <FF> \f 分页符
  - <nbsp>
  - <zwnbsp>
- LineTerminator(换行)
  - \n 正常换行
  - \r 回车
  - <LS> unicode中的行分隔符
  - <PS> unicode中的段落分隔符
- Comment
- Token
  - Punctuator
  - IdentifierName
    - identifier
    - keywords
    - 保留字
  - Literal(直接量)
    - Number
    - String
    - Boolean
    - Null
    - Undefined

