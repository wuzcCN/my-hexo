---
title: InterviewQuestions
copyright_url: https://www.aobayu.cn/2022/11/20/InterviewQuestions/
tags: 
    - InterviewQuestions
categories: 学习之路
date: 2022-11-20
keywords: InterviewQuestions
description: 本文是为记录面试题所创
---

## HashMap 解决hash冲突

### hash冲突产生原因

hash冲突是通过对数据进行再压缩，提高效率的一种办法。由于通过hash函数产生的hash值是有限的，当数据比较多时，经过hash函数处理后仍然有不同的数据对应相同的hash值，这就产生了hash冲突。

### 如何解决hash碰撞

Java 中的 HashMap 采用链表法来解决Hash冲突。原理，即具有相同桶下标的键值对使用一个链表储存。当链表变长时，查找和添加（需要确定 key 是否已经存在）都需要遍历这个链表，速度会变慢。JDK 1.8 后加入了链表转换为红黑树的机制，但是红黑树的转换并不是一个廉价的操作，只有当链表长度大于等于 TREEIFY_THRESHOLD（8） 才会 treeify（treeify方法是TreeNode类的一个实例方法，通过TreeNode对象调用，实现该对象打头的链表转换为树结构），而当HashMap的红黑树的元素小于等于6时重新转化为链表结构。实际上并不是只要链表长度大于 8 就会 treeify。当 table.length（桶的个数）小于 MIN_TREEIFY_CAPACITY（64） 时会优先扩容而不是转换为红黑树。

### 红黑树

**二叉搜索树具有以下特点：**

1. 节点的左孩子的值小于节点本身；
2. 节点的右孩子的值大于节点本身；
3. 左右子树同样为二叉搜索树；

**最终效果是:**

- 节点左子树的所有节点的值都小于节点本身；
- 节点右子树的所有节点的值都大于节点本身；
- 对二叉搜素树的一次中序遍历就是一个递增有序序列

