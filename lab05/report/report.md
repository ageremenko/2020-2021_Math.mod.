---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №5"
subtitle: "дисциплина: Математическое моделирование"
author: "Ерёменко Артём Геннадьевич, НПИбд-02-18"

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

Построить модель Лотки-Вольтерры типа "хищник - жертва" с помощью Julia.

# Задание

**Вариант 4**

Для модели «хищник-жертва»:

$$
\begin{cases}
    \frac{\partial x}{\partial t} = -0.15x(t)+0.044x(t)y(t)
    \\
    \frac{\partial y}{\partial t} = 0.35y(t)-0.032x(t)y(t)
\end{cases}
$$

Постройте график зависимости численности хищников от численности жертв, а также графики изменения численности хищников и численности жертв при следующих 
начальных условиях: $x_0 = 9, y_0 = 14$. Найдите стационарное состояние системы.

# Выполнение лабораторной работы

1. Полагается, что $x$ -- число жертв, а $y$ -- число хищников. Изучил начальные условия. Коэффициент 0,15 описывает скорость естественного 
прироста числа жертв в отсутствие хищников, 0,35 -- естественное вымирание хищников, лишенных пищи в виде жертв. Вероятность взаимодействия жертвы и хищника 
считается пропорциональной как количеству жертв, так и числу самих хищников $(xy)$. Каждый акт взаимодействия уменьшает популяцию жертв, но способствует 
увеличению популяции хищников (коэффициенты 0,044 и 0,032). Стационарное состояние будет в точке: $x_0 = 9, y_0 = 14$.

2. Оформил начальные условия в код на Julia:

```
	a = 0.15
	b = 0.044
	c = 0.35
	d = 0.032
	par = [a,b,c,d]

	x0 = 9
	y0 = 14
	u0 = [x0,y0]

```

3. Решение для колебаний изменения числа популяции хищников и жертв искал на интервале $t \in [0; 200]$ (шаг 0,05), значит, $t_{0} = 0$ -- начальный момент 
времени, $t_{max} = 200$ -- предельный момент времени, $dt = 0,05$ -- шаг изменения времени.

4. Добавил в программу условия, описывающие время:
```
	t0 = 0
	tmax = 200
	t = (t0, tmax)
	dt = 0.05
```

5. Запрограммировал заданную систему уравнений: 
```
function model(du,u,p,t)
    a,b,c,d = p
    x, y = u
    du[1] = -a*x+b*x*y
    du[2] = c*y-d*x*y
    return du
end
```

6. Запрограммировал решение системы уравнений:
```
sol = solve(ODEProblem(model, u0, t, par), saveat = dt)
```

7. Переписал отдельно $x$ (жертв) в $y_1$, а $y$ (хищников) в $y_2$:
```
n = size(sol,2)
#Переписываем отдельно
#x в y1, y в y2
y1 = Array{Float16}(undef, n)
y2 = Array{Float16}(undef, n)
for i = 1: n
    y1[i] = sol[1, i]
    y2[i] = sol[2, i]
end
```

8. Описал построение графика колебаний изменения числа популяции хищников и жертв:
```
plot(sol, xlabel = "Время", ylabel = "Численность", label = ["Хищники" "Жертвы"])
```

9. Описал построение графика зависимости изменения численности хищников от изменения численности жертв:
```
plot(y1,y2, xlabel = "Число жертв", ylabel = "Число хищников", label = "Эволюция популяций")
```

10. Добавил на второй график обозначение стационарного состояния:
```
scatter!((x0,y0), label = "Стационарное состояние")
```

11. Собрал код программы воедино и получил следующее:
```
using DifferentialEquations, Plots

a = 0.15
b = 0.044
c = 0.35
d = 0.032
par = [a,b,c,d]

x0 = 9
y0 = 14
u0 = [x0,y0]

t0 = 0
tmax = 200
t = (t0, tmax)
dt = 0.05

function model(du,u,p,t)
    a,b,c,d = p
    x, y = u
    du[1] = -a*x+b*x*y
    du[2] = c*y-d*x*y
    return du
end

sol = solve(ODEProblem(model, u0, t, par), saveat = dt)

plot(sol, xlabel = "Время", ylabel = "Численность", label = ["Хищники" "Жертвы"])
```

```
n = size(sol,2)
#Переписываем отдельно
#x в y1, y в y2
y1 = Array{Float16}(undef, n)
y2 = Array{Float16}(undef, n)
for i = 1: n
    y1[i] = sol[1, i]
    y2[i] = sol[2, i]
end

plot(y1,y2, xlabel = "Число жертв", ylabel = "Число хищников", label = "Эволюция популяций") 
scatter!((x0,y0), label = "Стационарное состояние")
```

12. Получил графики колебаний изменения числа популяции хищников и жертв (см. рис. -@fig:001), а также график зависимости изменения численности хищников 
от изменения численности жертв (см. рис. -@fig:002):

![Колебания изменения числа популяции хищников и жертв](images/1.png){ #fig:001 width=70% }

![Зависимость изменения численности хищников от изменения численности жертв](images/2.png){ #fig:002 width=70% }

# Выводы

Построил модель Лотки-Вольтерры типа "хищник -- жертва" с помощью Julia.