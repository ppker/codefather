## Java 并发库中提供了哪些线程池实现？它们有什么区别？
> 八股文一网打尽，更多面试题请看[程序员面试刷题神器 - 面试鸭](https://www.mianshiya.com/)


## 回答重点

Java 并发库中提供了 5 种常见的线程池实现，主要通过 `Executors` 工具类来创建。

1）**FixedThreadPool**：创建一个固定数量的线程池。

线程池中的线程数是固定的，空闲的线程会被复用。如果所有线程都在忙，则新任务会放入队列中等待。

适合负载稳定的场景，任务数量确定且不需要动态调整线程数。

2）**CachedThreadPool**：一个可以根据需要创建新线程的线程池。

线程池的线程数量没有上限，空闲线程会在 60 秒后被回收，如果有新任务且没有可用线程，会创建新线程。

适合短期大量并发任务的场景，任务执行时间短且线程数需求变化较大。

3）**SingleThreadExecutor**：创建一个只有单个线程的线程池。

只有一个线程处理任务，任务会按照提交顺序依次执行。

适用于需要保证任务按顺序执行的场景，或者不需要并发处理任务的情况。

4）**ScheduledThreadPool**：支持定时任务和周期性任务的线程池。

可以定时或以固定频率执行任务，线程池大小可以由用户指定。

适用于需要周期性任务执行的场景，如定时任务调度器。
   
5）**WorkStealingPool**：基于任务窃取算法的线程池。

线程池中的每个线程维护一个双端队列（deque），线程可以从自己的队列中取任务执行。如果线程的任务队列为空，它可以从其他线程的队列中“窃取”任务来执行，达到负载均衡的效果。

适合大量小任务并行执行，特别是递归算法或大任务分解成小任务的场景。

## 扩展知识

### **不同线程池的选择总结**：
- **FixedThreadPool** 适合任务数量相对固定，且需要限制线程数的场景，避免线程过多占用系统资源。
- **CachedThreadPool** 更适合大量短期任务或任务数量不确定的场景，能够根据任务量动态调整线程数。
- **SingleThreadExecutor** 保证任务按顺序执行，适合要求严格顺序执行的场景。
- **ScheduledThreadPool** 是定时任务的最佳选择，能够轻松实现周期性任务调度。
- **WorkStealingPool** 适合处理大量的小任务，能更好地利用 CPU 资源。




> 八股文一网打尽，更多面试题请看[程序员面试刷题神器 - 面试鸭](https://www.mianshiya.com/)