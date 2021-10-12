# Allen's KDB Interview Prep
<a name="top"></a>

<br>


### What is an Atom vs a List?

```q
An atom - is an irreducible value of a specific data type
A list -  is an ordered sequence of items
```

<hr> 

### What is a dictionary and a table? How are they related?

```q
Dictionaries are a data structure that maps from a domain to a range of values. 
Contains a ! to separate keys and values.

A table is a flipped dictionary. Vectors of data are organized by columns. 
Tables are encased by parathesis ( ) and contain brackets [ ] which assigns the key.
```

<hr> 

### what is the difference between a table and a keyed table?

```q
A table - is a flipped dictionary. Vectors of data are organized by columns.

A keyed table - is a table of keyed records mapped to a table of value records.
```

<hr> 

### What is the difference between a sym and a string?

```q
A sym -  is an atomic entity holding text. Represented with a back tick. 
Smaller in size than a char.

A string - is a list of chars. Represented by " " double parathesis
```

<hr> 

### What is casting? Cast an int to a float

```q
casting converts one datatype to another
```

```q
`int$3.0 / cast float to int
3
```

<hr> 

### What happens when you cast a date to an int?

```q
`int$2000.10.04
3
/ casts as dates from 2000.01.01
```

<hr> 

### Convert syms a b c to a String

```q
string `a`b`c
("a","b","c")
/ simply use the string function
```

<hr>

### How do you cast a string to a sym?

```q
`$"a","b","c"
"S"$"a","b","c"
`abc
```

<hr> 

### What is parsing?

Parsing is converting a string to another datatype.

```q
l:("1.00001"; "200"; "3.1417")
"FIF"$l

