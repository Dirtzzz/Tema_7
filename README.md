# Тема 2. Базовые операции языка Python
Отчет по Теме #2 выполнил:
- Ильдейкин Антон Александрович
- ИНО ЗБ ПОАС-22-2

| Задание | Лаб_раб | Сам_раб |
| ------ | ------ | ------ |
| Задание 1 | - | + |
| Задание 2 | - | + |
| Задание 3 | - | + |
| Задание 4 | - | + |
| Задание 5 | - | + |
| Задание 6 | - | - |
| Задание 7 | - | - |
| Задание 8 | - | - |
| Задание 9 | - | - |
| Задание 10 | - | - |


Работу проверили:
- к.э.н., доцент Панов М.А.
## Самостоятельная работа №1
### Найдите в интернете любую статью (объем статьи не менее 200 слов), скопируйте ее содержимое в файл и напишите программу, которая считает количество слов в текстовом файле и определит самое часто встречающееся слово. Результатом выполнения задачи будет: скриншот файла со статьей, листинг кода, и вывод в консоль, в котором будет указана вся необходимая информация.

```python
import re

file = open('text.txt', 'r', encoding='utf-8-sig')
words = file.read().split()
stopwords = ['в', 'на', 'и', 'с', 'к', 'а','но', 'за', 'до', 'по', 'о']
print(f'Длина статьи: {len(words)} слов.')


def clean_text(words, stopwords):
    words = [re.sub(r'[,()."—:«»]', '', i) for i in words if i not in stopwords and len(i) > 1]
    return words


def find_most_wstr(words):
    words = clean_text(words, stopwords)
    num_freq = {}

    for word in words:
        num_freq[word] = num_freq.get(word, 0) + 1
    sorted_num_freq = sorted(num_freq.items(), key=lambda item: item[1])
    top = sorted_num_freq[-1]
    return top

res = find_most_wstr(words)
print(f'Самое встречающееся слово: "{res[0]}". Встречается {res[1]} раз.')

file.close()
```
### Результат:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.1.png)
Текст в файле:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.1(1).png)

## Самостоятельная работа №2
### У вас появилась потребность в ведении книги расходов, посмотрев все существующие варианты вы пришли к выводу что вас ничего не устраивает и нужно все делать самому. Напишите программу для учета расходов. Программа должна позволять вводить информацию о расходах, сохранять ее в файл и выводить существующие данные в консоль. Ввод информации происходит через консоль. Результатом выполнения задачи будет: скриншот файла с учетом расходов, листинг кода, и вывод в консоль, с демонстрацией работоспособности программы.

```python
import csv

def record_expenses(expenses):
    date = input('Введите дату: ')
    category = input('Введите категорию: ')
    amount = float(input('Введите сумму: '))
    expenses.append({'date': date, 'category': category, 'amount': amount})
    with open('expenses.csv', 'a', newline='') as file:
        fieldnames = ['date', 'category', 'amount']
        writer = csv.DictWriter(file, fieldnames=fieldnames)
        if file.tell() == 0:
            writer.writeheader()
        writer.writerow(expenses[-1])

def view_expenses(expenses):
    with open('expenses.csv', 'r', newline='') as file:
        reader = csv.DictReader(file)
        for row in reader:
            print(f"{row['date']}, {row['category']}, {row['amount']}")

expenses = []

while True:
    print('1. Добавить запись')
    print('2. Просмотреть записи')
    choice = int(input('Введите номер действия: '))

    if choice == 1:
        record_expenses(expenses)
    elif choice == 2:
        view_expenses(expenses)
        break
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.2.png)
Полный вывод в консоли:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.2(2).png)
Файл CSV в Python
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.1(2).png)

## Самостоятельная работа 3
### Имеется файл input.txt с текстом на латинице. Напишите программу, которая выводит следующую статистику по тексту: количество букв латинского алфавита; число слов; число строк.

```python
import re
file = open('input.txt', 'r', encoding='utf-8-sig')

words = 0
stroki = 0
simvol = 0
for string in file:
    words += len(string.split())
    stroki += 1
    for letter in string:
        simvol += 1 if re.match(r'[a-zA-Z]+', letter) else 0

print('Статистика файла:', f'{simvol} букв;', f'{stroki} строки;', f'{words} слов.', sep='\n')
file.close()
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.3(z).png)

## Самостоятельная работа 4
### Напишите программу, которая получает на вход предложение, выводит его в терминал, заменяя все запрещенные слова звездочками * (количество звездочек равно количеству букв в слове). Запрещенные слова, разделенные символом пробела, хранятся в текстовом файле input.txt. Все слова в этом файле записаны в нижнем регистре. Программа должна заменить запрещенные слова, где бы они ни встречались, даже в середине другого слова. Замена производится независимо от регистра: если файл input.txt содержит запрещенное слово exam, то слова exam, Exam, ExaM, EXAM и exAm должны быть заменены на ****.

```python
x="А"
print (x*20)
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_2/blob/main/2.4.png)

## Самостоятельная работа 5
### Создайте три переменные: день (тип данных - числовой), месяц (тип данных - строка), год (тип данных - числовой) и выведите в консоль текущую дату в формате: "Сегодня день месяц год. Всего хорошего!" используя F строку и оператор end внутри print(), в котором вы должны написать фразу "Всего хорошего!". Программа должна занимать не более двух строк редактора кода.
Поправочка: в 2 строки кода не получается создать, как бы я не пытался :(

```python
from datetime import datetime
today = datetime.now()
print(f"Сегодня {today.day} {today.strftime('%B')} {today.year}. ", end="Всего хорошего!\n")
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_2/blob/main/2.5.png)

## Самостоятельная работа 6
### В предложении 'Hello World' вставьте 'my' между двумя словами. Выведите полученное предложение в консоль в одну строку. Программа должна занимать не более двух строк редактора кода.


```python
print("Hello my world")
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_2/blob/main/2.6.png)

## Самостоятельная работа 7
### Узнайте длину предложения 'Hello World', результат выведите в консоль. Программа должна занимать не более двух строк редактора кода.


```python
print(len("Hello world"))
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_2/blob/main/2.7.png)

## Самостоятельная работа 8
### Переведите предложение 'HELLO WORLD' в нижний регистр. Программа должна занимать не более двух строк редактора кода


```python
print("HELLO WORLD".lower())
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_2/blob/main/2.8.png)

## Самостоятельная работа 9
### Придумать свою задачу, связанную с взаимодействием числовых значений. 
Задача: дан прямоугольник ABCD. Точка G делит сторону BC на отрезки 5 и 3, а расстояние от точки O до стороны AD равно 2. Найти периметр прямоугольника.


```python
P = 2*(5+3+2)
print(P)
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_2/blob/main/2.9.png)

## Самостоятельная работа 10
### Придумать свою задачу, связанную с взаимодействием строковых значений. 
Задача: Создайте 4 переменные на каждое слово в предложении и объедините полученный результат в одно целое.
Предложение: i am feeling good!

```python
x1 = "I"
x2 = "am"
x3 = "feeling"
x4 = "good"
x5 = x1 + " " + x2 + " " + x3 + " " + x4 + "!"
print(x5)
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_2/blob/main/2.10.png)
