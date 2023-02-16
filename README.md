# 24 дополнительная задача: *args **kwargs.ipynb

![Alt-текст](https://avatars.mds.yandex.net/get-images-cbir/9363731/L6UTltERsS5uUZ1bkPggRw6245/ocr "Астерикс и Обеликс: Миссия Клеопатра") 

![Markdown](https://img.shields.io/badge/markdown-%23000000.svg?style=for-the-badge&logo=markdown&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Confluence](https://img.shields.io/badge/confluence-%23172BF4.svg?style=for-the-badge&logo=confluence&logoColor=white)
![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)



Пример кода на `Python`:
```Python
# создадим функцию
def add3(*args): 
  print(sum(args))
add3()
# даже если мы не введем числа, мы все равно получим результат, без ошибки
```

**Внимание:** Рассмотрим ситуацию, если мы хотим передать в функцию список, тогда нам необходимо пометить список тоже звездочкой.
Если мы не пометим звездочкой, то список будет упакован в кортеж и возникнет ошибка.

```Python
def add4(*args): 
  print(sum(args))

l = [1,2,3,4,5,6,7,8,9]

add3(*l)
```

**Заметка:** В такую конструкцию нельзя передавать генератор

Пример блока для `Python`:
```Python
def gen():
  for i in range (10+1):
    yield i

def add(*args):
  print(args)
  print(sum(args))

l = [1,2,3,4]
add(*gen())
```

Вся суть генератора в том, чтобы выдавать информацию по частям, экономя ресурсы машины.
В случае, когда мы помечаем генератор звездочкой - астериксом и передаем в функцию для обработки - генератор отрабатывает целиком всю свою последовательность.

**Заметка:** **kwargs - две звездочки означают упаковку в словарь. kwargs - это сокращение от kw - keywords, args - arguments.
```Python
def add(*args, **kwargs):
  print(kwargs)
l = [1, 2, 3]
add(*l, a="1", b="2", c="99")
```

Пример блока для `Python`:
```Python
from timeit import Timer

tmp = "Python 3.2.2 (default, Jun 12 2011, 15:08:59) [MSC v.1500 32 bit (Intel)] on win32."

def case1(): # А. инкрементальные конкатенации в цикле
    s = ""
    for i in range(10000):
        s += tmp

def case2(): # Б. через промежуточный список и метод join
    s = []
    for i in range(10000):
        s.append(tmp)
    s = "".join(s)

def case3(): # В. списковое выражение и метод join
    return "".join([tmp for i in range(10000)])

def case4(): # Г. генераторное выражение и метод join
    return "".join(tmp for i in range(10000))

for v in range(1,5):
    print (Timer("func()","from __main__ import case%s as func" % v).timeit(200))
```
