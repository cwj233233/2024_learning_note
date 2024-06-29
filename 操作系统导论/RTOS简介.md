# RTOS简介

实时操作系统（Real-time operating system, RTOS），它会按照排序运行、管理系统资源，并为开发应用程序提供一致的基础。与一般的操作系统相比，最大的特色就是**实时性**，如果有一个任务需要执行，实时操作系统会马上（在较短时间内）执行该任务，不会有较长的延时。这种特性保证了各个任务的及时执行。   

---

## 一、定义

实时操作系统（Real-time operating system, RTOS）有以下三个特性：
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

##  三、
