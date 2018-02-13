<!-- $theme: default -->
<!-- page_number: true -->
<!-- $size: 16:9 -->

# Python3

---
# 3
---
### 3.1 関数

* def  \[関数名]( \[引数名,...] ):
* 戻り値がない場合、returnは不要

```python
def hello(name):
    return "Hello " + name + " !"

print(hello("Jhon")) #Hello Jhon !
```
---

### 3.2 None

* Noneは値がないことを示す
* NoneTypeという型の唯一の値
* Javaのnullに相当する

```python
hoge = print('hello') #print()は戻り値のない関数
#判定は==またはisでする
hoge == None # True
hoge is None # True
```
---
### 3.3 例外処理
* try: - except: - else: - finaly:  ※else,finallyは省略可
* except \[例外名]:で例外を捕捉 ※例外名は省略可
```python
def divide(a,b):
    try:#エラーが発生する可能性がある処理
        print(a / b)
    except ZeroDivisionError: #ゼロ除算エラー発生時処理
        print('ZeroDivisionError: '+ str(a) + '/'+ str(b))
    else:#エラーがないときの処理
        print('No Error') 
    finally:#エラーの有無に関わらない最終処理
        print('Fin')  
        
divide(4,2) #2.0 #No Error #Fin
divide(5,0) #ZeroDivisionError: 5/0 #Fin
```
---
# 4
---
### 4.1 リスト

* Pythonにおける配列
* [開始:終了]で開始≦index<終了の要素を取得可能
※この記法をスライスという
 
```python
fruits = ['apple','orange','banana','melon'] #リストの定義
# 要素の取得
print(fruits[0])             #apple
print(fruits[-1])            #melon (-1は最後の要素を示す)
print(fruits[1:3])           #['orange','banana'] (スライスによる指定)
print(fruits.index('orange'))#1 orangeのindexを取得
print(len(fruits))           #4 要素数

for i in range(len(fruits)): #一般的にforはrange(len())を使う
	print(fruits[i]) 
```
---
### 4.2 リストの操作
 
```python
fruits = ['apple','orange','banana','melon'] #リストの定義

# 追加
fruits.append('lemon')   #リストの最後に'lemon'を追加
fruits.insert(1,'grape') #リストの1番目にgrapeを挿入

# 変更
fruits[0] = 'peach'

#削除
del fruits[1]            #1番目の要素の削除
fruits.remove('banana')  #要素を指定して削除

#ソート
fruits.sort()             #昇順ソート
fruiss.sort(reverse=True) #降順ソート
```
---
### 4.3 タプル

* 変更不可能(イミュータブル)な配列
* \[要素,...]ではなく,(要素,...)で定義する

```python
langs = ('Java','Ruby','Python','C') #タプルの定義 ()で定義
print(langs[0])    #Java
langs[0] = 'Swift' #変更はエラーになる
langs = ('COBOL','FORTRAN') #新しいタプルに書き換えることは可能

#リスト<-->タプルの変換
tuple(['a','b','c']) #list  -> tuple 変換 #('a','b','c')
list(('e','f','g'))  #tuple -> list　変換 #['e','f','g']
```
---
# 5

---
### 5.1 辞書

* Keyと対応する値の集合
* {\[Key]:\[値],...}で定義

```python
color_jp = {'red':'赤','blue':'青','green':'緑'} #辞書の定義
#Keyを指定して値を取得
print(color_jp['blue']) #青

# 辞書のループ
for key,item in color_jp.items():print(key,item)
# 値だけのループ
for value in color_jp.values():print(value) 
# Keyだけのループ
for key in color_jp.keys():print(key)

# 存在確認
'green' in color_jp        #True 
'green' in color_jp.keys() #True Keyの存在確認
'緑' in color_jp.values()  #True 値の存在確認
```
---
### 5.2 辞書の操作

