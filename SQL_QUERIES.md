# SQL-запросы

## Создание базы данных

> Выполняется в `psql`.

```sql
CREATE DATABASE p1_w3_d1_t1 OWNER postgres;
```

---

## Создание таблицы `movies`

```sql
CREATE TABLE movies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    title VARCHAR(100) NOT NULL UNIQUE,
    director VARCHAR(100),
    year INTEGER CHECK (year >= 1888),
    rating DECIMAL(3,1) CHECK (rating >= 0 AND rating <= 10),
    genres VARCHAR(50)[] NOT NULL DEFAULT ARRAY[]::VARCHAR[],
    is_released BOOLEAN NOT NULL DEFAULT TRUE,
    add_date TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

---

## Заполнение таблицы

```sql
INSERT INTO movies (
    title,
    director,
    year,
    rating,
    genres,
    is_released
)
VALUES
(
    'Прибытие поезда',
    'Люмьеры',
    1896,
    7.5,
    ARRAY['документальный'],
    TRUE
),
(
    'Начало',
    'Кристофер Нолан',
    2010,
    8.8,
    ARRAY['фантастика', 'триллер'],
    TRUE
),
(
    'Дюна: часть третья',
    'Дени Вильнёв',
    2027,
    NULL,
    ARRAY['фантастика'],
    FALSE
);
```

---

## Получить все фильмы

```sql
SELECT *
FROM movies;
```

---

## Получить фильм по ID

```sql
SELECT *
FROM movies
WHERE id = '293dd0dc-e7d2-4909-9e26-e4ed443e880c';
```

---

## Получить только вышедшие фильмы

```sql
SELECT *
FROM movies
WHERE is_released = TRUE;
```

---

## Обновить рейтинг фильма

```sql
UPDATE movies
SET rating = 9.0
WHERE id = '293dd0dc-e7d2-4909-9e26-e4ed443e880c';
```

---

## Удалить фильм

```sql
DELETE FROM movies
WHERE id = '293dd0dc-e7d2-4909-9e26-e4ed443e880c';
```