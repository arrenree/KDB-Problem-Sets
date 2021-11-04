# Allen's KDB Practice Problems
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

### Define the following variables

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

### Cast the Following

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

### Get today's date store it as variable d

```q
d: .z.d
2021-11-01d
```

### Calculate the number of days since last christmas

```q
d-2020.12.25
311i

/ can use algebra with dates (ints underneath)
```

### What day of the week was Jan 10, 2011?

```q
2011.01.10 mod 7
2i

/ since dates start on sunday, 2 days from sunday = Monday

.z.d mod 7
2i

/ todays date = monday, Nov 11
/ 2 days from sunday = Monday
```

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

### show all variables definied in current session of q

```q
\v
`a`b`c`d
```

### Close the current session
```q
\\
```

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

### Create Empty List d
```q

d: ()

/ redefine d to be empty list of type integer

d: `int $ ()

/ add 5 random elements to d

d, 5 ? til 10

/ 5?til 10 = randomly select 5 numbers from 0-9
/ d , joins these 2 lists, thereby adding into list
```

### Create list e with 1 element

```q

e: enlist 10

/ have to use enlist on single elements
/ or e:(), 10
```

### Create list l with 20 random values from 3 to 30
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

### Add each element of l to its index position. for ex, 0 to index 0, 1 to index 1, etc.

```q
l+: til count l

/ count l = 20 elements in list l
/ til 20 = 0 - 19, gives you the index position
/ so now you have 2 lists, just need to add together
```
### How many even numbers are there? 

```q

l mod 2
1 1 0 1 0 1 1 0 0 1 0 1 0 1 0 1 0 1 1 0

/ mod 2 tells us when the remainder is
/ so 0 = no remainder = even number
/ now need to count the 0s

count where not l mod 2

/ not = 0, so counts all the 0s (even numbers)
```

### what do you get dates when casting int to date?

```q

dates are stored as integers (days) from 2000.01.01
```

### Creating Matrix

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

### Nested Lists

```q

nest: (1 2 3; `a`c`b;10 11 12 14f; 100011b)

/ find the datatype of each row

type each nest

/ collapse this nested list

raze nest
```

### Define strings s1: "Hello" and s2: "Wrold"

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


### Dictionary Problem Set AquaQ

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
### Dictionary Problem Set (AquaQ)

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

### Tables Problem Set 2 AQ

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


### Tables Problem Set AQ
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

### Functions Problem Set AQUA Q
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

### QSQL Problem Set Aqua Q

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

### QSQL Problem Set Aqua Q

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
