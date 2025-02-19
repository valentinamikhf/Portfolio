### Прогноз количества заказов такси на следующий час: описание

- Компания «Чётенькое такси» собрала исторические данные о заказах такси в аэропортах.
- Чтобы привлекать больше водителей в период пиковой нагрузки, необходимо сТребуется построить модель для такого предсказания.
По условию заказчика:
- Значение метрики RMSE на тестовой выборке должно быть не больше 48.
- Тестовая выборка должна быть размером 10% от исходных данных.

### Ход работы над проектом
- Данные загружены и в хожде знакомства с ними выяснено, что в датасете имеется информация за период с 1 марта 2018 года по 31 августа 2018 года. Всего 26496 строк
- Произведено ресемплирование данных по одному часу.
- Произведен сследовательский анализ данных : оценивали тренды и сезонность, используя скользящее среднее
- Произведена проверка ряда на стационарность при помощи теста Дики-Фуллера
- Созданы дополнительные признаки: день недели, час, "отстающие значения" (24 значения) и скользящее среднее (окно 24 часа).
- На дополненном датасете обучены модели:
  - LinearRegression,
  - DesisionTreeRegressor,
  - RandomForestRegressor,
  - CatBoost
  - LGBMRegressor
  и подобраны оптимальные гиперпараметры для них.
- На кросс-валидации рассчитаны метрики RMSE для всех моделей. Всем моделям удалось достичь требуемого показателя метрики RMSE - не более 48,0
- Проверка модели на адекватность показала, что все модели с метриками меньше, чем 56.44, могут считаться адекватными.
- Наилучший показатель RMSE на тренировочной выборке был у CatBoostRegressor = 23.60, она и была проверена на тестовой выборке.


### Выводы и рекомендации
- RMSE модели CatBoostRegressor на тестовой выборке : 36.779. Модель адекватна. Модель удовлетворяет условию: "Значение метрики RMSE на тестовой выборке должно быть не больше 48."
- Анализ сравнительных графиков в двух масштабах, показал, что модель предсказывает хорошо, не пропуская практически ни одного пика. Модель хуже всего справляется с предсказаниями на высоких пиках и на части провалов, но в целом, угадывают направления движения.
- Рекомендуется к использованию модель CatBoost с гиперпараметрами: {'depth': 4, 'learning_rate': 0.03}

Дополнительно можно отметить:
- хорошо было бы иметь больше данных и разобраться с гипотезой о сезонности такси
- можно попробовать добавить признак "праздничный день", поскольку в праздничные дни точно изменяется поведение клиентов
- неплохо было бы также добавить в прогнозную модель крупные события в городе, которые могут повлиять на количество вызовов в час не просто в дни этих событий, а в часы этих событий (крупный концерт, форум, конференция, спортивные соревнования масштаба страны или мирового масштаба)
