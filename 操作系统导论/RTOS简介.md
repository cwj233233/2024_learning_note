# RTOS简介

实时操作系统（Real-time operating system, RTOS），它会按照排序运行、管理系统资源，并为开发应用程序提供一致的基础。与一般的操作系统相比，最大的特色就是**实时性**，如果有一个任务需要执行，实时操作系统会马上（在较短时间内）执行该任务，不会有较长的延时。这种特性保证了各个任务的及时执行。   

---

## 一、定义

实时操作系统（Real-time operating system, RTOS）有以下三个**特性**：
* 有限时间
* 处理信息
* 受外界刺激（对输入作反应）

## 二、触发

**Event or Time-driven Systems**  

* Time-triggered依时间触发: computation is triggered by the passage of time.
* Event-triggered依事件触发: computation is triggered by an external or internal event.

1. **Periodic（周期）**：if there is a bound on the minimum arrival interval of the event.
   如果事件的最小到达间隔有界。
2. **Sporadic（偶发）**：if the minimum arrival interval between events has random jitter.
   如果事件之间的最小到达间隔有随机抖动。（偶发事件可能随时发生，但两次连续事件之间至少必须间隔T个时间单位。）
3. **Aperiodic（无周期）**：if there is no such bound.
   如果没有这样的界限。（无周期任务的到达时间不规则。）

##  三、截止时间

Operating with Response Time Constraints（在响应时间内完成）

1. **A Hard Deadline（硬截止期）**：
   - 必须始终按时完成，不然系统失败/崩溃。
   - Must always be met since failure to do so will result in failure of the entire system.


2. **A Firm Deadline（确定截止期）**：
   - 必须始终按时完成，不然系统输出错误答案。
   - May be missed, but if so, then the result is useless.


3. **A Soft Deadline（软截止期）**：
   - 偶尔会错过，尽管不愿发生但不会出大问题。
   - May be missed occasionally (although late completion is undesirable).


##  四、并发

1. **Inherently parallel（固有并行性）**：
   - Lots of different things can be happening at the same time, so a real-time system may need to react to several different events at the same time.
   - 事件可能同时发生，系统同时处理。

2. **Non-deterministic（非确定性）**：
   - Events occur at unpredictable times, so a real-time system needs to deal with events as and when they happen.
   - 事件发生不可预测，要随时处理。

The operations carried out by a real-time system are called（实时系统执行的操作称为）：
   - **Tasks（任务）**
   - **Processes（进程）**
   - **Threads（线程）**

 同时处理这些叫做 **concurrency（并行）**

## 五、要求

General facilities required to program RTS（编写实时系统所需的要求）

### Task managementto run tasks concurrently（如何并行运行任务）

1. **Scheduling tasks（调度任务）**：
   - Deciding which task to run when
   - 决定何时运行哪个任务

2. **Memory management（内存管理）**：
   - Allow tasks to be stopped and resumed
   - 允许任务被暂停和恢复

3. **Inter-task communication and synchronization（任务间通讯和同步）**

### Resource managementto interface with environment（资源分配与外部交互）

1. **Real-time clock（实时时钟）**

2. **Input/Output（输入/输出）**

3. **Interrupt handling（中断处理）**

# RTS和RTOS

- RTS 是指整个实时系统，它包含硬件、软件和网络等多个组件，这些组件共同工作以满足实时约束。
- RTOS 是RTS中的一个重要软件组件，它负责管理实时任务和资源，确保系统按时完成任务。

---

## RTOS使用的技术

### 调度

运行状态（runing），大多数任务大部分时间都处于阻塞（block）或就绪（ready）状态，因为通常每个 CPU 内核一次只能运行一个任务。就绪队列中的项数可能会有很大差异，具体取决于系统需要执行的任务数和系统使用的调度程序类型。在更简单的非抢占式但仍然多任务处理的系统上，任务必须将其在 CPU 上的时间让给其他任务，这可能导致就绪队列具有更多处于准备执行状态的整体任务（资源匮乏）。

一些常见的**调度算法**：

- Cooperative scheduling 合作调度
- Preemptive scheduling 抢占式调度  
    - Fixed-priority pre-emptive scheduling 固定优先级抢占式调度
    - Fixed-Priority Non-preemptive Scheduling 固定优先级非抢占式调度
    - Static-time scheduling 静态时间调度
    - Round-robin scheduling 循环调度

- Earliest Deadline First approach 最早的截止日期优先方法
- Stochastic digraphs with multi-threaded graph traversal 具有多线程图遍历的随机二图
  
### 任务间通信和资源共享
<font color=#FF0000>我是红色</font>
像Unix这样的多任务操作系统在实时任务方面很差。计划程序为计算机上需求最低的作业提供最高优先级，因此无法确保时间关键型作业能够访问足够的资源。多任务处理系统必须管理多个任务之间的共享数据和硬件资源。两个任务同时访问相同的特定数据或硬件资源通常是不安全的。     

有三种常用方法可以解决此问题：  
1. **临时屏蔽/禁用中断（）**
2. **互斥**
3. **消息传递**