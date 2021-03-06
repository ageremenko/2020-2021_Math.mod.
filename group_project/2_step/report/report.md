---
# Front matter
lang: ru-RU
title: "Отчёт по второму этапу группового проекта"
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

Проработать алгоритм решения поставленной научной проблемы.

# Описание алгоритма

В начальный момент времени частицы будут распределяться в плоскости случайным 
образом. При достаточно большом количестве частиц распределение будет 
равномерным. Модуль радиус-вектора $|r|$ и азимутальный угол $\alpha$ выберем случайным 
образом, радиус газопылевого облака $r_0$ зададим вручную. Тогда согласно закону 
Кеплера получаем, что $v_x = - y\omega_0(\frac{r_0}{r})^\frac{3}{2}$, 
$v_y = - x\omega_0(\frac{r_0}{r})^\frac{3}{2}$, $v_z = 0$, где $\omega_0$ 
- угловая скорость частиц на расстоянии $r_0$ от оси диска.

Потенциальная энергия гравитационного взаимодействия одной частицы 
со всеми остальными описывается формулой:

$$U_i = -\sum_{j \neq i} \frac{\gamma m_j m_i}{r_{i j}}$$

Полная потенциальная энергия системы частиц равна:

$$U = \frac{1}{2} \sum_i U_i$$

Сила, действующая на данную молекулу равна:

$$F_i = - \frac{\partial U}{\partial r_i}$$

Движение частиц описывается вторым законом Ньютона: 
$$m_i \frac{d^2 r_i}{d t^2} = F_i.$$

В итоге имеем систему, состоящую из N обыкновенных дифференциальных 
уравнений второго порядка, перепишем эти уравнения в виде дифференциальных уравнений 
первого порядка:

$$\left\{\begin{matrix} \frac{d r_i}{d t} = v_i \\ \frac{d v_i}{d t} = a_i \end{matrix}\right.$$

Данные уравнения позволяют моделировать движение частиц без учёта сил трения 
и отталкивания. Сила отталкивания появится при движении частиц на расстояние 
меньшее их радиусов, она будет равна:

$$F^r(b) = k((\frac{a}{b})^8 - 1)$$

Здесь $a=R_i+R_j$, сумма радиусов частиц, $b=r_{i,j}=r_i - r_j$.

Энергия отталкивания в таком случае равна:

$$E=-\int^r F^r(x)dx$$

Сила трения перпендикулярна радиус-вектору взаимодействия b и 
направлена против движения частиц относительно друг друга. 
Единичный вектор вдоль силы трения для двумерной модели равен:

$$n = (n_x, n_y) = \frac{-b_y, b_x}{\sqrt{b_x^2 + b_y^2}}$$

Относительная скорость поверхностей частиц, перпендикулярная радиусу,
$W_\perp = W \cdot n - \omega_i R_i - \omega_j R_j$, где \omega_i и \omega_j — угловые скорости вращения
частиц i и j, $W = v_i - v_j$ - относительная скорость двух взаимодействий соответствующих частиц.

# Вывод

В ходе работы был составлен алгоритм решения поставленной научной проблемы.