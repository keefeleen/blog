---
title: 用Python来描述一些基本算法其一
date: 2019-04-28 18:17:58
tags:
  - 技术沉淀
---

### 初衷

本身不是学计算机出身，所以说一些基本的概念还是比较薄弱的。很多次被问到一些基础的算法问题，其实脑海中都有印象自己看过，但是有时候就是想不起来。

用的少不是借口(虽然在开发过程中确实用的少)，现在看来，这些基础的算法概念，是对一个人逻辑思维的展现。其实思考这些算法的实现过程，也是一个“重复造轮子的过程”，但是，你写出来了，就是一个能够“造轮子的人”。

### 冒泡算法

其实这个是读书时期接触到的可谓是第一个算法，但是有时候知道概念，嗯，很简单，提笔写或者拿键盘敲起来，就下不了手了。这里，现根据印象，写一下这个方法(写的代码比较难看哈哈)

```
def bsort(target=None):
    if not target:
        target = range(100)
        random.shuffle(target)
    print 'origin data: {}'.format(target)
    # 用于原始结果
    res = copy.deepcopy(target)
    counter = len(target)
    while counter > 0:
        for idx, val in enumerate(target):
            if idx != len(target) - 1 and val > target[idx + 1]:
                # 冒个泡，交换了的话，去到下一层循环时，其实取的就是新的值了
                target[idx] = res[idx +1]
                target[idx + 1] = res[idx]
                res = copy.deepcopy(target)
        counter -= 1
    print 'sorted data: {}'.format(target)
```

写完后，google 一查，上面这东西有点在扯淡的感觉。

这个 counter 是什么鬼，为什么 couter 为 0 就结束排序呢，主要是，本人当时是跟着感觉走的。那么意思是对于任何长度的列表，我外层循环的次数一定要等于列表长度以保证排序完了？

而且，enumerate 使用不当！使用不当！使用不当！于是我这个菜鸟思考了一下，大概想了一下潜在问题，是否正确，会否看看源码。

> enumerate 本质上是个生成器，作用于的是一个可迭代对象，如果你在代码中修改了这个迭代对象，后果是难以预估的，你也不会得到想要的结果

这些思想都很危险啊。

那么回头看看冒泡排序的概念，其关键语句如下：

```
对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
这个工作，从第一个元素开始，到倒数第二个元素为结束的，这样，就能得到最大的元素在列表的结尾了。
如上，然后循环的对子列表进行排序。
```

好的，那么重新梳理下逻辑，那么改下我们的代码，就是如下的结果了

```
def bsort(target=None):
    if not target:
        target = range(10)
    random.shuffle(target)
    print 'origin data: {}'.format(target)
    # 记录现在处理到了哪个位置
    current = len(target)
    while current > 0:
        for idx in range(0, current - 1):
               if target[idx] > target[idx + 1]:
                # 冒个泡，交换了的话，去到下一层循环时，其实取的就是新的值了
                tmp = target[idx]
                target[idx] = target[idx +1]
                target[idx + 1] = tmp
        current -= 1
    print 'sorted data: {}'.format(target)
```

