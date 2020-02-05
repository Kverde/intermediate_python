% Intermediate Python
% Obi Ike-Nwosu
% leanpub.com, 2016

# Intermediate Python

Перевод книги [Intermediate Python](https://leanpub.com/intermediatepython) Obi Ike-Nwosu. Перевод выполнен с сокращениями, часть текста и примеры изменены.

## 1. Благодарности

Благодарю всех кто помогал при написании и корректировке книги. 

## 2. Введение

Эта книга рассчитана на средний уровень знакомства с Python. В качестве интерпретатора подразумевается [CPython](https://www.python.org/). [Документация](https://docs.python.org/3/reference/index.html) последней стабильной версии.

## 3. Очень короткий учебник

Этот короткий учебник раскрывает основные концепции и возможности языка программирования Python.

### 3.1 Использование Python

Python установлен по умолчанию на Unix-системах. Для проверки установлен ли Python, откройте командную строку и введите `python`. Если Python не установлен то откройте [сайт Python](https://www.python.org/) и следуйте инструкциям для вашей платформы.

Если после установки Python не запускается из командной строки, проверьте добавлен ли путь к интерпретатору в системные пути.

Запуск интерпретатора командой `python` начинает интерактивную сессию [REPL](https://ru.wikipedia.org/wiki/REPL). Основная подсказка `>>>` предлагает ввести команду, вторичная подсказка `...` сигнализирует о продолжении предыдущей инструкции:

```python
>>> def hello():
...     print("Hello world")
...
>>>
```

Пользователь вводит инструкции python и немедленно получает ответ. В режиме REPL Python может использоваться как продвинутый калькулятор:

```python
Python 3.8.0 (tags/v3.8.0:fa919fd, Oct 14 2019, 19:21:23) [MSC v.1916 32 bit (In
tel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> a = 3
>>> b = 3
>>> a * b + 5
14
>>>
```

Введите Ctrl+Z для завершения сессии интерпритатора.

### 3.2 Операторы Python, строки и отступы

Программа на Python состоит из логических строк ограниченных токеном **NEWLINE**. Каждая логическая строка эквивалентна простому оператору. Составные операторы формируются из нескольких логических строк.

Логическая строка создаётся из одной или нескольких физических строк используя явные или не явные правила объединения строк. Физическая строка — это последовательность символов завершающаяся символами перевода строки (end-of-line sequence). Python неявно рассматривает физические строки как логические, устраняя необходимость в точке с запятой для разделения выражений. Однако точка с запятой может использоваться для разделения одной физической строки на несколько логических:

```Python
>>> i = 5; print i;
5
```

Несколько физических строк в явном виде объединяются в одну логическую символом "\\":

```Python
>>> name = "Obi Ike-Nwosu"
>>> cleaned_name = name.replace("-", " "). \
... replace(" ", "")
>>> cleaned_name
'ObiIkeNwosu'
>>>
```

Физические строки соединяются неявно, без использования символа продолжения строки ("\\"), когда выражение находится в тройных строковых кавычках, заключено в скобки `(...)`, `[...]`, или `{...}`.

Python содержит два типа операторов.

Простые операторы занимающие одиночные логические строки. Они включают в себя присваивание, **yield** и др. Общий синтаксис простых операторов:

```
simple_stmt ::= expression_stmt
            | assert_stmt
            | assignment_stmt
            | augmented_assignment_stmt
            | pass_stmt
            | del_stmt
            | return_stmt
            | yield_stmt
            | raise_stmt
            | break_stmt
            | continue_stmt
            | import_stmt
            | global_stmt
            | nonlocal_stmt
```

Составные операторы занимающие несколько логических строк. Они включают в себя выражения циклов **while** и **for**. Общий синтаксис составных операторов:

```
compound_stmt ::= if_stmt
              | while_stmt
              | for_stmt
              | try_stmt
              | with_stmt
              | funcdef
              | classdef

suite ::= stmt_list NEWLINE | NEWLINE INDENT statement+ DEDENT

statement ::= stmt_list NEWLINE | compound_stmt

stmt_list ::= simple_stmt (";" simple_stmt)* [";"]
```

Составные операторы содержат одно или несколько предложений (clause). Предложение состоит из заголовка (header) и тела (suite). Заголовки предложений для одного составного оператора имеют одинаковый отступ и начинаются с уникального идентификатора (**while**, **if** и т.д.) и с двоеточия. Составной оператор **if** определяется так:

```
if_stmt ::=  "if" expression ":" suite
             ( "elif" expression ":" suite )*
             ["else" ":" suite]
```

Выполнение тела предложения контролируется заголовком:

```Python
>>> num = 6
# оператор if является составным оператором
    # Заголовок предложения контролирует выполнение следующего блока с отступом
>>> if num % 2 == 0:
        # блок тела с отступом
...     print("The number {} is even".format(num))
...
The number 6 is even
>>>
```

Тело (suite) может быть набором из одного или нескольких операторов который следуют за двоеточием заголовка, в этом случае, операторы разделяются точкой с запятой:

```Python
>>> x = 1
>>> y = 2
>>> z = 3
>>> if x < y < z: print(x); print(y); print(z)
...
1
2
3
```

Но обычно тело (suite) записывается со следующей после заголовка строки в виде одного или нескольких операторов с отступом:

```Python
>>> x = 1
>>> y = 2
>>> z = 3
>>> if x < y < z:
...    print(x)
...    print(y);
...    print(z)
...
1
2
3
```

Отступы используются для обозначения блоков кода таких как тела функций, условий, циклов и классов. Ведущий пробел в начале логической строки используется для вычисления отступа для этой строки, который, в свою очередь, используется для определения группировки оператора. Отступ используемый в теле блока всегда должен совпадать с отступом первого оператора в блоке.

### 3. Строки

Строки в Python обрамляются двойными "..." или одинарными '...' кавычками. Спецсимволы указываются внутри строки с экранированием:

```python
# кавычка используется как апостроф, поэтому мы экранируем её чтобы 
# предотвратить завершение строки
>>> name = 'men\'s'
>>> name
"men's"
>>>
```

Для того чтобы отключить обработку спецсимволов в строке, добавьте перед строкой символ **r**:

```python
>>> print('C:\some\name') # здесь \n означает перевод строки!
C:\some
ame
>>> print(r'C:\some\name') # добавлен r перед кавычкой
C:\some\name
```

Многострочные строковые литералы задаются тройными кавычками. Перевод строки автоматически добавляется при достижении конца строки:

```python
>>> para = """hello world I am putting together a
... book for beginners to get to the next level in python"""
# Обратите внимание на символ перевод строки
>>> para
'hello world I am putting together a \nbook for beginners to get to the next level in python'
# При выводе текст разделяется на несколько срок
>>> print(para)
hello world I am putting together a
book for beginners to get to the next level in python
>>>

Чтобы перевод строки не добавлялся используйте символ **\** в конце строки:

​```python
>>> para = """hello world I am putting together a \
... book for beginners to get to the next level in python"""
>>> para
'hello world I am putting together a book for beginners to get to the next level in python'
>>> print(para)
hello world I am putting together a book for beginners to get to the next level in python
>>>
```

Строки неизменяемые, один раз созданная строка не может быть изменена. Для символов отдельного типа нет, они являются строками длинной в 1 символ. Строки являются одним из типов последовательностей, поэтому поддерживают все операции с последовательностями, за исключением присваивания по индексу из-за неизменяемости. Обращение к отдельному символу происходит по индексу:

```python
>>> name = 'obiesie'
>>> name[1]
'b'
>>>
```

Строки соединяются оператором **+**:

```python
>>> name = 'obiesie'
>>> surname = " Ike-Nwosu"
>>> full_name = name + surname
>>> full_name
'obiesie Ike-Nwosu'
>>>
```

Написанные рядом строковые литералы соединяются автоматически:

```python
>>> 'Py' 'thon'
'Python'
>>>
```

Встроенная функция **len** возвращает длину строки:

```python
>>> name = "obi"
>>> len(name)
3
>>>
```

### 3.4 Управляющие конструкции

#### if-else и if-elif-else

Оператор **if** применяется для условного выполнения блока кода:

```python
>>> name = "obi"
>>> if name == "obi":
...     print("Hello Obi")
...
Hello Obi
>>>
```

За оператором **if** следует ноль или больше операторов **elif** и не обязательный оператор **else**. Если не один из операторов **if** или **elif** не был выполнен, то выполняется блок **else**:

```python
>>> if name == "obi":
...     print("Hello Obi")
... elif name == "chuks":
...     print("Hello chuks")
... else:
...     print("Hello Stranger")
Hello Stranger
>>>
```

#### for и range

В Python два вида циклов: **while** и **for**.

Оператор **for** используется для перебора последовательностей (list, set, tuple и т.д.). В общем случае, цикл **for** используется для перебора любых объектов реализующих протокол итератора Python (python iterator protocol). Подробнее это будет описано в следующих главах.

Пример использования цикла **for**:

```python
>>> names = ["Joe", "Obi", "Chris", "Nkem"]
>>> for name in names:
...     print(name)
...
Joe
Obi
Chris
Nkem
>>>
```

Большинство языков программирования использует синтаксис похожий на этот для перебора последовательности чисел:

```
for(int x = 10; x < 20; x = x+1) {
// do something here
}
```

В Python используется конструкция **range()** для генерации арифметической прогрессии целых чисел:

```python
>>> for i in range(10, 20):
...     print i
...
10
11
12
13
14
15
16
17
18
19
```

Функция range(start, stop, step) допускает три аргумента. Значение параметра **stop** не входит в возвращаемую последовательность.

#### while

Оператор **while** выполняет блок кода пока условное выражение вычисляется в **True**:

```python
>>> counter = 10
>>> while counter > 0: # условное выражение 'counter > 0'
...     print(counter)
...     counter = counter - 1
...
10
9
8
7
6
5
4
3
2
1
```

#### break и continue

Команда **break** завершает выполнение цикла, после **break** происходит немедленный выход из цикла.

```python
>>> for i in range(10):
...     if i == 5:
...         break
...     else:
...         print(i)
...
0
1
2
3
4
```

Команда **continue** принудительно запускает следующую итерацию цикла. Все команды внутри цикла после **continue** игнорируются.

```python
>>> for i in range(10):
        # если i равно 5 то начинаем новую итерацию цикла, без выполнения остальных команд
...     if i == 5:
...         continue
...     print("The value is " + str(i))
...
The value is 0
The value is 1
The value is 2
The value is 3
The value is 4
# no printed value for i == 5
The value is 6
The value is 7
The value is 8
The value is 9
```

В примере выше, значение 5 не напечатано, из-за условия и команды **continue**. Все остальные значения напечатаны.

#### циклы и else 

В Python ключевое слово **else** применяется вместе с операторами цикла. Блок после **else** выполняется если цикл не был завершён оператором **break**.

```python
# loop exits normally
>>> for i in range(10):
...     print(i)
... else:
...     print("I am in quirky else loop")
...
0
1
2
3
4
5
6
7
8
9
I am in quirky else loop
```

Если цикл завершён оператором **break**, то блок **else** пропускается:

```python
>>> for i in range(10):
...     if i == 5:
...        break
...     print(i)
... else:
...     print("I am in quirky else loop")
...
0
1
2
3
4
```

#### Enumerate

Иногда нужно перебрать коллекцию, поучая одновременно индекс и значение элементов. Можно использовать такой подход:

```python
>>> names = ["Joe", "Obi", "Chris", "Jamie"]
>>> name_count = len(names)
>>> index = 0
>>> while index < name_count:
...   print("{}. {}".format(index, names[index]))
...   index = index + 1
...
0. Joe
1. Obi
2. Chris
3. Jamie
```

В Python есть более эффективное решение с функцией **enumerate**:

```python
>>> for index, name in enumerate(names):
...     print("{}. {}".format(index, name))
...
0. Joe
1. Obi
2. Chris
3. Jamie
>>>
```
### 3.5 Функции

Именованные функции определяются ключевым словом **def**, за которым следует название функции и список параметров в скобках. Ключевое слово **return** используется для возвращения значения функции:

```python
def full_name(first_name, last_name):
    return " ".join((first_name, last_name))
```

Для вызова функции используется её имя, параметры передаются в скобках:

```python
full_name("Obi", "Ike-Nwosu")
```

Функции могут вернуть несколько значений в виде кортежа. В следующим примере функция возвращает частное и остаток от деления:

```python
>>> def divide(a, b):
...     return divmod(q, r)
...
>>> divide(7, 2)
(3, 1)
>>>
```

Функция без **return** всегда возвращает **None**:

```python
>>> def print_name(first_name, last_name):
...     print(" ".join((first_name, last_name)))
...
>>> print_name("Obi", "Ike-Nwosu")
Obi Ike-Nwosu
>>> x = print_name("Obi", "Ike-Nwosu")
Obi Ike-Nwosu
>>> x
>>> type(x)
<type 'NoneType'>
>>>
```

Ключевое слово **return** может использоваться без значения чтобы прервать выполнение функции:

```python
>>> def dont_return_value():
...     print("How to use return keyword without a value")
...     return
...
>>> dont_return_value()
```

Выражение **lambda** позволяет объявить функцию без имени. Такая функция состоит всего из одного выражения которое и является значением функции. Поэтому не требуется использовать **return**.


```python
>>> square_of_number = lambda x: x**2
>>> square_of_number
<function <lambda> at 0x101a07158>
>>> square_of_number(2)
4
>>>
```

Функция созданная через **lambda** эквивалентна именованной функции определённой через **def**.


