# 数値変数とカテゴリ変数を分ける  
- trainデータを上から200データくらいとってきてcsv出力をして眺める  
- 数値カラムとカテゴリカラムに分けて

```python  
# csv出力
train[0:200].to_csv('check.csv')
```

```python  
# 数値カラムに対してまとめて処理
for i in ['card1', 'card2', 'card3', 'card5']:
    print(train[i].value_counts(dropna=False, normalize=True))
  
# カテゴリカラムに対してまとめて処理


```

# distplot(ヒストグラム)  
- ヒストグラムを描写するモジュール  
- データの分布を確認したいときに使う  
- 横軸がデータ、縦軸が度数を表す  
- kdeはカーネル密度推定という確率密度関数を表示する  
- kdeをFalseにしないと縦軸が正規化された値になるので度数で表したい場合はFalseに  
- binsでデータを分割する数を指定する。デフォルトは適当にseabornが判断した値になる  
## example1  
```python  
sns.distplot(train['card1'], kde=False)  
```

![image](https://user-images.githubusercontent.com/53253817/75964017-d3254180-5f09-11ea-80c0-112ba110e06b.png)

## example2  
```python  
sns.distplot(train['card1'], bins=10,kde=False)  
```

![image](https://user-images.githubusercontent.com/53253817/75963947-b983fa00-5f09-11ea-904a-4b7b3d9aa424.png)

## example3  
```python  
sns.distplot(train['card1'], bins=10)  
```

![image](https://user-images.githubusercontent.com/53253817/75963844-91949680-5f09-11ea-85ed-7e1c68300040.png)

## 参考文献  
https://teratail.com/questions/240222  

# countplot(棒グラフ)  
- 棒グラフを表示するモジュール  
- カテゴリ変数に対して行う可視化  
- x軸がカテゴリ、y軸が度数  
- カテゴリ変数のカウントを行って描写する  
- NaNは無視して描画されるので、NaNも表示したかったらほかの値で置き換える  
- value_countsをしてからNaNの有無を確認した後にcountplotを行うかを決めればいいと思う  
- カテゴリが多くて見にくい場合は、引数をxからyに変更すると見やすくなる  
- データが数値の場合軸がおかしくなる？？(example1)  
- value_countsを使ったほうがいいかもしれない(example2)  
- カテゴリ数が多すぎる場合はvalue_countsで(example4)  

```python  
sns.countplot(x=列名, data=データフレーム)
```

## example1  
```python  
sns.countplot(x='id_03', data=train)
```

![image](https://user-images.githubusercontent.com/53253817/75963659-35ca0d80-5f09-11ea-9732-78a35bc382b9.png)

## example2  
```python  
train['id_03'].value_counts(dropna=False, normalize=True).head()
```

```
NaN    0.887689233582822
0.0    0.108211128797372
1.0    0.001461374335354
3.0    0.001131168083449
2.0    0.000712906831036
Name: id_03, dtype: float64
```

## example3  
```python  
train['ProductCD'].value_counts(dropna=False, normalize=True).head()
sns.countplot(y='ProductCD', data=train)
```

```
W    0.744522
C    0.116028
R    0.063838
H    0.055922
S    0.019690
Name: ProductCD, dtype: float64
```

![image](https://user-images.githubusercontent.com/53253817/75964530-b50c1100-5f0a-11ea-85bf-3aa0f7eb39cd.png)

## example4  
```python  
# 上位20個の度数を表示
train['id_30'].value_counts(dropna=False, normalize=True)[:20]
```

```
NaN                 0.868654
Windows 10          0.035823
Windows 7           0.022200
iOS 11.2.1          0.006303
iOS 11.1.2          0.006264
Android 7.0         0.004862
Mac OS X 10_12_6    0.004333
Mac OS X 10_11_6    0.003976
iOS 11.3.0          0.003414
Windows 8.1         0.003241
Mac OS X 10_10_5    0.002796
iOS 11.2.6          0.002789
iOS 10.3.3          0.002638
Mac OS X 10_13_2    0.002406
Mac OS X 10_13_1    0.002051
iOS 11.2.5          0.002032
Linux               0.001924
Android             0.001827
iOS 11.2.2          0.001527
Mac OS X 10_13_3    0.001456
Name: id_30, dtype: float64
```

## example4  
- hueでpandasのgroupby的な感じで処理できる  

```python  
sns.countplot(x='card4', data=train, hue='isFraud')
```

![image](https://user-images.githubusercontent.com/53253817/75983263-88b4bc80-5f2b-11ea-978c-87508a5ef6f2.png)

# わかったこと  
- 上から200個くらいデータをとってきてcsv出力してデータの全体を見るようにしてlabelencodingするべきものとかを区別する  
- 上から200個くらいデータをとってきてcsv出力して数値変数とカテゴリ変数に分ける  
- カテゴリ変数が多過ぎたら、度数が少ないものを包括して'other'という特徴量データにまとめる（今回は0.1％以下のモノ）  


# 参考にする文献  
https://qiita.com/4m1t0/items/76b0033edb545a78cef5
