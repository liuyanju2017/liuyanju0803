1，HDFS中，假设数据块有3个副本，则它们的存放策略为（）：
A．	存放元信息的namenode和存放数据块的3个datanode分别位于不同的机架
B．	存放元信息的namenode和存放数据块的1个datanode位于同一个机架,，其他两个datanode位于同一个机架
C．	存放元信息的namenode位于一个机架，存放数据块的3个datanode位于另外一个机架。

答案：B
解析：当datanode和namenode存放在一个节点或机架上时，可以减少他们之间的命令运行时间，所有datanode和namenode设置在同一机架上。另外，两个不同机架上的两个节点同时出现故障的概率要远远小于同一个机架上两个节点处故障的概率，所以另外两个节点设置在另外的机架上。

2，HDFS的特点有：
A.	通过数据在硬件上的冗余操作，可以有效的实现容错
B.	数据一次写入多次读取，可以对数据进行后续的修改
C.	数据一次写入多次读取，不可以对数据进行后续的修改
D.	只适合存储大文件
E.	可以存储各种文件，包括大文件和小文件
F.	适合数据批量读写，吞吐量高
G.	不适合交互应用，低延迟很难满足

答案：ACDFG
解析：在HDFS中，数据只允许一次写入，而不允许进行修改。另外HDFS适合存储大文件，而不适合存储小文件。

3，HDFS中存放数据的最小单位是（）
A.	文件
B.	Block
C.	目录
D.	Split

答案：B 
解析：在HDFS中，存放数据的最小单位为BLOCK.

4，MapReduce中最小的计算单元是：
A.	block
B.	split
C.	文件
D.	一个目录
答案：B
解析，在MapReduce计算中的最小单位为split.


5，在hadoop2.0及以后的版本中，系统默认数据块的最大值为128M。现有两个个文件，大小分别为130M和2M，则存放在HDFS中的数据块的个数及大小分别为：
A．2个,130M，2M
B．2个，66M，66M
C.  2个，128M，4M
D．3个，128M，2M，2M

   答案：D
   解析:HDFS中存储的最小单位为block，2.0版本之后系统默认数据块的最大值为128M，当一个数据块的大小大于128M时，进行切割，当小于128M时，以实际大小为准。另外，一个数据块只能存放一个文件。

6，以下节点中可以做客户端有：
A．	namenode
B．	datanode
C．	非namenode和非datanode的其他节点

答案：ABC
解析：namenode和datanode都可以作为客户端来使用。

7，对应一个mapreduce的job，其运行过程有（）
A．	分割任务并输入（input split）
B．	各自进行统计（map过程）
C．	交换过程（shuffle）
D．	再次统计（reduce过程）
E．	筛选出结果并输出（output输出）

答案：ABCDE

8，JobTracker的角色有（）
A．	作业调度。对客户端提交的作业安装某些规则比如先到先服务或公平调度器原则进行调度
B．	对tasktracker进行任务分配，并监控TaskTracker的任务执行进度
C．	监控TaskTracker的状态
D．	执行部分tasktracker的任务

答案:ABC

9， MapReduce运行的容错机制有：
A．	重复执行，当一个执行的任务出现错误时，就重复执行，当达到最大执行次数是停止执行
B．	推测执行。一般情况下，只有map端的TaskTracker任务都执行完时，才会启动reduce端的TaskTracker。在map端的几个TaskTracker中，如果某个TaskTracker执行任务过慢，则再启动另外一个TaskTracker执行相同的任务。尔后查看当一个TaskTracker执行完就终止另外一个TaskTracker，并且使用执行完任务的TaskTracker的结果。

答案：AB

10，客户端向HDFS中写入数据库的方式：
A．	客户端根据namenode提供的datanode的信息，分别向各个datanode写入数据块
B．	客户端根据namenode提供的datanode的信息，先向一个datanode写入数据块，然后通过这个datanode再向其他datanode写入数据块
C．	客户端先向namenode写数据，然后通过namenode分别向各个datanode写入数据
D．	客户端先向namenode写数据，然后通过namenode先向一个datanode写入数据块，然后通过这个datanode再向其他datanode写入数据块

答案：B
解析：当向HDFS写数据时，首先会依次向一个datanode顺序写入，同时已写入数据的datanode依次顺序向其他指定的datanode进行数据写入。这样可以降低客户端和HDFS之间的传输带宽压力。

