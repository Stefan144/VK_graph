# (отчет - в процессе)

###### Выполнил: Николич Стефан (БПМИ144)
 
 
### Содержание
 
1. Введение
2. Краткое описание предметной области
3. Постановка задачи, описание ограничений
5. Данные
    * Описание
    * Экспорт
6. Алгоритмы
    * Описание
    * Реализация
    * Сложность
7. Результаты работы
    * Выделененные сообщества
    * Оценка вычислительной сложности
8. Заключение 
9. Приложение

### Введение

* В рамках курса Прикладная теория графов мною был выбран проект "Выявление сообществ в социальной сети vk.com ". В ходе проекта мною будет решаться задачи выявления сообществ в социальном графе Вконтакте, что в свою очередь разбивается на множество подзадач: выбор группы в Вконтакте для импорта участников, способа для импорта, формата хранения графа, алгоритмов выявления сообществ и реализация всего выше перечисленного. В конце стоит задача вывода и описания результатов работы алгоритмов.


### Краткое описание предметной области
* Большое количество интересных для исследования социальных систем можно представить в виде
графа - в нашем случае граф пользователей Вконтакте и наличие связи - отношение дружбы. Бурное развитие роста данных и доступа к ним в социальных сетях позволило даже простым обывателям иметь возможность эксперементировать с различными методами анализа графов и подобных им структур. В теории графов сообществом (связанная подгруппа) принято считать группу вершин социальной сети, которые связаны существенно большим количеством рёбер, чем между сообществами. В настоящее время в области выявления сообществ предложено множество алгоритмов и часто появляются исследования. 

### Постановка задачи, описание ограничений
* В данной работе ставится исследовать алгоритмы (теоретически, реализовать, посмотреть на результаты работы, посчитать время работы в зависимости от размера графа) выявления сообществ - k-core и Лувеанский метод. Для этого нужно импортировать данные из социальной сети (Вконтаке) с помощью vk api, выбрать структуру для хранения графа и способы реализации алгоритмов.

* Главным ограничением работы является импортирование участников групп в vk - api позволяет импортировать 1000 участников, но это можно преодолеть смещая параметр offset при импорте. 



### Данные
* Описание

* Экспорт
 ```python
code here
```
### Алгоритмы
* В ходе работы было применено два алгоритма выявления сообществ: k-core(k-ядра) для различных значения k, а также Лувенский метод выявления сообществ. k-ядром называется максимальный подграф содержащий вершины степени k или больше.

![](https://i.imgur.com/BJtYxQj.jpg?1)
![](https://i.imgur.com/7wUZ5wB.jpg?1)

[Источник изображений](http://www.dislab.org/GraphHPC-2016/slides/GraphHPC-2016_9_Klimov_Graphical-parallel-programming-on-the-example-of-detecting-communities-in-graphs_ru.pdf)
* Реализация
* Сложность
### Результаты работы
* Выделененные сообщества
* Оценка вычислительной сложности

### Заключение

### Приложение
* Полная реализация всего выше описанного, а также данные лежат по ссылке:
https://github.com/Stefan144/VK_graph/

