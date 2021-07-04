# 对于串行GC
- 执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms128m -Xmx128m GCLogAnalysis
- 堆内存执行了多次Full GC 并且最后发生了OOM，大概16毫秒发生一次youngGC
- 执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms512m -Xmx512m GCLogAnalysis
- 没有OOM，，大概44毫秒发生一次youngGC，
- 执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms1g -Xmx1g GCLogAnalysis
- 没有OOM，，大概100毫秒发生一次youngGC，
- 执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms2g -Xmx2g GCLogAnalysis
- 没有OOM，，大概280毫秒发生一次youngGC，
- 随着堆内存的增大，GC频率变低，GC次数也变低，但是GC暂停时间变长。

# 对于并行GC，得出同样的结论

# 对比串行和并行GC，执行一下两条语句
- java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms512m -Xmx512m GCLogAnalysis
- java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseParallelGC -Xms512m -Xmx512m GCLogAnalysis
# 串行GC生成对象次数：8495，发生5次fullGC；并行GC生成对象次数：7307次，发生8次fullGC
# 将堆内存设置成4g
# 串行生成对象次数：8193，没有fullGC；并行GC生成对象次数：11820，没有FullGC。在堆内存较大时，并行GC提高了吞吐量
# 将GCLogAnalysis的执行时间延长，从1秒改成8秒，再执行以下语句
- java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms512m -Xmx512m GCLogAnalysis
- java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseParallelGC -Xms512m -Xmx512m GCLogAnalysis
# 串行GC下生成对象次数：48445次，并行GC下生成对象次数：25342次
# 将堆内存设置为4g
# 串行GC生成对象次数：130336次；并行GC生成对象次数：144505
# 将堆内存设置为10g
# 串行GC下生成对象次数：158304次；并行Gc生成对象次数：171554次；
# 并行GC虽然能够提高吞吐量，但是效果并不明显，而且在堆内存比较小的情况下，吞吐量甚至不如串行GC

