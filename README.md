# python_learning
Learning the basic structure of python

## 安裝環境

1. Win10 Python 3.5
2. Numpy安裝需要上官網 [Unofficial Windows Binaries for Python Extension Packages](https://pypi.python.org/pypi/numpy)，下載適合自己系統版本的Numpy。
3. 安裝Numpy：在CMD命令模式下進入Numpy安裝文件的目錄下，執行`pip install numpy-1.15.0rc1+mkl-cp37-cp37m-win_amd64.whl`
4. 安裝ipython：安裝IPython前請先安裝Python，Python的安裝步驟可參考[一日程式人 終身程式人](http://pg-code.blogspot.com/2014/10/python.html)。若依前述步驟安裝好Python，接著打開CMD並執行`pip install "ipython[notebook]"`。

## 程式檔的讀取

1. 想看現在的資料夾下有什麼檔案：`ls`
2. 當然可以知道現在的路徑是什麼：`pwd`
3. 也可以用cd進入某個資料夾：`cd /d C:\Users\Wang Yang\Desktop`
4. 現在如果我們要在桌面上放置一個python_learning資料夾：`mkdir python_learning`，當然再`cd python_learning`, 之後檔案存取都是在這裡
5. %bookmark魔術指令(書籤功能)：例如我們現在在剛剛`~/Desktop/python_learning`中，如果我直接設`%bookmark wang`，以後不管我路徑在哪邊，只要`cd wang`就會到`~/Desktop/python_learning`裡面
6. 如何知道現在python的安裝路徑：

```
import sys
path = sys.executable
print(path)
```

## 存取和執行

1. IPython 提供了非常方便的存檔和執行指令，例如說剛剛打完程式碼，最後要存下去的輸入列是第1行，第3、4、5行，第12行這樣，想存成wang.py檔，那便是要在CMD中這樣打`%save wang.py 1 3-5 12`。
2. 要在IPython中執行一個.py檔：`%run wang.py`

# Python Coding Practice 

## Count Primes

### Write a function that returns the number of prime numbers that exist up to and including a given number.

```
def count_primes(num):
	# Check for 0 or 1 input
	if num < 2:
		return 0
	# Check for 2 or greater
	primes = [2]
	x = 3
	while x <= num:
		for y in primes:
			if x % y == 0:
				x += 2
				break
		else:
			primes.append(x)
			x += 2
			
	print(primes)
	return len(primes)
```


## Calculate the number of upper case letters and lower case letters

### Write a python function that accepts a string and calculate the number of upper case letters and lower case letters

Sample string: 'Hello Mr. Wang, how are you this fine Friday?'

Expected output:

No. UC characters: 4

No. LC characters: 30

```
def up_low(s):
  d = {"upper": 0, "lower": 0}
  for c in s:
    if c.isupper():
      d["upper"] += 1
    elif c.islower():
      d["lower"] += 1
    else:
      pass
  print("Original String: ", s)
  print("No. UC characters:", d["upper"])
  print("No. LC characters:", d["lower"])
```

## Palindrome(回文)

### Write a python function that checks whether a passed string is palindrome or not.

Note: A palindrome is word, phrase, or sequence that reads the same backward as forward, e.g., madam or nurses run.

```
def palindrome(s):
	return s == s[::-1]
```

## Dot Product Speed Comparison

### Slow dot product

```
import numpy as np
from datetime import datetime

a = np.random.randn(100)
b = np.random.randn(100)
T = 100000

def slow_dot_product(a, b):
	result = 0
	for e, f in zip(a, b):
		result += e * f
	return result

t0 = datetime.now()
for t in range(T):
	slow_dot_product(a, b)
dt1 = datetime.now() - t0

t0 = datetime.now()
for t in range(T):
	a.dot(b)
dt2 = datetime.now() - t0

print("dt1 / dt2: ", dt1.total_seconds() / dt2.total_seconds())
```

## Pangram(全字母短句，指包括英語全部26个字母的短句)

### Write a python function to check whether a string is pangram or not.

Note: Pangrams are words or sentences containing every letter of the alphabet at least once.

For example: "The quick brown fox jumps over the lazy dog."

```
import string

def ispangram(str1, alphabet = string.ascii_lowercase):
	alphaset = set(alphabet)
	return alphaset <= set(str1.lower())
```

# LEGB Rule

LEGB作用域查找原則：當引用一個變量時，Python 按以下順序依次進行查找：從本地變量中，在任意上層函數的作用域，在全局作用域，最後在內置作用域中查找。第一個能夠完成查找的就算成功。變量在代碼中被賦值的位置通常就決定了它的作用域。

>* L: Local -- Names assigned in any way withina function (def or lambda), and not declared global in that function.
>
>* E: Enclosing function locals -- Names in the local scope of any and all enclosing functions (def or lambda), from inner to outer.
>
>* G: Global (Module) -- Names assigned at the top-level of a module file, or declared global in a def within the file.
>
>* B: Built-in (Python) -- Names preassigned in the built-in names module: open, range, SyntaxError, ...

>* L -- Local: 本地作用域;
>
>* E -- Enclosing: 上一層結構中 def 或 lambda 的本地作用域;
>
>* G -- Global: 全局作用域;
>
>* B -- Build-in: 內置作用域。

# Class

參考自[關於Python的類別(Class)](https://medium.com/@weilihmen/%E9%97%9C%E6%96%BCpython%E7%9A%84%E9%A1%9E%E5%88%A5-class-%E5%9F%BA%E6%9C%AC%E7%AF%87-5468812c58f2)

模組為了有架構的呈現功能一定是好由幾個py檔組成，而這些py檔裡面再用class及def結構化，所以class跟def是組成模組功能的最低架構。

在python裡，就是用class 開宗明義定義一個類別名稱，通常會用首字大寫的單字。

```def __init__(self):```這邊代表宣告時會自動執行的函式，也就是宣告類別的"起手式"，所以一般會拿來放基礎的屬性設定。

"class的概念是屬性集合，而不是所有物" 

簡單範例: 互動案例-存款與取款

```
class Account:
    def __init__(self, number, name):
        self.number = number
        self.name = name
        self.balance = 0
        
    def deposit(self, amount):  #存款動作: amount代表存入金額
        if amount <= 0:
            raise ValueError('must be positive')
        self.balance += amount
        
    def withdraw(self, amount): #取款動作: amount代表取款金額
        if amount <= self.balance:
            self.balance -= amount
        else:
            raise RuntimeError('balance not enough')
```

這邊的簡單例子，便是創造一個銀行戶頭，然後銀行戶頭可以進行存款與取款的互動

定義完class之後，就可以寫一些存取款動作

```
acct1 = Account(‘123–456–789’, ‘Justin’) #開一個帳戶
acct1.deposit(100)
acct1.withdraw(30)
print(acct1.balance) #餘額是 70
```

# Web Crawler (網路爬蟲)

## 網路抓取所需的庫

要先安裝visual c++ build tools，不然可能會出現錯誤代碼：[Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

* Urllib2：這是一個可用於獲取URL的Python模塊。它定義了函數和類來幫助URL操作（基本和摘要式身份驗證，重定向cookie等）。
```
pip install requests
```
* BeautifulSoup：這是一個從網頁中提取信息的工具。可以使用它來提取表格、列表和段落，也可以使用過濾器從網頁中提取信息。
```
pip install BeautifulSoup4
pip install lxml
pip install html5lib
```

由於BeatifulSoup不會為我們提取網頁，所以我們才要使用urllib2與BeautifulSoup庫結合使用。

## 熟悉HTML標籤

[HTML筆記](https://kknews.cc/tech/b2kjya6.html)

```
<!DOCTYPE html>
<html>
<body>

<h1>My First Heading</h1>

<p>My First paragraph.</p>

</body>
</html>
```

## 利用Wikipedia回答專業知識

如果是讓機器人只能回答我們的問答集，那就有點無聊了。為了提升機器人的智能，我們可以撰寫一Python網路爬蟲，讓該爬蟲根據我們的關鍵字到維基百科上搜尋專業知識，並將專業知識的第一段串接到對話流程中，便能讓我們的Open Jarvis回答專業問題了。

參考自[[Open Jarvis] 如何讓對話機器人利用 Wikipedia 回答專業知識?](https://www.youtube.com/watch?v=T5UIySP9Owc&feature=youtu.be)

```
import speech_recognition
import tempfile
from gtts import gTTS
from pygame import mixer 

def listenTo():
    r = speech_recognition.Recognizer()

    with speech_recognition.Microphone() as source:
        r.adjust_for_ambient_noise(source)
        audio = r.listen(source)

    return r.recognize_google(audio, language='zh-TW')


def speak(sentence):
    mixer.init()
    with tempfile.NamedTemporaryFile(delete=True) as fp:
        tts = gTTS(text=sentence, lang='zh')
        tts.save("{}.mp3".format(fp.name))
        mixer.music.load('{}.mp3'.format(fp.name))
        mixer.music.play()

import requests
from bs4 import BeautifulSoup

def getWiki(term):
    res = requests.get('https://zh.wikipedia.org/wiki/{}'.format(term))
    soup = BeautifulSoup(res.content, 'html.parser')
    article = soup.select_one('.mw-parser-output p').text
    return article
    
speak(getWiki(listenTo()))
```

