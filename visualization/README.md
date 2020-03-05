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

![image](https://user-images.githubusercontent.com/53253817/75953912-c3036700-5ef5-11ea-951b-0724accf28f2.png)

## example2  
```python  
sns.distplot(train['card1'], bins=10,kde=False)  
```

![image](https://user-images.githubusercontent.com/53253817/75953814-8899ca00-5ef5-11ea-812e-812ba2aa2645.png)

## example3  
```python  
sns.distplot(train['card1'], bins=10)  
```

![image](https://user-images.githubusercontent.com/53253817/75953963-e4645300-5ef5-11ea-9b14-de4074c0bbf8.png)

## 参考文献  
https://teratail.com/questions/240222  

# countplot(棒グラフ)  
- 棒グラフを表示するモジュール  
- カテゴリ変数に対して行う可視化  
- x軸がカテゴリ、y軸が度数  
- カテゴリ変数のカウントを行って描写する  
- カテゴリが多くて見にくい場合は、引数をxからyに変更すると見やすくなる  
- データが数値の場合軸がおかしくなる？？  
- value_countsを使ったほうがいいかもしれない   

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
