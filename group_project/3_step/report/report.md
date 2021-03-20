---
# Front matter
lang: ru-RU
title: "Отчёт по третьему этапу группового проекта"
subtitle: "Образование планетной системы"
author: "Абакумов Егор, Сухарев Кирилл, Калинина Кристина, Еременко Артем"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
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

Провести моделирование одного из этапов эволюции Вселенной - образование некой «солнечной» 
системы из межзвездного газа.

## Цель этапа

Написать программу, реализующую модель образования планетарной системы.

# Описание программы

## Константы

- Количество частиц($N$);

- Гравитационная постоянная($G$). В целях ускорения процесса может отличаться от существующей;

- Коэффициент отталкивания($k$);

- Временной промежуток между итерациями ($dt$).

## Переменные

Каждая частица имеет следующие характеристики: 

- координаты ($x, y$), определяющие положение частицы в пространстве;

- скорость ($v_x, v_y$);

- ускорение ($a_x, a_y$);

- радиус ($r$), определяющий размеры частицы;

- масса ($m$);

- коэффициент трения ($\mu$).

## Ход программы

На каждой итерации:

1. Для каждой частицы:

* создаём переменные для нового ускорения ($a_{n + 1}$)

* в них помещаем ускорение, образованное векторной суммой следующих сил:

    * $a_1 = G \frac{m}{r^2}$, направлено вдоль прямой, соединяющей 2 частицы;
	
    * $a_2 = \frac{k}{m} ((\frac{a}{b})^8 - 1)$, направлено против прямой, соединяющей 2 частицы;
	
    * $a_3 = \mu a_2$, направлено перпендикулярно прямой, соединяющей 2 частицы;

    * данные ускорения считаются для каждой пары частиц.

2. Рассчитываем новые координаты:

$$ x_{n+1} = x_n + v_n dt + \frac {a_n dt^2}{2}$$

3. Рассчитываем новые скорость и ускорение: 

$$ v_{n+1} = v_n + \frac {a_{n + 1} + a_n}{2} dt $$

4. При сближении частиц на расстояние меньшее трети суммы их радиусов производим слипание частиц

$$ r = \frac {m_i r_i + m_j r_j}{ m_i + m_j } $$

$$ v = \frac {m_i v_i + m_j v_j}{ m_i + m_j } $$

$$ R = \sqrt[3]{R_i^3 + R_j^3} $$

# Вывод

В ходе работы был разработан программный код решения поставленной научной проблемы.