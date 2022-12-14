# task_for_Lesta_Studio
 Вакансия Junior Python Programmer (стажер)

##### 1. Побитовое сравнение.
Число нечетно, когда его младший бит равен 1, и четно, когда младший бит равен 0.
<br/>

```python
def isEven(value):
    return value & 1 == 0
```


##### 2.FIFO – (first-in, first-out) первые элементы в очереди выходят первыми.
Для этой задачи можно использовать готовые классы в Python:
###### -класс deque() модуля collections
(Большое количество методов, что, при необходимости, может расширить наш функционал при работе с очередями (2-ой принцип SOLID - open/close - код/компонент/модуль должен быть закрыт для изменения, но доступен для расширения, это значит, что если нам понадобится изменить принцип работы с очередью, то ничего не надо будет дописывать/переписывать - мы просто будем использовать другие методы класса)).
<br/>
###### -класс queue.Queue()
(Имеет строго необходимый нам функционал, подходит под принцип KISS (большинство систем работают лучше всего, если они остаются простыми, а не усложняются), так же есть удобный функционал для работы очереди с приорететом: модуль queue.PriorityQueue()).

```python
from collections import deque
import queue

//класс deque() модуля collections возвращает новый объект deque()
dq = deque([1, 8, 9])
print(*dq) # 1 8 9
dq.append('j')
print(*dq) # 1 8 9 j
dq.extend('kls')
print(*dq) # 1 8 9 j k l s
print(dq.popleft()) #1
print(*dq) # 8 9 j k l s

//класс queue.Queue() - базовый контейнер типа FIFO:
q = queue.Queue()
for i in range(5):
    q.put(i)
while not q.empty():
    print(q.get(), end=' ') # 0 1 2 3 4
```

Просто классы, без использования библиотек, которые реализуют очередь FIFO:
```python
//Без указания длины:
class Fifo:
    def __init__(self):
        self.mas = []

    def append_element(self, element):
        self.mas.append(element)

    def get_element(self):
        if self.mas:
            out = self.mas.pop(0)
        else:
            out = None
        return out

    def return_list(self):
        return self.mas

//С указанием длины:
class Fifo_with_len:
    def __init__(self, max_len):
        self.mas = []
        self.max_len = max_len

    def append_element(self, element):
        if len(self.mas) < self.max_len:
            self.mas.append(element)
        else:
            print("Очередь переполнена!")

    def get_element(self):
        if self.mas:
            out = self.mas.pop(0)
        else:
            out = None
        return out

    def return_list(self):
        return self.mas


a = Fifo_with_len(3)
a.append_element(8)
a.append_element(4)
a.append_element(5)
a.append_element(2)
# Очередь переполнена!
print(a.get_element()) # 8
print(a.return_list()) # [4, 5]
```

##### 3. Быстрая сортировка Хоара.
Время выполнения: N*log2N. Плюс в том, что каждый раз выбирается не 1-ый элемент, а случайный - это ускоряет работу и уменьшает память,  т.к. в быстрой сортировке по первому элементу следующий массив уменьшается всего на 1 элемент.
<br/>
Для реальных заданий по сортировке в Python  используется метод sort().
<br/>

```python
import random
def rec(s):
    if len(s) <= 1:
        return s
    elem = s[random.randint(0, len(s)-1)]
    left = list(filter(lambda x: x < elem, s))
    center = [i for i in s if i == elem]
    right = list(filter(lambda x: x > elem, s))
    return rec(left) + center + rec(right)

print(rec([1,3,1,9,3])) # [1, 1, 3, 3, 9]
```


Резюме на  Хабр Карьере: https://career.habr.com/swee1 

