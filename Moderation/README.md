### Модерация токсичных комментариев: описание
Интернет-магазин «Викишоп» запускает новый сервис. Теперь пользователи могут редактировать и дополнять описания товаров, как в вики-сообществах. То есть клиенты предлагают свои правки и комментируют изменения других. Магазину нужен инструмент, который будет искать токсичные комментарии и отправлять их на модерацию.

Требуется обучить модель классифицировать комментарии на позитивные и негативные при помощи имеющегося набора данных с разметкой о токсичности правок.

Необходимо построить модель со значением метрики качества F1 не меньше 0.75.

### Ход работы над проектом
- Данные лемматизированы с использованием SpaSy и очищены
- На подготовленных данных обучены три модели:
  - Logisticregression,
  - DecisionTreeClassifier
  - CatBoost.
- Параметры подобраны на тренировочной выборке, на кросс-валидации определена метрика F1 для каждой модели

### Выводы и рекомендации
- Лучшая модель по итогам проверки на кросс-валидации - это модель Logisticregression с метрикой F1 = 0,7601
- Модель Logisticregression рекомендована к работе, проверена на тестовой выборке и выдает метрику для предсказания на ней, равную 0,7561
