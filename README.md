# Тема 7. Работа с файлами (ввод, вывод)
Отчет по Теме #7 выполнил:
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
import re

file = open('input1.txt', 'r', encoding='utf-8-sig')
stopwords = file.read().split()
string = '''What is this life if, full of care, we have no time to stand and stare. A poor life this if, full of care, 
we have no time to stand and stare.'''


def censor(string, stopwords):
    for stopword in stopwords:
        string = re.sub(stopword, lambda x: '*' * len(x.group()), string, flags=re.IGNORECASE)
    return string


res = censor(string, stopwords)
print(res)

file.close()
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.4().png)

## Самостоятельная работа 5
### Напишите программу, которая считывает содержимое текстового файла и удаляет все строки, которые начинаются с #, а затем, записывает оставшиеся строки обратно в файл.

```python
remove_char = '#'

with open('input2.txt', 'r') as file:
    lines = file.readlines()

file.close()

with open('input2.txt', 'w') as file:

    for line in lines:
        if line[0] != remove_char:
            file.write(line)

file.close()
```

### Результат:
Исходный текст:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.5%20(0).png)
Что получилось послеу даления:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.5(1).png)
Сравнение с исходным текстом:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.5(2).png)
Выполненный код:
![Меню](https://github.com/Dirtzzz/Tema_7/blob/main/7.5(3).png)
