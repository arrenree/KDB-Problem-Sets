# Allen's KDB Practice Problems + Solutions
<a name="top"></a>

1. [General Knowledge / System](#gen)
2. [Casting / Datatypes / Temporal](#cast)
3. [Lists](#list)
4. [Dictionary](#dictionary)
5. [Tables](#tables)
6. [Functions](#functions)
7. [qSQL](#qsql)
8. [Adverbs](#adverbs)
9. [Attributes](#attributes)
10. [Joins](#joins)

<hr>

<a name="gen"></a>
### 🔴 General Knowledge / System
[Top](#top)

### [gen] What is an Atom vs a List?

```q
An atom - is an irreducible value of a specific data type
A list -  is an ordered sequence of items
```

### [gen] Order of Operations

```q
a = 5
b = a -3
c = 3b + 1

a: 5
b: a -3
c: (3*b)-1 or 1+3*b

/ now re-write as single statement

c: 1 + 3 * b: -3 + a:5

/ right to left 
```

### [gen] What are the common operators?

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

### [gen] What is a dictionary and a table? How are they related?

```q
Dictionaries are a data structure that maps from a domain to a range of values. 
Contains a ! to separate keys and values.

A table is a flipped dictionary. Vectors of data are organized by columns. 
Tables are encased by parathesis ( ) and contain brackets [ ] which assigns the key.
```


### [system] show all variables definied in current session of q

```q
\v
`a`b`c`d
```

### [system] Close the current session
```q
\\
```

### [gen] what is the difference between equals = and match ~

```q
4 = 4.0
1b / true

4 ~ 4.0
0b / false. match is a lot more strict.
```
### [system] How do you load a file with column headers?

```q
/ With Column Headers

/ if a delimiter is enlisted, the first row of the csv file is read as a column header

("SSJ"; enlist",")0: `sample.csv

/ S=sym
/ J=int
```
```q
/ Without Column Headers

/ if the CSV file contains data but no column names, dont need to enlist a delimiter

("SSJ";",") 0: `:sample.csv
```

### [system] How would you comparing current orders against potential crosses

```q
Objectives:
1. Pull in CSV file of current orders (trade)
2. Pull in CSV file of proposed crosses (cross)
3. For each symbol, check opposing direction, and pull in quantity to cross
4. Create new column displaying shares that can cross
5. Retrieve columns in clean format to export back into csv

/ load csv file of current orders

t:("SSJ";enlist",") 0: `:trade.csv

ric    |side | qty
------------------
1810.HK| Buy |	500
0700.HK| Buy |	500
9988.HK| Buy |	500
0001.HK| Buy |	500
0016.HK| Buy |	500
0151.HK| Buy |	500
0005.HK| Buy |	500

/ load csv file of proposed crosses

c:("SSJ";enlist",") 0: `:cross.csv

ric    |brokerside | brokerquantity
---------------------------------
1810.HK|    Sell   |	100
0700.HK|    Sell   |	100
9988.HK|    Sell   |	100
8888.HK|    Sell   |	100
0016.HK|    Buy    |	100
1234.HK|    Buy    |	100
3033.HK|    Buy    |	100

/ first set the RIC as a key column in cross file
1!`c

/ add column crossableqty, check opposing side, calc difference
A: update crossableqty:?[side=brokerside;0N; qty - brokerquantity] from t lj 1!c

ric    |side|qty|brokerside|brokerquantity|crossableqty
-------------------------------------------------------
1810.HK|Buy |500|   Sell   |      100     |	400
0700.HK|Buy |500|   Sell   |	    100     |	400
9988.HK|Buy |500|   Sell   |	    100     |	400
0001.HK|Buy |500|   Sell   |	    100     |	400

A2: select from A where crossableqty > 0

ric    |side|qty|brokerside|brokerquantity|crossableqty
-------------------------------------------------------
1810.HK|Buy |500|   Sell   |      100     |	400
0700.HK|Buy |500|   Sell   |	    100     |	400
9988.HK|Buy |500|   Sell   |	    100     |	400
0001.HK|Buy |500|   Sell   |	    100     |	400

select ric, side, crossableqty from A2

ric    |brokerside | brokerquantity
---------------------------------
1810.HK|    Buy    |	400
0700.HK|    Buy    |	400
9988.HK|    Buy    |	400
0001.HK|    Buy    |	400

/ this is the end result. these are the lines where you can cross 
```

<hr>

### [system] Netting off buys and sells from same Stock

```q

/ same stock, multiple lines of buys and sells in the same stock
/ determine what is the net quantity

t:([] ric:`AAPL; side:`buy`sell`sell`buy`buy; size:10 30 50 100 90)

ric | side | size
-----------------
AAPL| buy  | 10
AAPL| sell | 30
AAPL| sell | 50
AAPL| buy  | 100
AAPL| buy  | 90

select ?[side=`buy;size;neg size] by ric from t

ric  | size
-------------------------
AAPL | 10 -30 -50 100 90

select sum ?[side=`buy;size;neg size] by ric from t

ric  | size
-----------
AAPL | 120
```


<hr>

<a name="cast"></a>
### 🔴 Casting / Datatypes / Temporal
[Top](#top)


### [cast] What is the difference between a sym and a string?

```q
A sym -  is an atomic entity holding text. Represented with a back tick. 
Smaller in size than a char.

A string - is a list of chars. Represented by " " double parathesis
```

### [cast] What is casting? Cast an int to a float

```q
casting converts one datatype to another
```

```q
`int$3.0 / cast float to int
3
```

<hr> 

### [cast] What happens when you cast a date to an int?

```q
`int$2000.10.04
3
/ casts as dates from 2000.01.01
```

<hr> 

### [cast] Convert syms a b c to a String

```q
string `a`b`c
("a","b","c")
/ simply use the string function
```

<hr>

### [cast] How do you cast a string to a sym?

```q
`$"a","b","c"
"S"$"a","b","c"
`abc
```

<hr> 

### [cast] Cast the Following

```q
/ "2014.01.01" to a date

"D" $ "2014.01.01"
-14h

/ "2014.01.01" was originally a string
/ use capital "D" to cast strings to date

/ `2013.01.01 to a date

"D" $ string `2013.01.01

/ `2013.01.01 is a sym
/ requires first to cast to string, then cast to date

/ 3.14 to an int

`int $ 3.14 
3

/ note rounding for ints
/ alternatively "I" $ 3.14

/ "abcde" to a sym

`$"abcde"
```

### [cast] What is parsing?

Parsing is converting a string to another datatype.

```q
l:("1.00001"; "200"; "3.1417")
"FIF"$l

1.00001 / float
200 / int
3.1417 / float
```

### [cast] what do you get dates when casting int to date?

```q

dates are stored as integers (days) from 2000.01.01
```

### [temporal] Get today's date store it as variable d

```q
d: .z.d
2021-11-01d
```

### [temporal] Calculate the number of days since last christmas

```q
d-2020.12.25
311i

/ can use algebra with dates (ints underneath)
```

### [temporal] What day of the week was Jan 10, 2011?

```q
2011.01.10 mod 7
2i

/ since dates start on sunday, 2 days from sunday = Monday

.z.d mod 7
2i

/ todays date = monday, Nov 11
/ 2 days from sunday = Monday
```
### [string] Define strings s1: "Hello" and s2: "World"

```q
s1: "hello"
s2: "world"

/ join the 2 strings together and save to s

s:s1, " ",s2
"hello world"

/ find index position of "w"

s?"w"
6

/ find index positions of all "l" in s

ss[s;"l"]
2 3 9

/ ss = search string function. returns index position

/ find index position of last l

last ss[s;"l"]

/ remove "hello" and add " of warcraft" to s

ssr["hello world"; "hello ";""], " of warcraft"
world of warcraft

ssr[s;"hello ";""], " of warcraft"
world of warcraft
```
## [datatypes] Turn 2 lists of symbols into one longer list. 

```q
`AAPL`IBM`VOD and `O`N`L

/ expected outcome
AAPL.O IBM.N VOD.L

/ convert syms O N L into strings
/ add . to each element of O N L
/ convert APPL IBM VOD into strings
/ concatenate the 2 lists of strings together
/ convert the strings back into symbols
/ strings are NOT a datatype

L1: `AAPL`IBM`VOD
L2:`O`N`L 

string L2 / convert from sym to string
("O";"N";"L")

s2: ".",/: string L2 / using EACH RIGHT to add . to every element of O N L
(".O";".N";".L")

s1: String L1 / convert sym to string
("AAPL";"IBM";"VOD")

S1,'S2 / using EACH BOTH joins each element of s1 to each element of s2
("AAPL.O";"IBM.N";"VOD.L")

"S" $ (S1,'S2) / cast back to sym
 `AAPL.O`IBM.N`VOD.L
```

<hr>

<a name="list"></a>
### 🔴 Lists
[Top](#top)


### [list] Create Empty List d
```q

d: ()

/ redefine d to be empty list of type integer

d: `int $ ()

/ add 5 random elements to d

d, 5 ? til 10

/ 5?til 10 = randomly select 5 numbers from 0-9
/ d , joins these 2 lists, thereby adding into list
```

### [list] Create list e with 1 element

```q

e: enlist 10

/ have to use enlist on single elements
/ or e:(), 10
```

### [list] Create list l with 20 random values from 3 to 30
```q

l: 20 ? 3_til 31

/ drop first 3 elements, so range is 3-30
/ alternatively can do 1:20?3+til 28

/ find the 20th number in list l

l[19]

/ use indexing to retrieve 19th index position = 20th number
/ since starts on 0

/ are any of these numbers in the list? 3 5 7 11 13 17

3 5 7 11 13 17 in l
```

### [list] Add each element of l to its index position. for ex, 0 to index 0, 1 to index 1, etc.

```q
l+: til count l

/ count l = 20 elements in list l
/ til 20 = 0 - 19, gives you the index position
/ so now you have 2 lists, just need to add together
```
### [list] How many even numbers are there? 

```q

l mod 2
1 1 0 1 0 1 1 0 0 1 0 1 0 1 0 1 0 1 1 0

/ mod 2 tells us when the remainder is
/ so 0 = no remainder = even number
/ now need to count the 0s

count where not l mod 2

/ not = 0, so counts all the 0s (even numbers)
```
### [list] Creating Matrix

```q
m:(1 2 3; 4 5 6; 7 8 9)
1 2 3
4 5 6
7 8 9

/ get middle column of m and save it as new variable a

a: m[;1]

/ [row;column]
/ blank for row; 1 = index position 2, so 2nd row

/ replace middle row of me with a

m[1]:a

/ [row;column] 
/ index position 1 = 2nd row

/ transpose m and store as mm

mm: flip m

/ transpose is a fancy way of saying flip

/ join extra row to mm, consisting of all 10s

mm,: 3#10

/ the syntax ,: appends items to list

```

### [list] Nested Lists

```q

nest: (1 2 3; `a`c`b;10 11 12 14f; 100011b)

/ find the datatype of each row

type each nest

/ collapse this nested list

raze nest
```

### [list] list problem set
```q
games:`crash`streets`echo`crash2`sonic`micro`pokemon`supermario`bomber`zelda
platform: `ps1`sega`sega`ps1`sega`ps1`gameboy`gameboy`sega`gameboy
level: (7 9 6i; 2 5i; 4 4i; 10 2 1i; 1 10i; 8i; 0 3i; 6 0i; 8 4i; 1 10i)

/ count number of users per game

users: count each level
3 2 2 3 2 1 2 2 2 2

/ calc average user level each game

userlevel: avg each level
7.3 3.5 4 4.3 5.5 8 1.5 3 6 5.5

/ create boolean list indicating where avg user level > 6

6 < avg each level
1000010000b

/ calc games where avg user level > 6

games where 6 < avg each level
`crash`micro

/ sum the users for each platform. which one most popular?

sum users where platform in `ps1
sum users where platform in `sega
sum users where platform in `gameboy

/ sum the total count where column platform = ps1, etc.
```

<a name="dictionary"></a>
### 🔴 Dictionary
[Top](#top)

### How do you upsert different keys/values from the original dict's datatype?

```q
/ The upserted keys and values must match in type
/ Way around this is to keep dictionary generic using null item

dz: enlist[::]!enlist[::]
dz
dz[`a]:100
dz[100]:`a

key value
a 100
100 a
```

### [dict] Show 3 ways to retrieve values from a dictionary

```q
d: `a`b`c!1 2 3

d[`a] = 1
d@`a = 1
d `a = 1
```

<hr> 

### [dict] What happens when you try retrieving from a dictionary that has non-unique keys?

```q
d: `a`b`c`a!1 2 3 4
d[`a] = 1 / returns the first entry
```

<hr> 

### [dict] Take first 2 items from dict. retrieve value from key 'c

```q
d: `a`b`c!1 2 3
2 # d / returns a dictionary of first 2 rows
(enlist `c) # d / have to use enlist when retrieving single domain
```


### [dict] Dictionary Problem Set AquaQ

```q

d1: `london`paris`athens`toronto`sydney`tokyo`chicago!0 1 2 -5 9 8 -6

key      value
---------------
london  |	0
paris	  | 1
athens	| 2
toronto	|-5
sydney	| 9
tokyo	  | 8
chicago	|-6

/ extract the hours for tokyo and athens

d1[`tokyo`athens]
8 2
```

```q
/ if it's 12:30 in Paris, what time is it in Chicago?

(d1`paris)-d1`chicago = 7

/ paris vs chicago 7 hour difference
/ need to convert to hours (cuz 7 is just a long)

((d1`paris) - d1`chicago)*01:00
07:00u

/ then calculate difference from 12:30 (paris)

12:30 - 07:00
05:30u

12:30 - (((d1`paris) - d1`chicago)*01:00)

/ final answer
/ alternatively syntax could be:

12:30 + 01:00 *(d1`chicago)-d1`paris

/ right to left
```
```q
/ change London's time from 0 to 1

d1[`london]:1
```
```q
/ add in rome +1

d1[`rome]:1

/ or alternative syntax

d1,:(enlist `rome)!enlist 1

/ when using join assign, must enlist if single atom!
```
```q
d3:`belfast`cardiff`edinburg`london!(12 10 11 9; 11 10 10 10; 10 10 12 9; 15 12)

/ what's the average temp in each city?

avg each d3

/ convert all temp from C to F (temp x 9/5 + 32)

(d3*(9%5))+32

/ find the max temp for belfast

max d3[`belfast]

/ Given new dict d4, find max temp for belfast

d4:(enlist `temperature)!enlist d3

max d4[`temperature;`belfast]

/ so d4 is a dict within a dict
/ first column = temperature
/ 2nd column is the entire dict of 3


/ to add a row to d4:

d4,:(enlist`rainfall)!enlist`belfast`cardiff`edinburgh`london!60 65 58 40
```
### [dict] Dictionary Problem Set (AquaQ)

```q
/ create dictionary with letters from a-z with corresponding numbers

dict: .Q.a ! 1+til 26

key value
---------
a  |  1
b  |  2
c  |  3
...

/ .Q.a = returns list of lowercase alphabets
```
```q
/ retrieve values of abc

dict "abc"
1 2 3

/ sum values of abc

sum dict "abc"
6

/ sum values of "yourname"

sum dict "yourname"
112
```
```q
/ rename keys to capital letters

dict:.Q.A ! value dict

key value
---------
A  |  1
B  |  2
C  |  3

/ can simply override existing dict
/ .Q.A = capital letters
/ value dict = retrieves existing values of dict
```
```q
/ create another dict, change uppercase "HELLO WORLD" to lowercase

dict2: .Q.A ! .Q.a

/ this dict maps all uppercase to lowercase

dict2 "HELLO WORLD"
"hello world"

/ the uppcase letters act as KEYS
/ retrieves the lower case value
```
```q
/ create dictionary morse, which contains letters n-s as keys, and a code for the values

morse: "nopqrs"! (10; 111; 0110; 1101;010;0)

key value
---------
n	  10
o	  111
p	  110
q	  1101
r	  10
s	  0

/ the key is simply a string of chars
/ the values are just random "codes" you make up

/ join numbers 0 to 4 onto the existing dictionary

morse,:("01234")!(1; 10; 100; 1000; 10000)

key value
---------
0	   1
1	   10
2	   100
3	   1000
4	   10000

/ don't get confused, you add "01234" as strings, each with their own "codes"

/ phrase SOS using your code

morse "sos"
0 111 0

/ you are querying keys "sos" to retrieve associated values

```
```q
/ create 2 dictionaries, one for r13, one for r12

places:`london`edinbugh`belfast`manchester`tobermory`portsmouth`cardiff
r13:557 704 944 867 1681 674 1152
r12: 600 854 1020 955 1789 544

d1: places!r13
d2:(-1_places)!r12

/ have to drop last one since value length longer than keys

d1
key       value
----------------
london	   557
edinbugh	 704
belfast	   944
manchester 867
tobermory  1681
portsmouth 674
cardiff	   1152

d2
key        value
----------------
london	   600
edinbugh	 854
belfast	   1020
manchester 955
tobermory	 1789
portsmouth 544

/ extract keys from first dictionary
key d1

extract values from first dictionary
value d1
```
```q
/ create new dict with sum of annual rainful over both years

d3: d1+d2

d3
key        value
-----------------
london	    600
edinbugh	  854
belfast	    1020
manchester	955
tobermory	  1789
portsmouth	544

/ can simply add together both dict since they are keyed (dict always keyed)
/ will find some keys, and add values together
/ if no match, will leave as is
```
```q
/ find the average rainfall over the two years for each city

avg (d1;d2)

/ since the dict is keyed, can perform operations like avg easily

key         value
------------------
london	    578.5
edinbugh	  779.0
belfast	    982.0
manchester	911.0
tobermory 	1735.0
portsmouth	609.0
cardiff	    576.0
```
```q
/ which location had more rainfall over the 2 years?

d1>d2

/ can simply use comparison operator to check if true or false

key         value
------------------
london	    0b
edinbugh	  0b
belfast	    0b
manchester	0b
tobermory	  0b
portsmouth	1b
cardiff	    1b
```
```q
/ find the average rainfall over the 2 years for the UK

sum(d1+d2)%2
6170.5


/ d1+d1 will simply add each row together
/ the sum will aggregate all values together into 1 single value
```

```q
/ create a dict of variables in the workspace as keys, and values as values

system "v"

/ this shows all keys in the workspace

value each (system "v")

/ this shows all values for each key in the workspace

vars: (system "v")! (value each (system "v"))

/ maps keys = variables and values  = values for each key

key   | value
--------------------------------------------------------------------------
d1	  | `lond`edin`bel`man`tober`port`cardiff!557 704 944 867 1681 674 1152
d2	  | `lond`edin`bel`man`tober`port!600 854 1020 955 1789 544
d3	  | `lond`edin`bel`man`tober`port`car!578.5 779 982 911 1735 609 576
places| `lond`edin`bel`manc`tober`port`car
r12	  | 600 854 1020 955 1789 544
r13	  | 557 704 944 867 1681 674 1152
```

<a name="tables"></a>
### 🔴 Tables
[Top](#top)

### [table] what is the difference between a table and a keyed table?

```q
A table - is a flipped dictionary. Vectors of data are organized by columns.

A keyed table - is a table of keyed records mapped to a table of value records.
```
### [tables] Tables Problem Set 2 AQ

```q
/ create 3 lists of 4 elements each for a, b, c

a: 1 2 3 4
b: `a`b`c`d
c: 100 200 300 400

/ create a table using these 3 lists

t:([] a;b;c)

a b c
--------
1	a	100
2	b	200
3	c	300
4	d	400

/ create a dictionary using this table

flip t
key|value
-----------------
a	 | 1 2 3 4
b	 | `a`b`c`d
c	 | 100 200 300 400
```
```q
/ create empty table sym (sym), side (char), size (int), price (float)

trade:([] sym:`$(); side:`char$(); size:`int$(); price:`float$())

/ note for sym all you need is ` to cast

/ create another table, lasttrade, which is a copy of trade, but sym is keyed

lasttrade: 1!trade

/ is there a difference in the metadata between 2 tables?

meta trade ~ meta lasttrade
1b (true)

/ is there a difference in type?

type trade ~ type lasttrade
0b (false)

/ trade = 98h = table
/ lasttrade = 99 = dict (since you keyed)
```
```q
/ use 3 join commands to add rows to trade 
     / sym IBM, MSFT, AAPL
     / side "B" or "S"
     / consistent values for other columns

trade
sym|side|size|price
-------------------

trade,:(`IBM;"B";10i; 100f)
trade,:(`MSFT;"S";20i;200f)
trade,:(`APPL,"B";30i;300f)

/ note - when using ,:join assign to insert data into table, you HAVE TO
/ specify datatype, otherwise will fail
/ for ex, simply appending 10, 100 will fail
```
```q
/ use a single join command to add 3 more rows into join

trade:([] sym:`IBM`MSFT`AAPL;side:"B","S","B";size: 10 20 30; price: 100 200 300)

/ note - when upserting into table, you don't need to specify datatype
/ need to separate chars with comma
```
```q
/ fill lasttrade with data from trade

lasttrade:trade
lasttrade,:trade
```
```q
/ create the following table

stock:([] item:`soda`bacon`mush`eggs;brand:`fry`prok`veg`veg;price:1.5 1.99 0.88 1.55; order:50 82 45 92)

item   brand price order
------------------------
soda	 fry	 1.5	 50
bacon	 prok	 1.99	 82
mush	 veg	 0.88	 45
eggs	 veg	 1.55	 92


/ add row of tomato, veg, 1.35 70

stock,:(`tomato;`veg;1.35;70)

item   brand price order
------------------------
soda	 fry	 1.5	 50
bacon	 prok	 1.99	 82
mush	 veg	 0.88	 45
eggs	 veg	 1.55	 92
tomato veg	 1.35	 70

/ key the table according to item and brand

2!stock
`item`brand xkey stock

/ does the meta data change when you key/unkey tables?

no, it does not
```
```q
trader:([]item:`soda`bacon`mush`eggs`tomato;brand:`fry`prok`veg`veg`veg;price:1.5 1.99 0.88 1.55 1.35; order:200 180 110 210 100)

item   brand price order
------------------------
soda	 fry	 1.5	 200
bacon	 prok	 1.99	 180
mush	 veg	 0.88	 110
eggs   veg	 1.55	 210
tomato veg	 1.35	 100

/ create new table, totalorders, which has sum of both orders from traders
/ drop the price column before adding together

totalorders:(2!(enlist `price)_stock)+(2!(enlist `price)_trader)

item   brand order
------------------
soda	 fry	 250
bacon	 prok	 262
mush	 veg	 155
eggs	 veg	 302
tomato veg	 170

/ need to key the tables before adding together
/ but also need to drop the column
/ since only dropping 1 column, need to use enlist + col name
```
```q
/ create new list called newprices, which is 75% of original price

newprices:0.75*stock`price
1.125 1.4925 0.66 1.1625 1.0125

/ syntax for operations on columns is tablename`colname

/ join newprices to the totalorders table

totalorders:totalorders,' ([] newp:newprices)

item   brand order newprices
---------------------------
soda   fry	 250	 1.125
bacon	 prok	 262	 1.4925
mush	 veg	 155	 0.66
eggs	 veg	 302	 1.1625
tomato veg	 170	 1.0125

/ this method you are appending the column to existing table

update newprices from totalorders

item   brand order newprices
---------------------------
soda   fry	 250	 1.125
bacon	 prok	 262	 1.4925
mush	 veg	 155	 0.66
eggs	 veg	 302	 1.1625
tomato veg	 170	 1.0125

/ this is the SQL method (probably cleaner
/ update col that doesnt exist will append it to table
```
```q
/ how much savings per week will the manager and trader have?

sum ((0!stock)`price)*((0!stock)`order) *0.25
128.72

sum ((0!trader)`price)*((0!trader)`order) *0.25
303.875

/ 75% off, so savings = 0.25
/ syntax is table+`colname
/ calc operations within a table cannot be keyed (need to unkey first 0!)
/ notional = price * qty, though not explicitly explained

/ if you are performing operations within a table, it cannot be keyed

stock
item   brand price order
------------------------
soda	 fry	 1.5	 50
bacon	 prok	 1.99	 82
mush	 veg	 0.88	 45
eggs	 veg	 1.55	 92
tomato veg	 1.35	 70

(stock`price)*(stock`order)
75 163.18 39.6 142.6 94.5

/ this works
/ however, if you key it:

1!`stock
(stock`price)*(stock`order)
type

/ this doesnt work anymore (since its keyed)
```

### [tables] Tables Problem Set AQ
```q

tab1:([id:"abc"]pupil:`john`paul`rachel;subject:`maths`physics`chem;mark:96 55 82)

id pupil   subject mark
-----------------------
a	 john	   maths	 96
b	 paul	   physics 55
c	 rachel  chem	   82

/ extract dictionary corresponding to id = b

tab1["b"]
/ note - id columns are chars not sym! 

/ add the 2 rows of information to tab1
(id = d;pupil = emma; subject = maths; mark = 76)
(id = e;pupil = michael;subject = bio; mark = 63)

tab1,:([id:"de"]pupil:`emma`michael; subject:`maths`bio;mark:76 63)

id pupil   subject mark
-----------------------
a	 john	   maths	 96
b	 paul	   physics 55
c	 rachel  chem	   82
d	 emma	   maths	 76
e	 michael bio	   63

/ id are keyed strings so need " "
/ other values are `syms

/ remove entire keyed column from tab1 rename new table tab2

tab2: value tab1

/ value + table will only return its values

pupil   subject mark
-----------------------
john	   maths	 96
paul	   physics 55
rachel   chem	   82
emma	   maths	 76
michael  bio	   63


/ find first index where chem appears in tab2

tab2[`subject]?`chem
2

/ index position 2 is where subject = `chem appears
/ utilize the ? find operator to search for index position of value
```


### [table] What are some common table functions?

```q
t:([] company:`ford`bmw; employees:300 100)
t
type t               / what datatypes the table is
count t              / return number of rows
cols t               / retrieve symbol list of column names
meta t               / shows info on type, foreign keys, and attributes
`employees xasc t    / sorts table by employee column
```

### [table] Show examples of union, except, and inter function on tables

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

### [table] Show 2 ways to insert data into a table

```q
t:([] company:(); employees:())
insert[`t; (`ferrari;8)]
insert[`t; ([] company:`subaru`hyundai; employees:55 56)]
```
both work; second example specifies column names

<hr> 

### [table] Show how to append using table joins , (comma)

```q
t:([] company:(); employees:())
t:t,([] company:`bmw`skoda; employees:200 300)
```

### [tables] Tables Problem Set (GS)

```q
t1: ([] sym:`a`b`c;ex:`x)
t2:([] ex:`y;sym:`a`b`c)

ps:(( [] sym:`a`b`c`a`b`c; ex:`x`x`x`y`y`y; price: 1.1 2.1 3.1 1.2 2 3.3); ( [] sym:`a`b`c`a`b`c; ex:`x`x`x`y`y`y; size: 200 100 300 200 50 200))

/ Part 1: Join the first two tables using t1 schema ##

Desired Result:

sym | ex
--------
 a  | x
 b  | x
 c  | x
 a  | y
 b  | y
 c  | y

t3: t1,t2

sym | ex
--------
 a  | x
 b  | x
 c  | x
 a  | y
 b  | y
 c  | y

/ Part 2: Join list of tables to newly created table using sym and ex as a keys

Desired Result:

sym | ex | price | size
-----------------------
 a  |  x |  1.1  | 200
 b  |  x |  2.1  | 100
 c  |  x |  3.1  | 300
 a  |  y |  1.2  | 200
 b  |  y |    2  | 50
 c  |  y |  3.3  | 200

ps1:2!first ps
ps2:2!last ps

/ you want to split up list of tables ps into 2 separate tables by using first ps, last ps
/ use 2! to set the sym and ex columns as keys

ps1

sym| ex |price
--------------
`a`|`x` |	1.1
`b`|	`x`|	2.1
`c`|	`x`|	3.1
`a`|	`y`|	1.2
`b`|	`y`|	2.0
`c`|	`y`|	3.3

ps2

sym| ex |size
-------------
`a`|`x` |	200
`b`|	`x`|	100
`c`|	`x`|	300
`a`|	`y`|	200
`b`|	`y`|	50
`c`|	`y`|	200

ps3:ps1 lj ps2

/ join the ps1 and ps2 tables back together to make table ps3

sym|ex |price|size
------------------
`a`|`x`| 1.1 |	200
`b`|`x`| 2.1 | 100
`c`|`x`| 3.1 | 300
`a`|`y`| 1.2 | 200
`b`|`y`| 2   |  50
`c`|`y`| 3.3 | 200

t4: t3 lj ps3

/ use left join to join ps3 to t3

sym|ex|prirce|size
-|-|-|-
x|	a|	1.1|	200
x|	b|	2.1|	100
x|	c|	3.1|	300
y|	a|	1.2|	200
y|	b|	2.0|	50
y|	c|	3.3|	200

/ Part 3: Add 3 new columns: avg_price_by_sym, avg_size_by_ex, wavg_price_by_sym (weighted by size)

Desired Result:

sym|ex|prirce|size|avg_price_by_sym|avg_size_by_ex|wavg_price_by_sym
--------------------------------------------------------------------
 x | a|  1.1 |	200|      1.15      |      200     |    1.15
 x |	b|  2.1 |	100|      2.05      |      200     |    2.0667
 x |	c|  3.1 |	300|      3.2       |      200     |    3.18
 y |	a|  1.2 |	200|      1.15      |      150     |    1.15
 y |	b|  2.0 |	 50|      2.05      |      150     |    2.06667
 y |	c|  3.3 |	200|      3.2       |      150     |    3.18

update avg_price_by_sym: avg price by sym from `t4
update avg_price_by_ex: avg size by ex from `t4
update wavg_price_by_sym: size wavg price by sym from `t4

sym|ex|prirce|size|avg_price_by_sym|avg_size_by_ex|wavg_price_by_sym
--------------------------------------------------------------------
 x | a|  1.1 |	200|      1.15      |      200     |    1.15
 x |	b|  2.1 |	100|      2.05      |      200     |    2.0667
 x |	c|  3.1 |	300|      3.2       |      200     |    3.18
 y |	a|  1.2 |	200|      1.15      |      150     |    1.15
 y |	b|  2.0 |	 50|      2.05      |      150     |    2.06667
 y |	c|  3.3 |	200|      3.2       |      150     |    3.18
```
### [tables] Tables Problem Set 4 (GS)

```q
orders: ( [] order:10*1 + til 8; sym:`NYSE`NYSE,6#`NASDAQ; start: 08:00 09:00 09:00 08:00 10:00 12:30 13:30 18:00; end:11:00 13:00 15:30 13:30 11:30 13:30 14:30 19:00)


order |  sym | start | end
-----------------------------
  10  |  NYSE|	08:00 | 11:00
  20  |  NYSE|	09:00 | 13:00
  30  |NASDAQ|	09:00 | 15:30
  40  |NASDAQ|	08:00 | 13:30
  50  |NASDAQ|	10:00 | 11:30
  60  |NASDAQ|	12:30 | 13:30
  70  |NASDAQ|	13:30 | 14:30
  80  |NASDAQ|	18:00 | 19:00

/ need to create vertical timeline for "buckets" of time
/ flip table 90 degrees
/ check for each bucket, how many active orders per sym
/ then create function to check max number of active orders by exchange for every order id

/ set every startcount and endcount TIME to 1

startcount: select num: count i by ex, time:start from orders
endcount: select num: count i by ex, time: end from orders

startcount
ex     time   num
-----------------
NASDAQ  08:00	1
NASDAQ  09:00	1
NASDAQ  10:00	1
NASDAQ  12:30	1
NASDAQ  13:30	1
NASDAQ  18:00	1
NYSE    08:00	1
NYSE    09:00	1

endcount
ex     time   num
-----------------
NASDAQ  11:30	1
NASDAQ  13:30	2
NASDAQ  14:30	1
NASDAQ  15:30	1
NASDAQ  19:00	1
NYSE	   11:00	1
NYSE	   13:00	1

startcount-endcount

/ startcount minus endcount will tell me every time an order starts (+1), and ends (-1)
/ if i simply do startcount minus endcount, i get this messy table that's not sorted
/ So i need to sort this by exchange and time in order for it to line up with
/ my vertical time buckets.   

`ex`time xasc startcount-endcount

ex     time   num
-----------------
NASDAQ 08:00	1
NASDAQ 09:00	1
NASDAQ 10:00	1
NASDAQ 11:30  -1
NASDAQ 12:30	1
NASDAQ 13:30  -1
NASDAQ 14:30  -1
NASDAQ 15:30  -1
NASDAQ 18:00	1
NASDAQ 19:00  -1
NYSE	  08:00	1
NYSE	  09:00	1
NYSE	  11:00  -1
NYSE	  13:00  -1

/ Part 1 = create a table that has the number of active orders for each time bucket.
/ Update the num column using the fby function, which filters by exchange, an aggregate 
/ of the running sums from the NUM column.
/ i retrieve this fby function FROM startcount-endcount sorted by exchange and time

active: update num: (sums;num) fby ex from `ex`time xasc startcount-endcount

ex     time   num
-----------------
NASDAQ 08:00	1
NASDAQ 09:00	2
NASDAQ 10:00	3
NASDAQ 11:30	2
NASDAQ 12:30	3
NASDAQ 13:30	2
NASDAQ 14:30	1
NASDAQ 15:30	0
NASDAQ 18:00	1
NASDAQ 19:00	0
NYSE	  08:00	1
NYSE	  09:00	2
NYSE	11:00	1
NYSE	13:00	0

/ now that i have this active table, i can go back to my original orders table,
/ check EACH row, for the max num from the ACTIVE table,
/ where ex from ACTIVE is equal to the ex from ORDERS. and where the time from ACTIVE
/ is equal to the start and end time from orders. after executing this, update it to 
/ column d

update d: ({exec max num from active where ex=x`ex, time within x`start`end} each orders) from orders
```

<a name="functions"></a>
### 🔴 Functions
[Top](#top)

### [func] Functions Problem Set AQUA Q
```q
/ write function that calculates square of a number

f:{[a] a*a}

/ execute f with a:5 and assign result to new variable b

a:5
b:f[a]

/ write new funciton g, which takes square of first argument divided by square of second argument

g:{(x*x) % y*y}

/ execute g with arguments a and b, store this to c

c:g[a;b] 

/ create dyadic function f1 indicating whether product of 2 numbers is greater than sum

f1: {(x*y) > x+y}

/ write formual g1: x^5-3x^2 + 5
/ when x=4

g1:{((x xexp 5) - 3*(x xexp 2))+5}
g1[4]
981f

/ create function that calculates area of triangle. height = 7, base = 10

t:{x*y%2}
t[7;10]
35

/ create function that calculates the sum of 2 squares of a number x

f:{x xexp 2 + x xexp 2}
f:{2*(x xexp 2)}

/ create a function that calculates a^3+b^2+c
/ find value of function at 13,3,6

f:{(x xexp 3) + (y xexp 2) + z}
f[13;3;6]

/ BMI is weight divide by height squared. create an implicit formula

bmi: {x%y*y}

/ create a func called perimeters, which will take perimeter of a square
/ and return its area

perimeter:{(x%4) xexp 2}
perimeter[8]
4

/ car depreciates 15% first 3 years, then 8% next 3 years
/ create func k to find value after 6 years (original value 15000)

k:{x*(0.85 xexp 3)*(0.92 xexp 3)}
k[15000]
7173.1765
```

### [func] Create a function that will return latest prices (with max timestamp within the date) for the date.
If there is not any price for that particular date, return the latest previous price
There is no predefined ordering of the source table.
Try to preserve the column order.

```q
t: ([] date:raze (3#2016.01.06;4#2016.01.07;6#2016.01.08); sym:`a`b`c`a`b`a`b`a`b`c`a`b`c; price:1 2 3 1.1 2.1 1.2 2.2 1.3 2.3 3.2 1.4 2.4 3.3; timestamp:raze (3#2016.01.06T22:00:00.000; 2#2016.01.07T22:00:00.000; 2#2016.01.08T23:00:00.000; 3#2016.01.08T22:00:00.000; 3#2016.01.06T22:30:00.000))

Example 1:
f [t; 2016.01.06]

date      |sym|price| timestamp
---------------------------------------------
2016-01-06| a |  1  | 2016-01-06T22:00:00.000
2016-01-06| b |  2  | 2016-01-06T22:00:00.000
2016-01-06| c |  3  | 2016-01-06T22:00:00.000

Example 2:
f [t; 2016.01.07]

date      |sym|price| timestamp
---------------------------------------------
2016-01-06| c |  3  | 2016-01-06T22:00:00.000
2016-01-07| a | 1.2 | 2016-01-08T23:00:00.000
2016-01-07| b | 2.2 | 2016-01-08T23:00:00.000

Example 3:
f [t; 2016.01.08]

date      |sym|price| timestamp
---------------------------------------------
2016-01-08| a | 1.3 | 2016-01-08T22:00:00.000
2016-01-08| b | 2.3 | 2016-01-08T22:00:00.000
2016-01-08| c | 3.2 | 2016-01-08T22:00:00.000

f:{[t;d] select last price, max timestamp by date, sym from t where date<=d, timestamp=(max;timestamp) fby date, price=(last;price) fby sym}

/ select last price, max timestamp
/ set date, sym as keys
/ date <=d means look for previous day if current date doesnt satisfy query conditions
/ the FBY is the most important part of this problem. 
/ the ORDER of the FBY also matters a lot. 
/ you want to filter the LAST PRICE by sym, then
/ you want to filter the MAX TIMESTAMP by the date
```

<a name="qsql"></a>
### 🔴 qSQL
[Top](#top)

### [QSQL] Problem Set Aqua Q

```q
\l salestable.q
tables[]
`quote`sales`stock`trade

/ tables [] shows you what tables are within the script
```
```q
/ add new column to sales containing profit
/ profit = price * qty

update profit:price*quantity from `sales

trader product price quantity profit
------------------------------------
Bob	  pencil	3	 84	     252
Bob	  pen	3	 82	     246
Paul	  book	3	 64	     192
```
```q
/ work out total profit for each trader and product
/ (group by trader and product)

select sum profit by trader, product from sales

trader product profit
---------------------
Bob    book    79
Bob    paper   1353
Bob    pen     728

```
```q
/ sort by profit

select [<profit] profit:sum profit by trader, product from sales

trader product profit
---------------------
John   book	34
Bob    book	79
Paul   pencil	105
/ can also use xasc

`profit xasc select profit:sum profit by trader, product from sales

trader product profit
---------------------
John   book	34
Bob    book	79
Paul   pencil	105

/ or alternatively:

select [<profit] profit:sum quantity*price by trader, product from sales

trader product profit
---------------------
John   book	34
Bob    book	79
Paul   pencil	105

```

### [QSQL] Problem Set Aqua Q

```q
/ extract all the following results:
/ gender - male and grade - A
/ gender - female and grade - B
/ gender - female and grade - A

results:([]name:`John`Paul`Rachel`Jane`Emma;gender:"MMFFF";grade:"ABBAC")

name  |gender|grade
--------------------
John  |   M  | 	A
Paul  |   M  |	B
Rachel|   F  |	B
Jane  |   F  |	A
Emma  |   F  | 	C

/ individually this would be the syntax for each query

select from results where gender="M", grade="A"
select from results where gender="F", grade="B"
select from results where gender="F", grade="A"

/ however, can use a table search function
/ usually it goes: where col_name in value (where gender = "A")
/ so you can go where (table of col names) in (table of values)

select from results where ([]gender;grade) in ([] gender:"MFF";grade:"ABA")

name  |gender|grade
--------------------
John  |   M  | 	A
Rachel|   F  |	B
Jane  |   F  |	A
```

### [QSQL] Problem Set Aqua Q

```q
f:{([]subject:(4*x)#`maths`english`french`ict;class:raze 4#/:x?"ABCDE";gender:raze 4#/:x?"MF";mark:35+(4*x)?60;id:raze 4#/:til x)}
marks:f[300]

/2 find marks for class A
select from marks where class ="A"

/3 find marks for males of class B
select from marks where gender="M",mark="B"

/4 find avg french mark in class c
select avg mark from marks where class = "C", subject=`french

/5 find avg mark for each subject, ignoring classes
select avg mark by subject from marks

/6 for class A, produce table of avg, min, max and sd of math marks
select average:avg mark, low: min mark, high: max mark, sd:dev mark from marks where subject =`maths, class ="A"

/7 display lowest, median and highest mark according to gender and subject
select low:min mark, median:med mark, high: max mark by gender, subject from marks

/8 how many people are in each class (use id)?
select count distinct id by class from marks

/9 for class b ict marks, find med, range, sum of marks and num of distinct marks
select median:med mark, range:(max mark) - min mark, total: sum mark, num: count distinct mark from marks where class = "B", subject =`ict

/9 calc avg mark by subject for class E
select avg mark by subject from marks where class ="E"

/10 calc highest avg subject mark for class e, calling it topmark
select topmark: max mark from select avg mark by subject from marks where class = "E"  

/11 calc average mark for french in class d without using avg
select average:(sum mark % count mark) from marks where class="D", subject=`french

/12 calc the range of marks among males in class D in ict and french
select range:((max mark) - min mark) by subject from marks where class = "D", subject in `ict`french, gender="M"

/13 delete class E results
delete from marks where class="E"

/14 add 5 marks to each of class A french paper
update mark:5+mark from `marks where class="A",subject=`french

/15 add new col called average, contains average mark for class and subject
update average:avg mark by class, subject from marks 
```

### [func] More Complicated problem set - AquaQ

```q
/ 1 create function takes 3 parameters (startdate, enddate, symbols) which extracts the trade data 
/ for the date range and symbol list

tradeticks:{[startdate;enddate;symbols] 
            select date, sym, time, size, price 
            from trade
            where date within (startdate;enddate), sym in symbols}
            
tradeticks[2021.11.03;2021.11.04;`MS]

date      sym time         size  price
--------------------------------------
2021-11-03 MS 09:30:01.423 63000 58.46
2021-11-03 MS 09:30:01.768 95500 81.06
2021-11-03 MS 09:30:01.928 13400 82.90

/ hints:
/ date range = date within startdate/enddate
/ symbol list = sym in list of symbols
```
```q
/ 2.1 extracting temporal data from timestamp
/ assume table called depth

depth
time                       sym  price
-------------------------------------
2021-11-07T08:04:21.425000 YHOO 33.99
2021-11-07T08:14:59.215000 ORCL 35.16
2021-11-07T08:21:30.944000 NOK  42.01

meta depth

c    |t|f|a
------------
time	|p| |		
sym	|s| |g
bid1	| |f|		

/ time column is datatype p = timestamp

/ extract the timestamp

select time from depth

time
--------------------------
2021-11-07T08:04:21.425000
2021-11-07T08:14:59.215000
2021-11-07T08:21:30.944000

/ extract the date from timestamp

select `date$time from depth

time
----------
2021-11-07
2021-11-07
2021-11-07

/ extract the time from timestamp

select time.time from depth
select `time$time from depth

time
------------
08:04:21.425
08:14:59.215
08:21:30.944
```

```q
/2 create func2, which adds additional parameters: start time and end time. 
/ this func will only extract the trades that fall within time range
/ hint - need to extract the time portion from timestamp e.g time.time or `time$time

tradeticks2:{[startdate;enddate;symbols;starttime;endtime] 
            select date, sym, time, size, price 
            from trade
            where date within (startdate;enddate), sym in symbols,
            `time$time within (starttime;endtime)}

tradeticks2[2021.11.03;2021.11.04;`MS; 09:30:00;09:31:00]

date      sym time         size  price
--------------------------------------
2021-11-03 MS 09:30:17.569 11400 79.89
2021-11-03 MS 09:30:17.573 18400 96.09
2021-11-03 MS 09:30:21.264 8500 101.73

/ so in this case, time is in the temporal format of 2021.01.01D09:00:00
/ need to extract only the time portion
/ so that your argument inputs for starttime;endtime make sense
```
```q
/3 create function which is same as func1, but uses a start timestamp and end timestamp as the parameters
/ it should query across the date boundaries (should include all ticks within that period)
/ make sure it uses date partitions correctly. date portion should be run first and separately from timestamp query

tradeticks3:{[starttimestamp;endtimestamp;symbols] 
            select date, sym, time, size, price 
            from trade 
            where date within `date$(starttimestamp;endtimestamp), sym in symbols,
            time within (starttimestamp;endtimestamp)}

/ inputs are timestamps, which include date+time
/ need to filter first by date within the timestamp
/ then time within the timestamp

tradeticks3[2021.11.07D09:00;2021.11.07D10:00;`AAPL]

date       sym  time         size  price
----------------------------------------
2021-11-07 AAPL 09:30:21.088 20600 62.30
2021-11-07 AAPL 09:30:21.490 900   59.15
2021-11-07 AAPL 09:30:22.052 1500  95.94

```
```q
/ i dont get this

/4 Update func3 such that if the start timestamp is = first second of day, and end timestamp = last second of day
/ then it doesnt execute the where filter on the time column

/ hint start of day timestamp = 1d xbar timestamp or
/ `timestamp$00:00+`date$timestamp
/ to get endtime, subtract 1 from the start of next date
/ -1+`timestamp$1+`date$endtimestamp
tradeticks3:{[starttimestamp;endtimestamp;symbols] 
            $[starttimestamp=`timestamp$00:00+`date$starttimestamp)and
            (endtimestamp=-1+`timestamp$1+`date$endtimestamp);
            /call tradeticks
            tradeticks[`date\$starttimestamp;`date$endtimestamp;symbols];
            /call tradetick3
            tradeticks3[starttimestamp;endtimestamp;symbols]]}

```

<hr>

<a name="adverbs"></a>
### 🔴 Adverbs
[Top](#top)

### [adverb] What is an ADVERB?

```q
An adverb modifies an existing verb or function to alter how its applied to its arguments

x,'y / each both
x,\: y / each left
x,/: y / each right	
x \ y / scan
x / y / over
```

### [adverb] Each Both

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

### [adverb] Each Left
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

### [adverb] Each Right
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

### [adverb] Scan

```q
1 +\ 0 1 2 3

1 2 4 7

/ scan is an accumulating iterator.
/ returns the result of each result
```

### [adverb] Over

```q
1 +/ 0 1 2 3

7
/ over is an accumulating iterator
/ returns the final result
```

### [adverb] Create a function that calculates the moving sum with window size of 2

```q
/ each prior = perform action on each element with its prior element

L: 20 30 4 6 1 2
+': [L]
20 50 34 10 7 3

/ alternatively:

2 msum L

/ or 
 
{x+y}': [L]
 
```

### [adverb] Join the 2 lists together to form a nested list

```q
/ use each both to join 2 lists together

numbers: 5 7 9
powers: 8 3 4

numbers, 'powers
(5 8;7 3;9 4)
```

### [adverb] Raise the first element of list1 to first element of list2 and so on. 

```q
numbers xexp' powers
390625 343 6561f
```

### [adverb] A bank account pays 5% interest a year. Write a function that takes the current balance and returns the new balance after one year. Then use scan\ with that function to display the interest every year, up to 7 years in the future

```q
/ assume starting balance of 100

{x * 1.05} 100
105

{x * 1.05} \ [7; 100.]

105 
110.25
115.7625
...
140.71

/ use monadic version of scan that takes 2 arguments
/ first argument = how many times to run
/ second argument = starting value for function
```

### [adverb] Create a function, fib, that takes a fibonnaci sequence as its argument and returns the sequence complete with the next entry

```q
/ the fib seq = 1 + prior 
/ 1 1 2 3 5 8 ...

fib: {sum -2#x}
fib 1 1

1 1 2

/ take last 2 elements of argument and sum it
```

### [adverb] Use the over function to create a function, fibn, to generate a fib sequence n numbers long where n is the functions argument

```q
fibn: {x fib/ 1 1}
fibn 5
1 1 2 3 5 8 13
```

### [adverb] Use the scan to calculate the depreciation of cars 

```q
/ c = initial car value
/ r = depreciation rate per year

depr:{[c;r] c*1-r%100}
depr[100;8]
92

/ What is the value after 5 years?

depr[;8]\[5;100]
100
92
84.64
77.86
71.63
65.90

/ use scan to iterate the function 5x
```


<a name="attributes"></a>
### 🔴 Attributes
[Top](#top)


### [attribute] What are Attributes?

```q
Attributes describe how the underlying data in lists are structured.
This speeds up queries and optimizes memory usage.

1. Sorted 's#
2. Unique 'u#
3. Grouped 'g#
4. Parted 'p#
```

### [attribute] Sorted
```q
's#listname
requires elements to be sorted
allows binary search instead of fully scanning (much faster)
```
### [attribute] Unique
```q
'u#listname
requires elements to be unique
creates unique hash table in the background, allowing for constant time lookup of elements
```
### [attribute] Grouped
```q
'g#listname
a lookup table from each distinct value in the table is created to map to the positions where value occurs.
allows for much faster lookup
```
### [attribute] Parted
```q
'p#listname
requires all elements of same value to occur together
allows for faster queries
```

<a name="joins"></a>
### 🔴 Joins
[Top](#top)

### [join] What are some differences between left join and union join?

```q
A. (no match) nulls
      1. lj - if no match on key, then columns added to end of table, values = null
      2. uj - if no match on key, then row is REMOVED (no nulls)

B. Key
      1. lj - lookup table must be keyed
      2. uj - lookup table can be keyed or unkeyed

```
### [join-TS] Keyed UJ + xbar Problem Set

```q
/ union join + xbar example

/ calc avgmid price from quotes table for `GOOG

t1:select avgmid:avg .5*bid+ask by 5 xbar time.minute from quote where sym =`GOOG

/ avg mid quote = (bid + ask) /2
/ since you're grouping into 5 xbar, avg will calc avg over 5 min bucket
/ by = group, so this becomes keyed by 5 xbar time

minute| avgmid
--------------
09:30 | 79.7
09:35 |	80.4
09:40 |	79.5
09:45 |	79.4
09:50 |	80.4

/ calc avg price in 5 minute time window for `GOOG

t2:select avgprice: avg price by 5 xbar time.minute from trade where sym=`GOOG

/ notice some buckets have nulls = no trades during this bucket

minute| avgprice
----------------
09:30 | 80.0
09:35 |	
09:40 |	79.7
09:45 |	
09:50 |	80.4

/ combine the 2 tables together

t1 uj t2

minute| avgmid | avgprice
--------------------------
09:30 |  79.7  |  80.0
09:35 |	 80.4  |
09:40 |	 79.5  |  79.7
09:45 |	 79.4  |
09:50 |	 80.4  |  80.4

/ fill nulls with prev price (since no trades)

fills t1 uj t2

minute| avgmid | avgprice
--------------------------
09:30 |  79.7  |  80.0
09:35 |	 80.4  |  80.0
09:40 |	 79.5  |  79.7
09:45 |	 79.4  |  79.7
09:50 |	 80.4  |  80.4
```


```q
\l ex-joins.q

\a

/ **fbTrades** (headers = dt, sym, size, book)
/ **newsItems** (headers = ndate, ticker, title) 
/ **quote** (headers = date, time, sym, size, cond, bid, ask, asize, bside)
/ **stock** (headers = sym, sector, employees)
/ **trade** (headers = dt, sym, price, size)
```

### [join-TS] Find the total value of trades by sector, include sectors that are unknown (totalvalue = price x size)

```q
/ the columns you need are price x size (trade table) and sector (stock table) 
/ need to use left join because 1) include null sectors 2) union join would dupe values 
/ also - union join only works on tables. if you do meta trade + meta stock, you'll see stock = dictionary

trade lj stock
/ joins tables together, but does not calculate totalValue

dt        |sym|price|size|sector|employees
-------------------------------------------
2015-01-01|C  |	10.0| 10 | Fin  | 262000
2015-01-02|C  | 10.5| 100| Fin  | 262000
2015-01-04|DBK|	35.6| 55 |	|	


select totalvalue: price*size by sector from trade lj stock
/ can perform calc on joined tables

sector | totalValue
-------------------
	|,1,958
Fin	| 100 1,050 3,900 2,200 51,000 101,600f
Tech	| 20,200 306,000f

/ need to aggregate values so add in sum

select totalValue:sum price*size by sector from trade lj stock

sector   | totalValue
-------------------
         | 1958.0
`Fin`    | 159850.0
`Tech`   | 326200.0

/ amend blank null to "unknown"

select totalValue:sum price*size by `unknown^sector from trade lj stock

sector   | totalValue
-------------------
`Fin`    | 159850.0
`Tech`   | 326200.0
`unknown`| 1958.0

/ use `unknown^sector to rename the null sectors (visually more appeasing)
/ price * size will get you all the individual prices, but you want an aggregate figure. so need to use sum price
/ queried by sector, so this becomes keyed
```

<hr>

### [join-TS] Combine trade and fbTrades into a table t2, sorted by date. Include all columns

```q
/ include all columns, so we use union join
/ can't use lj since not keyed

t2: trade uj fbTrades

dt        |sym  |price |size|book
----------------------------------
2015-01-06|AAPL |1020.0| 300| 	
2015-01-07|MS	|254.0 | 400| 	
2015-01-02|FB	|      |1000| A
2015-01-03|FB	|      |1000| B
2015-01-05|FB	|      |1000| A

/ joins tables together, but doesnt sort by date

t2:`dt xasc trade uj fbTrades

dt        |sym  |price |size|book
---------------------------------
2015-01-02|FB	|      |1000| A
2015-01-03|FB	|      |1000| B
2015-01-05|FB	|      |1000| A
2015-01-06|AAPL |1020.0| 300|	
2015-01-07|MS	|254.0 | 400|	

/ `dt xasc sorts dates by ascending
/ since you are joining table together, no select query
```

<hr>

### [join-TS] Find the highest and lowest price in the trade table for each sym

```q
/ highest = max

select max price by sym from trade

sym | price
------------
AAPL| 1020.0
C   | 11.0
DBK | 35.6
MS  | 260.0

/ lowest = min

select min price by sym from trade

sym | price
-------------
AAPL| 1010.0
C   | 10.0
DBK | 35.6
MS  | 254.0
```

<hr>

### [join-TS] Find the 2 highest trade prices for each sym

```q

select price by sym from trade

sym | price
------------------
AAPL| 1,020 1,010f
C   | 10 10.5 11
DBK | ,35.6
MS  | 260 255 254f

/ this returns all prices grouped by sym

select 2 sublist desc price by sym from trade

sym | price
------------------
AAPL| 1,020 1,010f
C   | 11 10.5
DBK | ,35.6
MS  | 260 255f

/ sublist = creates a subset of a list
/ 2 sublist = takes 2 
/ desc price = sorts by high to low

ungroup select 2 sublist desc price by sym from trade

sym | price
------------------
AAPL| 1,020
AAPL| 1,010
C   | 11 
C   | 10.5
DBK | 35.6
MS  | 260
MS  | 255

/ if you use ungroup, you will break apart the by grouping

```

<hr>

### [join-TS] Find the average daily price for each sym in trade table. Join the newsItems table to show only those items where the sym had a newsItem on that date

```q

trade
dt        | sym |price |size
-----------------------------
2015-01-01| C   |10.0  | 10
2015-01-02| C   |10.5  | 100
2015-01-03| MS  |260.0 | 15
2015-01-04| C   |11.0  | 200
2015-01-04| DBK	|35.6  | 55
2015-01-05| AAPL|1010.0| 20
2015-01-06| AAPL|1020.0| 300
2015-01-07| MS	|255.0 | 200
2015-01-07| MS	|254.0 | 400

newsItems
ndate      | ticker | title
----------------------------------------------
2015-01-06 |   MS   | traders did it!
2015-01-04 |   C    | regulators investigating

/ from trade table, find avg price. then join the newsItem table where matches date and sym
/ so date and sym need to be keys in the newsItems table
/ notice the column headers are different in the newsItems table
/ for a ij, the column headers have to match up!

/ first step is calc the avg price grouped by dt, sym from trade table

t1: select avgprice: avg price by dt, sym from trade

dt        | sym | avgprice
---------------------------
2015-01-01| C   | 10.0
2015-01-02| C   | 10.5
2015-01-03| MS  | 260.0
2015-01-04| C   | 11.0
2015-01-04| DBK | 35.6
2015-01-05| AAPL| 1010.0
2015-01-06| AAPL| 1020.0
2015-01-07| MS  | 254.5

/ change column names for newsItems table + add keys to first 2 cols

t2: 2!`dt`sym xcol newsItems

dt         |  sym   | title
----------------------------------------------
2015-01-06 |   MS   | traders did it!
2015-01-04 |   C    | regulators investigating

/ then use an ij to join the 2 tables together

(select avg price by dt, sym from trade) ij (2!`dt`sym xcol newsItems)
/ or simply:
t1 ij t2

dt        | sym |price|title
----------------------------------------------
2015-01-04|  C  |11.0 |regulators investigating

/ inner join = only rows that match will be returned
/ need to set key to newsItems table in order for the ij to work
/ notice nothing joined for MS since the date didnt match
/ so only C was returned in the ij
```

<hr>

### [join TS] Take the newsItems table and join the trade table to bring in the latest price for each ticker

```q
newsItems
ndate      | ticker | title
----------------------------------------------
2015-01-06 |   MS   | traders did it!
2015-01-04 |   C    | regulators investigating

trade
dt        | sym |price |size
-----------------------------
2015-01-01| C   |10.0  | 10
2015-01-02| C   |10.5  | 100
2015-01-03| MS  |260.0 | 15
2015-01-04| C   |11.0  | 200
2015-01-04| DBK	|35.6  | 55
2015-01-05| AAPL|1010.0| 20
2015-01-06| AAPL|1020.0| 300
2015-01-07| MS	|255.0 | 200
2015-01-07| MS	|254.0 | 400

/ take newsItem table, join the trade table to add column for latest price
/ need to amend columns of newsItems to match trade table (dt, ticker)

`dt`sym xcol newsItems

dt         |  sym   | title
----------------------------------------------
2015-01-06 |   MS   | traders did it!
2015-01-04 |   C    | regulators investigating

/ need to key the sym column for trade table

/ since they want the latest price, 2015.01.03 = no trades for MS
/ so we need to retrieve the last price
/ easiest way to do this is to sort by `dt ascending
/ so the ij will automatically take the last price
/ luckily table is already sorted by ascending, but just in case:

`dt xasc `sym xkey trade

sym     dt              price   size
-------------------------------------
C	2015-01-01	10.0	10
C	2015-01-02	10.5	100
MS	2015-01-03	260.0	15
C	2015-01-04	11.0	200
DBK	2015-01-04	35.6	55
AAPL	2015-01-05	1010.0	20
AAPL	2015-01-06	1020.0	300
MS	2015-01-07	255.0	200
MS	2015-01-07	254.0	400

/ join the table via inner join

(`dt`sym xcol newsItems) ij (`dt xasc`sym xkey trade)

dt         |  sym   | title                   | price| size
------------------------------------------------------------
2015-01-06 |   MS   | traders did it!         | 260 | 15 
2015-01-04 |   C    | regulators investigating| 10  | 10

/ then you can delete the size column

delete size from (`dt`sym xcol newsItems) ij (`dt xasc`sym xkey trade)

dt         |  sym   | title                   | price
------------------------------------------------------
2015-01-06 |   MS   | traders did it!         | 260 
2015-01-04 |   C    | regulators investigating| 10  
```

```q
/ alternative solution: as of join method

/ quick 101
/ aj [`col_1`col_2; soure_table; `col_1`col_2 lookup_table]

/ last item of columns will be less than or equal join
/ aj looks for values (columns) from source to lookup table and pulls in the most recent price

aj [`ticker`ndate;newsItems; `ndate`ticker xcol trade]

/ from newsItems table, retrieve values in columns `ticker and `ndate
/ look for matches in trade table, rename dt to `ndate and sym to `ticker
/ it will pull in the most recent values in the matching columns (price, size)

dt         |  sym   | title                   | price| size
------------------------------------------------------------
2015-01-06 |   MS   | traders did it!         | 260 | 15 
2015-01-04 |   C    | regulators investigating| 10  | 10

/ delete the size column

delete size from aj [`ticker`ndate;newsItems; `ndate`ticker xcol trade]

dt         |  sym   | title                   | price
------------------------------------------------------
2015-01-06 |   MS   | traders did it!         | 260 
2015-01-04 |   C    | regulators investigating| 10  
```

[Top](#top)
