# Frequenty Asked Questions 
Imagenet with Hadoop 

## What is Imagenet 
[image-net.org](http://www.image-net.org/)


## What is the project  ?
[ Large Scale Visual Recognition Challenge 2017 (ILSVRC2017)](http://image-net.org/challenges/LSVRC/2017/index)


## Can you break it down for me here ?
We have to attempt to learn how to create ML models that can be used for real world scenarios. Since the data is Image based this about helping computers learn and see what we see. 

Generically and from the deloper point of view 
automate end to end pipeline. i.e. the following tasks need to be automated 
1. given the data , 
2. and some scripts, 
3. deploy hadoop (custom setup), 
4. transform data in hadoop , 
5. train a model 
6. test the model.
7. save the results(model, test-results) 
8. destroy hadoop.

Focus on automation would allow us to save significant amout of time on this project and would also give us skills for future.

## So it is vision ML problem ?
Yes and no. 
Yes it a vision problem because we are going to deal with images mostly 
No it is not just a vision problem because the matshs behind any ML is widely applicable.

Basically becasue we are infants in this fields we are starting with a well defined and well supported problem with adequate scope to deep dive on.


## Can we run ML algos on Hadoop  ? 
Yes , We there are several projects that allow for running ML algos on hadoop , Apache Mahout , H20 , spark , and we can have our own custom solutions as well.
Initially we believed that we would use Hadoop only for data trasnforming but now we know about tese existing tools we don't need to limit our thinking here 

## Do you mean  all ML should be done on hadoop ?

No , Hadoop is primarity the data storage and transformation system for us. We are free to transfrorm data with hadoop and then take the o/p and train seprately from hadoop.


## Why do we want to use shells for interating with hadoop 
Programmability from the start, i.e. We are from the very beginning faimialr with tools that allow us to automate things. Remever we have too little time allotted to thei project as it is.

However this does not mean we should disown UI solutions. It is the IDE like environment that actually makes the shell interaction more usable(think RStudio)The shells we currently used were no more than commandline prompts 

Although we don't yet know the IDEs that can allow us to use shells for hive , hbase , spark but we believe there would be a lot , we just need to discover them.


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


## Why hadoop ?
Open source , industry standard , great community support , portable skills , Insane amout of scenarios supported , fast and faster ....

Hadoop is the most versatile system for any big data related tasks. In any ML problem more than 80% time gets spent on transforming data in to something usable by set of model. i.e. when we are not even dealing with big data. 

As we go forward in ML it is important to have skills in big data ( defacto hadoop) and then we have better chances of being a successful ML practitioner. So lets get our tools going.


## Deadline 

Mid november to get friendlier with hadoop technologies and be able to do some rudimentary machine learning tasks. 

 
## Where are the hadoop binaries?

* /user/hdp/

