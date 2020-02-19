# DSA Python


## 1. 图灵机 计算模型 Turling Machine
> * 无限长的纸带： 每个格子 记录1个符号
> * 来回移动得读写头： 读写和擦除
> * 状态寄存器： 记录有限状态中的1个状态
> * 控制规则（5个）： 状态；字符；改成什么字符 如何移动； 改变成什么状态
eg：< S0,a,B,Si,R >
eg：Visual Turling

## 2. 算法和计算复杂性
### 2.1 计算复杂性
> * 计算时间
> * 存储空间
> * 可行性

## 3. 数据抽象 ADT
> * 只有功能 描述 和功能实现的接口（不用管功能是如何实现的）
> * 封装 可以把处理数据的细节隐藏起来
> * 采用程序设计语言的控制结构和基本数据类型来实现ADT所提供的逻辑接口 属于ADT得物理层次
> * ADT实现逻辑（like复杂的数据模型 可以保持稳定）与物理层次（可以持续改进）的分离

## 4.算法分析
**算法->底层实现得研究**
> * 存储空间或内存
> * 执行时间
time模块

### 4.1 大O记号
**Upperbound （所有的上限中，最小的那个上限，用得最多）**
数量级函数：T（n）中增加速度最快的部分 O（n）（主导的部分）
eg：5n^2+7n=1005 ->O(n^2)
**渐进分析（Asymptotic Analysis）**

> * constant function 常数复杂度 eg：2^2000  O(1)
顺序执行（不含循环），包含循环但是转向的目标必然不可能达到的，隐式的循环（递归）
> * 对数 logn （复杂度无限接近于常数）O(logn)
常底数无所谓，常数次幂无所谓，对数多项式
> * 多项式 一般的：O(n^k)
**低次项都是可以忽略的,仅保留最高级**
线性 O（n）
> * 指数复杂度 O(a^n)
存在c>1  n<sup>c</sup> = O(2<sup>n</sup>)
eg：n<sup>1000</sup> = O(1.00000001<sup>n</sup>)= O(2<sup>n</sup>) upperbound
1.00000001<sup>n</sup> = omega(n<sup>1000</sup>) lowerbound
计算成本增长极快，一般都是不可忍受的
eg：子集的划分：NP——complete：就目前的计算模型而言，不存在可在多项式时间内回答此问题的算法，就此意义而言，直觉算法已属最优
**指数幂到多项式一般是分水岭 tracable -> intractable**
<center>**复杂度综述：
O(2<sup>n</sup>)>O(n<sup>3</sup>)>O(n<sup>2</sup>)>O(nlogn)>O(n)>O(logn)>O(1)**</center>

### 4.2 大Omega记号
**所有下限中最大的下限**
### 4.3 大Theta记号
**上下限相等的情况下，可以用大Theta**
### 4.4 “变为词”判断问题
包含相同的字母但是顺序不一样（长度相等）
1. 把第一个词中的逐个在第二个里面检查，打勾 O(n^2)
2. 排序比较，按照字母顺序排序，比较
  （主导的是排序算法的耗时 O(nlogn)）
3. 暴力法：穷尽所有可能组合 s1全排列 与s2比较
4. 计数比较：每个字母出现的次数（为每个字母设置计数器），对比 O(n)
**时间和空间得取舍和权衡**
###4.5 Python数据类型的性能
主要为列表list和字典dict （均为可变的）
####4.5.1 list
80/20准则： 80%的功能只有20%使用率

>* a[i],a[i]=v    O(1)
>* list.append  O(1)
list=list+[v]   O(n+k)
>* pop() O(1)
删除最后一位,不随list大小变化
pop(i)  O(n)
从中部移除的时候,要把后面的元素都要往前移动,所以是O(n)。这样按照索引取值和赋值就是O(1)，随list大小变化
>* reverse O(n)
……

#### 4.5.2 dict
>* 取值 赋值 d[k]=v   O(1)
判断是否存在  O(1)

https://wiki.python.org/moin/TimeComplexity

## 5. 线性结构 Linear Structure
>* 唯一个前驱（第一个没有），唯一个后继（最后一个没有），数据相之间存在先后的次序
>* 前后 左右 上底
**关键的是添加减少数据项的方式，不同的的方式构成了以下四种强大的结构**

### 5.1 Stack 栈
>* 数据想的加入和一处都尽发生在同一端（栈顶 top），另一端叫做栈底（base）。like：盘子，书堆
>* 后进先出 LIFO，时间越短离top越近，越长离base越近。反转次序
>* 调用接口就可以实现

将ADT Stack实现为Python的一个Class，将ADT Stack的操作实现为Class的方法
#### 5.1.1 **基本操作：**
1. Stack（）:创建一个空栈，不包含任何数据项
2. push（item）：将item加入栈顶，无返回值
3. pop（）：将栈顶数据项移除，并返回所移除的值，栈被修改
4. peek（）：“窥视”栈顶数据项，返回栈顶的数据项但不移除，栈不被修改
5. isEmpty（）：返回栈是否为空栈
6. size（）：返回栈中有多少个数据项
```python
#尾端作为栈顶
class Stack:
    #初始化
    def __init__(self):
        self.items = []
    #判断是否为空集
    def isEmpty(self):
        return self.items == []
    #添加新元素到栈顶
    def push(self,item):
        self.items.append(item)
    #删除栈顶元素
    def pop(self):
        return self.items.pop()
    #窥探栈顶元素
    def peek(self):
        return self.items[-1]
    #查看栈的大小
    def size(self):
        return len(self.items)
    
myStack = Stack()
myStack.peek()

```
```python
#另一种实现
#将list首段设为栈顶和将list末端设为栈顶。栈顶首段的版本（左边）push/pop的复杂度为O(n)，而栈顶尾端的实现（右边），其push/pop的复杂度为O(1)。就是前面讲的insert()，insert(i)区别
```
#### 5.1.2 应用
dfs stack 深度优先搜索 

##### 1. 简单括号匹配

**平衡原则** ：左右对称
```python
# -*- coding: UTF-8 -*-
from pythonds.basic.stack import Stack

def judge(st):
    s = Stack()
    j = True # 相当于一个标志符
    index = 0
    while index < len(st) and j:
        sym = st[index]
        if sym == '(':
            s.push(sym)
        else:
            if s.isEmpty():
                j = False
            else:
                s.pop()
        index += 1
    if j and s.isEmpty(): #一定要判断是否为j是否为真,不然有可能是14排匹配失败才跳出循环的情况
        return True
    else:
        return False

print(judge('(())'))
```

##### 2. 通用括号的匹配

