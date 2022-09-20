# Прогнозирование рыночной стоимости автомобилей

![car prices](https://st2.depositphotos.com/4370503/6436/i/600/depositphotos_64364335-stock-photo-three-race-cars.jpg)

## Описание проекта

**ЦЕЛЬ ПРОЕКТА:**

Построить несколько прототипов моделей для определения цены автомобилей `по их характеристикам`.

Предсказания позволят клиентам `онлайн-сервиса` по продаже автомобилей быстро **оценивать их рыночную стоимость**.


Результат работы моделей будем оценивать по 3-м критериям:

- качество предсказаний
- скорость предсказаний
- время обучения
    
В нашем распоряжении данные с **характеристиками автомобилей**, собранные из разных анкет автовладельцев. 

=========================================================================================

**ЛИЧНАЯ ЦЕЛЬ:**

- Познакомиться с основными возможностями **бустера** `LightGBM` и сравнить его работу с **RandomForest**.


- Научиться использовать **пайплайны**  c помощью классов `Pipeline` и `ColumnTransformer` для кодирования категорий и построения моделей.


- Испытать подход с **ресемплингом** для задач EDA.


- Попробовать свои силы в Feature Engineering **категорий** для задач регрессии и найти возможности для улучшения результатов предсказаний!

[Посмотреть проект](Predicting_stock_prices_for_cars_v1.ipynb)
## Навыки

<div class="alert alert-success">
<br> ✔️ Исследовательский анализ  ✔️ Поиск аномалий </br>
<br> ✔️ Регрессия  ✔️ Категориальные признаки</br>
<br> ✔️ Пайплайны для кодирования категорий</br>
<br> ✔️ OneHot  ✔️ Ordinal  ✔️ Dummy  ✔️ Target encoding</br>
<br> ✔️ Feature Engineering</br>
<br> ✔️ Оценка скорости алгоритмов</br>
</div>

## Исходные данные


```python
import pandas as pd

df = pd.read_csv('/datasets/autos.csv')
display(df.iloc[:, :9].head(3))
df.iloc[:, 9:].head(3)
```


<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DateCrawled</th>
      <th>Price</th>
      <th>VehicleType</th>
      <th>RegistrationYear</th>
      <th>Gearbox</th>
      <th>Power</th>
      <th>Model</th>
      <th>Kilometer</th>
      <th>RegistrationMonth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-03-24 11:52:17</td>
      <td>480</td>
      <td>NaN</td>
      <td>1993</td>
      <td>manual</td>
      <td>0</td>
      <td>golf</td>
      <td>150000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-03-24 10:58:45</td>
      <td>18300</td>
      <td>coupe</td>
      <td>2011</td>
      <td>manual</td>
      <td>190</td>
      <td>NaN</td>
      <td>125000</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-03-14 12:52:21</td>
      <td>9800</td>
      <td>suv</td>
      <td>2004</td>
      <td>auto</td>
      <td>163</td>
      <td>grand</td>
      <td>125000</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>





<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FuelType</th>
      <th>Brand</th>
      <th>NotRepaired</th>
      <th>DateCreated</th>
      <th>NumberOfPictures</th>
      <th>PostalCode</th>
      <th>LastSeen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>petrol</td>
      <td>volkswagen</td>
      <td>NaN</td>
      <td>2016-03-24 00:00:00</td>
      <td>0</td>
      <td>70435</td>
      <td>2016-04-07 03:16:57</td>
    </tr>
    <tr>
      <th>1</th>
      <td>gasoline</td>
      <td>audi</td>
      <td>yes</td>
      <td>2016-03-24 00:00:00</td>
      <td>0</td>
      <td>66954</td>
      <td>2016-04-07 01:46:50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>gasoline</td>
      <td>jeep</td>
      <td>NaN</td>
      <td>2016-03-14 00:00:00</td>
      <td>0</td>
      <td>90480</td>
      <td>2016-04-05 12:47:46</td>
    </tr>
  </tbody>
</table>
</div>
