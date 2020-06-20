
Python libraries
Python core
	Os, sys, logging, re, datetime, contextlib, zipfile, shutil (for file), subprocess, math, json, csv, time, uuid, multiprocessing, traceback, platform, argparse, glob, xlrd, fnmatch, email, smtplib, typing, logging,
ThreadPoolExecutor,
Typedpy
Kafka-python

PyYAML
Requests
Pyodbc, sqlalchemy
Urllib3
Pymqi, CMQC (for mq)

Test: Click testing to test command line program

•	Python feature: interpreting script, dynamic typed, function/class is first class (as return, parameter)
•	Reverse a list: testlsit[::-1]
•	Randomize: random.shuffle(testlist)
•	For i in range(1, 10, -1): # loop in reverse order
•	Pickling and unpickling
•	Generators
•	*args, **kwargs
•	Re: split(), sub(), subn()
•	Delete file: os.remove(“xyz.txt”)
•	Built-in types: int, float, complex, str, Boolean, built-in functions
•	Global Interpreter Lock (GIL): similar to lock in java. Not real multithreading
•	Monkey patching: dynamic modification of a class or module at run-time
•	Access specifier: single underscore (private), double underscore (protected, like Java’s final)
•	object(): create a featureless object that is a base for all classes. No parameters.
•	Bubble sort in python
•	Produce start triangle
•	Fibonacci at n, and series to n
•	Check if number is prime
•	Check if a sequence is palindrome
•	Count the number of capital letters in a file
sum(1 for line in "just A test for This" for c in line if c.isupper())
•	Dogpile effect: when cache expires, multiple requests at the same time -> instances try to get the data to cache -> need a lock/semaphore to allow only one to get data to cache
•	
Python
Exchange variable values
print(f’this is good {varName}’)
Tuple unpacking 
Pass
enumerate(list)
Zip
Import random from shuffle
is vs == (similar to Javascript)

Scope: nolocal, global

String method
  find, capitalize, title, isipper, is alpha, 
Lamda

Decorators

counter.getCount() is the same as MyCounter.getCount(counter)
Class variable is like static variable in Java

issubclass

raise NameError(‘Hi there’)

Generator: yield, to produce list of values

zlib, re, Json, glob


https://www.python.org/downloads/windows/ 
Anaconda: 
spyder (for data science), pycharm (for web or large projects)
Anaconda is the leading open data science platform powered by Python. The open source version of Anaconda is a high performance distribution of Python and R and includes over 100 of the most popular Python, R and Scala packages for data science.
https://www.continuum.io/downloads#windows 
http://bbs.fishc.com/forum-243-1.html

Intellij
1.	Python plugin
2.	Settings/Editor/General/Auto Import
a.	Check “Add unambiguous imports on the fly
b.	Optimize imports on the fly

Visual Studio Code Plugins: 
1.	python -m pip install --user numpy scipy matplotlib ipython jupyter pandas sympy nose
2.	Intellij IDEA keybindings, Python Extension Pack, vscode-icons, 
3.	Python test exploer
>> from math import *
>> sqrt(9)
Basics
语句后没有分号
Alt + N/P (上一条/下一条命令)
>>>  5*3
>>> print(“hello” + “world”)
>>> 'str' 'ing'	# 自动拼接
>>> Print(“hello” * 8)
>>> print(“hello\n” + 8)  # TypeError, can’t convert int to string


Python没有变量，只有名字
# 单引号或者双引号都可以
Variable name rules
Must start with a letter or underscore
Must consist of letter, number or underscore
Case sensitive

Mnemonic variable names: >>> hours = 3.5
Cryptic: >>> a = 3.5
>> del a
Reserved words
And del for is raise assert elif from lambda return break else global not try class except if or while continue exec import pass yield def finally in print
 

转义
>>> print(‘let\’s go!’)

>>> print(‘c:\\work’)

#原始字符串
>>> str = r’c:\work’
>>> print(str)

Import random
Random.randint(1, 10) 	# 1~10之间的随机数

User input

>>> temp = input(“please input a number”)
>>> guess = int(temp)
>>> name = raw_input(‘Who are you?’)
>>> print ‘welcome ’, name



1.1.	 Basic data types
Int, float, Boolean, complex, e, string
(In Python3, long is merged to int, maximum 9 trillion)
Boolean： True ==1, False==0  # 注意首字符大写！
False: None, 0, 0.0, [], (), ‘’, “”, {}   # empty list, tuple, mapping are all false!!
>>> bool(0) # False

互相转换：int(a), float(a), str(a)
>>> type(a)
>>>isinstance(a, str) # no quotes on str

type(3L) # int and long, only limited by memory size. No leak issue for int.

# not like Java, no auto type conversion!!
>> “book price is $” + str(5.99) 

>>> float(3)

>>> sval=’123’
>>> int(sval)

支持浮点和复数
-4.78e-2 #type ‘float’
>>> a = 3.0+4.0j
>>> a.real
>>> a.imag
>>> a.conjugate()

在交互模式中，最后一个打印出来的表示会赋值给变量_
>>> round(_, 2)

>>> True + False  # 1


1.2.	 Operator
+, -, *, /, % (modular/remainder), ** (power), // (12//3 = 4, 12/3 = 4.0)
>>, <<, ~ & | ^
and, or, not
there is no ++, -- unlike in Java/Javascript!!

$ not(5 > 3) # False
抛弃了所有小数点的操作符//
>>> 3/2
>>> -3**2  #-9，注意优先级**更高

 

>>> 10 / 2	#5.0
>>> 10.0/2	#5.0

原始字符串操作符（r/R）
F = open(r’c:\python\test.py’, ‘w’)
F = open(’c:\\python\\test.py’, ‘w’)


Ternary operator
>>> small = x if x<y else y

>>> assert 3>4
# 条件为假时，程序崩溃并抛出AssertionError

Strings
Basic operations and functions
Index starts from 0
https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str 
>>> str1 = str1[:6] + ‘insert’ + str1[6:]	# [a:b], inclusive a, exclusive b
>>> str2.capitalize()	# 首字母大写
>>> casefold()
>>> str5.join(‘12345’) 	
len()
str(5) # convert int to string
str[index]

index = 0
while index < len(fruit)
	letter = fruit[index]
	index = index + 1

fruit = ‘banana’
for letter in fruit :
	print letter

