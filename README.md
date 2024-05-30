# interview







相关链接：

[计算机考研面试题（关于408）](https://zhuanlan.zhihu.com/p/475519720)

[香港大学的面试题](https://github.com/xiahouzuoxin/notes/blob/master/essays/%E6%89%BE%E4%BA%86%E5%87%A0%E9%81%93%E7%A0%94%E7%A9%B6%E7%94%9F%E5%A4%8D%E8%AF%95%E9%9D%A2%E8%AF%95%E9%A2%98.md)

[计算机考研面试题](https://www.cnblogs.com/lihello/p/13326858.html)



## 课程

### 算法

快速排序的时间复杂度（平均和最差）

### 数据结构

+ 数组和链表的区别
+ 二维数组和指针的关系
+ 栈和队列的区别
+ 如何从尾到头打印单向链表，不改变链表结构



什么是多态？

调用成员函数时，会根据调用函数的对象的类型来执行不同的函数。





哈夫曼树怎么实现，时间复杂度：

使用堆（nlogn）



并查集：

+ 对于n个元素的并查集，l个操作，复杂度为n+l
+ 路径压缩
+ 按秩排序





### 计算机组成原理

在32位机器上，指针的大小

什么是冯诺依曼体系结构

中断的作用



什么是冯诺依曼体系结构？

+ CPU、存储器、控制器、IO组成

+ 采用存储程序的方式：任何要计算机完成的工作都要先被编写程序，然后将程序和原始数据送入主存并启动执行，一旦程序执行开始，计算机就能在不需操作人员干预下，自动完成逐条取出指令和执行指令的任务
+ 内部以二进制标识指令和数据



分页的作用、好处和原因：

作用：（实际上是使用逻辑空间的好处）

+ 扩大寻址空间（使用逻辑空间的好处）
+ 多进程内存保护
+ 将内存划分成页为单位，一定程度上解决了内存碎片的问题













### 操作系统

什么是操作系统？

+ 管理计算机硬件与软件资源的程序
+ 软件通过操作系统来获取硬件资源
+ 操作系统统筹了硬件的各项事宜，屏蔽了硬件的复杂性



操作系统内核和操作系统？

操作系统内核是操作系统的核心部分，它负责管理硬件的内存管理，硬件设备管理，文件系统管理，以及应用程序的管理



操作系统的六大功能：

+ 进程和线程的管理
+ 存储管理
+ 文件系统
+ 设备管理
+ 网络管理
+ 安全管理



什么是用户态和内核态？

用户态和内存态是一种进程在系统上运行的权限等级

+ 用户态运行的进程看可以直接读取用户程序的数据，拥有较低的权限，当需要进行一些特殊操作如写磁盘和硬盘，需要进行权限的转换

+ 内核态运行的内存几乎可以访问计算机的任何资源包括系统的内存空间，设备权限，当操作系统接收到进程的的系统调用，就会从用户态切换到内核态，执行相应的系统调用，并将结果返回给进程，最后再从内核态切换成用户态



切换的方式

+ 访管（trap）
+ 中断
+ 异常



为什么需要系统调用？

+ 直接访问硬件可能会导致系统的不稳定性
+ 抽象的接口利于使用



有了进程为什么还要线程

+ 线程切换开销较小
+ 更轻量化，一个进程可以创建多个线程
+ 有了线程的进程可以做多件事
+ 同一进程内的线程共享内存和文件，因此无需调用内核



线程间同步方式

+ 锁：互斥锁、自旋锁、读写锁
+ 信号量
+ 事件驱动
+ 屏障



进程间通信:

+ 管道
+ 共享内存
+ 套接字
+ 消息队列





进程与线程的区别。操作系统设计中为什么要在进程的基础上提出线程的概念

进程调度的方法



静态链接和动态链接

+ 静态：静态库代码被复制到可执行文件中
+ 链接发生在编译器
+ .lib和.a
+ 更新要重新编译
+ 运行快



动态链接库：

+ 只记录动态库的符号引用
+ 链接在运行时，动态链接库的代码被加载到内存中
+ 动态库.dll和.so
+ 独立更新
+ 运行慢



什么是虚拟内存？

简单来说进程访问物理内存的简化的内存管理



如果没有虚拟内存：

+ 用户进程可以访问任意物理内存，可能影响到操作系统的运行，造成崩溃
+ 程序的所有数据或指令都要载入物理内存



寻你地址和物理地址转换

MMU （memory management unit）来将虚拟地址转化成物理地址

+ 分段机制
+ 分页机制
+ 段页机制



页面置换算法：

+ 最不常使用
+ 先进先出
+ 最久未使用



局部性：

+ 时间局部性：程序中存在一些循环或者重复操作，会反复访问同一个页或一些特定的页
+ 空间局部性：程序中数据和指令的访问通常具有一定的空间连续性



文件系统：

什么是硬链接：

+ 使用同一个inode，源头是同一个文件
+ 只有删除了源文件和所有对应的硬链接文件才算真正的删除
+ 不能对目录以及不存在得文件创建硬链接， 该文件才会被真正删除



什么是软链接：

+ 软连接和源文件得inode节点号不饿同，而是指向同一个文件路径
+ 源文件删除后，软连接依然存在，但是指向的是一个无效的文件路径
+ 可以为目录或者不存再文件创建软连接，软连接可以跨越文件系统





磁盘调度算法

+ 先到先服务
+ 最短寻道时间优先算法
+ 扫描算法
+ 循环扫描算法（c会1-n后又是1-n）
+ look（look不到头）
+ c-look













### 计算机网络

IP/TCP协议栈包括那几层，UDP属于哪层协议的

介绍一下CSMA/CD



IPV6出现的动力：

+ IPv4不够用了



报文头发生了哪些变化：

+ 地址发生了变化，IPV6 是16个字节







### 自动机

介绍一下np和p：

+ 一般来说：
  + np指的是多项式时间可以验证的问题集合
  + p指的是多项式时间内可以解决的问题集合
+ 严谨来说是：
  + np是一类语言，它们在一个但纸带、非确定性图灵机上是多项式时间可判定的
    + 或者这类语言存在着一个多项式时间的确定性的验证机
  + p是一类语言，它们在一个单纸带，确定性图灵机上是多项式时间可判定的



什么是算法：

+ 是指一个被定义好的、计算机可实行其指示的有限步骤或次序
+ 严谨来说，算法是一个图灵机，其通过终止状态接收，无论接受与否，它都注定会停机



什么是时间复杂度：

+ 描述算法在输入规模增加时，执行所需要的时间是如何变化的
+ 算法图灵机在接收长度为n的字符串时跳转的最大步骤

什么是空间复杂度：

+ 描述算法在输入规模增加时，执行所需要的空间的变化
+ 算法图灵机在接收长度为n的字符串时所扫过的最大纸带格子数



DFA

NFA

PDA



### 编译原理

编译过程：

c文件 -> 预处理（宏定义、条件编译展开）-> 编译（汇编代码）-> 汇编（可重定目标程序）-> 链接器



词法分析 ->语法分析 ->语义分析 ->中间代码生成 ->中间代码优化 -> 目标代码生成



什么是词法分析：

将构成程序的字符流进行扫描，然后根据构词规则识别单词（标识符，变量名，常量等），检查是否存在不满足构词规则的单词，构词规则一般是正则表达式描述



什么是语法分析：

在词法分析的基础上，将单词流按照语法规则组合成各种类型的语法短语，如程序，语句，表达式等，检查是否存在不满足语法规则的单词流，语法规则使用上下文无关语法描述

+ 括号是否匹配
+ 关键字是否使用正确

+ 。。。



什么是语义分析：

审查源程序有无语义错误，为代码生成阶段生成类型信息

+ 赋值语句左右类型是否一致，或者相容
+ 函数返回值和函数签名是否一致，或相容
+ 形参和实参类型是否一致

从而构成一些符号表：

符号表存储了什么信息：

标识符名称：变量名、函数名、类型

标识符类型：整数、结构体、数组、函数

标识符的作用域：局部变量、全局变量、类成员





中间代码生成：

将原程序代码生成一种内部标识形式，如三地址码、四元式、三元式、抽象语法树



SSA是什么：

SSA（static single assignment form） 是 一种特定形式的中间表达式，每个变量只被赋值一次



什么是前端：

词法分析、语法分析、语义分析、中间代码生成、中间代码优化



什么是后端：

目标代码生成



有穷自动机：

为什么是有穷的：

+ 状态和输入字母表是有穷的



NFA和DFA的区别：

+ 状态的输出是一个集合
+ 初态可以存在多个
+ NFA存在epsilon转移，即没有输入的转移
+ 子集构造法可以将NFA转化成DFA



语法分析方法：

+ 自顶向下的语法分析规则：
  + LL（1）：根据当前的输入唯一确定选用那个产生式替换非终结符
+ 自下而上的分析方法：
  + 根据文法的产生式规则，把产生式的右部替换成左部
  + LR（0）：不根据first、follow等信息
  + SLR（1）：使用first、follow等信息
  + LR（1）：向前看1，减少移入、规约冲突
  + LALR（1）：对LR（1）计算项目集规范族合并同心项



**分析表比较：LR(0)、SLR(1)、LR(1)、LALR(1)**
1.LR(0)分析表局限性大，但其构造方法是其他构造方法的基础；
2.SLR分析表虽然不是对所有文法都存在，但这种分析表较易实现又极有使用价值；
3.LR分析表的分析能力最强，能适用于一大类文法，但是，实现代价过高（表过大）；
4.LALR分析表的能力介于SLR和LR之间，实现效率较高。



中间代码优化不依赖于计算机
对比目标代码优化（这是依赖于具体的计算机的）
优化所需要的基础是在中间代码生成之后或者目标代码生成（不只是中间代码可以优化唔）之后。





代码优化：

+ 公用子表达式

+ 合并已知项
+ 强度消弱
+ 删除无用赋值（死代码检测）



循环优化：

+ 代码外提
+ 归纳变量
+ 循环合并
+ 循环展开
+ 强度消弱





### 离散数学

全序：反对称、传递、完全

偏序：自反、传递、反对称

+ 自反：a和a有偏序关系
+ a<= b, b<= a, a = b
+ 传递

什么是树：

+ 最大无环图和最小联通图，n个节点，n-1条边



群：

+ 集合+ 二元操作
+ 公理：（有幺有逆，结构封闭）
  + 封闭性
  + 结合性
  + 幺元
  + 逆元



格：

+ 偏序集
+ 任意两个元素都有最小上界和最大下界



欧拉图：

+ 存在欧拉回路的图
  + 欧拉回路：经过所有点（不重复）的一个环
  + 充分必要条件：奇顶点个数为0，欧拉通路是仅有2个奇顶点
+ DFS



哈密顿图：

+ 存在哈密顿回路的图
  + 哈密顿回路：经过所有边的一个环
  + 充分条件： 图中每一对顶点度数之和大于n-1，为哈密顿通路， n的话就是哈密顿回路
  + 必要条件：太复杂了



等价关系：

自反、传递、对称





二分图：

+ 二部图，图上的节点可以分成两个数组，并且这两个数组

将一个图分成二分图：

染色法：一个边黑红，如果发现一个边的两个节点都被染色，并且是相同颜色则不存在二分图

二分图的充分必要条件：

+ 至少有两个顶点
+ 所有的回路的长度都是偶数









### 并发算法

什么是死锁

死锁的几个必要条件： 循环等待、不可抢夺、互斥、占有并等待

并行和并发：

+ 并行：当系统有一个以上的CPU时，当一个CPU执行一个进程时，另外一个CPU可以执行另一个进程，两个进程互相不抢占资源可以同时进行
+ 并发：一个处理器在一个时间段内处理了多个任务，每个任务是不同的事件篇



读者写者问题：







### 数据库

操作系统的文件系统和数据库文件系统的区别：

+ 数据库采用表格的形式来组织数据，使用表、行和列存储数据，这些数据通常是结构化的，具有明确的关系；操作系统采用层次结构来阻止文件和目录，使用文件夹、文件等来进行存储

+ 数据库需要支持复杂的操作，如SQL查询语言，提供食物管理和数据完整性保护等；操作系统只需要支持如文件的创建、读取、写入和删除即可

  





### AI

大数定理



## 线代

线性相关：

+ 一组向量v1 v2 v3...，存在常数a, b,c ,..., st. av1+ bv2+ cv3... = 0,且这些常数不全为零

+ 一个向量可以为其他向量线性表示



矩阵的秩：

+ 一个向量的线性无关的向量的集合的势



矩阵的特征值：

+ 满足Ax = 入x（入是特征值，x是特征向量）
+ 当A为实数对称矩阵的话，A可以进行分解



如何求解线性方程组：

+ Ax = b
+ A列满秩一定要么没有解（b不在A的列空间里），唯一解（b在A的列空间）
+ A不是列满秩是没有解和有多个解

迭代法：

+ 高斯迭代
+ 雅可比迭代







## 计算机语言

### C/C++语法

C++中struct和class的区别

static作用于局部变量和c文件中的函数前有什么区别

new和malloc的区别：

+ new是关键字和malloc方法
+ new会调用构造函数
+ new产生的指针有类型



`void* p`p可以指向什么类型



静态绑定是程序编译时确定的程序行为

动态绑定是程序运行时来确定程序的行为



C++和python的区别

+ C++是静态类型，python是动态类型的
+ C++的编译执行的，python主要是解释执行
+ C++要手动管理堆内存，python不需要
+ C++性能更高，python相对来说没有那么快
+ 语法不同
+ 应用场景不同：C++写于硬件相关或游戏，python写脚本



C++和java的区别

+ C++要手动管理堆内存，java不需要
+ C++是混合风格的语言，Java 主要面向对象
+ C++允许多继承，java不能多继承，但可以实现多个接口



指针和引用有什么区别？

+ 指针可以为空，引用不能为空
+ 指针可以改变指向（没有const等限制），引用可以为空
+ 指针大小为系统内指针的大小，引用的大小为其指向的变量的大小
+ 引用没有空所以更加安全



java类加载：

- 通过一个类的全限定名来获取定义此类的二进制字节流。
- 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构。
- 在内存中生成一个代表这个类的 java.lang.Class 对象，作为方法区这个类的各种数据的访问入口。



动态类型语言：动态性语言是指在运行期间才去做数据类型检查的语言，也就是说动态类型语言编程时，永远不用给任何变量指定数据类型，该语言会在第一次赋值给变量时，在内部将数据类型记录下来。Python和Ruby就是一种典型的动态类型语言，其他的各种脚本语言如VBScript也多少属于动态类型语言。

静态类型语言：静态类型语言与动态类则刚好相反，它的数据类型在编译期间检查，也就是说在写程序时要声明所有变量的数据类型，C/C++是静态类型语言的典型代表，其他静态语言还有C#、Java等。



## 英语

英语介绍课程