```python
color_jp = {'red':'赤','blue':'青','green':'緑'} #辞書の定義

#取得
#get()は第一引数で指定したKeyが存在しないとき、第二引数の値を返す
print(color_jp.get('red','赤はない'))    #赤
print(color_jp.get('yellow','黄はない')) #黄はない

#追加
#setdefault()はKeyが存在しないときに限り追加する
color_jp.setdefault('black','黒')#追加される
color_jp.setdefault('red','紅')  #追加されない(変更もされない)

#変更
color_jp['blue'] = '蒼'

#削除
del color_jp['blue']
```
---
# 6
---
### 6.1 文字列
```python
# 基本
"What's your name?"  #'を含む場合""で囲む
'タブ\tです'          #タブ	です
'タブ\\tです'         #タブ\tです #エスケープシーケンス\
r'タブ\tです'         #タブ\tです #先頭にrをつけると生の文字列

# 複数行文字列 ※複数行コメントとしてもよく使用される
'''
3つクオートを並べると
改行コードを使わずに
複数行の文字列が定義できる
'''
# indexとスライスによる指定
alphabets = 'abcdefg'
alphabets[0]   #a
alphabets[2:5] #cde

# 文字列を含むか否かの判定
'is a' in 'This is a pen' #True
```
---

### 6.2 文字列のメソッド1

```python
# 大文字/小文字の変換
ppap = 'This is a pen.'
print(ppap.upper())  #THIS IS A PEN. #全て大文字の文字列を返す
print(ppap.lower())  #this is a pen. #全て小文字の文字列を返す

# 構成する文字の判定
'This'.isalpha()    #True #英字のみの場合True 
'0123Abc'.isalnum() #True #英字か数字のみの場合True
'0123'.isdecimal()  #True #数字のみの場合True
' \t\n'.isspace()   #True #スペース、タブ、改行のみの場合True
'This Is A Pen'.istitle() #True #単語の先頭のみ大文字の場合True

# 始まりと終わりの判定 ※大文字と小文字は区別する
'This is a pen.'.startswith('This') #True #指定文字列で始まる場合True
'This is a pen.'.endswith('pen.')   #True #指定文字列で終わる場合True

```
---

### 6.3 文字列のメソッド2

```python
# リストの要素を結合する
'_'.join(['snake','case','string']) #snake_case_string

# 文字列をリストに分割
'snake_case_string'.split('_') #['snake','case','string']

# 文字列の位置揃え
'title'.center(15,'-') #'-----title-----' #15文字中央寄せ'-'埋め
'1,000'.rjust(15)      #'          1,000' #15文字右寄せ
'abcde'.ljust(15)      #'abcde          ' #15文字左寄せ

# 文字列の空白文字(スペース、タブ、改行)の除去
'  apple  '.strip()       #'apple'   #両端から空白文字を除去
'ppappleppap'.strip('pa') #'le'      #両端から指定文字を除去 ※順番は関係しない
'  apple  '.rstrip()      #'  apple' #右端から空白文字を除去 
'  apple  '.lstrip()      #'apple  ' #左端から空白文字を除去
```

---

# 7

---
### 7.1 正規表現

正規表現を使用するにはreモジュールをインポートする

```python
#reモジュールをインポート
import re 

# 1.Regrexオブジェクトの生成
iphone_regex = re.compile(r'iPhone\d+S?') #正規表現はraw文字列を使うと便利

# 2.検索の実行 serch()メソッドは最初の1件を返す
match_obj = iphone_regex.search('iPhone8が発売開始!') #結果はMatchオブジェクトに格納される

# 3.検索結果の取得 
match_obj.group() #'iPhone8'

```

---

### 7.2 グループマッチ

正規表現を括弧で囲むことでグループを区切ることができる

```python
import re

iphone_regex = re.compile(r'(iPhone\d+)(S?)') #括弧でグループごとに囲む
match_obj = iphone_regex.search('iPhone7Sが発売開始!')

# 全体の取得 ()と(0)は同じ結果になる
match_obj.group()  #'iPhone7s'
match_obj.group(0) #'iPhone7s'

# グループ毎の取得
match_obj.group(1) #'iPhone7'
match_obj.group(2) #'S'

# グループ毎に一度に取得
match_obj.grop(2)  #('iPhone7','S')  #タプルで結果が返る

```
---

