<!-- $theme: default -->
<!-- page_number: true -->
<!-- $size: 16:9 -->

# 12 Excelシート

---
# TL;DR
## [openpyxl](https://openpyxl.readthedocs.io/en/stable/#)によるExcel操作まとめ

```python
'''
Excelブックを読み込み、セルの値を更新して別名で保存する処理
'''
import openpyxl

workbook = openpyxl.load_workbook('Book1.xlsx') #ブックの読込
sheet = workbook.get_sheet_by_name('Sheet1')    #シートの読込
cell = sheet.cell(row=1,column=1)               #セルの取得
cell.value = 'Value'                            #値の更新

workbook.save('Book1_new.xlsx')                 #ブックの保存
```
```python
'''
新規Excelブックの作成と保存
'''
workbook = openpyxl.Workbook()
workbook.save('Book2.xlsx')
```

---
# 12.1 Excelブックとシートの読込
* サードパーティーモジュール openpyxlを使用する
```python
import openpyxl

'''---Excelブックの操作---'''
#Excelブックの読み込み
workbook = openpyxl.load_workbook('hoge.xlsx') #Workbookオブジェクトを返す
workbook2 = openpyxl.load_workbook('hoge.xlsx', data_only=True) #数式の結果を取得する場合

#シート名の一覧取得
workbook.get_sheet_names() #['Sheet1','Sheet2','Sheet3']

'''---シートの操作---'''
#シート名からシートを取得
sheet = workbook.get_sheet_by_name('Sheet1') #Worksheetオブジェクトを返す

#アクティブシートの取得
active_sheet = workbook.active #WorkSheetオブジェクトを返す

#シート名の取得
sheet.title #'Sheet1'
```

---
# 12.2 セルの取得-セル番地から取得
Medal.xlsx
|  | A | B |
| - | - | - |
| 1  | 金 | 4 |
| 2 | 銀 | 5 |

```python
'''~シートの取得まで省略~'''
#セルの取得
cell = sheet['A1'] #Cellオブジェクトを返す
#値
cell.value         #'金'
#行
cell.row           # 1
#列
cell.column        #'A'
#番地
cell.coordinate    #'A1'
#範囲で取得
cells = sheet['A1':'C3']
```

---
# 12.3 セルの取得-行列番号から取得
*行と列の先頭番号は1であり、0ではないので注意*

Medal.xlsx
|  | A | B |
| - | - | - |
| 1  | 金 | 4 |
| 2 | 銀 | 5 |
```python
'''~シートの取得まで省略~'''
cell = sheet.cell(row=1,column=1) #sheet['A1']と同じ結果が得られる
cell.value #'金'
```
---
# 12.4 シートサイズの取得

Medal.xlsx
|  | A | B |
| - | - | - |
| 1  | 金 | 4 |
| 2 | 銀 | 5 |
```python
'''~シートの取得まで省略~'''
sheet.max_row    #2 シートの最終行
sheet.max_column #2 シートの最終列

#セルのループ
for i range(1,sheet.max_row + 1):
    for j range(1,sheet.max_column + 1):
    	print(sheet.cell(row=i, column=j).value)
```

---

# 12.5 列名と列番号の変換

openpyxl 2.4からはopenpy.cellからopenpy.utilsに変更となっているため注意
```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string

#列番号→列名
get_column_letter(1) #'A'

#列名→列番号
column_index_fromstring('A') #1
```
---

# 12.6 Excelブックの作成と保存

```python
import openpyxl

#新しいWorkbookオブジェクトの作成
wb = openpyxl.Workbook()

#シートの追加
wb.create_sheet(index=1, title='NewSheet') #引数は省略可

#セルに値を書き込む
sheet = wb.get_sheet_by_name('NewSheet')
sheet['A1'].value = 'Content'
sheet.cell(row = 1, column = 1).value = 'Content'

#シートの削除
wb.remove_sheet(sheet) #引数はシート名ではなくWorksheetオブジェクト

#シートの保存 
wb.save('NewBook.xlsx')
```
---

# 12.7 フォント

```python
import openpyxl
form openpyxl.styles import Font

wb = openpyxl.Workbook()
sheet = wb.get_sheet_by_name('Sheet1')
#フォントオブジェクトの作成
font = Font(name='Times New Roman',size=24, italic=True, bold=True)
#フォントの設定
sheet['A1'].font = font
```
Fontオブジェクトの主な引数
| 引数 | 説明 |
| - | - |
| name | フォント名|
| size | フォントサイズ(ポイント数)|
| bold | Trueで太字|
| italic| Trueで斜体 |

---

# 12.8 行と列の幅の変更

```python
'''~シートの取得まで省略~'''
sheet.row_dimensions[1].height = 70 #1行目の高さを設定  設定範囲:0~409
sheet.column_dimensions['B'].width = 20 #A列の幅を設定  設定範囲:0~255
```
---

# 12.9 セルの結合/結合解除

```python
'''~シートの取得まで省略~'''
#セルの結合
sheet.merge_cells('A1:D5')    #結合範囲を文字列で指定する
sheet['A1'].value = 'Content' #値を設定する場合は、左上のセルを指定する

#セル結合の解除
sheet.unmerge_cells('A1:D5')
```

---
# 終わり



