## Maternal Health Risk


- Задача: создать прогностическую модель рисков беременных.
- Метрика: решаете сами
- Особенности: В последних ячейках необходимо вывести метрики и матрицу ошибок на трейне и тесте.

**Описание данных:**

`Age`: Age in years when a woman is pregnant.

`SystolicBP`: Upper value of Blood Pressure in mmHg, another significant attribute during pregnancy.

`DiastolicBP`: Lower value of Blood Pressure in mmHg, another significant attribute during pregnancy.

`BS`: Blood glucose levels is in terms of a molar concentration, mmol/L.

`HeartRate`: A normal resting heart rate in beats per minute.

`Risk Level`: Predicted Risk Intensity Level during pregnancy considering the previous attribute.

### Модели машинного обучения

Для обучения были выбраны модели:
- LogisticRegression
- KNeighboursClassifier
- DesigionTreeClassifier
- RandomForestClassifier
- LGBMClassifier
- CatBoostRegressor

Все они были обучены с предварительным масштабированием и без него, результаты занесены в таблицу.

После этого была выбрана лучшая модель. Это оказалась модель CatBoost с параметрами :

```python
{'model__bagging_temperature': 0.5,
 'model__depth': 3,
 'model__l2_leaf_reg': 3,
 'model__learning_rate': 0.01,
 'model__od_type': 'IncToDec',
 'model__random_strength': 1.5}
```

 После этого была построена матрица ошибок, по которой стало очевидно, что лучшая модель хорошо определяет класс низкого и высокого риска, а средний риск путает с низким.
 
 Было принято решение добавить синтетически представителей класса среднего риска, что и было сделано с использованием SMOTE.

После этого на новых данных с добавлением синтетики была обучена модель catboost, для которой взяли лучшие параметры по кросс-валидации предыдущего шага. Данная модель показала себя лучше, угадывая уже 25% класс среднего риска против 12,5 в лучшей модели до балансировки данных.

_______________________________________

 В случае, если не рендерится ноутбук, [ссылка на google colab с ноутбуком](https://colab.research.google.com/drive/1V36czcGNlxQjFwYbUeFFoQMoi2z8TXNf?usp=sharing)
