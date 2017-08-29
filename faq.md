# Frequenty Asked Questions 
Imagenet with Hadoop 


## Can we run ML algos on Hadoop  ? 
Yes , We there are several projects that allow for running ML algos on hadoop , Apache Mahout , H20 , spark , and we can have our own custom solutions as well.
Initially we believed that we would use Hadoop only for data trasnforming but now we know about tese existing tools we don't need to limit our thinking here 


## Why do we want to use shells for interating with hadoop 
Programmability from the start, i.e. We are from the very beginning faimialr with tools that allow us to automate things. Remever we have too little time allotted to thei project as it is.
HOwever this does not mean we should disown UI solutions. The shells we currently used were no more than commandline prompts , it is the IDE like environment that actually makes the shell interaction more usable(think RStudio). Althout we don't yet know the IDEs that can allow us to use shells for hive , hbase , spark but we believee there would be a lot , we just need to discover them.


## How will we store these images in Hadoop ?
We don't have the exact answer, to begin with limiations here is that big-data systems like to work with big files e.g. the min file size for hadoop is generally cofigured to be 128 MB, comparabably our iamges are going to be just in KBs. We can surely stre them as-si but every image will be padded to 128 MB size which is alot of waste. 

So there are atleast two ways that we can store images 
1. Create bundles of images (similar to tar files) and keep them in hdfs. 
2. store individual images in hbase as blob. Hive will eventually be storing them in hdfs but is more suitable to handle small files.

In both these cases the metadata about the images e.g. this image conatins a building at this location needs to be stored separately. For this we are currently thinking of using Hive (Sql) 

So the index of images is readily queriable and once we know which images we need from the index, we can pull them from packets/hbase in the next step adn do the required transformations

## How we do we manipulate image data ?

Since the programmability is mostly in python (or java) we can use the libraries which have binding for these languages. The assumption is that whatever works on your desk should also work in hadoop given suitable setup.

Some good libraries we already know about are 
1. OpenCV , apparently it should work with hadoop 
2. ImageMagick it has bindings for most programmign languages so hoepfully it would work too.

## Great how to proceed now ?
Currently we are learning the ropes of hadoop and attempting to create helloworld docs for each of the technologies we are interested in e.g. hive, hbase , spark are done. We stil lneed to do map-reduce , sqoop , flume which we are working on. 

After those there are scenarios that we want to accomplish ( not a complete list and not in order of priority)
1.  How do process an image in hadoop environment
2. how do we store images in hadoop , efficiently and with flexibility. 
3. How do we create credentials in hadoop.  
4. How do we get a repeatble hadoop deployment 
5. ....





## But what i am really supposed to do ?

Chose what you like the most and do it or talk to us to help ensure best use of your time. You can also propose ans specific scenario/tool etc we should work on and we will add it to the list. 

Suggestion here is to take ownership of a small item ( say which less than 4-6 hours of effort) and finish it before moving on to the next. 




 


