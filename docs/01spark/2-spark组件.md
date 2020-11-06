# Driver Program
运行Application的main()函数并创建SparkContext。

Driver负责**将Spark应用程序转换为称为tasks的较小的执行单元**，然后和集群管理器安排它们在executors上运行。Driver还负责执行Spark应用程序，并将结果/状态返回给用户。

Driver包含各种组件：
- DAGScheduler
- TaskScheduler
- BackendScheduler
- BlockManager

Driver特性：
- 存储RDD及其分区的元数据。
- 在用户将Spark应用发送到集群管理器（YARN）后创建
- 优化DAG转换
- 创建Spark WebUI

# Application master
ApplicationMaster是特定于框架的实体，负责与ResourceManager协商资源，并与NodeManager一起执行和监视应用程序任务。集群上运行的每个应用程序都有自己的专用Application Master实例。

在集群部署模式下，当用户使用spark-submit提交Spark应用程序时，会在同一节点上同时创建Spark Master和Driver。

Driver把executor的需求通知给Application Master，后者与资源管理器协商资源来托管executor。

# Spark Context
Spark Context是Spark功能的主要入口点，是Spark应用程序的核心。它允许Driver通过集群管理器访问集群，用来在集群上创建RDD、累加器和广播变量。
当用户首次提交时，Spark驱动程序会为每个Spark应用程序创建Spark Context。它存在于Spark应用程序的整个生命周期中。

# 