![BinarySearchTree](https://image.aobayu.cn/images/BinarySearchTree.png)**二叉平衡树(AVL)** ：二叉平衡树是在二叉搜素树的基础上加上了限制：任意节点，左右子树的高度差不能超过1。这个约束常常借助左旋和右旋操作实现。

**左旋**：逆时针旋转两个节点，让一个节点被其右子节点取代，而该节点成为右子节点的左子节点

左旋操作步骤如下：

首先断开节点PL与右子节点G的关系，同时将其右子节点的引用指向节点C2；然后断开节点G与左子节点C2的关系，同时将G的左子节点的应用指向节点PL

![L-Spin](https://image.aobayu.cn/images/L-Spin.png)

**右旋**：顺时针旋转两个节点，让一个节点被其左子节点取代，而该节点成为左子节点的右子节点

右旋操作步骤如下：

首先断开节点G与左子节点PL的关系，同时将其左子节点的引用指向节点C2；然后断开节点PL与右子节点C2的关系，同时将PL的右子节点的应用指向节点G

![](https://image.aobayu.cn/images/R-Spin.png)

**红黑树（带有自平衡功能的AVL树）**

红黑树的英文是“Red-Black Tree"，简称R-B Tree。它是一种不严格的平衡二叉查找树。

**红黑树的规则特性：**

1. 节点分为红色或者黑色；
2. 根节点必为黑色；
3. 叶子节点都为黑色，且为null。也就是说，叶子节点不存储数据；
4. 连接红色节点的两个子节点都为黑色（红黑树不会出现相邻的红色节点）；
5. 从任意节点出发，到其每个叶子节点的路径中包含相同数量的黑色节点；

![R-B Tree](https://image.aobayu.cn/images/RBTree.png)

### 为什么 HashMap选择红黑树

因为红黑树的特性让它拥有较高的查询性能的同时，避免维持平衡带来的很大开销。

红黑树相比AVL树，在检索的时候效率其实差不多，都是通过平衡来二分查找。但对于插入删除等操作效率提高很多。红黑树不像AVL树一样追求绝对的平衡，他允许局部很少的不完全平衡，这样对于效率影响不大，但省去了很多没有必要的调平衡操作，AVL树调平衡有时候代价较大，所以效率不如红黑树，在现在很多地方底层都是红黑树。

红黑树的高度只比高度平衡的AVL树的高度（log2n）仅仅大了一倍，在性能上却好很多。

HashMap在里面就是链表加上红黑树的一种结构，这样利用了链表对内存的使用率以及红黑树的高效检索，是一种很happy的数据结构。

AVL树是一种高度平衡的二叉树，所以查找的非常高，但是，有利就有弊，AVL树为了维持这种高度的平衡，就要付出更多代价。每次插入、删除都要做调整，就比较复杂、耗时。所以，对于有频繁的插入、删除操作的数据集合，使用AVL树的代价就有点高了。

红黑树只是做到了近似平衡，并不严格的平衡，所以在维护的成本上，要比AVL树要低。

所以，红黑树的插入、删除、查找各种操作性能都比较稳定。对于工程应用来说，要面对各种异常情况，为了支撑这种工业级的应用，我们更倾向于这种性能稳定的平衡二叉查找树。

## 线程和进程的概念

进程是系统中正在运行的一个程序，程序一旦运行就是进程。

进程可以看成程序执行的一个实例。进程是系统资源分配的独立实体，每个进程都拥有独立的地址空间。一个进程无法访问另一个进程的变量和数据结构，如果想让一个进程访问另一个进程的资源，需要使用进程间通信，比如管道，文件，套接字等。

一个进程可以拥有多个线程，每个线程使用其所属进程的栈空间。线程与进程的一个主要区别是，统一进程内的一个主要区别是，同一进程内的多个线程会共享部分状态，多个线程可以读写同一块内存（一个进程无法直接访问另一进程的内存）。同时，每个线程还拥有自己的寄存器和栈，其他线程可以读写这些栈内存。

线程是进程的一个实体，是进程的一条执行路径。

线程是进程的一个特定执行路径。当一个线程修改了进程的资源，它的兄弟线程可以立即看到这种变化。

### 创造进程的三种方式

| 基于什么创建 | 创建的方式         |
| ------------ | ------------------ |
| Thread类     | 继承`Thread`类     |
| Runnable接口 | 实现`Runnable`接口 |
| callable接口 | 实现`callable`接口 |

**通过Thread类创建**

**步骤**

- 自定义线程类继承`Thread`类
- 重写`run()`方法，编写线程执行体（当成`main()`方法用）
- 创建线程对象，调用`start()`方法启动线程

**通过实现Runnable接口来创建线程**

**创建步骤**

- 创建一个实现了`Runnable`接口的类
- 实现类去实现`Runnable`接口中的抽象方法：`run()`
- 创建实现类的对象
- 将此对象作为参数传递到`Thread`类的构造器中，创建`Thread`类的对象
- 通过`Thread`类的对象调用`start()`
- 这里的`start()`首先启动了当前的线程，然后调用了`Runnable`类型的target的`run()`

### 线程的生命周期

**新建状态（New）：**

当线程对象对创建后，即进入了新建状态，如：Thread t = new MyThread();

**就绪状态（Runnable）：**

当调用线程对象的start()方法（t.start();），线程即进入就绪状态。处于就绪状态的线程，只是说明此线程已经做好了准备，随时等待CPU调度执行，并不是说执行了t.start()此线程立即就会执行；

**运行状态（Running）：**

当CPU开始调度处于就绪状态的线程时，此时线程才得以真正执行，即进入到运行状态。注：就   绪状态是进入到运行状态的唯一入口，也就是说，线程要想进入运行状态执行，首先必须处于就绪状态中；

**阻塞状态（Blocked）：**

处于运行状态中的线程由于某种原因，暂时放弃对CPU的使用权，停止执行，此时进入阻塞状态，直到其进入到就绪状态，才 有机会再次被CPU调用以进入到运行状态。根据阻塞产生的原因不同，阻塞状态又可以分为三种：

**等待阻塞：**运行状态中的线程执行wait()方法，使本线程进入到等待阻塞状态；

**同步阻塞 :** 线程在获取synchronized同步锁失败(因为锁被其它线程所占用)，它会进入同步阻塞状态；

**其他阻塞 :** 通过调用线程的sleep()或join()或发出了I/O请求时，线程会进入到阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入就绪状态。

**死亡状态（Dead）：**

线程执行完了或者因异常退出了run()方法，该线程结束生命周期。