---
## Front matter
lang: ru-RU
title: "Отчет по лабораторной работе 4"
author: |
	Artyom Gennadievich Yeryomenko\inst{1}
institute: |
	\inst{1}RUDN University, Moscow, Russian Federation

## Formatting
toc: false
slide_level: 2
theme: metropolis
header-includes: 
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
aspectratio: 43
section-titles: true
---

# **Цель выполнения лабораторной работы**

## Цель

Построить модель гармонических колебаний с помощью Julia.

# **Задачи выполнения лабораторной работы**

## Задание. Вариант 41

Постройте фазовый портрет гармонического осциллятора и решение уравнения гармонического осциллятора для следующих случаев:

1. Колебания гармонического осциллятора без затуханий и без действий внешней силы $\ddot {x} + 15x = 0$

2. Колебания гармонического осциллятора c затуханием и без действий внешней силы $\ddot {x} + 10 \dot {x} + x = 0$

3. Колебания гармонического осциллятора c затуханием и под действием внешней силы $\ddot {x} + 3 \dot {x} + x = \sin (3t)$

На интервале $t \in [0; 55]$ (шаг 0,05) с начальными условиями $x_0 = 0, y_0 = 2$

# **Результаты выполнения лабораторной работы**

## График колебаний без затуханий и без действий внешней силы

![](images/1.png){ #fig:001 width=70% } 

## График колебаний c затуханием и без действий внешней силы

![](images/2.png){ #fig:002 width=70% }

## График колебаний c затуханием и под действием внешней силы

![](images/3.png){ #fig:003 width=70% }

## Выводы

Построил модель гармонических колебаний с помощью Julia.