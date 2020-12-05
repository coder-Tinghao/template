---
layout: article
title: Knuth-Shuffle洗牌算法
date: 2020-12-05 19:44:06
tags: 算法
---

# Knuth-Shuffle洗牌算法

该算法来自于一个问题：**设计一个公平的洗牌算法**

这个问题表面上看是一个随机问题，很容易想到的是，每次随机交换两张牌，交换一定次数，且交换次数与牌的数量相关。而这种方法就忽略了这个问题的另一个方面，也是问题的本质：**公平**。就是**对于生成的排列，每一个元素都能独立等概率地出现在每一个位置。**或者反过来，**每一个位置都能独立等概率地放置每个元素。**

抛开时间复杂度来看，只要得到n个元素的全排列再随机选取一个就可以实现公平，但复杂度可以达到O（n！），是不可以被使用的。

下面给出Knuth提出的洗牌算法：

```c++
for(int i=n-1; i>=0; i--){
    swap(arr[i], arr[rand(0, i)])  //rand(0,i)为生成[0,i]之间的速随机整数
}
```

接下来验证Knuth洗牌算法的公平性：用简单的5个数字：1，2，3，4，5进行模拟

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201205201725842.png" alt="image-20201205201725842" style="zoom:50%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201205201840375.png" alt="image-20201205201840375" style="zoom:50%;" />

从5开始，随机和包括5在内的数字进行对换，假设这一步随机到2。因为每个数被随机到的可能性为1/5，所以任意元素出现在最后一个位置的概率均为1/5。



<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201205202037477.png" alt="image-20201205202037477" style="zoom:50%;" />

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201205202100703.png" alt="image-20201205202100703" style="zoom:50%;" />

接下来，对第四个位置重复上一步的过程，只看这个四个元素，任意元素出现在该位置的概率为1/4，算入第一步选取该四个数的4/5，即从总体上看任意元素出现在该位置的概率为1/4 * 4/5 = 1/5，和最后一个位置的概率相同，同理可以完成该算法的公平性验证！

**其实这个过程也可以理解为一个从袋子里随机取出球不放回的过程，但本算法空间上在原地完成，是工程实现前提下的算法思想。**





