---
# Front matter
lang: ru-RU
title: "Лабораторная работа №2"
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

# Цель работы

Познакомиться с шифрами перестановки.

# Задание

1. Программно реализовать маршрутное шифрование.
2. Программно реализовать шифрование с помощью решёток.
3. Программно реализовать шифр Виженера.

# Выполнение лабораторной работы
### Маршрутное шифроваие

1) Код сначала подготавливает текст для шифрования, заменяя пробелы на “sp” и определяя размеры матрицы на основе длины текста и заданного ключа. Затем, символы текста последовательно записываются в матрицу по строкам, заполняя её слева направо и сверху вниз. Эта матрица используется для маршрутного шифрования.

![ реализация маршрутного шифрования](images/route_encryption1.jpg){ width=70% }

1.1     # 3. Чтение матрицы по столбцам
    cipher_text = "" После заполнения матрицы, код считывает ее по столбцам сверху вниз, формируя зашифрованный текст. Символы каждого столбца добавляются в общий шифрованный текст, который затем возвращается как результат работы алгоритма. Таким образом текст шифруется путем записи по строкам и чтения по столбцам.
![ реализация маршрутного шифрования2](images/route_encryption2.jpg){ width=70% }

### Шифрование с помощью решеток
Этот код реализует шифрование с использованием решетки (grill  e cipher). Сначала он подготавливает текст, удаляя пробелы и проверяя, что текст не превышает размер решетки. Затем, он создает матрицу (решетку) нужного размера, заполняет ее символами текста в порядке, заданном списком grille, и, наконец, считывает матрицу построчно, формируя зашифрованный текст.

В примере, решетка (grille) задается списком кортежей, где каждый кортеж указывает строку и столбец, куда должен быть помещен соответствующий символ текста. Результат работы алгоритма — зашифрованный текст, сформированный из прочитанных по строкам элементов матрицы.
![ реализация шифрования с помощью решеток](images/grillie_encryption.jpg){ width=70% }

### Таблица Виженера 
Этот код реализует шифрование Виженера, где каждый символ текста сдвигается на величину, определяемую соответствующим символом ключа, повторяющегося по циклу. Функция vigenere_cipher_encrypt сначала приводит текст и ключ к верхнему регистру, а затем для каждой буквы текста вычисляет её сдвиг, используя соответствующую букву ключа и выполняя операцию взятия остатка от деления на 26. Результатом является шифрованный текст, где неалфавитные символы остаются неизменными.В этом конкретном примере текст “HELLO” шифруется с помощью ключа “KEY”, что приводит к зашифрованному тексту, где буквы сдвигаются на величину, задаваемую буквами ключа. Разница между шифрованием Виженера и другими шифрами, например, маршрутным или решеточным, заключается в том, что Виженер использует полиалфавитный шифр с циклическим ключом, в то время как маршрутный и решеточный шифры используют перестановку символов.

![ реализация  шифрования таблица виженера ](images/vigenere_encryption.jpg){ width=70% }

В коде для шифрования Виженера на русском языке, добавлен русский алфавит (alphabet_ru) и его длина (alphabet_length), чтобы обрабатывать символы русского языка. Индексы букв берутся из русского алфавита alphabet_ru.find(), и для шифрования используется модуль от деления на длину русского алфавита. Если символ не найден в русском алфавите, он добавляется в зашифрованный текст без изменений.
![ с русским алфавитом таблица Виженера](images/vigenere_encryption_ru.jpg){ width=70% }

# Выводы

Программно реализованы шифры перестановки.