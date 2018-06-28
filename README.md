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
4. 現在如果我們要在桌面上放置一個python_learning資料夾：`mkdir python_learning`，當然再 cd python_learning, 之後檔案存取都是在這裡
5. %bookmark魔術指令(書籤功能)：例如我們現在在剛剛`~/Desktop/python_learning`中，如果我直接設`%bookmark wang`，以後不管我路徑在哪邊，只要`cd wang`就會到`~/Desktop/python_learning`裡面

## 存取和執行

1. IPython 提供了非常方便的存檔和執行指令，例如說剛剛打完程式碼，最後要存下去的輸入列是第1行，第3、4、5行，第12行這樣，想存成wang.py檔，那便是要在CMD中這樣打`%save wang.py 1 3-5 12`。
2. 要在IPython中執行一個.py檔：`%run wang.py`

# Dot Product Speed Comparison

## Slow dot product

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
for t in xrange(T):
	slow_dot_product(a, b)
dt1 = datetime.now() - t0

t0 = datetime.now()
for t in xrange(T):
	a.dot(b)
dt2 = datetime.now() - t0

print "dt1 / dt2: ", dt1.total_seconds() / dt2.total_seconds
```