eg：([)],((()])),[{()] 都算是不匹配
```python
# -*- coding: UTF-8 -*-
from pythonds.basic.stack import Stack

def judge(st):
    s = Stack()
    j = True # 相当于一个标志符
    index = 0
    while index < len(st) and j:
        sym = st[index]
        if sym in "{[(":
            s.push(sym)
        else:
            if s.isEmpty():
                j = False
            else:
                top = s.pop()
                if not matches(top, sym): #判断是否是对应的做括号
                    balanced = False
        index += 1
    if j and s.isEmpty(): #一定要判断是否为j是否为真,不然有可能是14排匹配失败才跳出循环的情况
        return True
    else:
        return False

def matches(open, close):
    opens = "([{"
    closers = ")]}"
    return opens.index(open) == closers.index(close) #位置是一样的就成对 eg：'(' , ')'都位于opens 和 closers里面的0位置，减少了if else的使用

print(judge('(())'))
```

**栈广泛应用于层次结构化文档校验和操作**

##### 3.进制转换
```python
# -*- coding: UTF-8 -*-
from pythonds.basic.stack import Stack

def trs(decNum,base):

    digits="0123456789ABCDEF"

    s = Stack()
    
    while decNum > 0:
        rem = decNum % base
        s.push(rem)
        decNum = decNum // base

    ans=""
    while not s.isEmpty():
        ans = ans + digits[s.pop()] #ans是一个字符串，字符串不能和int想加减，所以先将栈里的int转换成str
    return ans

print(trs(56,16))
```
##### 4. 表达式转换

>* 全括号中缀表达式
>* 前缀、后缀表示法：与数字离得最近的操作符优先计算
eg：(A+B)*(C+D) = AB+CD+*(后缀)=*+AB+CD(前缀)
A+B+C+D=AB+C+D+(前缀)=+++ABCD(后缀)
>* 中缀到前缀：运算符都按顺序移到左括号处；中缀到后缀：运算符都按顺序移到右括号处
>* 后缀表达中：数字顺序相同，但是运算符顺序相反。用栈来存储还未处理的操作符（最近存进去的），当遇到一个新的操作符，就需要跟栈顶的操作符比较一下优先级，再进行处理
```python
# -*- coding: UTF-8 -*-
from pythonds.basic.stack import Stack

# 中缀表达式转为后缀表达式
def infixToPostfix(infixexpr):
    prec = {}  # 定义一个字典，保存优先级
    prec["*"] = 3
    prec["/"] = 3
    prec["+"] = 2
    prec["-"] = 2
    prec["("] = 1
    opStack = Stack()  # 栈是用来存括号和运算符的
    postfixList = []  # 保存要输出的后缀表达式
    tokenList = infixexpr.split()  # 把中缀表达式转换成列表

    for token in tokenList:
        if token in "ABCDEFGHIJKLMNOPQRSTUVWXYZ" or token in "0123456789":
            postfixList.append(token)
        elif token == '(':  # 如果是左括号，就压入栈
            opStack.push(token)
        elif token == ')':  # 遇到右括号，循环判断栈顶元素是否为（，如果不是（，就把栈顶都加到后缀列表中
            topToken = opStack.pop()#提出栈顶
            while topToken != '(':
                postfixList.append(topToken)
                topToken = opStack.pop()
            print(opStack.isEmpty())  # True False False
        else:  # 如果是运算符，当栈不为空并且栈顶元素的等级比token的等级高时，栈顶元素加入到后缀列表中
            while (not opStack.isEmpty()) and (prec[opStack.peek()] >= prec[token]):
                postfixList.append(opStack.pop())
            opStack.push(token)  # 把token压入栈

    while not opStack.isEmpty():  # 把opStack中剩下的操作符依次弹出，加到后缀列表后面
        postfixList.append(opStack.pop())
    return ''.join(postfixList)


print(infixToPostfix("A * B + C * D"))
print(infixToPostfix("( A + B ) * C - ( D - E ) * ( F + G )"))
```

##### 5. 后缀表达式求值
>* 先暂存操作数（弹出的时候是先弹出右操作数）；操作符只作用于最近的操作数
>* split函数把单词转换成列表
```python
# -*- coding: UTF-8 -*-
from pythonds.basic.stack import Stack

def Eval(Exp):
    opStack = Stack()
    tokenList = Exp.split()
    for val in tokenList:
        if val in '0123456789':
            opStack.push(int(val)) # 字符串转换为整形
        else:
            num2 = opStack.pop() # 第二个操作数
            num1 = opStack.pop() # 第一个操作数
            result = doCal(num1, val, num2)
            opStack.push(result) # 计算结果要压回栈
    return opStack.pop()

def doCal(num1,opt, num2):
    if opt == '+':
        result = num1 + num2
    elif opt == '-':
        result = num1 - num2
    elif opt == '/':
        result = num1 / num2
    else:
        result = num1 * num2
    return result
```

### 5.2 Queue 队列
（bfs queue 广度优先）
#### 5.2.1 基本操作
>* 新数据项的添加总在一端（rear尾端），移除总在另一端（front首端）
>* 先进先出 FIFO，先到先服务
>* 不允许插在中间 or 从中间移除
>* 函数：
1. Queue():创建一个空队列对象，返回对象
**队列初始化（创建一个队列）**
2. enqueue(item):item添到队尾，无返回  
**入队（把数据添加到队尾）**
一般右边对首，左边对尾。
3. dequeue():对首移除数据项，返回队首数据项，队列被修改 
**出队（从队首取出一个数据）**
4. inEmpty():测试是否会空队列，返回bool
5. size():返回数据项个数
**获取队列的长度**
6. pop(): 移除最后一位
销毁一个队列（把整个队列的数据从内存中删除）
#### 5.2.2 应用
##### 1. 热土豆应用（约瑟夫）
```python
from pythonds.basic.queue import Queue

def hotPotato(namelist, num):
    simqueue = Queue()
    for name in namelist:
        simqueue.enqueue(name)
    while simqueue.size() > 1:
        for i in range(1, num):
            simqueue.enqueue(simqueue.dequeue()) #把队首排出立马又从队尾入队完成一次土豆的传递
        simqueue.dequeue()#传递了num次后，把队首的人移除，不再入队，知道队列中剩余1人
    return simqueue.dequeue()#最后剩下的人
print(hotPotato(['Bill', 'Jack', 'Andy', 'Jane', 'Kent'],7))
```
##### 2. 打印任务
多人共享一台打印机 先到先打印
模拟仿真分析性能

>* 对象：打印机，打印队列，打印任务
1. 打印机属性：速度，是否busy
2. 打印队列属性：fifo
3. 打印任务属性：提交时间，打印页数

>* 主程序：打印。（时间按照秒的单位流逝）
1. 生成打印作业，加入队列
2. 如果闲打印，记录其**等待时间**
3. 如果忙，按照打印速度进行1s打印
4. 打印完成，进入空闲
**作业的打印时间：页数/速度**

>* 时间用尽，统计平均等待时间
```python
from pythonds.basic.queue import Queue
import random

class Printer: #打印机对象

    def __init__(self,ppm): #初始化属性
        self.pagerate = ppm # 打印速度
        self.currentTask = None #当前打印任务，初始化的时候还是空闲
        self.timeRemaining = 0 #当前正在打印的任务还有多少时间（s）打印完成

    def tick(self): #打印方法，如果有作业正在打印，timeremaining - 1
        if self.currentTask != None: #如果有作业正在打印
            self.timeRemaining -= 1 #剩下时间-1
            if self.timeRemaining <= 0:#打印完成
                self.currentTask = None#进入空闲

    def busy(self): #判断打印机状态是否busy
        if self.currentTask != None:
            return True
        else:
            return False

    def startNew(self,newtask):#打印新任务
        self.currentTask = newtask
        self.timeRemaining = newtask.getpages() * 60 / self.pagerate


class Task: #打印类
    def __init__(self,time):
        self.timestamp = time  #生成时间戳
        self.pages = random.randrange(1,21) #页数是随机的且概率相同。所以随机生成1-20页/task

    def getStamp(self):
        return self.timestamp

    def getPages(self):
        return self.pages

    def waitTime(self, currentTime): #当前时间 - 生成时间
        return currentTime - self.timestamp


def newPrintTask(): #bool函数 返回True/False。判断当前有无新task生成
    num = random.randrange(1,181) #1s范围内，是否生成新的打印任务. [20个tasks/h ->20/3600(s)=1/180,180s生成一个task，概率是1/180]
    if num == 180: # 可以是任何一个数 1-180以内都可以，概率都是1/180
        return True
    else:
        return False


def simulation (numSeconds, pagesPerMinite): #模拟时间，打印机模式 5 pages/s or 10 pages/s
    labprinter = Printer(pagesPerMinite) #生成printer打印对象
    printQueue = Queue() # 准备打印队列
    waitingtime = []
    
    for currentSecond in range(numSeconds):
        #如果有新任务生成
        if newPrintTask():
            task = Task(currentSecond)
            printQueue.enqueue(task) # 把打印任务排到队列里面去
        #打印过程
        if(not labprinter.busy()) and (not printQueue.isEmpty()): #如果不忙且队列里有排队的task
            nexttask = printQueue.dequeue() # 任务出队开始打印
            waitingtime.append(nexttask.waitTime(currentSecond)) # 把它等待的时间放到waitTime列表里去
            labprinter.startNew(nexttask)
        
        labprinter.tick()
        
    averageWait = sum(waitingtime) / len(waitingtime)
    print("Average waiting time is : %6.2f secs %3d tasks remaining"%(averageWait,printQueue.size()))
```
### 5.3 Deque 双端队列
#### 5.3.1 基本操作：
>* 两端都可以看作是“首”，“尾”；数据项可以从两端加入或移出（相当于集合了栈和队列的能力，但是不是具有内在的LIFO/FIFO）
>* 函数：（**左边是队尾，右边是队首**）
1. Deque():创建空双端序列
2. addFront(item):item加入队首 O(1)
3. addRear(item):item加入队尾 O(n)
4. removeFront():从队首移除，返回移除数据项 O(1)
5. removeRear():从队尾移除，返回移除数据项 O(n)
6. isEmpty():是否为空
7. size():返回包含数据项个数
#### 5.3.2 应用
##### 1. 回文词判断
>* 将判断的词加入双端队列
>* 从两端同时移除字符判定是否相同，直到队列中剩下0 or 1个字符
```python
from pythonds.basic.deque import Deque

def palchecker(nums):
    deq = Deque()
    for num in nums:
        deq.addRear(num)
    while deq.size() > 1 and True:
        first = deq.removeRear()
        last = deq.removeFront()
        if first == last:
            return True
        else:
            return False
print(palchecker('abcdefedcb'))
```
### 5.4 List 列表
#### 5.4.1 单链表基本操作
>* 一种数据项按照相对位置存放的数据集
>* 函数：
1. List():创建空列表
2. add(item):添加一个数据项（原本不存在于列表中）
3. remove(item):移除item，列表被修改
4. search(item):在列表中查找item，返回bool类型值 True/False
5. isEmpty():返回列表是否为空
6. size():包含了多少数据项
7. append(item)
8. index(item)
9. insert(pos,item)
10. pop():删除末尾  O(1)
11. pop(pos)：删除指定位置 O(n)
>* 采用链表实现无序表
1. 地址不一定是连续存放 ——> 数据项之间建立链接指向，可以保持相对位置
2. 队首，队尾
3. 基本元素Node节点：数据项 + 引用信息 next（为none的时候没有下一个了）
```python
class Node:
    def __init__(self, initdata):
        self.data = initdata
        self.next = None
        
    def getData(self): #当前数据项
        return self.data
    
    def getNext(self): #当前next
        return self.next
    
    def setData(self,newdata): #设置新的data
        self.data = newdata
        
    def setNext(self,newnext): #设置新的next
        self.next = newnext
```
>* 链表的第一个和最后一个节点最重要，所以无需表必须要有对第一个节点的引用信息
```python
class UnorderedList:
    def __init__(self):
        self.head = None #空表
```
无序表的head始终指向第一个节点

#### 5.4.2 单链表无序表的实现
>* add  O(1)
最先加的在最后
```python
def add(self,item):
    temp = Node(item)  #为item生成新的节点
    temp.setNext(self.head)  #把它的next设置为head（原本的第一个元素）
    self.head = temp  #把表头指向新增加的item
    
    #后面两个语句的次序特别重要，如果先更换head，整个链表就丢失了
```
>* size (O(n))
```python
def size(self):
    current = self.head 
    count = 0
    while current != None:
        count += 1
        current = current.getNext() #当前节点设置成当前节点的下一个
    return count
```
>* search (O(n))
```python
def search(self, item):
    current = self.head
    found = False
    while current != None and not found:
        if current.getData() == item:
            found = True
        else:
            current = current.getNext()
    return found
```
>* remove
和search 相似，先找到后删除。需要维护当前的前一个节点。
```python
def remove(self,item):
    current = self.head
    previous = None
    found = False
    while not found:
        if current.getData()== item:
            found = True
        else:
            previoous = current # 把当前current给previous
            current = current.geNext() #current到下一个
    if previous == None: # 第一个元素就是要删除的元素
        self.head = current.getNext() #直接把head改成current的下一个（原本的第二个）
    else:
        previoous.setNext(current.getNext) #否则就要把previous的next改成current的next
    
```
#### 5.4.3 双链表
既有Next又有Previous
#### 5.4.4 有序表
>* 数据项按照某种可比性质排列
>* 基本操作：
1. OrderList():创建空有序列表
2. add(item):添加一个数据项（原本不存在于列表中）
3. remove(item):移除item，列表被修改
4. search(item):在列表中查找item，返回bool类型值 True/False O(n)
5. isEmpty():返回列表是否为空
6. size():包含了多少数据项  O(n)
7. append(item)
8. index(item)
9. insert(pos,item)
10. pop():删除末尾  O(1)
11. pop(pos)：删除指定位置 O(n)
>* 实现
##### 1. head
```python
class UnorderedList:
    def __init__(self):
        self.head = None #空表
```
##### 2. isEmpty/size/remove 和无序表一样
##### 3. search
```python

def search(self, item):
    current = self.head
    found = False
    stop = False #标志变量
    while current != None and not found and not stop: #当current data>我们要找的item的时候stop
        if current.getData() == item:
            found = True
        else:
            if current.getData() > item:
                stop = True
            else:
                current = current.getNext()
    return found
```
##### 4.add
```python
def add(self,item):
    current = self.head
    previous = None
    stop = False
    while current != None and not stop:
        if current.getData() > item: #发现插入位置
            stop = True
        else:
            previoous = current # 把当前current给previous
            current = current.getNext() #current到下一个
    temp = Node(item)
    if previous == None: # 插入在表头
        temp.setNext(self.head)
        self.head = temp
    else: #插入在表中
        temp.setNext(current)
        previoous.setNext(current.getNext) #否则就要把previous的next改成current的next
```
#### 5.4.5 链表算法分析
和python内置列表（顺序存储）的时间复杂度不同
### 5.5 线性结构的小结

## 6. 递归 Recursion
### 6.1 基本操作
>* 分解为小的非常简单的相同方法，然后在算法流程中调用自身

eg: 数列和 = 首个数 + 余下数列
```python
def listsum(numlist):
    if len(numlist) == 1:
        return numlist[0]
    else:
        return numlist[0] + listsum(numlist[1:])
```
>* 三定律：
1. 有一个基本的结束条件：最小规模问题的直接解决
2. 必须能一直减小问题规模直至最小规模
3. 调用自身来解决规模减小的问题


### 6.2 应用
#### 1. 任意进制转换
```python
def toStr(n,base):
    convertString = "0123456789ABCDEF"
    if n < base:
        return convertString[n]
    else:
        return toStr(n // base, base) + convertString[n % base] #哪里调用就返回哪里
```
#### 2. 汉诺塔：（移动盘子，大盘子不能在小盘子上面）
>* n个盘子，上面n-1个盘子移到中间柱子
>* n-1个盘子，上面n-2个盘子移到中间柱子
>* 最小规模问题：1个盘片（结束条件）
```python
def move(n,a,b,c):
    if n == 1:
        print(a,"--->",c)
    else:
        move(n-1,a,c,b)
        print(a,"--->",c)
        move(n-1,b,a,c)

move(3,"A","B","C")

```
#### 3. 探索迷宫
>* 整个迷宫看成方格，判断每个方格是墙壁还是路 ——> 看成矩阵，墙壁‘+’，投放点S
```python
import turtle

# 迷宫类
class Maze(object):
	# 读取迷宫数据，初始化迷宫内部，并找到海龟初始位置。
	def __init__(self, mazeFileName):
		rowsInMaze = 0							#初始化迷宫行数
		columnsInMaze = 0 						#初始化迷宫列数
		self.mazelist = []						#初始化迷宫列表
		mazeFile = open(mazeFileName, 'r')		#读取迷宫文件
		for line in mazeFile:					#按行读取
			rowList = [] 						#初始化行列表
			col = 0 							#初始化列
			# for ch in line[:-1]:				#这样会丢失最后一列
			for ch in line:						#按列读取
				rowList.append(ch)				#添加到行列表
				if ch == 'S':					#S为乌龟初始位置，即迷宫起点
					self.startRow = rowsInMaze	#乌龟初始行
					self.startCol = col 		#乌龟初始列
				col = col + 1 					#下一列
			rowsInMaze = rowsInMaze + 1 		#下一行
			self.mazelist.append(rowList)		#行列表添加到迷宫列表
			columnsInMaze = len(rowList) 		#获取迷宫总列数
		self.rowsInMaze = rowsInMaze 			#设置迷宫总行数
		self.columnsInMaze = columnsInMaze		#设置迷宫总列数
		self.xTranslate = -columnsInMaze/2 		#设置迷宫左上角的初始x坐标
		self.yTranslate = rowsInMaze/2 			#设置迷宫左上角的初始y坐标
		self.t = turtle.Turtle()				#创建一个海龟对象
		self.t.shape('turtle')					#给当前指示点设置样式(类似鼠标箭头)，海龟形状为参数指定的形状名，指定的形状名应存在于TurtleScreen的shape字典中。多边形的形状初始时有以下几种："arrow", "turtle", "circle", "square", "triangle", "classic"。
		self.wn = turtle.Screen()				#创建一个能在里面作图的窗口
		self.wn.setworldcoordinates(-columnsInMaze/2, -rowsInMaze/2, columnsInMaze/2, rowsInMaze/2)			#设置世界坐标系，原点在迷宫正中心。参数依次为画布左下角x轴坐标、左下角y轴坐标、右上角x轴坐标、右上角y轴坐标

	# 在屏幕上绘制迷宫
	def drawMaze(self):
		self.t.speed(20)						#绘图速度
		for y in range(self.rowsInMaze):		#按单元格依次循环迷宫
			for x in range(self.columnsInMaze):
				if self.mazelist[y][x] == OBSTACLE:	#如果迷宫列表的该位置为障碍物，则画方块
					self.drawCenteredBox(x + self.xTranslate, -y + self.yTranslate, 'orange')

	# 画方块
	def drawCenteredBox(self, x, y, color):
		self.t.up()								#画笔抬起
		self.t.goto(x - 0.5, y - 0.5)			#前往参数位置，此处0.5偏移量的作用是使乌龟的探索路线在单元格的正中心位置
		self.t.color(color)						#方块边框为橙色
		self.t.fillcolor('green')				#方块内填充绿色
		self.t.setheading(90)					#设置海龟的朝向，标准模式：0 - 东，90 - 北，180 - 西，270 - 南。logo模式：0 - 北，90 - 东，180 - 南，270 - 西。
		self.t.down()							#画笔落下
		self.t.begin_fill()						#开始填充
		for i in range(4):						#画方块边框
			self.t.forward(1)					#前进1个单位
			self.t.right(90)					#右转90度
		self.t.end_fill()						#结束填充

	# 移动海龟
	def moveTurtle(self, x, y):
		self.t.up()								#画笔抬起
		self.t.setheading(self.t.towards(x + self.xTranslate, -y + self.yTranslate))	#setheading()设置海龟朝向，towards()从海龟位置到由(x, y)，矢量或另一海龟位置连线的夹角。此数值依赖于海龟初始朝向，由"standard"、"world"或"logo" 模式设置所决定。
		self.t.goto(x + self.xTranslate, -y + self.yTranslate)	#前往目标位置

	# 画路径圆点
	def dropBreadcrumb(self, color):
		self.t.dot(color)						#dot(size=None, color)画路径圆点

	# 用以更新迷宫内的状态及在窗口中改变海龟位置，行列参数为乌龟的初始坐标。
	def updatePosition(self, row, col, val):
		self.mazelist[row][col] = val 			#设置该标记状态为当前单元格的值
		self.moveTurtle(col, row)				#移动海龟
		if val == PART_OF_PATH: 				#其中一条成功路径的圆点的颜色
			color = 'green'
		elif val == TRIED:						#尝试用的圆点的颜色
			color = 'black'
		elif val == DEAD_END:					#死胡同用的圆点的颜色
			color = 'red'
		self.dropBreadcrumb(color)				#画路径圆点并上色

	# 用以判断当前位置是否为出口。
	def isExit(self, row, col):
		return (row == 0 or row == self.rowsInMaze - 1 or col == 0 or col == self.columnsInMaze - 1)								#根据海龟位置是否在迷宫的4个边线位置判断

	# 返回键对应的值，影响searchFrom()中maze[startRow][startColumn]值的获取
	def __getitem__(self, key):
		return self.mazelist[key]

# 探索迷宫，注意此函数包括三个参数：一个迷宫对象、起始行、起始列。
def searchFrom(maze, startRow, startColumn):
	# 从初始位置开始尝试四个方向，直到找到出路。
	# 1. 遇到障碍，失败
	if maze[startRow][startColumn] == OBSTACLE:
		return False
	# 2. 发现已经探索过的路径或死胡同
	if maze[startRow][startColumn] == TRIED or maze[startRow][startColumn]== DEAD_END:
		return False
	# 3. 发现出口
	if maze.isExit(startRow, startColumn):
		maze.updatePosition(startRow, startColumn, PART_OF_PATH) #显示出口位置，注释则不显示此点
		return True
	maze.updatePosition(startRow, startColumn, TRIED) #更新迷宫状态、设置海龟初始位置并开始尝试
	# 4. 依次尝试每个方向（北南西东）
	found = searchFrom(maze, startRow - 1, startColumn) or \
            searchFrom(maze, startRow + 1, startColumn) or \
            searchFrom(maze, startRow, startColumn - 1) or \
            searchFrom(maze, startRow, startColumn + 1)
	if found:													#找到出口
		maze.updatePosition(startRow, startColumn, PART_OF_PATH)#返回其中一条正确路径
	else:														#4个方向均是死胡同
		maze.updatePosition(startRow, startColumn, DEAD_END)
	return found

if __name__ == '__main__':
	PART_OF_PATH = 'O'			#部分路径
	TRIED = '.'					#尝试
	OBSTACLE = '+'				#障碍
	DEAD_END = '-'				#死胡同
	myMaze = Maze('maze.txt')	#实例化迷宫类，maze文件是使用“+”字符作为墙壁围出空心正方形空间，并用字母“S”来表示起始位置的迷宫文本文件。
	myMaze.drawMaze()			#在屏幕上绘制迷宫。
	searchFrom(myMaze, myMaze.startRow, myMaze.startCol)	#探索迷宫
```
>* 防止死循环：记录走过的路径
结束条件：
1. 碰到墙壁 False
2. 碰到面包屑 False
3. 出口 True
4. 四个方向都探索失败 False

#### 4. 分而治之
>* 大问题划分为小问题，汇总的得到原问题的解
>* 应用：排序、查找、遍历、表达式求值

#### 5. 优化问题和贪心算法
>* 找零最少个数的硬币问题 ——> 贪心策略
用尽量大的面值最多个数 ——> 次大的 ——> 最小面值的
**每次都试图解决问题的尽量大的部分**： 以最多数量的最大面值来迅速减少找零面值
（严重依赖于硬币的面值来决定，有特殊面值的话就会失效）

#### 6.找零兑换的递归解法
不依赖于面值，都可以找到
>* 首先确定截止条件
找零值恰好等于某种硬币的面值
>* 减小规模：
对每种面值都尝试一次：-1——>求最少数量；-5——>求最少数量；-10——>求最少数量；-25——>求最少数量
再求mini——>最优解

```python
def recMC(coinValueList, change): #硬币体系，找零数
	minCoins = change
	if change in coinValueList: #找零=面值
		return 1
	for i in [c for c in coinValueList if c <= change]: #只在面值比找零数小的硬币里找，[]是生成除去比找零数大的面值的coinValueList
		numCoins = 1 + recMC(coinValueList , change - i)
		if numCoins < minCoins:
			minCoins = numCoins
	return minCoins

print(recMC([1,5,10,25], 63))
 #速度极慢，重复计算
```
#### 7.找零兑换的备忘录计数优化算法
```python
 # 优化： 消除重复计算，用一个表把计算过的中间结果保存起来，在计算之前查表看看是否已经计算过。这个算法的中间结果就是部分找零的最优解
额外空间占用（成本：KnownResultsLists），改善时间复杂度
 def recMC(coinValueList, change, knownResults): #硬币体系，找零数
	minCoins = change
	if change in coinValueList: #找零=面值
		knownResults[change] = 1 #记录最优解
		return 1
	elif knownResults[change] > 0: # 查找最优解
		return knownResults[change] # 因为knownresults初始化全部为0，如果不为0则说明记录过最优解，查表成功

	for i in [c for c in coinValueList if c <= change]: #只在面值比找零数小的硬币里找，[]是生成除去比找零数大的面值的coinValueList
		numCoins = 1 + recMC(coinValueList , change - i,knownResults)
		if numCoins < minCoins:
			minCoins = numCoins
			knownResults[change] = minCoins #记录最优解

	return minCoins

print(recMC([1,5,10,25], 63,[0]*64))

```
#### 8. 找零兑换的动态规划算法
>* 大问题的优化解一定是小问题的最优解推出来的
>* 从最简单的“1分钱找零”的最优解开始，逐步递加上去直到我们需要的找零钱数
>* 上一个找零数的最优解+任意面值=下一值的最优解
>* **最主要的思想是从最简单的情况开始到达所需找零的循环；其每一步都是依靠以前的最优解来得到本不走的最优解，直到得到答案**
```python
def dpMakeChange(coinValueList, change, minCoins): #硬币体系，找零数，最优硬币数量
	#从change = 1 开始逐个计算最少硬币数
	for cents in range(1, change + 1): #左闭右开
		#1. 初始化一个最大值
		coinCount = cents
		#2. 减去每个硬币，向后查找最优解，同时记录最优解（最少硬币数）
		for j in [c for c in coinValueList if c <= cents]: # j是每一种硬币面值
			if minCoins[cents - j] + 1 < coinCount:
				coinCount = minCoins[cents - j] + 1
		#3. 得到当前最优解，并记录
		minCoins[cents] = coinCount
	#返回最后一个结果
	return minCoins[change]

print(dpMakeChange([1,5,10,21,25], 63, [0] * 64))
```
>* 扩展：记录最优解的硬币组合
生成最优解列表时跟踪记录所选择的硬币
```python
def dpMakeChange(coinValueList, change, minCoins,coinsUsed): #硬币体系，找零数，最优解数组，具体硬币面值
	for cents in range(1, change + 1):
		#初始化一个最大值
		coinCount = cents
		newCoin = 1
		for j in [c for c in coinValueList if c <= cents]:
			if minCoins[cents - j] + 1 < coinCount:
				coinCount = minCoins[cents - j] + 1
				newCoin = j #对应最优解所减的那个面值
		minCoins[cents] = coinCount
		coinsUsed[cents] = newCoin #记录本步骤+的一个硬币面值
	return minCoins[change]

def printCoins(CoinsUsed, change):
	coin = change
	while coin > 0:
		thisCoin = CoinsUsed[coin]
		print(thisCoin)
		coin = coin - thisCoin
amt = 63
clist = [1,5,10,21,25]
coinsUsed = [0] * (amt+1)
coinsCount = [0] * (amt+1)
print('Making changes for ', amt, "requires ",end = '')
print(dpMakeChange(clist, amt, coinsCount, coinsUsed),'coins')
print('They are:')
printCoins(coinsUsed,amt)
print('The used list is as follows:')
print(coinsUsed)
```

### 6.3 递归调用的实现
>* 现场数据压入系统调用栈，用栈帧恢复现场（调用次序和返回次序是相反的）
>* 深度限制：
1. 是否忘记设置基本结束条件，导致无限递归
2. 或者向基本结束条件演进太慢
3. getrecursionlimit()可以得到或者设置最大递归深度
###6.4 递归可视化
>* turtle 海龟作图
```python
import turtle

t = turtle.Turtle()

t.pencolor('red')
t.pensize(3)

def drawSpiral(t, lineLen):
    if lineLen > 0:
        t.forward(lineLen)
        t.right(90)
        drawSpiral(t,lineLen - 5)
drawSpiral(t,100)
turtle.done()
```
>* 分行树：自相似(部分和整体相似)
```python
import turtle

def tree(branch_len):
    if branch_len > 5: #树干太短，递归结束条件
        t.forward(branch_len)
        t.right(20)
        tree(branch_len - 15) # -15: 规模缩小
        t.left(40) #向左回40度
        tree(branch_len - 15)
        t.right(20) #回正
        t.backward(branch_len) #必须退回到原地再转向

t = turtle.Turtle()
t.left(90)
t.penup()
t.pencolor('green')
t.pensize(3)
tree(80)
t.hideturtle()
turtle.done()
```
>* 谢尔宾斯基三角形
面积趋近于0，周长趋近于无穷 ——> 介于一维和二维之间的构造
```python
import turtle

def sierpinski(degree, points): # 阶数和三角形三个顶点的字典:left top right; 包含元组：x坐标，y坐标
    colormap = ['blue','red','green','white','gray','orange']
    drawTriangle(points, colormap[degree]) #画出等边三角形
    if degree > 0: # 画出三个品字形拼接的三角形，它们分别以原来三角形的左，顶，右顶点为一个点，另外两个顶点为边长的一半
        sierpinski(degree - 1, {'left':points['left'],'top':getMid(points['left'],points['top']),'right':getMid(points['left'],points['right'])})
        sierpinski(degree - 1, {'left': getMid(points['left'], points['top']),'top':points['top'],
                                'right': getMid(points['top'], points['right'])})
        sierpinski(degree - 1, {'left': getMid(points['left'], points['right']), 'top': getMid(points['top'], points['right']),
                                'right':points['right']})
def getMid(p1,p2):
    return ((p1[0]+ + p2[0]) / 2, (p1[1]+ + p2[1]) / 2) #x坐标加起来除以二

def drawTriangle(points, color):
    t.fillcolor(color) # 填色
    t.penup()
    t.goto(points['top'])
    t.pendown()
    t.begin_fill()
    t.goto(points['left'])
    t.goto(points['right'])
    t.goto(points['top'])
    t.end_fill()

t=turtle.Turtle()
points ={'left':(-200,-100),'top': (0,200),'right':(200,-100)} #points是一个字典
sierpinski(5,points)
turtle.done()
```
###6.4 动态规划实例问题
#### 1. 博物馆大盗问题
>* i:前i个物品，组合不超过w重量得到的最大价值；
m(i,w):当i-1时，怎么把第i个加进来：
1. 第i件太重，加不进来，还是前i-1最优 ——> m(i,w) = m(i-1 , w)
2. 第i件可以加进来——> m(i,w) = max{m(i-1,w),vi+m(i-1,w - wi)}
**和求maximum subarray一样**
```python
tr = [None, {'w':2,'v':3},{'w':3,'v':4},{'w':4,'v':8},{'w':5,'v':8},{'w':9,'v':10}] #宝物的重量和价值,第0件是0
max_w = 20
 # 初始化二维表格m[(i,w)]
 #表示前i个宝物中，最大重量w的组合，所得到的最大价值-

 #当i什么都不取的时候，或w上限为0，价值均为0
m = {(i , w):0 for i in range(len(tr)) for w in range(max_w + 1)}
#逐个填写这个二维表格
for i in range(1,len(tr)): # 每前i个物品
	for w in range(1,max_w + 1): # 都会经历背包容量的所有情况
		if tr[i]['w'] > w:
			m[(i,w)] = m[(i-1 , w)]
		else:
			m[(i, w)] = max(m[(i-1, w)], tr[i]['v'] + m[(i-1, w - tr[i]['w'])])
print(m[(len(tr) - 1, max_w)])
```
### 6.5 递归小结
>* 解决具有自相似问题的有效方法
>* **三定律**
>* 某些问题递归可以代替迭代
>* 递归可以用“记忆话/函数值缓存”来通过增加存储空间记录中间计算结果来有效减少重复计算
>* 递归是自顶向下，动态规划是自底向上；如果一个问题的最优解包括规模更小的相同问题的最优解，就可以用动态规划来解决；递归和动态规划一般是可以相互转换的

## 7. 顺序查找 Sequential Search
>* 列表中按下标增长顺序查找
>* 假定数据项在列表中出现在任意位置的可能性是一样的
>* 最好情况：1次；最差情况：n次 ——> n/2     O(n)
>* 有序表中的查找在元素不存在的情况下比无序表简单。可以提前结束查找。（虽然复杂度都是O(n)，但可以减少计算次数（不能改变数量级））

### 7.1 二分查找（有序表）
>* 从中间项开始比对，查找项和中间项大小比对，小：前半部；大：后半部 （必须是排好序）
>* 分而治之：分成小规模问题
>* O(logn)，其他开销：排序、切片，etc.
```python
#递归解法
def binarySearch(nums, item):
	if len(nums) == 0:
		return False #基本结束条件
	else:
		midpoint = len(nums) // 2 
		if nums[midpoint] == item:
			return True
		else:
		    if item < nums[midpoint]:
			    return binarySearch(nums[:midpoint], item) #切片
		    else:
			    return binarySearch(nums[midpoint : ], item)
```
### 7.2 冒泡排序（无序表）
>* 对无序表进行多趟比较排序
```python
def bubbleSort(nums):
	for passnum in range(len(nums)-1, 0, -1): # n-1 到 1
		for i in range(passnum):
			if nums[i] > nums[i+1]:
				nums[i], nums[i + 1] = nums[i + 1], nums[i]
```

>* 比对和交换的次数的时间复杂度是 O(n^2)
>* 效率很低下，但是节省了额外空间的开支；并且可以用于链表的排序
>* 记录已经交换的对
```python
def bubbleSort(nums):
	exchange = True #逆序的情况下发生了交换 exchange = True，如果一趟下来 false都没有变成True，说明已经排序好了
	passnum = len(nums)-1
	while passnum > 0 and exchange:
		exchange = False
		for i in range(passnum):
			if nums[i] > nums[i+1]:
				exchange = True
				nums[i], nums[i + 1] = nums[i + 1], nums[i]
		passnum -= 1
```
### 7.3 选择排序算法(冒泡排序的优化)

>* 每躺只做1次交换，每趟就位最大项。 逆序的时候并不交换，只是把他的位置记录下来，直到for循环这一趟完成之后，把这个项和最后一个项交换一下
```python
def selectSort(nums):
	for fillsort in range(len(nums) - 1, 0, -1):
		positionOfMax = 0
		for location in range(1, fillsort + 1):
			if nums[location] > nums[positionOfMax]:
				positionOfMax = location
				
```

### 7.4 插入排序
>* 后半部取一个出来，查找其应该在前半部整理好顺序的位置（扑克牌），不断扩展一排序好的子列表
>* 越接近有序，比对次数越少
```python
def insertSort(nums):
	for index in range(1, len(nums)): # 新项位置
		currentValue = nums[index]
		position = index
		while position > 0 and nums[position - 1] > currentValue: #把新的一项和他前面一项依次比较查找适合的位置
			nums[position] = nums[position - 1]
			position -= 1
		nums[position] = currentValue # 比新项小的第一个数的后面一个位置就是新项的位置
```
### 7.5 谢尔排序 （shell Sort）
>* 对子列表进行排序，让间隔越来越小，=1时就是有序序列
>* 一般间隔从n/2，有2个子列表
```python
def shellSort(nums):
	sublistcount = len(nums) // 2 #间隔设定
	while sublistcount > 0:
		for startposition in range(sublistcount): #间隔是多少，子列表就会有多少个
			gapInsertPosition(nums, startposition, sublistcount)
		print("After increments of size",sublistcount,"The list is ", nums)
		sublistcount //= 2 #缩小间隔

def gapInsertPosition(nums, start, gap):
	for i in range(start + gap, len(nums), gap):
		currentValue = nums[i]
		position = i

		while position >= gap and nums[position - gap] > currentValue:
			nums[position] = nums[position - gap] # 和插入排序一样
			position -= gap

		nums[position] = currentValue
```
### 7.6 归并排序（Merge Sort）
>* 分而治之，持续分裂对半，再进行归并排序
>* 结束条件：数据表仅有1个数据项
缩小规模：不断分为两半
调用自身排序
>* 归并
```python
def mergeSort(nums):
	if len(nums) > 1:
		mid = len(nums) // 2
		left = nums[:mid]
		right = nums[mid:]

		mergeSort(left)
		mergeSort(right)

		# 对排好序的左右半部进行合并
		# 1. 比较左右两部分的最小，哪边最小的更小，就放在左边
		i = j = k = 0
		while i < len(left) and j < len(right):
			if left[i] < right[j]:
				nums[k] = left[i]
				i += 1
			else:
				nums[k] = right[j]
				j += 1
			k += 1
		#2. 归并左部分剩余的
		while i < len(left):
			nums[k] = left[i]
			i += 1
			k += 1
		# 3. 归并右部分剩余的
		while j < len(right):
			nums[k] = right[j]
			j += 1
			k += 1

	print("Merging", nums)

mergeSort([2,6,3,4,5,3,1,6,8,3,1,6,9,2,0,2,45,7,2])
```
```python
def mergeSort(nums):
	if len(nums) <= 1:
		return nums

	mid = len(nums) // 2
	left = mergeSort(nums[:mid])
	right = mergeSort(nums[mid:])
	merged = []
	#1. 归并左右两边
	while left and right: # 只要左右半部都还有数据
		if left[0] <= right[0]:
			merged.append(left.pop(0)) # 永远比较left 和 right 第一个元素，比较后小的那个append并且在原本的left，right中删除首个元素，接着比较下一个
			print(merged)
		else:
			merged.append(left.pop(0))
			print(merged)
	#2. 归并左部分剩余的
	if right != None:
		merged.extend(right)
	if left != None:
		merged.extend(left)
	return merged

```
>* 1. 分裂：O(logn);
2. 归并： O(n)
总的时间复杂度：O(nlogn)
**但是用了一倍的额外存储空间来做归并**

### 7.7 快速排序
>* 依据一个中值，一半小于中值，一半大于；找中位值的话需要额外开销
**先分拣后分裂** O(nlogn)
>* 结束条件：length = 1
缩减规模：中值（最好是想等规模的两半）
调用自身：将分两半排序
>* 在数列之中，选择一个元素作为”基准”（pivot），或者叫比较值。
>* 数列中所有元素都和这个基准值进行比较，如果比基准值小就移到基准值的左边，如果比基准值大就移到基准值的右边
>* 以基准值左右两边的子列作为新数列，不断重复第一步和第二步，直到所有子集只剩下一个元素为止。

```python 
def quick_sort(b):

    """快速排序"""
    if len(b) < 2:
        return b
    # 选取基准，随便选哪个都可以，选中间的便于理解
    mid = b[len(b) // 2]
    # 定义基准值左右两个数列
    left, right = [], []
    # 从原始数组中移除基准值
    b.remove(mid)
    for item in b:
        # 大于基准值放右边
        if item >= mid:
            right.append(item)
        else:
            # 小于基准值放左边
            left.append(item)
    # 使用迭代进行比较
    return quick_sort(left) + [mid] + quick_sort(right)
```
## 8. 散列
Hash Table
>* 数据集，其中数据项的存储方式尤其有利于将来快速地查找定位
>* 每个存储位置称为槽 slot，保存数据项，唯一的名称 （和dict有点像）
>* 实现从数据项到存储槽名称的转换：hash function 散列函数（数据项是参数，返回槽名称）
>* 求余数
>* 负载因子：槽被数据项占据的比例
>* 冲突 collision：两个数据项放在同一slot

### 8.1 完美散列函数
>* 如果可以把所有数据项都映射到不同的槽中
>* 冲突最少，近似完美；计算难度低；充分分散数据项（利用率越高）
>* 一致性娇艳的数据（eg：指纹）：压缩性，易计算，抗修改性，抗冲突性
>* MD5（128位），SHA（160……）
>* 一致性校验，密码匹配……
>* 区块链技术：每个节点都包含所有数据
去中心化：所有节点都是平等的，所有数据在每个节点上都是平等的
1. block
2. head：元数据和连接到前一个区块的信息 （生成时间，前一个区块head+body的散列值）
3. body：实际的数据
4. 工作量证明（POW）
### 8.2 散列函数的设计
#### 1. 折叠法
隔数反转（微调手段）
适合key较多位的情况
#### 2. 平方取中
eg： 44^2 = 1936
98 % 11 = 5
计算量较大
#### 3. 非数项
抓换成ASCII码
```python
def hash(astring, tableSize):
	sum = 0 
	for pos in range(len(astring)):
		sum = sum + ord(astring[pos])
	return sum % tableSize
```
>* 变为词？ 每个字幕的位置加上权重因子（例如根据位置1，2，3）

### 8.3 散列冲突解决方案

####1.Open Addressing寻找空槽
>* 为冲突的slot找一个开放的空slot来存放
>* 向后逐个顺序查找的方法：linear probing
>* 查找的时候也是相同规则
>* 缺点：有聚集趋势 ——> 跳跃式探测，二次探测，逐步增加skip的值：1，4，9，16……
>* rehashingL: rehash(pos) = (pos + skip) % sizeoftable **（skip的值不能被散列别长度整除，可以直接把散列表的长度设置成质数）**

####2.数据项链
>* 每个槽可以存放多个数据项——>散列和查找的综合

###8.4 映射数据类型
##### 8.4.1 ADT Map 
>* 字典：key映射到value
>* 键值关联的无序集合，唯一关键码，唯一value
>* 基本操作：
1. map():创建一个空映射
2. put(key,value):将key-value加入映射中，如果key已经存在，用新的value代替旧的
3. get(key):返回关联的value，如果不存在，返回None
4. del map(key)：删除key-val的关联
5. len()：
6. key in map:返回key是否存在与关联中，返回bool值
>* 快速查找：HashTabel，一个slot：key，一个data：value
>* 特殊查找方法：
```python
	def __getitem__(self, key):
		return self.get(key)
	
	def __setitem__(self, key, value):
		self.put(key, value)
```
>* 散列在最好的情况下可以提供O(1)
>* 评估散列冲突最重要的信息就是负载因子 lamda：越小冲突几率越小

### 8.5 排序小结
>* 在无需表或者有序表上的顺序查找，时间复杂度位O(n)
>* 有序表上的二分查找，最差复杂度O(nlogn)
>* 散列表可以实现常数级时间的查找
>* 完美散列函数作为数据一致性校验，应用广泛

## 9. 树
>* 层次化的，越接近顶部的，越普遍，越底部的越独特
>* 一个节点的子节点和另外几个节点的子节点相互之间时隔离的，独立的
>* 每个叶节点都具有独特性

### 9.1 相关术语

>* 节点 node： 名称/键值
>* 边 edge：连接两个节点，具有出入方向；每个节点恰有**一条**来自另一节点的入边，有多条可以到其他节点的出边
>* 跟 root：没有入边的节点
>* 路径 path：由边依次连接在一起的节点的有序列表
>* 子节点 children：入边来自于同一节点的若干节点
>* 父节点 parent
>* 兄弟节点 sibling：具有同一个父节点
>* 子树 subtree：一个节点和所有子孙节点以及相关边的集合
>* 叶节点 leaf：没有子节点的节点
>* 层级 level：从根节点开始到达一个节点的路径所包含的边的数量
>* 高度：所有节点的最大层级

### 9.2 树的定义
>* 节点定义：每个节点，都恰有1条来自parent的入边；每个节点从root开始的路径是唯一的；如果每个节点最多有两个子节点——>二叉树
>* 递归定义：空集，或者由根节点及0或多个子树构成（子树也是树）

### 9.3 嵌套列表实现 （list）
>* 三个元素：根节点的值(数据项)，左子树（三元素列表），右子树 （三元素列表）
```python
[root, left, right]
```
>* 容易扩展到多叉树
>* BinaryTree
insertLeft/insertRight
get/setRootVal
getLeft/RightChild
```python
def BinaryTree(r):
	return [r, [], []]

def insertLeft(root, newBranch):
	t = root.pop(1) # 把左子树给pop出来
	if len(t) > 1: # 原先有左子树
		root.insert(1, [newBranch, t, []]) # 插入位置是1：左子树,新子树的根就是newbranch，他的左子树就是原来的左子树（pop出来那个）
	else:
		root.insert(1, [newBranch, [], []]) # 原先是个空，newbranch的左右列表页都是空
	return root

def insertright(root, newBranch):
	t = root.pop(2) # 把右子树给pop出来
	if len(t) > 1: # 原先有右子树
		root.insert(2, [newBranch, [], t]) # 插入位置是2：右子树,新子树的根就是newbranch，他的右子树就是原来的右子树（pop出来那个）
	else:
		root.insert(2, [newBranch, [], []]) # 原先是个空，newbranch的左右列表页都是空
	return root

def getRootVal(root):
	return root[0]

def setRootVal(root, newVal):
	root[0] = newVal

def getLeftChild(root):
	return root[1]

def getRightChild(root):
	return root[2]

r = BinaryTree(3)
insertLeft(r, 4)
insertLeft(r, 5)
insertright(r, 6)
insertright(r, 7)

l = getLeftChild(r)
print(l)

setRootVal(l, 9)
print(r)
insertLeft(l, 11)
print(r)
print(getRightChild(getRightChild(r)))

# 结果
[5, [4, [], []], []]
[3, [9, [4, [], []], []], [7, [], [6, [], []]]]
[3, [9, [11, [4, [], []], []], []], [7, [], [6, [], []]]]
[6, [], []]
```
### 9.4 树的链表实现
>* 每个节点保存根节点的数据项，以及指向左右子树的链接
key：根节点数据项；成员left/right：保存指向左/右子树的引用
```python
class BinaryTree:
	def __init__(self, rootObj):
		self.key = rootObj
		self.leftChild = None
		self.rightChild = None

	def insertLeft(self, newNode):
		if self.leftChild == None: # 如果原来的左指向是空的的
			self.leftChild = BinaryTree(newNode)
		else:
			t = BinaryTree(newNode) #生成一个二叉树
			t.leftChild = self.leftChild # 新的左子树指向原来的左子树
			self.leftChild = t#root的左子树指向新的左子树

	def insertRight(self, newNode):
		if self.rightChild == None: # 如果原来的左指向是空的的
			self.rightChild = BinaryTree(newNode)
		else:
			t = BinaryTree(newNode) #生成一个二叉树
			t.rightChild = self.rightChild # 新的左子树指向原来的左子树
			self.rightChild = t#root的左子树指向新的左子树
			
	def getRootVal(self):
		return self.key

	def setRootVal(self, obj):
		self.key = obj

	def getLeftChild(self):
		return self.leftChild

	def getRightChild(self):
		return self.rightChild
```
### 9.5 应用：解析树
>* 分析表示语言中的成分，程序设计语言的编译，自然语言处理
>* 子节点求值然后合并成一个节点
>* 1.从全括号表达式构建表达式解析树（分解为单词token）

>>* eg：(3+(4*5))   ->   ['(','3','+','(','4','*','5',')',')']
空树  ->  当前节点：根节点  ->  '(' 代表表达式的开始，创建左子点，当前节点下降  -> '3' 当前节点为3，上升到父节点（下一个肯定是操作符）   ->  '+' 当前节点，创建有子节点   ->  读入'(',新的表达式出现了，创建左子节点，当前节点下降  ->  '4'，当前节点为4，上升到父节点  ->  '*'为当前节点，创建右子节点，下降  ->  ‘5’上升到父节点  ->  ‘)’ 当前表达式结束，上升到父节点 ->  ‘)’ 当前表达式结束，上升到父节点，表达式结束
>>* **从左到右扫描全括号表达式的每一个单词，1. '(': 添加新节点为左子节点，下降当前节点；2.操作符：设置为当前节点，增加右子节点，下降当前节点；3. 操作数：设置为当前节点的值，上升到父节点；4.')'：当前节点上升到父节点**
>>* **对当前节点的跟踪非常重要**
>>* 上升到父节点没有方法支持？
我们可以用**栈**来跟踪父节点，当下降的时候，把下降前的节点push到stack，当需要上升到父节点的时候：pop()出stack里的节点就可以了
```python
from pythonds.basic.stack import Stack


class BinaryTree:
	def __init__(self, rootObj):
		self.key = rootObj
		self.leftChild = None
		self.rightChild = None

	def insertLeft(self, newNode):
		if self.leftChild == None:  # 如果原来的左指向是空的的
			self.leftChild = BinaryTree(newNode)
		else:
			t = BinaryTree(newNode)  # 生成一个二叉树
			t.leftChild = self.leftChild  # 新的左子树指向原来的左子树
			self.leftChild = t  # root的左子树指向新的左子树

	def insertRight(self, newNode):
		if self.rightChild == None:  # 如果原来的左指向是空的的
			self.rightChild = BinaryTree(newNode)
		else:
			t = BinaryTree(newNode)  # 生成一个二叉树
			t.rightChild = self.rightChild  # 新的左子树指向原来的左子树
			self.rightChild = t  # root的左子树指向新的左子树

	def getRootVal(self):
		return self.key

	def setRootVal(self, obj):
		self.key = obj

	def getLeftChild(self):
		return self.leftChild

	def getRightChild(self):
		return self.rightChild

def biuldParseTree(fpexp):
	fplist = fpexp.split() #把解析式分开存入list
	pStack = Stack() #节点栈
	eTree = BinaryTree('') #空的树
	pStack.push(eTree) #当前节点入栈
	currentTree = eTree #当前节点设置为刚才创建的第一个节点
	for i in fplist:
		if i =='(':#左括号：添加新节点为左子节点，当前节点入stack然后下降当前节点
			currentTree.insertLeft('')
			pStack.push(currentTree)# 入栈下降
			currentTree = currentTree.getLeftChild()
		elif i not in ['+', '-', '*', '/', ')']: #操作数：设置为当前节点的值，上升到父节点
			currentTree.setRootVal(int(i))
			parent = pStack.pop()# 出栈上升
			currentTree = parent
		elif i in ['+', '-', '*', '/']: #操作符：设置为当前节点，增加右子节点，下降当前节点
			currentTree.setRootVal(i)
			currentTree.insertRight('')
			pStack.push(currentTree)# 入栈下降
			currentTree = currentTree.getRightChild()
		elif i == ')': #右括号：当前节点上升到父节点
			currentTree = pStack.pop() # 出栈上升
		else:
			raise ValueError
	return eTree
```
>* 2.利用表达式解析树对表达式求值
>>* 是一个递归数据结构，可以用递归算法来处理
>>* 越底层的越先计算
>>* 基本结束条件：叶节点是最简单的子树，根节点的数据项即为字表达是的值
缩小规模：分为左右子树
调用自身：计算左右子树的值，然后根节点的操作符进行计算从而得到表达式的值
```python
def evaluate(parseTree):
	opers = {'+':operator.add, '-':operator.sub,'*':operator.mul, '/':operator.truediv} # 从加减乘除的符号到函数的映射
	leftC = parseTree.getLeftChild() # 缩小规模
	rightC = parseTree.getRightChild()
	
	if leftC and rightC: #存在左右子树
		fn = opers[parseTree.getRootVal()] #get操作符
		return fn(evaluate(leftC),evaluate(rightC)) #根据字典，操作符转换成了都拥有两个参数的函数
	else:
		return parseTree.getRootVal() #基本结束条件（是个叶节点）
```

