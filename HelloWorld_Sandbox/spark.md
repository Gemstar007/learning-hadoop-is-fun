# Spark (hdp sandbox)

## Prerequisites 

* Hdp sandbox is running
* sandbox-ip 
* sandbox-credendital

## Setup

* ssh to sandbox-ip:2222 (10.137.174.204:2222)
* use the sandbox-credentials
* if ipython is not already installed use 
   *  "sudo easy_install ipython==1.2.1"
* get test data 
   * wget https://raw.githubusercontent.com/ruchisahu/machine-learning/master/daily_weather.csv
* copy data to hdfs 
   * hdfs dfs -put ~/daily_weather /ruchi/daily_weather.csv


## Hands on 
start pyspark 

* PYSPARK_DRIVER_PYTHON=ipython pyspark

## Basic Commands



```bash

# Import random
data=[1,2,3,6,12,8,5,11]
random.shuffle(data)

d=sc.parallelize(data)
print(d)
#o/p ParallelCollectionRDD[1] at parallelize at PythonRDD.scala:475

d.count()
#o/p 8

d.take(3)
#o/p [11,5,12]


d.takeSample(False,3)
#[8,2,3]

d.first()

d.takeOrdered(3)
d.mean()
#o/p 6.0

 d_m=d.filter(lambda x:x>3)
print(d_m)
#o/p PythonRDD[9] at RDD at PythonRDD.scala:48



d_m.count()
#5
d_c=d_m.map(lambda x:(x-32)*5.0/9.0)

 print(d_c)
#o/p PythonRDD[11] at RDD at PythonRDD.scala:48
```

## Basic operation on weather dataset

```bash

df=spark.read.csv('/ruchi/daily_weather.csv',header=True)

df.columns

df.printSchema()
df.describe()
len(df.columns)

df.count()
removeAllDF=df.na.drop()

removeAllDF.describe(['air_temp_9am']).show()

for x in imputeDF.columns:
    meanValue=removeAllDF.agg(avg(x).first()[0]
    print(x,meanValue)
    imputeDF=imputeDF.na.fill(meanValue,[x])

imputeDF.describe(['air_temp_9am']).show()

```

## Resources 

* more on RDD programmming [rdd programming guide](https://spark.apache.org/docs/latest/rdd-programming-guide.html)

 