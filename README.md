# Relational Databases for Data Science — Homework 2

Домашня робота з завантаження даних у PostgreSQL, staging/clean-підхід, аудит якості та базовий DQL/EDA.

## Dataset

Для роботи використано **UCI Bank Marketing**.

Офіційне джерело:

https://archive.ics.uci.edu/dataset/222/bank+marketing

У роботі використовується повний набір **bank-full.csv**.

## Вибірка

Додаткова вибірка не формувалась: використано весь доступний набір Bank Marketing.

Кількість рядків:

```text
45 211
```

Кількість колонок:

```text
17
```

Дані отримуються відтворюваним способом у notebook через `ucimlrepo` за ID `222`.

Оскільки `ucimlrepo` представляє частину документованих категорій `unknown` як `NaN`, перед формуванням CSV ці значення явно відновлюються для колонок `job`, `education`, `contact` і `poutcome`. Після цього CSV завантажується в PostgreSQL через `COPY FROM STDIN`.

## Структура обробки

```text
UCI Bank Marketing
        ↓
CSV
        ↓
hw3_bank_staging
        ↓
INSERT INTO ... SELECT
        ↓
hw3_bank_marketing
        ↓
Data-quality audit / DQL / EDA
```

Staging-таблиця зберігає сирі значення як `TEXT`. Типізація та мінімальне очищення виконуються вже в PostgreSQL під час перенесення даних у фінальну таблицю.

## Запуск

1. Відкрити `goit-rdb-hw-03-final.ipynb` у Google Colab.
2. Виконати **Runtime → Restart session and run all**.
3. Notebook:
   - перевірить наявність PostgreSQL і встановить його за потреби;
   - запустить PostgreSQL як системний сервіс;
   - встановить Python-залежності;
   - створить базу `goit_hw3`;
   - завантажить UCI Bank Marketing;
   - створить staging- і clean-таблиці;
   - завантажить дані через `COPY FROM STDIN`;
   - виконає аудит якості, аналіз розподілів, outlier-check та DQL/EDA-запити.

Ручне завантаження або підготовка CSV не потрібні.

## Основні технології

- PostgreSQL 16
- Python
- pandas
- SQLAlchemy
- Psycopg 3
- Google Colab