>* 3.从表达式解析树恢复原表达式的字符串形式，要用到下面讲到的中序遍历：左中右
```python
def printexp(tree):
	sVal = ''
	if tree:
		sVal = '(' + printexp(tree.getLefChild())
		sVal += str(tree.getRootVal())
		sVal += printexp(tree.getRightChild()) + ')'
	return sVal
```

### 9.6 树的遍历 Tree Traversals
>* 前序遍历 preorder：先访问root，然后左子树，右子树
```python
def preorder(tree):
	if tree:
		print(tree.getRootVal())
		preorder(tree.getLeftChild())
		preorder(tree.getRightChild())
```
>* 中序遍历 inorder：左子树，root，右子树
```python
def inorder(tree):
	if tree != None:
		inorder(tree.getLeftChild())
		inorder(tree.geRootVal())
		print(tree.getRightChild())
```
>* 后序遍历 postorder：左子树，右子树，root (表达式求值)
```python
def postorder(tree):
	if tree != None:
		postorder(tree.getLeftChild())
		postorder(tree.getRightChild())
		print(tree.getRootVal())
```
```python
# 表达式求值
def postOrderCal(tree):
	res1 = None
	res2 = None
	opers = {'+': operator.add, '-': operator.sub, '*': operator.mul, '/': operator.truediv}
	if tree:
		res1 = postOrderCal(tree.getLeftChild())
		res2 = postOrderCal(tree.getRightChild())
		if res1 and res2:
			return opers[tree.getRootVal()](res1, res2)
		else:
			return tree.getRootVal()
```
### 9.7 优先队列（priority queue）和二叉堆
>* 队列：FIFO，但是可以插队
>* 从队首出队，但是在内部是按照优先级来确定次序的，高优先级在队首，低优先级在队尾（入队比较复杂）
>* 二叉堆来实现：入队出队都在O(nlogn)，逻辑上和二叉树相似，但其实是用非嵌套的列表来实现的

