---
title: lab0-C编程
lang: zh_CN
---

# C-Programming

### lab0的任务pdf与压缩包
[英文版pdf点这里](http://www.cs.cmu.edu/afs/cs/academic/class/15213-f17/www/labs/cprogramminglab.pdf)

[下载压缩包击这里](http://www.cs.cmu.edu/afs/cs/academic/class/15213-f17/www/labs/cprogramminglab-handout.tar)

### 任务概述

下载的压缩文件中包含 queue.h 和 queue.c 2个主要文件，任务目标是实现一个string的单链表，其中queue.h包含如下结构:

```c
/* Linked list element */
typedef struct ELE {
    int value;
    struct ELE *next;
} list_ele_t;

/* Queue structure */
    typedef struct {
    list_ele_t *head; /* Linked list of elements */
} queue_t;
```

需要实现的结构如下:
<img :src="$withBase('/images/lab0-1.png')">

如图所示，将它们组合起来以实现一个队列。队列的顶级表示是类型queue_t的结构。在入门代码中，此结构仅包含一个字段“ head”，但是你将需要添加其他字段。队列内容表示为单链接列表，每个元素由类型为list_ele_t的结构表示，具有字段“值”和“下一个”，分别存储队列值和指向下一个列表元素的指针。你可以向此结构添加其他字段，尽管不必这样做。在我们的C代码中，队列是类型为queue_t *的指针。我们区分两种特殊情况：NULL队列是一种将指针设置为NULL的队列。空队列是指向有效的queue_t结构且头字段设置为NULL的队列。你的代码将需要正确处理这两种情况，以及包含一个或多个元素的队列

### 任务目标
我们的任务是修改queue.h和queue.c，实现以下函数

- q_new：创建一个空队列
- q_free：释放队列使用的所有内存
- q_insert_head：在队列头部插入一个新元素
- q_insert_tail：在队列尾部插入一个新元素
- q_remove_head：删除队头元素
- q_size：计算队列中元素的个数
- q_reverse：逆置队列。这个函数不能申请或者释放任何队列元素

### 补充

可以在这两个文件的注释中找到更多详细信息，包括如何处理无效操作（例如，从空队列或NULL队列中删除）以及函数应具有的副作用和返回值。
以下是有关如何实现这些功能的一些重要说明。 
- 其中两个功能：q_insert_tail和q_size将需要您付出一些努力才能达到所需的性能标准。天真的实现将需要O(n)个步骤来处理具有n个元素的队列。我们要求您的实现在时间O(1)内运行，即所需时间与队列大小无关。你可以通过在queue_t数据结构中包括其他字段并在插入，删除和反转列表元素时正确管理这些值来实现。 
- 必须以不需要分配任何额外内存的方式来实现q_reverse。相反，代码应修改现有列表中的指针。由于我们的测试代码监视对free和malloc的调用的方式，因此需要分配新列表元素的实现将无法通过性能测试。 
- 程序将在具有1,000,000个以上元素的队列上进行测试。你会发现你无法使用递归函数遍历这么长的列表，因为这将需要太多的堆栈空间。

### 测试

你可以通过以下代码来编译你的代码
```shell
linux>make
```

如果没有错误，编译器将生成可执行程序qtest，提供一个命令界面，你可以使用该界面创建，修改和检查队列。可以通过启动此程序并运行help命令找到有关可用命令的文档
```shell
linux> ./qtest
cmd>help
```

以下文件（traces / trace-eg.cmd）说明了示例命令序列:
```shell
# Demonstration of queue testing framework
# Initial queue is NULL.
show
# Create empty queue
new
# Fill it with some values. First at the head
ih 2
ih 1
ih 3
# Now at the tail
it 5
it 1
# Reverse it
reverse
# See how long it is
size
# Delete queue. Goes back to a NULL queue.
free
# Exit program
quit
```

可以通过在批处理模式下运行qtest来查看这些命令的效果：
```shell
linux> ./qtest -f traces/trace-eg.cmd
```

使用入门代码，将看到许多这些操作没有正确实现。跟踪目录包含14个跟踪文件，其名称格式为trace-k-cat.txt，其中k是跟踪号，而cat指定要测试的属性的类别。每个跟踪都由一系列命令组成，类似于上面显示的命令。他们测试程序的正确性，健壮性和性能的不同方面。你可以使用这些自己的跟踪文件，以及与qtest的直接交互来测试和调试程序。

你的程序将使用上述十四条轨迹进行评估。你将为正确执行的每一个功劳（根据跟踪，分别为7或8点），总和最高为100。驱动程序driver.py在跟踪上运行qtest并计算分数。这是将用于通过Autolab计算分数的相同程序。你可以使用以下命令直接调用它：
```shell
linux> ./driver.py

//或者

linux> make test
```

### 写在实现前

以上内容对于已经熟系c与基本数据结构的人来说应该并不是特别困难，花一些时间就行，希望大家能认真自己完成。

### 实现

待上传...