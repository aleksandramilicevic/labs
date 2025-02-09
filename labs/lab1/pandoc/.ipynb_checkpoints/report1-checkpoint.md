---
# Front matter
lang: ru-RU
title: "Лабораторная работа №1"
subtitle: "Дисциплина: Математические основы защиты информации и информационной безопасности"
author: "Алгайли Абдулазиз Мохаммед"

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

Познакомиться с шифрами Цезаря и Атбаш.

# Задание

1. Реализовать шифр Цезаря с произвольным ключом k.
2. Реализовать шифр Атбаш.

# Выполнение лабораторной работы

1) Этот код реализует шифр Цезаря для шифрования текста. Он сдвигает каждую букву на указанное число позиций в алфавите, сохраняя регистр (заглавные или строчные). Все остальные символы, такие как цифры или знаки препинания, остаются без изменений. Формула (ord(char) - ord('a') + shift) % 26 + ord('a') используется для преобразования букв: она вычисляет позицию буквы в алфавите, добавляет сдвиг, возвращает результат в диапазон от 0 до 25 (циклично) и преобразует обратно в символ.

![Шифр Цезаря](images/ceaser1.png){ width=70% }

2)Этот код запрашивает у пользователя текст и значение сдвига, затем вызывает функцию caesar_cipher для шифрования текста и выводит результат на экран.

![вывод результата шифра Цезаря](images/ceaser2.png){ width=70% }

3)В строке reverse_alphabet = alphabet[::-1] создается перевернутый алфавит, где буквы идут в обратном порядке. Затем с помощью генератора словаря cipher_dict для каждой буквы из оригинального алфавита создается пара, сопоставляющая её с буквой из перевернутого алфавита.
![reverse alphabet](images/Atbash1.png){ width=70% }
4)
Этот код перебирает каждый символ в строке text (приведенной к нижнему регистру). Если символ — буква, она заменяется по словарю cipher_dict; если нет (например, пробел или знак препинания), символ остается без изменений. Все измененные символы собираются в список result, который затем объединяется в строку и возвращается.
![цикл главный](images/Atbash2.png){ width=70% }
5)Код шифрует строку text с помощью функции atbash_cipher и выводит исходный и зашифрованный текст.
![вывод](images/Atbash3.png){ width=70% }
# Выводы

Реализрваны шифр Цезаря и  шифр Атбаш.