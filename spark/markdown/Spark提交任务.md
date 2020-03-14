Spark Standalone 

```sh
$$SPARK_HOME/bin/spark-submit --master spark://node1:7077 --class  org.apache.spark.examples.SparkPi ../lib/spark-examples-2.4.4.jar 100
```