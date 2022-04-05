# Allen's KDB Practice Problems + Solutions
<a name="top"></a>

1. [General Knowledge / System](#gen)
2. [Casting / Datatypes / Temporal/ Enumeration](#cast)
3. [Lists](#list)
4. [Dictionary](#dictionary)
5. [Tables](#tables)
6. [Keyed Tables](#key_table)
7. [Foreign Key Restrictions](#fkey_table)
8. [Functions](#functions)
	1. [Intro to Functions](#func_intro)
	2. [Functions on Strings - AQ](#func_strings)
	3. [Projected Functions - TS](#func_proj)
	4. [Function Loop Problem Set - TS](#func_loop)
	5. [Prime Numbers Problem Set - TS](#func_prime)
	6. [Function Problem Set 1 - TS](#func_set1TS)
	7. [Functions Problem Set 1 (easy) - AQ](#func_set1AQ)
	8. [Functions Problem Set 2 (med) - AQ](#func_set2AQ)
	9. [Functions Problem Set 3 (med/hard) - AQ](#func_set3AQ)
	10. [Functions Problem Set 4 - AQ](#func_set4AQ)
	11. [Int Problem Set 1 - GS](#func_int1)
	12. [Int Problem Set 2 - GS](#func_int2)
10. [qSQL](#qsql)
	1. [QSQL Problem Set 1 - TS](#sql_1)
	2. [QSQL Problem Set 2 - TS](#sql_2)
	3. [xbar Problem Set - TS](#sql_3)
	4. [fby Problem Set](#sql_4)
	5. [QSQL Problem Set 3 - TS](#sql_5)
	6. [Table Query Problem Set 1](#sql_6)
	7. [Table Query Problem Set 2](#sql_7)
	8. [Table Query Problem Set 3](#sql_8)
	9. [BIN Problem Set](#sql_9)
	10. [Signum Deltas Problem Set](#sql_10)
	11. [Select vs Exec Example](#sql_11)
	12. [Deltas/Differ Problem Set](#sql_12)
	13. [QSQL Problem Set 1 - AQ](#sql_13)
	14. [QSQL Problem Set 2 - AQ](#sql_14)
	15. [Nested Tables Problem Set](#sql_15)
12. [Adverbs](#adverbs)
13. [Attributes](#attributes)
14. [Joins](#joins)
15. [@ & . Operator](#at)
16. [Racking & Alignment](racking)

<hr>

<a name="gen"></a>
### 🔴 1. General Knowledge / System
[Top](#top)

### [gen] What is an Atom vs a List?

```q
atom 
/ is an irreducible value of a specific data type

"a" / char atom
`sym / sym atom

list
/ is an ordered sequence of items
```

### [gen] What is the difference between a sym and a string?

```q
sym
/ is an atomic entity holding text 
/ represented with a back tick ` 
/ smaller in size than a char

`sym / sym atom
`one`two`three / sym vector

String 
/ list of chars
/ represented by " " double parathesis

"the quick brown fox" / string aka char vector

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

### [gen] What is a dictionary vs a table? 

```q
Dictionaries
/ are data structures that map from a domain of keys to a range of values 
/ contains a ! to separate keys and values
/ flip a dictionary and you get a table

Tables
/ is a list of dictionaries (flipped)
/ any single row is a dictionary
/ tables are ordered, which means you can index them
/ tables are encased by parathesis ( ) and contain brackets [ ] which assigns the key.
```

### [system] Show all variables defined in current session of q

```q
\v
`a`b`c`d
```

### [system] Close the current session
```q
\\
```

### [gen] What is the difference between equals = and match ~

```q
/ equals will match on value, but not datatype
/ match will match on both value and datatype

4 = 4.0
1b / true

/ = will match on values, but not datatype
/ 4 int = 4 float

4 ~ 4.0
0b / false. match is a lot more strict.
/ ~ will match on both value + datatype
```

### [gen] What is 2 | 5

```q
5

/ larger of x | y
```

### [gen] What is 2 & 5

```q
2

/ amper = smaller of x & y
```

### [gen] What is 2 cut 1 2 3 4 5 6

```q
(1 2; 3 4; 5 6)

/ cuts list into elements of 2
/ x cut y
/ y = list
```

### [gen] What is 1 4 cut 1 2 3 4 5 6

```q
(2 3 4; 5 6)

/ 2nd element (4) = cut list by 4
/ first element (1) = AFTER cutting, then drop everything before this element (1) from output
```

### [gen] What is 2 3 cut 1 2 3 4 5 6

```q
(3; 4 5 6)

/ 2nd element (3) = cut list into elements of 3
/ 1st element (2) = drop all elements before 2
```
### [gen] What is signum -2 0 1 3

```q
-1 0 1 1

/ neg, 0, pos pos
```
### [gen] What is 1 cross 3 4?

```q
1 3
1 4

/ returns all possible combinations of x cross y
/ note - does NOT multiply or add
```

### [gen] Cross Lists + Tables

```q
s:`IBM`MSFT
v: 1 2

s cross v
((`ibm;1);(`ibm;2);(`apple;1);(`apple;2))

/ returns a list of tuples
```

```q
s:`IBM`MSFT
v: 1 2

([] s) cross ([] v)

s     | v
----------
ibm   | 1
ibm   | 2
apple | 1
apple | 2
```

```q
/ building xbar timeseries

time: 09:00 09:15
sym: `GOOG`IBM

([]sym) cross ([]time)

sym  | time
-----------
GOOG | 09:00
GOOG | 09:15
 IBM | 09:00
 IBM | 09:15
```

### [system] How do you read a txt file?

```q
/ assume txt file named test.txt

hopen `:test.txt
read0 `:test.txt

/ hopen = opens the txt file
/ read0 = reads the txt file
```

### [system] How do you Open and Edit a txt file?

```q
fh: hopen `:hi.txt
fh "10"
fh "20"
neg[fh] "30"
read0 `:hi.txt

"1020"
"30"

/ fh = temp ref number that OS assigns to file requested to be opened
/ neg[fh] = enter new line
/ read0 = reads the txt file
/ hclose fh = closes file hand so you can no longer edit it
```

### [system] How do you load a file with column headers?

```q
/ With Column Headers

/ if a delimiter is enlisted, the first row of the csv file is read as a column header

("SSJ"; enlist",")0: `sample.csv

/ 0: function prepares, saves, and loads text files
/ "SSJ" = sym, sym, long
/ enlist "," = delimiter = what separates each column
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
0700.HK|Buy |500|   Sell   |	  100     |	400
9988.HK|Buy |500|   Sell   |	  100     |	400
0001.HK|Buy |500|   Sell   |	  100     |	400

A2: select from A where crossableqty > 0

ric    |side|qty|brokerside|brokerquantity|crossableqty
-------------------------------------------------------
1810.HK|Buy |500|   Sell   |    100     |	400
0700.HK|Buy |500|   Sell   |    100     |	400
9988.HK|Buy |500|   Sell   |    100     |	400
0001.HK|Buy |500|   Sell   |    100     |	400

select ric, side, crossableqty from A2

ric    |brokerside | brokerquantity
---------------------------------
1810.HK|    Buy    |	400
0700.HK|    Buy    |	400
9988.HK|    Buy    |	400
0001.HK|    Buy    |	400

/ this is the end result. these are the lines where you can cross 
```
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
### 🔴 2. Casting / Datatypes / Temporal
[Top](#top)

### [datatype] What is a negative datatype?

```q
/ a negative type is an atom
/ a positive type is for everything else (ie, a list)

type 5
-7h

/ integer atom

type 2 3 4
7h

/ integer vector
```

### [cast] What is casting?
```q
casting converts one datatype to another
```

### [cast] Show 3 ways to conver FLOAT 4.5 to an INT
```q
`int$4.5
"i"$4.5
6h$4.5
```

### [cast] What happens when you cast a DATE to an INT?

```q
`int$2000.10.04
3

/ casts as dates from 2000.01.01
```

### [cast] Convert SYMS a b c to a STRING

```q
string `a`b`c
("a","b","c")

/ simply use the string function
```

### [cast] How do you cast CHARS "a","b","c" to a SYM?

```q

/ a string is a list of chars

`$"a","b","c"
"S"$"a","b","c"
`abc
```

### [cast] Cast the Following

```q
/1. Cast STRING "2014.01.01" to a DATE

"D" $ "2014.01.01"
-14h

/ "2014.01.01" was originally a string
/ use capital "D" to cast strings to date
```

```q
/2. Cast SYM `2013.01.01 to DATE

"D" $ string `2013.01.01

/ `2013.01.01 is a sym
/ requires first to cast to STRING, then cast to DATE
```

```q
/3. Cast FLOAT 3.14 to an INT

`int $ 3.14 
3

/ note rounding for ints
/ alternatively "I" $ 3.14
```

```q
/4. Cast STRING "abcde" to a SYM

`$"abcde"

/ can simply use backtick to cast to sym
```

### [cast] What is parsing?

```q
/ parsing is converting a string to another datatype.
```

### [cast] Given mixed list L: ("100.1";"hello";"10"), convert elements to float, char, and int
```q
l:("1.00001"; "200"; "3.1417")
"FIF"$l

1.00001 / float
200 / int
3.1417 / float
```

### [cast] Given strings "2001.02.02" and "2003.08.09", parse the strings into KDB dates
```q
"D"$("2001.02.02";"2003.08.09")

/ these are strings which you are trying to parse into the date datatype
/ have to use upper case when parsing
```

### [cast] why do you get dates when casting int to date?

```q
/ dates are stored as integers (days) from 2000.01.01
```

### [temporal] Get today's date store it as variable d

```q
d: .z.d
2021-11-01d
```

### [temporal] Calculate the number of days since last christmas

```q
d - 2020.12.25
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

### [temporal] How many days were there in 2004?

```
2005.01.01 - 2004.01.01
366
```

### [string] Define strings s1: "Hello" and s2: "World"

```q
s1: "hello"
s2: "world"
```

```q
/2. join the 2 strings together and save to s

s:s1, " ",s2
"hello world"
```

```q
/3. find index position of "w"

s?"w"
6

/ utilize the ? find operator to search index position within string
```

```q
/4. find index positions of all "l" in s

ss[s;"l"]
2 3 9

/ ss = search string function. returns index position
```

```q
/5. find index position of last l

last ss[s;"l"]
```

```q
/6. remove "hello" and add " of warcraft" to s

ssr["hello world"; "hello ";""], " of warcraft"
world of warcraft

/ ssr = string search replace
/ hello world = string
/ hello = what you want to replace
/ "" = replacing with blank (delete)
/ then you are joining a string , of warcraft

ssr[s;"hello ";""], " of warcraft"
world of warcraft
```

```q
/7. Find index location for "ryan" in "hello ryan where is ryan"

"hello ryan where is ryan" ss "ryan"
6 20

/ ss = string search
/ returns index location
/ ryan appears twice; at the 6th and 20th index location
```

```q
/8. Replace "ryan" with "john"

ssr["hello ryan where is ryan";"ryan";"john"]
hello johhn where is john

/ ssr = search string replace function
/ first arg = input string
/ second arg = what to replace
/ third arg = what to replace with
```


### [enumeration] Create an enumeration t2 containing values p q r that is restricted to domain t1

```q
t1: `symbol$()
t2: `t1$`p`q`r

/ t2 is now an enumeration which only contain domain t1 (syms)
```

### [enumeration] Insert new value `u into t2

```q
t2,:`u
error

/ since t2 is restricted to domain t1, need to first add `u into t1 before adding to t2

t1,:`u
t2,:`u
`p`q`r`u

/ now it works
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

### [datatype] How do you convert a list of syms to strings?

```q
string `a`b`c
"a","b","c"
```

### [cast] How do you convert a list of syms to a list of chars?

```q
raze string `a`b`c
"abc"

/ sym to string, then string to char
/ use raze function to collapse 1 layer
```

<hr>

<a name="list"></a>
### 🔴 3. Lists
[Top](#top)

### [list] Creating Lists

```q
/1. Create a list of 1 to 10

1 + til 10
1 2 3 4 5 6 7 8 9 10
```

```q
/2. Create a list of 10 even numbers

2 * 1 + til 10
2 4 6 8 10 12 14 16 18

/ til 10 = 0 1 2 3
/ +1 = 1 2 3 4 5
/ *2 = 2 4 6 8 etc.
```

```q
/3. Create a list of 10 odd numbers

1 + 2 * til 10
1 3 5 7 9 11 13 15 17 19

/ 2 * til 10 = 0 2 4 6..
/ +1 = 1 3 5 7...
```

```q
/4. Obtain the first 10 even numbers starting from 42

42 + 2 * til 10
42 44 46 48 50 52 54 56 58 60
```

### [list] Drop item at index position x

```q
/ drop item from list at index position 2

k: 1 2 3 4
k _ 2

/ if you put LIST _ x
/ then it will remove item from index position x from list
```

### [list] Sublist

```q
5 sublist 1 2 3
1 2 3

/ sublist is like take, but ONLY takes whats available
/ does not wrap around
```

```q
2 2 sublist 1 2 3 4 5 6
3 4

/ from index position 2, take 2 elements
```


### [list] Problem Set (easy)

```q
/1 create Empty List d

d: ()
```
```q
/2 redefine d to be empty list of type integer

d: `int $ ()
```
```q
/3  add 5 random elements to d

d, 5 ? til 10

/ 5 ? til 10 = randomly select 5 numbers from 0-9
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
```
```q
/2 find the 20th number in list l

l[19]

/ use indexing to retrieve 19th index position = 20th number
/ since starts on 0
```

```q
/3 are any of these numbers in the list? 3 5 7 11 13 17

3 5 7 11 13 17 in l
0011001

/ will return list of booleans
```

### [list] Add each element of l to its index position. for ex, 0 to index 0, 1 to index 1, etc.

```q
l+: til count l

/ count l = 20 elements in list l
/ til 20 = 0 - 19, gives you the index position
/ so now you have 2 lists, just need to add together
```
```q
/2 How many even numbers are there? 

l mod 2
1 1 0 1 0 1 1 0 0 1 0 1 0 1 0 1 0 1 1 0

/ returns a list of booleans
/ mod 2 tells us when the remainder is
/ so 0 = no remainder = even number
/ now need to count the 0s

count where not l mod 2

/ not = 0, so counts all the 0s (even numbers)
```
### [list] Matrix Problem Set

```q
m:(1 2 3; 4 5 6; 7 8 9)
1 2 3
4 5 6
7 8 9

/1 get middle column of m and save it as new variable a

a: m[;1]

/ [row;column]
/ blank for row; 1 = index position 2, so 2nd row
```

```q
/2 replace middle row of m with a

m[1]:a

/ [row;column] 
/ index position 1 = 2nd row
```

```q
/3 transpose m and store as mm

mm: flip m

/ transpose is a fancy way of saying flip
```

```q
/4 join extra row to mm, consisting of all 10s

mm,: 3#10

/ the syntax ,: appends items to list
```

### [list] Nested Lists

```q

nest: (1 2 3; `a`c`b;10 11 12 14f; 100011b)

/1 find the datatype of each row

type each nest
```
```q
/2 collapse this nested list

raze nest
```

### [list] Calculate the average size where price is greater than 5

```q
size: 100 300 50 70
price: 4 8 6 2

avg size where price > 5
```

### [list] List Problem Set AQ
```q
games:`crash`streets`echo`crash2`sonic`micro`pokemon`supermario`bomber`zelda
platform: `ps1`sega`sega`ps1`sega`ps1`gameboy`gameboy`sega`gameboy
level: (7 9 6i; 2 5i; 4 4i; 10 2 1i; 1 10i; 8i; 0 3i; 6 0i; 8 4i; 1 10i)

/1 count number of users per game

users: count each level
3 2 2 3 2 1 2 2 2 2
```
```q
/2 calc average user level each game

userlevel: avg each level
7.3 3.5 4 4.3 5.5 8 1.5 3 6 5.5
```

```q
/3 create boolean list indicating where avg user level > 6

6 < avg each level
1000010000b

/ or

userlevel > 6
1000010000
```

```q
/4 calc games where avg user level > 6

games where 6 < avg each level
`crash`micro
```

```q
/5 sum the users for each platform. which one most popular?

sum users where platform in `ps1
sum users where platform in `sega
sum users where platform in `gameboy

/ sum the total count where column platform = ps1, etc.
```

### [list] what is the difference between 3 ? 10 and 3 ? 10 20 30

```q
/ atom ? atom
3 ? 10

/ returns 3 random numbers from 0-9

/ atom ? list
3 ? 10 20 30
10 10 30

/ returns 3 random numbers from the list
```

### [list] List Problem Set - TS

```q
/1. Retrieve the first 3 items from list p

p: 100 200 300 400 500 600
t: "say hello world to bob"
m: (1 2 3; 10 20 30; 100 200 300)

3#p
100 200 300

/ use # take function to retrieve items from list
```

```q
/2. From t, retrieve the list "sold"

t?"sold"
0 8 6 14

/ find the index position where the character exists

t[0 8 6 14]
"sold"

/ then retrieve it using indexing to return "sold"
```

```q
/3. Create the nested list ("shoot";"bob") by indexing into t

t?"shoot"
0 4 8 8 16

/ find index positions of each element in string "shoot"

t? "bob"
19 8 19

/ find index positions of each element in string "bob"

t(0 4 8 8 16; 19 8 19)
("shoot";"bob")

/ you are finding the index locations of those chars from list t
/ then retrieving those index positions (letters) to spell out 
/ retrieve values using index position of a nested list
/ notice use parathesis ( ) instead of square bracket [ ]
```

```q
/4. Change the last number in p to 1000

p[5]: 1000
/ upsert. find index location 5, replace value with 1000
```

```q
/5. Find the 3 highest numbers in p

3#desc p
100 500 400

/ take 3 numbers from descending list p
```

```q
/6. Find values of p that are below the mean

p where p < avg p
100 200 300 400
```

```q
/7. Given list L and K, find the common numbers in both lists
l: 7 5 13 20 19 17 30 
k: 7 17 200 300 400 1000 

l inter k
7 17

/ inter = finds same values in x inter y
```

```q
/8. Find the sum of the first 5 numbers in l

l: 7 5 13 20 19 17 30

sum 5#l
64

/ take first 5 numbers from l
/ then sum them together
```

```q
/9. Find the result when you remove the last 2 items from k

k: 7 17 200 300 400 1000

-2_k
7 17 200 300

/ drop last 2 items from k
```

```q
/10. Return only numbers in l that are wholly divisible by 5

l: 7 5 13 20 19 17 30 

l mod 5
2 0 3 0 4 2 0

/ returns remainder where l divide by 5
/ 0 means fully divisible

l where not l mod 5
5 20 30

/ l where not l mod 5 = 

/ return value where l mod 5 = 0
/ not l mod 5 will return the values at 0
```

```q
/11. Subtract the average of list l from max value in list k

max[k] - avg [l] 
984.14

/ or also:

max k - avg l
9784.14
```

```q
/12. Generate list p of 1000 random integers between 0 and 100.
Find all values in p that are square numbers

p: 1000?100
a: sqrt p

/ a = list containing square roots of every number in p
/ a will contain both ints and floats

a = `int$a

/ cast a as an integer (whole number)
/ since a is made up ints and floats

p where a=`int$a

/ return value in p where a = whole number (square numbers)

count p where a=`int$a

/ count number of p = square numbers
```
### [list] Find ? List Questions

```q
1 2 3 4 5 ? 3
2

/ find index position of 3
/ list ? x 
/ retrieves index position of x
```

```q
1 2 3 4 5 ? 7
5

/ find index position of 7
/ not found (out of range), returns max index + 1
/ 4 (max index position) + 1 = 5
```

```q
1 2 2 3 4 ? 2
1

/ find index position of 2
/ multiple occurence, only returns first
```


<a name="dictionary"></a>
### 🔴 4. Dictionary
[Top](#top)

### [dict] What is a dictionary?
```q
a dictionary is a data structure that maps domains to a range of values. The keys and values are separated by !
```

### [dict] How to retrieve values as a dictionary?

```q
/ have to use take #

d: `a`b`c!1 2 3

Key | Value
-----------
a   |	1
b   |	2
c   |	3

`a`b#d

Key | Value
------------
a   |	1
b   |	2

/ when retrieve using take #, result is a dictionary
```

### [dict] How to retrieve single item as dictionary?

```q
/ have to use enlist

d: `a`b`c!1 2 3

Key | Value
------------
a   |	1
b   |	2
c   |	3

(enlist `a)#d

Key | Value
-----------
a   |	1
```

### [dict] Dictionary Problem Set 1 (easy) TS

```q
/1. given the below dictionary, find the type, the keys, and its values

d:`p`q`r`s!10 20 40 100

key|value
---------
p  | 10
q  | 20
r  | 40
s  | 100

type d
99h

key d
p q r s

value d
10 20 40 100
```

```q
/2. add new entry u 200 to dict d

d[`u]: 200

key|value
---------
p  | 10
q  | 20
r  | 40
s  | 100
u  | 200

/ upsert. will update if key exists, if not, will append it
```

```q
/3. Change value of p to 2

d[`p]:2

key|value
---------
p  | 2
q  | 20
r  | 40
s  | 100
u  | 200
```

```q
/4. Create dictionary d2, by TAKING values of p q r from dictionary d

d2:`p`q`r#d

key|value
---------
p  | 2
q  | 20
r  | 40

/ when TAKE # from dict, output is a dict contains both keys + values
```

```q
/5. Find common keys in d and d2, and retrieve keys + values from combined d+d2

d+d2

key|value
---------
p  | 4
q  | 40
r  | 80
s  | 100
u  | 200

/ adds all values together where there is a match in keys
```

```q
d inter d2
2 20 40

/ dict inter dict will return values occuring in both dicts
/ but you want to return both keys + values, not just values
```

```q
key[d] inter key[d2]
(key d) inter (key d2)

`p`q`r

/ retrieve keys in both d and d2
/ inter = retrieves common values 
/ so this will return the keys in both dict
```

```q
/ now that you know the common keys, use TAKE
/ to retrieve a dict from combined d + d2

(key[d] inter key[d2]) # d + d2
((key d) inter (key d2)) # (d + d2)


key|value
---------
p  | 4
q  | 40
r  | 80

/ combining together, you take the keys occuring in both dict from d1 + d2
/ and show its values
```

### [dict] Dictionary Problem Set 2 (Easy) - TS

```q
/1. Given the 2 dictionaries below, find those who are greater than 1.7m in height

dheight:`john`mark`luke`paul`ian`peter!1.5 1.6 1.7 1.8 1.9 1.4
dweight:`john`mark`luke`paul`ian`peter!81 72 88 91 55 110

dheight
key  | value
------------
john | 1.5
mark | 1.6
luke | 1.7
paul | 1.8
ian  | 1.9
peter| 1.4

dweight
key  | value
------------
john | 81
mark | 72
luke | 88
paul | 91
ian  | 55
peter| 110

dheight > 1.7
/ comparison operator on a dict returns a table of booleans

key  |value
-----------
john | 0b
mark | 0b
luke | 0b
paul | 1b
ian  | 1b
peter| 0b

where dheight > 1.7
paul ian

/ where = returns the keys
```

```q
/2. Find the average height of people who weight over 90

where dweight > 90
paul peter

dheight where dweight > 90
1.8 1.4

avg dheight where dweight > 90
1.6
```

### [dict] Nested Dictionaries Problem Set

```q
d: `alpha`bravo`charlie ! ((1 2 3);(4 5 6);(7 8 9))

key     | value
----------------
alpha	| 1 2 3
bravo	| 4 5 6
charlie	| 7 8 9
```

```q
/1. add 2 new rows: delta, echo with 10 11 12 and 13 14 15, respectively

/ UPSERT method

d[`delta, `echo]: ((10, 11, 12); (13, 14, 15))

key     | value
----------------
alpha	| 1 2 3
bravo	| 4 5 6
charlie	| 7 8 9
delta   | 10 11 12
echo    | 13 14 15

/ upsert method you "index" new key [`echo] and assign new values 13, 14, 15
/ adds key since doesnt exist, along with new values
```

```q
/ JOIN ASSIGN method

d,:(`delta`echo)!((10 11 12);(13 14 15))

key     | value
----------------
alpha	| 1 2 3
bravo	| 4 5 6
charlie	| 7 8 9
delta   | 10 11 12
echo    | 13 14 15

/ join assign = you JOIN a dict, so needs !
/ ,: join assign updates the underlying table

```

```q
/2. add 1 new row: golf with value 100

/ UPSERT method

d[enlist `golf]: 100

key     | value
----------------
alpha	| 1 2 3
bravo	| 4 5 6
charlie	| 7 8 9
delta   | 10 11 12
echo    | 13 14 15
golf    | 100

/ need enlist since upserting single row
/ enlist only for KEY, no need for value
```

```q
/ JOIN ASSIGN method

d,: (enlist `golf)!(enlist 100)

key     | value
----------------
alpha	| 1 2 3
bravo	| 4 5 6
charlie	| 7 8 9
delta   | 10 11 12
echo    | 13 14 15
golf    | 100

/ join assign = need to add in dict! so need bang !
/ need to use enlist if adding single row to dictionary
```

```q
/3. Calculate the average value per column (per column in values)

key     | value
----------------
alpha	| 1 2 3
bravo	| 4 5 6
charlie	| 7 8 9

avg d
33.5 34.2 35

/ avg + dictionary name = average value per column
/ since values are kinda like a matrix, with 3 columns
```

```q
/4. Calculate the average value per row

avg each d

key     | value
----------------
alpha	| 2
bravo	| 5
charlie	| 8
delta   | 11
echo    | 14
golf    | 100

/ avg each + dictionary name = average value per row
```

### [dict] How do you upsert different keys/values from the original dict's datatype?

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

### [dict] What happens when you try retrieving from a dictionary that has non-unique keys?

```q
d: `a`b`c`a!1 2 3 4
d[`a] = 1 

/ returns the first entry
```

### [dict] Take first 2 items from dict. Retrieve value from key 'c

```q
d: `a`b`c!1 2 3
2 # d 

/ returns a dictionary of first 2 rows

(enlist `c) # d 

key | value
---------
c   | 3

/ have to use enlist when retrieving single domain
```

### [dict] Dictionary Problem Set 1 AquaQ

```q

d1: `london`paris`athens`toronto`sydney`tokyo`chicago!0 1 2 -5 9 8 -6

key     | value
---------------
london  | 0
paris	| 1
athens	| 2
toronto	|-5
sydney	| 9
tokyo	| 8
chicago	|-6
```

[dict] 1. Extract the hours for tokyo and athens

```q
d1[`tokyo`athens]
8 2

/ or

`tokyo`athens # d1

key    | value
---------------
tokyo  | 8
athens | 2

/ when you perform take # on dictionary, returns a dictionary
```

[dict] 2. If it's 12:30 in Paris, what time is it in Chicago?

```q
(d1`paris)-d1`chicago
7

d1[`paris]-d1[`chicago]
7

/ paris vs chicago 7 hour difference
/ need to convert to hours (cuz 7 is just a long)

((d1`paris) - d1`chicago)*01:00
07:00u

(d1[`paris]-d1[`chicago])*01:00
07:00u

/ then calculate difference from 12:30 (paris)

12:30 - 07:00
05:30u

12:30 - (((d1`paris) - d1`chicago)*01:00)
05:30u

/ final answer
/ alternatively syntax could be:

12:30 + 01:00 *(d1`chicago)-d1`paris
05:30u

/ right to left
```

[dict] 3. change London's time from 0 to 1

```q
d1[`london]:1
```

[dict] 4. add in rome with value of +1

```q
/ UPSERT method

d1[`rome]:1

/ JOIN ASSIGN method

d1,:(enlist `rome)!enlist 1

/ when using join assign, must enlist if single atom!
```

### [dict] Dictionary Problem Set 2 AquaQ

```q
Given:

d3:`belfast`cardiff`edinburg`london!(12 10 11 9; 11 10 10 10; 10 10 12 9; 15 12)

Key	 | Value
----------------------
belfast	 | 12 10 11 9
cardiff	 | 11 10 10 10
edinburg | 10 10 12 9
london	 | 15 12
```

[dict] 1. What's the average temp in each city?

```q
avg each d3

Key	Value
----------------
belfast	 | 10.5
cardiff	 | 10.25
edinburg | 10.25
london	 | 13.5

/ avg each returns average of each key
```

[dict] 2. Convert all temp from C to F (temp x 9/5 + 32)

```q
(d3* (9%5) ) + 32

Key	 | Value
--------------------------------
belfast	 | 405.6 338 371.8 304.2
cardiff	 | 371.8 338 338 338
edinburg | 338 338 405.6 304.2
london	 | 507 405.6

/ you can amend ALL values in table with math
/ d3 + 100 = add 100 to every value in d3
```

[dict] 3. Find the max temp for belfast

```q
max d3[`belfast]
12

/ or

max d3`belfast
12

/ calling d3[`belfast] returns values 12 10 11 9
/ so max of this is 12
```

[dict] 4. Given new dict d4, find max temp for belfast

```q
d4:(enlist `temperature)!enlist d3

max d4[`temperature;`belfast]

/ so d4 is a dict within a dict
/ first column = temperature
/ 2nd column is the entire dict of 3
```

```q
Add a row to d4:

d4,:(enlist`rainfall)!enlist`belfast`cardiff`edinburgh`london!60 65 58 40
```

### [dict] Dictionary Problem Set (AquaQ)

```q
/1 create dictionary with keys as letters from a-z with corresponding numbers

dict: .Q.a ! 1+til 26

key value
---------
a  |  1
b  |  2
c  |  3

/ .Q.a = returns list of lowercase alphabets
/ key values are chars
```

```q
/2 retrieve values of abc 

dict "abc"
1 2 3

/ or

dict ["abc"]
1 2 3

/ abc = keys, to retrieve values, use indexing
/ the key values are chars, so need to use parathesis to retrieve
```

```q
/3 sum values of abc

sum dict "abc"
6
```

```q
/4 sum values of "yourname"

sum dict "yourname"
112
```

```q
/5 rename keys to capital letters

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
/6 create another dict, change uppercase "HELLO WORLD" to lowercase

dict2: .Q.A ! .Q.a

Key | Value
------------
A   | a
B   | b
C   | c
D   | d

/ create dict2, which maps uppercase keys to lowercase values

dict2 "HELLO WORLD"
"hello world"

/ the uppcase letters act as KEYS
/ by indexing the keys, you retrieve the lowercase value
```

```q
/7 create dictionary morse, which contains letters n-s as keys, and a code for the values

morse: "nopqrs"! (10; 111; 0110; 1101;010;0)

key value
---------
n  10
o  111
p  110
q  1101
r  10
s  0


/ the key is simply a string of chars
/ the values are just random "codes" you make up
```

```q
/8 join numbers 0 to 4 onto the existing dictionary

morse,:("01234")!(1; 10; 100; 1000; 10000)

key| value
---------
0  | 1
1  | 10
2  | 100
3  | 1000
4  | 10000

/ don't get confused, you add "01234" as strings, each with their own "codes"

/ phrase SOS using your code

morse "sos"
0 111 0

/ you are querying keys "sos" to retrieve associated values
```

```q
/9 create 2 dictionaries, one for r13, one for r12

places:`london`edinbugh`belfast`manchester`tobermory`portsmouth`cardiff
r13:557 704 944 867 1681 674 1152
r12: 600 854 1020 955 1789 544

d1: places!r13
d2:(-1_places)!r12

/ have to drop last one since value length longer than keys

d1
key       | value
-----------------
london	  | 557
edinbugh  | 704
belfast	  | 944
manchester| 867
tobermory | 1681
portsmouth| 674
cardiff	  | 1152

d2
key        | value
------------------
london	   | 600
edinbugh   | 854
belfast	   | 1020
manchester | 955
tobermory  | 1789
portsmouth | 544
```

```q
/10 extract keys from first dictionary
key d1

/11 extract values from first dictionary
value d1
```

```q
/12 create new dict with sum of annual rainful over both years

d3: d1+d2

d3
key        | value
-----------------
london	   | 600
edinbugh   | 854
belfast	   | 1020
manchester | 955
tobermory  | 1789
portsmouth | 544

/ can simply add together both dict since they are keyed (dict always keyed)
/ will find some keys, and add values together
/ if no match, will leave as is
```

```q
/13 find the average rainfall over the two years for each city

avg (d1;d2)

/ since the dict is keyed, can perform operations like avg easily

key         | value
------------------
london	    | 578.5
edinbugh    | 779.0
belfast	    | 982.0
manchester  | 911.0
tobermory   | 1735.0
portsmouth  | 609.0
cardiff	    | 576.0
```

```q
/14 which location had more rainfall over the 2 years?

d1>d2

/ can simply use comparison operator to output booleans

key        | value
------------------
london	   | 0b
edinbugh   | 0b
belfast	   | 0b
manchester | 0b
tobermory  | 0b
portsmouth | 1b
cardiff	   | 1b
```

```q
/15 find the average rainfall over the 2 years for the UK

sum(d1+d2) % 2
6170.5

/ d1+d1 will simply add each row together
/ the sum will aggregate all values together into 1 single value
```

```q
/16 create a dict of variables in the workspace as keys, and values as values

system "v"

/ this shows all keys in the workspace

value each (system "v")

/ this shows all values for each key in the workspace

vars: (system "v")! (value each (system "v"))

/ maps keys = variables and values  = values for each key

key   | value
--------------------------------------------------------------------------
d1    | `lond`edin`bel`man`tober`port`cardiff!557 704 944 867 1681 674 1152
d2    | `lond`edin`bel`man`tober`port!600 854 1020 955 1789 544
d3    | `lond`edin`bel`man`tober`port`car!578.5 779 982 911 1735 609 576
places| `lond`edin`bel`manc`tober`port`car
r12   | 600 854 1020 955 1789 544
r13   | 557 704 944 867 1681 674 1152
```

<a name="tables"></a>
### 🔴 5. Tables
[Top](#top)

### [table] What is the difference between a table and a keyed table?

```q
A table - is a flipped dictionary. Vectors of data are organized by columns.

A keyed table - is a dictionary mapping a table of key records to a table of value records.

```

### [table] Creating Blank Table with Datatypes

```q
/ create an empty table with the following columns/datatypes:
/ sym (sym)
/ side (char)
/ size (int)
/ price (float)

t: ([] sym:`$(); side: `char$(); size:`int$();price:`float$())

sym | side | size | price
--------------------------
```
### [table] 1. Insert Single Row (using JOIN ASSIGN)

```q
/ add `IBM, "B", 10I, 100f to empty table

t,:(`IBM;"B";10i; 100f)

sym | side | size | price
--------------------------
IBM | B    | 10   | 100

/ must use correct datatypes
/ JOIN ASSIGN can ignore column header
/ DON'T need to backtick table t
```

### [table] 2. Insert Single Row (using INSERT)

```q
`t insert(`IBM;"B";10i;100f)

/ INSERT don't need headers
/ don't need enlist
/ but NEED to backtick table name
```

### [table] 5. Upsert Single Row (UPSERT)

```q
/ Upsert `GOOG; "B"; 30i; 300f

`t upsert (`GOOG;"B"; 30i; 300f)

/ same syntax as INSERT
/ notice you don't need to use enlist
/ don't need column headers
```

### [table] 3. Insert Multiple Rows (INSERT)

```q
/ insert the following rows:
/ `IBM`MSFT`AAPL
/ "B" "S" "B"
/ 10i 20i 30i
/ 100f 200f 300f

`t insert(`IBM`MSFT`AAPL;"B","S","B";10i, 20i, 30i;100f, 200f, 300f)

sym  | side | size | price
-------------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0

/ no column header!
/ must use correct datatype!
/ ints have to be separated by commas
/ floats have to be separated by commas
```

### [table] 4. Upsert Multiple Rows (UPSERT)

```q
/ upsert the following rows:
/ `IBM`MSFT`AAPL
/ "B" "S" "B"
/ 10i 20i 30i
/ 100f 200f 300f

`t upsert([]sym:`IBM`MSFT`AAPL;side:"B","S","B";size: 10i, 20i, 30i; price: 100f, 200f, 300f)

sym  | side | size | price
-------------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0

/ to UPSERT multiple, have to upsert a TABLE 
/ MUST include column names
/ must have commas between ints and floats!
```

### [table] 3 Ways to Add Single Rows

```q
/ Create empty table cars with brand = sym, model = sym, and date = date

cars:([] brand:`$();model:`$();date:`date$())
```

```q
/2. Insert single row of bmw, 505, 2021.11.13

`cars insert(`bmw;`505;2021.11.13)

brand| model| date
------------------------
bmw  | 505  | 2021-11-13

/ INSERT don't need column headers
/ INSERT don't need enlist when using inserting single row
/ need corret datatype
```

```q
/3. Insert Single Row using Alternative Syntax

insert[`cars;(`audi;`s5;2021.11.13)]

brand| model| date
------------------------
bmw  | 505  | 2021-11-13
audi | s4   | 2021-11-13

/ don't need column header
/ don't need enlist
/ need correct datatype
```

```q
/4. Upsert Single Row of bmw, 505, 2021.11.13

`cars upsert(`bmw;`505;2021.11.13)

brand| model| date
------------------------
bmw  | 505  | 2021-11-13

/ UPSERT has same syntax as INSERT
/ note - you cannot upsert multiple rows; have to upsert a dictionary
```

### [table] how do you INSERT multiple rows into a table at once?

```
/ method 1

`cars insert(`ferrari`benz;`F50`S500;2021.11.13 2021.11.13)

brand  | model| date
------------------------
bmw    | 505  | 2021-11-13
audi   | s4   | 2021-11-13
ferrari| F50  | 2021-11-13
benz   | S500 | 2021-11-13

/ can INSERT multiple lines using same syntax
/ no column headers
/ remember to backtick table name `cars
```

Alternative Solution:

```q
/ alternative syntax

insert[`cars;(`ferrari`benz;`F500`S500;2021.11.13 2021.11.13)]

brand  | model| date
------------------------
bmw    | 505  | 2021-11-13
audi   | s4   | 2021-11-13
ferrari| F50  | 2021-11-13
benz   | S500 | 2021-11-13
```

### [table] how do you UPSERT multiple rows into a table?

```q
/ you cannot upsert multiple rows into a table
/ instead must upsert a dictionary
```

```q
given table t:

t:( []fruit:`apple`orange; price: 11 23; quantity:100 200)

fruit | price | quantity
--------------------
apple |	11    |	100
orange| 23    |	200

```

```q
/ upsert pear, banana, 20 30 into t

`t upsert ( [] fruit:`pear`banana; price: 20 30)

fruit  | price | quantity
-------------------------
apple  |   11  |   100
orange |   23  |   200
pear   |   20  |	
banana |   30  |	

/ UPSERTING multiple rows = upsert TABLE
/ need column names
/ notice you can skip columns when upserting (quantity left blank)
```

### [table] What is the difference between xcol and xcols?

```q
/ xcol is used to rename table columns
/ xcols is used to rearrange table columns
```

[tables] xcol example

```q
/ xcol renames columns

t: ( [] company: `ford`bmw; employee: 300 100)

company | employee
------------------
ford    |   300
bmw     |   100

/ rename company to a and employee to b

`a`b xcol t

a   | b
---------
ford| 300
bmw | 100

/ renames first 2 columns from company/employee to a/b
/ xcol will only change col names from left to right
/ have to use backtick + new col name
```

[tables] xcols example:

```q
/ xcols re-arranges columns

t: ( [] company: `ford`bmw; employee: 300 100)

company | employee
------------------
ford    |   300
bmw     |   100

`employees`company xcols t

employee | company
------------------
300      |  ford 
100      |  bmw  

/ reorders columns
/ doesn't have to be complete list of columns
/ just moves it to left of table
```

### [table] What are some common table functions?

```q
t:([] company:`ford`bmw; employees:300 100)
t
type t               / what datatypes the table is
count t              / return total number of rows in table
cols t               / retrieve list of column names
meta t               / shows info on type, foreign keys, and attributes
`employees xasc t    / sorts table by employee column
```

### [table] Show examples of union, except, and inter function on tables

```q
t:( [] company:`ford`bmw`benz; employees:100 200 300)
u:( [] company:`ford`bmw`ferrari; employees:5 200 400)

table t
company | employees
-------------------
ford    | 100
bmw     | 200 
benz    | 300

table u
company | employees
--------------------
ford    | 5
bmw     | 200 
ferrari | 400
```

[tables] Union Table Example

```q
/1 UNION TABLE = merges 2 tables together, but does NOT dupe values!

t:( [] company:`ford`bmw`benz; employees:100 200 300)
u:( [] company:`ford`bmw`ferrari; employees:5 200 400)

t union u

company | employees
-------------------
ford    | 100 
bmw     | 200 
benz    | 300
ford    | 5
ferrari | 400

/ matches on keys (bmw). if same value, copies value (200)
/ does NOT dupe same values
/ if match on key (ford), but no match on value (100 v 5), returns BOTH values
/ if no match on key (ferrari), returns key + value as new row
```

[tables] EXCEPT Table Example

```q
/2 EXCEPT TABLE = only returns values in left table NOT in right table

table t
company | employees
-------------------
ford    | 100
bmw     | 200 
benz    | 300

table u
company | employees
--------------------
ford    | 5
bmw     | 200 
ferrari | 400

t except u 

company | employees
-------------------
ford    | 100 
benz    | 300

/ returns item in t NOT in u
/ if match on key (ford) but not value (100 v 5), returns key + value in table x
/ if match on key (bmw) and value (200), REMOVE
/ if no match on key (benz), returns key + value
```

[tables] INTER table Example

```q
/3 INTER TABLE = only returns common elements in both t and u (inner join) 

table t
company | employees
-------------------
ford    | 100
bmw     | 200 
benz    | 300

table u
company | employees
--------------------
ford    | 5
bmw     | 200 
ferrari | 400

t inter u 

company | employees
--------------------
bmw     | 200 

/ only returns matches in both key (bmw) and value (200)
```

### [table] Show how to append using table joins , (comma)

```q
t:([] company:(); employees:())
/ empty table t

t: t, ([] company:`bmw`skoda; employees:200 300)

company | employee
------------------
bmw	| 200
benz	| 300

/ joins empty table t with new table
/ essentially you add rows by joining a table into table
```

### [table] How do you join 2 tables with same columns? (add rows)

```q
/ if 2 tables columns MATCH, can JOIN to ADD ROW
/ called vertical joins

t1
sym  side price size
---------------------
IBM  buy   10 	 100
AAPL sell  20    200

t2
sym  side price size
---------------------
GOOG buy   30 	 300
MSFT sell  40	 400

t1, t2

sym  side price size
---------------------
IBM  buy   10 	 100
AAPL sell  20	 200
GOOG buy   30 	 300
MSFT sell  40	 400

/ simply use comma to join 2 tables together with same schema (column names)
/ this will keep column headers the same
/ and append the new rows
```

### [table] How do you join 2 tables with different columns? (add columns)

```q
/ if 2 tables have same number of rows
/ and NO matching columns
/ can join tables together by adding extra columns
/ similar to LEFT JOIN

t1:( [] sym: `IBM`AAPL`GOOG; ex: `nyse`nyse`nasdaq)
t2:( [] price:10 20 30; size: 100 200 300)

t1
sym  ex
----------
IBM  nyse
AAPL nyse
GOOG nasdaq

t2
price size
----------
10    100
20    200
30    300

t1,'t2

sym  ex     price size
----------------------
IBM  nyse    10   100
AAPL nyse    20   200
GOOG nasdaq  30   300

/ use ,' each both adverb to combine tables together
/ t1 and t2 have diff column names
/ but same number of rows
```

### [tables] Tables Problem Set 1 TS

```q
stock: ( [] sym: `MS`C`AAPL; sector:`Financial`Financial`Tech; employees: 100 100 100)

sym |sector    |employees
-------------------------
MS  |Financial |100
C   |Financial |100
AAPL|Tech      |100
```

[tables] 1. Extract the employees numbers (without the header)

```q
/ since they only want values and no header, use INDEX retrieve

stock[`employees]
100 100 100
```

other syntax:

```q
stock.employees
```
```q
stock`employees
```
```q
stock [ ; `employees]
```

[tables] 2. Key the first column in stock table above

```q
1!stock

`sym` |sector    |employees
-------------------------
`MS`  |Financial |100
`C`   |Financial |100
`AAPL`|Tech      |100
```

[tables] 3. Display only the first and second rows of the stock table

```q
/ use TAKE # method

2#stock

sym |sector    |employees
-------------------------
MS  |Financial |100
C   |Financial |100
```

alternative solution:

```q
/ use index retrieve method

stock [0 1]

/ returns index position 0 and 1 (first 2 rows)
```

[tables] 4. Select the last row of stock table as a dictionary

```q
last stock

key       | value
-----------------
sym       | AAPL
sector    | Tech
employees | 100

/ LAST will retrieve the last row from table stock
/ and return it as a dictionary
```

[tables] 5. Insert GOOG in the tech sector with 100 employees

```q
`stock insert(`GOOG; `Tech; 100)

sym |sector    |employees
-------------------------
MS  |Financial |100
C   |Financial |100
AAPL|Tech      |100
GOOG|Tech      |100

/ remember need to `stock otherwise error
/ saves + updates underlying table
```

alternative solution:

```q
insert [`stock; ([] sym: enlist `GOOG; sector: enlist `tech; employees: enlist 100)]

sym |sector    |employees
-------------------------
MS  |Financial |100
C   |Financial |100
AAPL|Tech      |100
GOOG|Tech      |100

/ syntax is insert + [table name; table with corresponding columns]
/ must use enlist when adding single row!!
```

### [tables] Tables Problem Set 2 TS

```q
boss: ( [] name:`bob`bill`belinda; height: 188 186 174)
employees: ( [] name:`jim`jane`john; height: 180 160 170)

boss:
name    | height
----------------
bob     | 188
bill    | 186
belinda | 174

employees:
name| height
-----------
jim | 180
jane| 160
john| 170
```

[tables] 1. Find the average height of the bosses, the employees, and both the bosses and employees

```q
avg boss[`height]
182.667

avg employees [`height]
170f

avg (boss,employees)[`height]
176.33

/ first JOIN boss and employees tables together
/ index retrieve values from the height column
/ then find average
```

[tables] 2. Find the 2 tallest employees

```q
2 # `height xdesc employees

name | height
-------------
jim  | 180
john | 170

/ first sort employees table by height (xdesc)
/ syntax is column_name xdesc table_name
/ then you take the first 2 rows 
```

### [tables] Tables Problem Set 3 TS

```q
stock: ( [sym:`MS`C`AAPL] sector:`Fin`Fin`Tech; employees: 100 100 100)
trade: ( [] dt: 2021.01.01+til 5; sym:`C`C`MS`C`AAPL; price: 10 20 30 40 50; size: 100 200 300 400 500)

stock:
sym  |sector| employees
-----------------------
MS   |Fin   | 100
C    |Fin   | 100
AAPL |Tech  | 100

trade:
dt        |sym  |price| size
----------------------------
2021-01-01|C	|10   | 100
2021-01-02|C	|20   | 200
2021-01-03|MS   |30   | 300
2021-01-04|C	|40   | 400
2021-01-05|AAPL	|50   | 500
```

[tables] 1. Insert the following rows into trade table

```q
dt        |sym  |price| size
----------------------------
2021-11-01|JPM	|1    | 100
2021-11-02|UBS	|2    | 200

meta trade

c	t f a
---------------
dt	d		
sym	s		
price	j		
size	j		

/ since the values you insert HAS to match the datatype of table trade
/ meta helps you know what each column datatype is

`trade insert (2011.11.01 2021.11.02; `JPM`UBS; 1 2; 100 200)

dt        | sym  | price| size
-------------------------------
2021-01-01| C	 |  10  | 100
2021-01-02| C	 |  20  | 200
2021-01-03| MS   |  30  | 300
2021-01-04| C	 |  40  | 400
2021-01-05| AAPL |  50  | 500
2021-11-01| JPM	 |   1  | 100
2021-11-02| UBS	 |   2  | 200

/ can simply insert the values (without headers)
/ remember to backtick `trade table name
```

alternative solution:

```q
/ insert table method

`trade insert( [] dt:2021.11.01+1 ; sym:`JPM`UBS; price:1 2; size: 100 200) 

/ requires column header names
```

alternative solution:

```q
/ alternative syntax, but also requires column headers

insert [`trade; ([] dt:2021.11.01+1 ; sym:`JPM`UBS; price:1 2; size: 100 200)]

dt        |sym  |price| size
----------------------------
2021-01-01|C	|10   | 100
2021-01-02|C	|20   | 200
2021-01-03|MS   |30   |	300
2021-01-04|C	|40   | 400
2021-01-05|AAPL	|50   |	500
2021-11-01|JPM	|1    | 100
2021-11-02|UBS	|2    | 200

/ have to use backtick table in order to amend the underly table
```

[tables] 2. Insert the following record into stock

```q
sym|sector|employees
--------------------
FB |Tech  | 100

`stock insert (`FB; `Tech; 100)

sym  |sector|employees
---------------------
MS   |Fin   | 100
C    |Fin   | 100
AAPL |Tech  | 100
FB   |Tech  | 100

/ insert values without header
/ `FB automatically becomes keyed since table column sym is keyed
/ remember to backtick `stock
```

[tables] 3. In the stock table, change the number of employees for C to 300

```q
stock upsert (`C;`Fin;300)

/ to update table values, use UPSERT
/ don't need backtick on table name
```

alternative solution:

```q
/ alternative syntax
/ but this requires headers

stock upsert ([sym: enlist`C] employees: enlist 300)

sym|sector|employees
--------------------
C  |Fin   |300

/ have to use enlist to create a vector for an atom
```

[tables] 4. Sort the stock table by sym

```q
`sym xasc `stock

sym |sector| employees
--------------------
AAPL|Tech  | 100
C   |Fin   | 100
MS  |Fin   | 100

/ `column name + xasc + `table name
```

### [tables] Tables Problem Set 1 AQ

[tables] 1. Create 3 lists called a, b, c with 4 elements each

```q
a: 1 2 3 4
b: `a`b`c`d
c: 100 200 300 400
```

[tables] 2. Create a table using these 3 lists

```q
t:( [] a;b;c)

a b c
--------
1 a 100
2 b 200
3 c 300
4 d 400

/ you can simply create a table using lists 
/ which are vectors of equal length
```

[tables] 3. Create a dictionary using this table

```q
flip t

key|value
-----------------
a  | 1 2 3 4
b  | `a`b`c`d
c  | 100 200 300 400

/ a table is just a flipped dictionary
/ so you can flip a table back into a dictionary
```

[tables] 4. Create empty table sym (sym), side (char), size (int), price (float)

```q
trade:( [] sym:`$(); side:`char$(); size:`int$(); price:`float$())

sym | side | size | price

/ created empty table trade
/ to cast datatype sym use backtick `
```

[tables] 5. Create another table, lasttrade, which is a copy of trade, but sym is keyed

```q
lasttrade: 1!trade

`sym` | side | size | price

/ created empty table lasttrade, with keyed sym column
```

[tables] 6. Is there a difference in the metadata between 2 tables?

```q
meta trade ~ meta lasttrade
1b (true)

/ no difference when you key columns
/ meta queries TYPE, foreign key, attributes
```

[tables] 7. Is there a difference in type?

```q
type trade ~ type lasttrade
0b (false)

/ once you KEY a table, the TYPE becomes a dictionary
/ so YES, the metadata will change once you key

/ trade = 98h = table
/ lasttrade = 99 = dict (since you keyed)
```

[tables] Joining rows to table

```q
/ use 3 join commands to add rows to trade 
/ sym: IBM, MSFT, AAPL
/ side: "B" or "S"
/ size: 10i 20i 30i
/ price: 100f 200f 300f

trade
sym|side|size|price
-------------------

trade,:(`IBM;"B";10i; 100f)
trade,:(`MSFT;"S";20i;200f)
trade,:(`APPL,"B";30i;300f)

/ JOIN ASSIGN ,: dont need columns
/ values separated by semi colon ;
/ don't need backtick trade table
/ need to specify datatype since the table was assigned datatypes earlier
```

[tables] Use a single join command to add 3 more rows into join

```q
/ method 1: simply build a table

trade:([] sym:`IBM`MSFT`AAPL;side:"B","S","B";size: 10 20 30; price: 100 200 300)

sym  | side | size | price
---------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0
```

Method 2: INSERT multiple rows

```q
`t insert(`IBM`MSFT`AAPL;"B","S","B";10i, 20i, 30i;100f, 200f, 300f)

sym  | side | size | price
---------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0

/ when INSERT multiple rows, no column headers!
/ must backtick table name `t
/ ints and floats separated by commas!
```

Method 3: UPSERT multiple

```q
`t upsert( []sym:`IBM`MSFT`AAPL;side:"B","S","B";size: 10i, 20i, 30i; price: 100f, 200f, 300f)

sym  | side | size | price
--------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0

/ to UPSERT multiple, have to upsert a table 
/ MUST include column names
/ must have commas between ints and floats!
```

[tables] Fill lasttrade with data from trade

```q
lasttrade:trade

sym  | side | size | price
--------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0

/ you can simply "assign" table lasttrade to trade
```

alternative syntax:

```q
lasttrade,'trade

/ this joins the 2 tables together
```

### [tables] Tables Problem Set 2 AQ

```q
/1 create the following table

stock:([] item:`soda`bacon`mush`eggs;brand:`fry`pork`veg`veg;price:1.5 1.99 0.88 1.55; order:50 82 45 92)

item  | brand| price | order
----------------------------
soda  | fry  | 1.5   | 50
bacon | pork | 1.99  | 82
mush  | veg  | 0.88  | 45
eggs  | veg  | 1.55  | 92
```

[tables] 2. Add row of tomato, veg, 1.35 70

```q
/ insert method (most straightforward)

`stock insert (`tomato;`veg;1.35;70)

item   | brand| price| order
----------------------------
soda   | fry  | 1.5  | 50
bacon  | pork | 1.99 | 82
mush   | veg  | 0.88 | 45
eggs   | veg  | 1.55 | 92
tomato | veg  | 1.35 | 70

/ INSERT no header
/ need to backtick `stock table
```

alternative syntax:

```q
/ JOIN ASSIGN method

stock,:(`tomato;`veg;1.35;70)

item   | brand| price| order
----------------------------
soda   | fry  | 1.5  | 50
bacon  | pork | 1.99 | 82
mush   | veg  | 0.88 | 45
eggs   | veg  | 1.55 | 92
tomato | veg  | 1.35 | 70
```

[tables] 3. Key the table according to item and brand

```q
2!stock

`item`   | `brand`| price| order
----------------------------
`soda`   | `fry`  | 1.5  | 50
`bacon`  | `pork` | 1.99 | 82
`mush`   | `veg`  | 0.88 | 45
`eggs`   | `veg`  | 1.55 | 92
`tomato` | `veg`  | 1.35 | 70

/ use ! method to key
```

alternative syntax:

```q
`item`brand xkey stock

`item`   | `brand`| price| order
--------------------------------
`soda`   | `fry`  | 1.5  | 50
`bacon`  | `pork` | 1.99 | 82
`mush`   | `veg`  | 0.88 | 45
`eggs`   | `veg`  | 1.55 | 92
`tomato` | `veg`  | 1.35 | 70

/ use xkey method to key
```

[tables] 4. Does the meta data change when you key/unkey tables?

```q
(meta stock) ~ (meta (2!stock))
1b

/ true, the 2 tables match
/ so no, changing keys does not affect a tables meta
```

[tables] Tables Problem Set 3 AQ

```q
trader:([]item:`soda`bacon`mush`eggs`tomato;brand:`fry`pork`veg`veg`veg;price:1.5 1.99 0.88 1.55 1.35; order:200 180 110 210 100)

item   | brand| price| order
----------------------------
soda   | fry  | 1.5  | 200
bacon  | pork | 1.99 | 180
mush   | veg  | 0.88 | 110
eggs   | veg  | 1.55 | 210
tomato | veg  | 1.35 | 100
```

[tables] 1. Create new table, totalorders, which has sum of both orders from traders

```q
/ also, drop the price column before adding together

totalorders:(2!(enlist `price)_stock) + (2!(enlist `price)_trader)

item   | brand| order
----------------------
soda   | fry  | 250
bacon  | pork | 262
mush   | veg  | 155
eggs   | veg  | 302
tomato | veg  | 170

/ first, need to KEY the tables before adding together
/ since you have 2 columns of syms, and 1 column of ints
/ need to KEY BOTH SYM COLUMNS 2!
/ second, need to also DROP the price column before adding
/ since only dropping 1 column, need to use ENLIST
```

[tables] 2. Create new list called newprices, which is 75% of stock's price

```q
newprices:0.75 * stock[`price]
1.125 1.4925 0.66 1.1625 1.0125

/ using indexing to retrieve price values from stock table
/ alternative syntax: stock`price
```

[tables] 3. Join newprices to the totalorders table

```q
/ newprices = list of values
/ trying to join these values onto a table as a column

totalorders: totalorders,' ( [] newprices)

/ so ([] newprices) turns the list into a single column
/ then you simply join it onto existing totalorders table
/ since the number of rows add up, it appends the column

item   |brand |order | newprices
--------------------------------
soda   | fry  | 250  | 1.125
bacon  | pork |	262  | 1.4925
mush   | veg  |	155  | 0.66
eggs   | veg  |	302  | 1.1625
tomato | veg  |	170  | 1.0125
```

alternative solution:

```q
/ QSQL method:

update newp:newprices from totalorders

item   |brand |order | newprices
--------------------------------
soda   | fry  | 250  | 1.125
bacon  | pork |	262  | 1.4925
mush   | veg  |	155  | 0.66
eggs   | veg  |	302  | 1.1625
tomato | veg  |	170  | 1.0125

/ update col that doesnt exist will append it to table
```

[tables] 4. With the 75% discount, how much savings per week will the stock and trader have?

```q
stock

`item`   | `brand`| price| order
--------------------------------
`soda`   | `fry`  | 1.5  | 50
`bacon`  | `pork` | 1.99 | 82
`mush`   | `veg`  | 0.88 | 45
`eggs`   | `veg`  | 1.55 | 92
`tomato` | `veg`  | 1.35 | 70

/ price x order = notional
/ notional * 0.25 = savings

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
item  | brand | price | order
-----------------------------
soda  | fry   | 1.5   | 50
bacon | pork  | 1.99  | 82
mush  | veg   | 0.88  | 45
eggs  | veg   | 1.55  | 92
tomato| veg   | 1.35  | 70

(stock`price)*(stock`order)
75 163.18 39.6 142.6 94.5

/ this works
/ however, if you key it:

1!`stock
(stock`price)*(stock`order)
type

/ this doesnt work anymore (since its keyed)
```

alternative syntax:

```q
/ QSQL method (honestly, easier)

stock:update savings: price*order*0.25 from stock

item  | brand | price | order | savings
---------------------------------------
soda  | fry   | 1.5   | 50    | 18.75
bacon | pork  | 1.99  | 82    | 40.795
mush  | veg   | 0.88  | 45    | 9.9
eggs  | veg   | 1.55  | 92    | 35.65
tomato| veg   | 1.35  | 70    | 23.624

select sum savings from stock
128.72

/ so much cleaner!
```

### [tables] Tables Problem Set (GS)

```q
t1: ([] sym:`a`b`c;ex:`x)
t2: ([] ex:`y;sym:`a`b`c)

ps:(( [] sym:`a`b`c`a`b`c; ex:`x`x`x`y`y`y; price: 1.1 2.1 3.1 1.2 2 3.3); ( [] sym:`a`b`c`a`b`c; ex:`x`x`x`y`y`y; size: 200 100 300 200 50 200))

/ Part 1: Join the first two tables using t1 schema

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

sym| ex | price
--------------
`a`| `x`| 1.1
`b`| `x`| 2.1
`c`| `x`| 3.1
`a`| `y`| 1.2
`b`| `y`| 2.0
`c`| `y`| 3.3

ps2

sym| ex | size
-------------
`a`| `x`| 200
`b`| `x`| 100
`c`| `x`| 300
`a`| `y`| 200
`b`| `y`| 50
`c`| `y`| 200

ps3:ps1 lj ps2

/ join the ps1 and ps2 tables back together to make table ps3

sym|ex |price|size
------------------
`a`|`x`| 1.1 | 200
`b`|`x`| 2.1 | 100
`c`|`x`| 3.1 | 300
`a`|`y`| 1.2 | 200
`b`|`y`| 2   |  50
`c`|`y`| 3.3 | 200

t4: t3 lj ps3

/ use left join to join ps3 to t3

sym|ex|price|size
------------------
 x |a |	1.1 | 200
 x |b |	2.1 | 100
 x |c |	3.1 | 300
 y |a |	1.2 | 200
 y |b |	2.0 |  50
 y |c |	3.3 | 200

/ Part 3: Add 3 new columns: avg_price_by_sym, avg_size_by_ex, wavg_price_by_sym (weighted by size)

Desired Result:

sym|ex|prirce|size|avg_price_by_sym|avg_size_by_ex|wavg_price_by_sym
--------------------------------------------------------------------
 x |a | 1.1 | 200 |      1.15      |      200     |    1.15
 x |b | 2.1 | 100 |      2.05      |      200     |    2.0667
 x |c | 3.1 | 300 |      3.2       |      200     |    3.18
 y |a | 1.2 | 200 |      1.15      |      150     |    1.15
 y |b | 2.0 |  50 |      2.05      |      150     |    2.06667
 y |c | 3.3 | 200 |      3.2       |      150     |    3.18

update avg_price_by_sym: avg price by sym from `t4
update avg_price_by_ex: avg size by ex from `t4
update wavg_price_by_sym: size wavg price by sym from `t4

sym|ex|price|size|avg_price_by_sym|avg_size_by_ex|wavg_price_by_sym
--------------------------------------------------------------------
 x | a| 1.1 |200 |      1.15      |      200     |    1.15
 x |b | 2.1 |100 |      2.05      |      200     |    2.0667
 x |c | 3.1 |300 |      3.2       |      200     |    3.18
 y |a | 1.2 |200 |      1.15      |      150     |    1.15
 y |b | 2.0 | 50 |      2.05      |      150     |    2.06667
 y |c | 3.3 |200 |      3.2       |      150     |    3.18
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
NYSE	11:00	1
NYSE	13:00	1

startcount-endcount

/ startcount minus endcount will tell me every time an order starts (+1), and ends (-1)
/ if i simply do startcount minus endcount, i get this messy table that's not sorted
/ So i need to sort this by exchange and time in order for it to line up with
/ my vertical time buckets.   

`ex`time xasc startcount-endcount

ex    | time | num
-------------------
NASDAQ| 08:00|  1
NASDAQ| 09:00|  1
NASDAQ| 10:00|  1
NASDAQ| 11:30| -1
NASDAQ| 12:30|  1
NASDAQ| 13:30| -1
NASDAQ| 14:30| -1
NASDAQ| 15:30| -1
NASDAQ| 18:00|  1
NASDAQ| 19:00| -1
NYSE  | 08:00|  1
NYSE  | 09:00|  1
NYSE  | 11:00| -1
NYSE  | 13:00| -1

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
NYSE   08:00	1
NYSE   09:00	2
NYSE   11:00	1
NYSE   13:00	0

/ now that i have this active table, i can go back to my original orders table,
/ check EACH row, for the max num from the ACTIVE table,
/ where ex from ACTIVE is equal to the ex from ORDERS. and where the time from ACTIVE
/ is equal to the start and end time from orders. after executing this, update it to 
/ column d

update d: ({exec max num from active where ex=x`ex, time within x`start`end} each orders) from orders
```

<a name="key_table"></a>
### 🔴 6. Keyed Tables
[Top](#top)

### [keyed tables] How do you add/change keys in a table?

```q
kt
id |name|employer| age
----------------------
a  |jane|  citi  | 11
b  |jim |  citi  | 22
c  |kim |    ms  | 13
e  |john|    ts  | 15

2!kt

`id` |`name`|employer| age
--------------------------
`a`  |`jane`|  citi  | 11
`b`  |`jim` |  citi  | 22
`c`  |`kim` |    ms  | 13
`e`  |`john`|    ts  | 15

/ keys the first 2 columns of table kt
```

alternative solution:

```q
`id`name xkey kt

`id` |`name`|employer| age
----------------------
`a`  |`jane`|  citi  | 11
`b`  |`jim` |  citi  | 22
`c`  |`kim` |    ms  | 13
`e`  |`john`|    ts  | 15
```

### [keyed tables] How do you delete/remove keys from a table?

```q
`id` |`name`|employer| age
--------------------------
`a`  |`jane`|  citi  | 11
`b`  |`jim` |  citi  | 22
`c`  |`kim` |    ms  | 13
`e`  |`john`|    ts  | 15

0!kt

id | name |employer| age
--------------------------
a  | jane |  citi  | 11
b  | jim  |  citi  | 22
c  | kim  |    ms  | 13
e  | john |    ts  | 15

/ 0! removes all keys from table
```

alternative syntax:

```q
`id` |`name`|employer| age
--------------------------
`a`  |`jane`|  citi  | 11
`b`  |`jim` |  citi  | 22
`c`  |`kim` |    ms  | 13
`e`  |`john`|    ts  | 15

() xkey kt

id | name |employer| age
--------------------------
a  | jane |  citi  | 11
b  | jim  |  citi  | 22
c  | kim  |    ms  | 13
e  | john |    ts  | 15
```

### [keyed tables] How do you upsert keyed rows/tables into a table?

```q
t1:( [sym:`a`b`c]; ex:`one`two`three; size:100 200 300)
t2:( [sym:`c`d`e]; ex:`four`five`six; size:400 500 600)

upsert[t1;t2]

`sym` | ex    | size
------------------
`a`   | one   | 100
`b`   | two   | 200
`c`   | four  | 400
`d`   | five  | 500
`e`   | six   | 600

/ both tables have to be keyed!
/ the schemas have to match (column names)
/ if key exists and matches, updates value (c match, replaces old values)
/ if new key, adds new row (d and e)
```

alternative syntax

```q
/ using JOINS method

t1,t2

`sym` | ex    | size
------------------
`a`   | one   | 100
`b`   | two   | 200
`c`   | four  | 400
`d`   | five  | 500
`e`   | six   | 600

/ since the tables are KEYED
/ and the SCHEMA are the same
/ you can simply "join" the tables together
/ and return the same result
```

alternative syntax:

```q
/ you can also upsert by typing out a table

upsert[t1;( [sym:`f`g] ex:`seven`eight; size: 700 800)]

sym | ex    | size
------------------
a   | one   | 100
b   | two   | 200
c   | four  | 400
f   | seven | 700
g   | eight | 800
```

### [keyed table] SINGLE KEY TABLE PROBLEM SET

```q
t1:([sym:`a`b`c];ex:`one`two`three;size:100 200 300)

t1
`sym` | ex    | size
------------------
`a`   | one   | 100
`b`   | two   | 200
`c`   | four  | 400
`d`   | five  | 500
`e`   | six   | 600
```

1. Retrieve SINGLE ROW as a DICTIONARY <br/>
(SINGLE KEY TABLE)

```q
t1`a

Key  | Value
------------
ex   | one
size | 100

/ don't need ENLIST
/ simply returns VALUES from key a as dictionary
```

2. Retrieve MULTI ROW as DICTIONARY <br/>
(SINGLE KEY TABLE)

```q
/ table lookup method

t1 ( [] sym:`a`b)

ex  | size
-----------
one | 100
two | 200

/ NOTE - even tho underlying column sym is KEYED
/ when you retrieve, you leave [ ] blank
/ and simply retrieve the column names sym:`a`b
/ outputs VALUES as a dictionary
```

3. Retrieve SINGLE ROW as TABLE <br/>
(SINGLE KEY TABLE)

```q
/ use TAKE # Method

( [] sym:enlist`b) # t1

`sym` | ex  | size
----------------
`a`   | one | 100

/ need ENLIST since only 1 row
/ by using take #, you return a table
/ includes the KEY column
```

4. Retrieve MULTI ROW as TABLE <br/>
(SINGLE KEY TABLE)

```q
/ use TAKE # Method

( [] sym:`a`b) # t1

`sym` | ex  | size
----------------
`a`   | one | 100
`b`   | two | 200

/ by using take #, you return a table
/ includes the KEY column
```

### [keyed table] MULTI KEY TABLE PROBLEM SET

```q
kt:([employer:`kx`ms`ms;loc:`NY`NY`HK] size: 10 20 30; area: 1 2 3)

`employer`| `loc`|size|area
----------------------------
`kx`	  | `NY` | 10 | 1
`ms`	  | `NY` | 20 | 2
`ms`	  | `HK` | 30 | 3

/ both employer and loc are keyed columns
```

1. Retrieve SINGLE ROW as a DICTIONARY <br/>
(MUTLI KEY TABLE)

```q
/ retrieve values for keys = MS + HK as a dictionary

kt`ms`HK

key  | value
-----------
size | 30
area | 3

/ returns VALUES as a DICTIONARY
/ for set of keys `MS + `HK
```

2. Retrieve MULTI ROWs as a DICTIONARY <br/>
(MUTLI KEY TABLE)

```q
/ Retrieve values where keys = ms/HK and kx/NY

kt(`ms`HK;`kx`NY)

size| area
-----------
30  | 3
10  | 1

/ so you are querying 2 sets of keys
/ `ms`HK and `kx`NY
/ returns VALUES only
```

3. Retrieve SINGLE ROWs as a TABLE <br/>
(MUTLI KEY TABLE)

```q
( [] employer:enlist`kx; loc:`NY) # et

`employer`|`loc`|size|area
--------------------------
`kx`      | `NY`| 10 | 1

/ have to use ENLIST for single row
/ NOTE - even though underlying table is keyed
/ when RETRIEVE using TAKE #
/ leave the [ ] blank
```

4. Retrieve MULTI ROWS as a TABLE <br/>
(MULTI KEY TABLE)

```q
/ uses the TAKE # function
/ retrieve values for keys `ms`HK + `kx`NY

( [] employer:`ms`kx; loc:`HK`NY) # et

employer | loc | size | area
----------------------------
ms	 | HK  |   30 |   3
kx	 | NY  |   10 |   1

/ using TAKE # returns a table which includes the KEY columns
/ NOTE - even tho underlying table is keyed
/ when retrieving, leave [ ] BLANK
/ and simply call the col names
```

### [keyed tables] Keyed Tables Problem Set 1 TS

```q
p: ( [book:`A`B`B`C; ticker:`MS`AAPL`MS`C] size:100 200 300 400)

`book`| `ticker`| size
----------------------
`A`   | `MS`    | 100
`B`   | `AAPL`  | 200
`B`   | `MS`    | 300
`C`   | `C`     | 400
```

1. Retrieve entries where book is B, using select

```q
/ QSQL method

select from p where book=`B

book | ticker|size
------------------
`B`  | `AAPL`| 200
`B`  | `MS`  | 300
```

2. Retrieve entries where book is C and ticker is c, using take**

```q
( [] book:enlist`C;ticker:enlist`C) # p

book | ticker| size
-------------------
`C`  | `C`   | 400

/ need to use enlist since only one row
/ NOTE - even tho underlying table is keyed
/ when retrieving, leave [ ] BLANK
/ and simply call the col names
```

3. Upsert the following values in **

```q
/ Upsert the values encased with **

`book` | `ticker`|size
----------------------
`A`    | `MS`    | 100
`B`    | `AAPL`  | 200
`B`    | `MS`    | 300
`C`    | `C`     |**400**
**`D`**|**`MS`** |**500**

upsert [p; ([book:`C`D; ticker:`C`MS]size:400 500)]

/ for `C`C -> updates old value to 400
/ `D`MS 500 -> adds new row
```

### [keyed tables] Tables Problem Set AQ

```q

tab1:([id:"abc"]pupil:`john`paul`rachel;subject:`maths`physics`chem;mark:96 55 82)

id| pupil |subject  | mark
--------------------------
a | john  | maths   | 96
b | paul  | physics | 55
c | rachel| chem    | 82
```

[keyed tables] 1. Extract dictionary corresponding to id = b

```q
id"b"

key     | value
-----------------
pupil	| paul
subject	| physics
mark	| 55

/ note - id columns are chars not sym! 
```

alternative syntax

```q

tab1["b"]

key     | value
-----------------
pupil	| paul
subject	| physics
mark	| 55

/ note - id columns are chars not sym! 
```

[keyed tables] 2. Add the 2 rows of information to tab1

```q
/ Add the 2 rows to tab1

(id = "d";pupil = emma; subject = maths; mark = 76)
(id = "e";pupil = michael;subject = bio; mark = 63)
```

```q
/ UPSERT method

upsert [tab1; ([id:"de"] pupil: `emma`michael; subject:`maths`bio; mark: 76 63)]

id| pupil  |subject  | mark
--------------------------
a | john   | maths   | 96
b | paul   | physics | 55
c | rachel | chem    | 82
d | emma   | maths   | 76
e | michael| bio     | 63

/ id is a KEY column
/ since id datatype is char, need parathesis " "
```

alternative syntax

```
/ JOIN ASSIGN method

tab1,:([id:"de"]pupil:`emma`michael; subject:`maths`bio;mark:76 63)

id| pupil  |subject  | mark
--------------------------
a | john   | maths   | 96
b | paul   | physics | 55
c | rachel | chem    | 82
d | emma   | maths   | 76
e | michael| bio     | 63

/ id is a KEY column
/ since id datatype is char, need parathesis " "
/ other values are `syms
```

3. Remove entire keyed column from tab1 rename new table tab2

```q
tab2: value tab1

/ value + table will only return its values

pupil  |subject  | mark
--------------------------
john   | maths   | 96
paul   | physics | 55
rachel | chem    | 82
emma   | maths   | 76
michael| bio     | 63
```

alternative syntax: 

```q
/ QSQL method

tab2:delete id from tab1

pupil  |subject  | mark
--------------------------
john   | maths   | 96
paul   | physics | 55
rachel | chem    | 82
emma   | maths   | 76
michael| bio     | 63
```

to "drop" the id column

```q
/ note - since tab2 is a keyed table (`id is keyed), you cannot "drop" the column
/ if you want to drop the column, must first unkey

() xkey `tab1
(enlist `id)_tab1

pupil  |subject  | mark
--------------------------
john   | maths   | 96
paul   | physics | 55
rachel | chem    | 82
emma   | maths   | 76
michael| bio     | 63
```

```
/4 find first index position where chem appears in tab2

tab2[`subject]?`chem
2

/ index position 2 is where subject = `chem appears
/ utilize the ? find operator to search for index position of value
```

<a name="fkey_table"></a>
### 🔴 7. Foreign Key Restrictions
[Top](#top)

### [fkey] Problem Set 1 - TS

```q
/ 1. Given [company] and [employee] tables

company:([sym:`TS`KX`C`AAPL`GOOG`MS] advice: 6?`HOLD`BUY`SELL; level: 6?100)
company
sym   |advice| level
---------------------
`TS`  | HOLD | 40
`KX`  | HOLD | 51
`C`   | SELL | 55
`AAPL`|	BUY  | 90
`GOOG`|	SELL | 73
`MS`  |	SELL | 90

employee:( [] name:`ryan`charlie`arthur`greg; employer:`TS`KX`KX`MS)

employee 
name   |employer
-----------------
ryan   | TS
charlie| KX
arthur | KX
greg   | MS
```

[fkey] 1. set an FKEY for the employer column from employee table

```q
/ 1. set an FKEY for the [employer column] from [employee table] 
/ to the domain of [company table]

update `company$employer from `employee
```

[fkey] 2. Use meta to check fkey

```q
/2. confirm the fkey is set for column employer

meta employee

c       | t |   f   | a
------------------------
name    | s |       |		
employer| s |company| 	

/ meta shows [employer column] has an fkey set to [company table]
```

[fkey] 3. Upserting values not in fkey

```q
/3. upsert name:`james`claire and employer:`RBS`RBS into the [employee table]

/ need to FIRST add RBS into the company domain (as a keyed sym)
/ remember  need to use enlist when adding single rows

insert[`company; ([sym:enlist `RBS] advice:enlist `SELL; level: enlist 20)]

company
sym   |advice| level
---------------------
`TS`  | HOLD | 40
`KX`  | HOLD | 51
`C`   | SELL | 55
`AAPL`|	BUY  | 90
`GOOG`|	SELL | 73
`MS`  |	SELL | 90
`RBS` | SELL | 20

/ now you can append james and claire

upsert[employee; ( [] name:`james`claire; employer:`RBS`RBS)]

employee 
name   |employer
-----------------
ryan   | TS
charlie| KX
arthur | KX
greg   | MS
james  | RBS
claire | RBS
```

[fkey] 4. Retrieving Values from fkey

```q
/4. Retrieving Values from fkey

/ from the [employee table], retrieve the values from the [advice column]
/ and the [level column] from the [company table]

company
sym   |advice| level
---------------------
`TS`  | HOLD | 40
`KX`  | HOLD | 51
`C`   | SELL | 55
`AAPL`|	BUY  | 90
`GOOG`|	SELL | 73
`MS`  |	SELL | 90
`RBS` | SELL | 20

employee
name   |employer
-----------------
ryan   | TS
charlie| KX
arthur | KX
greg   | MS
james  | RBS
claire | RBS

meta employee
c       |t|   f   |a
----------------------
name    |s|       |		
employer|s|company| 	
```

```q
update employer.advice, employer.level from employee

name   |employer|advice|level
---------------------------
ryan   |TS	|SELL  |12
charlie|KX      |BUY   |10
arthur |KX      |BUY   |10
greg   |MS      |SELL  |90
```

### [fkey] Retrieve values from multi fkey - TS

```q
office: ([sym:`TS`KX`C; loc:`LDN`NY`LDN] employees:10+3?1000)

office
`sym` | `loc`  | employees
---------------------------
`TS`  | `LDN`  | 875
`KX`  | `NY`   | 354
`C`   | `LDN`  | 1007

/ columns SYM and LOC are KEYED

employee: ([] name:`ryan`charlie`arthur; employer:`TS`KX`KX; city:`LDN`NY`NY)

employee
name   |employer|city
-------------------
ryan   |TS      |LDN
charlie|KX      |NY
arthur |KX      |NY
```

[fkey] 1. Set the fkey for employee table

```q
/ fkey the [employer] and [city] columns from [employee]
/ to the domain of [office] table

exec `office$flip (employer;city) from employee
0 1 1

/ since the [office table] has 2 keyed columns
/ you have to "cast" the 2 columns as fkey
/ ignore the flip syntax
/ set fkey by linking the [EMPLOYER column] and [CITY] from [employee table]
/ to the domain of [office table] (keyed columns)

/ ryan    -> look for TS and LDN in office table, found on row 0
/ charlie -> look for KX and NY in office table, found on row 1
/ arthur  -> look for KX and NY in office table, found on row 1
```

[fkey] 2. Add new column to employee table

```q
/ from [employee table]
/ add new column called [empOffice]
/ which returns the INDEX LOCATION of fkey [employer] and [city] columns
/ from the [office table]

update empOffice:`office$flip(employer;city) from `employee

employee
name   |employer|city|empOffice
-----------------------------
ryan   |TS      |LDN |	0
charlie|KX      |NY  |	1
arthur |KX      |NY  |	1

/ adds new column [empOffice], and sets fkey to domain of [office table]

/ ryan    -> look for TS and LDN in office table, found on row 0
/ charlie -> look for KX and NY in office table, found on row 1
/ arthur  -> look for KX and NY in office table, found on row 1
```

[fkey] 3. Check meta of employee table

```q
/ check if the new column empOffice has an fkey

meta employee
c        |t|  f   | a
----------------------
name     |s|	  |	
employer |s|	  |
city     |s|	  |
empOffice|j|office|

/ meta shows us [empOffice] has an foreign key 
/ referencing the [office table]
```

[fkey] 4. Retrieve fkey values

```q
/ add to the [employee table]
/ new columns [sym] and [loc] from the [office table]
/ using the fkey from the [empOffice column]

update empOffice.sym, empOffice.loc from employee

name   |employer|city|empOffice| sym| loc
-------------------------------------------
ryan   |   TS   |LDN |	 0     | TS | LDN
charlie|   KX   |NY  |   1     | KX | NY
arthur |   KX   |NY  |   1     | KX | NY

/ prev set [empOffice column] as foreign key
/ to the domain of [office table]
/ so you can pull in values from [office table]
```

### [fkey] FKEY Problem Set - TS

```q
book: ([id:`fmgoh`fddig`lefhe`bfjnf] name:`jim`allen`bob`sherman)

book
`id`    | name
----------------
`fmgoh` | jim
`fddig` | allen
`lefhe` | bob
`bfjnf` | sherman

trade:([] date:2021.01.01; time: 09:00; sym:`D`AA`UPS`A; price:109 93 34 56; size: 100; cond: " ","B","A","C"; bookID:`fmgoh`fddig`lefhe`bfjnf)

trade
date      |  time | sym |price| size|cond|bookId
-------------------------------------------------
2021.01.01| 09:00 |   D | 109 | 100 |    | fmgoh
2021.01.01| 09:00 |  AA |  93 | 100 | B  | fddig
2021.01.01| 09:00 | UPS |  34 | 100 | A  | lefhe
2021.01.01| 09:00 |   A |  56 | 100 | C  | bfjnf
```

[fkey] 1. Insert new fkey column into trade table

```q
/ Insert new fkey column into [trade table]
/ called [owner], linking the [trade] and [book] table
/ using [bookID]

update owner: `book$bookId from `trade

date      |  time | sym |price| size|cond|bookId | owner
---------------------------------------------------------
2021.01.01| 09:00 |   D | 109 | 100 |    | fmgoh | fmgoh
2021.01.01| 09:00 |  AA |  93 | 100 | B  | fddig | fddig
2021.01.01| 09:00 | UPS |  34 | 100 | A  | lefhe | lefhe
2021.01.01| 09:00 |   A |  56 | 100 | C  | bfjnf | bfjnf

/ so if you ADD the column set as an fkey (bookID)
/ it returns the DOMAIN of the keyed table (keyed columns)
/ [bookID] from [trade] was set as fkey to [book]
/ adding the column returns the keyed column from [book]
```

[fkey] 2. Check the meta to confirm fkey

```q
meta trade

c      | t |   f  | a
-----------------------
date   | d |	  |	
time   | u |	  |	
sym    | s |	  |	
price  | j |	  |	
size   | j |	  |	
cond   | c |	  |	
bookID | s |	  |	
owner  | s | book |	


/ [owner column] from [trade] has an fkey
/ to [book table]
```

[fkey] 3. Retrieving fkey values

```q
/ Join the [book table] onto the [trade table]
/ and add the name of the person who did trade

update owner.name from `trade

date      |  time | sym |price| size|cond|bookId | owner | name
---------------------------------------------------------------
2021.01.01| 09:00 |   D | 109 | 100 |    | fmgoh | fmgoh | jim
2021.01.01| 09:00 |  AA |  93 | 100 | B  | fddig | fddig | allen
2021.01.01| 09:00 | UPS |  34 | 100 | A  | lefhe | lefhe | bob
2021.01.01| 09:00 |   A |  56 | 100 | C  | bfjnf | bfjnf | sherman

/ [owner column] has an fkey set to [book table]
/ so you use that column to pull values from [book table]
/ name = column name from book you want to retrieve values from
```


<a name="functions"></a>
### 🔴 8. Functions
[Top](#top)

### 🔵 [func 1.0] Intro to Functions
<a name="func_intro"></a>

[func 1.1] What is a lambda expression?

```q
/ a lambda expression is an anonymous function
```

[func 1.2] What are local variables?

```q
/ a variable that is created and exist only for the duration of an application
```

[func 1.3] What is function prefix syntax?

```q
/ a unary function is a function with only one parameter
/ when you separate the function from its argument , this is called a prefix syntax

{x*x} 5
25

/ in this case, 5 is an implicit variable
```

### 🔵 [func 2.0] Functions on Strings - AQ
<a name="func_strings"></a>
[Top](#top)

```q
/ create a function that uses SSR (string search replace)
/ to convert sym `welcome to string "welcoME"

/ quick reminder on SSR

ssr["hello ryan where is ryan";"ryan";"john"]
hello johhn where is john
```

[func 2.1] Pass single sym through function

```q
f: {ssr[(string x);y;z] }
f[`welcome;"me";"ME"]
"welcoME"

/ so x gets converted from `sym to string
/ then SSR is run on string "welcome"
/ and replaces "me" with "ME"
```

[func 2.2] re-written as lambda function

```q
/ alternative syntax (lambda function)

{ssr[string x;y;z]} [`welcome; "me";"ME"]
"welcoME"

/ did not define function (lambda)
/ uses implicit arguments x, y, z
/ passes arguments immediately after function
/ string x = ONLY applies to argument x
```

[func 2.3] Alternative method to call arguments 

```q
/ alternative syntax (lambda + alt method to call argument)

{ssr[string x;y;z]} [ ; "me";"ME"] `welcome
"welcoME"

/ so sym `welcome is implicit argument x
/ since arguments y and z are already defined as "me" and "ME"
/ this is useful when iterating through a LIST of syms
```

[func 2.4] re-write function to pass a LIST of syms

```q
/ instead of converting one sym
/ need to iterate function through list of syms

f:{ssr [string x;y;z]} 
f[ ;"me";"ME"] each `welcome`home`mermaid
"welcoME"
"hoME"
"MErmaid"

/ function remains the same
/ but when you CALL the function, need adverb EACH
/ this iterates through each sym
/ the list of syms `welcome`home`mermaid gets passed through x
/ REQUIRES x to be left blank inside [ ] 
/ while locking in arguments y and z as constants
```

[func 2.5] re-written as lambda function

```q
/ lambda notation

{ssr [string x;y;z]} [ ;"me";"ME"] each `welcome`home`mermaid
"welcoME"
"hoME"
"MErmaid"

/ function remains the same
/ but when you CALL the function, need adverb EACH
/ this iterates through each sym
/ the list of syms `welcome`home`mermaid gets passed through x
/ REQUIRES x to be left blank inside [ ] 
/ while locking in arguments y and z as constants```
```

### 🔵 [func 3.0] Projected Functions - TS
<a name="func_proj"></a>
[Top](#top)

```q
/1. create first function called raise

raise: {x xexp y}
raise [10; 2 3 4]
100 1000 1000f
 
/ calls x = 10 and y = 2 3 4
```

```q
/2. create second function called g, which projects function raise
/ keeps x constant @ 10

g: raise [10; ]
g 1 2 3
10 100 1000

/ you've already created function raise previously
/ so g is a PROJECTION of the original function RAISE
/ so x = constant 10
/ y becomes arguments you call in (1 2 3)
```

```q
/3.  create another function square, which projects function raise

square: raise[ ;2]
square 1 2 3
1 4 9

/ in this case, leaves first argument blank (x)
/ and keeps second argument constant at 2
/ calls in 1 2 3 for x xexp 2
```

### 🔵 [func 4.0] Function Loop Problem Set - TS 
<a name="func_loop"></a>
[Top](#top)

```q
/ generate list of 100 random numbers from 0-99
/ sum all values in list > 50 using while loop

d: 100?100
i: 0
r1: 0

while [i < count d; if [d[i]>50; r1+:d[i] ]; i+:1]

/ d = list of 100 random numbers from 0-99
/ i = iterative counter (goes from 0-99). Counts through every element of list d
/ r1 = result of while loop

/ while i is less than total number of items in list d (99)
/ if value of list d at index position i is less than 50
/ add this value to results list (r1)
/ then go onto next iteration (i+1)

/ remember, WHILE LOOPS -> if first argument is TRUE, execute all arguments that follow
/ WHILE LOOP = used as iterative counter through all elements of list d (0-99)
/ IF STATEMENT = tests IF condition true, add to list
```

### [func 4.1] Vector Operation Solution

```
HOWEVER, much faster using vector operations:

r2: sum d where d > 50

/ so use vector operations whenever possible
/ also a lot more flexible:

max sum d where d>50
min sum d where d>50
avg sum d where d>50
```

### 🔵 [func 5.0] Prime Numbers Problem Set - TS
<a name="func_prime"></a>
[Top](#top)


```q
/ create function that finds primes up to argument x
/ since you are returning list of numbers
/ will require an 1) empty list
/ and 2) an iterator to check every number up to x

/ iterator starts from 1
/ if iterator is prime, append to list r (need to use ,: NOT sum)
/ then go onto next number
/ keep checking until WHILE condition is no longer true (a<n)
/ then return list r

findprime: {[n] r:(); a:1; while [a<n; if[isprime[a];r,:a]; a:a+1];r}
findprime 10 
2 3 5 7

/ n = single argument
/ r() = empty list thats gonna contain our result
/ a starts from 1 (iterator)
/ while a(1) < n = TRUE
/ if a = prime number,
/ append a to list r (r,:a = append a to list r)
/ go through every value of a (a+:1)
/ finally, return our list r

/ in other words..
/ starting from 1, look up to our argument
/ checking if each number is a prime number
/ and if it is, append it to our list (r)
/ finally, return the list of primes
/ still need to write the isPrime function

/ a:1, n:5
/ while a(1) < n(5) = TRUE
/ if a(1) = prime = FALSE
/ skip rest of while loop
/ a:a+1 = 1+1 = 2

/ while a(2) < n(5) = TRUE
/ if a(2) = prime = TRUE
/ append a(2) to r (2)
/ a:a+1 = 2+1 = 3

/ while a(3) < n(5) = TRUE
/ if a(3) = prime = TRUE
/ append a(3) to r (2,3)
/ a:a+1 = 3+1 = 4

/ while a(4) < n(5) = TRUE
/ if a(4) = prime = FALSE
/ skip rest of while loop
/ a:a+1 = 4+1 = 5

/ while a(5) < n(5) = FALSE
/ skips entire while loop
/ returns r (2, 3)
```

```q
/ isPrime function

/ create function with 1 argument input
/ and checks whether argument is Prime (True) or not (False)

/ prime = any num can only % by itself and 1
/ prime numbers begin on 2
/ will need 3 components:
/ 1. number < 2 (not prime)
/ 2. number = 2 (prime)
/ 3. number > 2 (could be prime)

/ the outcomes for component 1 and 2 are quite binary. 
/ component 3 -> requires you to check if number has any factors
/ which means dividing by every number up to x number

/ general reminder:
/ IF brackets [contain condition + statement to execute if true]
/ WHILE brackets [contain condition + statement to execute if true]

isprime:{if[x<2; :0b]; a:2; while[a<x; if[(x mod a)=0; :0b]; a+:1]; 1b}

Component 1 (number < 2)
/ if argument less than 2, return FALSE 0b (not prime)
/ since primes cannot be less than 2
/ if[x<2; :0b]
/ single colon : means return. nothing after gets executed
/ if x = 1
/ x(1) < (2) (TRUE) so returns 0b (not prime)
/ if FALSE, then moves onto NEXT statement

Component 2 (number = 2)
/ Create variable a, which begins on 2
/ a is your iterator (will check every number up to x number)
/ while[a<x; if_false_skip_this_entire_while_loop]; 1b
/ while condition a < x is FALSE
/ skip ENTIRE while loop
/ and go straight to the end, return TRUE 1B (prime)
/ if x = 2
/ x(2) < a(2) = FALSE. Skip while loop
/ goes to end, returns 1b (True)

Component 3 (number > 3)
/ while condition a < x is TRUE (iterator < x number)
/ check if a is a factor of x number
/ this check is done by x mod a = 0 (even number/factor exists = NOT PRIME)
/ if TRUE, return false :0b
/ otherwise, iterate through until WHILE condition (a<i) is no longer true

/ if x = 5
/ a(2) < x(5) = TRUE
/ x(5) mod a(2) = 0 = FALSE = skips :0b
/ a:a+1 so 2 + 1 = 3
/ a(3) < x(5) = TRUE
/ x(5) mod a(3) = 0 = FALSE = skips :0b
/ a:a+1 so 3+1 = 4
/ a(4) < x(5) = TRUE
/ x(5) mod a(4) = 0 = FALSE = skips :0b
/ a(5) < x(5) = FALSE, SKIPS entire while loop
/ goes to end, returns 1b (True) 
```

[func 5.1] Vector Based Solution

```q
/ the above function uses control statements and loops
/ but this is very slow
/ instead, can re-write without do or while loops 
/ using a vector based solution
```

[func 5.2] isprime Vector Solution

```q
/ re-write isprime function using vector based solution

/ original function

isprime:{if[x<2; :0b]; a:2; while[a<x; if[(x mod a)=0; :0b]; a+:1]; 1b}

/ we can rewrite the while loop portion

/ instead of looping through every iteration of argument x 
/ we can simply use til to generate a list

{til x} 10
0 1 2 3 4 5 6 7 8 9

/ removes first 2 elements (since not prime)

{2_til x} 10
2 3 4 5 6 7 8 9
/ drops 0, 1 since not prime

/ check each number if it is a factor of argument x(10)

{x mod 2_til x} 10
0 1 2 0 4 3 2 1

/ 10 mod 2 = 0
/ 10 mod 3 = 1
/ 10 mod 4 = 2
/ 0 means no remainder = factor of x = NOT PRIME

/ show us factors of argument x

{0=x mod 2_til x} 10
10010000b
/ shows us factors of argument 10
/ 1 = true
/ 0 = false

/ are there ANY factors of 10? (mod = 0)

{any 0=x mod 2_til x} 10
1b
/ TRUE, because list contains SOME factors of 10

/ does the list NOT contain any factors of 10?

{not any 0=x mod 2_til x} 10
0b
/ FALSE, because list DOES contain factors of 10
/ hence, NOT prime

/ still need component for numbers less than 2
/ so re-use the x<2 IF/Else clause

isprimeB: {if[x<2; :0b]; not any 0=x mod 2_til x}
isprimeB 10
0b

/ x(10)<2 = FALSE, skips if statement
/ goes onto second statement
/ FALSE, 10 is NOT prime
```

[func 5.3] findprimes Vector Solution

```q
/ re-write findprimes function using vector based solution

/ original findprime function:

findprime: {[n] r:(); a:1; while [a<n; if[isprime[a];r,:a]; a:a+1];r}

/ use til instead of while loop

{til x} 10
0 1 2 3 4 5 6 7 8 9

/ perform isprime function on EACH of the numbers
{isprimeB each til x} 10
0011010100b

/ returns us a list of booleans
/ does this list contain any prime?
/ 0 = no
/ 1 = yes

/ convert booleans BACK into numbers
/ want 1 (true) = prime turned back into numbers
/ use WHERE function

findprimesB: {where isprimeB each til x}
findprimesB 10
2 3 5 7
```

### 🔵 [func 6.0] Function Problem Set 1 - TS
<a name="func_set1TS"></a>
[Top](#top)

[func 6.1] Volume of cone function

```q
/ create func called volc that accepts 2 arguments (r and h)
/ returns volume of cone
/ vol of cone = 1/3 * pi * r^2 * h
/ pi = -4 * atan -1

volc: {[r;h] pi:-4*atan -1; pi*r*r*h%3}
volc[2;3]
12.57

/ define arguments [r;h] first
/ define variable pi
/ must have space after atan and before -1
/ no space for volc[2;3]
```

[func 6.2] Area and Volume of cone function

```q
/ create function, called sph, that accepts argument radius
/ and returns the area and volume of a cone as a dict

/ volume = 4/3 * pi * r^3
/ area = 4 * pi * r^2
/ pi = -4 * atan -1

sph:{[r] pi:-4 * atan -1; v:(4%3)*pi*r xexp 3; a:4* pi * r xexp 2; `area`volume!(a;v)}
sph[1]

key    | value
----------------
area   | 12.56
volume | 4.188

/ define argument [r]
/ you can define variables with functions inside your function!
/ define variable pi with formula
/ define variable a with formula
/ define variable v with formula
/ then you can create dictionary using the variables you defined
/ show dictionary with keys `area `volume against values a and v
/ create keys as syms (`area`volume) mapped to values defined by your variables (a;v)
```

[func 6.3] Implicit Arguments and Global Variables

```q
/ create function, setc, that takes 1 implicit argument
/ and sets the value of global variable c to that argument

c:10

setc: {x::c}
setc[15]
10

/ set global variable c to 10
/ x is your implicit variable
/ you assign x the value of global variable c
/ so WHATEVER value you call using setc, it assigns
/ that value to the global value of q
/ so even though you call func with 15
/ the output is 10 (global variable)
```

[func 6.4] Projected Functions

```q
/ raise:{x xexp y}
/ create projection of raise called root
/ which calculates the square root of argument 
/ ie, root[9] = 3

raise: {x xexp y}
root: raise[ ; 0.5]
root[9]
3

/ first define function raise
/ then we take a PROJECTION of that function, rename as root
/ and we set the y variable CONSTANT as 0.5
/ this allows the projected function ROOT to only allow 1 input as x
/ so the projected function will always be x xexp 0.5
```

[func 6.5] Convert all elements of list l to a string

```q
l: (100;`price;1b)

string l
"100"
"price"
"1b"

/ l is a list of long, sym, and boolean
/ simply using the "string" function, converts all elements to strings
/ mixed lists have to be contained in parathesis ( )
```

[func 6.6] Given string st, replace "cow" with "kangaroo"

```q
/ st: "the cow jumped over the moon"

st: "the cow jumped over the moon"
ssr [st; "cow";"kangaroo"]
"the kangaroo jumped over the moon"

/ ssr = string search replace.
/ first condition = string
/ second condition = what to target
/ third condition = what to replace with
```

[func 6.7] Create function that takes [name;age] and returns "hello age year old name"

```q
/ create function, sayHi, that takes 2 arguments: name and age
/ and returns "hello age year old name"
```

```q
sayHi:{[name;age] "hello " , string[age] , " year old " , name}
sayHi["joe";90]
hello 90 year old joe

/ name and age are your arguments
/ name is a string
/ age is an int
/ the output is a list of chars (or one long string)
/ so you have to convert your [age] argument to a string
/ and join them together using string concatenation
/ string concatenation simply done with a comma ,
/ when you define argument "joe" have to use parathesis otherwise wont work
```

[func 6.8] Arithmetic on Lists

```q
/ I have a box of 7 eggs, and the weights are
/ eggs: 10 20 30 40 50 60 70
/ find the median and average weight of these eggs

med eggs
40f

avg eggs
40f

/ note, division will always return a float
/ apparently same with med and avg functions
```

[func 6.9] Weighted Averaged WAVG Function

```q
/ I sold 2 boxes of eggs
/ one box had 10 eggs and i sold each egg for 50 each
/ the other box had 20 eggs and i sold each for 100 each
/ find the average price paid per egg

10 20 wavg 50 100
83.3

/ to find the average price per egg
/ you want to find the weighted average of the 2 lists
/ wavg = weighted average function
/ qty1 qty2 wavg value1 value2
```

[func 6.10] Moving Average Window Functions

```
/ generate list k with 10 random ints
/ find moving average with window size of 3

k: 10?10
8 7 9 9 7 7 1 9 1 0

mavg[3;k]
8 7.5 8 8.3 8.3 7.6 5 5.6 3.6 3.3
```

```q
/ Find the 3 largest numbers in list k

desc k
9 9 9 8 7 7 7 1 1 0

3#desc k
9 9 9 

/ take 3 of the largest from k, sort by desc
```

```q
/ Find the difference between the successive elements of k

k
8 7 9 9 7 7 1 9 1 0

deltas k
8 -1 2 0 -2 0 -6 8 -8 -1

/ the deltas functions returns the difference (delta) of each element
/ 8-0 = 8
/ 7-8 = -1
/ 9-7 = 2
/ etc
```

[func 6.11] Factorial Function using While Loops

```q
/ Create function factw, which uses a loop to write a factorial function
/ factorial = multiply every iteration up to number x

factw:{i:1; r:1; while[i<x; r*:i; i+:1];:r*x}
factw 4
24

/ while loop, so need some sort of iterative counter (i)
/ want to mutiply every iteration of x, up to x 
/ so also need an empty list to store these iterations (r) 
/ first define i:1 (no point starting at 0)
/ and define r:1 (this is the list of numbers you want to multiply)
/ while i is less than implicit argument x (your input number)
/ multiply i with r, and r becomes that new number (r*:i mean r: r*i)
/ then move onto next iteration (i+:1 means i:i+1)
/ keep running this while loop until x-1, then stop executing
/ finally, return r * x (your original input)
```

```q
/ alternative syntax (shorter)

factw:{r:i:1; while[i<=x; r*:i; i+:1];r}
factw 3

/ x is implicit variable= 3
/ set r = i = 1
/ while i(1) <= x(3) TRUE, execute following statements
/ r = r(1) * i(1) = 1
/ i = i(1) + 1 = 2

i(2) <= x(3) TRUE, so continue executing
/ r = r(1) x i(2) = 2
/ i = i(2) + 1 = 3

i(3) <= x(3) TRUE
/ r = r(2) x i(3) = 6
/ i = i(3) + 1 = 4

i(4) <= x(3) FALSE, so returns r = 6
```

[func 6.12] Factorial Function using Vector Conditional

```q
/ re-write the factorial function as factp WITHOUT using loops
/ must use vector conditional approach

/ to replace WHILE loop using vector conditional
/ usually replaces with til function

til 4
0 1 2 3

1_til 4
1 2 3

prd 1_til 4
1*2*3

4 * prd 1_til 4
1*2*3*4

/ so putting it all together, replacing variable with x

factp:{x*prd 1_til x}
factp 4
24

/ KEY TAKEAWAY
/ prds = multiplies all elements together
/ must remember to drop first element 0 (otherwise will all be 0)
/ must multiple original x back in
/ since til only generates list up to, but not including x
```

[func 6.13] Timing Calculations

```q
/ Demonstrate which calculation is faster,
/ factorial using loops or via KDB (vector conditional)
/ use \ts to time
/ do function useful (do x number times)

\ts do[1000;factw 12]
4 1008

/ 4 miliseconds 1008 bytes of memory

\ts do[1000;factp 12]
0 1008

/ 0 miliseconds 1008 bytes of memory
```

[func 6.14] Protetcted Evaluations on Functions

```q
/ Create function called safefact
/ that wraps factp with protected evaluation
/ to return null On instead of error 
/ when calling on a negative number

safefact:{@[factp; x; 0N]}
safefact -10
0N

/ you "wrap" your function using the @ operator ("apply")
/ @ = apply 
/ first condition = factp function
/ if TRUE, return x
/ if FALSE, return ON
```

[func 6.15] If/Else Statements (w reverse operator)

```q
/ Write a function called isPalindrome 
/ that accepts single argument as a list of ints 
/ returns `yes if list of ints is a palindrome
/ otherwise return `no

/ palindrome = same forwards + backwards
/ example = 1 2 3 3 2 1

isPalindrome:{$[x~reverse x;`yes;`no]}
isPalindrome 1 2 2 1
yes

/ since we are taking in 1 argument
/ with a binary outcome (true vs false)
/ need to use if/else statement $ [ ]
/ implicit argument x is a list of integers
/ need to utilize REVERSE function 
/ to compare if x = reverse x
```

[func 6.16] Find the sum of all multiples of 3 or 5 below 1000

```q
/ check every number up to 1000
/ if its a factor of 3 or 5
/ x mod 3 = 0
/ x mod 5 = 0

/1. generate list of ints from 0-999

til 1000
0 1 2 3...999

/2. check if number is a factor of 3 or 5

{(0=x mod 3) or (0=x mod 5)} [til 1000]
1001011

/ you get a list of booleans
/ ie, true, the number is a factor of 3 or 5
/ IMPORTANT! the 0 = has to come in FRONT of (0=x mod 5)
/ (x mod 5 = 0) does NOT work

/3. CONVERT list of booleans to their numbers, use WHERE

where {(0=x mod 3) or (0=x mod 5)} [til 1000]
0 3 5 6 9 10 12 15 18 20 21 

/4. lastly, use sum to add up all numbers in the list

sum where {(0 = x mod 3) or (0 = x mod 5)} [til 1000]
233168

/ by using anonymous function, you can perform QSQL (sum where)
/ as well as call argument x as a list (til 1000) in place
/ x mod 3 and x mod 5 = search for any multiples of 3 or 5
/ since dividing by a factor will be 0
/ oddly enough, the 0 = in (0 = x mod 3) HAS TO come first
/ (x mod 3 = 0) doesn't work for some reason
```

### 🔵 [func 7.0] Functions Problem Set 1 (easy) - AQ
<a name="func_set1AQ"></a>
[Top](#top)


[func 7.1] write function f that calculates the square of a number

```q
f:{[a] a*a}

```

[func 7.2] write new funciton g, which takes square of first argument divided by square of second argument

```q

g: {(x*x) % (y*y)}
g [2;4]
0.25
```

[func 7.3] execute g with arguments a and b, store this to c

```q
c: g[a;b] 

```

[func 7.4] create dyadic function f1 indicating whether the product of 2 numbers is greater than sum

```q
/ dyadic means 2 arguments

f1: {(x*y) > x+y}
```

[func 7.5] write this func with proper KDB order of operations g1: x^5-3x^2 + 5

```q
/ then call the function when x=4

g1:{((x xexp 5) - 3*(x xexp 2))+5}
g1[4]
981f

/ note - you have to put 3*(x xexp 2)
/ an int next to parenthesis won't automatically mutiply
```

[func 7.6] create function that calculates area of triangle

```q
/ then call func with arguments height = 7, base = 10

t:{x * y % 2 }
t [7;10]
35
```

[func 7.7] create function that calculates the sum of 2 squares of a number x

```q

f: {x xexp 2 + x xexp 2}
f: {(x*x) + x*x}
```

[func 7.8] create a function that calculates a^3+b^2+c

```q
/ then call your function with arguments: 13,3,6

f:{(x xexp 3) + (y xexp 2) + z}
f [13;3;6]
2212

/ have to use parathensis ( ) around xexp
```

[func 7.9] BMI is weight divide by height squared. create an implicit formula

```q
bmi: { x % (y*y) }
```

[func 7.10] create a func called perimeters, which will take perimeter of a square and return its area

```q
perimeter:{ (x%4) xexp 2}
perimeter[8]
4
```

[func 7.11] Car Depreciation Problem

```q
/ a car depreciates 15% every year for the first 3 years
/ then 8% every year for the next 3 years
/ create func k to find value after 6 years
/ with original value 15000

k: {x*(0.85 xexp 3)*(0.92 xexp 3) }
k [15000]
7173.1765
```

### 🔵 [func 8.0] Functions Problem Set 2 (med) - AQ
<a name="func_set2AQ"></a>
[Top](#top)


```q
/ load fakedb.q

makehdb[`:hdb;10;1000;1000]

/ `: directory name
/ 10 = number of partitions
/ 1000 = trades in each table
/ 1000 = number of quotes in each table

\l hdb

\a
`depth`quotes`trades
```

```q
select from trades

date       | sym  | time	               | src | price | size
--------------------------------------------------------------------
2014-04-21 | AAPL | 2014-04-21T08:00:44.437000 |  O  | 25.34 | 1785
2014-04-21 | AAPL | 2014-04-21T08:04:41.246000 |  L  | 25.34 |  427
2014-04-21 | AAPL | 2014-04-21T08:04:47.586000 |  L  | 25.34 | 1528
2014-04-21 | AAPL | 2014-04-21T08:08:09.192000 |  L  | 25.35 | 8136
2014-04-21 | AAPL | 2014-04-21T08:11:23.934000 |  L  | 25.35 | 8945
```

[func 8.1] create function with 3 arguments (symbols, startdate, enddate)

```q
/ name this func tradeticks
/ queries a date range and sym filter
/ taking in 3 arguments (startdate, enddate, symbols)

tradeticks:{ [startdate;enddate;symbols] 
            select date, sym, time, size, price 
            from trades
            where date within (startdate;enddate), sym in symbols}
            
tradeticks[2021.11.03;2021.11.04;`MS]

date      sym time         size  price
--------------------------------------
2021-11-03 MS 09:30:01.423 63000 58.46
2021-11-03 MS 09:30:01.768 95500 81.06
2021-11-03 MS 09:30:01.928 13400 82.90

/ date (from trades) within (startdate;enddate) from ARG
/ COL WITHIN ARG

/ sym (from trades) in symbols (from arg)
/ COL in ARG
```

[func 8.2] Extracting temporal data from Timestamp

```q
select from depth

depth
time                       sym  price
-------------------------------------
2021-11-07T08:04:21.425000 YHOO 33.99
2021-11-07T08:14:59.215000 ORCL 35.16
2021-11-07T08:21:30.944000 NOK  42.01

/ notice [time column] datatype is timestamp (includes date and time)

meta depth

c    | t | f | a
------------------
time | p |   |		
sym  | s |   | g
bid1 |   | f |		

/ time column is datatype p = timestamp
```
[func 8.3] Extract the TIMESTAMP from timestamp

```q
select time from depth

time
--------------------------
2021-11-07T08:04:21.425000
2021-11-07T08:14:59.215000
2021-11-07T08:21:30.944000

/ since time is already of timestamp datatype, just need to extract
```

[func 8.4] extract the DATE from timestamp

```q
select `date$time from depth

time
----------
2021-11-07
2021-11-07
2021-11-07

/ extract time, then cast timestamp to date datatype
```
[func 8.5] extract the TIME from timestamp

```q
select time.time from depth
select `time$time from depth

time
------------
08:04:21.425
08:14:59.215
08:21:30.944

/ time column is in timestamp format (date + time)
/ to strip out only the time
/ need to cast it as a time datatype
```

[func 8.6] create tradeticks2 with additional parameters: starttime and endtime

```q
/ this func will only extract the trades that fall within time range
/ original equation's parameters = sym, startdate, enddate
/ hint - need to extract the time portion from timestamp e.g time.time or `time$time

tradeticks2:{ [startdate; enddate; symbols; starttime; endtime] 
              select from trades where 
	      date within (startdate;enddate), 
	      sym in symbols,
              `time$time within (starttime;endtime) }

tradeticks2[2021.11.03;2021.11.04;`MS; 09:30:00;09:31:00]

date      sym time         size  price
--------------------------------------
2021-11-03 MS 09:30:17.569 11400 79.89
2021-11-03 MS 09:30:17.573 18400 96.09
2021-11-03 MS 09:30:21.264 8500 101.73

/ [time column] from trades is in the timestamp temporal format of 2021.01.01D09:00:00
/ need to extract only the time portion by CASTING as time
/ such that it matches your arguments for starttime and endtime
```

[func 8.7] create function3, but uses a start timestamp and end timestamp as parameters

```q
/ arguments = symbols, starttimestamp, endtimestamp
/ timestamp args = TIMESTAMP format

/ break up the query such that DATE and TIME
/ are extracted from the TIMESTAMP argument
/ and queried separately

tradeticks3:{ [ticker;starttimestamp;endtimestamp]
              select from trades where
              sym in ticker,
              `date$time within `date$(starttimestamp;endtimestamp),
              `time$time within `time$(starttimestamp;endtimestamp) }

/ arguments are TIMESTAMPS datatype = DATE + TIME

/ need to extract [DATE] from [timestamp value] from [time column]
/ and query [DATE] from your [timestamp argument]
/ cast both as `date$

/ need to extract [TIME] from [timestamp value] from [time column]
/ and query [TIME] from your [timestamp argument]
/ cast both as `time$

tradeticks3[2021.11.07D09:00;2021.11.07D10:00;`AAPL]

date       sym  time         size  price
----------------------------------------
2021-11-07 AAPL 09:30:21.088 20600 62.30
2021-11-07 AAPL 09:30:21.490 900   59.15
2021-11-07 AAPL 09:30:22.052 1500  95.94
```

```q
/ i dont get this

/ Update func3 such that if the starttimestamp is = first second of day, 
/ and endtimestamp = last second of day
/ then it DOESN'T execute the WHERE filter on the time column

/ hint start of day timestamp = 1d xbar timestamp or
/ `timestamp$00:00 + `date$timestamp

/ to get endtime, subtract 1 from the start of next date
/ -1+`timestamp$1+`date$endtimestamp

tradeticks3:{ [starttimestamp; endtimestamp; symbols] 
             $[starttimestamp = `timestamp$00:00 + `date$starttimestamp) and
              (endtimestamp = -1 + `timestamp$1 + `date$endtimestamp);
            
	    / call tradeticks
            	    tradeticks[`date\$starttimestamp;`date$endtimestamp;symbols];
            
	    /call tradetick3
            tradeticks3[starttimestamp;endtimestamp;symbols]] }

/ so this is using a simple IF/OR statement
/ IF first condition is true
/ execute first statement
/ otherwise, execute last statement
```

[func 8.8] create function, quotechanges, to retrieve data when bid or ask changes

```q
/ create a function called quotechanges
/ select from quote table
/ for a given date list and symbol
/ retrieve the data where either bid or ask price changes

select from quotes

date       | sym  | time                       |  bid  |  ask
---------------------------------------------------------------
2014-04-21 | AAPL | 2014-04-21T08:05:56.520000 | 25.34 | 25.35
2014-04-21 | AAPL | 2014-04-21T08:18:39.592000 | 25.34 | 25.35
2014-04-21 | AAPL | 2014-04-21T08:23:23.765000 | 25.33 | 25.38
2014-04-21 | AAPL | 2014-04-21T08:33:55.105000 | 25.34 | 25.39


quotechanges:{ [dates; symbols]
		select from quotes where
		date in dates, 
		sym in symbols,
		(differ bid) or differ ask}

/ differ bid or differ ask = any change in bid or ask
```

### 🔵 [func 9.0] Functions Problem Set 3 (med/hard) - AQ
<a name="func_set3AQ"></a>
[Top](#top)

```q
/ load fakedb.q

\l hdb

\a
`depth`quotes`trades
```

[func 9.1] Write func that calcs the avg spread between bid and ask

```q
/ write a func that calc the avg spread between bid and ask per date 
/ and sym from the quote table 
/ for a given date range and sym list

/ args = startdate; enddate; symbols
/ need new col called avgspread

avgspread:{ [startdate; enddate; symbols]
            select avgspread: avg ask-bid by date, sym 
	    from quotes
	    where date within (startdate;enddate), 
	    sym in symbols}

avgspread[2021.11.09; 2021.11.11; `GOOG]

date       | sym  | avgspread
-----------------------------
2021-11-09 | GOOG | 1.59
2021-11-10 | GOOG | 1.60
2021-11-11 | GOOG | 1.60
```

[func 9.2] Create func that calcs the high, low, open, close  

```q
/ create function called dailystats1
/ which calcs the High, Low, Open, Close 
/ for a given date range and list of instruments

/ HLOC buckets by date and sym
/ for given date range = need [start date] and [end date] as args
/ args = startdate, enddate, symbols

dailystats1: { [startdate; enddate; symbols]
               select high: max price, low:min price, open: first price,
               close: last price
               by date, sym from trades
               where date within (startdate;enddate), sym in symbols}

dailystats1[2021.10.01; 2021.11.11; `AAPL]

date       | sym  | high  | low  | open | close
-------------------------------------------------
2021-11-07 | AAPL | 109.9 | 50.0 | 78.6 | 68.0
2021-11-08 | AAPL | 109.9 | 50.0 | 60.8 | 90.4
2021-11-09 | AAPL | 109.9 | 50.0 | 55.1	| 77.0
2021-11-10 | AAPL | 109.9 | 50.0 | 72.2	| 93.3
2021-11-11 | AAPL | 109.9 | 50.0 | 62.3	| 76.1
```

[func 9.3] Using previous function, add on vwap column

```q
/ create function called dailystats2
/ which is the same as dailystats1
/ but also calculates the vwap value

dailystats2: { [startdate; enddate; symbols]
		select high:max price, low: min price, open: first price,
		close: last price, vwap: size wavg price
		by date, sym
		from trades
		where date within (startdate;enddate), sym in symbols}

dailystats2[2021.10.01; 2021.11.11; `AAPL]

date       | sym  | high  | low  | open | close | vwap
-----------------------------------------------------------
2021-11-07 | AAPL | 109.9 | 50.0 | 78.6 |  68.0 | 2,570.77
2021-11-08 | AAPL | 109.9 | 50.0 | 60.8 |  90.4 | 2,568.23
2021-11-09 | AAPL | 109.9 | 50.0 | 55.1	|  77.0 | 2,448.23
2021-11-10 | AAPL | 109.9 | 50.0 | 72.2	|  93.3 | 2,349.31
2021-11-11 | AAPL | 109.9 | 50.0 | 62.3	|  76.1 | 2,973.91

/ KDB has a built in function called [WAVG]
/ used for calculating weighted averages
/ [size wavg price] = VWAP calculation
```

[func 9.4] Bucketing data by time period using xbar

```q
/ create function, dailystats3
/ which is the same as dailystats2
/ but includes a BUCKETING value of [type timespan] using xbar
/ add [bucket] as an arg

dailystats3: { [startdate; enddate; symbols; bucket]
		select high:max price, low: min price, open: first price,
		close: last price, vwap: size wavg price
		by date, sym, bucket xbar time
		from trades
		where date within (startdate;enddate), sym in symbols}

dailystats3[2014.04.20; 2014.04.21;`AAPL; 08:04:47.586000]

date	   | sym | time                       |high | low |open |close|vwap
-----------------------------------------------------------------------------
2014-04-21 | AAPL| 2014-04-21T07:39:19.548000 |25.39|25.16|25.34| 25.2|2650.7
2014-04-21 | AAPL| 2014-04-21T15:44:07.134000 |25.19|25.15|25.17|25.15|2122.1

/ add a "bucket" grouping using xbar
/ bucket xbar time = takes [time column], groups by [bucket ARG]
/ [bucket ARG] = timespan datatype
/ timespan format = 12:00:00.000000000
```

[func 9.5] Opening price same as prev close price [med]

```q
/ create dailystats 4
/ which is the same as dailystats3
/ since you've grouped values by [buckets]
/ the [open price] "should" = [close price] of prev bucket for same symbol
/ but what if there's no prev close (ie, the FIRST bucket)

/ hence, we want to update OPEN PRICE = to PREV CLOSE (for each bucket)

dailystats4: { [startdate; enddate; symbols; bucket]
		update open:open^prev close
		by sym
		from dailystats3[startdate; enddate; symbols; bucket] }



/ update the open column from prev function
/ embedded function - creating new function from old function
/ need to include arguments from old function 
/ ^ replaces nulls on right with atom on left
/ so replaces the [OPEN] value with [PREV CLOSE] value
```

[func 9.6] Calculating TWAP [hard]

```q
/ create function that calculates the VWAP and TWAP per day per symbol
/ for a supplied list of dates and symbols

/ While VWAP = volume weighted by size = size wavg price
/ TWAP = weighted by [length of time] that exists as last price
/ so TWAP = time wavg price
/ need to get [time diff] between ticks and multiply by price

twapandvwap1: { [startdate; enddate; symbols]
		select vwap: size wavg price, 
		twap: (next deltas time) wavg price
		by date, sym
		from trades
		where date within (startdate; enddate),
		sym in symbols }

twapandvwap1[2014.04.20;2014.04.21;`AAPL]

date       | sym  | vwap  | twap
----------------------------------
2014-04-21 | AAPL | 25.28 | 25.25

/ deltas time = tells us diff btwn consecutive times
/ need to use "next" to move it along
/ at each point, its the diff btwn [current value] and [next]
/ [next deltas time] = the entire time 
```

[func 9.7] Calculating max disparity btwn VWAP and TWAP [hard]

```q
/ create function twapandvwap2
/ which calculates the max disparity per date using fby

twapandvwap1: { [startdate; enddate; symbols]
		select from
		  (update diff:100*abs 1-twap%vwap
		  from twapandvwap1[startdate;enddate;symbols] )
		where diff=(max;diff) fby sym}

/ you want to figure out where the largest disparity
/ between vwap and twap are
/ so essentially you're taking vwap/twap -1 *100
/ order of operations right to left
/ this is the [DIFF]
/ then you filter by sym for the [max diff]
```

[func 9.8] Calculating standard deviations [hard]

```q
/ create function called bigdays
/ which returns across [one month window]
/ any days where the [vol of shares traded] was greater
/ than [n stddevs] from the avg for that month
/ so your args = n month, n stddev

/ need to select [total quantity traded] each day
/ then calc the [avg] and [dev]
/ and find any outliers
/ pass a [month] as the parameter

bigdays: { [mnth;stddevs]
	   select from
	     (select tradecount:sum `long$size by date
	     from trades
	     where date.month = mnth)
	   where (abs tradecount-avg tradecount) > stddevs*dev tradecount}

/ tradecount = total trades per day
/ cast size to long (so no decimals)
/ then sum them all up

/ take [date column] from table = 2014.04.21d
/ and cast as a [month] = 2014.04m
/ this will match your arg input of [mnth]

/ standard deviation = measures dispersion of dataset relative to its mean
/ calcuated as square root of its valence
/ dev = kdb function to calc standard deviation

/ filter where trades per day - avg trades per day
/ is greater than x standard deviations from trades per day
```

[func 9.9] Forcing xbar bucket to start at specific time

```q
/ create function called bucket
/ arguments = startdate, enddate, starttime, endtime, bucket, symbols
/ want to xbar 25 min buckets
/ trading day starts at 9:00
/ but i want first bucket to be 9:25
/ bucket value should be int or long (instead of timespan)
/ have to move [start time] of bucket by [subtracting] start time
/ then [adding it back] on

select from trades

date       | sym  | time	               | src | price | size
--------------------------------------------------------------------
2014-04-21 | AAPL | 2014-04-21T08:00:44.437000 |  O  | 25.34 | 1785
2014-04-21 | AAPL | 2014-04-21T08:04:41.246000 |  L  | 25.34 |  427
2014-04-21 | AAPL | 2014-04-21T08:04:47.586000 |  L  | 25.34 | 1528
2014-04-21 | AAPL | 2014-04-21T08:08:09.192000 |  L  | 25.35 | 8136
2014-04-21 | AAPL | 2014-04-21T08:11:23.934000 |  L  | 25.35 | 8945

bucket: { [startdate; enddate; starttime; endtime; bucket; symbols]
	  select sum size by date, sym,
	  starttime + bucket xbar time.minute - starttime
	  from trades
	  where date within (startdate;enddate),
	  sym in symbols,
	  time.time within (starttime;endtime) }

bucket[2014.04.20; 2014.04.21;09:25; 15:00; 25; `AAPL]

date       | sym  | starttime | size
-------------------------------------
2014-04-21 | AAPL |   09:25   |	13918
2014-04-21 | AAPL |   09:50   |	14205
2014-04-21 | AAPL |   10:15   |	9036
2014-04-21 | AAPL |   10:40   |	14062
2014-04-21 | AAPL |   11:05   |	14000
2014-04-21 | AAPL |   11:30   |	3361

/ starttime = 9:25
/ bucket = 25 mins
/ grouping by date, sym, xbar bucket of 25 mins

/ the [TIME column] is the main problem, as it is [timespan type]
/ need to CAST [time column] to minutes = time.minute
/ since your xbar bucket = 25 mins

/ since your (starttime;endtime) args = [time] datatype = 09:25
/ need to cast [time column] to from [timespan] to [time] datatype
/ during the where filter
```
[func 9.10] bucketing values in variable widths (using BIN instead of XBAR)

```q
/ want buckets to start at:
/ 08:00 08:15 08:32 08:50 09:27 12:00

/ use [BIN] to group [instead of xbar]

/ index [time column] into list of bucket times using BIN
/ then use index to pull out the appropriate bucket and group on that
/ buckets arg = list of your defined start times

/ b bin time.minute = returns an index into bucket list
/ b b bin time.minute = maps the index back to the bucket value

variablebucket: { [startdate; enddate; symbols; buckets]
		  select sum size by date, sym,
		  buckets buckets bin time.minute
		  from trades
		  where date within (startdate;enddate),
		  sym in symbols,
		  time.time >= first buckets}

variablebucket[2014.04.20; 2014.04.21;`AAPL;08:00 08:15 08:32 08:50 09:27 12:00]

date       | sym  | minute | size
-----------------------------------
2014-04-21 | AAPL |  08:00 | 27398
2014-04-21 | AAPL |  08:15 | 11727
2014-04-21 | AAPL |  08:32 | 8385
2014-04-21 | AAPL |  08:50 | 18982
2014-04-21 | AAPL |  09:27 | 73375
2014-04-21 | AAPL |  12:00 | 148039

/ for arg [buckets], you are passing in a LIST of times
/ first cast [time column] from table from [timespan] to [minutes]
/ aka time.minute

/ then you "bin" those [list of minutes] from table
/ into your [defined buckets] of start times
/ this returns the index position
/ then you map it BACK into the [bucket value]

/ b bin time.minute = returns an index into bucket list
/ b b bin time.minute = maps the index back to the bucket value

/ BIN reminder
/ BIN takes [LHS defined buckets], and returns [index position] of [RHS list]

100 300 500 bin 100 200 300 400 500 600
/ 0 0 1 1 2 2

/ can map index positions into buckets

`one`two`three 100 300 500 bin 100 200 300 400 500 600
`one`one`two`two`three`three
```

[func 9.11] Creating buckets of evenly cumulative traded volume

```q
/ create function called volumebuckets1
/ to split the trading day into [even volume buckets]
/ for ex, if arg numbuckets = 5,
/ how much volume would be traded in each bucket?
/ and what would the start and end times of the bucket be?

/ use [xrank] to group buckets [instead of xbar]

/ HINT - use xrank on the cumulative size value
/ output = date, num, startime, endtime, total vol

volumebuckets1:{ [startdate; enddate; symbol; numbuckets]
		  select starttime:first time, endtime: last time,
		  totalvol:sum size 
		  by date,
		  num:numbuckets xrank sums size
		  from trades
		  where date within (startdate;enddate), 
		  sym = symbol }
		  
volumebuckets1[2014.04.20; 2014.04.21; `AAPL; 5]

date       | num | starttime  	              | endtime                    | totalvol
--------------------------------------------------------------------------------------
2014-04-21 |  0  | 2014-04-21T08:00:44.437000 | 2014-04-21T09:24:13.929000 | 66492
2014-04-21 |  1  | 2014-04-21T09:43:05.829000 | 2014-04-21T11:15:35.791000 | 60324
2014-04-21 |  2  | 2014-04-21T11:16:51.859000 | 2014-04-21T13:11:40.724000 | 45872
2014-04-21 |  3  | 2014-04-21T13:15:06.432000 | 2014-04-21T15:28:43.900000 | 70350
2014-04-21 |  4  | 2014-04-21T15:29:52.766000 | 2014-04-21T16:26:29.954000 | 44868

/ numbuckets = how many "buckets" to split day into = 5
/ num = taking total size grouped into 5 buckets
/ aka num = 5 xrank sum size

/ xrank reminder:
/ xrank partitions list into [index position] buckets

2 xrank 1 2 3 4 5 6
0 0 0 1 1 1
```

[func 9.12] Calc avg start and end time for each bucket

```q
/ create volumebuckets2
/ which calcs the avg start and end time
/ for each vol bucket across a set of dates
/ this will give the average volume profile
/ should invoke volumebuckets1

volumebuckets2:{ [startdate;enddate;symbol;numbuckets]
		 select starttime:`time$avg starttime.time,
		 endtime:`time$avg endtime.time
		 by volbucket
		 from volumebuckets1[startdate;enddate;symbol;numbuckets] }

volbucket | starttime    | endtime
---------------------------------------
    0     | 08:00:44.437 | 09:24:13.929
    1     | 09:43:05.829 | 11:15:35.791
    2     | 11:16:51.859 | 13:11:40.724
    3     | 13:15:06.432 | 15:28:43.900
    4     | 15:29:52.766 | 16:26:29.954

/ piggy backing off the volumebuckets1 function (embedded func)
/ youre just amending the [starttime] + [endtime outputs]

/ you can use the [avg function] on time
/ since [all temporal datatypes] are integral counts (from 2000 midnight)
/ however, AFTER using [average] on [time]
/ must cast it BACK into [time datatype]

/ [startime + endtime] from prev equation are [timespan datatype]
/ first cast these to [time datatype]
/ then [calc average]
/ then cast back into [time datatype]
/ output = AVG TIME per volume bucket
/ retrieving FROM another function, so need to include [all arguments]
```

### 🔵 [func 10.0] Functions Problem Set 4 - AQ
<a name="func_set4AQ"></a>
[Top](#top)

```q
/ load fakedb.q

\l hdb

\a
`depth`quotes`trades
```

```q
select from trades

date       | sym  | time	               | src | price | size
--------------------------------------------------------------------
2014-04-21 | AAPL | 2014-04-21T08:00:44.437000 |  O  | 25.34 | 1785
2014-04-21 | AAPL | 2014-04-21T08:04:41.246000 |  L  | 25.34 |  427
2014-04-21 | AAPL | 2014-04-21T08:04:47.586000 |  L  | 25.34 | 1528
2014-04-21 | AAPL | 2014-04-21T08:08:09.192000 |  L  | 25.35 | 8136
2014-04-21 | AAPL | 2014-04-21T08:11:23.934000 |  L  | 25.35 | 8945
```

[func 10.0] tradeticks function

```q
/ name this func tradeticks1
/ queries a date range and sym filter
/ taking in 3 arguments (startdate, enddate, symbols)

tradeticks1:{ [startdate;enddate;symbols] 
            select date, sym, time, size, price 
            from trades
            where date within (startdate;enddate), sym in symbols}
            
tradeticks1[2014.04.20; 2014.04.21;`AAPL]

date       | sym  | time         | size  | price
------------------------------------------------
2014-04-21 | AAPL | 09:30:01.423 | 63000 | 58.46
2014-04-21 | AAPL | 09:30:01.768 | 95500 | 81.06
2014-04-21 | AAPL | 09:30:01.928 | 13400 | 82.90

/ date (from trades) within (startdate;enddate) from ARG
/ COL WITHIN ARG

/ sym (from trades) in symbols (from arg)
/ COL in ARG
```

[func 10.1] Using a projected function to retrieve from another function

```q
/ create function called calcreturns
/ using tradeticks1, add in column
/ which calc return of price vs the nth previous price
/ using xprev

/ tradeticks = given a range of dates + syms,
/ retrieve all the prices and sizes
/ now want to add on [return] column
/ which compares the nth prev price
/ need all tradeticks args + new arg n

return:{ [n;x] 100 * x % n xprev x}

calcreturns: { [startdate; enddate; symbols; n]
	       update ret:return[n;price]
	       by sym
	       from tradeticks1[startdate; enddate; symbols] }

/ return [n;x]
/ n = nth prev price
/ x = list of prices

/ return of something = (new-old)/old
/ if you want to check price vs PREV price
/ [1 xprev x] % x = (new - old) / old

/ this uses a [projected function] of [return]
/ n = nth prev price
/ x = list of prices

/ but also retrieves FROM another function [tradeticks1]
```

[func 10.2] Using a projected function to retrieve from another function (hard)

```q
/ (i dont really get this)

/ using tradeticks1 function,
/ create func to extract data and add in 
/ [running vwap] and [running twap] columns
/ [running vwap] = running sum of price*size / running sum of size
/ [running twap] = running sum of price*active time / running sum of time

/ use update to add in running columns
/ better to calc [activetime] once and use it twice

runningvwapandtwap:{ [startdate; enddate; symbols]
		     update rvwap:(sums size*price) % sums size,
		        rtwap:(sums activetime*price) % sums activetime
		     by date, sym
		     from 
		     	update activetime: next deltas time
		     by date, sym
		     	from tradeticks1[startdate; enddate; symbols] }

runningvwapandtwap[2014.04.20; 2014.04.21;`AAPL]

date      |sym |time                 |price|size|activetime   |rvwap|rtwap
---------------------------------------------------------------------------
2014-04-21|AAPL|2014-04-21T08:00:44.4| 5.34|1785|00:03:56.8090|25.34|25.34
2014-04-21|AAPL|2014-04-21T08:04:41.2|25.34| 427|00:00:06.3400|25.34|25.34
2014-04-21|AAPL|2014-04-21T08:04:47.5|25.34|1528|00:03:21.6060|25.34|25.34
2014-04-21|AAPL|2014-04-21T08:08:09.1|25.35|8136|00:03:14.7420|25.34|25.34
2014-04-21|AAPL|2014-04-21T08:11:23.9|25.35|8945|00:01:34.9280|25.34|25.34
2014-04-21|AAPL|2014-04-21T08:12:58.8|25.35|6577|00:03:55.4270|25.34|25.34

/ TWAP = price divided by [active time]
/ running TWAP = (sums active time * price) / (sums active time)
/ active time = next deltas time

/ want to group by date and sym
/ FROM this activetime calculation
```

[func 10.3] running sums by price group

```q
/ (i dont get this)

/ calc [running sum of vol] traded in each "price group"
/ use tradeticks1 to extract data from trade table
/ [price group] = series of [trades] all executed at [same price]

/ trick here is in the grouping
/ [differ price] = returns 1 when price changes
/ and 0 when no change
/ [sums differ price] = calcs the running sum of the changes
/ so those where no change will end up in same group

pricegroups: { [startdate; enddate; symbols]
		update pricegroupsize:sums size
		by sums differ price
		from tradeticks1[startdate;enddate;symbols]}

date	  |sym | time               	   | price| size | pricegroupsize
-------------------------------------------------------------------------
2014-04-21|AAPL| 2014-04-21T08:00:44.437000| 25.34| 1785 |	1785
2014-04-21|AAPL| 2014-04-21T08:04:41.246000| 25.34|  427 |	2212
2014-04-21|AAPL| 2014-04-21T08:04:47.586000| 25.34| 1528 |	3740
2014-04-21|AAPL| 2014-04-21T08:08:09.192000| 25.35| 8136 |	8136

/ i dont understand [sums differ price]
/ differ price = returns 1 or 0?
/ so sums would just add up 1s?
/ if grouping by sums differ price, shouldn't price = unique?
```

[func 10.4] VWAP if all bids or asks taken out

```q
/ extract from depth table
/ add column [BIDVWAP], which displays all the levels on the bid
/ ie, the VWAP you would get if you were to clear the depth
/ and do the same for [ASKVWAP]

/ so depth table has 3 bids, 3 bid sizes, 3 ask, and 3 ask sizes
/ VWAP = price weighted by volume
/ so take [all the bids] [wavg] by [all the bid sizes]
/ and [all the asks] [wavg] by [all the ask sizes]
/ wavg will vectorize across the columns

sidevwaps: { [startdate;enddate;symbols]
	     update bidvwap: (bsize1;bsize2;bsize3) wavg (bid1;bid2;bid3),
	            askvwap: (asize1;asize2;asize3) wavg (ask1;ask2;ask3)
	     from
	     	select date,time,sym,bid1,bid2,bid3,bsize1,bsize2,bsize3,
		 ask1,ask2,ask3,asize1,asize2,asize3
	       from depth
	       where date in (startdate;enddate),
	       sym in symbols}
	       
sidevwaps[2014.04.20;2014.04.21;`AAPL]

/ table returned shows all the bids (bid1, bid2, bid3)
/ all the bid sizes (bsize1, bsize2, bsize3)
/ as well as the asks
/ and lastly, the bidvwap and ask vwap

/ don't understand why need from all those col names
/ why can't just from quote?
```

[func 10.5] 

```q
/ (i dont get this)

/ extract 30 mins worth of depth ticks
/ for any date and sym
/ assume i sell 1,000 shares
/ calc for each tick how many levels down the book
/ i will have to go to fill my order

/ use bin
1.2 3.4 6.9 11.2 bin 3.7 12.0
1 3

/ accumulate up depth sizes, find how far down the book 
/ we have to go

/ use sums to accumulate all the columns together
/ then flip to transpose the bid size columns
/ into a list of lists

/ args: d = date
/ s = sym
/ st = start time
/ et = end time
/ 0 = ? (order book?)

findfilllevel: { [d;s;st;et;o]
 t: select date, time sym, 
 	bsizes:flip sums(bsize1;bsize2;bsize3;bsize4;bsize5)
  from depth
  where date in d, sym in s, time within (st;et);
  
 / use [bin] operator and [\: adverb] to apply each element
 / of the bsizes column in turn
 / need to add 2 as bin starts counting from -1
 / (if order fills at the very start)
 
 update filllevel:2 + bsizes bin \:o from t}
 
 ```

### [func 11.0] Int Problem Set 1 - GS
<a name="func_int1"></a>
[Top](#top)


```q
/ Create a function that will return latest prices (with max timestamp within the date) for the date.
/ If there is not any price for that particular date, return the latest previous price
/ There is no predefined ordering of the source table.
/ Try to preserve the column order.
```
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
/ set date, sym as keys (allows date + sym to be first 2 columns)
/ the 3 WHERE clauses are most important!
/ date <=d means look for previous day if current date doesnt satisfy query conditions
/ you want to filter the LAST PRICE by sym, then
/ you want to filter the MAX TIMESTAMP by the date
/ the ORDER of the fby also matters a lot. 
```

### [func 12.0] Int Problem Set 2 - GS
<a name="func_int2"></a>
[Top](#top)


[func 12.1] create table called price

```q
/ with columns date, ticker, ex, and price

price: ([] date: 2021.01.21 2021.03.21 2021.09.21; ticker:`AAPL`AAPL`MSFT; ex: `US`UW`US; price: 10 20 30)

price:
date       | ticker | ex | price
--------------------------------
2021-01-21 |  AAPL  | US | 10
2021-03-21 |  AAPL  | UW | 20
2021-09-21 |  MSFT  | US | 30
```

[func 12.2] create function called f

```q
/ takes in 3 args: [sym, startdate, enddate]
/ queries the price table 
/ and returns the syms that falls within the [startdate] and [enddate]

f:{ [sym;start;end] select from price where date within (start;end), ticker in sym}
f[`AAPL;2021.01.21; 2021.12.21]

date       | ticker | ex | price
---------------------------------
2021-01-21 | AAPL   | US | 10
2021-03-21 | AAPL   | UW | 20

/ syntax is where COL_NAME (date) within (arg2;arg3)
/ COL_NAME (ticker) in (arg1)
```

[func 12.3] create 2nd table called input

```q
/ with 3 columns: ticker, start date, end date

input: ([] ticker: `AAPL`AAPL`MSFT; start: 2021.01.01 2021.03.01 2021.06.01; end: 2021.03.01 2021.06.30 2021.08.01)

ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01
```

[func 12.4] from input table, query the price table

```q
/ from the [input table], retrieve the [syms] from original [price table]
/ that match the [start] and [end dates] from [input]

/ thought process:

/ check if [ticker] from [price] = [ticker] from [input],
/ WHERE [date] from [price] falls within [start/end] from [input]
/ you need to query ENTIRE row from input table [sym + start + end]
/ then iterate through EACH row

/ so you can either run this query 3x, or you can iterate through each row using EACH
/ since you have 3 arguments (sym, start, end) from the original function
/ you can query these args as a LIST of values corresponding from [input table]
```

```q
/ Method 1:

/ since each row in table = dictionary
/ you can first retrieve a list of values from each column
/ for ex, ticker values would be `AAPL`AAPL`MSFT
/ then INPUT these [list of values] for each argument
/ then use EACH to iterate the function through each row

input table
ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01

input`ticker
`AAPL`AAPL`MSFT

input`start
(2021-01-01d; 2021-03-01d; 2021-06-01d)

input`end
(2021-03-01d; 2021-06-30d; 2021-08-01d)

/ using same function as earlier:

f:{ [sym;start;end] select from price where date within (start;end), ticker in sym}
raze f'[input`ticker;input`start;input`end]

ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30

/ original function doesnt change
/ orig func = from price table, retrieve syms where date within (start;end) 
/ your inputs = [LIST OF VALUES] from EACH column from input table
/ f' = run the function through EACH row (doesnt work if you do f each)
/ the output is a list of 3 tables, so to collapse 1 layer, use RAZE
/ raze = (,/)
```

[func 12.5] Method 2

```q
/ Method 2: Alternative Syntax

/ instead of querying original function
/ with lists of values by column as the 3 arguments
/ you can re-write the function
/ and use x to query the corresponding columns in the input table
/ iterating through each row using EACH

price:
date       | ticker | ex | price
--------------------------------
2021-01-21 |  AAPL  | US | 10
2021-03-21 |  AAPL  | UW | 20
2021-09-21 |  MSFT  | US | 30

input:
ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01

f1:{select from price where date within x`start`end, ticker in x`ticker}
raze f1 each input

/ so you create function f1, which takes implicit argument x
/ as the [input table]
/ from [price table], find where [date from price] is within [start, end from x]
/ and where [ticker from price] is = [ticker in x]

/ if you think about it, its the same syntax as table_name`col_name
/ only x is now the table name

/ to iterate through [EACH ROW] of [input table], you have use [EACH]
/ you return a list of tables, so need RAZE to level it 
```

[func 12.6] Method 3

```q
/ 2. create new function querying the [input table]
/ and use [sym] and [date] from [price table] as arguments

price:
date       | ticker | ex | price
--------------------------------
2021-01-21 |  AAPL  | US | 10
2021-03-21 |  AAPL  | UW | 20
2021-09-21 |  MSFT  | US | 30

input:
ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01

f2:{ [sym;date] select from input where date within (start;end), sym in ticker}

/ you can query one by one (each row)

f2 [`AAPL;2021.01.21]

ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01

f2[`MSFT;2021.09.21]

ticker |   start    |    end
--------------------------------
/ null since no match

/ but its probably more efficient to use adverb EACH
/ and query through entire table 

/ retrieve list of VALUES per COLUMN

price`ticker
`AAPL`AAPL`MSFT

/ values for column [ticker] from [price table]

price`date
(2021-01-21d; 2021-03-21d; 2021-09-21d)

/ values for column [date] from [price table]

raze f2'[price`ticker; price`date]

ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30

/ you are calling function with a LIST of 3 values
/ so you get a LIST of 3 tables
/ must use raze to flatten 1 level
/ also must use ' = each to iterate through each row
```

<a name="qsql"></a>
### 🔴 9. qSQL
[Top](#top)

### 🔵 [QSQL 1.0] QSQL Problem Set 1 - TS
<a name="sql_1"></a>

```q
/ load the trades.q script

\l trades.q
\a
`quote`stock`trade
```

[QSQL 1.1] select first price, first time by date for AAPL

```q
select first price, first time by date from trade where sym=`AAPL

`date`       | price| time
----------------------------------
`2021-05-29` | 78.6 | 09:30:03.025
`2021-05-30` | 60.8 | 09:30:02.686
`2021-05-31` | 55.1 | 09:30:18.274

/ by date = groups date as the key column
```

[QSQL 1.2] Find the total number of trades for RBS by date and time in hours

```q
/ hint - each row is 1 trade, so you want to count rows

select tot:count i by date,time.hh from trade where sym=`RBS

date       | hh | tot
-----------------------
2022-03-31 |  9 |  658
2022-03-31 | 10 | 1315
2022-03-31 | 11 | 1235
2022-03-31 | 12 | 1263
2022-03-31 | 13 | 1184

/ i is a virtual column that returns the number of rows (as column x)
/ cast [time] to [hours] using [time.hh]
```

[QSQL 1.3] Find all AAPL prices that are less than the avg price, grouped by date

```q
select by date from trade where sym = `AAPL, price < avg price

date	   | time         |  sym | price| size	| cond
-------------------------------------------------------
2022-03-31 | 17:29:58.907 | AAPL | 68.0 | 58000 | B
2022-04-01 | 17:29:57.090 | AAPL | 79.0 | 26200 | 
2022-04-02 | 17:29:56.273 | AAPL | 77.0 | 64400 | 
2022-04-03 | 17:29:54.142 | AAPL | 69.7 | 80800 | C
2022-04-04 | 17:29:58.262 | AAPL | 76.1 | 22500 | A
```

```q
/ alternative syntax:

select price by date from trade where sym=`AAPL, price < avg price

date        | price
--------------------------
`2021-05-29`| 100 99 22 33...
`2021-05-30`| 23 199 44 12...
```

[QSQL 1.4] Retrieve prices, keyed by TODAY, where AAPL's price is less than the avg price

```q
select price by date=.z.d from trade where sym=`AAPL, price < avg price

d   | price
--------------
`0` | 23 52 63...
`1` | 23 66 12...

/ grouped by today; 0 = false, 1 = true
```

[QSQL 1.5] Retrieve price divide by max price, keyed by today, for AAPL where the price is less than the avg price

```q
select {x % max x} price by date = .z.d from trade where sym=`AAPL, price < avg price

d    | price
-------------------
`0b` | 0.98 0.7 0.8
`1b` | 0.12 0.43 0.32
```

[QSQL 1.6] Retrieve all data for AAPL and RBS

```q
/ to query multiple syms, use [in]

select from trade where sym in `AAPL`RBS

date      | time         | sym |price   |size   | cond
------------------------------------------------------
2021-05-30| 09:30:02.743 | RBS | 97.113	| 80700 | C
2021-05-30| 09:30:03.025 | AAPL| 78.66  | 19000	| A

/ in function checks if every LHS argument occurs anywhere in RHS argument (AAPL or RBS)
/ a faster way of checking "or" arguments
```

[QSQL 1.7] Retrieve trades for RBS where price is between 95 and 100

```q
/ to query within a range, use [within]

select from trade where sym=`RBS, price within 95 100

date      |time          |sym   |price  | size | cond
------------------------------------------------------
2021-05-30| 09:30:02.743 | RBS  | 97.113| 80700 | C
2021-05-30| 09:30:03.025 | AAPL | 98.66 | 19000	| A

/ checks if LHS argument is within the range on RHS argument
/ has to have lower + upper bind
```

[QSQL 1.8] Retrieve trades for RBS within 95 and 100 and between 11:30 - 12:00

```q
select from trade where sym=`RBS, price within 95 100, time within 11:30 12:00

date      | time          |sym   | price  | size | cond
-------------------------------------------------------
2021-05-30| 11:40:02.743 | RBS   | 97.113 | 80700 | C
2021-05-30| 11:44:03.025 | AAPL  | 98.66  | 19000 | A
```

### 🔵 [QSQL 2.0] Problem Set 2 - TS
<a name="sql_2"></a>
[Top](#top)

```q
\l trades.q
```

[QSQL 2.1] Delete the entire cond column from trade

```q
delete cond from trade

date       time         sym  price    size 
-------------------------------------------
2021.11.18 09:30:02.553 C    107.2018 63500
2021.11.18 09:30:02.701 MSFT 96.87488 1700 
2021.11.18 09:30:02.743 RBS  97.11338 80700

/ cond columns is removed
/ cannot have by or where clause
```

[QSQL 2.2] Delete the entire row that has A for cond

```q
delete from trade where cond="A"

date       |  time   | sym |price|size| cond| maxprice
------------------------------------------------------
2021.03.01 | 15:09:01| JPM |  74 |41.2|  B  | 102
2021.03.01 | 15:09:01| UBS |  41 |31.2|  C  | 91

/ DELETE without WHERE clause = deletes entire column
/ DELETE with WHERE clause = deletes rows where conditions met
```

[QSQL 2.3] update all prices to 10 in trade table

```q
update price: 10.0 from trade

date       time         sym  price size  cond
---------------------------------------------
2021.11.18 09:30:02.553 C    10    63500 B   
2021.11.18 09:30:02.701 MSFT 10    1700  B   
2021.11.18 09:30:02.743 RBS  10    80700 C   
2021.11.18 09:30:02.758 A    10    50300 B  

/ notice no semi-colon after update
/ need 10.0 float datatype (since price = float)
```

[QSQL 2.4] update all prices of sym C to 10.0

```q
update price:10.0 from trade where sym=`C

date       | time         | sym | price| size  | cond
-----------------------------------------------------
2021.10.30 | 09:30:02.553 | C   | 10   | 63500 | B   

/ note the price has to be a float, otherwise query won't work
/ when in doubt, use META to check the datatypes
```

[QSQL 2.5] update the price to 10.0 for AAPL and GOOG

```q
update price:10.0 from trade where sym in `AAPL`GOOG

date       | time         | sym  | price| size  | cond
-----------------------------------------------------
2021.10.30 | 09:30:02.553 | AAPL | 10   | 63500 | B   
2021.10.30 | 09:30:02.701 | AAPL | 10   | 1700  | B   
2021.10.30 | 09:30:02.743 | GOOG | 10   | 80700 | C  

/ for multi where condition use "in" 
/ the where clause updates only the filtered records
```

[QSQL 2.6] add new column vol, which is price x size for AAPL and GOOG

```q
update vol:price*size from trade where sym in `AAPL`GOOG

date       | time         | sym  | price| size  | cond | vol
---------------------------------------------------------------
2021.10.30 | 09:30:02.553 | AAPL | 10   | 63500 | B    | 635000
2021.10.30 | 09:30:02.701 | AAPL | 10   | 1700  | B    |  17000
2021.10.30 | 09:30:02.743 | GOOG | 10   | 80700 | C    | 807000 
2021.11.18 | 09:30:02.743 | RBS  | 10   | 80700 | C    | 
2021.11.18 | 09:30:02.758 | A    | 10   | 50300 | B    |

/ update new column = adds new column to end
/ only populates values for AAPL and GOOG
```

[QSQL 2.7] update the prices of AAPL and GOOG to average price, grouped by sym 

```q
update price:avg price by sym from trade where sym in `AAPL`GOOG

date       | time         | sym  | price| size  | cond 
-------------------------------------------------------
2021.10.30 | 09:30:02.553 | AAPL | 79.98| 63500 | B    
2021.10.30 | 09:30:02.701 | AAPL | 79.98| 1700  | B    
2021.10.30 | 09:30:02.743 | GOOG | 34.32| 80700 | C 
```

[QSQL 2.8] randomly select 100 rows from trade, name this table tt

```q
tt:100?trade

date       |  time   | sym |price|size| cond
---------------------------------------------
2021.01.01 | 15:10:01| BAC | 70  |422| B
2021.03.01 | 15:09:01| JPM | 74  |412| C
```

[QSQL 2.9] update all cond to "D"

```q
update cond: "D" from trade

date       |  time   | sym |price|size| cond
---------------------------------------------
2021.01.01 | 15:10:01| BAC | 70  |422 | D
2021.03.01 | 15:09:01| JPM | 74  |412 | D
```

[QSQL 2.10] divide all size values by 100

```q
update size % 100 from trade

date       |  time   | sym |price|size| cond
---------------------------------------------
2021.01.01 | 15:10:01| BAC | 70  |42.2| D
2021.03.01 | 15:09:01| JPM | 74  |41.2| D
2021.03.01 | 15:09:01| UBS | 41  |31.2| D

/ can perform function on entire column. size divided by 100
```

[QSQL 2.11] add a new column called advice and populate with sell

```q
update advice:`sell from trade

date       |  time   | sym |price|size|cond|advice
---------------------------------------------------
2021.01.01 | 15:10:01| BAC |  70 |42.2|D   | sell
2021.03.01 | 15:09:01| JPM |  74 |41.2|D   | sell
2021.03.01 | 15:09:01| UBS |  41 |31.2|D   | sell

/ if you update a column that doesnt exist, it will add the column
/ new column added called advice and populates with sell
/ notice it has to be backtick sell
```

[QSQL 2.12] update advice to buy if price less than 70

```q
update advice: `buy from trade where price < 70

date       |  time   | sym |price|size|cond|advice
---------------------------------------------------
2021.01.01 | 15:10:01| BAC |  70 |42.2|  D | 
2021.03.01 | 15:09:01| JPM |  74 |41.2|  D | 
2021.03.01 | 15:09:01| UBS |  41 |31.2|  D | buy

/ if price less than 70, advice becomes buy
/ if not, then null value returned
```

[QSQL 2.13] add new column maxprice populated with max prices by sym

```q
update maxprice: max price by sym from trade

date       |   time  | sym |price|size|cond|maxprice
----------------------------------------------------
2021.01.01 | 15:10:01| BAC |  70 |42.2|  D | 104
2021.03.01 | 15:09:01| JPM |  74 |41.2|  D | 102
2021.03.01 | 15:09:01| UBS |  41 |31.2|  D | 91

/ since maxprice doesnt exist, adds new column to end
```

### 🔵 [QSQL 3.0] xbar Problem Set - TS
<a name="sql_3"></a>
[Top](#top)

```q
\l trades.q

```

[QSQL 3.1] Calculate the number and total size traded by sym for each $1 price 

```q
select num: count i, totalsize: sum size sym, 1 xbar price from trade

sym | price | num | totalsize
-----------------------------
A   |  50.0 | 810 | 40531900
A   |  51.0 | 821 | 42688700
A   |  52.0 | 787 | 38549900
A   |  53.0 | 834 | 41615700

/ groups the data by sym and 1 dollar price buckets
/ count i = tallies virtual column i
/ aka how many trades were executed by sym for that price bucket
```

[QSQL 3.2] Find the max price and total size of trades by ticker during 5 min buckets

```q
select max price, sum size by sym, 5 xbar time.minute from trades

sym  |minute | price|size
-------------------------
AAPL | 08:00 | 27.4 | 100
AAPL | 08:05 | 27.9 | 200
AAPL | 08:10 | 28.2 | 300

/ set xbar as 5 minute time buckets
/ grouped sym, then 5 min time buckets
/ sym + minute are keyed (since by)
```

[QSQL 3.3] Find the max price by sym in 45 min time buckets, specifically including 9:30 time bucket

```q
/ original query (incorrect as it doesn't include 9:30)

select max price by sym, 45 xbar time.minute from trade

sym |minute | price
----------------------
 A  |09:00  | 109.94
 A  |09:45  | 109.99
 A  |10:30  | 109.96

/ correct query

select max price by sym, 09:30 + 45 xbar time.minute - 09:30 from trade

sym|minute |price
------------------
 A | 09:30 |109.94
 A | 10:15 |109.99
 A | 10:45 |109.96

/ note! time format has to be 09:30 (not 9:30)
/ by adding 09:30 and subtracting 09:30 from xbar
/ you shift the time bucket
/ to include your desired time

/ logic here:
/ the 45 xbar time.minute = groups into 45 min buckets
/ subtracting your time 9:30 = you shift the list to include your desired time
/ adding 9:30 = reset to center around your desired time
```

### 🔵 [QSQL 4.0] fby Problem Set
<a name="sql_4"></a>
[Top](#top)


[QSQL 4.1] Calc the min temp by city (fby on 2 lists)

```q
city:`NY`NY`LA`SF`LA`SF`NY
temp:32 31 75 69 70 68 12

(min;temp) fby city
12 12 70 68 12

/ this performs an fby on 2 lists
/ calculates the min temp for every city (12 for NYC)
```

[QSQL 4.2a] find the max price per symbol

```q
\l trades.q
```

```q
/ this is the solution i used, but doesnt involve fby

select max price by sym from trade

sym | price
-------------
A   | 109.99
AA  | 109.99
AAPL| 109.99
B   | 109.99
BAC | 109.99
```

[QSQL 4.2b] find the max price per symbol (use fby)

```q
select from trade where price=(max;price) fby sym

time       |sym  |src| price | size
-----------------------------------
2019-03-11 |GOOG | L | 36.01 | 1427
2019-03-11 |GOOG | O | 36.01 | 708
2019-03-11 |MSFT | N | 35.5  | 7810
```

[QSQL 4.2c] find the max price and latest time per symbol (use fby)

```q
/ assume there are 2 syms with same max price 
/ you can add another fby filter for time

select from t where price=(max;price) fby sym, time=(max;time) fby sym

time      |sym  |src| price | size
-----------------------------------
2019-03-11|GOOG	| O | 36.01 | 708
2019-03-11|MSFT | N | 35.01 | 7810

/ in this case, you filtered max price by sym, and max time by sym
```

[QSQL 4.3] find the max price on today's date

```q
select from trade where date=2021.10.31, price=max price

date       | time         | sym | price | size | cond
------------------------------------------------------
2021-11-26 | 12:51:34.253 | F   | 109.9 | 58500|

/ filter by date, then the max price from this date
```

[QSQL 4.4] find max price by sym, today's date (use fby)

```q
select from trade where date=.z.d, price=(max;price) fby sym

date       | time         | sym | price | size | cond
------------------------------------------------------
2021-11-26 | 10:17:09.373 | A	| 109.9	| 94300| C
2021-11-26 | 10:25:22.268 | MSFT| 109.9	| 49100| C
2021-11-26 | 11:49:11.143 | D	| 109.9 |  5600| A

/ filter by date, then find max price by sym
/ groups the aggregation by sym
/ notice this returns the whole table (max price by sym)

/ if you did this instead:

select max price by sym from trade where date = 2021.11.26

sym  | price
-------------
A    | 109.9
AA   | 113.2
AAPL | 339.1

/ this will ONLY return the max price column
```

[QSQL 4.5] find max price using an [fby] for both [sym and cond] for today

```q
select from trade where date=.z.d, price=(max;price) fby ([] sym; cond)

date       | time         |sym | price | size  | cond
------------------------------------------------------
2022-04-05 | 09:30:31.122 | F  | 109.5 | 27300 | C
2022-04-05 | 09:30:49.628 | KX | 109.9 | 37300 | C
2022-04-05 | 09:35:00.553 | MS | 109.8 | 12700 | A
2022-04-05 | 09:36:37.757 | A  | 109.3 | 24000 | A

/ aggregate by more than one field using a table
/ filter by date, then max price by sym and cond
```

### 🔵 [QSQL 5.0] Problem Set 3 - TS
<a name="sql_5"></a>
[Top](#top)

```q
\l trades.q
```

[QSQL 5.1] Extract trades for MS greater than 1,000 in size

```q
select from trade where sym=`MS, size >1000

dt         |sym |price|size
----------------------------
2021.01.01 | MS | 225 | 200
2021.01.01 | MS | 234 | 400
```

[QSQL 5.2] Find the total size of all trades and the average price paid per sym

```q
select totalsize:sum size, avgprice:avg price by sym from trade

sym | totalsize   | avgprice
-----------------------------
A   | -1796963996 | 79.96
AA  | -1792025796 | 80.02
AAPL|  1789783596 | 79.98
B   | -1802424996 | 79.84
BAC | -1790778496 | 79.78
```

[QSQL 5.3] Find the trade that was largest size for each sym (use fby)

```q
select from trade where size=(max;size) fby sym

date       | time         | sym  | price | size  | cond
--------------------------------------------------------
2021-11-27 | 09:30:21.256 | B	 | 100.0 | 99900 |	 
2021-11-27 | 09:31:20.975 | AA	 | 67.3  | 99900 | C
2021-11-27 | 09:43:47.816 | GOOG | 72.4  | 99900 | A
2021-11-27 | 09:46:44.690 | F    | 73.2  | 99900 | B

/ alternatively, if you did this:

select max size by sym from trade

sym | size
-------------
A   | 99900
AA  | 99900
AAPL| 99900
B   | 99900
```

[QSQL 5.4a] Select the latest trade for each sym, and include all details (non-fby)

```q
select last date, last price, last time by sym from trade

sym | date       | price | time
----------------------------------------
A   | 2021-12-01 | 87.5  | 17:29:57.306
AA  | 2021-12-01 | 68.0	 | 17:29:58.789
AAPL| 2021-12-01 | 76.1	 | 17:29:58.262
B   | 2021-12-01 | 95.5	 | 17:29:56.912
```

[QSQL 5.4b] Select the latest trade for each sym, and include all details (fby)

```q
select from trade where time=(max;time) fby sym

date       | time         | sym  | price | size  | cond
-------------------------------------------------------
2022-04-01 | 17:29:58.861 |   AA |  60.0 | 20900 |  C
2022-04-01 | 17:29:58.878 | MSFT |  83.5 |  7700 |  B
2022-04-01 | 17:29:58.907 | AAPL |  68.0 | 58000 |  B
2022-04-01 | 17:29:58.968 |    D |  82.9 | 76800 |  A
```

[QSQL 5.5] Find all trades that have sym GOOG

```q
select from trade where sym=`GOOG

date       | time         | sym  | price | size  | cond
--------------------------------------------------------
2021-11-27 | 09:30:17.541 | GOOG | 86.1  | 83500 | C
2021-11-27 | 09:30:17.895 | GOOG | 80.5  | 91700 | B
2021-11-27 | 09:30:18.011 | GOOG | 81.0  | 49300 | B
```

[QSQL 5.6] Find all trades that have sym GOOG or RBS or A

```q
select from trade where sym in `GOOG`RBS`A

date       | time         | sym  | price | size  | cond
-------------------------------------------------------
2021-11-27 | 09:30:17.541 | GOOG | 86.1  | 83500 | C
2021-11-27 | 09:30:17.895 |  RBS | 80.5  | 91700 | B
2021-11-27 | 09:30:18.011 |    A | 81.0  | 49300 | B
```

[QSQL 5.7] Find all trades for google that had a price between 70 and 80

```q
select from trade where sym=`GOOG, price within 70 80

date       | time         | sym  | price | size  | cond
-------------------------------------------------------
2021-11-27 | 09:30:17.541 | GOOG | 73.1  | 83500 | C
2021-11-27 | 09:30:17.895 | GOOG | 75.5  | 91700 | B
2021-11-27 | 09:30:18.011 | GOOG | 77.0  | 49300 | B
```

[QSQL 5.8] Count the number of trades and total size of trades per hour for sym RBS

```q
select numtrades:count i, totalsize: sum size by time.hh from trade where sym=`RBS

hh | numtrades | totalsize
--------------------------
9  |	3186   | 159063500
10 |	6544   | 321195100
11 |	6280   | 315284200
12 |	6141   | 306898200
13 |	6086   | 305154900
```

[QSQL 5.9] Select the number of trades and total size of trades every 30 mins for sym RBS

```q
select numbertrades: count i, totalsize: sum size by 30 xbar time.minute from trade where sym=`RBS

minute|numbertrades|totalsize
-------------------------------
09:30 |    3186    | 159063500
10:00 |	   3271    |  62197000
10:30 |	   3273    | 158998100
```

[QSQL 5.10] Find all trades for A where the price was cheaper than the average for that day

```q
select from trade where sym=`A, price < avg price

date       | time         | sym | price | size  | cond
-------------------------------------------------------
2021-11-27 | 09:30:17.997 |  A	|  57.8 | 65600 | C
2021-11-27 | 09:30:23.144 |  A	|  54.5 | 31200	|
2021-11-27 | 09:30:23.570 |  A  |  60.8 | 8200	|
```

### 🔵 [QSQL 6.0] Table Query Problem Set 1
<a name="sql_6"></a>
[Top](#top)


[QSQL 6.1] retrieve values from t1 given date filter + column from t1 matches t2 

```q
/ date filter = 2021.10.21
/ column filter = match on columns sym and exch

t1: ([] date: 2021.10.21 2021.10.21 2021.10.21 2021.10.21; sym: `GOOG`MSFT`FB`AMZN; exch: `nyse`nyse`nasdaq`nasdaq)

t2: ([] sym: `GOOG`FB; exch: `nyse`nasdaq)

t1
date       | sym  | exch
----------------------------
2021-10-21 | GOOG | nyse
2021-10-21 | MSFT | nyse
2021-10-21 | FB	  | nasdaq
2021-10-21 | AMZN | nasdaq

t2
sym  | ex
------------
GOOG | nyse
FB   | nasdaq

select from t1 where date=2021.10.21,( [] sym; exch) in t2

date       | sym  | exch
----------------------------
2021-10-21 | GOOG | nyse
2021-10-21 | FB	  | nasdaq

/ use a table of syms + exch in t2 as a filter
/ this where filter will first filter by date in t1, then by the sym, exch found in t2
```

### 🔵 [QSQL 7.0] Table Query Problem Set 2
<a name="sql_7"></a>
[Top](#top)


[QSQL 7.1] Retrieve IBM from cond A, CSCO from cond A or B, and MSFT from cond C with date = today

```q
\l trades.q

```

```q
/ first, create table [toget], with all possible conditional outcomes

toget: ([] sym:`IBM`CSCO`CSCO`MSFT, cond:"AABC")

sym   cond
----------
IBM    A
CSCO   A
CSCO   B
MSFT   C
```

```q
select from trade where date = 2022.04.01, ( [] sym; cond) in toget

date       sym  price size cond
-------------------------------
2021-10-30 MSFT	60.66 48700 C
2021-10-30 IBM	59.00 28300 A
2021-10-30 MSFT	54.57 23700 C
2021-10-30 IBM	89.19 86600 A
2021-10-30 IBM	84.13 46600 A

/ create table of all possible outcomes
/ then filter using matching columns from original table
/ and your outcome table
```

### 🔵 [QSQL 8.0] Table Query Problem Set 3
<a name="sql_8"></a>
[Top](#top)

```q
/1 extract all the following results:

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
```

```q
/2 however, can use a TABLE SEARCH function

/ METHOD 1: 

select from results where ([]gender;grade) in ([] gender:"MFF";grade:"ABA")

name  |gender|grade
--------------------
John  |   M  | 	A
Rachel|   F  |	B
Jane  |   F  |	A

/ so the search table query takes in whatever parameters you are querying for
/ for example, you wanted filters on GENDER + GRADE
/ so the table search  = ([] gender;grade)
/ the last part is simply a table which contains the universe of the possible correct pairs
```

```q
/ METHOD 2:

/3 build table with target parameters

t2: ([] gender:"MFF"; grade: "ABA")

gender | grade
---------------
M      | A
F      | B
F      | A

/4 loop table back into original query

select from results where ([]gender;grade) in t2

name  |gender|grade
--------------------
John  |   M  | 	A
Rachel|   F  |	B
Jane  |   F  |	A
```

### 🔵 [QSQL 9.0] BIN Problem Set
<a name="sql_9"></a>
[Top](#top)


```q
\l trades.q
```
[QSQL 9.0] Group trades into small, medium, big buckets

```q
/ small = size < 999
/ medium = size 1000 - 8999
/ big = size > 8999

/ Solution 1: write it all out using multiple select queries

(select count i by sym, sizegroup:`small from trade where size within 0 999),
(select count i by sym, sizegroup:`medium from trade where size within 1000 8999),
(select count i by sym, sizegroup:`big from trade where size > 8999)

sym | sizegroup  | x
-------------------------
A   | large      | 45645
A   | med        | 4009
A   | small      | 480
AA  | large      | 45425

/ sizegroup = new col name, and you assign a sym (`small`med`large) based on a where filter for size
```

```q
/ Solution 2: Create a function that accepts list of sizes and sorts into BINS

tradesize:{`small`med`large 0 1000 9000 bin x}

/ function tradesize accepts x as a list of sizes
/ notice the bin ranges are pegged to the LOW end

select count i by sym, sizebucket:(tradesize;size) fby sym from trade

/ fby sytax = (agg;col_name)
/ func tradesize = aggregate function
/ size = col name from original trade table
```

### 🔵 [QSQL 10.0] Signum Deltas Problem Set
<a name="sql_10"></a>
[Top](#top)


```q
/ can make use of the deltas + signum function

/ deltas will calculate the change between subsequence elements
/ signum will tell you if the element is positive, negative, or 0

deltas 3 2 2 1 5
3 -1 0 -1 4

signum deltas prices
1 -1 0 -1 1
```

```q
/1 add in new col called direction which calcs the signum deltas of price

select from trade

sym | price | size  | cond
---------------------------
C   |  59   | 18400 | C 
F   |  104  | 62600 |    
IBM |  73   | 77500 | B 
A   |  63   | 73000 | B

update dir: signum deltas price from trade

sym | price | size  | cond | dir
--------------------------------
C   |  59   | 18400 | C    | 1  
F   |  104  | 62600 |      | 1  
IBM |  73   | 77500 | B    |-1 
A   |  63   | 73000 | B    |-1 

/ this will add a new column, dir, which will be +1, 0, or -1
```

```q
/2 you can also create a function for signum deltas

tickdir:{signum deltas [first x;x] }

/ x = argument for price
/ deltas [first x; x] = just means the difference between consecutive elements

update dir: tickdir price from trade

sym | price | size  | cond | dir
--------------------------------
C   |  59   | 18400 | C    | 1  
F   |  104  | 62600 |      | 1  
IBM |  73   | 77500 | B    |-1 
A   |  63   | 73000 | B    |-1 

/ tickdir takes price as its argument for x
```

```q
/3 Group this data by sym, and see total sie traded by direction (uptick, downtick, etc)

select sum size by sym, dir from update dir:tickdir price by sym from trade

sym  | dir | size
------------------------
A    |	-1 | 1250381100
A    | 	 0 | 8000
A    |	 1 | 1243181200
AAPL |	-1 | 1240192300
AAPL |	 0 | 58400
AAPL |	 1 | 1248680500

/ groups size by sym and dir (previously calculated signums)
/ TWO from statements as you are querying a table from which you previously created

/ you cannot simply do this:

select sum size by sym, dir:signum deltas price by sym from trades

/ error, as tickdir was calculated on entire price column as a whole
/ you cannot group by a column calculation on an entire column
/ have to use an fby instead

select sum size by sym, dir:(tickdir; price) fby sym from trades

sym|dir|size
-------------------
 A |-1 |1258345400
 A | 0 |7100
 A | 1 |1252317500
 
/ this will now work and returns same table as above
/ fby symtax = (Aggr;col_name) fby
/ aggr = tickdir as aggregator for signums from...
/ col = price column

/ the fby aggregates the tickdir from price column by sym
```

### 🔵 [QSQL 11.0] Select vs Exec Example
<a name="sql_11"></a>
[Top](#top)

[QSQL 11.1] Retrieve the distinct cities and countries from the table

```q
cnc: ([] city:`toronto`london`ny`vancouver; country:`canada`england`usa`canada)

city     | country
-------------------
toronto  | canada
london   | england
ny       | usa
vancouver| canada
```

```q
exec city, distinct country from cnc

key    | value
-----------------------------------
city   | toronto london ny vancouver
country| canada england usa
```

```q
select city, distinct country from cnc

/ error because select expects the columns to have the same length
```

### 🔵 [QSQL 12.0] Deltas/Differ Problem Set
<a name="sql_12"></a>
[Top](#top)

[QSQL 12.1] Return all trades where the trade price has changed

```q
select from trade where differ price

date       time         sym  price    size  cond
------------------------------------------------
2021.10.19 09:30:02.553 C    107.2018 63500 B   
2021.10.19 09:30:02.701 MSFT 96.87488 1700  B   
2021.10.19 09:30:02.743 RBS  97.11338 80700 C  

/ so differ will return all prices that are DIFFERENT then last
```

[QSQL 12.2] Add new column called change that calculates price changes between trades

```q
update change:deltas price from trade

date       time         sym  price    size  cond change    
--------------------------------------------------------
2021.10.19 09:30:02.553 C    107.2018 63500 B    107.201  
2021.10.19 09:30:02.701 MSFT 96.87488 1700  B    -10.326 
2021.10.19 09:30:02.743 RBS  97.11338 80700 C      0.238

/ so change = deltas from previous price
```

[QSQL 12.3] Select trades where trade prices have increased

```q
select from trade where (deltas price)> 0

date       time         sym    price    size  cond 
--------------------------------------------------
2021-10-19 09:30:02.553	C      107.2    63500  B
2021-10-19 09:30:02.743	RBS     97.1    80700  C
2021-10-19 09:30:02.758	A      100.3    50300  B
```

### 🔵 [QSQL 13.0] Problem Set 1 - AQ
<a name="sql_13"></a>
[Top](#top)


```q
\l salestable.q
tables[]
`quote`sales`stock`trade

/ tables [] shows you what tables are within the script
```

```q
/1 add new column to sales containing profit
/ profit = price * qty

update profit:price*quantity from `sales

trader |product |price| quantity| profit
-----------------------------------------
Bob    | pencil | 3   | 84      | 252
Bob    | pen	| 3   |	82	| 246
Paul   | book	| 3   |	64	| 192
```

```q
/2 work out total profit for each trader and product
/ (group by trader and product)

select sum profit by trader, product from sales

trader product profit
---------------------
Bob    book    79
Bob    paper   1353
Bob    pen     728
```

```q
/3 sort by profit

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

### 🔵 [QSQL 14.0] Problem Set 2 - AQ
<a name="sql_14"></a>
[Top](#top)


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

### 🔵 [QSQL 15.0] Retrieving values from Nested Table Problem Set
<a name="sql_15"></a>
[Top](#top)


```q
/1 create new column bidIndex, which shows the index position in descending values (large to small)

update bidIndex:({idesc x} each bidPrices) from t

t         bidPrices            bidSizes           bidIndex
----------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  57 0 72 50 62      2 1 0 4 
00:59:05  0.97 7.44 9.33 2.93  97 99 27 31        2 1 4 0
01:19:44  2.88 5.63 4.98 5.56  47 57 31 15 68 49  1 4 3 0

/ from col bidPrices, shows index position of descending values
/ 2nd index position = 3rd value = 9.84 largest
```

```q
/2 now isolate only the largest value

update bidIndex:({first idesc x} each bidPrices) from t

t         bidPrices            bidSizes           bidIndex
----------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  57 0 72 50 62      2 
00:59:05  0.97 7.44 9.33 2.93  97 99 27 31        2
01:19:44  2.88 5.63 4.98 5.56  47 57 31 15 68 49  1

/ adding first = only retrieves first value 
/ largest bid since ordered by idesc
```

```q
/3 add a new column, bestBid, and retrieve the bestBid from the index position in bidIndex

update bestBid:bidPrices@'bidIndex from update bidIndex:({first idesc x} each bidPrices) from t

t         bidPrices            bidSizes     bidIndex   bestBid
--------------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  0 72 50 62    2          9.84 
00:59:05  0.97 7.44 9.33 2.93  23 99 27 31   2          9.33
01:19:44  2.88 5.63 4.98 5.56  57 31 15 49   1          5.63

/ bestbid = looks at bidIndex col, retrieves index position 2 from bidPrice col = 9.8
/ everything after from is what we calculated above as the bidIndex col
```

```q
/4 add new column, bestBidSize, and retrieve the largest bidsize based on the bidIndex column

update bestBidSize:bidSizes@'bidIndex from update bidIndex:({first idesc x} each bidPrices) from t

t         bidPrices            bidSizes     bidIndex   bestBidSize
------------------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  0 72 50 62    2          50 
00:59:05  0.97 7.44 9.33 2.93  23 99 27 31   2          27
01:19:44  2.88 5.63 4.98 5.56  57 31 15 49   1          31

/ bestBidSize = looks at bidIndex col, retrieves index position 2 from bidSizes col = 50
```

```q
/5 Now combine all 3 queries into single one:

update bestBid:bidPrices@'bidIndex, bestBidSize:bidSizes@'bidIndex from update bidIndex:({first idesc x}each bidPrices) from t

t         bidPrices            bidSizes     bidIndex   bestBid  bestBidSize
---------------------------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  0 72 50 62    2          9.84       50
00:59:05  0.97 7.44 9.33 2.93  23 99 27 31   2          9.33       27
01:19:44  2.88 5.63 4.98 5.56  57 31 15 49   1          5.63       31

/ useful to use index position to retrieve value in another column
/ lookup colum @`source column
/ you can have multiple update statements to add new columns
/ the bestBid and bestBidSize columns actually retrieve from a new column called bidIndex
```

<hr>

<a name="adverbs"></a>
### 🔴 10. Adverbs
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

### [adverb] What is the difference between over and scan?
```q
/ [over] takes a function (like addition) and iterates through list
/ [over] is an accumulating iterator
/ begin with initial value, sequentially add each item into prev item
/ upon completion, the accumulator holds the final result

0 +/ 1 2 3 4 5
15

/ [scan] returns all intermediate values

(+\) 1 + til 10
1 3 6 10 15 21 28 36 45 55

/ scan converts a binary function to a unary uniform function (one that returns list of same length as input)
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
### 🔴 11. Attributes
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
### 🔴 12. Joins
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

### [joins-TS] QSQL Joins Problem Set

```q
\l ex-joins.q

\a

/ **fbTrades** (headers = dt, sym, size, book)
/ **newsItems** (headers = ndate, ticker, title) 
/ **quote** (headers = date, time, sym, size, cond, bid, ask, asize, bside)
/ **stock** (headers = sym, sector, employees)
/ **trade** (headers = dt, sym, price, size)
```

### Find total value of trades by sector (total value = price x size)

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

### [join] Join Problem Set

```q
\l fakedb.q
makedb[1000;1000]
tables[]
```
```q
/ select avg price by sym and save to t1

t1:select avg price by sym from trades

/ join this data onto the trades table

trades lj t1

/ select max bid, min ask for `IBM`MSFT`NOK from quotes

t2:select maxbid:max bid, minask:min ask by sym from quotes where sym in`IBM`MSFT`NOK

/ join this data onto the trades table

trades lj t2

/ join t1 onto t2 showing the data for all syms

t2 uj t1

/ need to use uj to show all data for all syms
```

<a name="at"></a>
### 🔴 13. @ & . Operator
[Top](#top)

### [@ Operator] Problem Set from AQ
```q
list1: 1 2 3 4 5 6 7 8 9 10
list2:((1 2 3 4; 4 3 2 1);(5 6 7 8;25 36 49 64); (9 10; 11 12); (13 14 15; 16 17 18; 19 20 21))
```
### [@ Operator] use @ operator to retrieve elements at index 3, 6 and 7 from list1
```q
@[list1;3 6 7]
4 7 8
```

### [@ Operator] use @ and . to retrieve value 11 from list2
```q
list2
(1 2 3 4;4 3 2 1)
(5 6 7 8;25 36 49 64)
(9 10; 11 12)
(13 14 15; 16 17 18; 19 20 21)

.[list2; 2 1 0]
11
```

### [@ Operator] return the first list from each nested list in list2
```q
.[list2;(::;0)]
1 2 3 4
5 6 7 8
9 10
13 14 15

/ :: return in place
```

### [@ Operator] calc the square of number at index 1 and 3 of list1
```q
@[list1;1 3;{x*x}]
1 4 3 16 5 6 7 8 9 10

/ still returns list1, but replaces values at index pos
/ 1 and 3 with their squares (2 -> 4 and 4-> 16)
```

### [@ Operator] add 5 to all items at odd indices of list1

```q
@[list1; where mod[til count list1;2];+; 5]
1 7 3 9 5 11 7 13 9 15
```
### [@ Operator] add "..." to the end of each word for ("quick","brown","fox")
```q
@[("quick";"brown";"fox");0 1 2;,[;"..."]]
"quick..."
"brown..."
"fox..."
```

### [@ Operator] Extract values from key a in dict using @ or .

```q
dict:`a`b`c!(1 2;3 4; 5 6)
a| 1 2
b| 3 4
c| 5 6

@[dict;`a]
1 2

.[dict;enlist `a]
1 2
```

### [@ Operator] turn the dict into a table using @ or .
```q
@[flip; dict]
a b c
-----
1 3 5
2 4 6
```

### [@ Operator] change values of key b to: 0 1 2 3 4 5 6 permanently

```q
@[`dict;`b; : ; til 7]

key | value
-------------------
a   | 1 2
b   | 0 1 2 3 4 5 6
c   | 5 6
```

### [@ Operator] change the syms in the table accordingly:
A = AAPL
B = GOOG
C = IBM

```q
t:([] sym:`A`B`B`C`A; price: 11.2 15.6 15.4 4.0 11.9; size: 101 97 151 403 149)

sym  | price | size
-------------------
A    |	11.2 |	101
B    |	15.6 |	97
B    |	15.4 |	151
C    |	4.0  |	403
A    |	11.9 |	149

@[t;`sym; :; `AAPL`GOOG`GOOG`IBM`AAPL]

sym   | price | size
-------------------
AAPL  |	11.2 |	101
GOOG  |	15.6 |	97
GOOG  |	15.4 |	151
IBM   |	4.0  |	403
AAPL  |	11.9 |	149
```

### [@ Operator] update the price with the volume traded (price * size) without using an update statement
```q
@[t;`price;{x*y}; @[t;`size]]

sym | price | size
-------------------
AAPL| 1131.2| 101
GOOG| 1513.2| 97
GOOG| 2325.4| 151
IBM | 1612.0| 403
AAPL| 1773.1| 149
```

### [@ Operator] permanently key the table by the sym column

```q
.[!;(1;`t)]

sym  | price  size
------------------
AAPL | 11.2   101
GOOG | 15.6   97
GOOG | 15.4   151
IBM  | 4.0    403
AAPL | 11.9   149

/ or

.[xkey;(`sym;`t)]

sym  | price  size
------------------
AAPL | 11.2   101
GOOG | 15.6   97
GOOG | 15.4   151
IBM  | 4.0    403
AAPL | 11.9   149

```
### [@ Operator] extract the price and size for IBM from the table

```q
.[t; (`IBM;`price`size)]
4f
403
```

<a name="racking"></a>
### 🔴 14. Racking & Alignment
[Top](#top)

### [QSQL] Racking xbar Problem Set 1 AQ

```q
trade:([] sym:`GOOG`IBM`GOOG`IBM`IBM; 
       time: 09:00 09:01 09:20 09:32 09:34; 
       size: 200 100 1200 200 400; 
       price: 30.9 36 30.9 36.1 36.2)

sym  | time  | size | price
---------------------------
GOOG | 09:00 |  200 | 30.9
IBM  | 09:01 |  100 | 36.0
GOOG | 09:20 | 1200 | 30.9
IBM  | 09:32 |  200 | 36.1
IBM  | 09:34 |  400 | 36.2

/1 lets bucket the size by sym in 15 min windows

select sum size by sym, 15 xbar time.minute from trade

sym  | minute | size
---------------------
GOOG | 09:00  |  200
GOOG | 09:15  |	1200
IBM  | 09:00  |  100
IBM  | 09:30  |  600

/ but not all syms + time buckets are present
/ ex, GOOG @ 9:30 isn't present
```

```q
/2 start by creating complete list of buckets

start: 09:00
end: 09:59
bucket: 15

/ so each bucket will be 15 mins

/3 Calc number of buckets required for time span (end-start)

(end-start) % bucket
3.933

/ round up to whole number

ceiling (end-start) % bucket
4

/ ceiling function will round 3.933 up to 4
```

```q
/4 create list of buckets by creating list of integers to num of buckets
/ this is done by multiplying each element x bucket size (15)

bucket * til ceiling (end-start) % bucket
0 15 30 45

/ bucket x til 4
/ 15 x 0 1 2 3

/5 add start time by making list of time buckets and rename as times

times: start+bucket * til ceiling (end-start) % bucket
09:00u; 09:15u; 09:30u; 09:45u
```

```q
/6 cross distinct syms with times list you just created and sort by sym

rack:(`sym xasc select distinct sym from trade) cross ([] minute:times)

sym  | minute
-------------
GOOG | 09:00
GOOG | 09:15
GOOG | 09:30
GOOG | 09:45
IBM  | 09:00
IBM  | 09:15
IBM  | 09:30
IBM  | 09:45
```

```q

/7 Join rack with original xbar table using # take operator

rack # select sum size, last price by sym, bucket xbar time.minute from trade

sym  | time  | size | price
---------------------------
GOOG | 09:00 |  200 | 30.9
GOOG | 09:15 | 1200 | 30.9
GOOG | 09:30 |	    |	
GOOG | 09:45 |	    |	
IBM  | 09:00 | 100  | 36.0
IBM  | 09:15 |	    |	
IBM  | 09:30 | 600  | 36.2
IBM  | 09:45 |      |		
```

```q
/8 update null size with 0

update 0^size from rack # select sum size, last price by sym, bucket xbar time.minute from trade

sym  | time  | size | price
---------------------------
GOOG | 09:00 |  200 | 30.9
GOOG | 09:15 | 1200 | 30.9
GOOG | 09:30 |	  0 |	
GOOG | 09:45 |	  0 |	
IBM  | 09:00 |  100 | 36.0
IBM  | 09:15 |	  0 |	
IBM  | 09:30 |  600 | 36.2
IBM  | 09:45 |    0 |	
```

```q
/9 update null price with last price

update fills price by sym from update 0^size 
from rack # select sum size, last price by sym, 
bucket xbar time.minute from trade

sym  | time  | size | price
---------------------------
GOOG | 09:00 |  200 | 30.9
GOOG | 09:15 | 1200 | 30.9
GOOG | 09:30 |	  0 | 30.9	
GOOG | 09:45 |	  0 | 30.9	
IBM  | 09:00 |  100 | 36.0
IBM  | 09:15 |	  0 | 36.0	
IBM  | 09:30 |  600 | 36.2
IBM  | 09:45 |    0 | 36.2	
```

### [QSQL] Racking xbar Problem Set 2 AQ

```q
/1 create a function for creating a rack of time buckets

createrack:{[start;end;bucket;symbols]
            times:start + bucket * til ceiling (end-start:bucket xbar start)% bucket}

/ takes in 4 arguments
/ i don't undersatnd the end-start: bucket syntax :(

/ lets test it out by calling the function

createrack[2014.04.21D09:23; 2014.04.23D12:44; 0D00:15; `GOOG]

2014-04-21T09:15:00.000000p
2014-04-21T09:30:00.000000p
2014-04-21T09:45:00.000000p
...
/ returns a list of dates/times
```

```q
/2 add cross against list of syms

createrack:{[start;end;bucket;symbols]
            times:start+bucket*til ceiling (end-start:bucket xbar start)% bucket;
            ([] sym:symbols,()) cross ([] time:times)}

sym  | time                       
---------------------------------
GOOG | 2014-04-21T09:15:00.000000
GOOG | 2014-04-21T09:30:00.000000 
GOOG | 2014-04-21T09:45:00.000000 
GOOG | 2014-04-21T10:00:00.000000 
```

```q
/3 write another function which takes 4 parameters, calling our createrack func 
/ and joins to the rack the bucket of data from trade table

jointables:{[start;end;bucket;symbols] 
            createrack[start;end;bucket;symbols]
            #select sum size by sym, bucket xbar time from trades 
            where date within `date$(start;end), sym in symbols, 
            time within (start;end)}

/ call same argument as before            

jointables[2014.04.21D09:23; 2014.04.23D12:44; 0D00:15; `GOOG]

sym  | time                       | size
------------------------------------------
GOOG | 2014-04-21T09:15:00.000000 | 53559
GOOG | 2014-04-21T09:30:00.000000 | 108224
GOOG | 2014-04-21T09:45:00.000000 | 87757
GOOG | 2014-04-21T10:00:00.000000 | 86012
```







[Top](#top)