####  9.7.1 二叉堆

##### 1. 基本操作：

>* （优先级最高）最小key排在队首的成为：最小堆min heap；最大key排在队首的是：最大堆max heap
>* BinaryHeap():创建一个空的二叉堆
>* insert(k):加入新key
>* findMin():返回最小项
>* delMin():返回最小项，同时删除 （出队）
>* isEmpty():返回堆是否为空
>* size():返回堆中key个数
>* buildHeap(list):从一个key列表创建新堆

##### 2. 保持二叉树的平衡

>* 完全二叉树结构来近似实现“平衡”：叶节点最多只出现在底层和次底层，而且最底层的叶节点都连续集中在最左边，每个内部节点都有两个子节点，最多可以右1个节点例外
（若设⼆叉树的⾼度为h，除第 h 层外，其它各层 (1～h-1) 的结点数都达到最⼤个数，第h层有叶⼦结点，并且叶⼦结点都是从左到右依次排布，这就是完全⼆叉树。）
>* 可以由非嵌套列表实现 （根节点是从1开始表示才有如下性质）
节点：P；左子节点：2P；右子节点：2P+1；父节点：p//2
>* 堆次序：任何一条path都是一条排序的数列，根节点的key最小

##### 3. 实现

>* 二叉堆初始化：
```python
class BinHeap:
	def __init__(self): # 表首的下标为0的无用，为了后面方便整除，保留
		self.heapList = [0]
		self.currentSize = 0
```
>* insert(key): 添到列表末尾？破坏堆节点次序 ——> 沿着路径上浮，和父节点交换直到比子节点小
```python
	def perUp(self,i): # 上浮
		while i//2 > 0: # 沿着路径一直往上
			if self.heapList[i] < self.heapList [i // 2]: #父节点
				temp = self.heapList[i // 2]
				self.heapList[i // 2] = self.heapList[i]
				self.heapList[i] = temp
			i //= 2
	
	def insert(self,k):
		self.heapList.append(k) # 添加到末尾
		self.currentSize += 1
		self.perUp(self.currentSize)#上浮操作
```
>* demMin():其实就是移走root（最小的key）.
和上浮相反，将root进行下沉操作，直到比两个子节点都小
选择子节点里面较小的进行交换
```python
	def percDown(self, i):
		while (i * 2) <= self.currentSize:# 只要i<=currentsize，就沿某条路径往下
			mc = self.minChild(i) # 子节点中更小的那个
			if self.heapList[i] > self.heapList[mc]:
				tmp = self.heapList[i]#交换
				self.heapList[i] = self.heapList[mc]
				self.heapList[mc] = tmp
			i = mc # 当前的root就下沉到了交换的那个位置
			
	def minChild(self,i): 
		if i * 2 + 1 > self.currentSize:
			return i * 2 # 如果只有一个子节点
		else:
			if self.heapList[i * 2] < self.heapList[i * 2 + 1]:
				return i * 2
			else:
				return i * 2 + 1

	def delMin(self):
		retVal = self.heapList[1] #移走堆顶
		self.heapList[1] = self.heapList[self.currentSize] # 把最后一个节点搬到root
		self.currentSize -= 1
		self.heapList.pop()# 删掉最后的那个节点（已经被搬到了root）
		self.percDown(1)#开始下沉，纠正次序
		return retVal
```