11，MapRduce的特点有哪些（）
A．	易于编程。通过map函数和reduce函数就可以实现一个分布式的作业。
B．	良好的扩展性。
C．	高容错性。有高效的软硬件容错机制。
D．	适合PB级以上海量数据的离线处理。
E．	可以上实现高效的实时计算。
答案：ABCD
解析：HDFS存储海量的数据，不能实施实时查询。

12，MapReduce将作业的整个运行过程分成（）阶段和（）阶段。
A.	Map阶段
B.	Reduce阶段
C.	输入阶段
D.	输出阶段

答案：AB
解析：MapReduce将作业的整个运行过程分成Map阶段和Reduce阶段。map阶段有一定数量的maptask组成。Maptask也有一定的输入和输出，它的输入是inputFormat，InputFormat负责获取切片，并把数据交给mapper处理，然后由partitioner按照key值分发给相关的reducer。Reduce阶段也有一定的ReduceTask组成。ReduceTask接收到partitioner的分发数据后，按照key值进行排序和整合，经过Reducer处理后通过OutputFormat输出。

13，在inputFormat分段过程中，假如一行数据被截断了，那么：
A．	前一个split读取此行的内容，后一个split不读取此行的内容
B．	前一个split不读取此行的内容，后一个split读取此行的内容
C．	前后两个split均读取此行内容
D．	前后两个split均不读取此行内容

答案：A
解析：在inputFormat分段过程中，假如一行数据被截断了，那么前一个split读取此行的内容，后一个split不读取此行的内容。这样既不多读数据也不会少读数据。

14，关于combiner的说法，以下正确的是
A．	combiner的逻辑位置位于mapper和partitioner之间
B．	combiner可以减少maptask输出的数据量
C．	combiner可以减少reduce-map网络传输的数据量
D．	结果叠加和对结果求平均值均可使用combiner

答案：ABC
解析：只有结果叠加的才可以使用combiner。求平均值不能使用combiner。

15，在hadoop2.0及后续的版本中，关于MRAppMaster的说法，以下正确的是：
A．	负责资源的管理
B．	任务划分
C．	资源申请并将之二次分配给mapTask和ReduceTask
D．	任务状态监控和容错管理

答案：BCD
解析：在hadoop2.0及后续版本中，资源的管理由YARN负责完成。

16，HDFS采用master-slave架构，其master和slave分别对应以下的节点：
A.	namenode datanode
B.	datanode namenode
C.	datanode datanode
D.	namendoe namenode

答案：A
解析：在HDFS中，采用主从结果，其中master指的是namenode，slave指的是datanode。

17，HDFS的可靠性策略有：
A．	文件的完整性。如果一个副本的文件有损坏，则用其他的副本进行取代。
B．	Datanode定期向namenode返回heartbeat，当一定时间内没有返回心跳，namenode认为此datanode处于死亡状态，namenode启动其他节点作为副本datanode。

答案：AB

18，关于active namenode和standby namenode的说法，以下正确的是：
A．	active namenode处于active状态，standby namenode处于standby状态，只有active namenode才能对外提供服务。
B．	active namenode处于active状态，standby namenode 处于standby状态，两台都能对外提供服务。
C．	active namenode处于active状态，standby namenode处于standby状态，只有standby  namenode才能对外提供服务。
D．	active namenode处于active状态，standby namenode 处于standby状态，两台都不能对外提供服务。

答案：A

19，datanode的主要功能有：
A.	存储数据块。每个块对应一个元数据的数据信息文件。这个文件主要描述这个块属于哪个文件、第几个块等信息。
B.	启动datanode线程时时会向namenode汇报其数据块信息。
C.	通过向namenode发送心跳保持与其联系，如果在一定时间内，namenode没有收到datanode的心跳，则认为其已经lost，并将其上的数据块复制到其他dataNode上。

答案：ABC

20，HDFS无法高效存储大量小文件，想让它能处理好小文件，比较可行的改进策略不包括  
A．利用SequenceFile、MapFile、Har等方式归档小文件  
B．多Master设计  
C．Block大小适当调小  
D．调大namenode内存或将文件系统元数据存到硬盘里 
	
答案：D
   解析：存储大量小文件会消耗大量的寻道时间。另外存储一个数据块的元信息大概需要156B的内存开销，也就是说无论存储文件的大小如何，总会有156B的内存开销。所以存储小文件占用的内存消耗较大，HDFS中尽量存储大文件，或者调大namenode内存或将文件系统元数据存到硬盘里。
