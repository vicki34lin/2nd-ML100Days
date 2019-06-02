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