>* biuldHeap():从无序表生成堆

```python
	def biuldHeap(self,alist):
		i = len(alist) // 2 # 从最后节点的父节点开始下沉
		self.currentSize = len(alist)
		self.heapList = [0] + alist[:]
		print(len(self.heapList), i)
		while(i > 0):
			print(self.heapList, i)
			self.percDown(i)
			i -= 1
		print(self.heapList, i)
```
### 9.8 二叉查找树及操作 Binary Search Tree
>* 比父节点小的key都出现在左子树，比父节点大的key都出现在右子树
>* 插入的顺序不一样，生成的BST也不一样
>* 需要用到两个class，bst和treenode
>* 删除操作：
1. 待删除节点既无左子树也无右子树：直接删除该节点即可
2. 待删除节点只有左子树或者只有右子树：将其左子树或右子树根节点代替待删除节点
3. 待删除节点既有左子树也有右子树：找到该节点右子树中最小值节点，使用该节点代替待删除节点，然后在右子树中删除最小值节点
```python
class BinarySearchTree:
	def __init__(self):
		self.root = None
		self.size = 0
	def length(self):
		return self.size
	def __len__(self):
		return self.size
	def __iter__(self):
		return self.rppt.__iter__()
class TreeNode:
	def __init__(self, key, val, left = None, right = None, parent = None):
		self.key = key # key
		self.playload = val #数据项
		self.leftChild = left
		self.rightChild = right #左右节点
		self.parent = parent #父节点

	def hasLeftChild(self):
		return self.leftChild

	def hasRightChild(self):
		return self.rightChild

	def isLeftChild(self): # 判断是不是其父节点的左子节点
		return self.parent and self.parent.leftChild == self

	def isRightChild(self):# 判断是不是其父节点的右子节点
		return self.parent and self.parent.rightChild == self

	def isRoot(self):
		return not self.parent

	def isLeaf(self):
		return not (self.rightChild or self.leftChild)

	def hasAnyChildren(self): # 是否有子节点
		return self.rightChild or self.leftChild

	def hasBothChildren(self):# 是否同时有左右子节点
		return self.rightChild and self.leftChild

	def replaceNodeData(self, key, value, lc, rc):
		self.key = key
		self.playload = value
		self.leftChild = lc
		self.rightChild = rc
		if self.hasLeftChild():
			self.leftchild.parent = self
		if self.hasRightChild():
			self.rightChild.parent = self

	def put(self, key, val):
		if self.root: # 树本来不空
			self._put(key,val,self.root)
		else:
			self.root = TreeNode(key, val)
		self.size += 1

	def _put(self, key, val, currentNode):
		if key < currentNode.key: # key 比current Node 小，key成为左节点
			if currentNode.hasLeftChild():
				self._put(key, val, currentNode.leftChild)
			else:#如果没有左子树，那么key就成为左子节点
				currentNode.leftChild = TreeNode(key, val, currentNode.leftCHild)
		else:
			if currentNode.hasRightChild():
				self._put(key, val, currentNode.rightChild)
			else:
				currentNode.rightChild = TreeNode(key, val, parent = currentNode)

	def __setitem__(self, key, value):# 索引赋值
		self.put(key, value)

	def get(self, key): # 通过key找到payload
		if self.root:
			res = self._get(key, self.root)
			if res:
				return res.payload #返回payload
			else:
				return None
		else:
			return None

	def _get(self, key, currentNode):
		if not currentNode:
			return None
		elif currentNode.key == key:
			return currentNode
		elif key < currentNode.key:
			return self._get(key, currentNode.leftChild)
		else:
			return self._get(key, currentNode.rightChild)

	def __getitem__(self, item): #实现 val = myZipTree['PKU']
		return self.get(item)

	def __contains__(self, item): # 归属判断
		if self._get(item, self.root):
			return True
		else:
			return False

	def __iter__(self): # 中序遍历
		if self: # root不为空
			if self.hasLeftChild():
				for elem in self.leftChild: # 递归调用
					yield elem # 每次调用返回一个elem
			yield self.key
			if self.hasRightChild():
				for elem in self.rightChild:
					yield elem

```

