# Selenium

## 環境構築
### WebDriverモジュールのインストール

```bash
pip install webdriver
```

### WebDriverのダウンロード
1. [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/downloads)をダウンロード

1. ダウンロードしたWebDriverを任意のディレクトリに配置しPathを通す。

### Seleniumによるブラウザ操作の実行

```python
# ChromeでWebサイトを開く
>>> from selenium import webdriver
>>> browser = webdriver.Chrome()
>>> browser.get('http://inventwithpython.com')
```
## ブラウザの操作
### 要素の取得

* element: 一致した最初の要素を取得
* element->elementsにすると、一致する全てをリストで取得

```python
#class
browser.find_element_by_class_name(name)
#selector
browser.find_element_by_css_selector(selector)
#id
browser.find_element_by_id(id)
#link text
browser.find_element_by_link_text(text)
#link text(partial match)
browser.find_element_by_partial_link(text)
#name attribute
browser.find_element_by_name(name)
#tag name(ignore case)
browser.find_element_by_tag_name(name)
```

### 操作

* クリック
```python
link = browser.find_element_by_link_text('Link')
# Mouse Click
link.click()
```
* キー入力
```python
login_form = browser.find_element_by_id('login')
# Input text
login_field.send_keys('hoge')
# Excec submit
login_field.submit()
```
* 特殊キー入力
```python
html_elem = browser.find_element_by_tag_name('html')
#↓
html_elem.send_keys(Keys.Down)
#↑
html_elem.send_keys(Keys.UP)
#→
html_elem.send_keys(Keys.RIGHT)
#←
html_elem.send_keys(Keys.LEFT)
#Enter
html_elem.send_keys(Keys.ENTER)
#Home
html_elem.send_keys(Keys.HOME)
#End
html_elem.send_keys(Keys.END)
#Back space
html_elem.send_keys(Keys.BACK_SPACE)
#Function Key
html_elem.send_keys(Keys.F1)
#Tab
html_elem.send_keys(Keys.TAB)
```

### ブラウザ全体の操作

```python
# Broser back
browser.back()
# Broser forward
browser.forward()
# Refresh page
browser.refresh()
# Close window
browser.quit()
```