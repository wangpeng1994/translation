<Chapter 2: Data Access>

# One of the classic computer science problems is determining where data should be stored for optimal reading and writing. Where data is stored is related to how quickly it can be retrieved during code execution. This problem in JavaScript is somewhat simplified because of the small number of options for data storage. Similar to other languages, though, where data is stored can greatly affect how quickly it can be accessed later. there are four basic places from which data can be accessed in JavaScript:

```
optimal reading and writing 最佳的读写（效率）
retrieved 重新取回
somewhat simplified 有点（被）简化了的
similar to 与...相似

while vs as
  1. while 后面接延续性行为，这个行为一般比主语长
  2. as 意为 一边...一边，与...同时，重在表示动作同时发生、伴随进行
```

# Literal values
# Any value that merely represents just itself and isn't stored in a particular location. JavaScript literals include: strings, numbers, Booleans, objects, arrays, functions, regular expressions, and the special values null and undefined as literals.

```
particular vs special
前者强调与众不同的特殊性，后者强调主观上特定的某一个，其自身本质未必很特殊

place vs location vs position
  # https://zhidao.baidu.com/question/542551769.html
  1. place 含义广泛，最普通用词，所指地点可小可大
  2. location 指某物设置的方向或地点
  3. position 多指物体相对于其他物体所处的位置或状态
```

# Variables
# Any developers-defined location for storing data created by using the var keyword.

# Array items
# A numerically indexed location within a JavaScript Array object.

# Object members
# A strin-indexed location within a JavaScript object.

# Each data storage location has special reading and writing afford. In most cases, performance difference between access a literal and a location variable is tiny. The cost of Access array items and object mumbers will higher, How much higher is depend on the browsers. Figure 2-1 showing the time spent in operating these four data types 200,000 times in various browsers.


---

# 之前的做法有些慢，现在只记录个人认为值得记录的用词用法。


go all the way through 遍历

simplistic 过分简单化的

a huge performance improvement 巨大的性能改进

impressive performance improvements 出色的性能改进

dozens of 几十

being accessed repeatedly 被反复访问

temporarily augment 临时增加...


as follows 如下所示， 比 as the following 更合适


# 2019-09-27

pushed to 被推向；pushed into 被推入

For this reason, 正因为这个原因

As shown previously, 正如前面提到的，As mentioned before(above),


# 2019-09-29

...clause ...的子句

inside of 在...之内

appropriately 适当地

do plan on 计划...

likelihood 可能性

solution 解决办法

occur 发生（错误等）

then 那么

indicate 表明，说明

minimize 使最小化，减小

performance impact (n.) 性能影响

delegate to 委托给


# 2019-10-16

appropriate 适当的

appropriately 适当地

temporary 临时的

predetermined 预先确定的

static analysis 静态分析

lookup (n.) 查找

hash-based 基于散列的 基于哈希的

closely mirrors (v.) 密切反映 类似


# 2019-10-18

has been popularized 已经流行普及

ubiquitous 无处不在的

an activation object 一个激活对象

among other things, 除了其他方面


# 2019-10-19

side effect 副作用

as 以...的方式

nonnative 非本地

performance penalty 性能损失


# 2019-10-20

exercise caution (v.) 谨慎小心

advice vs suggestion
  1. 价值不同：advice 更有指导意义和价值；suggestion 不太靠谱，只是斗胆发表了未必成熟的想法
  2. 针对的对象不同：advice 针对某一行动提出的；suggestion 针对某一问题，尤其为解决困难或改进工作提出的

by vs through vs with vs via
  1. by 侧重通过某种方式；through 侧重穿过、通过
  2. by 通常直接介绍发生作用或影响的动因；through 介绍的对象则比较间接
  3. with 通常与无生命的物体一起使用，指具体工具、手段或媒介
  4. via 经由、通过、凭借、借助于，指侧重通过某种媒介达到目的


frequently used 常用的

# 2019-11-11

As such, 因此

Since 因为

in addition to 除...之外

reference n. v. 引用

considered 被认为是...

whereas 然而，鉴于，但是，反之

literal 字面量，直接量


# 2019-11-15

tied to 把...绑定到

expose 开放，暴露

internal 内部的

build-in 内置的


# 2019-11-25 (2-9)

relation vs relationship
  1. 前者较不带感情，事实性的“关系”
  2. 后者主要形容人与人（或者拟人）之间的亲密关系


# 2019-11-27 (2-10)

determine v. 确定

pass in 传入（参数）


# 2019-11-28

everything else 其它的

suspect v. 怀疑，猜想

retrieve v. 取回，检索

perform v. 执行，机器运转

incur v. 引发，招致 （incur a performance penalty 引发性能损失）

overhead n. 开销

travese v. 遍历

amplify v. 放大，扩大，增强


# 2019-11-29

contain vs include
  1. 包含 vs 包括
  1. contain 强调容量，侧重内有，多用于客观事物，如容器有什么，什么东西有什么成分
  2. include 强调范围，所含之物一般是主语的同类，是同种事物之间的包含

to be more accurate 更精确地（说）

clearly 明显地

course 过程

yet ... 但仍然

eliminate v. 消除