```python
    # 删除
    def delete(self, root, data):
        flag, n, p = self.search(root, root, data)
        if flag is False:
            print "无该关键字，删除失败"
        else:
            if n.lchild is None:
                if n == p.lchild:
                    p.lchild = n.rchild
                else:
                    p.rchild = n.rchild
                del n
            elif n.rchild is None:
                if n == p.lchild:
                    p.lchild = n.lchild
                else:
                    p.rchild = n.lchild
                del n
            else:  # 左右子树均不为空
                pre = n.rchild
                if pre.lchild is None:
                    n.data = pre.data
                    n.rchild = pre.rchild
                    del pre
                else:
                    next = pre.lchild
                    while next.lchild is not None:
                        pre = next
                        next = next.lchild
                    n.data = next.data
                    pre.lchild = next.rchild
                    del next
#注意此处没有考虑BTS中只有一个根节点的情况。应该重新写一个if进行判断。
#if self.root==data:
#self.root=None
```
>* 二叉查找树的高度，又受存放数据项的顺序有关系
>* 如果key的列表是随机分布的话，那么大于和小于根节点Key的键值大致相等
>* BST的高度就是log2n而且这样就是平衡树
>* put的方法最差性能为O(log2n)
>* 但如果key列表分布极端情况:O(n)

