---

title: E-MapReduce Survey
date: 2017-07-11

---


# E-MapReduce 

## Log Service
https://help.aliyun.com/document_detail/28121.html?spm=5176.doc28131.6.624.kaZ3L5
###  Direct API Based DStream (Log Service)
```
    val logServiceProject = args(0)
    val logStoreName = args(1)
    val loghubConsumerGroupName = args(2)
    val loghubEndpoint = args(3)
    val accessKeyId = args(4)
    val accessKeySecret = args(5)
    val batchInterval = Milliseconds(args(6).toInt * 1000)
    val zkConnect = args(7)
    val checkpointPath = args(8)
    def functionToCreateContext(): StreamingContext = {
      val conf = new SparkConf().setAppName("Test Direct Loghub Streaming")
      val ssc = new StreamingContext(conf, batchInterval)
      val zkParas = Map("zookeeper.connect" -> zkConnect, "enable.auto.commit" -> "false")
      val loghubStream = LoghubUtils.createDirectStream(
        ssc,
        logServiceProject,
        logStoreName,
        loghubConsumerGroupName,
        accessKeyId,
        accessKeySecret,
        loghubEndpoint,
        zkParas,
        LogHubCursorPosition.END_CURSOR)
      ssc.checkpoint(checkpointPath)
      val stream = loghubStream.checkpoint(batchInterval)
      stream.foreachRDD(rdd => {
        println(rdd.count())
        loghubStream.asInstanceOf[DirectLoghubInputDStream].commitAsync()
      })
      ssc
    }
    val ssc = StreamingContext.getOrCreate(checkpointPath, functionToCreateContext _)
    ssc.start()
    ssc.awaitTermination()
```
## Spark Steaming
### Output Operations on DStreams
Output operations allow DStream’s data to be pushed out to external systems like a database or a file systems. Since the output operations actually allow the transformed data to be consumed by external systems, they trigger the actual execution of all the DStream transformations (similar to actions for RDDs). Currently, the following output operations are defined:
| Output Operation | Meaning |
|----------|-----------|
|foreachRDD(func)	|The most generic output operator that applies a function, func, to each RDD generated from the stream. This function should push the data in each RDD to an external system, such as saving the RDD to files, or writing it over the network to a database. Note that the function func is executed in the driver process running the streaming application, and will usually have RDD actions in it that will force the computation of the streaming RDDs.|

### A typical way to write data (we will use OTS)
```
dstream.foreachRDD(new VoidFunction<JavaRDD<String>>() {
  @Override
  public void call(JavaRDD<String> rdd) {
    rdd.foreachPartition(new VoidFunction<Iterator<String>>() {
      @Override
      public void call(Iterator<String> partitionOfRecords) {
        // ConnectionPool is a static, lazily initialized pool of connections
        Connection connection = ConnectionPool.getConnection();
        while (partitionOfRecords.hasNext()) {
          connection.send(partitionOfRecords.next());
        }
        ConnectionPool.returnConnection(connection); // return to the pool for future reuse
      }
    });
  }
});
```

## DataV
https://help.aliyun.com/document_detail/53844.html?spm=5176.doc54010.6.542.WiEsll
### Support Input Data Souce
* RDS for MySQL
* RDS for PostgreSQL
* RDS for SQLServer
* Hybrid DB
* TableStore
* Oracle
* 兼容MySQL数据库