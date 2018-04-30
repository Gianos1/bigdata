# Bigdata
01QYDOV

## Exercises:

1. WordCount problem

  * [Exercise 02](#ex2): all file in a directory

  * [Exercise 09](#ex9) : in-mapper combiner


2. PM10 pollution analysis

  * [Exercise 3](#ex3) : Use of `KeyValueTextInputFormat`

  * [Exercise 4](#ex4) : use of **custom type**

  * Exercise 5

    * [version 1](#ex5v1)

    * [verison 2](#ex5v2) : use of **combiner**

  * [Exercise 6](#ex6) : Min and Max without custom type

  * [Exercise 10](#ex10) : Custom counters

  * [Exercise 12](#ex12) : **Map Only Job** - _(user provided threshold)_


3. Income

  * [Exercise 8](#ex8) : Use of setup an clean up method

  * [Exercise 13](#ex13) : **TOP 1** (_custom type_)


4. Dictionary

  * [Exercise 14](#ex14) : Use of linked list - NullWritable for the output value

  * [Exercise 15](#ex15) : Each input word is written in the output only once and is associated with a unique identifiers


# Word Count Problem

## Exercise 2 <a name="ex2"></a>

Number of occurrences of each word appearing in the input file

### INPUT
Unstructured textual file
```
Test of the word count program
The word program is the Hadoop hello word program
Example document for hadoop word count
```

### OUTPUT
```
test    1
of      1
the     3
...
```

## Exercise 9 <a name="ex9"></a>

Number of occurrences of each word appearing in the input file

### INPUT
Unstructured textual file
```
Test of the word count program
The word program is the Hadoop hello word program
Example document for hadoop word count
```

### OUTPUT
```
test    1
of      1
the     3
...
```


# PM10 Pollution Analysis

## Exercise 3 <a name="ex3"></a>

Report, for each sensor, the number of days with PM10 above a specific threshold (hardcoded)

### INPUT
Structured textual file
```
s1,2016-01-01   20.5
25,2016-01-01   30.1
```

### OUTPUT
```
s1   2
s2   1
```

## Exercise 4 <a name="ex4"></a>

Report for each zone the list of dates associated with PM10 value above a specific threshold.

Suppose threshold=50

N.B.: in this case _Combiner_ is useless because no aggregation is possible after the Mappers

### INPUT
Structured textual file
```
zone1,2016-01-01    20.5
zone2,2016-01-01    30.1
zone1,2016-01-02    60.2
zone2,2016-01-02    20.4
zone1,2016-01-03    55.5
zone2,2016-01-03    52.5
```

### OUTPUT
```
zone1   [2016-01-03,2016-01-02]
zone2   [2016-01-03]
```

## Exercise 5 version 1 <a name="ex5v1"></a>

Report, for each sensor, the average value of PM10

### INPUT
Structured csv textual file
```
s1,2016-01-01,20.5
25,2016-01-01,30.1
...
```

### OUTPUT
```
s1   45.4
s2   34.3
```

## Exercise 5 version 2 <a name="ex5v2"></a>

Report, for each sensor, the average value of PM10
This version will use a **combiner** and a **custom type**.

### INPUT
Structured csv textual file
```
s1,2016-01-01,20.5
25,2016-01-01,30.1
...
```

### OUTPUT
```
s1   45.4
s2   34.3
```

## Exercise 6 <a name="ex6"></a>

Report, for each sensor, the maximum and the minimum value of PM10
This version will use a **combiner** but **no custom type**.

### INPUT
Structured csv textual file
```
s1,2016-01-01,20.5
25,2016-01-01,30.1
...
```

### OUTPUT
```
s1    max=60.2_min=20.5
s2    max=52.5_min=20.4
```

## Exercise 10 <a name="ex10"></a>

Total number of records.
No reducer nor combiner are used; the mapper increment the counter each time it receives an input.

### INPUT
Structured csv textual file
```
s1,2016-01-01,20.5
25,2016-01-01,30.1
...
```

### OUTPUT
```
MYCOUNTERS.TOT_RECORDS = 6
```

## Exercise 12 <a name="ex12"></a>

Output are records with a PM10 value below a **user provided** _(arguments of program)_ threshold.
**No Reducer**
**No Combiner**

### INPUT
Structured csv textual file
```
s1,2016-01-01	20.5
s1,2016-01-01	30.1
s2,2016-01-01	60.2
s2,2016-01-02	20.4
s1,2016-01-03	55.5
s2,2016-01-03	52.5

Threshold   21

```

### OUTPUT
```
s1,2016-01-01	20.5
s2,2016-01-02	20.4
```


## Income

## Exercise 8 <a name="ex8"></a>

Total income for each month of the year and average monthly income per year

### INPUT
```
2015-11-01    1000
2016-01-01    345
...
```

### OUTPUT
```
2015-11   2305
2015-12   1250
2015      1777.5
2016      1090.00
```

## Exercise 13 <a name="ex13"></a>

Output the couple (date, income) for which income represents the maximum value from the input set

### INPUT
```
2015-11-01	1000
2015-11-02	1305
2015-12-01	500
2015-12-02	750
2016-01-01	345
2016-01-02	1145
2016-02-03	200
2016-02-04	500
```

### OUTPUT
```
2015-11-02	1305
```


## Dictionary

## Exercise 14 <a name="ex14"></a>

The input words are written in the output only once.
To reduce network data, the mapper will use a linked list to keep track of each word.

### INPUT
```
Toy example
file for Hadoop
Hadoop running
example
```

### OUTPUT
```
example
file
for
hadoop
running
toy
```

## Exercise 15 <a name="ex15"></a>

The input words are written in the output only once and each word is associated with a unique integer.
To reduce network data, the mapper will use a linked list to keep track of each word.

**NB:** to implement unique identifier a private global `int` variable is used inside MyReducer class; every time a key comes to the reducer, the variable is incremented.

### INPUT
```
Toy example
file for Hadoop
Hadoop running
example
```

### OUTPUT
```
example
file
for
hadoop
running
toy
```
