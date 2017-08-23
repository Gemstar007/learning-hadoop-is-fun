# Hive (hdp sandbox)

This is a basic example of hive focussing on connecting with hdp sandbox and trying out simple commands in programmatic fashion. Once the basic connectivity is learnt , we are expected to use online sources for deeper understading. 

## Prerequisites 

* Hdp sandbox is running
* sandbox-ip 
* sandbox-credendital

##Optional :
(if you want to perform update and delete operations)
Before doing hive operations make some changes:

1.Log in to Ambari using user credentials raj_ops/raj_ops.

2.Enabling Hive ACID is simple: Ambari -> Hive -> Configs. Set ACID Transactions to On.

3.Set hive.enforce.bucketing to true and save changes.

4.restart all the affected services.


## Setup

* ssh to sandbox-ip:2222 (10.137.174.204:2222)
* use the sandbox-credentials
* Create a test user folder on sandbox (say sankalpg)
* cd sankalpg 
* Create a file with few lines e.g. student.txt with 3 lines with your favorite editor
	* 101 dev 30 Kirkland 
	* 202 anto 18 seattle
	* 303  rango 33 redmond
	

## Hands on 
Although we can use the hive shell now ( command "hive") but we will use the use hive directly from bash to be able to write queries later


```bash
#create a folder on the hadoop filesystem , this is different filesystem from the sandbox filesystem
hdfs dfs -mkdir /user/student

#create a new table in hive ( it takes 5-10 seconds to run the command in this mode)
hive -e "CREATE TABLE STUDENT ( STD_ID INT, STD_NAME STRING, AGE INT, ADDRESS STRING );"           

#load data from the local-fs to hive tables

hive -e "load data local inpath '/root/sankalpg/student.txt' into TABLE STUDENT;"

                   OR

#Insert rows in created table(optional)

hive -e "INSERT INTO TABLE STUDENT VALUES (101,'DEV',30,'KIRKLAND'),(102,'ANTO',18,'29 SEATTLE'),(103,'RANG',23,'34 REDMOND');"


# select from the newly created table
hive -e "select * from STUDENT;"

#upate hive table

hive -e  "update STUDENT
SET std_id=110
WHERE std_id=101;
"
#delete hive table
hive -e  " DELETE FROM STUDENT
where std_id=110;
"

# drop table when you are done
hive -e "drop table STUDENT;"

```

## Resources 

 * [Apache Hive Manual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)
* https://hortonworks.com/tutorial/using-hive-acid-transactions-to-insert-update-and-delete-data/

 * --Add more as appropriate--
 