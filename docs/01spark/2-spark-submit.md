# Spark-submit命令
Spark-submit命令在Spark bin文件夹下，用于启动集群上的应用。 它使用统一的提交接口支持各种类型的集群服务器， 这样你你就不必为每种类型都配置自己的应用。

# 命令行参数
使用命令行参数的主要原因是避免将值硬编码到代码中。
```
./bin/spark-submit \
  --class <main-class> \
  --master <master-url> \
  --deploy-mode <deploy-mode> \
  --conf <key>=<value> \
  ... # other options
  <application-jar> \
  [application-arguments]
```
下面是我的一个实际的例子：
```
spark-submit \
  --master yarn \
  --deploy-mode client \
  --executor-cores 2 \	
  --executor-memory 20g \
  --conf spark.driver.memory=12g  \
  --conf spark.executor.memoryOverhead=512 \
  --conf spark.driver.memoryOverhead=512  \
  --conf "spark.executor.extraJavaOptions=-XX:MaxPermSize=256m -XX:+PrintGCDetails -XX:+PrintGCTimeStamps" \
  --conf spark.network.timeout=30000  \
  --conf spark.executor.instances=100  \
  --class main.scala.com.WordCount \ 
  wordCount-1.0-SNAPSHOT.jar ${TX_DATA}
```
参数|参考值|说明|备注
-|-|-|-
--master|local<br>local[1]<br>local[*]<br>spark://hduser:7077<br>yarn<br>yarn-client<br>yarn_cluster|Spark 应用运行位置|--master yarn-client<br>等同于<br>--master yarn --deploy-mode client
--deploy-mode|client<br>cluster|部署模式：client模式下，driver运行在本地作为外部客户端；cluster模式下，driver运行在集群节点。场景：client模式适用于交互式和调试用途，希望立刻看到应用的输出；在生产作业中使用cluster模式。默认值为client模式
--class|org.apache.spark.examples.SparkPi|对于java和scala应用程序，写包含main方法的全路径类名
--conf||key-value格式的spark配置属性
