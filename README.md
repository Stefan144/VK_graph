# Итоговый отчет

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
1. В ходе работы был получен сам граф vk группы habrahabr в виде списка ребер. Формат хранения - txt. Файл friends_inside_1.txt лежит в репозитории по [ссылке](https://github.com/Stefan144/VK_graph/blob/master/friends_inside_1.txt)
2. Также перед этим был получен файл group_members.pkl, хранящий информацию о пользователях - id, пол, дата рождения, город, страна (у некоторых пользователей могут отсутствовать некоторые поля кроме id поскольку они удалены или заблокированны). Файл был получен с помощью функции dump библиотеки pickle переменной list хранящей словари по каждому пользователю с описанными выше полями. В итоге было экспортировано 10000 пользователей.

* Экспорт
1. group_members.pkl
 ```python
 
 # Function which takes community id in and returns list of it's members. Every member got id, sex, city and etc.

def extract_members(group_id):

    list_of_members = []
    
    for offset_number in range(0, 10000, 1000):
        
        url = group_api_url + str(group_id) + offset + str(offset_number) + count + fields
        json_response = requests.get(url).json()
        users = json_response['response']['users']
        list_of_members += users
        
    return list_of_members

# Taking habrahabr community for example, id - 20629724

group_members = extract_members(20629724)

output = open('group_members.pkl', 'wb')
pickle.dump(group_members, output)
output.close()
```
2. friends_inside_1.txt
 ```python
# Function takes in user id and returns list of id's of people which are his friends and community members at the 
# same time

def user_friends_list(user_id):
    
    url = id_api_url + str(user_id)
    
    try:
        json_response = requests.get(url).json()
    except requests.exceptions.RequestException: 
        return []
    
    if 'error' in json_response.keys():
        return []
    
    friends_inside_community_list = list(set(json_response['response']).intersection(members_ids))
    return friends_inside_community_list
 
 # Создаем файл, в нем список ребер: пары вершина - вершина 

f1 = open('friends_inside_1.txt', 'w')

for member_id in members_ids:
    
    a = user_friends_list(member_id)
    
    if len(a) != 0:
        
        for friend_id in a:
            f1.write('%d' % member_id)
            f1.write(' ')
            f1.write('%d' % friend_id)
            f1.write('\n')

f1.close()
 
 ```


### Алгоритмы
* В ходе работы было применено два алгоритма выявления сообществ: k-core(k-ядра) для различных значения k, а также Лувенский метод выявления сообществ. k-ядром называется максимальный подграф содержащий вершины степени k или больше.

![](https://i.imgur.com/BJtYxQj.jpg?1)
![](https://i.imgur.com/7wUZ5wB.jpg?1)

[Источник изображений](http://www.dislab.org/GraphHPC-2016/slides/GraphHPC-2016_9_Klimov_Graphical-parallel-programming-on-the-example-of-detecting-communities-in-graphs_ru.pdf)
* Поскольку для хранения графа мною была выбрана структура графа из библиотеки networkx, то логично было бы воспользоваться хорошоми алгоритмами адапатированными под эту структуру из той же библиотеки. В моем случае я выбрал k-cores и Louvain Method, реализуются они в таком случае очень просто:

```python
# k-cores
nx.k_core(G, k)

# Louvain Method
import community
community.best_partition(G)
 ```
### Результаты работы
* Выделененные сообщества, Оценка вычислительной сложности - в коде

### Заключение
В ходе работы мною была получена небольшая практика работы с python, networkx, vk api а также изучены и применены два метода выделения сообществ Louvain Method и k-cores.

### Приложение
* Полная реализация всего выше описанного, а также данные лежат по ссылке:
https://github.com/Stefan144/VK_graph/