# string is like list
>>> Parrot = “Norwegian Blue”
>>> print(parrot[3]
>>> print(parrot[0:6])
>>> print(parrot[0:6:2]) # from 0 to 5, skip every 2 -> Nre
>>> print(parrot[0::4]) # skip every 4 


>>> ‘n’ in ‘not’		# True, logical question

>>> If word = “banana”
>>> If word < “banana”		# True, word comes before “banana”

>>> greet = “Hello Bob”
>>> print greet.lower()

upper()
replace()
lstrip(), rstrip()	# remove white space, Java trim()
partition()
ljust(), rjust()
find(), rfind()
startswith()
count()
center()
isalnum()  # is alphanumeric
isalpha()

String formatting
print('''
Jan {2}
Feb {0}
Mar {2}
Apr {1}
'''.format(28, 30, 31))	# python3
formt_string %(arguments_to_convert)
print(‘there are %d punctuation marks. ‘ %(count))
print("This is {0} years old".format(100))

 

%5.2f #minimum 5 char wide, 2 digits
# Python 2
for i in range(1, 12):
    print("No. %2d square is %4d and cubed is %4d"%(i, i**2, i**3))

# Python 3
for i in range(1, 12):
    print("No. {0:2} square is {1:<4} and cubed is {2:<4}".format(i, i**2, i**3))
#0 => index, :2 number length

print("Pi is about {0:12.50}".format(22/7))



Def isHuiwen(sStr):
Return sStr === ‘’.join(reversed(sStr))
# cmp(sStr, ‘’.join(reversed(sStr))) == 0

Help(str.index)

 

capitalize()	  把字符串的第一个字符改为大写
  casefold()	  把整个字符串的所有字符改为小写
  center(width)	  将字符串居中，并使用空格填充至长度width的新字符串
  count(sub[,start[,end]])	  返回sub在字符串里边出现的次数，start和end参数表示范围，可选。
  encode(encoding='utf-8', errors='strict')	  以encoding指定的编码格式对字符串进行编码。
  endswith(sub[,start[,end]])	  检查字符串是否以sub子字符串结束，如果是返回True，否则返回False。start和end参数表示范围，可选。
  expandtabs([tabsize=8])	  把字符串中的tab符号（\t）转换为空格，如不指定参数，默认的空格数是tabsize=8。
  find(sub[,start[,end]])	  检测sub是否包含在字符串中，如果有则返回索引值，否则返回-1，start和end参数表示范围，可选。
  index(sub[,start[,end]])	  跟find方法一样，不过如果sub不在string中会产生一个异常。
  isalnum()	  如果字符串至少有一个字符并且所有字符都是字母或数字则返回True，否则返回False。
  isalpha()	  如果字符串至少有一个字符并且所有字符都是字母则返回True，否则返回False。
  isdecimal()	  如果字符串只包含十进制数字则返回True，否则返回False。
  isdigit()	  如果字符串只包含数字则返回True，否则返回False。
  islower()	  如果字符串中至少包含一个区分大小写的字符，并且这些字符都是小写，则返回True，否则返回False。
  isnumeric()	  如果字符串中只包含数字字符，则返回True，否则返回False。
  isspace()	  如果字符串中只包含空格，则返回True，否则返回False。
  istitle()	  如果字符串是标题化（所有的单词都是以大写开始，其余字母均小写），则返回True，否则返回False。
  isupper()	  如果字符串中至少包含一个区分大小写的字符，并且这些字符都是大写，则返回True，否则返回False。
  join(sub)	  以字符串作为分隔符，插入到sub中所有的字符之间。
  ljust(width)	  返回一个左对齐的字符串，并使用空格填充至长度为width的新字符串。
  lower()	  转换字符串中所有大写字符为小写。
  lstrip()	  去掉字符串左边的所有空格
  partition(sub)	  找到子字符串sub，把字符串分成一个3元组（pre_sub,sub,fol_sub），如果字符串中不包含sub则返回(‘原字符串’, ’’, ’’)
  replace(old,new[,count])	  把字符串中的old子字符串替换成new子字符串，如果count指定，则替换不超过count次。
  rfind(sub[,start[,end]])	  类似于find()方法，不过是从右边开始查找。
  rindex(sub[,start[,end]])	  类似于index()方法，不过是从右边开始。
  rjust(width)	  返回一个右对齐的字符串，并使用空格填充至长度为width的新字符串。
  rpartition(sub)	  类似于partition()方法，不过是从右边开始查找。
  rstrip()	  删除字符串末尾的空格。
  split(sep=None,  maxsplit=-1)	  不带参数默认是以空格为分隔符切片字符串，如果maxsplit参数有设置，则仅分隔maxsplit个子字符串，返回切片后的子字符串拼接的列表。
  splitlines(([keepends]))	  按照‘\n’分隔，返回一个包含各行作为元素的列表，如果keepends参数指定，则返回前keepends行。
  startswith(prefix[,start[,end]])	  检查字符串是否以prefix开头，是则返回True，否则返回False。start和end参数可以指定范围检查，可选。
  strip([chars])	  删除字符串前边和后边所有的空格，chars参数可以定制删除的字符，可选。
  swapcase()	  翻转字符串中的大小写。
  title()	  返回标题化（所有的单词都是以大写开始，其余字母均小写）的字符串。
  translate(table)	  根据table的规则（可以由str.maketrans(‘a’,‘b’)定制）转换字符串中的字符。
  upper()	  转换字符串中的所有小写字符为大写。
  zfill(width)	  返回长度为width的字符串，原字符串右对齐，前边用0填充。


Format
>>> “{a} love {b}.{c}”.format(a=”I”, b=”fishC”, c=”com”)
>>> “{{0}}”.format(“不打印”)
>>>’{0:.1f}{1}’.format(27.658, ‘GB’) # 27.7GB

>>> ‘%c %c %c’ %(97, 98, 99)
>>> ‘%s’ % ‘Here we go’


字符串格式化符号含义
  
   符   号	   说     明
     %c	   格式化字符及其ASCII码
     %s	   格式化字符串
     %d	   格式化整数
     %o	   格式化无符号八进制数
     %x	   格式化无符号十六进制数
     %X	   格式化无符号十六进制数（大写）
     %f	   格式化定点数，可指定小数点后的精度
     %e	   用科学计数法格式化定点数
     %E	   作用同%e，用科学计数法格式化定点数
     %g	   根据值的大小决定使用%f活%e
     %G	   作用同%g，根据值的大小决定使用%f或者%E
  
  
格式化操作符辅助指令
                                                 
   符   号	    说     明
     m.n	    m是显示的最小总宽度，n是小数点后的位数
       -	    用于左对齐
      +	    在正数前面显示加号（+）
       #	    在八进制数前面显示 '0o'，在十六进制数前面显示 '0x' 或 '0X'
       0	    显示的数字前面填充 '0' 取代空格

    
    
字符串转义字符含义
  
   符   号	    说     明
       \'	    单引号
       \"	    双引号
       \a	    发出系统响铃声
       \b	    退格符
       \n	    换行符
       \t	    横向制表符（TAB）
       \v	    纵向制表符
       \r	    回车符
       \f	    换页符
       \o	    八进制数代表的字符
       \x	    十六进制数代表的字符
       \0	    表示一个空字符
       \\	    反斜杠


>> from difflib import get_close_matches
>> get_close_matches(‘rainn’, [‘help’, ‘town’, ‘rain’])  # return [‘rain’]

1.3.	if, try
if (sky == ‘blue’) and \  # concate to 2nd line
    (sea == ‘blue’)

Test = ‘’’ no need to use line breaker with triple quotes
That’s right’’’
X = ‘today’; y = ‘tomorrow’; z = ‘later’;

If-elif-else
score = 80
if 100>= score >=90:
    print('A')
elif 90> score >=80:
    print('B')
else:
    print('error')

Indentation: important
Turn off tabs: NotePad++: Settings -> Preferences -> Language Menu/Tab Settings
If you mix tabs and spaces, you may get “indentation errors” even if everything looks fine.

Print(I, end=’’) # print on the same line

Try-except
遇到异常不会退出
if try works, except is skipped; otherwise jumps to except section
try:
	istr = int(astr)
except:
	istr = -1

Loops and Iteration
While: indefinite loops
>>> n=5
while n > 0:
	print n
	n = n – 1
print ‘Blastoff!’
print n

while True:
	if line == ‘done’:
		break
else:
	print(‘Happy ended’) # will not execute if go in “break”

k = 5
for i in range(1, 10):
    if k == 3:
        break
else:	# 正常结束时执行
print(i)

print(I, end=’ ’) # 1 2 3 4  # concatenate numbers

For: definite loops
>>> str=’fish’
>>> for I in str:
	print(I, end=’ ‘)
>>> for I in str:
	print(I, len(i))
>>> range(5)  # 0, …, 4
>>> range(2,9)  # list(range(2,9))


>>> for item in items:
>>> else:
	Print(“else in for loop”)

break, continue

# find the smallest value in a array
>>> smallest  = None
For value in [9, 41, 12, 3, 74, 15]
	If smallest is None:
		Smallest = value
	Elif value < smallest:
		Smallest = value
	Print smallest, value
Print ‘After’, smallest

Don’t overuse “is”, “is not” operator, don’t use “if I is 4”. “is” means exactly the same thing.

Augmented assignment: x += 2, in python than efficient than x = x + 2; but they are the same for Java

For in list
y = [x*x for x in range(10) if x%3==0]
print(y)
# [0, 9, 36, 81]

for long string:
input_promt = (“please enter something here, type it please”
                            “please do it carefully”)
# “\” works too, but not recommended.

Function
$ dir(__builtins__) # list all built in functions

def hello():
	‘apply operation + to argument’ # 函数说明, print(fn.__doc__)
	Print ‘Hello’
	Print ‘fun’

hello()

built-in functions such as raw_print() are treated as reserved words
>>> max(‘Hello world’)	# w
>>> min(‘Hello world’)	# e
>>> int()
>>> str()
>>> type()


>>> def greet(lang):
	If lang == ‘es’:	
		Print ‘Hola’
>>> greet(‘en’)
Lang is called “parameter”, ‘en’ is called argument

Function with returned value (fruitful)
>>> def greet():
	Return “hello”
>>> print greet(), “Glenn”

# similar to Slang
def f(a, b=1, c='hello'):
    global d # define a global variable
    return a + ' ' + c
print(f('good '))
print(f(a='good2', b=2))

function name can be passed as argument!

Multiple args
def joinStr(*args):  # * takes toule, ** takes dictionary
    text = ', '.join(args)
    print(text)

joinStr('test1', 'test3', 'test2')  # test1, test3, test2


Lamda
$ def addme(x, y):
	Return x+y
$ addme2 = lamda x,y: x+y
$ addme2(2,5)

Recursion
Fibonacci number
Hanoi problem
Exercise: 
4.编写一个找前5个默尼森数的程序。P是素数且M也是素数，并且满足等式M=2P（2的P次方）-1，则称M为默尼森数。例如，P=5，M=2P（2的P次方）-1=31，5和31都是素数，因此31是默尼森数。输出结果：
P      M
2      3
3      7
5      31
7      127
13     8191

for i in range(17):
    print("Binary of {0:>2} is {0:>8b}".format(i))

XOR can be used to reverse image

$ myiter = iter(‘test’)
$ print(next(myiter))

List序列
Collection
数组

>>> mix=[‘ad’, 2, [32, 2]] # any type is valid
>>> mix.append(‘adfas’)
>>> mix.extend([‘crazy’, ‘shaolin’])
>>> mix.insert(1, ‘mudan’)
>>> mix.remove(‘crazy’)
>>> del mix[1]
>>> str = mix.pop()  # return and remove最后一个元素

>>> word[0:2] #截取字符串
>>> word[:2] # 前2个
>>> word[2:] #除了前2个字符
>>> word[-1] # The last character
>>> word[-2] # The last-but-one character
>>> word[-2:] # The last two characters
>>> word[:-2] # Everything except the last two characters
>>> word[::-1] # reverse
>>> len(s)
>>> a = [‘spam’, ‘eggs’, 100, 1234]

>>> list1 = [123]
>>> list2 = [234]
>>> list1 > list2

>>> 123 in list1  # return True
>>> list[1][2]
>>> dir(list)
>>> list2.count(123)
>>> list2.index(123, 3, 7)	# 范围3到7
>>> list2.reverse()
>>> list2.sort()
>>> list2.sort().reserse()  	# list2.sort(reverse=True)

>>> list7 = list6[:]		# deep copy
>>> list8 = list6		# list8指向list6的同一个地址，shallow copy?

List Constants
>>> print [1, [5, 6], 7, ‘red’]
>>> print []
>>> friends = [‘joe’, ‘glen’, ‘sally’]

Range() returns a list of numbers
Range in python3 is a built-in type, in python2 is a function
>>>  range(len(frineds))

range(0, 5, 2) == range(0, 6, 2) # True
range(0, 100)[::-2] == range(99, 0, -2) # True
R = range(0, 100)
For i in r[::-2]:	// reversed, skip by 2
	Print(i) 

Backstring[::-1] # reverse a string

下面两个是一样的：
For friend in friends:
print ‘Happy New Year:’, friend

For I in range(len(friends)):
	print ‘Happy New Year: ’, friends[i]

xrange() is gone from python3

Concatnating lists using +
>>> a= [1, 2, 3]
>>> b = [4, 5, 6]
>>> c = a + b

del(a[2]) # remove element #2, this changes the list index!!

Slice lists
>>> t= [9, 41, 12, 3, 74, 15]
>>> t[:3] #0, 1, 2 element
>>> t[:]

>>> x = list()	# ie, x = []
>>> dir(x)
>>> 9 not in x		# True

Strings to Lists
>>> abc = ‘ with three     words’
>>> stuff = abc.split()	# split(‘;’)
>>> print stuff			# [‘with’, ‘three’, ‘words’]

“From stepehen.marquard@uct.ac.za Sat Jan 5 2008”
>>> words = line.split()
Email = words[1]		# email address
Pieces = email.split(‘@’)		# [‘stepehen.marquard’, ‘uct.ac.za’]
Print pieces[1]		# domain name

Append()
List(), iter(list), next(iter)
Len(a), max(b), min(), sum()
Sort()
>>> average = sum(num) / len(num)

If words[0] == [] : continue	# if len(words) < 1; if line == ‘’; 
If words[0] != ‘From’ : continue		# if there is empty line ([]), this will fail!

转换函数
List(), str(), Unicode(), basestring(), tuple()

序列类函数
Enumerate(), len(), max(), min()
Reversed(), sorted(), sum(), zip()

Test = range(10)
Test2 = test[::2] # == range(0, 10, 2)

Mylist.sort(), Mylist.pop(), mylist.pop(0), mylist.append()
Mylist.extend(anotherList)

for i,j in emuerate(week):
Print i+1, j # 1, Monday

Mylist.sort(reverse = true)
Mylist.sort(key = len)

列表解析
[i+1 for i in range(10) if i%2 == 0] # Out[42]: [1, 3, 5, 7, 9]
[(x+1, y+1) for x in range(2) for y in range(2)]
	# [(1,1), (1,2), (2,1), (2,2)]

Tuples元组

A, b = 2, 3
A, b = b, a # switch a and b
Pi, r = 3.14159, 3
Function much like a list, but immutable不能修改; it’s faster than list; prefer it if creating temporary list
Can’t do: sort(), append(), reverse()
>>> dir(list())
T = “a”, “b”, “c” # parenthesis is not required.
Print(t) # (‘a’, ‘b’, ‘c’)
>>> dir(tuple())
max(y)

title, artist, year = ‘a’, ‘b’, 3 # assigned separately, unpacking tuple

Tuples can be used as key in dictionary, and element in set, but list can not.

Tuple assignment
>>> (x, y) = (4, ‘fred’)
>>> x, y = (4, ‘fred’)		# () can be omitted
>>> print (d.items())	# it prints a list of tuples [(‘csev’, 2), (‘cwen’, 4)]
>>> for (k, v) in d.items():
		print k, v

(age, income) = "32,120000".split(',')

tuple is comparable
>>> (0, 1, 2) < (0, 3, 2)	# True, compare one by one
>>> (‘Jones’, ‘Sally’) < (‘Jones’, ‘Fred’)		# False

Sort lists of tuples by key
>>> d = {‘a’:10, ‘b’:1, ‘c’:22}
>>> t = d.items()
>>> t.sort()	# sort by keys
>>> t = sorted(d.items())
>>> for k, v in sorted(d.items()):		# built-in function sorted()
	Print k, v

The top 10 most common words
Fhand = open(‘romeo.txt’)
Counts = dict()
For line in fhand:
	Words = line.split()
	For word = words:
		Counts[word] = counts.get(word, 0) + 1

Lst = list()
For key, val in counts.items():
	Lst.append((val, key))
Lst.sort(reverse=True)
For val, key in lst[:10] :
	Print key, val

The top 10 most common words (shorter version)
>>> c = {‘a’:10, ‘b’:1, ‘c’:22}
>>> print sorted([(v, k) for k,v in c.items()])		# dynamically create a reversed tuples with (v, k), then sort it



Sort by values
>>> tmp = list()
>>> for k, v in c.items():
	Tmp.append((v, k))		# [(10, ‘a’), (22, ‘c’), (1, ‘b’)]
>>> tmp.sort(reverse=True)
>>> print tmp

>>> tuple1 = (1, 2, 3, 4, 5, 6)
>>> tuple1[1]
>>> temp = ()
>>> temp = (1,) 		# temp = (1) 只是Int, 不是tuple
>>> temp = 1,
>>> 8 * (8)	# 64
>>> 8 * (8,)	# (8, 8, 8, 8, 8, 8, 8, 8)
>>> temp = temp[:2] + (‘into’,) + temp[2:] 	#新建了一个元组
>>> del temp

列表、元组和字符串
1.	索引得到每一个元素
2.	从0开始
3.	通过片方法得到一个范围
4.	共同的操作符(append, 
5.	Lists are mutable (Strings are “immutable”)

Test = ([(1, ‘a’), (2, ‘b’)])
Test.append((3, ‘c’)) # if an element inside is a list, tuple can append!!


Tuple用途
映射类型中当作键使用
函数的特殊类型参数
Def func(args1, *argst):
Print args1
Print argst
Func(‘hello’, ‘wangdachui’, ‘Niuyun’, ‘LinLing’)
# Hello,
# (‘wangdachui’, ‘Niuyun’, ‘LinLing’)

作为很多内建函数的返回值
Enumerate(), coerce()
Def func():
    Return 1,2,3 # 返回tuple (1,2,3)


熟悉并自行构造小例子测试序列类型函数和方法的使用（鼓励做更多函数或方法的使用尝试）。
（1）序列类型函数
enumerate(), reversed(), sorted(), zip()
（2）字符串类型方法
join(), strip(), replace(), split(), translate(), startswith()
其中translate()需要使用maketrans()方法：
>>> z = str.maketrans(x,y) #in Python 2 from string import maketrans z = maketrans(x,y)
（3）列表类型方法
append(), count(), extend(), insert(), pop(), sort()

集合类型内建方法总结

  
集合（s）.方法名	等价符号	方法说明
s.issubset(t)	s <= t	子集测试（允许不严格意义上的子集）：s 中所有的元素都是 t 的成员
	s < t	子集测试（严格意义上）：s != t 而且 s 中所有的元素都是 t 的成员
s.issuperset(t)	s >= t	超集测试（允许不严格意义上的超集）：t 中所有的元素都是 s 的成员
	s > t	超集测试（严格意义上）：s != t 而且 t 中所有的元素都是 s 的成员
s.union(t)	s | t	合并操作：s "或" t 中的元素
s.intersection(t)	s & t	交集操作：s "与" t 中的元素
s.difference	s - t	差分操作：在 s 中存在，在 t 中不存在的元素
s.symmetric_difference(t)	s ^ t	对称差分操作：s "或" t 中的元素，但不是 s 和 t 共有的元素
s.copy()		返回 s 的拷贝（浅复制）
以下方法仅适用于可变集合		
s.update	s |= t	将 t 中的元素添加到 s 中
s.intersection_update(t)	s &= t	交集修改操作：s 中仅包括 s 和 t 中共有的成员
s.difference_update(t)	s -= t	差修改操作：s 中包括仅属于 s 但不属于 t 的成员
s.symmetric_difference_update(t)	s ^= t	对称差分修改操作：s 中包括仅属于 s 或仅属于 t 的成员
s.add(obj)		加操作：将 obj 添加到 s
s.remove(obj)		删除操作：将 obj 从 s 中删除，如果 s 中不存在 obj，将引发异常
s.discard(obj)		丢弃操作：将 obj 从 s 中删除，如果 s 中不存在 obj，也没事儿^_^
s.pop()		弹出操作：移除并返回 s 中的任意一个元素
s.clear()		清除操作：清除 s 中的所有元素

Dictionaries
List: a linear collection of values that stay in order
Dictionary: a “bag” of values, each with its own label
类似java的Map, HashMap
 
>>> purse = dict() # {}
>>> purse[‘money’] = 12 // purse.money is wrong
>>> purse[‘candy’] = 3
>>> jjj = {‘check’ : 1, ‘fred’ : 42,’jan’ : 100}

a1 = {}.fromkeys((‘t1’, ‘t2’, ‘t3’), 3000) #{‘t1’:3000, ‘t2’:3000, ‘t3’:3000}
sorted(a1) # [‘t1’, ‘t2’, ‘t3’]

aDict = dict(zip(aList, bList)) # 

It is an error to reference a key which is not in the dictionary; use “in” to check
>>> print(‘cserv’ in ccc)	# False
ccc.get(‘css’) # return None, better way to check

应用
Counts = dict()
names = [‘csev’, ‘cwen’, ‘csev’, ‘zqian’, ‘cwen’]
for name in names: 
	if name not in counts:
		Counts[name] = 1
	else:
		Counts[name] = counts[name] + 1
print counts

>>> print counts.get(name, 0)	# 0 is default value if name doesn’t exsit
上面的可以改成一个：
for name in names: 
	Counts[name] = counts.get(name, 0) + 1
print counts

update dict: mydict.update(newdata) # combine two dict

>>> newDict = mydict.copy()
>>> newDict.update(newdata) 

 
遍历dictionaries
for key in counts
	print key, counts[key]

>>> jjj = {‘check’ : 1, ‘fred’ : 42,’jan’ : 100}
>>> print list(jjj)
>>> print jjj.keys()
>>> print jjj.values()
>>> print jjj.items()		# list of key:value
>>> for aaa, bbb in jjj.items():	# two iteration variables
	Print aaa, bbb		# aaa is key, bbb is value

d = {'person': 2, 'cat': 4, 'spider': 8}
for animal, legs in d.iteritems():
    print 'A %s has %d legs' % (animal, legs)
print('cat' in d)	# True

可变长参数
 

$ testDict = {‘a’: 1, ‘b’: 2}
$ testDict.keys() # like a list, but it’s a view; if testDict is changed, this view will also change!!
$ testDict.values()
$ testDict.items() # entrySet in java

Set
NamesSet = set(namesWithDups) # will remove dups
namesSet2 = frozenset(namesWithDups) 

operators
比较 in, not in, ==, !=, 
< (子集), <=, > (超集), >=
       

emptySet = set() # can’t use {} which creates an empty dictionary
s.issubset(t) # <=
issuperset(t) # >=
union(t) # “|”,  there is no “+” operator for sets
intersection(t) # same as set1 & set2, set2.intersection(set1)
difference(t) # subtraction, or set1 – set2
symmetric_difference(t) # merge and remove the intersection, set1 ^ set2
difference_update() # remove, then merge
copy()

update(t)
intersection_update(t)
difference_update(t)
symmetric_difference_update(t)
add(obj)
remove(obj) # throw error if not found
discard(obj) # no error
pop()
clear()
frozenset() # immutable set

animals = {'cat', 'dog', 'fish'}
for idx, animal in enumerate(animals):
    print '#%d: %s' % (idx + 1, animal)

animals.copy()
animals.discard(2)  

Regular expressions
regex link:
http://deerchao.net/tutorials/regex/regex.htm
(2) 在线正则计算：
http://www.regexr.com/

Matching data
Import re		# import regular expressions libary
>>> if re.search(‘From:’, line):		# if line.find(‘From:’) >= 0: print line
	print line
>>> if re.search(‘^From:’, line):		# caret ^

^X.*:	# . can be any single character; * 0~any times
^X\S+:

Extracting data
>>> x = ‘My 2 favorite numbers are 19 and 42’
>>> y = re.findall(‘[0-9]+’, x)
>>> y = re.findall(‘[AEIOU]+’, x)

Greedy matching
The repeat characters (* and +) push outward in both directions (greedy) to match the largest possible string; “?” means “stop at the first”.
>>> x = “From: Using the: character’
>>  y = re.finall(‘^F.+:’, x)		# From: Using the:
>>  y = re.finall(‘^F.+?:’, x)		# From: 

Exact extraction
>>> x = ‘From stephen.marquard@uct.ac.za Sat Jan 2008’
>>> y = re.findall(‘\S+@\S+’, x)	# email address
>>> y = re.findall(‘^From (\S+@\S+)’, x)		# match the re, but only extrat what’s in the (), 

>>> y = re.findall(‘@([^ ]*)’, x)		#[^ ] means non-blank; print “uct.ac.za”
>>> y = re.findall(‘^From .*@([^ ]*)’, x)

>>> stuff = re.finall(‘^X-DSPAM-Confidence: ([0-9.]+)’, line)	# return a list of numbers
>>> if len(stuff) != 1 : continue

 

Class
class boy:
    gender='male'
    interest='girl'
def __init__(self, name):
    self.name = name
    def say(self):
	self.gener = ‘female’
        return 'i am a boy'

peter=boy()
print(peter.gender)
print(peter.say())

Inheritance
class AsianBoy(Boy):  # inheritance
	def __init__(self, name):
		super().__init__(name=name, lives=1)
  
class Dog(object):
def __init__(self, name):  # similar constructor
    self.name = name
    print “Hi, I am called %s.” % self.name
if __name__ == ‘__main__’:
dog = Dog(“Sara”)
dog.greet()

支持多继承

双下划线__ (private view scope)
__var 属性会被__classname_var替换，防止父类与子类中的同名冲突
单下划线_ (package view scope)
防止模块的属性用 “from mymodule import *”来加载


$ Kettle.switch_on(kenwood)  // like a static method in Java
$ print(kenwood.on)

@staticmethod



@property
Def score(self):
	Return self._score
@score.setter
Def score(self, score):
	self._score = score


overloading isn’t possible in Python and isn’t necessary

Polymorphism
class Animal():
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        raise NotImplementedError("Subclass must implement this abstract method")

class Dog(Animal):
    def speak(self):
        print(self.name + 'says woof!')


magic/dunder methods
__init__(self)
__str__(self)  # like Java toString():
	return f’{self.title} by {self.author}’
__len__(self):
	return self.pages
__del__(self):
	Print(‘A book is deleted’)



File and Network
Read File
Open() returns a “file handle”; handle = open(filename, mode); 
>>> xfile = open(‘mbox.txt’, ‘r’)

\n: newline, is one character

Count  = 0
for line in xfile:
	count = count + 1
	if line.startswith(‘From:’):
		line = line.rstrip()	# \n is counted as white space, this way remove newline
		print line		# will print a newline
	if not line.startswith(‘From:’):
		continue
	if not ‘@uct.ac.za’ in line:
		continue
	print line		# print every line in the file

>>> inp = xfile.read()	# read in the whole file
>>> print len(inp)
>>> print inp[:20]		# the first 20 characters


testFile = open(‘c:\\test.txt’, mode=’r+’)
testFile.close()
with open(‘c:\\test.txt’, mode=’r’) as foo # no need to close file, handles error
	print(foo.readlines)
	Imelda = eval(content) # convert tuple string to tuple objec

f.read(), f.write(), f.readline(), f.readlines() (read as list), f.writelines(), f.close(), f.seek()
f.tell() # check file pointer
f.see(offset, whence=0) # 0 head, 1 current, 2 end

Write File
with open(‘c:\\test.txt’, ‘w’) as testfile:
	print(city, file=testfile) // save to filename testfile, default flush data is false

bin_file.write(bytes(range(17)) # write into a binary file
bin_file.write(a.to_bytes(2, ‘big’)) # convert to bytes with 2 bytes

print(‘Adelaide’.strip(‘del’)) # Adelai, removed “de” at the end
Append File
with open('./fileappenddemo.txt', 'a') as tables:
    for i in range(2, 13):
        for j in range(1, 13):
            print('{1:>2} times {0} is {2}'.format(i, j, i*j), file=tables)
        print('-' * 20, file=tables)

Pickle
Serialization for Java

// read objects must the same the order as write
import pickle
imelda = ('More Myhem', 'Imelda May', '2011',
    ((1, 'Pulling the Rug'),
    (2, 'Psycho'),
    (3, 'Mayhem')))
even = [1, 2, 3]
with open('imdelda.pickle', 'wb') as picklefile:
    pickle.dump(imelda, picklefile)
    pickle.dump(even, picklefile)

with open('imdelda.pickle', 'rb') as picklefile2:
    imelda2 = pickle.load(picklefile2)
    even2 = pickle.load(picklefile2)

print(imelda2)

bin_file.write(a.to_bytes(2, 'big'))
e = int.from_bytes(bin_file.read(2), 'big'))

Shelve
Can load partial serialized data
Import shelve
with shelve.open(‘shelvetest’) as fruit:  # will be saved as fruit.db
	fruit = {‘orange’: ‘sweet’, ‘apple’: ‘good for making cider’, ‘lemon’: ‘sour’} # like a dictionary
# outside of with, file is closed

OS module
2. Python的os模块提供了执行文件和目录处理操作的函数，例如重命名和删除文件。
要使用这个模块，你必须先导入它，然后才可以调用相关的各种功能。
import os
试一试以下的函数，理解它们的功能。
os.rename(current_file_name, new_file_name) #文件重命名
os.remove(file_name) #删除文件
os.mkdir(newdir) #创建目录
os.chdir(newdir) #改变目录
os.getcwd() #获得当前路径
os.rmdir(dirname) #删除目录
Network data
Urllib, urllib2, httplib, httplib2
Import urllib
R = urllib.urlopen(‘http://z.cn/’)
Html = r.read()
M = r.findall(“<tr><td class=\”>)

import requests
import re

def retrieve_dji_list():
    r = requests.get('http://money.cnn.com/data/dow30/')
    search_pattern = re.compile('class="wsod_symbol">(.*)<\/a>.*<span.*">(.*)<\/span>.*\n.*class="wsod_stream">(.*)<\/span>')
    dji_list_in_text = re.findall(search_pattern, r.text)
    return dji_list_in_text

dji_list = retrieve_dji_list()
print(dji_list)

if(os.path.exists(s))
listing = os.walk(‘.’)
for root, directories, files in listing:


nonlocal varName # not global, but in the enclosing scope
global varName
Modules and Imports
modules
Avoid using “from turtle import *”
Print(dir(shelve)) # list of functions for shelve 
Help(rand.randint)


webbrowser
Import webbrowser
webbrowser.open(‘https://www.python.org’)
help(webbrowser)

Time and DateTime
import time
from time import time as timer #monotonic, perf_counter
import random
print(time.gmtime(0))
print(time.localtime())
print(time.time())

waittime = random.randint(1, 6)
time.sleep(waittime)
starttime = timer()
print('started at ' + time.strftime('%X', time.localtime(starttime)))

python timezone library: pytz
$ pip install pytz
Timezone data source: inan.org/time-zones
Localtime -> save in UTC time -> display as localtime
Tkinter
GUI library


Database
SQLite: android built-in; python supported/built-in; from 2000, standalone
Stored in a single file


Create, Insert, Query

import sqlite3
db = sqlite3.connect('contacts.sqlite')
db.execute('CREATE TABLE IF NOT EXISTS contacts(name TEXT, phone INTEGER, email TEXT, price REAL)')
db.execute('INSERT INTO contacts(name, phone, email) VALUES("Tim", 6545678, "tim@gmail.com)')
# db.close()

cursor = db.cursor
cursor.execute('SELECT * FROM contacts')
for row in cursor:
    print(row)
cursor.close()
db.close()


Cursor, Transactions
############### without cursor
for row in db.execute('SELECT * FROM contacts'):
    print(row)

update_sql = 'UPDATE contacts SET email = "updated@gmail.com"'
update_cursor = db.cursor()
update_cursor.execute(update_sql)
print(f'{update_cursor.rowcount} rows updated')
update_cursor.connection.commit()

update_cursor.close()
for name, phone, email in db.execute('SELECT * FROM contacts'):
    print(name)
    print(phone)
    print(email)
    print('-' * 20)
db.close()

Placeholders and parameter subsitution
update_sql2 = 'UPDATE contacts SET email = ? WHERE phone = ?'
update_cursor.execute(update_sql2, (new_email, phone))

PostGreSQl, MySql
>> pip install psycopg2
>> pip install mysql-connector
con = mysql.connector.connect(
    user="ardit700_student", 
    password = "ardit700_student", 
    host="108.167.140.122", 
    database = "ardit700_pm1database"
)

Exception

try:
print('something')
db.execute(‘update …’)
db.execute(‘update …’)
except RecursionError:
print('something is wrong')
db.rollback()
//sys.exit(2)
else:
    pass
finally:
    print('do it no matter what happened')



Comprehension and Lamda


Generators and yield, next and ranges

# Fibinacci number
def fibinacci():
    current, previous = 0, 1
    while True:
        current, previous = current + previous, current
        yield current

fib = fibinacci()

for i in range(10):
    print(next(fib))

# create pi
import math

def oddNumber():
    current = 1
    while True:
        current += 2
        yield current

pi = 1
nextOdd = oddNumber()
for i in range(1, 10):
    val = next(nextOdd)
    print(f'next odd is {val}')
    pi += (-1)**i / val

print(pi*4)

os.walk Generator
import os
import fnmatch
# import id3reader_p3 as id3reader
root = '.'

for path, directories, files in os.walk(root, topdown=True):
    print(path)
    for f in files:
        print(f'{f}')


import os
import fnmatch
import id3reader_p3 as id3reader

def find_music(start, extension):
    for path, dir, files in os.walk(start):
        for file in fnmatch.filter(files, '*.{}'.format(extension)):
            absPath = os.path.abspath(path)
            yield os.path.join(absPath, file)

musicFiles = find_music('music', 'mp3')

for f in musicFiles:
    id3r = id3reader.Reader()
    print('Artist: {}, Album: {}, Track: {}, Song: {}'.format(
        id3r.get_value('performer'),
        id3r.get_value('album'),
        id3r.get_value('track'),
        id3r.get_value('title')
    ))

List Comprehensions
testlist = [x*x for x in range(10) if x % 2 == 0]

text = '-'.join(args)
text = '-'.join(str(arg) for arg in args)  # convert some int to str, generator
text = '-'.join([str(arg) for arg in args]) # same, comprehensions

meals = [meal if 'spam' not in meal else 'a meal skipper' for meal in menu]

# nested comprehension
for meals in [(burger, topping) for burger in burgers for topping in toppings]:
    print(meals)

# this is the same as:
for burger in burgers:
    for topping in toppings:
        print((burger, topping))

for nested_meals in [[(burger, topping) for burger in burgers] for topping in toppings]:
    print(nested_meals)

Dict comprehension
{x:x**2 for x in range(10)}  # {0: 0, 1: 1, 2: 4, 3: 9… 10: 100}
{k:v**2 for k,v in zip([‘a’, ‘b’], range(2))} # {a: 0, b: 1}

timeit
module to measure execution time
import statistics
sqrt, mean, stdev

Lint and unit test

Pylint

import unittest
import basic

class TestBasic(unittest.TestCase):
    def test_one_word(self):
        text = 'python'
        result = basic.capText(text)
        self.assertEqual(result, 'Python')

if __name__  == '__main__':
    unittest.main()



pytest
https://semaphoreci.com/community/tutorials/testing-python-applications-with-pytest 
import pytest
from LC929_UniqueEmailAddresses import Solution

@pytest.fixture
def testObj():
    return Solution()

def test_processEmail(testObj):
    assert testObj.processEmail('test.email+alex@leetcode.com') == 'testemail@leetcode.com'

def test_numUniqueEmails(testObj):
    testEmails = ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
    assert testObj.numUniqueEmails(testEmails) == 2





Numpy
Windows CMD: >> pip install numpy
import numpy as np
print(np.version.full_version)

array
a = np.arange(20) # list 里必须同类型
a.reshape(2,2,5)
a.ndim, .shape, size, dtype, dsize
raw = [0,1,2,3,4]
a = np.array(raw) # convert list to array

np.zeros((4,5))
np.ones((4,5), dtype=int)
np.full((2,2), 7) # constant array
np.eye(2) # diagonal are 1
np.random.rand(5) # array([ 0.45681137,  0.74852765,  0.1659447 ,  0.68798561,  0.38209482])
A slice of an array is a view into the same data, so modifying it will modify the original array.

a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
row_r1 = a[1, :]    # Rank 1 view of the second row of a  
row_r2 = a[1:2, :]  # Rank 2 view of the second row of a
row_r3 = a[[1], :]  # Rank 2 view of the second row of a

integer array indexing??

简单的四则运算已经重载过了，全部的'+'，'-'，'*'，'/'运算都是基于全部的数组元素的
类似C++，'+='、'-='、'*='、'/='操作符在NumPy中同样支持

.exp(), .sqrt(), .square(), .power()

a = np.arange(20).reshape(4,5)
np.arange(10).reshape(3,3)
print "a:"
print a
print "sum of all elements in a: " + str(a.sum())
print "maximum element in a: " + str(a.max())
print "minimum element in a: " + str(a.min())
print "maximum element in each row of a: " + str(a.max(axis=1))
print "minimum element in each column of a: " + str(a.min(axis=0))

Note that unlike MATLAB, * is elementwise multiplication, not matrix multiplication. We instead use the dot function to compute inner products of vectors
v.dot(w), np.dot(v, w)

matrix
a = np.arange(20).reshape(4, 5)
a = np.asmatrix(a)
print type(a)
b = np.arange(2, 45, 3).reshape(5, 3)
b = np.mat(b)
print b

b = np.matrix('1.0 2.0; 3.0 4.0')
print type(b)

np.linspace(0, 2, 9) # array([ 0.  ,  0.25,  0.5 ,  0.75,  1.  ,  1.25,  1.5 ,  1.75,  2.  ])

print a[0][1]
print a[0, 1]

b = a
b = a.copy() # deep copy

a[:, [1,3]] # pick column 1 and 3

a[:, 2][a[:, 0] > 5]

loc = numpy.where(a==11)
print loc
print a[loc[0][0], loc[1][0]]

a.T
a = np.transpose(a) # 转置

import numpy.linalg as nlg
ia = nlg.inv(a) # 逆矩阵
eig_value, eig_vector = nlg.eig(a) 

np.column_stack((a,b)) #按列拼接两个向量成一个矩阵

NumPy提供nan作为缺失值的记录，通过isnan判定
a[0,1] = np.nan
np.isnan(a)

np.nan_to_num(a)  #将nan替换成0

想详细了解可参考链接
http://wiki.scipy.org/Numpy_Example_List
http://docs.scipy.org/doc/numpy

matrix operations
# baseball is available as a regular list of lists
# updated is available as 2D numpy array

# Import numpy package
import numpy as np

# Create np_baseball (3 cols)
np_baseball = np.array(baseball)

# Print out addition of np_baseball and updated
print(np_baseball + updated)

# Create numpy array: conversion
conversion = np.array([0.0254, 0.453592, 1])

# Print out product of np_baseball and conversion
print(np_baseball * conversion)


Broadcasting
# We will add the vector v to each row of the matrix x,
# storing the result in the matrix y
x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
v = np.array([1, 0, 1])
y = x + v  # Add v to each row of x using broadcasting

Broadcasting two arrays together follows these rules:
1.	If the arrays do not have the same rank, prepend the shape of the lower rank array with 1s until both shapes have the same length.
2.	The two arrays are said to be compatible in a dimension if they have the same size in the dimension, or if one of the arrays has size 1 in that dimension.
3.	The arrays can be broadcast together if they are compatible in all dimensions.
4.	After broadcasting, each array behaves as if it had shape equal to the elementwise maximum of shapes of the two input arrays.
5.	In any dimension where one array had size 1 and the other array had size greater than 1, the first array behaves as if it were copied along that dimension
If this explanation does not make sense, try reading the explanation from the documentation or this explanation.
Functions that support broadcasting are known as universal functions. You can find the list of all universal functions in the documentation.



# 打印99乘法表
Def fun(x,y):
Return (x+1)*(y+1)
Arr = np.fromfunction(fun, (9,9))

Ufunc函数
Written in C, 10x faster than build-in; operate each element in matrix
basic statistics
np.mean, np.median, np.corrcoef, np.std
sum, sort

# np_baseball is available, [height, weight, age]

# Import numpy
import numpy as np

# Create np_height from np_baseball
np_height = np_baseball[:, 0]

# Print out the mean of np_height
print(np.mean(np_height))

# Print out the median of np_height
print(np.median(np_height))

# Print out correlation between first and second column. Replace 'None'
corr = np.corrcoef(np_baseball[:,0], np_baseball[:,1])
print("Correlation: " + str(corr))

# Heights of the goalkeepers: gk_heights
gk_heights = np_heights[np_positions == 'GK']

# Heights of the other players: other_heights
other_heights = np_heights[np_positions != 'GK']

# Print out the median height of goalkeepers. Replace 'None'
print("Median height of goalkeepers: " + str(np.median(gk_heights)))

# Print out the median height of other players. Replace 'None'
print("Median height of other players: " + str(np.median(other_heights)))

stack & split
np.hstack((im1, im2))  # stack horizontally
np.vstack((im1, im2)) # stack vertically
np.hsplit(im1, 3)  # equally split into 3 arrays horizontally
np.vsplit(im1, 2) 

SciPy
import numpy as np
import scipy.stats as stats
import scipy.optimize as opt

Random number and distributions
http://docs.scipy.org/doc/scipy/reference/stats.html
rv_unif = stats.uniform.rvs(size=10)
print rv_unif
rv_beta = stats.beta.rvs(size=10, a=4, b=2)
print rv_beta
np.random.seed(seed=2015)

Sample test
norm_dist = stats.norm(loc=0.5, scale=2)
n = 200
dat = norm_dist.rvs(size=n)
print "mean of data is: " + str(np.mean(dat))
print "median of data is: " + str(np.median(dat))
print "standard deviation of data is: " + str(np.std(dat))

检验这一组数据是否服从假设的分布，如正态分布
mu = np.mean(dat)
sigma = np.std(dat)
stat_val, p_val = stats.kstest(dat, 'norm', (mu, sigma))
print 'KS-statistic D = %6.3f p-value = %6.4f' % (stat_val, p_val)

检验这组数据的均值是不是0。典型的方法是t检验（t-test）
stat_val, p_val = stats.ttest_1samp(dat, 0)
print 'One-sample t-statistic D = %6.3f, p-value = %6.4f' % (stat_val, p_val)

双样本，检测均值是否相等
norm_dist2 = stats.norm(loc=-0.2, scale=1.2)
dat2 = norm_dist2.rvs(size=n/2)
stat_val, p_val = stats.ttest_ind(dat, dat2, equal_var=False)
print 'Two-sample t-statistic D = %6.3f, p-value = %6.4f' % (stat_val, p_val)

stats还提供其他大量的假设检验函数，如bartlett和levene用于检验方差是否相等；anderson_ksamp用于进行Anderson-Darling的K-样本检验等。

其他函数
有时需要知道某数值在一个分布中的分位，或者给定了一个分布，求某分位上的数值。这可以通过cdf和ppf函数完成：
g_dist = stats.gamma(a=2)
print "quantiles of 2, 4 and 5:"
print g_dist.cdf([2, 4, 5])
print "Values of 25%, 50% and 90%:"
print g_dist.pdf([0.25, 0.5, 0.95])

对于一个给定的分布，可以用moment很方便的查看分布的矩信息，例如我们查看N(0,1)的六阶原点矩：
stats.norm.moment(6, loc=0, scale=1)
norm_dist = stats.norm(loc=0, scale=1.8)
dat = norm_dist.rvs(size=100)
info = stats.describe(dat)
print "Data size is: " + str(info[0])
print "Minimum value is: " + str(info[1][0])
print "Maximum value is: " + str(info[1][1])
print "Arithmetic mean is: " + str(info[2])
print "Unbiased variance is: " + str(info[3])
print "Biased skewness is: " + str(info[4])
print "Biased kurtosis is: " + str(info[5])

当我们知道一组数据服从某些分布的时候，可以调用fit函数来得到对应分布参数的极大似然估计（MLE, maximum-likelihood estimation）。以下代码示例了假设数据服从正态分布，用极大似然估计分布参数：
norm_dist = stats.norm(loc=0, scale=1.8)
dat = norm_dist.rvs(size=100)
mu, sigma = stats.norm.fit(dat)
print "MLE of data mean:" + str(mu)
print "MLE of data standard deviation:" + str(sigma)

pearsonr和spearmanr可以计算Pearson和Spearman相关系数，这两个相关系数度量了两组数据的相互线性关联程度

linear regression
x = stats.chi2.rvs(3, size=50)
y = 2.5 + 1.2 * x + stats.norm.rvs(size=50, loc=0, scale=1.5)
slope, intercept, r_value, p_value, std_err = stats.linregress(x, y)
print "Slope of fitted model is:" , slope
print "Intercept of fitted model is:", intercept
print "R-squared:", r_value**2


StatsModels（http://statsmodels.sourceforge.net ）模块提供了更为专业，更多的统计相关函数。若在SciPy没有满足需求，可以采用StatsModels。


Optimization
假设考虑的问题全部是凸优化问题，即目标函数是凸函数
参考斯坦福大学Stephen Boyd教授的教材convex optimization，下载链接：http://stanford.edu/~boyd/cvxbook

Pandas
import pandas as pd
pd.__version__
import numpy as np
from pandas import Series, DataFrame
Series
与Array区别：有index
a = np.random.randn(5) # a is an array
s = Series(a)
s = Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'], name='my_series')

d = {'a': 0., 'b': 1, 'c': 2} # dictionary
s = Series(d)

Series(d, index=['b', 'c', 'd', 'a']) 
S[0], s[:2] # first 2 elem
S[2,0,4] # the 2, 0, 4th elem
S[‘e’, ‘I’]
S[s > 0.5]
‘e’ in s # False

Series1 + series2 # 合并两个series

Series 对象本身及其索引均有一个name属性。
Series的那么属性与其他重要功能关系密切。
DataFrame
将数个Series按列合并而成的二维数据结构, 以列作为操作的基础的
d = {'one': Series([1., 2., 3.], index=['a', 'b', 'c']), 'two': Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
df = DataFrame(d)
d = {'one': [1., 2., 3., 4.], 'two': [4., 3., 2., 1.]}
df = DataFrame(d, index=['a', 'b', 'c', 'd'])

d = {'one': [1., 2., 3., 4.], 'two': [4., 3., 2., 1.]}
df = DataFrame(d)
df = DataFrame() # empty dataframe


a = Series(range(5))
b = Series(np.linspace(4, 20, 5))
df = pd.concat([a, b], axis=1) # axis=1表示按列进行合并，axis=0表示按行合并

print df[1]
df.columns = ['a', 'b', 'c', 'd', 'e']
del df[‘pay’]

print df['b']	# type is Series
print df.b
print df[[‘a’, ‘d’]] # get 2 columns, type is DataFrame
print df['b'][2] # column ‘b’, row 2
print df['b']['gamma']
print df.iloc[1]	# get row 1
print df.loc['beta'] # get row called ‘beta’
print df[1:3] # row 1 and 2
bool_vec = [True, False, True, True, False]
print df[bool_vec] # row 0, 2, 3

print df[['b', 'd']].iloc[[1, 3]]
print df.iloc[[1, 3]][['b', 'd']]
print df[['b', 'd']].loc[['beta', 'delta']]
print df.loc[['beta', 'delta']][['b', 'd']]

print df.iat[2, 3]
print df.at['gamma', 'd']
print df.ix['gamma', 4]
print df.ix[['delta', 'gamma'], [1, 4]] # 混合索引和下标，注意要一致
print df.ix[[1, 2], ['b', 'e']]


pd.set_option('display.width', 200) #设置一下输出屏幕的宽度

dates = pd.date_range('20150101', periods=5)
df = pd.DataFrame(np.random.randn(5, 4),index=dates,columns=list('ABCD'))

只要是能转换成Series的对象，都可以用于创建DataFrame：
df2 = pd.DataFrame({ 'A' : 1., 'B': pd.Timestamp('20150214'), 'C': pd.Series(1.6,index=list(range(4)),dtype='float64'), 'D' : np.array([4] * 4, dtype='int64'), 'E' : 'hello pandas!' })


df.head() # first 5 rows
df.tail(3) # last 3 rows
df.describe() # count, mean, std, min, 25%, 50%, 75% max
print df.sort_index(axis=1, ascending=False).head() # Order by column names, descending
print "Order by column value, ascending:"
print df.sort(columns='tradeDate').head()
print "Order by multiple columns value:"
df = df.sort(columns=['tradeDate', 'secID'], ascending=[False, True])

print df.iloc[1:4][:] # rows 1,2,3 with all columns
print df[df.closePrice > df.closePrice.mean()].head() #收盘价在均值以上的数据
print df[df['secID'].isin(['601628.XSHG', '000001.XSHE', '600030.XSHG'])].head()

df['openPrice'][df['secID'] == '000001.XSHE'] = np.nan # change data

dataframe.dropna() # Drop all rows that have any NaN values
print df.dropna(thresh=6).shape # Drop rows who do not have at least six values that are not NaN
df.dropna(subset=['closePrice']) # Drop only if NaN in specific column


print df.fillna(value=20150101).head() # fill data for na

print df.mean(0) # mean on columns; df.mean(1) -> mean on rows
print df['closePrice'].value_counts().head()

print df[['closePrice']].apply(lambda x: (x - x.min()) / (x.max() - x.min())).head()

dat = dat1.merge(dat2, on=['secID', 'tradeDate']) # 合并数据, sql 查询表dat1, dat2

df.sort_values([‘Years Experience’])
degree_counts = df[‘Level of Education’].value_counts()
degree_counts.plot(kind = ‘bar’)

df_grp = df.groupby('secID')
grp_mean = df_grp.mean()
print grp_mean

#取每只股票的最新数据
df2 = df.sort(columns=['secID', 'tradeDate'], ascending=[True, False])
print df2.drop_duplicates(subset='secID')
print df2.drop_duplicates(subset='secID', take_last=True) #若想要保留最老的数据，可以在降序排列后取最后一个记录

中国石化一月的收盘价进行绘图，其中set_index('tradeDate')['closePrice']表示将DataFrame的'tradeDate'这一列作为索引，将'closePrice'这一列作为Series的值，返回一个Series对象，随后调用plot函数绘图，更多的参数可以在matplotlib的文档中查看
dat = df[df['secID'] == '600028.XSHG'].set_index('tradeDate')['closePrice']
dat.plot(title="Close Price of SINOPEC (600028) during Jan, 2015")
 


数据处理
Retrieve stock historical data
Matplotlib.mpl_finance
https://github.com/matplotlib/mpl_finance
自然语言工具包NLTK
from nltk.corpus import Gutenberg
import nltk
print Gutenberg.fileids()

数据准备
Quotesdf = pd.DataFrame(quotes, index=range(1, len(quotes)+1), columns=fields)

From datetime import date
From datetime import datetime

x = date.fromordinal(735190)
y = datetime.strftime(x ‘%Y-%m-%d’) #转换成固定格式

dates = pd.date_range('20141001', periods=7)


数据显示
Df.index
Df.columns
Df.values
Df.describe

Df[u’2013-12-02’:u’2013-12-06’] #get rows based on index
Df[‘code’] # but NOT df[‘code’, ‘price’] => loc
Df.loc[1:5,]
Df.loc[1:5, [‘code’, ‘lasttrade’]]
Df.iloc[1:5, [0,2]] # row 1~5, column 0 and 2 
Df.[df.index >= u’2014-01-01’] 
Df.[df.index >= u’2014-01-01’ & (df.close >= 95)] # 2014年后close price > 95

Df.mean(columns = ‘lasttrade’) #最近一个成交价的平均值
Df[df.lasttrade >= 120].name #最近一次成交价>=120的公司名称
Len(df[df.close > df.open]) # 最近一年涨的天数

数据选择
#最近一年相邻两天收盘价的涨跌情况
Status = np.sign(np.diff(df.close))
Status[np.where(status==1.)].size    #涨的天数
Status[np.where(status==-1.)].size   #跌的天数

#前三
Df.sort(columns=’lasttrade’)[27:].name

#2014年1月的开盘天数
Len(df[(df.index>=’2014-01-1’) & (df.index<’2014-02-01’)])

#统计近一年每个月的开盘天数
Import time
Listtemp = []
For I in range(0, len(df)):
Temp = time.strptime(df.index[i], “%Y-%m-%d”)
Listtemp.append(temp.tm_mon)
Print listtemp
Tempdf = df.copy()
Tempdf[‘month’] = listtemp    #增加一列
Print(tempdf[‘month’].value_counts()

简单处理, grouping
#或者用grouping
Tempdf.groupby(‘month’).count().month
 

#近一年每个月的总成交量
Tempdf.groupby(‘month’).sum().volume
#先得到volume再求和
Tempdf.groupby(‘month’)[‘volume’].sum()

Merge
Append, concat, merge (join)
Params: left, right, how, on, left_on, right_on, left_index, right_index, sort, suffixes, copy
 

 

 

练习：MSFT 2015第一季度股票收盘价的平均值
	from matplotlib.finance import quotes_historical_yahoo_ochl
from datetime import date
import pandas as pd
today = date.today()
start = (today.year-2, today.month, today.day)
quotesMS = quotes_historical_yahoo_ochl('MSFT', start, today)
attributes=['date','open','close','high','low','volume']
quotesdfMS = pd.DataFrame(quotesMS, columns= attributes)
list = []
for i in range(0, len(quotesMS)):
    x = date.fromordinal(int(quotesMS[i][0]))
    y = date.strftime(x, '%y/%m/%d')
    list.append(y)
quotesdfMS.index = list
quotesdfMS = quotesdfMS.drop(['date'], axis = 1)
list = []
quotesdfMS15 = quotesdfMS['15/01/01':'15/12/31']
for i in range(0, len(quotesdfMS15)):
    list.append(int(quotesdfMS15.index[i][3:5])) #get month just like '02'
quotesdfMS15['month'] = list
print(quotesdfMS15.groupby('month').mean().close)


Q Quant
 

Matplotlib
import numpy as np
import pylab as pl
t = np.arange(0., 4., 0.1)
pl.plot(t,t, t,t+2, t,t**2)

图像属性控制
plt.plot(x, y, ‘g--‘) # green, dashed
plt.plot(x, y, ‘rD’) # red, diamond
 
 

plt.subplot(211)
plt.subplot(212)




# Print the last item from year and pop
print(year[-1])
print(pop[-1])

# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Make a line plot: year on the x-axis, pop on the y-axis
plt.plot(year, pop)

# Display the plot with plt.show()
plt.show()


plt.scatter(x,y)

# Put the x-axis on a logarithmic scale
plt.xscale('log')


# Create histogram of life_exp data
plt.hist(life_exp, bins=5)
plt.clf() # clear graph
# Display histogram
plt.show()

# Strings
xlab = 'GDP per Capita [in USD]'
ylab = 'Life Expectancy [in years]'
title = 'World Development in 2007'

# Add axis labels
plt.xlabel(xlab)
plt.ylabel(ylab)

# Add title
plt.title(title)

# Definition of tick_val and tick_lab
tick_val = [1000,10000,100000]
tick_lab = ['1k','10k','100k']

# Adapt the ticks on the x-axis
plt.xticks(tick_val, tick_lab)


# Store pop as a numpy array: np_pop
np_pop = np.array(pop)

# Double np_pop
np_pop = np_pop * 2

# Update: set s argument to np_pop
plt.scatter(gdp_cap, life_exp, s = np_pop) // size of bubble

# Previous customizations
plt.xscale('log') 
plt.xlabel('GDP per Capita [in USD]')

plt.scatter(x = gdp_cap, y = life_exp, s = np.array(pop) * 2, c = col, alpha = 0.8) # set color and opacity
# Add grid() call
plt.grid(True)
 


Pandas 绘图
closeMeansKO.plot()
plt.title(‘Stock Stats of Coca-cola’)
直接对Series和DataFrame绘图

Quotesdf.plot(kind=’bar’)
Quotesdf.plot(kind=’scatter’, x=’closeINTC’, color=’g’)

Quotesdf.plot(kind=’kde’) #概率分布

Df.to_csv(‘stockIBM.csv’)
Result = Df.read_csv(‘stockIBM.csv’)
Df.to_excel(‘stockIBM.xsl’)


In the next lecture and in Section 17 we will use the OpenCV image processing library. Let us first make sure you have installed the OpenCV library. OpenCV is also referred to as cv2 in Python.

OpenCV: Image processing
1. Open the command line and type:
pip install opencv-python 
2. Open a Python session and try:
import cv2 
3. If you get no errors, you installed OpenCV successfully. If you get an error, see the FAQs below:

FAQs
1. My OpenCV installation didn't work on Windows
Solution:
1. Uninstall OpenCV with:
pip uninstall opencv-python
2. Download a wheel (.whl) file from this link and install the file with pip. Make sure you download the correct file for your Windows and your Python versions. For example, for Python 3.6 on Windows 64-bit you would do this:
pip install opencv_python 3.2.0 cp36 cp36m win_amd64.whl 
3. Try to import cv2 in Python again. If there's still an error, type the following again in the command line:
pip install opencv-python 
4. Try importing cv2 again. It should work at this point.

2. My OpenCV installation didn't work on Mac
Solution:
If pip install opencv-python didn't work, install OpenCV for Python 2 and use Python 2 to run the programs that contains cv2 code. Because Python 2 is installed by default on Mac, you don't need to install Python 2.
Here are the steps to correctly install OpenCV:
1. Install brew.
To install brew, open your terminal and execute the following:
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
2. OpenCV depends on GTK+, so install that dependency first with brew (always from the terminal):
brew install gtk+ 
3. Install OpenCV with brew:
brew install opencv 
4. Open Python 2 by typing:
python 
5. Import cv2 in Python:
import cv2 
If you get no errors, you installed OpenCV successfully.

3. My OpenCV installation didn't work on Linux
1. Open your terminal and execute the following commands one by one:
1.	sudo apt-get install libqt4-dev
2.	cmake -D WITH_QT=ON ..
3.	make
4.	sudo make install
2. 2. If the above commands don't work, execute this:
1.	sudo apt-get install libopencv-*
3. Then, install OpenCV with pip:
pip install opencv-python 
4. Import cv2 in Python. If you get no errors, you installed OpenCV successfully.

Folium: map
import folium
import pandas
 
data = pandas.read_csv("Volcanoes.txt")
lat = list(data["LAT"])
lon = list(data["LON"])
elev = list(data["ELEV"])
 
html = """<h4>Volcano information:</h4>
Height: %s m
"""
map = folium.Map(location=[38.58, -99.09], zoom_start=5, tiles="Mapbox Bright")
fg = folium.FeatureGroup(name = "My Map")
 
for lt, ln, el in zip(lat, lon, elev):
    iframe = folium.IFrame(html=html % str(el), width=200, height=100)
    fg.add_child(folium.Marker(location=[lt, ln], popup=folium.Popup(iframe), icon = folium.Icon(color = "green")))
 
map.add_child(fg)
map.save("Map_html_popup_simple.html")


聚类分析Cluster

 

Kmeans(data, 2) # 2 个中心

 
 




Nomintim
From geopy.geocoders import Nominatim
Nom = Nominatim()
N = nom.geocode(“155 W 68th St, New York, NY 10023”)


Django
>> pip install Django
>> Django-admin startproject wordcount
>> python manage.py runserver

Don’t change file manage.py
