# Allen's KDB Practice Problems + Solutions
<a name="top"></a>

1. [General Knowledge](#gen)
	1. [General Problem Set 1](#gen_ps1)
	2. [General Problem Set 2](#gen_ps2)
 	3. [General Problem Set 3](#gen_ps3)
  	4. [Case Study 1 - Comparing Potential Crosses](#gen_ps4)
	5. [Case Study 2 - Netting Buys and Sells](#gen_ps5)

2. [Datatypes & Casting](#cast)
	1. [Datatype Problem Set 1](#data_ps1)
 	2. [Datatype Problem Set 2 - Casting](#data_ps2)
  	3. [Datatype Problem Set 3 - Temporal](#data_ps3)
   	4. [Datatype Problem Set 4 - Strings](#data_ps4)
   	5. [Datatype Problem Set 5 - GS](#data_ps5)

3. [Lists](#list)
	1. [List Problem Set 1](#list_ps1)
	2. [List Problem Set 2](#list_ps2)
	3. [List Problem Set 3](#list_ps3)
	4. [List Problem Set 4 - Matrix](#list_ps4)
 	5. [List Problem Set 5 - AQ 1](#list_ps5)
  	6. [List Problem Set 6 - TS 1](list_ps6) 

4. [Dictionary](#dictionary)
	1. [Dictionary Problem Set 1](#dict_ps1)
 	2. [Dictionary Problem Set 2](#dict_ps2)
  	3. [Dictionary Problem Set 3 - TS 1](#dict_ps3)
   	4. [Dictionary Problem Set 4 - Nested](#dict_ps4)
   	5. [Dictionary Problem Set 5 - AQ 1](#dict_ps5)
   	6. [Dictionary Problem Set 6 - AQ 2](#dict_ps6)
   	7. [Dictionary Problem Set 7 - AQ 3](#dict_ps7)
   	8. [Dictionary Problem Set 8](#dict_ps8)

5. [Tables](#tables)
	1. [Tables Problem Set 1](#table_PS1)
	2. [Tables Problem Set 2](#table_PS2)
	3. [Tables Problem Set 3](#table_PS3)
	4. [Tables Problem Set 4](#table_PS4)
	5. [Tables Problem Set 5](#table_PS5)
	6. [Tables Problem Set 6](#table_PS6)
	7. [Tables Problem Set 7](#table_PS7)
	8. [Tables Problem Set 8](#table_PS8)
	9. [Tables Problem Set 9](#table_PS9)
	10. [Tables Problem Set 10](#table_PS10)
	11. [Tables Problem Set 11](#table_PS11)
	12. [Tables Problem Set 12](#table_PS12)
	13. [Tables Problem Set 13](#table_PS13)
	14. [Tables Problem Set 14](#table_PS14)

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
	3. [QSQL Problem Set 3 - TS](#sql_3)
	4. [Creating Buckets using xbar](#sql_4)
	5. [Creating Buckets using within](#sql_5)
	6. [Creating Buckets using BIN](#sql_6)
	7. [fby Problem Set](#sql_7)
	8. [Table Query Problem Set 1](#sql_8)
	9. [Table Query Problem Set 2](#sql_9)
	10. [Table Query Problem Set 3](#sql_10)
	11. [Signum Deltas Problem Set](#sql_11)
	12. [Select vs Exec Example](#sql_12)
	13. [Deltas/Differ Problem Set](#sql_13)
	14. [QSQL Problem Set 1 - AQ](#sql_14)
	15. [QSQL Problem Set 2 - AQ](#sql_15)
	16. [Nested Tables Problem Set](#sql_16)
11. [Adverbs](#adverbs)
12. [Attributes](#attributes)
13. [Joins](#joins)
14. [@ & . Operator](#at)
15. [Racking & Alignment](racking)
16. [x`each Problem Sets](#xeach)

<hr>

<a name="gen"></a>
### 🔴 1. General Knowledge
[Top](#top)


🔵 [Gen 1.1] General Problem Set 1
<a name="gen_ps1"></a>

```q
[Gen 1.1]

/ 1. Retrieve 3 random elements from 0-2

3 ? 3
2 0 1

/ atom ? atom
/ x ? y
/ retrieve x random elements from y 
/ retrieve 3 random elements from 0-2
/ so even though y is an atom, it's really a list
```

```q
[Gen 1.1]

/ 2. From list 1 2 3, find index position of 3

1 2 3 ? 3
2

/ list ? atom
/ from list x, find index position of element y
/ element 3 is in index position 2 of list 1 2 3
```

```q
[Gen 1.1]

/ 3. Return 3 random elements from list 1 2 3

3 ? 1 2 3 
1 1 3

/ atom ? list
/ return x number of random elements from list y
```

```q
[Gen 1.1]

/ 4. Combine the below 3 expressions into a single line

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

```q
[Gen 1.1]

/ 5. What are some common operators?

#   / take
_   / drop
?   / find, randomize
@   / apply
!   / dictionary, key, unkey, 
$   / cast, enumerate
,   / join
^   / fill
```

```q
[Gen 1.1]

/ 6. What is a dictionary?

/ A dictionary is a data structures that map from a domain of keys to a range of values 
/ contains a ! to separate keys and values
/ flip a dictionary and you get a table
```

```q
[Gen 1.1]

/ 7. What is a table?

/ is a list of dictionaries (flipped)
/ any single row is a dictionary
/ tables are ordered, which means you can index them
/ tables are encased by parathesis ( ) and contain brackets [ ] which assigns the key.
```

```q
[Gen 1.1]

/ 8. Show all variables in the current session of q

\v
`a`b`c`d
```

```q
[Gen 1.1]

/ 9. How do you close the current q session?

\\
```

```q
[Gen 1.1]

/ 10. What is the diff between equals = and match ~

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

```q
[Gen 1.1]

/ 11. What is 2 | 5

5

/ pipe calculates the larger of x | y
```

```q
[Gen 1.1]

/ 12. What is 2 & 5

2

/ amper = smaller of x & y
```

🔵 [Gen 1.2] General Problem Set 2
<a name="gen_ps2"></a>

```q
[Gen 1.2]

/ 1. What is 2 cut 1 2 3 4 5 6

(1 2; 3 4; 5 6)

/ cuts list into elements of 2
/ x cut y
/ y = list
```

```q
[Gen 1.2]

/ 2. What is 1 4 cut 1 2 3 4 5 6

(2 3 4; 5 6)

/ 2nd element (4) = cut list by 4
/ first element (1) = AFTER cutting, then drop everything before this element (1) from output
```

```q
[Gen 1.2]

/ 3. What is 2 3 cut 1 2 3 4 5 6

(3; 4 5 6)

/ 2nd element (3) = cut list into elements of 3
/ 1st element (2) = drop all elements before 2
```

```q
[Gen 1.2]

/ 4. What is signum -2 0 1 3

-1 0 1 1

/ signum will tell you if something is positive, 0, or negative
/ neg, 0, pos pos
```

```q
[Gen 1.2]

/ 5. What is 1 cross 3 4?

1 3
1 4

/ returns all possible combinations of x cross y
/ note - does NOT multiply or add
```

```q
[Gen 1.2]

/ 6. Create every possible combination between list s and v

s:`IBM`MSFT
v: 1 2

s cross v
((`ibm;1);(`ibm;2);(`apple;1);(`apple;2))

/ you are crossing 2 lists
/ returns a list of tuples of every possible combo
```

```q
[Gen 1.2]

/ 7. Create a table of every possible combination between list s and v

s:`IBM`MSFT
v: 1 2

( [] s) cross ( [] v)

s     | v
----------
ibm   | 1
ibm   | 2
apple | 1
apple | 2

/ if you did s cross v, this would return a list of tuples
/ you can "convert" list s and list v into tables
/ by adding ( [] )
/ therefore you are crossing 2 tables
```

```q
[Gen 1.2]

/ 8. Building xbar timeseries

time: 09:00 09:15
sym: `GOOG`IBM

( [] sym) cross ( [] time)

sym  | time
-----------
GOOG | 09:00
GOOG | 09:15
 IBM | 09:00
 IBM | 09:15

/ time is a list of times
/ sym is a list of syms
/ "convert" the 2 lists into tables
/ and when you cross them, it returns a table
```

🔵 [Gen 1.3] General Problem Set 3
<a name="gen_ps3"></a>

### [system] How do you read a txt file?

```q
[Gen 1.3]

/ 1. Assume txt file named test.txt
/ this file needs to be in the same directory/folder where your q is

hopen `:test.txt
read0 `:test.txt

/ hopen = opens the txt file
/ read0 = reads the txt file
```

```q
[Gen 1.3]

/ 2. How do you Open and Edit a txt file?

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

```q
[Gen 1.3]

/ 3. How do you load a csv file (headers vs no headers)?

/ 1. read file first to see what datatypes are contained in file
/ 2. extract what datatypes are in file
/ 3. headers or no headers?
/ 4. open the file
```

```q
[Gen 1.3]

/ 3.1 How do you load a csv file with Column Headers

/ if you want to load file with column headers, you'll need a delimiter
/ a delimiter = character (comma) that marks beg and end of a unit of data
/ by enlisting a delimiter (comma), the first row of csv file read as a column header

/ first, create a sample csv file called book1 and save to your directory

book1
city population temp
---------------------
LA      100     10
NY      200     20
SEA     300     30

/ step 1: read the csv file using read0

read0 `:book1.csv
("city,population,temp";"LA,100,10";"NY,200,20";"SEA,300,30")

/ read0 function will returns the contents of a text file as a list of strings
/ this gives you an idea of what datatypes are contained in the file
/ in this case, sym, int int

/ step 2: load the file enlisting a comma as a delimiter using 0:

t2:("SII";enlist",") 0: `:book1.csv
t2

city	population  temp
-------------------------
LA	100	    10
NY	200    	    20
SEA	300	    30

/ the 0: function helps you load files
/ t2 names your table
/ "SII" = sym, int, int for datatypes
/ since the csv file has headers, you'll need to enlist a comma
/ this is known as a delimiter
/ delimiter = is a character (comma) that marks the beginning or end of a unit of data
/ what separates each column
```

```q
[Gen 1.3]

/ 4.1 How do you load a csv file without Column Headers

/ if the CSV file contains data but no column names, dont need to enlist a delimiter

t3:("SSJ";",") 0: `:book1.csv

t3
LA	100	    10
NY	200    	    20
SEA	300	    30
```

🔵 [Gen 1.4] Case Study 1 - Comparing Potential Crosses
<a name="gen_ps4"></a>

```q
[Gen 1.4]

/ How would you compare current orders vs potential crosses?

Objectives:
1. Load CSV file of current orders (tradepad)
2. Load CSV file of proposed crosses (cross)
3. For each symbol, check opposing direction, and pull in quantity to cross
4. Create new column displaying shares that can cross
5. Retrieve columns in clean format to export back into csv
```

```q
[Gen 1.4]

/ 1. Create tradepad and cross csv files

tradepad
ric	side	qty
-------------------
1810.HK	Buy	500
0700.HK	Buy	500
9988.HK	Buy	500
0001.HK	Buy	500
0016.HK	Buy	500

cross
ric	  brokerside brokerqty
--------------------------------
1810.HK   Sell	     500
0700.HK   Sell	     300
9988.HK   Buy	     200
0003.HK   Sell	     500
0016.HK	  Sell	     800
```

```q
[Gen 1.4]

2. Pull in CSV file of current orders (tradepad)

/ 2a. first read file to see what datatypes it contains

read0 `:tradepad.csv
("ric,side,qty";"1810.HK,Buy,500";"0700.HK,Buy,500";"9988.HK,Buy,500";"0001.HK,Buy,500";"0016.HK,Buy,500")

/ file contains sym, sym, int

/ 2b. load the file with headers (need delimiter)

t:("SSI";enlist",") 0: `:tradepad.csv

ric	side	qty
-------------------
1810.HK	Buy	500
0700.HK	Buy	500
9988.HK	Buy	500
0001.HK	Buy	500
0016.HK	Buy	500
```

```q
[Gen 1.4]

/ 3. Load csv file of proposed crosses (cross)

/ 3a. first read file to see what datatypes it contains

read0 `:cross.csv
("ric,brokerside,brokerqty";"1810.HK,Sell,500";"0700.HK,Sell,300";"9988.HK,Buy,200";"0003.HK,Sell,500";"0016.HK,Sell,800")

/ file contains sym, sym, int

/ 3b. load the file with headers (need delimiter)

c:("SSJ";enlist",") 0: `:cross.csv

ric	  brokerside brokerqty
--------------------------------
1810.HK   Sell	     500
0700.HK   Sell	     300
9988.HK   Buy	     200
0003.HK   Sell	     500
0016.HK	  Sell	     800
```

```q
[Gen 1.4]

/ 4. Combine the 2 tables (using left join)

t lj 1!c

ric	 side qty brokerside brokerqty
---------------------------------------
1810.HK	 Buy  500 Sell	     500
0700.HK	 Buy  500 Sell	     300
9988.HK	 Buy  500 Buy	     200
0001.HK	 Buy  500		
0016.HK	 Buy  500 Sell	     800

/ need to key table c in order for lj to work
```

```q
[Gen 1.4]

/ 5. check if opposing sides (same side = no cross)
/ add new column called "crossqty"
/ where applicable, update crossqty column with crossable qty

/ need to use an IF/ELSE statement update the crossqty column
/ logic: IF sides are same, do nothing
/ ELSE, update column with brokerqty -qty (crossable qty)

/ syntax
$[condition; true_do_this; else_do_this]

a: update crossqty: ?[side=brokerside;0N;?[qty<brokerqty;qty;brokerqty]] from t lj 1!c
a
ric	 side qty  brokerside brokerqty crossqty
--------------------------------------------
1810.HK	 Buy  500  Sell	     500        500
0700.HK	 Buy  500  Sell	     300        300
9988.HK	 Buy  500  Buy	     200	
0001.HK	 Buy  500			
0016.HK	 Buy  500  Sell	     800        500

/ there is an embedded if/else statement, since you need to account
/ for when the cross qty is larger than your order qty
```

```q
[Gen 1.4]

/ 6. Retrieve only the RICs, side, and crossable qty

select ric, side, crossqty from a where crossqty > 0

ric	 side  crossqty
-----------------------
1810.HK	 Buy   500
0700.HK	 Buy   300
0016.HK	 Buy   500

/ here you have it. this is the final result
```

🔵 [Gen 1.5] Case Study 2 - Netting buys and sells
<a name="gen_ps5"></a>

```q
[Gen 1.5]

/ Given table t below
/ there are multiple lines of buys and sells in same stock
/ determine what is the net quantity

t:([] ric:`AAPL; side:`buy`sell`sell`buy`buy; size:10 30 50 100 90)

ric | side | size
-----------------
AAPL| buy  | 10
AAPL| sell | 30
AAPL| sell | 50
AAPL| buy  | 100
AAPL| buy  | 90
```

```q
[Gen 1.5]

/ 1. update the size column to include pos or neg signs

update size: ?[side=`buy;size;neg size] from t

ric	side	size
--------------------
AAPL	buy	  10
AAPL	sell	 -30
AAPL	sell	 -50
AAPL	buy	 100
AAPL	buy	  90
```

```
[Gen 1.5]

/ 2. retrieve the aggregate net position by summing column

select ?[side=`buy;size;neg size] by ric from t

ric  | size
-----------
AAPL | 120

/ thoughts - a computer wont understand 'buy' or 'sell'
/ but if qty are pos or neg, it can be "collapsed"
```

<hr>

<a name="cast"></a>
### 🔴 2. Datatypes & Casting
[Top](#top)

🔵 [Data 2.1] Datatype Problem Set 1
<a name="data_ps1"></a>

```q
[Data 2.1]

/ 1. What is an atom?

/ an atom is an irreducible value of a specific data type
/ has a negative datatype (ex, -7h)
/ atoms can be chars or syms

"a" / char atom
`sym / sym atom
```

```q
[Data 2.1]

/ 2. What is a list?

/ a list is an ordered sequence of items (members are called items)
/ encased by parathesis, separated by semi-colon
/ has a positive datatype (ex, 7h)
```

```q
[Data 2.1]

/ 3. What is a simple list?

(1;2;3)
("a";"b";"c")
(`life;`is;`great)

/ a simple list has  all same datatypes
/ aka vectors
/ can be a list of ints, chars, syms
```

```q
[Data 2.1]

/ 4. What is a General List?

(1;1.1;`1)
(-10.0; 3.1415e; 1b)

/ general list = mixed lists
/ general lists are lists NOT containing homogenous atoms
/ first list is an int, a float, and a sym
/ second list is a float, a real number, and a boolean
```

```q
[Data 2.1]

/ 5. What is a string?

"this is a string"

/ a string is a list of chars
/ a string is NOT a datatype
/ also called a char vector
```

```q
[Data 2.1]

/ 6. What is a sym?

/ a sym is an atomic entity holding text 
/ represented with a back tick ` 
/ smaller in size than a char

`sym / sym atom
`one`two`three / sym vector
```

```q
[Data 2.1]

/ 7. How is a sym diff from a char and a string?

/ syms start with a backtick`, while chars are encased with parathensis " "
/ syms are smaller in size than chars
/ syms (generally) cannot contain spaces while strings can

`thisisasym
"this is a char vector"

/ A string is a (list) of chars
/ aka char vector

/ syms are always atomic, while chars can be vectors

type `atomic
-11h

/ checking datatype of sym = negative = atomic

type "apple"
10h
/ vector (positive) datatype char
```

```q
[Data 2.1]

/ 8. What is a negative datatype?

/ a negative type is an ATOM
/ a positive type is for everything else (ie, a list)

type 5
-7h

/ integer atom

type 2 3 4
7h

/ integer vector
```

🔵 [Data 2.2] Datatype Problem Set 2 - Casting
<a name="data_ps2"></a>

```q
[Data 2.2]

/ 1. What is casting?

/ casting converts one datatype to another
```

```q
[Data 2.2]

/ 2. Show 3 ways to convert FLOAT 4.5 to an INT

`int$4.5
"i"$4.5
6h$4.5

/ casting always requires $
/ 1int$4.5 is probably the most common
```

```q
[Data 2.2]

/ 3. What happens when you cast a DATE to an INT?

`int$2000.10.04
3

/ casts as dates from 2000.01.01
```

```q
[Data 2.2]

/ 4. Convert syms `a`b`c to a string

string `a`b`c
("a","b","c")

/ to convert syms to strings,
/ simply use the STRING function

```

```q
[Data 2.2]

/ 5. How do you cast chars "a","b","c" to a sym?

`$"a","b","c"
`abc

/ alternative syntax:

"S"$"a","b","c"
`abc

/ when casting chars to syms
/ simply use backtick `$
/ or use capital "S"
/ a string is a list of chars
```

```q
[Data 2.2]

/ 6. Cast STRING "2014.01.01" to a DATE

"D" $ "2014.01.01"
-14h

/ "2014.01.01" was originally a string
/ use capital "D" to cast strings to date
```

```q
[Data 2.2]

/ 7. Cast SYM `2013.01.01 to DATE

"D" $ string `2013.01.01

/ `2013.01.01 is a sym
/ requires first to cast to STRING, then cast to DATE
```

```q
[Data 2.2]

/ 8. Cast FLOAT 3.14 to an INT

`int $ 3.14 
3

/ note rounding for ints
/ alternatively "I" $ 3.14
```

```q
[Data 2.2]

/ 9. Cast STRING "abcde" to a SYM

`$"abcde"

/ can simply use backtick to cast to sym
```

```q
[Data 2.2]

/ 10. What is parsing?

/ parsing is converting a STRING to another datatype.
```

```q
[Data 2.2]

/ 11. Given mixed list L: ("100.1";"hello";"10")
/ convert elements to float, char, and int

"FCI"$L
100.1 / float
" " / char
10i / int
```

```q
[Data 2.2]

/ 12. convert l:("1.00001"; "200"; "3.1417")
/ to a float, int, float

l:("1.00001"; "200"; "3.1417")
"FIF"$l

1.00001 / float
200 / int
3.1417 / float
```

```q
[Data 2.2]

/ 13. Given strings "2001.02.02" and "2003.08.09", parse the strings into KDB dates

"D"$("2001.02.02";"2003.08.09")

/ these are strings which you are trying to parse into the date datatype
/ have to use upper case when parsing
```

```q
[Data 2.2]

/ 14. Convert list of syms `a`b`c to strings

string `a`b`c
"a","b","c"
```

```q
[Data 2.2]

/ 15. Convert a list of syms to a list of chars?

raze string `a`b`c
"abc"

/ sym to string, then string to char
/ use raze function to collapse 1 layer
```

🔵 [Data 2.3] Datatype Problem Set 3 - Temporal
<a name="data_ps3"></a>

```q
[Data 2.3]

/ 1. Why do you get dates when casting int to date?

/ dates are stored as integers (days) from 2000.01.01
```

```q
[Data 2.3]

/ 2. Get today's date store it as variable d

d: .z.d
2021-11-01d

/ .z.d = retrieves today's date
```

```q
[Data 2.3]

/ 3. Calculate the number of days since last christmas

d - 2020.12.25
311i

/ can use algebra with dates (ints underneath)
```

```q
[ Data 2.3]

/ 4. What day of the week was Jan 10, 2011?

2011.01.10 mod 7
2i

/ since dates start on sunday, 2 days from sunday = Monday

.z.d mod 7
2i

/ todays date = monday, Nov 11
/ 2 days from sunday = Monday
```

```
[Data 2.3]

/ 5. How many days were there in 2004?

2005.01.01 - 2004.01.01
366
```

🔵 [Data 2.4] Datatype Problem Set 4 - Strings
<a name="data_ps4"></a>

```q
[Data 2.4]

/ 1. Define strings s1: "Hello" and s2: "World"

s1: "hello"
s2: "world"
```

```q
[Data 2.4]

/ 2. Join the 2 strings together and save to s

s:s1, " ",s2
"hello world"

/ join strings using ,
```

```q
[Data 2.4]

/ 3. From string s, find index position of "w"

s?"w"
6

/ utilize the ? find operator to search index position within string
```

```q
[Data 2.4]

/ 4. Find index positions of all "l" in s

ss[s;"l"]
2 3 9

/ ss = search string function. returns index position
```

```q
[Data 2.4]

/ 5. Find index position of last l

last ss[s;"l"]
```

```q
[Data 2.4]

/ 6. Remove "hello" and add " of warcraft" to s

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
[Data 2.4]

/ 7. Find index location for "ryan" in "hello ryan where is ryan"

"hello ryan where is ryan" ss "ryan"
6 20

/ ss = string search
/ returns index location
/ ryan appears twice; at the 6th and 20th index location
```

```q
[Data 2.4]

/ 8. Replace "ryan" with "john"

ssr["hello ryan where is ryan";"ryan";"john"]
hello johhn where is john

/ ssr = search string replace function
/ first arg = input string
/ second arg = what to replace
/ third arg = what to replace with
```

```q
[Data 2.4]

/ 9. Create an enumeration t2 containing values p q r that is restricted to domain t1

t1: `symbol$()
t2: `t1$`p`q`r

/ t2 is now an enumeration which only contain domain t1 (syms)
```

```q
[Data 2.4]

/ 10. Insert new value `u into t2

t2,:`u
error

/ since t2 is restricted to domain t1, need to first add `u into t1 before adding to t2

t1,:`u
t2,:`u
`p`q`r`u

/ now it works
```

🔵 [Data 2.5] Datatype Problem Set 5 - GS
<a name="data_ps5"></a>

```q
/ 1. Turn 2 lists of symbols into one longer list. 

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
### 🔴 3. Lists
[Top](#top)

🔵 [List 3.1] List Problem Set 1 - easy
<a name="list_ps1"></a>

```q
[List 3.1]

/ 1. Create a list from 1 to 10

1 + til 10
1 2 3 4 5 6 7 8 9 10
```

```q
[List 3.1]

/ 2. Create a list of 10 even numbers

2 * 1 + til 10
2 4 6 8 10 12 14 16 18

/ til 10 = 0 1 2 3
/ +1 = 1 2 3 4 5
/ *2 = 2 4 6 8 etc.
```

```q
[List 3.1]

/ 3. Create a list of 10 odd numbers

1 + 2 * til 10
1 3 5 7 9 11 13 15 17 19

/ 2 * til 10 = 0 2 4 6..
/ +1 = 1 3 5 7...
```

```q
[List 3.1]

/ 4. Obtain the first 10 even numbers starting from 42

42 + 2 * til 10
42 44 46 48 50 52 54 56 58 60
```

```q
[List 3.1]

/ 5. Given list k: 1 2 3 4 5, drop item from list at index position 2

k: 1 2 3 4
k _ 2

/ _ is drop
/ note syntax - have to include space before and after the _
/ _ will remove item from index position x from list
```

```q
[List 3.1]

/ 6. Using sublist, take 3 elements from list 1 2 3 4 5

3 sublist 1 2 3 4 5
1 2 3

/ x sublist y
/ where x = atom or pair and y = list
/ takes x elements from list y
```

```q
[List 3.1]

/ 7. Using sublist, take last 2 elements from 1 2 3 4 5

-2 sublist 1 2 3 4 5
4 5

/ -2 takes last 2 elements
/ sublist like take #
```

```q
[List 3.1]

/ 8. Using sublist, what happens when you take more elements than in list

5 sublist 1 2 3
1 2 3

/ sublist ONLY takes what's available
/ since only 3 elements in list, takes 3 elements then STOPS
/ does not wrap around
```

```q
[List 3.1]

/ 9. Using sublist, take 2 elements from index position 2

2 2 sublist 1 2 3 4 5 6
3 4

/ from index position 2, take 2 elements
```

🔵 [List 3.2] List Problem Set 2
<a name="list_ps2"></a>

```q
[List 3.2]

/ 1. Find index position of 3 from list 1 2 3 4 5

1 2 3 4 5 ? 3
2

/ ? = find 
/ list ? x 
/ "finds" index position of x in list 
```

```q
[List 3.2]

/ 2. What happens if you query index position > list length?

1 2 3 4 5 ? 7
5

/ find index position of 7
/ not found (out of range), returns max index + 1
/ 4 (max index position) + 1 = 5
```

```q
[List 3.2]

/ 3. Retrieve element from index position 2 from list 1 2 2 2

1 2 2 2 ? 2
1

/ find index position of 2
/ multiple occurence, only returns first
```

```q
[List 3.2]

/ 4. Pick 5 random items from list 1 2 3 4 5

5? 1 2 3 4 5
1 3 2 2 4

/ atom ? list
/ picks 5 random items from list
```

```q
[List 3.2]

/ 5. Pick 5 random items from 0 - 9

5 ? 10
8 5 5 9 2

/ atom ? atom (this atom becomes list)
/ 10 = list from 0 to 9
```

```q
[List 3.2]

/ 6. Pick 5 DISTINCT items from 0 - 9

-5 ? 10
8 4 1 9 3

/ using a negative sign = DISTINCT
/ aka "deal", like dealing cards from a deck
/ never repeats
```

```q
[List 3.2]

/ 7. What happens when you return 11 distinct numbers from 0 - 9

-11 ? 10
error

/ can't return 11 distinct items from list of 10 elements
```

```q
[List 3.2]

/ 8. Pick 5 random syms with length 2

5?`2
`mp`ik`mi`og`nm
```

```q
[List 3.2]

/ 9. Pick 5 random chars

5? " "
"lsefv"
```

```q
[List 3.2]

/ 10. What is the diff between list ? atom and atom ? list

list ? atom
1 2 3 4 5 ? 2
1

/ list ? atom = finds index location of atom in list

atom ? list
2 ? 1 2 3 4 5
3 4

/ atom ? list = returns 2 random elements from list
```

```q
[List 3.2]

/ 11. Given b: (1 2; (3 4; 5 6); 7; 8)
/ flatten all levels

1 2
    3 4
    5 6
7
8

raze/ [b]
1 2 3 4 5 6 7 8
```


🔵 [List 3.3] List Problem Set 3 - easy
<a name="list_ps3"></a>

```q
[List 3.3]

/ 1. Create empty List d

d: ()
```

```q
[List 3.3]

/ 2. Redefine d to be empty list of ints

d: `int $ ()

/ cast empty list as `ints
```

```q
[List 3.3]

/ 3. Add 5 random elements to d

d, 5 ? til 10

/ 5 ? til 10 = randomly select 5 numbers from 0-9
/ d , joins these 2 lists, thereby adding into list
```

```q
[List 3.3]

/ 4. Create list l with 20 random values from 3 to 30

l: 20 ? 3_til 31

/ til 31 = list from 0 to 30
/ 3_ drops first 3 elements
/ so you have 3 - 30
/ 20 ? = picks 20 random numbers from list
```

```q
[List 3.3]

/ 5. Find the 20th number in list l

l[19]
16

/ indexing starts at 0
/ so index position 0 = first element
/ so element 20 = 19th index position
```

```q
[List 3.3]

/ 6. Are any of these numbers in the list? 3 5 7 11 13 17

3 5 7 11 13 17 in l
0011100

/ returns list of booleans

where in 3 5 7 11 13 17 in l
2 3 4

/ retrieves index position where the elements show up in l
```

```q
[List 3.3]

/ 7.  Add each element of l to its index position.
/ so you have 2 lists; 20 elements of l, and its index position

l + til count l

/ count l = 20 elements in list l
/ til 20 = 0 - 19, gives you the index position
/ simply add list l to its index position 
```

```q
[List 3.3]

/ 8. How many even numbers are there? 

l mod 2
1 1 0 1 0 1 1 0 0 1 0 1 0 1 0 1 0 1 1 0

/ returns a list of booleans
/ mod 2 tells us when the remainder is
/ so 0 = no remainder = even number
/ and 1 = remainder = odd number

count where l mod 2
12

/ counts booleans = 1 (true) aka odd numbers

count where not l mod 2

/ counts NOT where boolean = true aka false aka 0 
/ not = 0, so counts all the 0s (even numbers)
```

```q
[List 3.3]

/ 9. Given the 2 lists size and price below,
/ Calculate the average size where price is greater than 5

size: 100 300 50 70
price: 4 8 6 2

avg size where price > 5
175
```

🔵 [List 3.4] List Problem Set 4 (Matrix)
<a name="list_ps3"></a>

```q
[List 3.4]

/ Given matrix m:

m:(1 2 3; 4 5 6; 7 8 9)
1 2 3
4 5 6
7 8 9
```
```q
[List 3.4]

/ 1. Retrieve the first element of each nested list

first each m
1 4 7

/ first + each returns the first element each nested list
```

```q
[List 3.4]

/ 2. Retrieve the middle column of m and save it as a

a: m[ ;1]

/ [row;column]
/ blank for row
/ column 1 = index position 2, so retrives 2nd column
```

```q
[List 3.4]

/ 3. Replace middle row (second row) of m with a

m[1; ]:a
(1 2 3;
2 5 8;
7 8 9)

/ [row;column] 
/ index position 1 = 2nd row

/ alternative syntax:

m[1]: a

/ ignores column since you are after the 2nd row
```

```q
[List 3.4]

/ 4. Transpose m and store as mm

mm: flip m

/ transpose is a fancy way of saying flip
```

```q
[List 3.4]

/ 5. join extra row to mm, consisting of all 10s

mm,: 3#10

/ adds row using , : join assign
```

```q
[List 3.3]

/ 6. Given matrix nest:

nest: (1 2 3; `a`c`b;10 11 12 14f; 100011b)
```

```q
[List 3.4]

/ 6.1 Find the datatype of each row

type each nest
7 11 9 1h

/ type each = returns datatype of EACH nested list
/ 7 = long
/ 11 = sym
/ 9 = float
/ 1h = boolean
```

```q
[List 3.4]

/ 6.2 Collapse this nested list

raze nest
1 2 3 `a`c`b 10 11 12 14f 100011b

/ raze collapses the nested list one level
```

🔵 [List 3.5] List Problem Set 5 (AQ 1)
<a name="list_ps5"></a>

```q
[List 3.5]

/ Given the 3 lists:

games:`crash`streets`echo`crash2`sonic`micro`pokemon`supermario`bomber`zelda
platform: `ps1`sega`sega`ps1`sega`ps1`gameboy`gameboy`sega`gameboy
level: (7 9 6i; 2 5i; 4 4i; 10 2 1i; 1 10i; 8i; 0 3i; 6 0i; 8 4i; 1 10i)
```

```q
[List 3.5]

/ 1. Combine the 3 lists into a single table

([] games; platform; level)

games     | platform |   level
-------------------------------
crash     | ps1      |  7 9 6i
streets   | sega     |    2 5i
echo      | sega     |	  4 4i
crash2    | ps1	     | 10 2 1i
sonic     | sega     | 	 1 10i
micro     | ps1	     |      8
pokemon   | gameboy  |	  0 3i
supermario| gameboy  |	  6 0i
bomber    | sega     |	  8 4i
zelda     | gameboy  |	 1 10i
```

```q
[List 3.5]

/ 2. Count the number of users per game and save as users
/ (hint - under level)

users: count each level
3 2 2 3 2 1 2 2 2 2

/ counts the number of elements for each game
```

```q
[List 3.5]

/ 3. Calc average user level each game

avg each level
7.3 3.5 4 4.3 5.5 8 1.5 3 6 5.5
```

```q
[List 3.5]

/ 4. Create boolean list indicating where avg user level > 6

6 < avg each level
1000010000b

/ note - if you put 6 at the end, you get something different
/ so the order of syntax matters!
/ for boolean output, need to number before comparison operator!
```

```q
[List 3.5]

/ 5. Calc games where avg user level > 6

games where 6 < avg each level
`crash`micro

/ note - order of syntax matters!
/ if you did: games where avg each level > 6 -> ERROR
```

```q
[List 3.5]

/ 6. Sum the users for each platform. which one most popular?

sum users where platform in `ps1
sum users where platform in `sega
sum users where platform in `gameboy

/ alternative syntax (i think this makes more sense):

sum users where platform = `ps1
7

sum users where platform = `sega
8

sum users where platform = `gameboy
6
```

```q
[List 3.5]

/ 7. what is the difference between 3 ? 10 and 3 ? 10 20 30

/ atom ? atom
3 ? 10

/ returns 3 random numbers from 0-9

/ atom ? list
3 ? 10 20 30
10 10 30

/ returns 3 random numbers from the list
```

🔵 [List 3.6] List Problem Set 6 (TS 1)
<a name="list_ps6"></a>

```q
[List 3.6]

p: 100 200 300 400 500 600
t: "say hello world to bob"
m: (1 2 3; 10 20 30; 100 200 300)

/ 1. Retrieve the first 3 items from list p

3#p
100 200 300

/ use # take function to retrieve items from list
```

```q
[List 3.6]

/ 2. From t, retrieve the list "sold"

t?"sold"
0 8 6 14

/ find the index position where the character exists

t[0 8 6 14]
"sold"

/ then retrieve it using indexing to return "sold"
```

```q
[List 3.6]

/ 3. Create the nested list ("shoot";"bob") by indexing into t

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
[List 3.6]

/ 4. Change the last number in p to 1000

p[5]: 1000
100 200 300 400 500 1000

/ upsert. find index location 5, replace value with 1000
```

```q
[List 3.6]

/ 5. Find the 3 highest numbers in p

3#desc p
100 500 400

/ take 3 numbers from descending list p
```

```q
[List 3.6]

/ 6. Find values of p that are below the mean

p where p < avg p
100 200 300 400
```

```q
[List 3.6]

/ 7. Given list L and K, find the common numbers in both lists

l: 7 5 13 20 19 17 30 
k: 7 17 200 300 400 1000 

l inter k
7 17

/ inter = finds same values in x inter y
```

```q
[List 3.6]

/ 8. Find the numbers in l that aren't in k

l except k
5 13 20 19 30

/ except = finds values in l that dont exist in k
```

```q
[List 3.6]

/ 9. Combine all elements between l and k without any dupes

l union k
7 5 13 20 19 17 30 200 300 400 1000

/ union = combines all elements btwn 2 lists, no dupes
/ aka only returns distinct elements in both lists
```

```q
[List 3.6]

/ 10. Find the sum of the first 5 numbers in l

l: 7 5 13 20 19 17 30

sum 5#l
64

/ take first 5 numbers from l
/ then sum them together
```

```q
[List 3.6]

/ 11. Find the result when you remove the last 2 items from k

k: 7 17 200 300 400 1000

-2_k
7 17 200 300

/ drop last 2 items from k
```

```q
[List 3.6]

/ 12. Return only numbers in l that are wholly divisible by 5

l: 7 5 13 20 19 17 30 

l mod 5
2 0 3 0 4 2 0

/ returns remainder where l divide by 5
/ 0 means fully divisible

l where not l mod 5
5 20 30

/ you need the NOT because
/ it thinks 0 = false boolean
/ while any positive number = true boolean

/ so while 0 = fully divisible by 5
/ you use "where not" to retrieve where value = 0
```

```q
[List 3.6]

/ 13. Subtract the average of list l from max value in list k

max[k] - avg [l] 
984.14

/ or also:

max k - avg l
9784.14
```

```q
[List 3.6]

/ 14.1 Generate list p of 1000 random integers between 0 and 100.

p: 1000?101

/ this generates a list of 1000 random numbers from 0-100
```

```q
[List 3.6]

/ 14.2 Find all values in p that are square numbers

a: sqrt p

/ a = square root of every number in p
/ a will contain both ints and floats
/ ints = square numbers, while floats = not square numbers

a = `int$a

/ use a comparison operator = to return a list of booleans
/ you are comparing if each element in list a is = a whole number
/ cast every element in list a to an int (whole number)
/ since a is made up ints and floats

p where a=`int$a

/ return value in p WHERE boolean is true from your comparison operator
/ boolean true = whole number = square number

count p where a=`int$a

/ count number of p = square numbers
```


<a name="dictionary"></a>
### 🔴 4. Dictionary
[Top](#top)

🔵 [Dict 4.1] Dictionary Problem Set 1
<a name="dict_ps1"></a>

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

🔵 [Dict 4.2] Dictionary Problem Set 2 - TS 1
<a name="dict_ps2"></a>

```q
[Dict 4.1]

/ 1. given the below dictionary, find the type, the keys, and its values

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
[Dict 4.1]

/ 2. add new entry u 200 to dict d

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
[Dict 4.1]

/ 3. Change value of p to 2

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
[Dict 4.1]

/ 4. Create dictionary d2, by TAKING values of p q r from dictionary d

d2:`p`q`r#d

key|value
---------
p  | 2
q  | 20
r  | 40

/ when TAKE # from dict, output is a dict contains both keys + values
```

```q
[Dict 4.1]

/ 5. Find common keys in d and d2, and retrieve keys + values from combined d+d2

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
[Dict 4.1]

d inter d2
2 20 40

/ dict inter dict will return values occuring in both dicts
/ but you want to return both keys + values, not just values
```

```q
[Dict 4.1]

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

🔵 [Dict 4.3] Dictionary Problem Set 3 - TS 2
<a name="dict_ps3"></a>

```q
[Dict 4.3]

/ 1. Given the 2 dictionaries below, find those who are greater than 1.7m in height

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
[Dict 4.3]

/ 2. Find the average height of people who weight over 90

where dweight > 90
paul peter

dheight where dweight > 90
1.8 1.4

avg dheight where dweight > 90
1.6
```

🔵 [Dict 4.4] Dictionary Problem Set 4 - Nested
<a name="dict_ps4"></a>

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

🔵 [Dict 4.5] Dictionary Problem Set 5 - AQ 1
<a name="dict_ps5"></a>

```q
[Dict 4.5]

/ 1. Given:

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

```q
[Dict 4.5]

/ 2. Extract the hours for tokyo and athens

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

```q
[Dict 4.5]

/ 3. If it's 12:30 in Paris, what time is it in Chicago?

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

```q
[Dict 4.5]

/ 4. Change London's time from 0 to 1

d1[`london]:1
```

```q
[Dict 4.5]

/ 5. Add in rome with value of +1

/ UPSERT method

d1[`rome]:1

/ JOIN ASSIGN method

d1,:(enlist `rome)!enlist 1

/ when using join assign, must enlist if single atom!
```

🔵 [Dict 4.6] Dictionary Problem Set 6 - AQ 2
<a name="dict_ps6"></a>

```q
[Dict 4.6]

/ 1. Given:

d3:`belfast`cardiff`edinburg`london!(12 10 11 9; 11 10 10 10; 10 10 12 9; 15 12)

Key	 | Value
----------------------
belfast	 | 12 10 11 9
cardiff	 | 11 10 10 10
edinburg | 10 10 12 9
london	 | 15 12
```

```q
[Dict 4.6]

/ 2. What's the average temp in each city?

avg each d3

Key	Value
----------------
belfast	 | 10.5
cardiff	 | 10.25
edinburg | 10.25
london	 | 13.5

/ avg each returns average of each key
```

```q
[Dict 4.6]

/ 3. Convert all temp from C to F (temp x 9/5 + 32)

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

```q
[Dict 4.6]

/ 4. Find the max temp for belfast

max d3[`belfast]
12

/ or

max d3`belfast
12

/ calling d3[`belfast] returns values 12 10 11 9
/ so max of this is 12
```

```q
[Dict 4.6]

/ 5. Given new dict d4, find max temp for belfast

d4:(enlist `temperature)!enlist d3

max d4[`temperature;`belfast]

/ so d4 is a dict within a dict
/ first column = temperature
/ 2nd column is the entire dict of 3
```

```q
[Dict 4.6]

/ 6. Add a row to d4:

d4,:(enlist`rainfall)!enlist`belfast`cardiff`edinburgh`london!60 65 58 40

```

🔵 [Dict 4.7] Dictionary Problem Set 7 - AQ 3
<a name="dict_ps7"></a>

```q
[Dict 4.7]

/ 1. Create dictionary with keys as letters from a-z with corresponding numbers

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
[Dict 4.7]

/ 2. Retrieve values of abc 

dict "abc"
1 2 3

/ or

dict ["abc"]
1 2 3

/ abc = keys, to retrieve values, use indexing
/ the key values are chars, so need to use parathesis to retrieve
```

```q
[Dict 4.7]

/ 3. Sum values of abc

sum dict "abc"
6
```

```q
[Dict 4.7]

/ 4. Sum values of "yourname"

sum dict "yourname"
112
```

```q
[Dict 4.7]

/ 5. Rename keys to capital letters

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
[Dict 4.7]

/ 6. Create another dict, change uppercase "HELLO WORLD" to lowercase

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
[Dict 4.7]

/ 7. Create dictionary morse, which contains letters n-s as keys, and a code for the values

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
[Dict 4.7]

/ 8. Join numbers 0 to 4 onto the existing dictionary

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

🔵 [Dict 4.8] Dictionary Problem Set 8
<a name="dict_ps8"></a>

```q
[Dict 4.8]

/ 1. Create 2 dictionaries, one for r13, one for r12

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
[Dict 4.8]

/ 2. Extract keys from first dictionary
key d1

/ 3. Extract values from first dictionary
value d1
```

```q
[Dict 4.8]

/ 4. Create new dict with sum of annual rainful over both years

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
[Dict 4.8]

/ 5. Find the average rainfall over the two years for each city

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
[Dict 4.8]

/ 6. Which location had more rainfall over the 2 years?

d1 > d2

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
[Dict 4.8]

/ 7. Find the average rainfall over the 2 years for the UK

sum(d1+d2) % 2
6170.5

/ d1+d1 will simply add each row together
/ the sum will aggregate all values together into 1 single value
```

```q
[Dict 4.8]

/ 8. Create a dict of variables in the workspace as keys, and values as values

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

<hr>

<a name="tables"></a>
### 🔴 5. Tables
[Top](#top)

🔵 [Table 5.1] Table Problem Set 1 - Easy
<a name="table_PS1"></a>

```q
t:([] company:`ford`bmw; employees:300 100)
t

company | employees
-------------------
ford    |   300
bmw     |   100
```

```q
/ 1. What datatype is table t?

type t
98h

/ 98h is a table
```

```q
/ 2. how many rows are in table t?

count t
2


/ counts how many rows in table
```

```q
/ 3. Retrieve a list of columns for table t

cols t
`company`employees
```

```q
/ 4. Check datatypes and any foreign key restrictions

meta t

c         | t |	f | a
----------------------
company	  | s |	  |	
employees | j |	  |	
```

```q
/ 5. Sort column employee in ascending order

`employees xasc t

company | employees
-------------------
bmw     |   100
ford    |   300

/ sorts employees in ascending order
```

🔵 [Table 5.2] Table Problem Set 2 - Easy
<a name="table_PS2"></a>

```q
/ 1. Create an empty table with the following columns/datatypes:
/ sym (sym)
/ side (char)
/ size (int)
/ price (float)

t: ([] sym:`$(); side: `char$(); size:`int$();price:`float$())

sym | side | size | price
--------------------------

/ notice to cast sym datatype is simply a backtick `
```

```q
/ 2. Add `IBM, "B", 10i, 100f to table (using JOIN ASSIGN)

t,:(`IBM;"B";10i; 100f)

sym | side | size | price
--------------------------
IBM | B    | 10   | 100

/ use join assign (,:) to add single row to table
/ must use correct datatypes
/ JOIN ASSIGN can ignore column header
/ DON'T need to backtick table t
/ auto saves to table t
```

```q
/ 3.  Insert `IBM, "B", 10I, 100f to table t (using INSERT)

`t insert(`IBM;"B";10i;100f)

/ NEED to backtick table otherwise wont work!
/ INSERT don't need headers
/ don't need enlist
/ note datatypes must still match
```

```q
/ 4. Upsert `GOOG; "B"; 30i; 300f to table t (using UPSERT)

`t upsert (`GOOG;"B"; 30i; 300f)

/ same syntax as INSERT
/ notice you don't need to use enlist
/ don't need column headers
/ UPSERT doesn't REQUIRE backtick table, but wont save
/ to save, still need to backtick `table
```

```q
/ 5. Insert the following rows to table t (using INSERT)
/ `IBM`MSFT`AAPL
/ "B" "S" "B"
/ 10i 20i 30i
/ 100f 200f 300f

`t insert(`IBM`MSFT`AAPL; "B","S","B"; 10i, 20i, 30i; 100f, 200f, 300f)

sym  | side | size | price
-------------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0

/ NEED to backtick table otherwise wont work!
/ INSERT don't need headers
/ must use correct datatype!
/ ints have to be separated by commas
/ floats have to be separated by commas
```

```q
/ 6. Upsert the following rows to table t (using UPSERT)
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

/ to UPSERT multiple rows, have to upsert a TABLE 
/ MUST include column names
/ must have commas between ints and floats!
/ UPSERT requires table to have backtick
```

🔵 [Table 5.3] Table Problem Set 3 - Easy
<a name="table_PS3"></a>

```q
/ 1. Create empty table cars with brand = sym, model = sym, and date = date

cars:([] brand:`$(); model:`$(); date:`date$())
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
/ need BACKTICK table though
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
/ need backtick table
```

```q
/4. Upsert Single Row of bmw, 505, 2021.11.13

`cars upsert(`bmw;`505;2021.11.13)

brand| model| date
------------------------
bmw  | 505  | 2021-11-13

/ UPSERT has same syntax as INSERT
/ note - you cannot upsert multiple rows; have to upsert a dictionary
/ need backtick table
```

```
/ 5. Insert multiple rows into table t
/ `ferrari`benz
/ `F50`s500
/ 2021.11.13 2021.11.13

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

```q
/ 6. Show alternative syntax to insert multiple rows in table

insert[`cars;(`ferrari`benz;`F500`S500;2021.11.13 2021.11.13)]

brand  | model| date
------------------------
bmw    | 505  | 2021-11-13
audi   | s4   | 2021-11-13
ferrari| F50  | 2021-11-13
benz   | S500 | 2021-11-13
```

```q
/ 7. How do you UPSERT multiple rows into table?

/ you cannot upsert multiple rows into a table
/ instead must upsert a dictionary
```

```q
given table t:

t:([] fruit:`apple`orange; price: 11 23; quantity:100 200)

fruit  | price | quantity
--------------------------
apple  |  11   |   100
orange |  23   |   200
```

```q
/ 7. Upsert pear, banana, 20 30 into t

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
🔵 [Table 5.4] Table Problem Set 4 - Easy
<a name="table_PS4"></a>

```q
/ 1. What is the difference between xcol and xcols?

/ xcol is used to rename table columns
/ xcols is used to rearrange table columns
```

```q
/ given table t:

t: ( [] company: `ford`bmw; employee: 300 100)

company | employee
------------------
ford    |   300
bmw     |   100
```

```q
/ 2. Rename company to a and employee to b

`a`b xcol t

a   | b
---------
ford| 300
bmw | 100

/ renames first 2 columns from company/employee to a/b
/ xcol will only change col names from left to right
/ have to use backtick + new col name
```

```q
/ 3. Rearrange columns in t to employees, company

`employees`company xcols t

employee | company
------------------
300      |  ford 
100      |  bmw  

/ reorders columns
/ doesn't have to be complete list of columns
/ just moves it to left of table
```

🔵 [Table 5.5] Table Problem Set 5 (Union, Except, Inter) - Easy
<a name="table_PS5"></a>

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

```q
/ 1. UNION TABLE = merges 2 tables together, but does NOT dupe values!

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

```q
/ 2. EXCEPT TABLE = only returns values in left table NOT in right table

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

```q
/ 3. INTER TABLE = only returns common elements in both t and u (inner join) 

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

🔵 [Table 5.6] Table Problem Set 6 (Table Joins) - Easy
<a name="table_PS6"></a>

```q
/ 1. Start with empty table t with cols company and employees

t:([] company:(); employees:())
company | employee
------------------
	| 

/ empty table t
```

```q
/ 2. Add the following into table t
/ `bmw`soda
/ 200 300

t: t, ([] company:`bmw`skoda; employees:200 300)

company | employee
------------------
bmw	| 200
benz	| 300

/ joins empty table t with new table
/ essentially you are joining a table into table
```

```q
/ 3. Given t1 and t2 with same column headers,
/ join the two tables together keeping the same schema

/ if 2 tables columns MATCH, can JOIN to ADD ROW
/ called vertical joins

t1:([] sym: `IBM`AAPL; side:`buy`sell; price: 10 20; size: 100 200)
t2:([] sym:`GOOG`MSFT; side:`buy`sell; price: 30 40; size: 300 400)

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

```q
/ 4. Given tables t1 and t2 below, join the two tables together
/ note: tables have different columns

t1:( [] sym: `IBM`AAPL`GOOG; ex: `nyse`nyse`nasdaq)
t2:( [] price:10 20 30; size: 100 200 300)

t1
sym  | ex
-------------
IBM  | nyse
AAPL | nyse
GOOG | nasdaq

t2
price | size
-------------
10   | 100
20   | 200
30   | 300
```
```q
/ reminder - if 2 tables have same no of rows
/ and NO matching columns
/ can join tables together using each both ,' 

t1,'t2

sym  |  ex    | price | size
----------------------------
IBM  | nyse   |  10   | 100
AAPL | nyse   |  20   | 200
GOOG | nasdaq |  30   | 300

/ use ,' each both adverb to combine tables together
/ t1 and t2 have diff column names
/ but same number of rows
```
🔵 [Table 5.7] Table Problem Set 7 (TS 1) - Easy
<a name="table_PS7"></a>

```q
Given:
stock: ( [] sym: `MS`C`AAPL; sector:`Financial`Financial`Tech; employees: 100 100 100)

sym  | sector    | employees
-----------------------------
MS   | Financial | 100
C    | Financial | 100
AAPL | Tech      | 100
```

```q
/ 1. Extract the employees numbers (without the header)

stock`employees
100 100 100

/ syntax is table`column name
/ retrieves values as a list

/ alternative syntax:

stock.employees
stock[`employees]
stock [ ; `employees]
```

```q
/ 2. Key the first column in stock table

1!stock

`sym` |sector    |employees
-------------------------
`MS`  |Financial |100
`C`   |Financial |100
`AAPL`|Tech      |100

/ syntax is 1 ! table name
```

```q
/ 3. Display only the first and second rows of the stock table
/ use TAKE # method

2#stock

sym |sector    |employees
-------------------------
MS  |Financial |100
C   |Financial |100

/ # take retrieves rows from table

/ alternative solution:

stock [0 1]

/ uses index retrieve method
/ returns index position 0 and 1 (first 2 rows)
```

```q
/ 4. Select the last row of stock table as a dictionary

last stock

key       | value
-----------------
sym       | AAPL
sector    | Tech
employees | 100

/ LAST will retrieve the last row from table stock
/ and return it as a dictionary
```

```q
/ 5. Insert GOOG in the tech sector with 100 employees (using insert)

`stock insert(`GOOG; `Tech; 100)

sym  | sector    | employees
----------------------------
MS   | Financial | 100
C    | Financial | 100
AAPL | Tech      | 100
GOOG | Tech      | 100

/ remember need to backtick `stock (otherwise error)

/ alternative solution:

insert [`stock; ([] sym: enlist `GOOG; sector: enlist `tech; employees: enlist 100)]

sym  | sector    | employees
----------------------------
MS   | Financial | 100
C    | Financial | 100
AAPL | Tech      | 100
GOOG | Tech      | 100

/ syntax is insert + [table name; table with corresponding columns]
/ must use enlist when adding single row!!
```
🔵 [Table 5.8] Table Problem Set 8 (TS 2) - Easy
<a name="table_PS8"></a>

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

```q
/ 1. Find the average height of the bosses, the employees, and both the bosses and employees

avg boss[`height]
avg boss`height

182.667

avg employees [`height]
avg boss`height

170f

avg (boss,employees)[`height]
176.33

/ first JOIN boss and employees tables together
/ index retrieve values from the height column
/ then find average
```

```q
/ 2. Find the 2 tallest employees

2 # `height xdesc employees

name | height
-------------
jim  | 180
john | 170

/ first sort employees table by height (xdesc)
/ syntax is column_name xdesc table_name
/ then you take the first 2 rows 
```
🔵 [Table 5.9] Table Problem Set 9 (TS 3) - Easy
<a name="table_PS9"></a>

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

```q
/ 1. Insert the following rows into trade table

dt         | sym  | price | size
--------------------------------
2021-11-01 | JPM  |   1   | 100
2021-11-02 | UBS  |   2   | 200

/ since the values you insert HAS to match the datatype of table trade
/ meta helps you know what each column datatype is

meta trade

c	t f a
---------------
dt	d		
sym	s		
price	j		
size	j		

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

```q
/ alternative syntax 1
/ insert table method

`trade insert( [] dt:2021.11.01+1 ; sym:`JPM`UBS; price:1 2; size: 100 200) 

/ insert table method requires column header names
/ still needs backtick table
```

```q
/ alternative syntax 2

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
/ requires column headers
```

```q
/ 2. Insert the following record into stock

sym | sector | employees
-------------------------
FB  |  Tech  | 100

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

```q
/ 3. In the stock table, change the number of employees for C to 300

stock upsert (`C;`Fin;300)

/ to update table values, use UPSERT
/ don't need backtick on table name
```

```q
/ alternative syntax 1

stock upsert ([sym: enlist`C] employees: enlist 300)

sym|sector|employees
--------------------
C  |Fin   |300

/ have to use enlist to create a vector for an atom
/ note this requires header
```

```q
/ 4. Sort the stock table by sym

`sym xasc `stock

sym | sector| employees
--------------------
AAPL| Tech  | 100
C   | Fin   | 100
MS  | Fin   | 100

/ `column name + xasc + `table name
```
🔵 [Table 5.10] Table Problem Set 10 (AQ 1) - Easy
<a name="table_PS10"></a>

```q
/ 1. Create 3 lists called a, b, c with 4 elements each

a: 1 2 3 4
b: `a`b`c`d
c: 100 200 300 400
```

```q
/ 2. Create a table using these 3 lists

t:( [] a; b; c)

a b c
--------
1 a 100
2 b 200
3 c 300
4 d 400

/ you can simply create a table using lists 
/ which are vectors of equal length
```

```q
/ 3. Create a dictionary using this table
 
flip t

key|value
-----------------
a  | 1 2 3 4
b  | `a`b`c`d
c  | 100 200 300 400

/ a table is just a flipped dictionary
/ so you can flip a table back into a dictionary
```

```q
/ 4. Create empty table sym (sym), side (char), size (int), price (float)

trade:( [] sym:`$(); side:`char$(); size:`int$(); price:`float$())

sym | side | size | price

/ created empty table trade
/ to cast datatype sym use backtick `
```

```q
/ 5. Create another table, lasttrade, which is a copy of trade, but sym is keyed

lasttrade: 1!trade

`sym` | side | size | price

/ created empty table lasttrade, with keyed sym column
```

```q
/ 6. Is there a difference in the metadata between 2 tables?

meta trade ~ meta lasttrade
1b (true)

/ no difference when you key columns
/ meta queries TYPE, foreign key, attributes
```

```q
/ 7. Is there a difference in type?

type trade ~ type lasttrade
0b (false)

/ once you KEY a table, the TYPE becomes a dictionary
/ so YES, the metadata will change once you key

/ trade = 98h = table
/ lasttrade = 99 = dict (since you keyed)
```
🔵 [Table 5.11] Table Problem Set 11 (AQ 2) - Easy
<a name="table_PS11"></a>

```q
/ 1. use 3 join commands to add rows to trade 
/ sym: IBM, MSFT, AAPL
/ side: "B" or "S"
/ size: 10i 20i 30i
/ price: 100f 200f 300f

trade
sym | side | size | price
-------------------------
    |      |      |

trade,:(`IBM;"B";10i; 100f)
trade,:(`MSFT;"S";20i;200f)
trade,:(`APPL,"B";30i;300f)

/ JOIN ASSIGN ,: dont need columns
/ values separated by semi colon ;
/ don't need backtick trade table
/ need to specify datatype since the table was assigned datatypes earlier
```

```q
/ 2. Use a single join command to add 3 more rows into join

/ Method 1: simply build a table

trade:([] sym:`IBM`MSFT`AAPL;side:"B","S","B";size: 10 20 30; price: 100 200 300)

sym  | side | size | price
---------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0
```

```q
/ Method 2 - INSERT multiple rows

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

```q
/ 3. Method 3 - UPSERT multiple rows

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
 
```q
/ 4. Fill lasttrade with data from trade

lasttrade:trade

sym  | side | size | price
--------------------------
IBM  | B    | 10   | 100.0
MSFT | S    | 20   | 200.0
AAPL | B    | 30   | 300.0

/ you can simply "assign" table lasttrade to trade
```

```q
/ alternative syntax:

lasttrade,'trade

/ this joins the 2 tables together
```
🔵 [Table 5.12] Table Problem Set 12 (AQ 3) - Easy
<a name="table_PS12"></a>

```q
/ 1. Create the following table

stock:([] item:`soda`bacon`mush`eggs;brand:`fry`pork`veg`veg;price:1.5 1.99 0.88 1.55; order:50 82 45 92)

item  | brand| price | order
----------------------------
soda  | fry  | 1.5   | 50
bacon | pork | 1.99  | 82
mush  | veg  | 0.88  | 45
eggs  | veg  | 1.55  | 92
```

```q
/ 2. Add row of tomato, veg, 1.35 70

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

```q
/ alternative syntax: 
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

```q
/ 3. Key the table according to item and brand

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

```q
/ alternative syntax:
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

```q
/ 4. Does the meta data change when you key/unkey tables?

(meta stock) ~ (meta (2!stock))
1b

/ true, the 2 tables match
/ so no, changing keys does not affect a tables meta
```
🔵 [Table 5.13] Table Problem Set 13 (AQ 4) - Easy
<a name="table_PS13"></a>

```q
/ given table called trader

trader:([]item:`soda`bacon`mush`eggs`tomato;brand:`fry`pork`veg`veg`veg;price:1.5 1.99 0.88 1.55 1.35; order:200 180 110 210 100)

item   | brand| price| order
----------------------------
soda   | fry  | 1.5  | 200
bacon  | pork | 1.99 | 180
mush   | veg  | 0.88 | 110
eggs   | veg  | 1.55 | 210
tomato | veg  | 1.35 | 100
```

```q
/ 1. Create new table, totalorders, which has sum of both orders from traders
/ also, drop the price column before adding together

totalorders:(2!(enlist `price)_stock) + (2!(enlist `price)_trader)

item   | brand| order
----------------------
soda   | fry  | 250
bacon  | pork | 262
mush   | veg  | 155
eggs   | veg  | 302
tomato | veg  | 170

/ to add 2 tables together, need to first key them
/ since they want you to drop the price column before adding
/ need to 1) unkey orig table, 2) drop price column (using enlist)
/ 3) re-key the table, then add the tables together
```

```q
/ 2. Create new list called newprices, which is 75% of stock's price

newprices:0.75 * stock`price
1.125 1.4925 0.66 1.1625 1.0125

/ need to first make sure stock is unkeyed
/ table`column = retrieves column values a list
```

```q
/ 3. Join newprices to the totalorders table
/ essentially you are joining a list to a table

totalorders: totalorders,' ( [] newprices)

item   |brand |order | newprices
--------------------------------
soda   | fry  | 250  | 1.1250
bacon  | pork |	262  | 1.4925
mush   | veg  |	155  |   0.66
eggs   | veg  |	302  | 1.1625
tomato | veg  |	170  | 1.0125

/ so ([] newprices) turns the list into a table
/ then use adverb "each both" ,` to join the list to table
/ only works if number of rows line up

/ something interesting is that ,` is only performed in place
/ so it doesnt "save" to the underlying table
/ hence need to assign new table to save the changes
```

```q
/ alternative solution:
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

```q
/ 4. With the 75% discount, how much savings per week will the stock and trader have?

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

```
/ alternative syntax:
/ QSQL method (honestly, easier)

stock:update savings: price*order*0.25 from stock

/ have to reassign table as stock for the updated column to save!

item  | brand | price | order | savings
---------------------------------------
soda  | fry   | 1.5   | 50    | 18.75
bacon | pork  | 1.99  | 82    | 40.795
mush  | veg   | 0.88  | 45    | 9.9
eggs  | veg   | 1.55  | 92    | 35.65
tomato| veg   | 1.35  | 70    | 23.624

select sum savings from stock
128.72

/ can perform operations on entire columns
/ so much cleaner!
```
🔵 [Table 5.14] Table Problem Set 14 (GS 1) - Med
<a name="table_PS14"></a>

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
🔵 [Table 5.15] Table Problem Set 15 (GS 2) - Med
<a name="table_PS15"></a>

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

🔵 [Func 8.1] Intro to Functions
<a name="func_intro"></a>
[Top](#top)

```q
/ 1. What is a lambda expression?

/ a lambda expression is an anonymous function
```

```q
/ 2. What are local variables?

/ a variable that is created and exist only for the duration of an application
```

```q
/ 3. What is function prefix syntax?

/ a unary function is a function with only one parameter
/ when you separate the function from its argument , this is called a prefix syntax

{x*x} 5
25

/ in this case, 5 is an implicit variable
```

🔵 [Func 8.2] Functions on Strings - AQ
<a name="func_strings"></a>
[Top](#top)

```q
/ 1. Convert string [welcome] to [welcoME]

/ create a function that uses SSR (string search replace)

/ quick reminder on SSR

ssr["hello ryan where is ryan";"ryan";"john"]
hello johhn where is john
```

```q
ssr["welcome";"me";"ME"]
"welcoME"
```

```q
/ 2. Create a function to perform SSR on the above

/ func accepts strings "welcome"
/ and outputs "welcoME"

f:{ssr[x;y;z]}
f["welcome";"me";"ME"]
"welcoME"

/ just wrap SSR into a function
/ x = original string
/ y = target
/ z = replacement 

/ note - inputs have to be strings!
```

```q
/ 3. Create an SSR function that accepts syms and outputs strings 

/ func accepts syms
/ and outputs strings
/ using same example above

f: {ssr[(string x);y;z] }
f[`welcome;"me";"ME"]
"welcoME"

/ x = input is a sym 
/ first x gets cast from `sym to string
/ then SSR is run on string "welcome"
/ and replaces "me" with "ME"
```

```q
/ 4. re-write above function as lambda function

/ and call the func on the same line

{ssr[string x;y;z]} [`welcome; "me";"ME"]
"welcoME"

/ did not define function (lambda)
/ uses implicit arguments x, y, z
/ passes arguments immediately after function
/ string x = ONLY applies to argument x
```

```q
/ Alternative method to call arguments on lambda function

/ alternative syntax (lambda + alt method to call argument)

{ssr[string x;y;z]} [ ; "me";"ME"] `welcome
"welcoME"

/ so sym `welcome is implicit argument x
/ since arguments y and z are already defined as "me" and "ME"
/ this is useful when iterating through a LIST of syms
```

```q
/ 5. re-write function to pass a LIST of syms as its arg

/ instead of converting one sym
/ need to iterate function through LIST of syms
/ `welcome`home`mermaid

f:{ssr [string x;y;z]} 
f[ ;"me";"ME"] each `welcome`home`mermaid
"welcoME"
"hoME"
"MErmaid"

/ function remains the same
/ but to iterate through a LIST, need adverb [EACH]
/ the LIST of syms [`welcome`home`mermaid] gets passed through x
/ this REQUIRES x to be left blank inside [ ] 
/ while locking in arguments y and z as constants
```

```q
/ 6. re-write above as lambda function + call list of syms

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

🔵 [Func 8.3] Projected Functions - TS
<a name="func_proj"></a>
[Top](#top)

```q
/ 1. Create function [raise], that takes x to the y

/ and raise 10 to the 2, 3 and 4

raise: {x xexp y}
raise [10; 2 3 4]
100 1000 1000f
 
/ x = 10 
/ y = 2 3 4
```

```q
/ 2. Create func called [g], which projects func [raise]

/ func g keeps x constant @ 10
/ but accepts args to raise power to 1 2 3

/ from earlier:
raise:{x xexp y}

g: raise [10; ]
g 1 2 3
10 100 1000

/ you've already created function [raise] previously
/ so g is a PROJECTION of the original function RAISE
/ g calls function raise, but keeps x constant @ 10
/ y becomes arguments you call in (1 2 3)
/ notice g is simply an ASSIGNMENT 
/ not a function, so dont need { }
```

```q
/ 3. Create func [square], which projects func [raise]

/ new func will square arguments passed through x

/ from earlier:
raise:{x xexp y}

square: raise[ ;2]
square 1 2 3
1 4 9

/ func [square] leaves first argument blank (x)
/ and keeps second argument constant @ 2
/ calls in 1 2 3 as argument x
```

🔵 [Func 8.4] Function Loop Problem Set - TS 
<a name="func_loop"></a>
[Top](#top)

```q
/ 1. using a LOOP, create a func that generates a list of 100 random numbers from 0-99, and sums all values from list thats greater than 50

/ reminder:
/ WHILE LOOPS -> if [first cond] is TRUE, execute all arguments that follow
/ IF STATEMENT -> if [first cond] TRUE, execute [FIRST ARG]. Else, execute [LAST ARG].

/ thought process:
/ first, generate list of 100 random numbers
/ then, iterate through each num, if > 50, add to placeholder list
/ for WHILE loops, you always need some form of [ITERATIVE COUNTER]
/ also need an empty [PLACEHOLDER LIST] for your results
```

```q
/ solution

d: 100?100
i: 0
r1: 0

while [i < count d; if [d[i]>50; r1+:d[i] ]; i+:1] r1
3356

/ d = list of 100 random numbers from 0-99
/ i = iterative counter (goes from 0-99). Counts through every element of list d
/ r1 = result of while loop

/ while i is less than total number of items in list d (100)
/ if value of [list d] at [index position i] is greater than 50
/ add this value, d[i], to results list [r1]
/ then go onto next iteration (i+1)

/ if d[i] is NOT greater than 50, then do nothing, and move onto next iteration
/ keep going until counter [i] goes through entire list of 100

/ remember, WHILE LOOPS -> if first argument is TRUE, execute all arguments that follow
/ WHILE LOOP = used as iterative counter through all elements of list d (0-99)
/ IF STATEMENT = tests IF condition true, add to list
```

```
/ 2.Re-write the above function as a Vector Solution (NO LOOPS)

d: 100?100

sum d where d > 50

/ look at how easy that is!
/ so use vector operations whenever possible
```

```q
/ vector operations also a lot more flexible:

max sum d where d>50
min sum d where d>50
avg sum d where d>50
```

🔵 [Func 8.5] Prime Numbers Problem Set - TS
<a name="func_prime"></a>
[Top](#top)

```q
/ 1. Create func that checks if argument x is prime or not

/ call this func: [isPrime]
/ accepts 1 argument input
/ and checks whether argument is Prime (True) or not (False)

/ prime = any num can only % by itself and 1
/ prime numbers begin on 2
/ will need 3 components:
/ 1. number < 2 (not prime)
/ 2. number = 2 (prime)
/ 3. number > 2 (could be prime)

/ the outcomes for component 1 and 2 are quite binary. 
/ component 3 -> requires you to check if [arg x] has any factors
/ which means dividing by every number up to [arg x]

/ general reminder:
/ IF brackets [contain condition + statement to execute if true]
/ WHILE brackets [contain condition + statement to execute if true]
```

```q
/ solution:

/ x = arg input number
/ a = iterator (check every number up to x number)

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
/ if while condition [a < x] is FALSE
/ skip ENTIRE while loop
/ and go straight to the end, return TRUE 1B (prime)
/ if x = 2
/ x(2) < a(2) = FALSE. Skip entire while loop
/ goes to end, returns 1b (True)

Component 3 (number > 3)
/ if while condition [a < x] is TRUE (iterator < x number)
/ check if [a] is a [factor] of x number
/ this check is done by x mod a = 0
/ if TRUE, return false :0b (since even number/factor exists = NOT PRIME)
/ otherwise, iterate through until WHILE condition (a<i) until no longer true

/ if x = 5
/ a(2) < x(5) = TRUE
/ x(5) mod a(2) = 0 = FALSE = skips :0b
/ a:a+1 so 2 + 1 = 3

/ a(3) < x(5) = TRUE
/ x(5) mod a(3) = 0 = FALSE = skips :0b
/ a:a+1 so 3+1 = 4

/ a(4) < x(5) = TRUE
/ x(5) mod a(4) = 0 = FALSE = skips :0b
/ a:a+1 so 4+1 = 5

/ a(5) < x(5) = FALSE, SKIPS entire while loop
/ goes to end, returns 1b (True) 
```

```q
/ 2. Using your [isprime] func, create another func that returns every prime number up to argument x

/ call this func [findprime]

/ since you are returning a [LIST] of numbers
/ will require an 1) empty list
/ and 2) an iterator to check every number up to x

/ iterator starts from 1
/ if iterator is prime, append to list r (need to use ,: NOT sum)
/ then go onto next number
/ keep checking until WHILE condition is no longer true (a<n)
/ then return list r
```

```q
/ solution

/ n = input arg number
/ r() = empty list thats gonna contain our result
/ a = iterator that checks every num up to arg n

findprime: {[n] r:(); a:1; while [a<n; if[isprime[a];r,:a]; a:a+1];r}
findprime 10 
2 3 5 7

/ a starts from 1 (iterator)
/ while your iterator (a) is less than input number (n),
/ feed iterator (a) into func [isprime]
/ and if (a) is prime, append to list r (r,:a = append a to list r)
/ then move onto next iterative cout (a+:1)
/ keep going until you check every number 
/ then return list r
```

```q
/ detailed logic for input

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
/ 3. Re-write [isprime] function using vector based solution (no loops!)

/ original [isprime] function
/ func check is arg x is prime or not
/ simply outputs true or false

isprime:{if[x<2; :0b]; a:2; while[a<x; if[(x mod a)=0; :0b]; a+:1]; 1b}
```

```q
/ we can rewrite the [while loop] portion
/ instead of looping through every iteration of argument x 
```

```q
/ 3.1 start by using til to generate a list

{til x} 10
0 1 2 3 4 5 6 7 8 9
```

```q
/ 3.2 remove first 2 elements (since not prime)

{2_ til x} 10
2 3 4 5 6 7 8 9

/ drops 0, 1 since not prime
```

```q
/ 3.3 check each number if it is a factor of argument x (10)

{x mod 2_ til x} 10
0 1 2 0 4 3 2 1 0

/ 10 mod 2 = 0
/ 10 mod 3 = 1
/ 10 mod 4 = 2
/ 0 means no remainder = factor of x = NOT PRIME
```

```q
/ 3.4 show us factors of argument x

{0 = x mod 2_ til x} 10
100100001b

/ shows us factors of argument 10
/ 1 = true
/ 0 = false
```

```q
/ 3.5 check if there are ANY factors of 10? (mod = 0)

{any 0 = x mod 2_ til x} 10
1b

/ TRUE, because list contains SOME factors of 10
```

```q
/ 3.6 does the list NOT contain any factors of 10?

{not any 0 = x mod 2_ til x} 10
0b

/ FALSE, because list DOES contain factors of 10
/ hence, NOT prime
```

```q
/ 3.7 plug this back into your original function 
/ still need component for numbers less than 2
/ so re-use the x<2 IF/Else clause

isprimeB: {if[x<2; :0b]; not any 0=x mod 2_til x}
isprimeB 10
0b

/ x(10)<2 = FALSE, skips if statement
/ goes onto second statement
/ FALSE, 10 is NOT prime
```

```q
/ 4. re-write [findprimes] function using vector based solution

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

🔵 [Func 8.6] Function Problem Set 1 - TS
<a name="func_set1TS"></a>
[Top](#top)

```q
/ 1. Create func called volc that accepts 2 arguments (r and h)
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

```q
/ 2. Create function, called sph, that accepts argument radius
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

```q
/ 3. Create function, setc, that takes 1 implicit argument
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

```q
/ 4. raise:{x xexp y}
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

```q
/ 5. Convert all elements of list l to a string

l: (100;`price;1b)

string l
"100"
"price"
"1b"

/ l is a list of long, sym, and boolean
/ simply using the "string" function, converts all elements to strings
/ mixed lists have to be contained in parathesis ( )
```

```q
/ 6. Given string st, replace "cow" with "kangaroo"

/ st: "the cow jumped over the moon"

st: "the cow jumped over the moon"
ssr [st; "cow";"kangaroo"]
"the kangaroo jumped over the moon"

/ ssr = string search replace.
/ first condition = string
/ second condition = what to target
/ third condition = what to replace with
```

```q
/ 7. Create function that takes [name;age] and returns "hello age year old name"

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

```q
/ 8. I have a box of 7 eggs, and the weights are
/ eggs: 10 20 30 40 50 60 70
/ find the median and average weight of these eggs

med eggs
40f

avg eggs
40f

/ note, division will always return a float
/ apparently same with med and avg functions
```

```q
/ 9. I sold 2 boxes of eggs
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

```
/ 10. Generate list k with 10 random ints
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

```q

/ 11. Create function factw, which uses a loop to write a factorial function
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

```q
/ 12. re-write the factorial function as factp WITHOUT using loops
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

```q
/ 13. Demonstrate which calculation is faster,
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

```q
/ 14. Create function called safefact
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

```q
/ 15. Write a function called isPalindrome 
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

```q
/ 16. Find the sum of all multiples of 3 or 5 below 1000
/ check every number up to 1000
/ if its a factor of 3 or 5
/ x mod 3 = 0
/ x mod 5 = 0

/ 1. generate list of ints from 0-999

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

🔵 [Func 8.7] Functions Problem Set 1 (easy) - AQ
<a name="func_set1AQ"></a>
[Top](#top)

```q
/ 1. Write function f that calculates the square of a number

f:{[a] a*a}
```

```q
/ 2. Write new funciton g, which takes square of first argument divided by square of second argument

g: {(x*x) % (y*y)}
g [2;4]
0.25
```

```q
/ 3. Execute g with arguments a and b, store this to c

c: g[a;b] 

```

```q
/ 4. Create dyadic function f1 indicating whether the product of 2 numbers is greater than sum

/ dyadic means 2 arguments

f1: {(x*y) > x+y}
```

```q
/ 5. write this func with proper KDB order of operations g1: x^5-3x^2 + 5
/ then call the function when x=4

g1:{((x xexp 5) - 3*(x xexp 2))+5}
g1[4]
981f

/ note - you have to put 3*(x xexp 2)
/ an int next to parenthesis won't automatically mutiply
```

```q
/ 6. Create function that calculates area of triangle
/ then call func with arguments height = 7, base = 10

t:{x * y % 2 }
t [7;10]
35
```

```q
/ 7. Create function that calculates the sum of 2 squares of a number x

f: {x xexp 2 + x xexp 2}
f: {(x*x) + x*x}
```

```q
/ 8. Create a function that calculates a^3+b^2+c
/ then call your function with arguments: 13,3,6

f:{(x xexp 3) + (y xexp 2) + z}
f [13;3;6]
2212

/ have to use parathensis ( ) around xexp
```

```q
/ 9. BMI is weight divide by height squared. create an implicit formula

bmi: { x % (y*y) }
```

```q
/ 10. Create a func called perimeters, which will take perimeter of a square and return its area

perimeter:{ (x%4) xexp 2}
perimeter[8]
4
```

```q
/ 11. Car Depreciation Problem

/ a car depreciates 15% every year for the first 3 years
/ then 8% every year for the next 3 years
/ create func k to find value after 6 years
/ with original value 15000

k: {x*(0.85 xexp 3)*(0.92 xexp 3) }
k [15000]
7173.1765
```

🔵 [Func 8.8] Functions Problem Set 2 (med) - AQ
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

```q
/ 1. Create function with 3 arguments (symbols, startdate, enddate)

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

```q
/ 2. Extracting temporal data from Timestamp

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

```q
/ 3. Extract the TIMESTAMP from timestamp

select time from depth

time
--------------------------
2021-11-07T08:04:21.425000
2021-11-07T08:14:59.215000
2021-11-07T08:21:30.944000

/ since time is already of timestamp datatype, just need to extract
```

```q
/ 4. Extract the DATE from timestamp

select `date$time from depth

time
----------
2021-11-07
2021-11-07
2021-11-07

/ extract time, then cast timestamp to date datatype
```

```q
/ 5. Extract the TIME from timestamp

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

```q
/ 6. Create tradeticks2 with additional parameters: starttime and endtime

/ this func will only extract the trades that fall within time range
/ original equation's parameters = sym, startdate, enddate
/ hint - need to extract the TIME portion from timestamp 
/ for whatever reason, only [time.time] works
/ if you try casting as [`time$time], it oddly doesnt work

tradeticks2:{ [symbols; startdate; enddate; starttime; endtime] 
              select from trades where 
	      date within (startdate;enddate), 
	      sym in symbols,
              time.time within (starttime;endtime) }

tradeticks2[`AAPL; 2014.04.20; 2014.04.21; 08:00:00; 08:31:00]

date	   | sym  | time
-----------------------------------------------
2014-04-21 | AAPL | 2014-04-21T08:00:39.491000
2014-04-21 | AAPL | 2014-04-21T08:14:36.412000
2014-04-21 | AAPL | 2014-04-21T08:20:09.827000
2014-04-21 | AAPL | 2014-04-21T08:20:16.896000
2014-04-21 | AAPL | 2014-04-21T08:20:45.539000

/ [time column] from trades is in the timestamp format of 2021.01.01D09:00:00
/ need to extract only the time portion by CASTING as time
/ such that it matches your arguments for starttime and endtime
```

```q
/ 7. Create tradeticks3, but uses a start timestamp and end timestamp as parameters

/ arguments = ticker, starttimestamp, endtimestamp
/ timestamp args = TIMESTAMP format (date + time)

/ break up the query such that DATE and TIME
/ are extracted from the TIMESTAMP argument
/ and queried separately

tradeticks3:{ [ticker;starttimestamp;endtimestamp]
              select from trades where
              sym in ticker,
              date within `date$(starttimestamp;endtimestamp),
              time within (starttimestamp;endtimestamp) }

tradeticks3[`AAPL; 2014.04.21D09:00; 2014.04.21D09:31]

date       |	sym	| time
----------------------------------------------------
2014-04-21 |	AAPL	| 2014-04-21T09:05:55.985000
2014-04-21 |	AAPL	| 2014-04-21T09:07:51.570000
2014-04-21 |	AAPL	| 2014-04-21T09:09:23.909000
2014-04-21 |	AAPL	| 2014-04-21T09:10:23.391000
2014-04-21 |	AAPL	| 2014-04-21T09:21:25.636000
2014-04-21 |	AAPL	| 2014-04-21T09:22:44.347000
2014-04-21 |	AAPL	| 2014-04-21T09:24:52.662000
2014-04-21 |	AAPL	| 2014-04-21T09:28:40.306000

/ [date column] from trades table = [date format]
/ your args [starttimestamp;endtimestamp] are in the [timestamp format]
/ need to first convert your args from [timestamp format] to [date format]
/ so original [date column] stays the same
/ and you cast your args to query in the same format as [date column]

/ [time column] from trades table = [timestamp format]
/ since your args are already in the [timestamp format]
/ you can simply query in the same format

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

```q
/ 8. Create function, quotechanges, to retrieve data when bid or ask changes

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

🔵 [Func 8.9] Functions Problem Set 3 (med/hard) - AQ
<a name="func_set3AQ"></a>
[Top](#top)

```q
/ load fakedb.q

\l hdb

\a
`depth`quotes`trades
```

```q
/ 1. write a func that calc the avg spread between bid and ask per date 
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

```q
/ 2. Create function called dailystats1
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

```q
/ 3. Create function called dailystats2
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

```q
/ 4. Create function, dailystats3
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

```q
/ 5. create dailystats 4
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

```q
/ 6. Create function that calculates the VWAP and TWAP per day per symbol
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

```q
/ 7. Create function twapandvwap2
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

```q
/ 8. Create function called bigdays
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

```q
/ 9. Create function called bucket
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

```q
/ 10. want buckets to start at:
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

```q
/ 11. create function called volumebuckets1
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

```q
/ 12. create volumebuckets2
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

🔵 [func 8.10] Functions Problem Set 4 - AQ
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

```q
/ 1. Name this func tradeticks1
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

```q
/ 2. Create function called calcreturns
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

```q
/ (i dont really get this)

/ 3. using tradeticks1 function,
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

```q
/ (i dont get this)

/ 4. calc [running sum of vol] traded in each "price group"
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

```q
/ 5. Extract from depth table
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

```q
/ (i dont get this)

/ 6. Extract 30 mins worth of depth ticks
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

🔵 [Func 8.11] Int Problem Set 1 - GS
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

🔵 [Func 8.12] Int Problem Set 2 - GS
<a name="func_int2"></a>
[Top](#top)

```q
/ 1. Create a table called price with columns date, ticker, exch, and price

price: ([] date: 2021.01.21 2021.03.21 2021.09.21; ticker:`AAPL`AAPL`MSFT; exch: `US`UW`US; price: 10 20 30)

price:
date       | ticker | exch | price
--------------------------------
2021-01-21 |  AAPL  | US   | 10
2021-03-21 |  AAPL  | UW   | 20
2021-09-21 |  MSFT  | US   | 30
```

### [func 8.12] Creating a Function

```q
/ 2. Create a function called f
/ takes in 3 args: [sym, start, end]
/ this function queries the price table 
/ checks the sym (input) against the ticker column (price table)
/ and returns the tickers (from price table) that fall within the start and end date (inputs)
/ return all columns

f:{ [sym;start;end] select from price where date within (start;end), ticker in sym}
f[`AAPL;2021.01.21; 2021.12.21]

date       | ticker | exch | price
---------------------------------
2021-01-21 | AAPL   | US   | 10
2021-03-21 | AAPL   | UW   | 20

/ since you want to return all columns, the filters come AFTER where clause
/ anytime you want to query between 2 dates (or times), use WITHIN
/ note the syntax = within (lowerband;upperband)
/ checks if [date column] from [price table] is within the 2 arguments you input
/ and if [ticker column] from [price table] matches the sym argument you input
/ checks COLUMN from [price table] against your inputs/arguments
/ and iterates through every row
```

### [func 8.12] Syntax that don't work using WITHIN

```q
/2b. Notice these variations of the WITHIN syntax DONT work

f:{ [sym;start;end] select from price where date within (start end), ticker in sym}
f:{[sym;start;end] select from price where date within [start;end], ticker in sym}
f:{ [sym;start;end] select from price where date within start end, ticker in sym}

/ within HAS to be (lowerbound;upperbound)

f:{ [sym;start;end] select from price where date within (start;end), ticker in sym}
```

### [func 8.12] Creating 2nd Table called Input

```q
/ 3. Create 2nd table called input with 3 columns: ticker, start and end date

input: ([] ticker: `AAPL`AAPL`MSFT; start: 2021.01.01 2021.03.01 2021.06.01; end: 2021.03.01 2021.06.30 2021.08.01)

input:
ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01
```

### [func 8.12] Querying the input vs price tables

```q
/ 4. From the [input table], retrieve the [syms] from original [price table]
/ that match the [start] and [end dates] from [input]

/ thought process:

/ you have 2 tables: price (table 1) and input (table 2)
/ you want to check if data from table 1 fall within specific parameters in table 2
/ first checks if [ticker] from [price table 1] = [ticker] from [input table 2]
/ then checks if [date] from [price table 1] falls within [start/end] from [input table 2] 
/ you need to query ENTIRE row from input table [sym + start + end]
/ then iterate through EACH row

/ so you can either run this query 3x, or you can iterate through each row using EACH
/ since you have 3 arguments (sym, start, end) from the original function
/ you can query these args as a LIST of values corresponding from [input table]
```

### [func 8.12a] Solution 1 (manual - no good)

```q
/ 4a. Solution 1: Manually run query through each row

price:
date       | ticker | exch | price
--------------------------------
2021-01-21 |  AAPL  | US   | 10
2021-03-21 |  AAPL  | UW   | 20
2021-09-21 |  MSFT  | US   | 30

input:
ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01

/ earlier you created a function to check the price table
/ based on 3 arguments (sym, start, end)
/ your input table have the same 3 arguments (ticker,start,end)
/ so you could just manually check each row

f:{ [sym;start;end] select from price where date within (start;end), ticker in sym}
f[`AAPL;2021.01.21; 2021.03.01]

ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01

/ so yes, the inputs you supplied matches the query
/ then you can do this for every row
/ however this is super manual and inefficient
```

### [func 8.12b] Solution 2 (using EACH + List of values)

```q
/ 4b. Solution 2: use EACH to iterate through list of values

/ you can retrieve a LIST of values from each COLUMN
/ syntax = table_name`column_name
/ for example, input`ticker = `AAPL`AAPL`MSFT

/ so instead of supply single arguments, you can supply a LIST of values
/ for each argument
/ then use EACH (f') to iterate through each row

input table
ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01

/ test out the 3 lists of values for each column first

input`ticker
`AAPL`AAPL`MSFT

input`start
(2021-01-01d; 2021-03-01d; 2021-06-01d)

input`end
(2021-03-01d; 2021-06-30d; 2021-08-01d)

/ using same function as earlier
/ when you CALL your function, use list of values for each argument
/ and use f' to iterate through EACH row
/ also need to use RAZE to collapse one level of nesting

f:{ [sym;start;end] select from price where date within (start;end), ticker in sym}
raze f'[input`ticker;input`start;input`end]

ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30

/ original function doesnt change
/ function queries [price table] and retrieves syms [arg1] where date column
/ falls within (start;end) [arg2;arg3]

/ this time around, your inputs = [LIST OF VALUES] for EACH column from [input table]
/ f' = run the function through EACH row (doesnt work if you do f each)
/ the output is a list of 3 tables, so to collapse 1 layer, use RAZE
/ raze = (,/)
```

### [func 8.12] Solution 3 (re-write function)

```q
/ 5. Create new function f2, using x to query corresponding columns
/ in the input table and iterating through EACH row

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

f2:{select from price where date within x`start`end, ticker in x`ticker}
raze f2 each input

/ the function:
/ f2 takes implicit argument x as the [input table]
/ remember, logic = column from table 1 vs input
/ so find where [date] from [price table] is within (start,end) from x (your input)
/ AND where [ticker] from [price table] matches [ticker] from x (your input)

/ calling your function:
/ so instead of 3 arguments, you only have one x
/ x is your entire input table
/ to iterate through EACH row of [input table], you have use [EACH]
/ you return a list of tables, so need RAZE to level it

/ oddly, these all work when calling your function

raze f2 each input
raze f2'[input]
f2[input]
```

<a name="qsql"></a>
### 🔴 9. qSQL
[Top](#top)

🔵 [QSQL 9.1] QSQL Problem Set 1 - TS
<a name="sql_1"></a>

```q
/ load the trades.q script

\l trades.q
\a
`quote`stock`trade
```

[QSQL 9.1] Select first price, first time by date for AAPL

```q
select first price, first time by date from trade where sym=`AAPL

`date`       | price| time
----------------------------------
`2021-05-29` | 78.6 | 09:30:03.025
`2021-05-30` | 60.8 | 09:30:02.686
`2021-05-31` | 55.1 | 09:30:18.274

/ by date = groups date as the key column
```

[QSQL 9.1] Find the total number of trades for RBS by date and time in hours

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

[QSQL 9.1] Find all AAPL prices that are less than the avg price, grouped by date

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

[QSQL 9.1] Retrieve prices, keyed by TODAY, where AAPL's price is less than the avg price

```q
select price by date=.z.d from trade where sym=`AAPL, price < avg price

d   | price
--------------
`0` | 23 52 63...
`1` | 23 66 12...

/ grouped by today; 0 = false, 1 = true
```

[QSQL 9.1] Retrieve price divide by max price, keyed by today, for AAPL where the price is less than the avg price

```q
select {x % max x} price by date = .z.d from trade where sym=`AAPL, price < avg price

d    | price
-------------------
`0b` | 0.98 0.7 0.8
`1b` | 0.12 0.43 0.32
```

[QSQL 9.1] Retrieve all data for AAPL and RBS

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

[QSQL 9.1] Retrieve trades for RBS where price is between 95 and 100

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

[QSQL 9.1] Retrieve trades for RBS within 95 and 100 and between 11:30 - 12:00

```q
select from trade where sym=`RBS, price within 95 100, time within 11:30 12:00

date      | time          |sym   | price  | size | cond
-------------------------------------------------------
2021-05-30| 11:40:02.743 | RBS   | 97.113 | 80700 | C
2021-05-30| 11:44:03.025 | AAPL  | 98.66  | 19000 | A
```

### 🔵 [QSQL 9.2] Problem Set 2 - TS
<a name="sql_2"></a>
[Top](#top)

```q
\l trades.q
```

[QSQL 9.2] Delete the entire cond column from trade

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

[QSQL 9.2] Delete the entire row that has A for cond

```q
delete from trade where cond="A"

date       |  time   | sym |price|size| cond| maxprice
------------------------------------------------------
2021.03.01 | 15:09:01| JPM |  74 |41.2|  B  | 102
2021.03.01 | 15:09:01| UBS |  41 |31.2|  C  | 91

/ DELETE without WHERE clause = deletes entire column
/ DELETE with WHERE clause = deletes rows where conditions met
```

[QSQL 9.2] update all prices to 10 in trade table

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

[QSQL 9.2] update all prices of sym C to 10.0

```q
update price:10.0 from trade where sym=`C

date       | time         | sym | price| size  | cond
-----------------------------------------------------
2021.10.30 | 09:30:02.553 | C   | 10   | 63500 | B   

/ note the price has to be a float, otherwise query won't work
/ when in doubt, use META to check the datatypes
```

[QSQL 9.2] update the price to 10.0 for AAPL and GOOG

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

[QSQL 9.2] add new column vol, which is price x size for AAPL and GOOG

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

[QSQL 9.2] update the prices of AAPL and GOOG to average price, grouped by sym 

```q
update price:avg price by sym from trade where sym in `AAPL`GOOG

date       | time         | sym  | price| size  | cond 
-------------------------------------------------------
2021.10.30 | 09:30:02.553 | AAPL | 79.98| 63500 | B    
2021.10.30 | 09:30:02.701 | AAPL | 79.98| 1700  | B    
2021.10.30 | 09:30:02.743 | GOOG | 34.32| 80700 | C 
```

[QSQL 9.2] randomly select 100 rows from trade, name this table tt

```q
tt:100?trade

date       |  time   | sym |price|size| cond
---------------------------------------------
2021.01.01 | 15:10:01| BAC | 70  |422| B
2021.03.01 | 15:09:01| JPM | 74  |412| C
```

[QSQL 9.2] update all cond to "D"

```q
update cond: "D" from trade

date       |  time   | sym |price|size| cond
---------------------------------------------
2021.01.01 | 15:10:01| BAC | 70  |422 | D
2021.03.01 | 15:09:01| JPM | 74  |412 | D
```

[QSQL 9.2] divide all size values by 100

```q
update size % 100 from trade

date       |  time   | sym |price|size| cond
---------------------------------------------
2021.01.01 | 15:10:01| BAC | 70  |42.2| D
2021.03.01 | 15:09:01| JPM | 74  |41.2| D
2021.03.01 | 15:09:01| UBS | 41  |31.2| D

/ can perform function on entire column. size divided by 100
```

[QSQL 9.2] add a new column called advice and populate with sell

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

[QSQL 9.2] update advice to buy if price less than 70

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

[QSQL 9.2] add new column maxprice populated with max prices by sym

```q
update maxprice: max price by sym from trade

date       |   time  | sym |price|size|cond|maxprice
----------------------------------------------------
2021.01.01 | 15:10:01| BAC |  70 |42.2|  D | 104
2021.03.01 | 15:09:01| JPM |  74 |41.2|  D | 102
2021.03.01 | 15:09:01| UBS |  41 |31.2|  D | 91

/ since maxprice doesnt exist, adds new column to end
```

### 🔵 [QSQL 9.3] Problem Set 3 - TS
<a name="sql_3"></a>
[Top](#top)

```q
\l trades.q
```

[QSQL 9.3] Extract trades for MS greater than 1,000 in size

```q
select from trade where sym=`MS, size >1000

dt         |sym |price|size
----------------------------
2021.01.01 | MS | 225 | 200
2021.01.01 | MS | 234 | 400
```

[QSQL 9.3] Find the total size of all trades and the average price paid per sym

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

[QSQL 9.3] Find the trade that was largest size for each sym (use fby)

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

[QSQL 9.3] Select the latest trade for each sym, and include all details (non-fby)

```q
select last date, last price, last time by sym from trade

sym | date       | price | time
----------------------------------------
A   | 2021-12-01 | 87.5  | 17:29:57.306
AA  | 2021-12-01 | 68.0	 | 17:29:58.789
AAPL| 2021-12-01 | 76.1	 | 17:29:58.262
B   | 2021-12-01 | 95.5	 | 17:29:56.912
```

[QSQL 9.3] Select the latest trade for each sym, and include all details (fby)

```q
select from trade where time=(max;time) fby sym

date       | time         | sym  | price | size  | cond
-------------------------------------------------------
2022-04-01 | 17:29:58.861 |   AA |  60.0 | 20900 |  C
2022-04-01 | 17:29:58.878 | MSFT |  83.5 |  7700 |  B
2022-04-01 | 17:29:58.907 | AAPL |  68.0 | 58000 |  B
2022-04-01 | 17:29:58.968 |    D |  82.9 | 76800 |  A
```

[QSQL 9.3] Find all trades that have sym GOOG

```q
select from trade where sym=`GOOG

date       | time         | sym  | price | size  | cond
--------------------------------------------------------
2021-11-27 | 09:30:17.541 | GOOG | 86.1  | 83500 | C
2021-11-27 | 09:30:17.895 | GOOG | 80.5  | 91700 | B
2021-11-27 | 09:30:18.011 | GOOG | 81.0  | 49300 | B
```

[QSQL 9.3] Find all trades that have sym GOOG or RBS or A

```q
select from trade where sym in `GOOG`RBS`A

date       | time         | sym  | price | size  | cond
-------------------------------------------------------
2021-11-27 | 09:30:17.541 | GOOG | 86.1  | 83500 | C
2021-11-27 | 09:30:17.895 |  RBS | 80.5  | 91700 | B
2021-11-27 | 09:30:18.011 |    A | 81.0  | 49300 | B
```

[QSQL 9.3] Find all trades for google that had a price between 70 and 80

```q
select from trade where sym=`GOOG, price within 70 80

date       | time         | sym  | price | size  | cond
-------------------------------------------------------
2021-11-27 | 09:30:17.541 | GOOG | 73.1  | 83500 | C
2021-11-27 | 09:30:17.895 | GOOG | 75.5  | 91700 | B
2021-11-27 | 09:30:18.011 | GOOG | 77.0  | 49300 | B
```

[QSQL 9.3] Count the number of trades and total size of trades per hour for sym RBS

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

[QSQL 9.3] Select the number of trades and total size of trades every 30 mins for sym RBS

```q
select numbertrades: count i, totalsize: sum size by 30 xbar time.minute from trade where sym=`RBS

minute|numbertrades|totalsize
-------------------------------
09:30 |    3186    | 159063500
10:00 |	   3271    |  62197000
10:30 |	   3273    | 158998100
```

[QSQL 9.3] Find all trades for A where the price was cheaper than the average for that day

```q
select from trade where sym=`A, price < avg price

date       | time         | sym | price | size  | cond
-------------------------------------------------------
2021-11-27 | 09:30:17.997 |  A	|  57.8 | 65600 | C
2021-11-27 | 09:30:23.144 |  A	|  54.5 | 31200	|
2021-11-27 | 09:30:23.570 |  A  |  60.8 | 8200	|
```

### 🔵 [QSQL 9.4] Creating Buckets using xbar
<a name="sql_4"></a>
[Top](#top)

```q
\l trades.q
```

[QSQL 9.4] Calculate the number and total size traded by sym for each $1 price 

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

[QSQL 9.4] Find the max price and total size of trades by ticker during 5 min buckets

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

[QSQL 9.4] Find the max price by sym in 45 min time buckets, specifically including 9:30 time bucket

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

[QSQL 9.4] Count the number of trades and total size of trades per hour for sym RBS

```q
select num_trades:count i, total_size: sum size by sym, 1 xbar time.hh from trade where sym=`RBS

`sym` | `hh` | num_trades | total_size
--------------------------------------
`RBS` |  `9` |    3186    | 159063500
`RBS` | `10` |    6544    | 321195100
`RBS` | `11` |    6280    | 315284200
`RBS` | `12` |    6141    | 306898200
`RBS` | `13` |    6086    | 305154900

/ you need to group BY SYM, since you're aggregating
/ the total num trades + total size
/ use count i = count virtual column
/ notice xbar comes AFTER the by sym, but BEFORE the where
/ both sym + xbar are aggregators
/ so both columns are keyed
```

```q
/ notice what happens if instead of group BY SYM
/ you group BY XBAR

select num_trades:count i, total_size: sum size by 1 xbar time.hh from trade where sym=`RBS

`hh` | num_trades | total_size
----------------------------
`9`  |    3186   | 159063500
`10` |    6544   | 321195100
`11` |    6280   | 315284200
`12` |    6141   | 306898200
`13` |    6086   | 305154900

/ the sym column is removed
/ but the underlying answer is still correct
```

[QSQL 9.4] Select the number of trades and total size of trades every 30 mins for the sym RBS

```q
select num_trades: count i, tot_size:sum size by sym, 30 xbar time.minute from trade where sym=`RBS

`sym` | `minute` | num_trades | tot_size
---------------------------------------
`RBS` |  `09:30` |    3186    | 159063500
`RBS` |  `10:00` |    3271    | 162197000
`RBS` |  `10:30` |    3273    | 158998100
`RBS` |  `11:00` |    3110    | 157994800
`RBS` |  `11:30` |    3170    | 157289400
`RBS` |  `12:00` |    3120    | 156311100

/ 30 xbar time.minute = groups minutes by 30
```

[QSQL 9.4] Calc the avgmid price from quotes for GOOG grouped by 5 min buckets

```q
/ need to retrieve from quotes table
/ avg mid quote = (bid + ask) /2
/ since you're grouping into 5 xbar, avg will calc avg over 5 min bucket
```

```q
select avgmid:avg .5*bid+ask by 5 xbar time.minute from quote where sym =`GOOG

minute| avgmid
--------------
09:30 | 79.7
09:35 |	80.4
09:40 |	79.5
09:45 |	79.4
09:50 |	80.4

/ by = group, so this becomes keyed by 5 xbar time
```

### 🔵 [QSQL 9.5] Creating Buckets using within
<a name="sql_5"></a>
[Top](#top)

```q
/ another powerful to aggregate data into buckets
/ is by first filtering your parameter using WITHIN
/ then "naming" that "bucket" 
/ load trades.q script
```

[QSQL 9.5] Add a new column called Sizegroup, and returns "small" when you retrieve the number of small trades (less than 999) for each sym, using WITHIN

```q
\l trades.q

/ small trades = size less than 999
/ add column called tradesize = small for each sym

select num:count i by sym, sizegroup:`small from trade where size within 0 999

`sym` | `sizegroup` | num
--------------------------
`A`   |   `small`   | 454
`AA`  |   `small`   | 521
`AAPL`|   `small`   | 493
`B`   |   `small`   | 499

/ num = number of trades which sizes are less than 999
/ use COUNT to return NUMBER of trades
/ since you're aggregating BY sym, the sym + sizegroup cols are keyed
/ use WHERE within x y = range of values to be selected
```

[QSQL 9.5] retrieve the number of [small], [med] and [large] trades for each sym

```q
/ small = 0 to 999
/ med = 1000 to 8999
/ large = greater than 8999

/ consolidate into same table

(select count i by sym, sizegroup:`small from trade where size within 0 999),
(select count i by sym, sizegroup:`medium from trade where size within 1000 8999),
(select count i by sym, sizegroup:`big from trade where size > 8999)

`sym | `sizegroup` | num
---------------------------
`A`   | `large`    | 45645
`A`   | `med`      | 4009
`A`   | `small`    | 480

/ we have successfully grouped each sym into "buckets"
/ of either small, med, or large
/ depending on the number of trades (from size)
/ there is a better way retrieve this, by writing function called BIN
```

### 🔵 [QSQL 9.6] Creating Buckets using BIN
<a name="sql_6"></a>
[Top](#top)

```q
\l trades.q
```

[QSQL 9.6] For list of sizes, group into buckets of 0, 1000 or 9000

```q
sizes: 2000 100 6000 11000

0 1000 9000 bin sizes
1 0 1 2

/ bin takes its LEFT hand buckets, and sorts index position of RIGHT argument
/ so sizes = 4 elements, will return index position of bin
/ 2000 = index position 1 bin
/ 100 = index position 0 bin
/ 6000 = index position 1 bin
/ 11000 = index position 2 bin
```

[QSQL 9.6] Rename BIN buckets as small, med, or large

```q
/ 2. name the buckets as small, med, or big
/ based on the buckets of 0, 1000, and 9000

`small`med`big 0 1000 9000 bin sizes
`med`small`med`big

/ syntax: 
/ `name1`name2`name3 size1 size2 size 3 bin LIST
/ still returns the index position based on the sizes
/ but now has a "name" associated to it (small, med, big)
```

[QSQL 9.6] Create function called tradesize that accepts a list of numbers and outputs them into buckets of either small (less 100), med (100-200), or big (> 200) using BIN

```q
/ function accepts a list of sizes as inputs
/ and bucket those sizes into bins of small, med, big
/ you have to pre-define your bucket parameters (small = less 100) etc

tradesize:{[x]`small`med`big 0 1000 9000 bin x}

/ test out the function with sizes (list of sizes from above)

sizes: 2000 100 6000 11000

tradesize [sizes]
`med`small`med`big

/ it works!
```

[QSQL 9.6] Use your tradesize function to retrieve total num of trades grouped by sym and size bucket

```q
/ from trade, group trade size by sym into bins using your tradesize function
/ so there should be a column called sizebucket with either small, med, or large
/ and the number of trades per bucket

\l trades.q
```

Soltuion 1

```q
select num:count i by sym, sizebucket:tradesize[size] from trade

sym | sizebucket | num
-------------------------
A   | large      | 50032
A   | med	 | 56
A   | small	 | 46
AA  | large	 | 49820
AA  | med	 | 44
AA  | small	 | 49

/ add new column called sizebucket
/ which retrieves output from your tradesize function
/ which takes size column from trade table as input
/ count i = virtual column
```

Solution 2

```q

select num:count i by sym, sizebucket:(tradesize;size) fby sym from trade

sym | sizebucket | num
-------------------------
A   | large      | 45645
A   | med        | 4009
A   | small      | 480
AA  | large      | 45425

/ NOTE! since you are creating a NEW COLUMN called [sizebucket]
/ you have to [select] the new column you are fby with
/ [from trade] goes all the way at the END

/ [sizebucket column] -> insert [tradesize function] you created
/ [size column] from [trade table] becomes argument x for [tradesize function]
/ [tradesize function] becomes an AGGREGATOR for fby
/ returns the number of trades (count i), sorted by sym and its size bucket
```

### 🔵 [QSQL 9.7] fby Problem Set
<a name="sql_7"></a>
[Top](#top)


[QSQL 9.7]  From the two lists below, find the lowest temperature by city (fby on 2 lists)

```q
city:`NY`NY`LA`SF`LA`SF`NY
temp:32 31 75 69 70 68 12

(min;temp) fby city
12 12 70 68 12

/ this calculates the min temp for every city (12 for NYC)
/ min = agg function
/ temp = column to agg
/ city = what you are filtering by
```

[QSQL 9.7] From trade table, find the max price per symbol, only return the sym and price columns (without using fby)

```q
\l trades.q
```

```q
select max price by sym from trade

sym | price
----------------
A   | 109.9989
AA  | 109.9987
AAPL| 109.9997
B   | 109.9992

/ notice only returns sym + max price columns
/ if you want to return the entire table
/ need to use fby
```

[QSQL 9.7] From trade table, find the max price per symbol, return all columns (using fby)

```q
select from trade where price=(max;price) fby sym

date	   | time         | sym  | price    | size  | cond
-----------------------------------------------------------
2023-09-05 | 10:38:23.110 | MS	 | 109.9994 | 58500 | B
2023-09-05 | 11:54:07.340 | AAPL | 109.9997 | 6800  |	 
2023-09-05 | 12:57:02.029 | MSFT | 109.9998 | 23400 | C
2023-09-05 | 13:20:30.544 | GOOG | 109.9999 | 12700 | C
2023-09-05 | 13:57:07.069 | AA	 | 109.9987 | 86100 | C

/ since you want ALL columns, need to filter AFTER the where clause
/ fby returns the ENTIRE table
/ fby goes at the END after where
/ syntax = col1 = (aggr;col1) fby col2
/ col 1 = price
/ aggr = max
/ col 2= sym
```

[QSQL 9.7] From trade, find the LATEST max price by sym (using 2 fby)

```q
/ notice there are 2 conditions you want to filter for now:
/ latest time + max price
/ assume there are 2 syms with same max price, and you want 
/ the latest one

select from trade where price=(max;price) fby sym, time=(max;time) fby sym

time      |sym  |src| price | size
-----------------------------------
2019-03-11|GOOG	| O | 36.01 | 708
2019-03-11|MSFT | N | 35.01 | 7810

/ since there are 2 conditions you want to filter by
/ can use 2 fby filters
/ fby goes AFTER the where clause
/ first fby max price by sym
/ then fby last time fby sym
```

[QSQL 9.7] From the trade table, find the ONE sym with the single highest price on 2023.09.05, and return all columns

```q
select from trade where date=2023.09.05, price=max price

date       | time         | sym  | price    | size  | cond
-----------------------------------------------------------
2023-09-05 | 13:20:30.544 | GOOG | 109.9999 | 12700 | C

/ since you need to retrieve ALL columns,
/ need to filter AFTER the where clause (returns all columns)
/ you are looking for the SINGLE highest price on a specific date
/ there's no aggregation invovled, hence no need for fby
```

[QSQL 9.7b] Notice what happens when you do this:

```q
select max price from trade where date = 2023.09.05

price
-----
109.999

/ only returns the single highest price
/ and nothing else
```
[QSQL 9.7c] Or what happens when you do this:

```q
select max price by sym from trade where date = 2023.09.05

sym  | price
-----------------
A    | 109.9971
AA   | 109.9987
AAPL | 109.9997
B    | 109.9953

/ if you group by sym, it retrieves the max price
/ for ALL syms on that date
/ and doesn't return any other columns
```

[QSQL 9.7] From trade table, find the max price by sym on 2023.09.05, return all columns (using fby)

```q
select from trade where date=2023.09.05, price=(max;price) fby sym

date       | time         | sym | price | size | cond
------------------------------------------------------
2021-11-26 | 10:17:09.373 | A	| 109.9	| 94300| C
2021-11-26 | 10:25:22.268 | MSFT| 109.9	| 49100| C
2021-11-26 | 11:49:11.143 | D	| 109.9 |  5600| A

/ since you want ALL COLUMNS, need to filter conditions after WHERE clause
/ first filters by date, then finds max price aggr by sym
/ you want the max price by sym, which means for each sym, aggregate all prices,
/ and find the largest one = needs aggregation
/ hence you need to use fby function
```
[QSQL 9.7b] Notice what happens if you do this instead:

```q
select max price by sym from trade where date = 2021.11.26

sym  | price
-------------
A    | 109.9
AA   | 113.2
AAPL | 339.1

/ this will ONLY returns the sym + max price column
/ if you want to return the entire table,
/ need to filter AFTER the where clause
```

[QSQL 9.7] From trade table, find the max price by sym AND cond on 2023.09.05, but return ALL columns

```q
select from trade where date=2023.09.05, price=(max;price) fby ([] sym; cond)

date       | time         | sym | price    | size  | cond
----------------------------------------------------------
2023-09-07 | 10:05:09.563 | C   | 109.9945 | 71600 | B
2023-09-07 | 10:35:14.496 | B   | 109.9953 | 44000 | A
2023-09-07 | 10:38:23.110 | MS  | 109.9994 | 58500 | B
2023-09-07 | 11:36:30.527 | A   | 109.9971 | 60800 | A

/ need to use fby AFTER the where clause to return all columns
/ in other words, i want the max price for EACH sym and cond combination
/ this means aggregating the max price for both sym and cond
/ to aggregate by more than one field, use fby + TABLE 
/ Table has 2 columns; sym and cond
/ first filters by date, then aggregates the max price by sym AND cond
```

[QSQL 9.7] VWAP Problem Set: Find the VWAP price from the 2 lists

```q
size: 100 200 300 400
price: 10 20 30 40

size wavg price
30f

/ VWAP = volume weighted average price, so can use the wavg function 
/ wavg = weighted average function
/ x wavg y = calculates the weighted average between the 2 lists
```

[QSQL 9.7] VWAP: Create a vwap function that uses size and price as arguments

```q
2. Create a vwap function that uses size and price as arguments

vwap:{[size;price] size wavg price}
vwap[size;price]
30f

/ the function allows inputs from list size + price
/ and output is the same as above
```

[QSQL 9.7] VWAP: From trade table, using your function, retrieve the vwap price for each sym

```q
3. From trade table, using your function, retrieve the vwap price for each sym

select vwap:vwap[size;price] by sym from trade

sym  | vwap
---------------
A    | 79.9450
AA   | 79.9903
AAPL | 79.9948
B    | 79.8015
BAC  | 79.8109

/ selecting a new column name will add that column
/ new column utilizes your vwap function
/ and uses size and price columns from trade table
```

[QSQL 9.7] VWAP: For each sym on 2023.09.07, retrieve only the prices that are greater than the VWAP price. Return all columns

```q
select from trade where date=2023.09.07, price > ({x[`size] wavg x`price}; ([]size;price)) fby sym

/ return all columns = filter to come AFTER where clause
/ retrieves prices that are greater than the vwap price for each sym
/ "for each sym" = fby sym
/ VWAP calculated via the wavg function

/ syntax:
/ actually follows the fby syntax: price > (aggr;price) fby sym
/ except in this case, the aggr = vwap
/ and price = the table of ([] size;price)

/ so the function calculates the wavg for every size and price
/ and the x` iterates through every row in the table
```

### 🔵 [QSQL 9.8] Table Query Problem Set 1
<a name="sql_8"></a>
[Top](#top)

[QSQL 9.8] Retrieve the values from t1 where date is June 13, 2023 and where the syms match in t2

```q
t1: ([] date: 2023.01.01 2023.01.01 2023.06.13 2023.06.13; sym: `GOOG`MSFT`FB`AMZN; exch: `nyse`nyse`nasdaq`nasdaq)

t2: ([] sym: `GOOG`MSFT`FB`AMZN; exch: `nyse`nyse`nasdaq`nasdaq)

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
MSFT | nyse
FB   | nasdaq
AMZN | nasdaq

select from t1 where date=2023.06.13, ([] sym; exch) in t2

date       | sym  | exch
--------------------------
2021-06-13 | FB   | nasdaq
2021-06-13 | AMZN | nasdaq

/ adding filter after the where clause returns all columns
/ first filters by date
/ then searches a table of (sym;exch) from t1 in t2 to find matches
```

### 🔵 [QSQL 9.9] Table Query Problem Set 2
<a name="sql_9"></a>
[Top](#top)


[QSQL 9.9] 1. Retrieve IBM from cond A, CSCO from cond A or B, and MSFT from cond C with date = today

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

### 🔵 [QSQL 9.10] Table Query Problem Set 3
<a name="sql_10"></a>
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

### 🔵 [QSQL 9.11] Signum Deltas Problem Set
<a name="sql_11"></a>
[Top](#top)


```q
/ can make use of the [deltas + signum] function

/ [deltas] will calculate the change between subsequence elements
/ [signum] will tell you if the element is [positive], [negative], or [0]

deltas 3 2 2 1 5
3 -1 0 -1 4

signum deltas prices
1 -1 0 -1 1
```

[QSQL 9.11] 1. Add in new col called direction which calcs the signum deltas of price

```q
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

/ this will add a new column, [dir], which will be [+1, 0, or -1]
/ tells you if its positive, negative or unch
```

[QSQL 9.11] 2. Create a function for signum deltas

```q
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

[QSQL 9.11] 3. Group this data by sym, and calc total size traded by direction (uptick, downtick, etc)

```q
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

### 🔵 [QSQL 9.12] Select vs Exec Example
<a name="sql_12"></a>
[Top](#top)

[QSQL 9.12] Retrieve the distinct cities and countries from the table

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

### 🔵 [QSQL 9.13] Deltas/Differ Problem Set
<a name="sql_13"></a>
[Top](#top)

[QSQL 9.13] 1. Return all trades where the trade price has changed

```q
select from trade where differ price

date       time         sym  price    size  cond
------------------------------------------------
2021.10.19 09:30:02.553 C    107.2018 63500 B   
2021.10.19 09:30:02.701 MSFT 96.87488 1700  B   
2021.10.19 09:30:02.743 RBS  97.11338 80700 C  

/ so differ will return all prices that are DIFFERENT then last
```

[QSQL 9.13] 2. Add new column called change that calculates price changes between trades

```q
update change:deltas price from trade

date       time         sym  price    size  cond change    
--------------------------------------------------------
2021.10.19 09:30:02.553 C    107.2018 63500 B    107.201  
2021.10.19 09:30:02.701 MSFT 96.87488 1700  B    -10.326 
2021.10.19 09:30:02.743 RBS  97.11338 80700 C      0.238

/ so change = deltas from previous price
```

[QSQL 9.13] 3. Select trades where trade prices have increased

```q
select from trade where (deltas price)> 0

date       time         sym    price    size  cond 
--------------------------------------------------
2021-10-19 09:30:02.553	C      107.2    63500  B
2021-10-19 09:30:02.743	RBS     97.1    80700  C
2021-10-19 09:30:02.758	A      100.3    50300  B
```

### 🔵 [QSQL 9.14] Problem Set 1 - AQ
<a name="sql_14"></a>
[Top](#top)

```q
\l salestable.q
tables[]
`quote`sales`stock`trade

/ tables [] shows you what tables are within the script
```

[QSQL 9.14] 1. Add new column called profit (price * qty)

```q
update profit:price*quantity from `sales

trader |product |price| quantity| profit
-----------------------------------------
Bob    | pencil | 3   | 84      | 252
Bob    | pen	| 3   |	82	| 246
Paul   | book	| 3   |	64	| 192
```

[QSQL 9.14] 2. Calculate total profit each trader and product

```q
select sum profit by trader, product from sales

trader product profit
---------------------
Bob    book    79
Bob    paper   1353
Bob    pen     728
```

[QSQL 9.14] 3. Sort profit by ascending order by trader and product

```q
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

### 🔵 [QSQL 9.15] Problem Set 2 - AQ
<a name="sql_15"></a>
[Top](#top)

```q
/ Create function f, then call 300 to create function called marks:

f:{([]subject:(4*x)#`maths`english`french`ict;class:raze 4#/:x?"ABCDE";gender:raze 4#/:x?"MF";mark:35+(4*x)?60;id:raze 4#/:til x)}
marks:f[300]
```
[QSQL 9.15] 1. Find marks for class A
```q
select from marks where class ="A"
```

[QSQL 9.15] 2. Find marks for males of class B
```q
select from marks where gender="M",mark="B"
```

[QSQL 9.15] 3. Find the average french mark in class c

```q
select avg mark from marks where class = "C", subject=`french
```

[QSQL 9.15] 4. Find the average mark for each subject, ignoring classes
```q
select avg mark by subject from marks
```

[QSQL 9.15] 5. For class A, produce table of avg, min, max and sd of math marks

```q
select average:avg mark, low: min mark, high: max mark, sd:dev mark from marks where subject =`maths, class ="A"
```

[QSQL 9.15] 6. Display lowest, median and highest mark according to gender and subject
```q
select low:min mark, median:med mark, high: max mark by gender, subject from marks
```

[QSQL 9.15] 7. How many people are in each class (use id)?
```q
select count distinct id by class from marks
```

[QSQL 9.15] 8. For class b, subject ict, find med, range, sum of marks and num of distinct marks

```q
select median:med mark, range:(max mark) - min mark, total: sum mark, num: count distinct mark from marks where class = "B", subject =`ict
```

[QSQL 9.15] 9. Calc average mark by subject for class E
```q
select avg mark by subject from marks where class ="E"
```

[QSQL 9.15] 10. Calc highest average subject mark for class e, calling it topmark
```q
select topmark: max mark by subject from marks where class = "E"  
```

[QSQL 9.15] 11. Calc average mark for french in class d without using avg
```q
select average:(sum mark % count mark) from marks where class="D", subject=`french
```

[QSQL 9.15] 12. Calc the range of marks among males in class D in subjects ict and french
```q
select range:((max mark) - min mark) by subject from marks where class = "D", subject in `ict`french, gender="M"
```

[QSQL 9.15] 13. Delete class E results
```q
delete from marks where class="E"
```

[QSQL 9.15] 14. Add 5 marks to each of class A french paper
```q
update mark:5+mark from `marks where class="A", subject=`french
```

[QSQL 9.15] 15. Add new col called average, contains average mark for class and subject
```q
update average:avg mark by class, subject from marks 
```

### 🔵 [QSQL 9.16] Nested Table Problem Set
<a name="sql_16"></a>
[Top](#top)


```q
/ Given nested table t:

t:([] t: 05:15:43 00:59:05 01:19:44; bidPrices: (7.83 8.20 9.84 6.93; 0.97 7.44 9.33 2.93; 2.88 5.63 4.98 5.56

t         bidPrices            bidSizes        
--------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  57 0 72 50 62
00:59:05  0.97 7.44 9.33 2.93  97 99 27 31
01:19:44  2.88 5.63 4.98 5.56  47 57 31 15 68 49
```
[QSQL 9.16] 1. Create new column bidIndex, which shows the index position in descending values of bidPrices (large to small)

```q
update bidIndex: idesc each bidPrices from t

t         bidPrices            bidSizes           bidIndex
----------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  57 0 72 50 62      2 1 0 3 
00:59:05  0.97 7.44 9.33 2.93  97 99 27 31        2 1 3 0
01:19:44  2.88 5.63 4.98 5.56  47 57 31 15 68 49  1 3 2 0

/ idesc will sort by descending (large to small) order
/ you have to use EACH since its a nested table
```

```q
/ look what happens when you do this:

update bidIndex: idesc bidPrices from t

t         bidPrices            bidSizes           bidIndex
----------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  57 0 72 50 62            0 
00:59:05  0.97 7.44 9.33 2.93  97 99 27 31              2
01:19:44  2.88 5.63 4.98 5.56  47 57 31 15 68 49        1

/ if you omit the EACH
/ it looks at the entire list (not the individual nested list)
```

```q
/ old solution - not sure why x is there

update bidIndex:({idesc x} each bidPrices) from t

t         bidPrices            bidSizes           bidIndex
----------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  57 0 72 50 62      2 1 0 4 
00:59:05  0.97 7.44 9.33 2.93  97 99 27 31        2 1 4 0
01:19:44  2.88 5.63 4.98 5.56  47 57 31 15 68 49  1 4 3 0

/ from col bidPrices, shows index position of descending values
/ 2nd index position = 3rd value = 9.84 largest
```

[QSQL 9.16] 2. From your bidIndex column, retrieve the largest value only

```q
update bidIndex: {first idesc x} each bidPrices from t

t         bidPrices            bidSizes           bidIndex
----------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  57 0 72 50 62      2 
00:59:05  0.97 7.44 9.33 2.93  97 99 27 31        2
01:19:44  2.88 5.63 4.98 5.56  47 57 31 15 68 49  1

/ need to insert a function (first idesc x)
/ x goes through each nested list within bidPrices column
/ since idesc = sorts by ascending order
/ the first value = largest value
/ so first idesc x = isolates the largest value
```

[QSQL 9.16] 3. Add a new column, bestBid, and retrieve the highest bid from the index position in the bidIndex column

```q
update bestBid:bidPrices@'bidIndex from update bidIndex:({first idesc x} each bidPrices) from t

t         bidPrices            bidSizes     bidIndex   bestBid
--------------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  0 72 50 62    2          9.84 
00:59:05  0.97 7.44 9.33 2.93  23 99 27 31   2          9.33
01:19:44  2.88 5.63 4.98 5.56  57 31 15 49   1          5.63

/ previously you retrieved the index position for the largest value in bidPrices
/ now you need to retrieve the VALUE for that index position

/ bidPrices@'bidIndex -> this syntax is funky; need to learn
/ but the @ retrives the VALUE in bidprice column
/ based on the index position in bidIndex col

/ so bidIndex 2 = 9.84 from the bidPrices col
/ syntax is strange since it has 2 from
```

[QSQL 9.16] 4. Add new column, bestBidSize, and retrieve the largest bid size based on the bidIndex column
 
```q
update bestBidSize:bidSizes@'bidIndex from update bidIndex:({first idesc x} each bidPrices) from t

t         bidPrices            bidSizes     bidIndex   bestBidSize
------------------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  0 72 50 62    2          50 
00:59:05  0.97 7.44 9.33 2.93  23 99 27 31   2          27
01:19:44  2.88 5.63 4.98 5.56  57 31 15 49   1          31

/ same syntax and logic as before
/ bestBidSize = looks at bidIndex col, retrieves index position 2 from bidSizes col = 50
```

[QSQL 9.16] 5. Combine all 3 queries into a single line

```q
update bestBid:bidPrices@'bidIndex, bestBidSize:bidSizes@'bidIndex from update bidIndex:({first idesc x}each bidPrices) from t

t         bidPrices            bidSizes     bidIndex   bestBid  bestBidSize
---------------------------------------------------------------------------
05:15:43  7.83 8.20 9.84 6.93  0 72 50 62    2          9.84       50
00:59:05  0.97 7.44 9.33 2.93  23 99 27 31   2          9.33       27
01:19:44  2.88 5.63 4.98 5.56  57 31 15 49   1          5.63       31

/ useful to use index position to retrieve value in another column
/ lookup column @`source column
/ you can have multiple update statements to add new columns
/ the bestBid and bestBidSize columns actually retrieve from a new column called bidIndex
```

<hr>

<a name="adverbs"></a>
### 🔴 10. Adverbs
[Top](#top)

[Adverbs 10.0] Quick Reminder on Adverbs

```q
An adverb modifies an existing verb or function to alter how it's applied to its arguments

x'y / each
x,'y / each both
x,\: y / each left
x,/: y / each right	
x \ y / scan
x / y / over
```

[Adverbs 10.0] Each Both

```q
x,'y

/ Joins corresponding elements from two vectors of the same length
```

```q
x,'y

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

[Adverbs 10.0] Each Left

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

[Adverbs 10.0] Each Right

```q
x,/:y 

The top of the / points RIGHT
Adds EACH element of y to ENTIRE x
```

```q
1 2 3 ,/: `a`b`c

1 2 3`a
1 2 3`b
1 2 3`c
```

[Adverbs 10.0] Scan

```q
1 +\ 0 1 2 3

1 2 4 7

/ scan is an accumulating iterator
/ returns the result of each result
```

[Adverbs 10.0] Over

```q
1 +/ 0 1 2 3
7

/ over is an accumulating iterator
/ returns the final result
```

[Adverbs 10.0] 1. Calculate the factorial of 6 using [over]

```q
/ 6! = 6*5*4*3*2*1

(*/) 1 + til 6
720

/ need the 1 + because til 6 starts on 0
/ need ( ) surrounding */
```

[Adverbs 10.0] 2. Calculate the sum of every integer leading up to 5

```q
(+/) til 5
10
```

[Adverbs 10.0] 3. Retrieve the max value in a list from 1 to 5

```q
(|/) 1 2 3 4 5
5

/ | means find the greater of x and y
```

```q
/alternative syntax

max 1 2 3 4 5
5

/ the word "max" also works the same
```

[Adverbs 10.0] 4. Retrieve the min value in a list from 1 to 5

```q
(&/) 1 2 3 4 5
1

/ & amper means the smallest value
```

```q
min 1 2 3 4 5
1

/ keyword "min" also works the same
```

[Adverbs 10.0] 5. What is the difference between over and scan?

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

[Adverbs 10.0] 6. Create a function that calculates the moving sum with window size of 2

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

[Adverbs 10.0] 7. Join the 2 lists together to form a nested list

```q
/ use each both to join 2 lists together

numbers: 5 7 9
powers: 8 3 4

numbers, 'powers
(5 8;7 3;9 4)
```

[Adverbs 10.0] 8. Raise the first element of [numbers] to first element of [powers] and so on. 

```q
numbers xexp' powers
390625 343 6561f
```

[Adverbs 10.0] 9. A bank account pays 5% interest a year. Write a function that takes the current balance and returns the new balance after one year. Then use scan\ with that function to display the interest every year, up to 7 years in the future

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

[Adverbs 10.0] 10. Create a function, fib, that takes a fibonnaci sequence as its argument and returns the next entry

```q
/ the fib seq = sum of prior 2 numbers
/ 1 1 2 3 5 8 ...
/ func will take a fib sequence as its arg
/ and return the NEXT sequential value
/ aka = sum of last 2 numbers

fib: {sum -2#x}
fib 1 1 2 3
5

/ take last 2 elements of argument x (list of numbers)
/ and sums it
```

[Adverbs 10.0] 11. Use the over function to create a function, fibn, to generate a fib sequence x numbers long

```q
/ i dont get this

/ using your fib function from above
/ accepts arg as singular number
/ and returns a sequence x numbers long

fibn: {x fib/ 1 1}
fibn 5
1 1 2 3 5 8 13
```

[Adverbs 10.0] 12. Use scan to calculate the depreciation of cars 

```q
/ c = initial car value
/ r = depreciation rate per year

depr:{[c;r] c*1-r%100}
depr[100;8]
92
```

[Adverbs 10.0] 13. What is the value after 5 years?

```q
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

<a name="xeach></a>
### 🔴 15. x`each Problem Sets
[Top](#top)

[x each 15.1] VWAP: For each sym on 2023.09.07, retrieve only the prices that are greater than the VWAP price. Return all columns (use fby)

```q
select from trade where date=2023.09.07, price > ({x[`size] wavg x`price}; ([]size;price)) fby sym

/ return all columns = filter to come AFTER where clause
/ retrieves prices that are greater than the vwap price for each sym
/ "for each sym" = fby sym
/ VWAP calculated via the wavg function

/ syntax:
/ actually follows the fby syntax: price > (aggr;price) fby sym
/ except in this case, the aggr = vwap
/ and price = the table of ([] size;price)

/ so the function calculates the wavg for every size and price
/ and the x` iterates through every row in the table
```

[x each 15.2] GS Probem Set

```q
/ Given the Price and Input tables:

price: ([] date: 2021.01.21 2021.03.21 2021.09.21; ticker:`AAPL`AAPL`MSFT; exch: `US`UW`US; price: 10 20 30)

price:
date       | ticker | exch | price
--------------------------------
2021-01-21 |  AAPL  | US   | 10
2021-03-21 |  AAPL  | UW   | 20
2021-09-21 |  MSFT  | US   | 30

input: ([] ticker: `AAPL`AAPL`MSFT; start: 2021.01.01 2021.03.01 2021.06.01; end: 2021.03.01 2021.06.30 2021.08.01)

input:
ticker |   start    |    end
--------------------------------
AAPL   | 2021-01-01 | 2021-03-01
AAPL   | 2021-03-01 | 2021-06-30
MSFT   | 2021-06-01 | 2021-08-01
```

```q
/ 1. Create a function that queries the price table and returns the syms that match the start and end dates from input table

/ thought process:

/ you have 2 tables: price (table 1) and input (table 2)
/ you want to check if data from table 1 fall within specific parameters in table 2
/ first checks if [ticker] from [price] = [ticker] from [input]
/ then checks if [date] from [price] falls within [start/end] from [input] 
/ you need to query ENTIRE row from input table [sym + start + end]
/ then iterate through EACH row
```

Solution

```q
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

f2:{select from price where date within x`start`end, ticker in x`ticker}
raze f2 each input

/ the function:
/ f2 takes implicit argument x as the [input table]
/ remember, logic = column from table 1 vs input
/ so find where [date] from [price table] is within (start,end) from x (your input)
/ AND where [ticker] from [price table] matches [ticker] from x (your input)

/ calling your function:
/ so instead of 3 arguments, you only have one x
/ x is your entire input table
/ to iterate through EACH row of [input table], you have use [EACH]
/ you return a list of tables, so need RAZE to level it

/ oddly, these all work when calling your function

raze f2 each input
raze f2'[input]
f2[input]
```

[Top](#top)