### 7.3 複数件の取得

findall()メソッドを使う

```python
import re 
iphone_regex = re.compile(r'iPhone\d+S?')

match_obj = iphone_regex.findall('iPhone8とiPhone10が発売開始!')

match_obj #['iPhone8', 'iPhone10']  #findall()は結果のリストが返る

# group()は実行不要(不可)

```


---

# 8

---

### 8.1 ディレクトリ操作

ディレクトリ操作をするにはosモジュールをインポートする

```python
import os

#カレントディレクトリ(CWD:カレントワーキングディレクトリ)の取得
os.getcwd() #/User/jhon/documents

#ディレクトリ内のファイルとフォルダの一覧
# ※引数がないとカレントディレクトリが対象になる
os.listdir(r'/User') #['jhon','michael','bob','cnf.txt'] 

#ディレクトリの移動(CD:チェンジディレクトリ)
os.chdir(r'/User/Jhon/workspace')  #パスは相対パスでも絶対パスでも良い
os.getcwd() #/User/jhon/workspace

#ディレクトリの作成
os.makedirs(r'/User/jhon/workspace/python3/chapter01') #中間のフォルダも作成される
 
```

---

### 8.2 テキストファイルの読取


```text
<kaimono.txt>
・にんじん
・じゃがいも
・豚肉
```

```python
#モジュールのインポートは不要

# ファイルを読取モードで開く
file = open('kaimono.txt')

# read()でファイルの内容全体を読み込む
file.read() #'・にんじん\n・じゃがいも\n・豚肉\n'

# 読取モードの場合はclose()は必要ない
```

```python
# 1行ずつ読み取る場合
file = open('kaimono.txt')
# readlines()で改行区切りで取得する
file.readlines() #['・にんじん\n', '・じゃがいも\n', '・豚肉\n']
```

---

### 8.3 テキストファイルの書込

```python
#書込モードでファイルを開く
file = open('todo.txt','w')  #ファイルが存在しない場合は新規作成される

#内容の書込
file.write('・ゴミ出し\n')    #6　＃write()は書き込んだ文字数を返す 
file.write('・洗濯\n')      　#4

#ファイルを閉じる
file.close()                 #書込/追加書込はclose()が必要
```

```python
#追加書込モードでファイルを開く
file = open('todo.txt','a')  #ファイルが存在しない場合は新規作成される

#内容の追記 
file.write('・買い出し\n')    #6

#ファイルを閉じる
file.close()                 #書込/追加書込はclose()が必要
```
---
# 9
---

### 9.1 ファイル操作

```python
import shutil #Shell Utilitiesのインポート

#1つのファイルのコピー copy(コピー元,コピー先)
shutil.copy('todo.txt',r'../')  #'../todo.txt'　#コピー先ファイルパスを返す

#フォルダ(中身含む)のコピー
shutil.copytree('/User/jhon/documents','/User/michael/documents')

#ファイル/フォルダの移動　move(移動元,移動先)
shutil.move('todo.txt',r'../')

#フォルダ(中身含む)の削除
shutil.rmtree('/User/michael/documents/tmp')
```

```python
import os

#ファイルの削除
os.unlink('todo.txt') #1つのファイル削除にはshutilは必要ない
```

---
### 9.2 Zipファイル操作

Zipファイルを扱うにはzipfileモジュールをインポートする
```python
#ファイル圧縮
import zipfile #インポート

#書込モードでZipファイルを開く
zip_file = zipfile.ZipFile('todo.zip','w') #'a'を指定すれば追加書込

#ファイルの書込 圧縮アルゴリズム:deflate
zip_file.write('todo.txt',compress_type=zipfile.ZIP_DEFLATED) 

# Zip ファイルを閉じる
zip_file.close()
```

```python
#圧縮ファイルの展開
import zipfile

# ZipFileオブジェクトの作成
zip_file = zipfile.ZipFile('todo.zip')

# 指定したディレクトリ以下に展開
zip_file.extractall('\User\jhon\documents')  #展開先は省略可
```
