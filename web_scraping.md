# WEB SCRAPING

## requests

### インストール

```python
pip install requests
```

### 基本

```python
import request
res = request.get('http://hogehoge.com')
#HTTP status e.g 403
status_code = res.status_code
#content
res.text
#raise exception if error occured when get
res.raise_for_status()
```

### ファイルダウンロードと保存

```python
import requests
res = requests.get('http://hogehoge.com/hoge.txt')
res.raise_for_status()
# Set mode 'wb(writing binary)' to write unicode
file = open('hoge.txt','wb')
# Writing file for each 100000 byte
for chunk in res.iter_content(100000):
    file.write(chunk)
file.close()
```

## BeautifulSoup

### インストール 

```python
pip install beautifulsoup4
```

### 基本

```python
import requests
import bs4

res = requests.get('http://hogehoge.com')
res.raise_for_status()
#HTML Parser:lxml (or html5lib,)
bs = bs4.BeautifulSoup(res.text,'lxml')

'''
Select elements
'''
#Select element
bs.select('div')
#Select by id
bs.select('#id_name')
#Select by class
bs.select('.class_name')
#Select span in div
bs.select('div span')
#Select span in div(directly under)
bs.select('div > span')
#Select input which have name attribute
bs.select('input[name]')
#Select input which have type = button
bs.select('input[type="button"]')
```

### Tagオブジェクト

```python
tags = bs.select('.title')
#[<h2 class="title"><b>Hoge</b></h2>, <h2 class="title"><b>Fuga</b></h2>]

#list
len(tags)#2

#type
type(tags[0])#bs4.element.Tag

#tag
tags[0]#'<h2 class="title"><b>Hoge</b></h2>'

#text
tags[0].getText() #'Hoge'

#attribute dictionary
tags[0].attrs #{'class': ['title']}

#get value by attribute
tags[0].get('class') #['title']
```