1.00001 / float
200 / int
3.1417 / float
```

<hr> 

### What are the common operators?

```q
#   / take
_   / drop
?   / find, randomize
@   / apply
!   / dictionary, key, unkey, 
$   / cast, enumerate
,   / join
^   / fill
```
<hr> 

### Show 3 ways to retrieve values from a dictionary

```q
d: `a`b`c!1 2 3

d[`a] = 1
d@`a = 1
d `a = 1
```

<hr> 

### What happens when you try retrieving from a dictionary that has non-unique keys?

```q
d: `a`b`c`a!1 2 3 4
d[`a] = 1 / returns the first entry
```

<hr> 

### Take first 2 items from dict. retrieve value from key 'c

```q
d: `a`b`c!1 2 3
2 # d / returns a dictionary of first 2 rows
(enlist `c) # d / have to use enlist when retrieving single domain
```

<hr> 

### How do you upsert different keys/values from the original dict's datatype?

The upserted keys and values must match in type. <br >
Way around this is to keep dictionary generic using null item

```q
dz: enlist[::]!enlist[::]
dz
dz[`a]:100
dz[100]:`a

key value
a 100
100 a
```

<hr> 

### What are some common table functions?

```q
t:([] company:`ford`bmw; employees:300 100)
t
type t               / what datatypes the table is
count t              / return number of rows
cols t               / retrieve symbol list of column names
meta t               / shows info on type, foreign keys, and attributes
`employees xasc t    / sorts table by employee column
```

<hr> 

### Show examples of union, except, and inter function on tables

```q
t:([] company:`ford`bmw`benz; employees:100 200 300)
u: ([] company:`ford`bmw`ferrari; employees:100 200 400)
```
table t

company | employees
-|-
ford	|100
bmw	|200
benz	|300

table u
company | employees
-|-
ford	|100
bmw	|200
ferrari	|400

```q
t union u / combines every key and value

ford 100
bmw 200
benz 300
ferrari	400
```

```q
t except u / returns item in t NOT in u

benz 300
```

```q
t inter u / returns only common elements in both t and u

ford 100
bmw 200
```

<hr> 

### Show 2 ways to insert data into a table

```q
t:([] company:(); employees:())
insert[`t; (`ferrari;8)]
insert[`t; ([] company:`subaru`hyundai; employees:55 56)]
```
both work; second example specifies column names

<hr> 

### Show how to append using table joins , (comma)

```q
t:([] company:(); employees:())
t:t,([] company:`bmw`skoda; employees:200 300)
```

<hr> 

### what is the difference between equals = and match ~

```q
4 = 4.0
1b / true

4 ~ 4.0
0b / false. match is a lot more strict.
```

<hr> 

### What is an ADVERB?

```q
An adverb modifies an existing verb or function to alter how its applied to its arguments

x,'y / each both
x,\: y / each left
x,/: y / each right	
x \ y / scan
x / y / over
```

### Each Both

```q
x,'y
Joins corresponding elements from two vectors of the same length
```
```q
1 2 3 ,' 10 20 30
1 10
2 20
3 30
```
```q
("car"; "far"; "mar") ,' "e"
"care"
"fare"
"mare"
```

### Each Left
```q
x,\:y 

The top of the \ points LEFT
Adds EACH element of LEFT (x) to ENTIRE y 
```

```q
1 2 3 ,\: `a`b`c

1`a`b`c
2`a`b`c
3`a`b`c
```

### each right ,/:
```q
x,/:y 

The top of the / points RIGHT
Adds each element of y to the entirety of x
```

```q
1 2 3 ,/: `a`b`c

1 2 3`a
1 2 3`b
1 2 3`c
```

### Scan

```q
1 +\ 0 1 2 3

1 2 4 7

/ scan is an accumulating iterator.
/ returns the result of each result
```

### Over

```q
1 +/ 0 1 2 3

7
/ over is an accumulating iterator
/ returns the final result
```

### What are Attributes?

```q
Attributes describe how the underlying data in lists are structured.
This speeds up queries and optimizes memory usage.

1. Sorted 's#
2. Unique 'u#
3. Grouped 'g#
4. Parted 'p#
```

### Attribute - Sorted
```q
's#listname
requires elements to be sorted
allows binary search instead of fully scanning (much faster)
```
### Attribute - Unique
```q
'u#listname
requires elements to be unique
creates unique hash table in the background, allowing for constant time lookup of elements
```
### Attribute - Grouped
```q
'g#listname
a lookup table from each distinct value in the table is created to map to the positions where value occurs.
allows for much faster lookup
```
### Attribute - Parted
```q
'p#listname
requires all elements of same value to occur together
allows for faster queries
```

### How do you load a file with column headers?

With Column Headers

```q
/ if a delimiter is enlisted, the first row of the csv file is read as a column header

("SSJ"; enlist",")0: `sample.csv

/ S=sym
/ J=int
```

Without Column Headers

```q
/ if the CSV file contains data but no column names, dont need to enlist a delimiter

("SSJ";",") 0: `:sample.csv
```

<hr>

### How would you comparing current orders against Potential Crosses

Objectives:
1. Pull in CSV file of current orders (trade)
2. Pull in CSV file of proposed crosses (cross)
3. For each symbol, check opposing direction, and pull in quantity to cross
4. Create new column displaying shares that can cross
5. Retrieve columns in clean format to export back into csv


```q
t:("SSJ";enlist",") 0: `:trade.csv
```
t 

ric| side | qty
-|-|-
1810.HK|	Buy|	500
0700.HK|	Buy|	500
9988.HK|	Buy|	500
0001.HK|	Buy|	500
0016.HK|	Buy|	500
0151.HK|	Buy|	500
0005.HK|	Buy|	500


```q
c:("SSJ";enlist",") 0: `:cross.csv
```
c

ric | brokerside | brokerquantity
-|-|-
1810.HK|	Sell|	100
0700.HK|	Sell|	100
9988.HK|	Sell|	100
8888.HK|	Sell|	100
0016.HK|	Buy|	100
1234.HK|	Buy|	100
3033.HK|	Buy|	100

```q
1!`c
```
first set the RIC as a key column in cross file

```q
A: update crossableqty:?[side=brokerside;0N; qty - brokerquantity] from t lj 1!c
```
A

ric|side|qty|brokerside|brokerquantity|crossableqty
-|-|-|-|-|-
1810.HK|	Buy|	500|	Sell|	100|	400
0700.HK|	Buy|	500|	Sell|	100|	400
9988.HK|	Buy|	500|	Sell|	100|	400
0001.HK|	Buy|	500|	Sell|	100|	400

```q
A2: select from A where crossableqty > 0
```
ric|side|qty|brokerside|brokerquantity|crossableqty
-|-|-|-|-|-
1810.HK|	Buy|	500|	Sell|	100|	400
0700.HK|	Buy|	500|	Sell|	100|	400
9988.HK|	Buy|	500|	Sell|	100|	400
0001.HK|	Buy|	500|	Sell|	100|	400

```q
select ric, side, crossableqty from A2
```
ric|side|crossableqty
-|-|-
1810.HK|	Buy|	400
0700.HK|	Buy|	400
9988.HK|	Buy|	400
0001.HK|	Buy|	400

* this is the end result. these are the lines where you can cross 

<hr>

<a name="nettingbuyssells_case"></a>
### 🔵 3. Netting off buys and sells from same Stock

* same stock, multiple lines of buys and sells in the same stock
* determine what is the net quantity

Given
```q
t:([] ric:`AAPL; side:`buy`sell`sell`buy`buy; size:10 30 50 100 90)
```
ric | side |size
-|-|-
AAPL|	buy|	10
AAPL|	sell|	30
AAPL|	sell|	50
AAPL|	buy|	100
AAPL|	buy|	90

```q
select ?[side=`buy;size;neg size] by ric from t
```
ric | size
-|-
AAPL |	10 -30 -50 100 90

```q
select sum ?[side=`buy;size;neg size] by ric from t
```
ric | size
-|-
AAPL |	120

<hr>

## Turn 2 lists of symbols into one longer list. 

```q
`AAPL`IBM`VOD and `O`N`L

/ expected outcome
AAPL.O IBM.N VOD.L
```

* convert syms O N L into strings
* add . to each element of O N L
* convert APPL IBM VOD into strings
* concatenate the 2 lists of strings together
* convert the strings back into symbols
* strings are NOT a datatype

```q
L1: `AAPL`IBM`VOD
L2:`O`N`L 

string L2 / convert from sym to string
/ ("O";"N";"L")

s2: ".",/: string L2 / using EACH RIGHT to add . to every element of O N L
/ (".O";".N";".L")

s1: String L1 / convert sym to string
/ ("AAPL";"IBM";"VOD")

S1,'S2 / using EACH BOTH joins each element of s1 to each element of s2
/ ("AAPL.O";"IBM.N";"VOD.L")

"S" $ (S1,'S2) / cast back to sym
/ `AAPL.O`IBM.N`VOD.L
```

* convert L1 and L2 to strings (so you can add . and later join)
* use EACH BOTH ADVERB to join each elemnt of S1 to each elemnt of S2
* cast the list of strings back to list of syms


<hr> 

### Create a function that will return latest prices (with max timestamp within the date) for the date.
If there is not any price for that particular date, return the latest previous price
There is no predefined ordering of the source table.
Try to preserve the column order.

Given: 

```q
t: ([] date:raze (3#2016.01.06;4#2016.01.07;6#2016.01.08); sym:`a`b`c`a`b`a`b`a`b`c`a`b`c; price:1 2 3 1.1 2.1 1.2 2.2 1.3 2.3 3.2 1.4 2.4 3.3; timestamp:raze (3#2016.01.06T22:00:00.000; 2#2016.01.07T22:00:00.000; 2#2016.01.08T23:00:00.000; 3#2016.01.08T22:00:00.000; 3#2016.01.06T22:30:00.000))
```

Example 1:
f [t; 2016.01.06]

date | sym | price | timestamp
-|-|-|-
2016-01-06|	a|	1|	2016-01-06T22:00:00.000
2016-01-06|	b|	2|	2016-01-06T22:00:00.000
2016-01-06|	c|	3|	2016-01-06T22:00:00.000

Example 2:

f [t; 2016.01.07]

date | sym | price | timestamp
-|-|-|-
2016-01-06|	c|	3|	2016-01-06T22:00:00.000
2016-01-07|	a|	1.2|	2016-01-08T23:00:00.000
2016-01-07|	b|	2.2 |	2016-01-08T23:00:00.000

Example 3:

f [t; 2016.01.08]

date | sym | price | timestamp
-|-|-|-
2016-01-08|	a|	1.3|	2016-01-08T22:00:00.000
2016-01-08|	b|	2.3|	2016-01-08T22:00:00.000
2016-01-08|	c|	3.2|	2016-01-08T22:00:00.000

```q
f:{[t;d] select last price, max timestamp by date, sym from t where date<=d, timestamp=(max;timestamp) fby date, price=(last;price) fby sym}
```

* select last price, max timestamp
* set date, sym as keys
* date <=d means look for previous day if current date doesnt satisfy query conditions
* the FBY is the most important part of this problem. 
* the ORDER of the FBY also matters a lot. 
* you want to filter the LAST PRICE by sym, then
* you want to filter the MAX TIMESTAMP by the date

<hr>

### Given the 2 tables:

```q
t1: ([] sym:`a`b`c;ex:`x)
t2:([] ex:`y;sym:`a`b`c)

ps:(( [] sym:`a`b`c`a`b`c; ex:`x`x`x`y`y`y; price: 1.1 2.1 3.1 1.2 2 3.3); ( [] sym:`a`b`c`a`b`c; ex:`x`x`x`y`y`y; size: 200 100 300 200 50 200))
```

## Part 1: Join the first two tables using t1 schema ##

Desired Result:

sym | ex
-|-
a | x
b |x
c |x
a |y
b |y
c |y

```q
t3: t1,t2
```
sym | ex
-|-
a|	x
b|	x
c|	x
a|	y
b|	y
c|	y

## Part 2: Join list of tables to newly created table using sym and ex as a keys

Desired Result:

sym | ex | price | size
-|-|-|-
a|	x| 1.1 | 200
b|	x|2.1|100
c|	x|3.1|300
a|	y|1.2|200
b|	y|2|50
c|	y|3.3|200

```q
ps1:2!first ps
ps2:2!last ps
```
* you want to split up list of tables ps into 2 separate tables by using first ps, last ps
* use 2! to set the sym and ex columns as keys

ps1

sym|ex|price
-|-|-
`a`|`x`|	1.1
`b`|	`x`|	2.1
`c`|	`x`|	3.1
`a`|	`y`|	1.2
`b`|	`y`|	2.0
`c`|	`y`|	3.3

ps2

sym|ex|size
-|-|-
`a`|`x`|	200
`b`|	`x`|	100
`c`|	`x`|	300
`a`|	`y`|	200
`b`|	`y`|	50
`c`|	`y`|	200

```q
ps3:ps1 lj ps2
```
* join the ps1 and ps2 tables back together to make table ps3

sym|ex|price|size
-|-|-|-
`a`|`x`|1.1|	200
`b`|	`x`|	2.1|100
`c`|	`x`|	3.1|300
`a`|	`y`|	1.2|200
`b`|	`y`|	2| 50
`c`|	`y`|	3.3| 200

```q
t4: t3 lj ps3
```

* use left join to join ps3 to t3

sym|ex|prirce|size
-|-|-|-
x|	a|	1.1|	200
x|	b|	2.1|	100
x|	c|	3.1|	300
y|	a|	1.2|	200
y|	b|	2.0|	50
y|	c|	3.3|	200


## Part 3: Add 3 new columns: avg_price_by_sym, avg_size_by_ex, wavg_price_by_sym (weighted by size)

Desired Result:

sym|ex|prirce|size| avg_price_by_sym| avg_size_by_ex | wavg_price_by_sym
-|-|-|-|-|-|-
x|	a|	1.1|	200 | 1.15 | 200 | 1.15
x|	b|	2.1|	100|2.05| 200| 2.0667
x|	c|	3.1|	300|3.2| 200| 3.18
y|	a|	1.2|	200|1.15| 150| 1.15
y|	b|	2.0|	50|2.05| 150| 2.06667
y|	c|	3.3|	200|3.2| 150| 3.18

```q
update avg_price_by_sym: avg price by sym from `t4
update avg_price_by_ex: avg size by ex from `t4
update wavg_price_by_sym: size wavg price by sym from `t4
```
sym|ex|prirce|size| avg_price_by_sym| avg_size_by_ex | wavg_price_by_sym
-|-|-|-|-|-|-
a|	x|	1.1|	200|	1.15|	200|	1.15
b|	x|	2.1|	100|	2.05|	200|	2.0667
c|	x|	3.1|	300|	3.2	|200	|3.18
a|	y|	1.2|	200|	1.15|	150|	1.15
b|	y|	2.0|	50	|2.05	|150	|2.0667
c|	y|	3.3|	200|	3.2	|150	|3.18


### Given the table, compute column d

```q
orders: ( [] order:10*1 + til 8; sym:`NYSE`NYSE,6#`NASDAQ; start: 08:00 09:00 09:00 08:00 10:00 12:30 13:30 18:00; end:11:00 13:00 15:30 13:30 11:30 13:30 14:30 19:00)
```

order | sym | start | end
-|-|-|-
10|	NYSE|	08:00|	11:00
20|	NYSE|	09:00|	13:00
30|	NASDAQ|	09:00|	15:30
40|	NASDAQ|	08:00|	13:30
50|	NASDAQ|	10:00|	11:30
60|	NASDAQ|	12:30|	13:30
70|	NASDAQ|	13:30|	14:30
80|	NASDAQ|	18:00|	19:00

<hr>


[Top](#top)
