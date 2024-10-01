# Проект по классификации взаимодействий клиентов

## Описание проекта

Этот проект направлен на построение модели машинного обучения для предсказания взаимодействий клиентов с различными маркетинговыми каналами и событиями. Задача заключается в том, чтобы предсказать, будет ли клиент вовлечён (целевой класс `1`) или нет (целевой класс `0`) на основе различных характеристик их поведения.

## Данные

Основной набор данных содержит информацию о взаимодействиях клиентов с маркетинговыми каналами и событиями. Для каждого клиента представлены следующие признаки:

- `client_id`: идентификатор клиента.
- `total_quantity`: общее количество покупок клиента.
- `total_spent`: общая сумма, потраченная клиентом.
- `avg_price`: средняя цена за покупку.
- `max_price`: максимальная цена за покупку.
- `total_clicks`: общее количество кликов.
- `total_opens`: общее количество открытий писем.
- `days_since_last_purchase`: количество дней с момента последней покупки.
- `event`: тип события (клик, покупка, отправка и др.).
- `channel`: канал, по которому было отправлено сообщение (email, push и др.).
- `has_interaction`: индикатор взаимодействия с маркетинговыми кампаниями.
- `target`: целевая переменная (1 - вовлечённый клиент, 0 - невовлечённый клиент).

### Проблемы с данными

1. **Несбалансированные классы**: Класс 1 (вовлечённые клиенты) встречается крайне редко (1.9%), что требует дополнительных методов для работы с дисбалансом.
2. **Мультиколлинеарность**: Некоторые признаки имеют высокую корреляцию, что было учтено с помощью анализа Variance Inflation Factor (VIF).

## Методы

### Препроцессинг данных

1. **Обработка пропусков**: Пропуски в категориальных и числовых данных были заполнены значениями на основе стратегии "no_information".
2. **Нормализация**: Числовые признаки были нормализованы для улучшения работы модели.
3. **Мультиколлинеарность**: Удалены признаки с высокой мультиколлинеарностью на основе VIF.
4. **Обработка дисбаланса**: Предприняты попытки улучшить распознавание редкого класса, включая взвешивание классов и oversampling методов (например, SMOTE).

### Используемая модель

Была использована модель классификации (например, `CatBoostClassifier` или `RandomForestClassifier`), настроенная для работы с несбалансированными данными.

Основные этапы:
- Построение базовых моделей.
- Оптимизация гиперпараметров.
- Оценка на тестовой выборке с использованием метрик, таких как ROC AUC и F1.

## Метрики

1. **ROC AUC Score**: 0.706.
2. **Precision и Recall** для класса 1 равны 0, что связано с дисбалансом классов.
3. **Общая точность**: 0.98 (ввиду сильного перевеса класса 0).

## Как запустить проект

1. Установите зависимости:
    ```bash
    pip install -r requirements.txt
    ```

2. Подготовьте данные:
    - Поместите файл с данными в директорию `data/` и убедитесь, что он в нужном формате.

3. Запустите скрипт обучения модели:
    ```bash
    python train_model.py
    ```

4. Для визуализации результатов (scatter plot, VIF):
    ```bash
    python visualize.py
    ```

## Используемые библиотеки

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `statsmodels`
- `gensim` (для работы с Word2Vec эмбеддингами)
- `CatBoost`, `XGBoost` или другие алгоритмы

## Результаты и выводы

Модель показала хороший результат по общей точности, но проблемы с дисбалансом классов остаются актуальными. Для дальнейшего улучшения результатов можно применить техники генерации синтетических данных для увеличения числа наблюдений целевого класса.

## Контакты

