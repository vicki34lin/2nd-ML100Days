# 2nd-ML100Days

## Day1
...
## Day17
### 特徵工程簡介

特徵工程是**事實對應**到後續**評估分數**的轉換

資料彙整之後，以及擬合模型之前

至少要包含⼀種**類別編碼**和一種**特徵縮放**方法

## Day18
### 特徵類型

* 數值型特徵
* 類別型特徵
* 二元特徵
* 排序型特徵
* 時間型特徵

## Day19
### 數值型特徵 - 補缺失值與標準化

填補缺值的方式

* 填補統計值（平均值、中位數、眾數）
* 填補指定值（補零、不可能出現的數值）
* 填補預測值
```
df.fillna(replace_with)
```

平衡數值特徵間的影響力
* 標準化（適合常態分佈的資料）
* 最小最大化（適合均勻分佈、去除掉離群值的資料）
```
from sklearn.preprocessing import MinMaxScaler
from sklearn.preprocessing import StandardScaler

MinMaxScaler().fit_transform(df)
StandardScaler().fit_transform(df)
```

## Day20
### 數值型特徵 - 去除離群值

調整離群值
```
df[column] = df[column].clip(min, max)
```
去除離群值
```
keep_indexs = (df[column] > min) & (df[column] < max)
df = df[keep_indexs]
```

## Day21
### 數值型特徵-去除偏態

* 對數去偏
* 方根去偏
* 分布去偏(boxcox)

```
import numpy as np
from scipy import stats

df[column] = np.log1p(df[column])
df[column] = stats.boxcox(df[column], lmbda=0.15)
df[column] = stats.boxcox(df[column], lmbda=0.5)
```

## Day22
### 類別型特徵 - 基礎處理

* 標籤編碼(Label Encoding)
* 獨熱編碼(One Hot Encoding)

## Day 23
### 類別型特徵 - 均值編碼

* 均值編碼(Mean Encoding)

平滑化

(類別樣本數 * 類別樣本數 + 全部的總平均 * 調整因子) / (類別樣本數 + 調整因子)

## Day 24
### 類別型特徵 - 其他進階處理

* 計數編碼(Counting)

    類別在資料中的出現次數，當目標平均值與類別筆數呈正/負相關時，可以考慮使用。

* 特徵雜湊(Feature Hash)

    類別型特徵最麻煩的問題 : 相異類別的數量非常龐大！像是姓名欄位。

## Day 25
### 時間型特徵

* 將時間拆解成 年/月/日/時/分/秒 的分類值
* 將時間以週期循環特徵為優化方向 （例如：冷熱、是否精神飽滿...等）


## Day 26
### 特徵組合 - 數值與數值組合

單純知道欄位是數值，預測力有限。

如果能知道這個數值和座標、經緯度有關，即可透過換算來增加預測力。

因此，對問題領域知識的了解，是特徵工程最重要的環節。


## Day 27
### 特徵組合 - 類別與數值組合

類別型特徵與數值型特徵，可做群聚編碼。

可用的運算包括取類別的 mean, median, mode, max, min, count。


## Day 28
### 特徵選擇

特徵組合為的是增加特徵，特徵選擇則是在減少特徵

* 過濾法
* 包裝法
* 嵌入法


## Day 29
### 特徵評估

樹狀模型的特徵重要性：分支次數、特徵覆蓋度、損失函數降低量


## Day 30
### 分類型特徵優化 - 葉編碼

葉編碼 (leaf encoding)：採用決策樹的葉點作為編碼依據重新編碼。

葉編碼的目的是重新標記資料，以擬合後的樹狀狀模型分歧條件，將資料離散化。

每棵樹視為一個新特徵，多個分類預測結果，需要先將機率倒推回對應數值，相加後再由 sigmoid 函數算回機率，類似邏輯斯回歸的算法。


## Day 31
### 