### 9.9 AVL树的定义 (平衡的二叉查找树)
AVL树是带有平衡条件的二叉查找树，一般要求每个节点的左子树和右子树的高度最多差1（-1，0，1）(空树的高度定义为-1)。
>* balanceFactor = height (leftsubTree) - height(rightsubTree)
如果平衡因子>0，称之为左重，小于零称之为右重 最差情况O(logn)
>* 插入： 影响父节点的平衡因子，父节点的平衡因子再往上影响到根节点，或者是某一节点的平衡因子被影响到0为止
>>* 右重：左旋。（右子节点作为newroot，将oldroot作为左子节点，如果newroot原本有左子节点，将其改到oldroot的右子节点）
在左旋之前要检查右子节点的因子，如果右子节点“左重”的话，先对他进行右旋转再实施原来的左旋转

```python
	def _put(self, key, val, currentNode):
		if key < currentNode.key: # key 比current Node 小，key成为左节点
			if currentNode.hasLeftChild():
				self._put(key, val, currentNode.leftChild)
			else:#如果没有左子树，那么key就成为左子节点
				currentNode.leftChild = TreeNode(key, val, currentNode.leftCHild)
				self.updateBalance(currentNode.leftChild)
		else:
			if currentNode.hasRightChild():
				self._put(key, val, currentNode.rightChild)
			else:
				currentNode.rightChild = TreeNode(key, val, parent = currentNode)
				self.updateBalance(currentNode.rightChild)
	
	def updateBalance(self, node):
		if node.balanceFactor > 1 or node.balanceFactor < -1:
			self.rebalance(node) #不平衡要重新调整
			return
		if node.parent != None:#有父节点
			if node.isLeftChild():
				node.parent.balanceFactor += 1
			elif node.isRightChild():
				node.parent.balanceFactor -= 1
			if node.parent.balanceFactor != 0:
				self.updateBalance(node.parent)
```
>* rebalance:将不平衡的子树进行旋转rotation；根据左重 or 右重进行不同方向的旋转，同时更新父节点的饮用，以及更新以后被影响的节点平衡因子
>>* 左重：右旋。（左子节点作为newroot，将oldroot作为左子节点，如果newroot原本有左子节点，将其改到oldroot的右子节点）
在右旋之前要检查左子节点的因子，如果左子节点“右重”的话，先对他进行左旋转再试实施原来的右旋转

```python
	#左旋
	def rotateLeft(self, rotRoot): #rotRoot是旧根
		newRoot = rotRoot.rightChild # 右子节点
		rotRoot.rightChild = newRoot.leftChild #右子节点如果有左子节点，赋给旧root做他的右子节点1
		if newRoot.leftChild != None:
			newRoot.leftChild.parent = rotRoot
		newRoot.parent = rotRoot.parent
		if rotRoot.isRoot():# 判断旧的根有没有父节点
			self.root = newRoot
		else:
			if rotRoot.isLeftChild():
				rotRoot.parent.leftChild = newRoot
			else:
				rotRoot.parent.rightChild = newRoot
		newRoot.leftChild = rotRoot
		rotRoot.parent = newRoot
		rotRoot.balanceFactor = rotRoot.balanceFactor + 1 - min(newRoot.balanceFactor, 0)
		newRoot.balanceFactor = newRoot.balanceFactor + 1 + max(rotRoot.balanceFactor, 0) 
		#左旋对平衡因子的影响：子树的平衡因子不会变，只有newroot和oldroot变换，表达式转换就可以得到newroot，oldroot的关系
```

>>* 左重：右旋（左子节点作为newroot，将oldroot作为右子节点，如果newroot原本有右子节点，将其改到oldroot的左子节点）
右旋之前检查左子节点的因子，如果左子节点“右重”的话，先对其进行左旋转，再实施原来的右旋转
```python
#左旋和右旋
	def rebalance(self,node):
		if node.balanceFactor < 0: # 右重需要左旋
			if node.rightChild.balanceFactor > 0: # 先判断右子节点是不是左重
				self.rotateRight(node.rightChild)
				self.rotateLeft(node)
			else:
				self.rotateLeft(node)
		elif node.balenceFactor > 0: # 左重需要右旋
			if node.leftChild.balanceFactor < 0: # 先判断左子节点是不是右重
				self.rotateLeft(node.leftChild)
				self.rotateRight(node)
			else:
				self.rotateRight(node)
```
>* get 始终保持O（logn），
put方法比较复杂：插入的是leaf节点：O(logn)；插入的会引起平衡因子改变：O(logn)
### 9.10 小结
>* 用于表达式解析和求值的二叉树
>* 用于实现ADT Map的二叉查找树BST树
>* 改进了性能的AVL树
>* 实现了最小堆的二叉堆
## 10. 图 Graph
### 10.1 基本术语
>* 顶点 Vertex：基本组成部分，顶点具有名称标志key，也可以携带数据项payload
>* 边 edge（弧：Arc）：可以是有向的或者无向的
>* 权重：weight（代价）：赋权图
>* 图 G(V,E):顶点的集合和边的集合；E中每条边e=(v,w):v,w都是V中的顶点
如果是赋权图，可以在e中添加权重分量
>* 路径 path：由边依次连接起来的顶点序列；无权路径的长度为边的数量，有权路径的长度为所有变的权重的和
>* 圈 cycle：起点重点是同一个顶点
如果一个graph没有cycle：有向无圈图（DAG），**如果可以表示为DAG就可以很好的解决问题（树）**
### 10.1 基本操作
>* Graph()：创建一个空的图
>* addVertex(vert):将顶点vert加入图中
>* addEdge(fromVert, toVert)
>* addEdge(fromVert, toVert, weight)
>* getVertex(vKey):查找名称为vKey的顶点
>* getVertices():返回图中所有定点列表
>* in:按照 vert in graph 的语句形式，返回定点是否在graph中的True/False

### 10.2 adjacency matrix 邻接矩阵
>* 如果图的边数很少， sparse matrix，效率很低（现实中大部分都是很稀疏的）

### 10.3 adjacency list 邻接表
>* 维护一个包含所有丁点的主列表 master list，祝列表中的每个顶点，再关联一个与自身有边链接的所有顶点的列表
eg：id = "V0" adj = {V1:5, V5:2}
>* 紧凑高效，容易获得顶点以及相连接的边的信息
```python
class vertex: # 包含了顶点信息，以及顶点链接信息
	def __init__(self, key):
		self.id = key
		self.connectedTo = {} # 链接的字典

	def addNeighbor(self, nbr, weight = 0): # 加边进去
		self.connectedTo[nbr] = weight # nbr是和顶点连接的key，与nbr的连接的权重为weight

	def __str(self): # 把所有顶点以字符串的形式打印出来
		return str(self.id) + 'connectedTo:' + str([x.id for x in self.connectedTo])

	def getConnections(self):  # 把这个顶点连接的所有顶点打印出来
		return self.connectedTo.keys()

	def getId(self):
		return self.id

	def getweight(self, nbr):
		return self.connectedTo[nbr] # 返回连接到nbr这个顶点的权重

class Graph: # 包含了所有顶点的主表
	def __init__(self):
		self.vertList = {}
		self.numVertices = 0 # 顶点数量

	def addVertex(self, key):
		self.numVertices = self.numVertices + 1
		newVertex = vertex(key)
		self.vertList[key] = newVertex
		return newVertex

	def getVertex(self, n):
		if n in self.vertList:
			return self.vertList[n]
		else:
			return None

	def __contains__(self, item):
		return item in self.vertList

	def addEdge(self, f, t, cost = 0):
		if f not in self.vertList:
			nv = self.addVertex(f) # 如果起始f顶点不存在，那么先添加f顶点
		if t not in self.vertList:
			nv = self.addVertex(t) # 如果终点t顶点不存在，先添加
		self.vertList[f].addNeighbor(self.vertList[t], cost) # 把cost作为权重，连接f和t顶点
		
	def getVertices(self): # 把顶点以list形式全部返回
		return self.vertList.keys()
	
	def __iter__(self):
		return iter(self.vertList.values())
```
```python
g = Graph()
for i in range(6):
	g.addVertex(i)
	
0 connectedTo: []
1 connectedTo: []
2 connectedTo: []
3 connectedTo: []
4 connectedTo: []
5 connectedTo: []

# 结果
{0: 0 connectedTo: [], 1: 1 connectedTo: [],……, 5: 5 connectedTo: []}

g.addEdge(0, 1, 5)
g.addEdge(0, 5, 2)
g.addEdge(1, 2, 4)
g.addEdge(2, 3, 9)

for i in g:
	for w in v.getConnection():
		print "(%s, %s)" % (v.getId(), w.getId()) # 把成对的有连接的顶点都打印出来了

# 结果
(0, 1)
(0, 5)
(1, 2)
(2, 3) 
```

