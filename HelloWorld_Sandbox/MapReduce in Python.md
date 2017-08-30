# MapReduce in Python

MapReduce programs are typically run in Java in Hadoop.  However, Hadoop and other packages provide other interfaces to do this.  

## Hadoop Streaming

This is a way of passing a Map python script and a Reduce python script, and have them connected by STDIN/STDOUT.  The following is how to execute a WordCount algorithm.

### Prerequisites 

* Hdp sandbox is running
* sandbox-ip 
* sandbox-credential
* Test content in /tmp/gutenberg (can be obtained from [here]( http://www.michael-noll.com/tutorials/writing-an-hadoop-mapreduce-program-in-python/))


### Setup

* ssh to sandbox-ip:2222 (10.137.174.204:2222)
* use the sandbox-credentials
* if ipython is not already installed use 
   *  "sudo easy_install ipython==1.2.1"
* copy test content to your user directory in HDFS with:
	* `hadoop dfs -copyFromLocal /tmp/gutenberg /user/username/gutenberg`

### Hands on 

MapReduce is composed of two programs - Map, and Reduce.  Copy this code to mapper.py:

```
'#!/usr/bin/env python

import sys

# input comes from STDIN (standard input)
for line in sys.stdin:
    # remove leading and trailing whitespace
    line = line.strip()
    # split the line into words
    words = line.split()
    # increase counters
    for word in words:
        # write the results to STDOUT (standard output);
        # what we output here will be the input for the
        # Reduce step, i.e. the input for reducer.py
        #
        # tab-delimited; the trivial word count is 1
        print '%s\t%s' % (word, 1)

		
```

And this code to reducer.py:

```
#!/usr/bin/env python

from operator import itemgetter
import sys

current_word = None
current_count = 0
word = None

# input comes from STDIN
for line in sys.stdin:
    # remove leading and trailing whitespace
    line = line.strip()

    # parse the input we got from mapper.py
    word, count = line.split('\t', 1)

    # convert count (currently a string) to int
    try:
        count = int(count)
    except ValueError:
        # count was not a number, so silently
        # ignore/discard this line
        continue

    # this IF-switch only works because Hadoop sorts map output
    # by key (here: word) before it is passed to the reducer
    if current_word == word:
        current_count += count
    else:
        if current_word:
            # write result to STDOUT
            print '%s\t%s' % (current_word, current_count)
        current_count = count
        current_word = word

# do not forget to output the last word if needed!
if current_word == word:
    print '%s\t%s' % (current_word, current_count)
```

### Run locally
```
echo "foo foo quux labs foo bar quux" | ./mapper.py
echo "foo foo quux labs foo bar quux" | ./mapper.py | sort -k1,1 | ./reducer.py
```

### Run using Hadoop!

```
hadoop jar /usr/hdp/2.6.1.0-129/hadoop-mapreduce/hadoop-streaming.jar \
-file /home/maria_dev/mapper.py    -mapper /home/maria_dev/mapper.py \
-file /home/maria_dev/reducer.py   -reducer /home/maria_dev/reducer.py \
-input /user/maria_dev/gutenberg/* -output /user/maria_dev/gutenberg-output
```
It will print out the location of the output, and you can see job information here:

[http://10.137.174.204:19888/jobhistory](http://10.137.174.204:19888/jobhistory) 

## Other technologies
Most ways to run python on Hadoop (with MapReduce) are just frameworks built on Hadoop Streaming.  Hadoop Streaming's performance is acceptable - approximately 1.5 times the time taken for a 20GB sample algorithm.  MrJob, dumbo, and hadoopy are much slower:

![Performance](http://blog.cloudera.com/wp-content/uploads/2013/01/performance.png)

## Resources 

* [Python MapReduce tutorial](http://www.michael-noll.com/tutorials/writing-an-hadoop-mapreduce-program-in-python/)
* [Python MapReduce technologies comparison](https://blog.cloudera.com/blog/2013/01/a-guide-to-python-frameworks-for-hadoop/)
 