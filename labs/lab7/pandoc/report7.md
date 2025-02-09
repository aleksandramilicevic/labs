---
# Front matter
lang: ru-RU
title: "Лабораторная работа №7"
subtitle: "Дисциплина: Математические основы защиты информации и информационной безопасности"
author: "Миличевич Александра"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # Список рисунков
lot: true # Список таблиц
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---
#### Как работает:

1.  **Базовый случай:** Если `b` равно 0, возвращается кортеж `(a, 1, 0)`.
2.  **Рекурсия:** Рекурсивно вызывается `extended_euclidean(b, a % b)`, результат разворачивается, и вычисляются новые коэффициенты `x` и `y`.

### 1. Функция `modular_inverse(a, n)`

Эта функция вычисляет обратное к `a` по модулю `n`.

#### Описание:

*   **Вход:**
    *   `a` (int): Число, для которого ищется обратное.
    *   `n` (int): Модуль.
*   **Выход:**
    *   Обратное к `a` по модулю `n`.

#### Как работает:

1.  Используется функция `extended_euclidean(a, n)` для получения коэффициентов Безу.
2.  Возвращается коэффициент `x` (второй элемент в кортеже), который является обратным к `a` по модулю `n`.
![ modular inverse ](images/modular_inverse.jpg){ width=70% }

### 2. Функция `pollard_step(x, a, b, params)`

Эта функция реализует один шаг алгоритма Полларда для дискретного логарифмирования.

#### Описание:
*   **Вход:**
    *   `x` (int): Текущее значение `x`.
    *   `a` (int): Текущее значение `a`.
    *   `b` (int): Текущее значение `b`.
    *   `params` (tuple): Параметры (G, H, P, Q).
*  **Выход:**
    *   Кортеж обновленных значений `(x, a, b)`.

#### Как работает:

1. **Разделение на подмножества:** Использует `x % 3` для определения подмножества.
2. **Обновление значений в зависимости от подмножества:**
   * Если `x % 3 == 0`: `x` умножается на `G` по модулю `P`, `a` увеличивается на 1 по модулю `Q`.
   * Если `x % 3 == 1`: `x` умножается на `H` по модулю `P`, `b` увеличивается на 1 по модулю `Q`.
   * Если `x % 3 == 2`: `x` возводится в квадрат по модулю `P`, `a` и `b` умножаются на 2 по модулю `Q`.

![ pollard step ](images/pollard_step.jpg){ width=70% }

### 3. Функция `pollard_rho_discrete_log(generator, value, prime)`

Эта функция реализует алгоритм Полларда для дискретного логарифмирования.

#### Описание:

*   **Вход:**
    *   `generator` (int): Генератор группы.
    *   `value` (int): Значение, для которого ищется дискретный логарифм.
    *   `prime` (int): Простое число (порядок группы).
*   **Выход:**
    *   Дискретный логарифм (если найден) или сообщение об ошибке.

#### Как работает:

1.  **Инициализация:** Устанавливаются начальные значения `Q`, `x`, `a`, `b`, `X`, `A`, `B`.
2.  **Основной цикл:**
    *   Используются "заяц" и "черепаха" для поиска коллизии, где заяц делает два шага за итерацию, а черепаха - один.
    *   Функция `pollard_step` применяется для каждого шага.
    *   Цикл выполняется до тех пор, пока не будет найдена коллизия (`x == X`).
3.  **Вычисление дискретного логарифма:**
    *   Вычисляется числитель `a - A` и знаменатель `B - b`.
    *   Вычисляется обратный элемент знаменателя по модулю `Q` с помощью функции `modular_inverse`.
    *   Вычисляется дискретный логарифм: `(inverse_denominator * numerator) % Q`.
4.  **Верификация:** Вызывается функция `verify` для проверки правильности найденного логарифма.
    *   Если логарифм верный, то он возвращается.
    *   Если логарифм не верный (при `pow(generator, result, prime) != value`), то `result` увеличивается на `Q` и возвращается.

![ pollard descrete log ](images/pollard_rho_descrete_log.jpg){ width=70% }

### 4. Функция `verify(generator, value, prime, x)`

Эта функция проверяет правильность вычисленного дискретного логарифма.

#### Описание:

*   **Вход:**
    *   `generator` (int): Генератор группы.
    *   `value` (int): Значение, для которого ищется дискретный логарифм.
    *   `prime` (int): Простое число (порядок группы).
    *   `x` (int): Вычисленный дискретный логарифм.
*   **Выход:**
    *   `True`, если логарифм верный, `False` в противном случае.

![ verify ](images/verify.jpg){ width=70% }

#### Как работает:

1. Вычисляет `generator^x mod prime`.
2. Сравнивает с `value`. Возвращает `True`, если равны, иначе `False`.

