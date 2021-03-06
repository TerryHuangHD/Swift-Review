# Swift-Review

本项目的问题来自脉脉职言区的[帖子](https://taou.cn/plVM0)，看到之后感觉挺有意思的，有一些知识会用但是不知道原理。借着这次机会深入的了解一下，顺便对自己的知识点进行一次查漏补缺。问题的答案有的是自己写的，有的是摘录博客上的，如有错误欢迎指出。目前只更新了一部分问题的答案，之后会慢慢更新的，如果你有兴趣，欢迎你一起回答问题。



## 目录

- [Swift 底层本质](#Swift-底层本质)
  - [关键字](#关键字)
  - [探究本质](#探究本质)
  - [特性和优化](#特性和优化)
- [UI](#UI)
  - [图像显示、卡顿优化和离屏渲染相关的问题](#图像显示、卡顿优化和离屏渲染相关的问题)
  - [图片加载](#图片加载)
  - [视图绘制](#视图绘制)
  - [事件传递/响应机制](#事件传递/响应机制)
  - [TableView](#TableView)
- [内存](#内存)
  - [内存基础](#内存基础)
  - [内存布局](#内存布局)
  - [循环引用](#循环引用)
  - [自动释放池](#自动释放池)
  - [Copy on write](#Copy-on-write)
- [多线程](#多线程)
  - [多线程基础](#多线程基础)
  - [GCD](#GCD)
  - [多线程同步和锁](#多线程同步和锁)
  - [Perform Selector](#Perform-Selector)
- [RunLoop](#RunLoop)
  - [RunLoop 基础](#RunLoop-基础)
  - [Runloop 的常见问题](#Runloop-的常见问题)
  - [Runloop 的应用](#Runloop-的应用)
- [Runtime](#Runtime)
  - [Runtime 数据结构](#Runtime-数据结构)
  - [isa 指针](#isa-指针)
  - [Runtime 消息机制](#Runtime-消息机制)
  - [Runtime 的实际应用](#Runtime-的实际应用)
  - [Swift 中的 Runtime](#Swift-中的-Runtime)
- [KVO & KVC](#KVO-&-KVC)
  - [KVC](#KVC)
  - [KVO](#KVO)
  - [Swift 中的 KVO 和 KVC](#Swift-中的-KVO-和-KVC)
- [网络相关](#网络相关)
  - [网络基础](#网络基础)
  - [网络常见问题](#网络常见问题)
- [数据结构和算法](#数据结构和算法)
  - [数据结构基础](#数据结构基础)
  - [算法](#算法)
  - [实际问题](#实际问题)
  - [其他常见算法](#其他常见算法)





## Swift 底层本质

### 关键字

- [Self 和 self 的区别？](MD/Swift底层本质/关键字/Self和self的区别.md)
- [.self 的理解？](MD/Swift底层本质/关键字/self.md)
- [.type 和 type(of: ) 的区别？](MD/Swift底层本质/关键字/type.md)
- [Any, AnyObject, Anyclass 的区别？](MD/Swift底层本质/关键字/Any.md)
- [is, isKind, isMenber 的区别？](MD/Swift底层本质/关键字/is.md)
- [throws 和 rethrows 的区别？](MD/Swift底层本质/关键字/throws.md)
- [open, public, internal, fileprivate, private 的区别？](MD/Swift底层本质/关键字/权限.md)



### 探究本质

#### Swift 各种属性的本质

- [let 和 var 的区别？](MD/Swift底层本质/探究本质/let和var的区别.md)
- [计算型属性的本质是什么？占多少个字节？是存储在当前对象里的吗？可以用 let 修饰吗？](MD/Swift底层本质/探究本质/计算属性.md)
- [枚举的原始值的本质是什么？占几个字节？它在内存中是存储在枚举里吗？](MD/Swift底层本质/探究本质/枚举.md)
- [枚举可以定义存储属性吗？枚举可以定义类型存储属性吗？](MD/Swift底层本质/探究本质/枚举2.md)
- [lazy 属性可以用 let 修饰吗？lazy 属性是线程安全的吗？](MD/Swift底层本质/探究本质/lazy.md)
- [观察型属性在初始化的时候会触发吗？定义的时候给定默认值会触发吗？](MD/Swift底层本质/探究本质/观察属性.md)
- [inout 修饰的函数参数本质是什么？](MD/Swift底层本质/探究本质/inout.md)
- [inout 参数能传递计算属性吗？传递计算属性的底层原理是什么？](MD/Swift底层本质/探究本质/inout2.md)
- [inout 参数传递观察型属性会触发观察的 willSet 和 didSet 方法吗？底层原理是什么？为什么这样设计？](MD/Swift底层本质/探究本质/inout3.md)
- 类型存储属性和 lazy 一样是延迟加载吗？如果一样那么是线程安全的吗？为什么？



#### String, Array, Option 本质

- [String 类型占多少个字节？String 类型变量的字面量在内存中是怎样存储的？](MD/Swift底层本质/探究本质2/String.md)
- [数组在内存中占多少个字节？数组存储在栈空间还是堆空间？](MD/Swift底层本质/探究本质2/Array.md)
- [可选类型的本质？](MD/Swift底层本质/探究本质2/Option.md)



#### Swift 闭包的本质

- [闭包是什么？闭包表达式和闭包是什么关系？](MD/Swift底层本质/闭包/闭包.md)
- [闭包值捕获的原理是什么？捕获到的值存储在哪里？](MD/Swift底层本质/闭包/闭包捕获.md)
- [捕获多个值时它们在内存中是连续存储的吗？]((MD/Swift底层本质/闭包/闭包捕获2.md))
- [一个捕获到 Int 值的闭包在内存中占几个字节？]((MD/Swift底层本质/闭包/闭包捕获3.md))
- [DispatchQueue.async 闭包体内为什么要强制加 self. 访问成员变量？](MD/Swift底层本质/闭包/DispatchQueue.md)
- [逃逸闭包是什么？](MD/Swift底层本质/闭包/逃逸闭包.md)



#### Swift 多态&方法派发

- [Swift 里是怎样实现多态的？](MD/Swift底层本质/多态/多态.md)
- [Swift 支持哪些方法派发方式？引用类型、值类型、协议的方法派发有什么不同？](MD/Swift底层本质/多态/方法派发.md)
- [为什么建议使用 struct 而不使用 class？](MD/Swift底层本质/多态/Q1.md)



#### Swift 里的指针

- [Swift 里有那几种类型的指针？有什么区别？](MD/Swift底层本质/指针/指针.md)



### 特性和优化

#### 函数和协议编程 Swift 反射机制 Swift 性能优化

- [大概描述一下 Swift 的编译流程？Swift 和 OC 的区别？](MD/Swift底层本质/特性和优化/Swift编译流程.md)
- 面向协议编程的理解？对函数式编程的理解？
- [map, flatMap, compactMap 的区别？](MD/Swift底层本质/特性和优化/map.md)
- [filter, reduce 的区别？](MD/Swift底层本质/特性和优化/filter-reduce.md)
- [对反射机制的理解？](MD/Swift底层本质/特性和优化/反射.md)
- [如何优化 Swift 性能？](MD/Swift底层本质/特性和优化/优化.md)





## UI

### 图像显示、卡顿优化和离屏渲染相关的问题

- [图像绘制的原理和过程？](MD/UI/图像/图像绘制.md)
- [卡顿掉帧的原因？卡顿掉帧应该怎么优化？](MD/UI/图像/卡顿掉帧.md)
- [什么是离屏渲染？为什么会有离屏渲染机制？离屏渲染消耗性能的原因？](MD/UI/图像/离屏渲染.md)
- [哪些场景会触发离屏渲染？怎么解决？](MD/UI/图像/Q1.md)



### 图片加载

- 图片加载优化原理
- 如何设计一个图片缓存框架？缓存清理怎样设计？
- UllmageView 的 name和 contentOfFile 方法有什么区别？注意点？
- iOS 图片加载的详细流程是什么？应该怎样去优化？
- 简单说一下图片后台强制解压缩的流程？



### 视图绘制

- 视图绘制的全流程有哪些阶段？
- 什么是异步绘制，怎样进行异步绘制？
- 系统绘制的流程是怎样的？视图绘制优化方案？drawRect 注意点？



### 事件传递/响应机制

- [手指触摸屏幕后发生了什么？事件的传递和响应链是怎么样的？](MD/UI/事件传递和响应/事件.md)
- [hitTest 内部实现逻辑？](MD/UI/事件传递和响应/hitTest.md)
- 事件传递具体有哪些应用场景？



### TableView

- 对 TableView 重用机制的理解？
- 如何实现一个自定义的重用池？
- 重用可能带来的问题，平常是怎么解决的？
- 重用 Cell 的获取方式和区别？
- 多线程情况下数据源同步方案？
- TableView 常用方法的理解和注意点？
- TableView 的一般优化思路是什么？





## 内存

### 内存基础

- [iOS 内存布局结构？](MD/内存/基础/iOS内存布局.md)
- [堆区和栈区的区别？为什么要设计堆和栈，主要解决哪些问题？](MD/内存/基础/堆区栈区.md)
- Swift 对象堆空间申请过程？
- Swift 里 let 和 var 变量的内存布局有何不同？
- [内存对齐是什么？为什么要内存对齐？对齐的规则？](MD/内存/基础/内存对齐.md)
- [引用计数的存储方式？](MD/内存/基础/引用计数.md)
- [ARC 在编译时和运行时分别做了哪些工作？](MD/内存/基础/ARC.md)
- [retain, release 的实现机制？](MD/内存/基础/retain-release.md)
- 你对 iOS 内存管理的理解？



### 内存布局

- [结构体的内存布局？](MD/内存/布局/结构体.md)
- [类的内存布局？](MD/内存/布局/类.md)
- [枚举的内存布局？有原始值的布局是怎样的？有关联值的布局又是怎样的？](MD/内存/布局/枚举.md)
- [协议的内存布局？协议的属性存储在什么地方？VWT 是什么？PWT 又是什么？](MD/内存/布局/协议.md)
- Swift 和 OC 类对象内存布局的区别？



### 循环引用

- [对循环引用的理解？强引用和弱引用的区别？](MD/内存/循环引用/循环引用.md)
- [weak 和 unowned 有什么区别？](MD/内存/循环引用/weak-unowned.md)
- [weak 指针实现原理？为什么对象销毁后会被置为 nil？](MD/内存/循环引用/weak.md)
- 在 SideTable 里的存取过程又是怎样的？Side Table 的组成？为什么有多张 Side Table？Side Table 为什么会有一把自旋锁？
- 说说循环引用的场景和解决思路？闭包为什么会产生循环引用？手写循环引用例子



### 自动释放池

- [什么是自动释放池？自动释放池的管理原理是怎样的？](MD/内存/自动释放池/autoreleasepool.md)
- [AutoreleasePool 和 Runloop 的关系？](MD/内存/自动释放池/autoreleasepool-runloop.md)



### Copy on write

- [什么是 Copy on write？](MD/内存/copy-on-write/copy-on-write.md)
- [如何为结构体手动实现 Copy on write？](MD/内存/copy-on-write/Q1.md)
- Swift 对象的深度复制(使用 Codable 协议)





## 多线程

### 多线程基础

- [进程是什么？有哪几种状态？进程和线程的区别？](MD/多线程/基础/进程.md)
- [什么是并发？什么是并行？并发和并行的区别？](MD/多线程/基础/并发.md)
- [对多线程的理解？多线程的底层原理？多线程的优缺点？](MD/多线程/基础/多线程理解.md)
- [多线程有哪些实现方案？](MD/多线程/基础/多线程方案.md)
- [怎样实现一个常驻线程？自定义 Runloop 的应用线程保活？](MD/多线程/基础/常驻线程.md)
- [多线程会有哪些安全隐患？一般有什么解决方案？](MD/多线程/基础/多线程隐患.md)
- [死锁产生的条件有哪些？](MD/多线程/基础/死锁.md)
- [多线程间怎么通信？底层原理是什么？](MD/多线程/基础/多线程通信.md)
- NSThread(对应 Swift 中的 Thread)内部实现的原理是什么？启动流程又是怎样的？2 种初始化方法有什么区别？



### GCD

- [创建一个 GCD 队列？各个参数有什么作用？](MD/多线程/GCD/队列.md)
- [GCD 有哪几种队列？主队列和全局队列分别是什么队列？](MD/多线程/GCD/队列2.md)
- [GCD 队列的执行方式有什么区别？不同队列不同执行方式的区别？主队列异步执行多个任务会开启新线程吗？为什么？](MD/多线程/GCD/队列3.md)
- [GCD 什么情况会发生死锁？原因是什么？](MD/多线程/GCD/死锁.md)
- [GCD 任务提交方式有哪些？DispatchWorkItem 提交有什么好处？](MD/多线程/GCD/任务提交.md)
- [GCD 延迟执行 DispatchTime 和 DispatchWillTime 有什么区别？](MD/多线程/GCD/延迟执行.md)
- [DispatchSource 的理解？](MD/多线程/GCD/DispatchSource.md)
- [DispatchSourceTimer 和 Timer 比哪个更精准的？](MD/多线程/GCD/DispatchSourceTimer.md)
- [DispatchGroup 的底层原理是什么？一般用在什么场景？有哪几种添加进组的方式？](MD/多线程/GCD/DispatchGroup.md)
- [barrier 的理解？](MD/多线程/GCD/栅栏.md)
- [DispatchSemaphore 的理解？对信号量控制方法的理解？信号量底层原理是怎样？](MD/多线程/GCD/DispatchSemaphore.md)



### 多线程同步和锁

- [多线程同步方案有哪些？哪些锁的性能最好？](MD/多线程/多线程同步和锁/锁.md)
- [线程同步的各种锁的理解？有哪几种类型？](MD/多线程/多线程同步和锁/各种锁的理解.md)
- [OSSpinLock 不安全的原因？](MD/多线程/多线程同步和锁/OSSpinLock.md)
- [os_unfair_lock 怎样使用？](MD/多线程/多线程同步和锁/os_unfair_lock.md)
- [pthread_mutex 锁的理解？有哪几种类型？](MD/多线程/多线程同步和锁/pthread_mutex.md)
- [NSLock 和 NSRecursiveLock 的理解？](MD/多线程/多线程同步和锁/NSLock.md)
- [NSConditionLock 条件锁的理解？怎样使用？](MD/多线程/多线程同步和锁/NSConditionLock.md)
- [文件读写安全方案(多读单写)有哪几种解决方案？](MD/多线程/多线程同步和锁/多读单写.md)



### Perform Selector

- [你对 Perform Selector 几个方法的理解？哪几种方法是同步执行的？哪几种方法是异步执行的？](MD/多线程/PerformSelector/PerformSelector.md)





## RunLoop

### RunLoop 基础

- [什么是 RunLoop？](MD/RunLoop/基础/RunLoop.md)
- [RunLoop 的启动方式有哪些？](MD/RunLoop/基础/run.md)
- [RunLoop 的退出方式有哪些？](MD/RunLoop/基础/stop.md)
- [RunLoop 和线程有什么关系？线程间如何通信？](MD/RunLoop/基础/thread.md)
- [RunLoop 有哪几种 mode？对常见 mode 的理解？](MD/RunLoop/基础/mode.md)
- [RunLoop 的事件源有哪些？特点是什么？](MD/RunLoop/基础/source.md)
- [RunLoop 的监听状态有哪些？怎样监听？](MD/RunLoop/基础/observer.md)
- [RunLoop 的内部循环逻辑是怎样的？](MD/RunLoop/基础/loop.md)



### Runloop 的常见问题

- [RunLoop 和 AutoreleasePool 的关系？](MD/RunLoop/常见问题/AutoreleasePool.md)
- [事件响应的过程？](MD/RunLoop/常见问题/事件响应.md)
- [手势识别的过程？](MD/RunLoop/常见问题/手势识别.md)
- [UI 绘制 setNeedsDisplay 的原理？](MD/RunLoop/常见问题/UI.md)
- [定时器滑动失效的原因？怎样处理？为什么 Timer 不精准？如何实现精准的定时？](MD/RunLoop/常见问题/Timer.md)
- [Perform Selector after Delay 的实现原理？](MD/RunLoop/常见问题/PerformSelector.md)
- [GCD 和 Runloop 的关系？](MD/RunLoop/常见问题/GCD.md)



### Runloop 的应用

- [如何实现一个常驻线程？](MD/RunLoop/应用/常驻线程.md)





## Runtime

Runtime 相关的知识点一环扣一环，如果你对 Runtime 还不了解，建议先阅读[这个系列](https://www.jianshu.com/p/30de582dbeb7)的文章，读完之后下面这些问题就都迎刃而解了。

### Runtime 数据结构

- [Runtime 中的数据结构有哪些？](MD/Runtime/数据结构/数据结构.md)



### isa 指针

- [isa 的指向关系？](MD/Runtime/isa/isa.md)
- [实例对象、类对象和元类对象的联系和区别有哪些？](MD/Runtime/isa/实例对象、类对象和元类.md)
- [ARM 64 位之后 isa 优化原理？](MD/Runtime/isa/优化.md)



### Runtime 消息机制

- [消息发送的过程是怎样的？](MD/Runtime/消息机制/消息发送.md)
- [动态方法解析阶段的过程？](MD/Runtime/消息机制/动态方法解析.md)
- [消息转发的过程是怎样的？](MD/Runtime/消息机制/消息转发.md)



### Runtime 的实际应用

- Runtime 常用的 API 有哪些？
- 平常有用过 Runtime？一般来干什么？怎样实现？



### Swift 中的 Runtime

- 你对 Swit 中 Runtime 的理解？





## KVO & KVC

### KVC

- 什么是 KVC？
- KVC 的本质？
- KVC 的实现机制是怎样的？
- KVC 设/取值流程是怎样的？
- KVC 修改属性时如果该属性被 KVO 观察的话会触发 KVO 吗？为什么？



### KVO

- 什么是 KVO？
- KVO 的本质是什么？
- KVO 的实现机制是怎样的？
- KVO 设取值观察原理是怎样的？派生类的内部实现逻辑又是怎样的？



### Swift 中的 KVO 和 KVC

- Swift 中有没有 KVC？原理是什么？
- Swift 中如何使用 KVO？需要注意什么？





## 网络相关

### 网络基础
#### HTTP

- 你是怎样理解 HTTP？具体包含哪些内容？报文结构？
- HTTP 请求方案？状态码的含义？
- POST 请求体常见格式？
- GET/POST 的区别？从语义角度？常规角度？
- GET 安全性的理解？幂等性的理解？可缓存的理解？
- HTTP 连接和断开流程？三次握手流程？为什么3次而不是2次？四次挥手流程？为什么4次？
- HTTP 的特点？对无连接的理解？为什么HTTP要持久连接？
- 持久连接涉及到的头部字段？怎样判断一个持久连接的请求是否结束？



#### TCP/UDP

- 简单说一下 TCP/UDP 首部格式？
- TCP/UDP 的特点？
- UDP 无连接的理解？面向报文的理解？
- TCP 面向连接的理解？TCP 为什么是可靠的？原理是什么？可靠传输有什么特点？
- TCP 面向字节流的理解？
- TCP 流量控制的理解？原理是什么？
- TCP 拥塞控制的理解？有哪几个阶段？过程是什么？什么是快速重传机制？
- TCP 建立连接的过程？为什么3次握手而不是2次？为什么要4次挥手？



#### DNS 解析

- DNS 的理解？
- 查询方式？
- 如何防劫持？
- 和HTTP有关系吗？



#### Session 和 Cookie

- Session 和 Cookie 的理解？
- 交互流程？
- 有什么区别？



### 网络常见问题

- 怎样实现文件的断点下载？基本原理是什么？
- 如何处理大文件的上传下载？边下边写基本原理？分段读取基本原理？
- Alamofire 的理解？有哪几个模块？请求的过程？
- Moya 的理解？主要解决什么问题？





## 数据结构和算法

### 数据结构基础

- 你对数据结构的理解，什么是逻辑结构？什么是物理结构？常见数据结构有哪些？有什么特点？
- 线性表的特点是什么？说一下线性链表和顺序表的优缺点对比？各自适用什么场景？
- 栈的概念？有哪些基本操作？特点？什么是假溢出？
- 队列的概念？有啷些基本操作？特点？
- 什么是树？树的度？树的深度又是什么？
- 什么是二叉树？满二叉树的概念？完全二叉树的概念？
- 二叉树的先序遍历、中序遍历、后序遍历方式是怎样的？



### 算法

#### 排序

- 冒泡排序
- 选择排序
- 插入排序
- 快速排序



#### 链表

- 寻找单链表的中间元素？
- 判断一个链表是否有环？有环则找出入口节点？有环则找出环上节点数？
- 判断 2 个无环单链表是否相交？相交则找出交点？
- 反转单链表？
- 合并 2 个有序单链表？
- 找到链表的倒数第 n 个节点？
- 删除链表内倒数第 n 个节点？
- 旋转单链表？
- 倒序打印链表节点值？
- 删除有序链表中等于给定值的所有节点？
- 删除有序链表中值重复的节点(去重和重复的都删除 2 种情况)？
- 划分链表相关问题？奇偶链表？



#### 二叉树

- 求二叉树深度？
- 反转一颗二又树？
- 平衡二叉树判断？对称二叉树判断？相同二叉树判断？
- 二叉搜索树的查找？



### 实际问题

- 寻找两个 View 共同父视图？
- 查找 View 上的所有 Button 控件(包含子 View)？
- 查找 View 所在的视图控制器？



### 其他常见算法

- 字符串反转
- 只出现过一次的字符
- 有序数组合并
- 寻找数组中只出现一次的数(除了一个出现一次，其他都出现 2 次)
