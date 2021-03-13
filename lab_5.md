---
# Front matter
lang: ru-RU
title: "Отчет по лабораторной работе №5 "

subtitle: "Модель хищник-жертва"

author: "Миличевич Александра, НПИ-02-18"


 
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

Создать простейшую модель взаимодействия двух видов типа «хищник — жертва» -
модель Лотки-Вольтерры

# Задание
**Вариант 27**

Для модели хищник-жертва:

$\frac{dx}{dt}$ = -0.73x(t)+0.037x(t)y(t)

$\frac{dy}{dt}$ = -0.52x(t)+0.039x(t)y(t)

Постройте график зависимости численности хищников от численности жертв,

а также графики изменения численности хищников и численности жертв при

следующих начальных условиях:

x~0~ = 7 , y~0~ = 16

Найдите стационарное состояние системы.



# Выполнение лабораторной работы

## Постановка задачи

В лесу проживают х число волков, питающихся зайцами, число которых в
этом же лесу у. Пока число зайцев достаточно велико, для прокормки всех волков,
численность волков растет до тех пор, пока не наступит момент, что корма
перестанет хватать на всех. Тогда волки начнут умирать, и их численность будет
уменьшаться. В этом случае в какой-то момент времени численность зайцев снова
начнет увеличиваться, что повлечет за собой новый рост популяции волков. Такой
цикл будет повторяться, пока обе популяции будут существовать. Помимо этого,
на численность стаи влияют болезни и старение. Данная модель описывается
следующим уравнением:

*$\frac{dx}{dt}$ = -ax(t)+bx(t)y(t)*

*$\frac{dx}{dt}$ = cy(t)+dx(t)y(t)*

*a, d - коэффициенты смертности*

*b, c - коэффициенты прироста популяции*

1. Построить график зависимости x от y и графики функций

*x(t), y(t)*

2. Найти стационарное состояние системы

фомула по которой основиваем нашу систему (рис. -@fig:001).

![Модель](image/formula1.png){ #fig:001 width=70% }

В этой модели *x* – число жертв, *y* - число хищников. Коэффициент a
описывает скорость естественного прироста числа жертв в отсутствие хищников, с
- естественное вымирание хищников, лишенных пищи в виде жертв. Вероятность
взаимодействия жертвы и хищника считается пропорциональной как количеству
жертв, так и числу самих хищников *(xy)*. Каждый акт взаимодействия уменьшает
популяцию жертв, но способствует увеличению популяции хищников (члены -bxy
и dxy в правой части уравнения). 






**Код задачи**
```
import numpy as np
from scipy. integrate import odeint
import matplotlib.pyplot as plt
import math

a = 0.73
b = 0.037
c = 0.52
d = 0.039

y0 = [16, 7]

def syst2(y, t):
    y1, y2 = y
    return [-a*y1 + b*y1*y2, c*y2 - d*y1*y2 ]

t = np.arange( 0, 200, 0.1)
y = odeint(syst2, y0, t)
y11 = y[:,0]
y21 = y[:,1]

fig = plt.figure(facecolor='white')
plt.plot(t, y11, linewidth=2)
plt.ylabel("x")
plt.xlabel("t")
plt.grid(True)
plt.show()
fig.savefig('01.png', dpi = 600)

fig2 = plt.figure(facecolor='white')
plt.plot(t, y21, linewidth=2)
plt.ylabel("y")
plt.xlabel("t")
plt.grid(True)
plt.show()
fig2.savefig('02.png', dpi = 600)

fig3 = plt.figure(facecolor='white')
plt.plot(y11, y21, linewidth=2)
plt.ylabel("y")
plt.xlabel("x")
plt.grid(True)
plt.show()
fig3.savefig('03.png', dpi = 600)

print("Xст = ", a/b)
print("Yст = ", c/d)
```
**Полученные графы**

Построение графика колебаний изменения числапопуляции хищников (рис. -@fig:002).

![Хищники](image/хищники.png){ #fig:002 width=70% }

Построение графика колебаний изменения числа популяции жертв  (рис. -@fig:003)

![Жертвы](image/жертвы.png){ #fig:003 width=70% }

Построение графика зависимости изменения численности хищников от изменения численности жертв (рис. -@fig:004)

![Численность_изменения](image/Численность_изменения.png){ #fig:004 width=70% }

*Стационарное состояние системы*

Xст =  19.72972972972973
Yст =  13.333333333333334

# Выводы

Выучила как построить граф изменения численности популяции жертв x и хищников и е

 и график зависимости изменения численности хищников от изменения численности жертв
