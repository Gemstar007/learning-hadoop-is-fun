## MapReduce Investigation Summary (ongoing)
Goal to be able to trasfrom an image

### Status Summary 
Currently We have not yet figured out how to read an image and use an external library in hadoop context. However we are not blocked. 

It was supposed to be straightforward , but apparently it is not so. Several assumptions have been challenged in this investigation I am adding the summary from me and Ruchi below regardign the attempts


#### The succeeded investigations in this direction are 
* Hdoop streaming works (very well for text) , but it is not what we need for Images
* Ruchi is able to use a Imagemagick jar with python outside of hadoop context. She tried using streaming but of course it didn't work.
* We think we have figured out how to specify third party libraries to hadoop , but we have to verify that with end 2 end scenario (-libjars)


#### Issues

* Python , there are a few frameworks that can work in python top being pydoop, mrjava , we read through them but both donot seem to be providing the solutions out of box. 
* all the documentation that we came across uses mostly hadoop-streaming which is not useful in image context
* the best hadoop documentations here were based on java and not on python

#### Is images possible then ?
Yes, yes, yes. But not simply.

In java world they have created generic interfaces for everything hadoop (specificiations). and there are a lot of ope source implementations of these (lego bricks) that we can pick and chose from to create our scenario

e.g. we will store images in HAR (Shazia's current recommendation) and index in hive, based on the requirements we can read images using a custom reader and store them in avro file format which apparently works with binary data, think of cosmos structured stream with binary data column. 
Then once we have the suitable image packets created for our investigation we would read and transform them using image processing libraries. 

Once we understand the process we will work on simpifyin/abstracting it as well by organizing these tools and attempting to use python/scala etc for programmability


#### Directions 
* We need to invest in java too, till we understand the hadoop ropes.
* Understand all the apis around MapReduce. 
* hbase may not be a useful solution, instead avro,har seems the one we should go with 
* Pig latin seems useful in this the avro/har context . It should be like SCOPE 

## Java/hadoop investigations so far 
* We can write hadoop MR jobs in java now , reading text files without streaming them
* We understand the api structure engough to proceed. 
* We were able to use avro outside hadoop context
* Using avro within hadoop seems to be suffering from dll-hell problem

## Very useful link 
* [MapReduce tutorial on apache website](cd https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html)











