# week2
执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms128m -Xmx128m GCLogAnalysis
堆内存执行了多次Full GC 并且最后发生了OOM，大概16毫秒发生一次youngGC
执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms512m -Xmx512m GCLogAnalysis
没有OOM，，大概44毫秒发生一次youngGC，
执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms1g -Xmx1g GCLogAnalysis
没有OOM，，大概100毫秒发生一次youngGC，
执行 java -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseSerialGC -Xms2g -Xmx2g GCLogAnalysis
没有OOM，，大概280毫秒发生一次youngGC，
随着堆内存的增大，GC频率变低，GC次数也变低，但是GC暂停时间变长。
