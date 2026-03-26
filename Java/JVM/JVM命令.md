1. **-Xmx**
	用于设置**堆内存的最大值**，即 JVM 运行时堆内存可以扩展到的最大上限。
	通常为物理内存的四分之一
2.  **-Xms**
	用于设置**堆内存的初始值**，即 JVM 启动时分配的堆内存大小。
	通常为物理内存的 1/64，但小于 1GB。

标准参数（`-X` 开头）和高级参数（`-XX` 开头）

**`-Xss<size>`**：设置每个线程的栈大小（默认 1MB）。如果线程较多或递归调用较深，可以适当增大。


1. **选择垃圾回收器**
    - **`-XX:+UseSerialGC`**：使用串行垃圾回收器（适合单线程环境）。
    - **`-XX:+UseParallelGC`**：使用并行垃圾回收器（适合多线程环境，吞吐量优先，默认回收器）。
    - **`-XX:+UseConcMarkSweepGC`**：使用 CMS（Concurrent Mark-Sweep）垃圾回收器（低延迟场景）。
    - **`-XX:+UseG1GC`**：使用 G1（Garbage First）垃圾回收器（Java 9 之后的默认回收器，适合低延迟场景）。
    - **`-XX:+UseZGC`**：使用 ZGC（低延迟、高吞吐量，适合大内存场景）。
    - **`-XX:+UseShenandoahGC`**：使用 Shenandoah GC（低延迟垃圾回收器）。
2. **GC 日志**：
    
    - **`-XX:+PrintGC`**：打印 GC 信息（已废弃，建议使用 `-Xlog`）。
    - **`-Xlog:gc`**：打印 GC 日志。
        
        复制
        
        `java -Xlog:gc MyApp`
        
    - **`-Xlog:gc*:file=gc.log:time,uptime,level,tags`**：将 GC 日志输出到文件。
        
        复制
        
        `java -Xlog:gc*:file=gc.log:time,uptime,level,tags MyApp`