### 10.4 图的应用：词梯问题
>* 相邻两个单词之间差异只能是1个字母，找到最短的演变关系
：
>* 1.将可能的单词之间的演变关系表达为图：单词作为顶点如果两个词之间只相差1个字母，就在他们之间设一条边（无向图，没有权重）
建立边：创建大量的桶，每个桶放若干个单词，桶标记是去掉一个字母的单词，所有匹配的单词都放到这个同理，再在这个桶里的每个单词之间建立边即可
>* 2.**广度优先搜索 Breadth First Search** ，搜索所有有效路径。FIFO，  O(|V|+|E|)
>>* 可以搜索出所有从s到目的地的边，在到达更远的距离为k+1的顶点之前，bfs会找到全部距离为k的顶点，能保证在怎加层次之前，添加了所有兄弟节点到树中
>>* 为了避免重复的顶点：
1. 记录三个属性（距离distance：到起始顶点的距离， 前驱顶点predecessor，颜色color：标志了这个顶点是已经发现的灰色，尚未发现的的白色，完成探索的黑色）;
2. 队列来对已经发现的顶点进行排列（决定了下一个要探索的顶点: 队首）
```python
def bfs(g, start):
	start.setDistance(0)
	start.setPred(None)
	vertQueue = Queue()
	vertQueue.enqueue(start)
	while (vertQueue.size() > 0): # 对每个顶点都访问一次
		currentVert = vertQueue.dequeue() #取队首作为当前顶点
		for nbr in currentVert.getConnectioins(): # 每个顶点连接的所有边，遍历所有连接顶点的点
			if (nbr.getColor() == 'white'): # white代表没有探索过
				nbr.setColor('gray') # gray代表正在探索
				nbr.setDistance(currentVert.getDistance() + 1)
				nbr.setPred(currentVert) # 前驱设为当前顶点
				vertQueue.enqueue(nbr) # 入队
		currentVert.setColor('black') # 探索完成
```
>>* 3.找到最短路径
通过一个回途追溯函数来确定最短路径O(|V|)
```python
def traverse(y):
	x = y
	while(x.getPred()):
		print(x.getId())
		x = x.getPred()
	print(x.getId())
```
### 10.5 图的应用:骑士周游问题
>* 马走日：最多可以有8个格子合法
```python
def genLegalCoord(x, y, bdSize):
	newMoves = []
	moveOffsets = [(-1, -2), (-1, 2), (-2, -1), (-2, 1), ( 1, -2), ( 1, 2), ( 2, -1), ( 2, 1)] # 马走日的8个格子，根据当前的位置来确定的相对位置坐标
	for i in moveOffsets:
		newX = x + i[0]
		newY = y + i[1]
		if legalCoord(newX, bdSize) and legalCoord(newY, bdSize): # 判断有没有走出棋盘
			newMoves.append(newX, newY)
	return newMoves

def legalCoord(x, bdSize):
	if x >= 0 and x < bdSize:
		return True
	else:
		return False
def knightGraph(bdSize): # 构建走棋的关系图
	ktGraph = Graph()
	for row in range(bdSize):
		for col in range(bdSize): # 遍历每一个格子
			nodeId = posToNodeId(row, col, bdSize)
			newPositions = genLegalMoves(row, col, bdSize) # 只要是合法的格子 就放到newPosition里面去
			for e in newPositions:
				nid = posToNodeId(e[0], e[1], bdSize) # 获取合法格子
				ktGraph.addEdge(nodeId, nid) # 加边
	return ktGraph

def posToNodeId(row, col, bdSize):
	return row * bdSize + col   # 每个格子的id和行列有关系
```
>* **深度优先搜索 Depth First Search**
1. 每个顶点只访问一次
2. 顶点可以重复访问
```python
def knightTour(n, path, u, limit): # n：层次， path：路径， u：当前顶点，limit：探索总深度 8x8 ——> 63
	u.setColor('gray') # 当前节点正在探索
	path.append(u) # 加入路径(入栈 push)
	if n < limit: # 还没有到预定深度
		nbrList = list(u.getConnections()) # 接下来访问的连接的合法格子
		i = 0
		done = False
		while i < len(nbrList) and not done: # 获取所有合法的格子
			if nbrList[i].getColor() == 'white': #还没被探索过的
				done = knightTour(n+1, path, nbrList[i], limit) # 递归，当前节点变成了nbrList[i]
			i += 1
			if not done:
				path.pop() # 已经完成了所有合法格子的探索 但是还没有到大预定深度，那么就标白，然后回溯上一个节点（pop掉当前顶点）
				u.setColor('white')
			else:
				done = True
			return done
```
>* 分析：DFS骑士周游的复杂度高度依赖于棋盘的大小 O(k^n)
>* 改进：Warnsdorff 算法：进修改了遍历下一个的次序；将u的合法移动目标棋盘格排序为具有最少合法移动目标的格子优先搜索
（刚才dfs算法中的nbrList直接以最原始的顺序来确定深度优先搜索的分支次序，不关心nbrList里面顶点的顺序）
```python
def oderByAvail(n):
	resList = [] # 下一个合法顶点的集合
	for v in n.getConnections():
		if v.getColor() == 'white':
			c = 0
			for w in v.getConnections():
				if w.getColor() == 'white':
					c += 1
			resList.append((c,v))
	resList.sort(key = lambda x: x[0]) # 指定按照resList里面每个元组的第0个元素排序; 
	return [y[1] for y in resList] #具有最少合法格子的下一个顶点在最前面
```
>* 启发式规则：heuristic。采用先验的只是来改进算法性能的做法（减少时间复杂度）会沿着棋盘的周边走再走到中间

### 10.6 通用的Depth First Search
>* 在图上进行尽量深度搜索，连接尽量多的顶点，必要时可以进行分支（创立树），由多个分支 ——> 森林
>* 设置发现时间和结束时间属性（前者是第几部访问到这个顶点的（灰色），后者是在第几步完成了对此顶点的探索的（黑色））
```python
class DFSGraph(Graph): # Graph的子类
	def __init__(self):
		super().__init__() #单继承，即只有一个父类
		self.time = 0

	def dfs(self): # O(V)
		for aVertex in self:
			aVertex.setColor('white') # 颜色初始化，所有颜色都是白色的，没有探索过
			aVertex.setPred(-1)
		for aVertex in self:
			if aVertex.getColor() == 'white': # 只要是白色的，就从他开始建立单棵的树
				self.dfsVisit(aVertex)
				
	def dfsVisit(self, startVertex): # 创建单棵的深度优先树 O(E)
		startVertex.setColor('gray')
		self.time += 1
		startVertex.setDiscovery(self.time) # 时间设置为当前时间
		for nextVertex in startVertex:
			if nextVertex.getColor() == 'white':
				nextVertex.setPred(startVertex)
				self.dfsVisit(nextVertex)
		startVertex.setColor('black') # 探索完毕
		self.time += 1
		startVertex.setFinish(self.time) # 结束探索，设置finish time
```
>* DFS构建的树，其顶点的“发现时间”和“”结束时间，就类似于括号的性质。
发现时间<所有子顶点发现时间，结束时间>所有子顶点结束时间。
**发现的越早，结束的越晚**

### 10.7 图的应用：拓扑排序
>* 从工作流程图得到工作次序线性排列的算法 ——> 拓扑排序 （处理DAG）
有V到W的边，那线性序列中v一定在w前面 （相互依赖事件的排序）
>* 对DAG调用DFS算法，来得到每个顶点的“结束时间”，按结束时间从小到大排列，输出这个次序下的顶点列表

### 10.8 图的应用：强联通分支
>* 定义为G的一个子集C：C中的任意两个顶点v w之间都有路径来回，C是具有这样性质的最大子集
>* 转置：（v，w）转换为（w，v）
>* kosaraju算法：DFS记录结束时间，转置，结束时间最大的顺序DFS

### 10.9 图的应用：最短路径
>* Dijkstra：一个顶点到所有顶点的最短路径
>* 顶点vertex类中的成员dist用于记录从开始顶点到本顶点的最短带权路径长度（权重之和），对途中每个顶点迭代一次
>* 顶点的访问次序是由一个优先队列来控制的，作为优先级的是顶点的dist属性
>* 只能处理图里面权重 > 0的
>* 需要具备整个图的所有数据，不能及时更新（耗时耗力）
```python
from pq import PriorityQueue, Graph, Vertex


# 最短路径
# G - 无向赋权图
# start - 开始节点
# 返回从开始节点到其它所有节点的最短带权路径
def dijkstra(G, start):
    pq = PriorityQueue()  # 创建优先队列 #O(v)
    start.setDistance(0)  # 起点距离设置为0，其它节点距离默认maxsize
    # 将节点排入优先队列，start在最前面
    pq.buildHeap([(v.getDistance(), v) for v in G])
    while not pq.isEmpty(): #O(logv)
        # 只要还有点取从start开始距离最小的节点出队列，作为当前节点
        # 当前节点已解出最短路径
        currentVert = pq.delMin() #出队：O(|v|logv)
        # 遍历节点的所有邻接节点
        for nextVert in currentVert.getConnections():
            # 从当前节点出发，逐个加上邻接节点的距离进行检验
            newDist = currentVert.getDistance() \
                      + currentVert.getWeight(nextVert)
            # 如果小于邻接节点原有距离，就更新邻接节点
            if newDist < nextVert.getDistance():
                # 更新距离值
                nextVert.setDistance(newDist)
                # 更新返回路径
                nextVert.setPred(currentVert)
                # 更新优先队列
                pq.decreaseKey(nextVert, newDist) O(|E|logv)
        #总的复杂度： O((|v|+|E|)logv)


G = Graph()
ndedge = [('u', 'v', 2), ('u', 'w', 5), ('u', 'x', 1),
          ('v', 'x', 2), ('v', 'w', 3), ('x', 'w', 3),
          ('x', 'y', 1), ('w', 'y', 1), ('w', 'z', 5),
          ('y', 'z', 1)]
for nd in ndedge:
    G.addEdge(nd[0], nd[1], nd[2])
    G.addEdge(nd[1], nd[0], nd[2])
start = G.getVertex('u')
dijkstra(G, start)
print(G)
```
### 10.10 图的应用：生成最小树
>* 信息的广播：最小权重的生成树（拥有图中所有的顶点和最少数量的边以保持联通的子图）
>* 最小生成树T：包含所有顶点v，以及e的无圈子集，并且边权重之和最小
>* 贪心策略 prim：安全添加边
```python
from pq import PriorityQueue, Graph, Vertex

# 最小生成树prim算法
# G - 无向赋权图
# start - 开始节点
# 返回从开始节点创建最小生成树
def prim(G, start):
    pq = PriorityQueue()  # 创建优先队列
    start.setDistance(0)  # 起点最小权重代价设置为0，其它节点最小权重代价默认maxsize
    # 将节点排入优先队列，start在最前面
    pq.buildHeap([(v.getDistance(), v) for v in G])
    while not pq.isEmpty():
        # 取距离*已有树*最小权重代价的节点出队列，作为当前节点
        # 当前节点已解出最小生成树的前驱pred和对应最小权重代价dist
        currentVert = pq.delMin()
        # 遍历节点的所有邻接节点
        for nextVert in currentVert.getConnections(): #检查在树里的节点所连接的最小权重边
            # 从当前节点出发，逐个检验到邻接节点的权重
            newCost = currentVert.getWeight(nextVert)
            # 如果邻接节点是"安全边"，并且小于邻接节点原有最小权重代价dist，就更新邻接节点
            if nextVert in pq and newCost < nextVert.getDistance(): # 检查是否在安全添加的边里
                # 更新最小权重代价dist
                nextVert.setPred(currentVert)
                # 更新返回路径
                nextVert.setDistance(newCost)
                # 更新优先队列
                pq.decreaseKey(nextVert, newCost)


G = Graph()
ndedge = [('A', 'B', 2), ('A', 'C', 3), ('B', 'C', 1),
          ('B', 'D', 1), ('B', 'E', 4), ('C', 'F', 5),
          ('D', 'E', 1), ('E', 'F', 1), ('F', 'G', 1)]
for nd in ndedge:
    G.addEdge(nd[0], nd[1], nd[2])
    G.addEdge(nd[1], nd[0], nd[2])
start = G.getVertex('A')
prim(G, start)
print(G)

G = Graph()
ndedge = [('v1', 'v2', 6), ('v1', 'v3', 1), ('v1', 'v4', 5),
          ('v2', 'v3', 5), ('v3', 'v4', 5), ('v2', 'v5', 3),
          ('v3', 'v5', 6), ('v3', 'v6', 4), ('v4', 'v6', 2),
          ('v5', 'v6', 6)]
for nd in ndedge:
    G.addEdge(nd[0], nd[1], nd[2])
    G.addEdge(nd[1], nd[0], nd[2])
start = G.getVertex('v1')
prim(G, start)
print(G)
```
### 10.10 小结
>* BFS：解决无权图最短路径的问题 （队列）
>* Digkstra：解决带权图最短路径（优先队列）
>* DFS：回溯
>* 强连通分支（简化图），拓扑排序（关联任务排序）
>* 最小树生成（prim）：广播；和Digkstra相似，但是是贪心算法
