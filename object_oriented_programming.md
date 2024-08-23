# [На главную](https://github.com/xXxCLOTIxXx/python_couch)


## Основные концепции ООП

### Классы и объекты:
  Класс – это шаблон (чертеж) для создания объектов. Он описывает, какие свойства и методы будут у объектов.
  Объект – экземпляр класса. Он имеет конкретные значения свойств и может вызывать методы.

### Атрибуты:
  Атрибуты класса – переменные, определённые внутри класса, но вне методов. Общие для всех объектов класса.
  Атрибуты объекта – переменные, определённые внутри методов класса, но относящиеся к конкретному объекту.

### Методы:
  Функции, определённые внутри класса. Операции, которые могут выполняться над объектами.


# 1. Определение класса

Класс в Python создаётся с помощью ключевого слова class.

```python

class MyClass:
    # Тело класса
    pass  # Заглушка, если класс пока не содержит никаких элементов
```
# 2. Конструктор класса (__init__)

Конструктор – это специальный метод, который вызывается при создании нового объекта. В Python конструктор называется __init__.

```python

class MyClass:
    def __init__(self, param1, param2):
        self.param1 = param1  # Присваивание значения атрибуту объекта
        self.param2 = param2
```
#### Пример использования:

```python

class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

my_dog = Dog("Барбос", "Овчарка")
print(my_dog.name)  # Вывод: Барбос
print(my_dog.breed)  # Вывод: Овчарка
```
# 3. Атрибуты класса и объекта

  Атрибуты объекта – принадлежат каждому конкретному объекту и инициализируются в конструкторе.
  Атрибуты класса – общие для всех объектов и инициализируются на уровне класса.

```python

class MyClass:
    class_attribute = "Это атрибут класса"

    def __init__(self, instance_attribute):
        self.instance_attribute = instance_attribute  # Атрибут объекта

obj1 = MyClass("Значение 1")
obj2 = MyClass("Значение 2")

print(obj1.instance_attribute)  # Вывод: Значение 1
print(obj2.instance_attribute)  # Вывод: Значение 2
print(MyClass.class_attribute)  # Вывод: Это атрибут класса
```
# 4. Методы класса

Методы – это функции, которые определяются внутри класса и работают с объектами этого класса.

```python

class MyClass:
    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Привет, {self.name}!"

obj = MyClass("Алиса")
print(obj.greet())  # Вывод: Привет, Алиса!
```
# 5. Методы класса и статические методы

  Методы класса (@classmethod) принимают параметр cls, который ссылается на сам класс, и могут работать с атрибутами класса.
  Статические методы (@staticmethod) не принимают ни self, ни cls, и используются для создания методов, которые не зависят от состояния экземпляра или класса.

``` python

class MyClass:
    class_variable = "Переменная класса"

    @classmethod
    def class_method(cls):
        return f"Это {cls.class_variable}!"

    @staticmethod
    def static_method():
        return "Это статический метод!"

print(MyClass.class_method())  # Вывод: Это Переменная класса!
print(MyClass.static_method())  # Вывод: Это статический метод!
```
# 6. Наследование

Класс может наследовать свойства и методы другого класса. Для этого в скобках после имени класса указывают имя родительского класса.

```python

class ParentClass:
    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Привет, {self.name}!"

class ChildClass(ParentClass):
    def greet_loudly(self):
        return f"ПРИВЕТ, {self.name.upper()}!"

child = ChildClass("Иван")
print(child.greet())  # Вывод: Привет, Иван!
print(child.greet_loudly())  # Вывод: ПРИВЕТ, ИВАН!
```
# 7. Множественное наследование

Класс может наследовать от нескольких классов, указанных через запятую.

```python

class A:
    def method_a(self):
        return "Метод A"

class B:
    def method_b(self):
        return "Метод B"

class C(A, B):
    pass

obj = C()
print(obj.method_a())  # Вывод: Метод A
print(obj.method_b())  # Вывод: Метод B
```
# 8. Инкапсуляция

Инкапсуляция заключается в ограничении доступа к внутренним данным и методам класса. В Python это реализуется через:

  Префикс _ перед именем атрибута или метода указывает, что это внутренний элемент (соглашение).
  Префикс __ делает атрибут или метод частным, доступ к нему возможен только внутри класса.

```python

class MyClass:
    def __init__(self, name):
        self._name = name  # Защищенный атрибут
        self.__secret = "Секрет"  # Частный атрибут

    def get_secret(self):
        return self.__secret

obj = MyClass("Тест")
print(obj._name)  # Вывод: Тест
print(obj.get_secret())  # Вывод: Секрет
# print(obj.__secret)  # Ошибка: AttributeError
```
# 9. Полиморфизм

Полиморфизм – это способность объектов разных классов использовать один и тот же интерфейс (методы с одинаковыми именами).

```python

class Animal:
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "Гав"

class Cat(Animal):
    def sound(self):
        return "Мяу"

animals = [Dog(), Cat()]
for animal in animals:
    print(animal.sound())  # Вывод: Гав, Мяу
```
# 10. Абстрактные классы

Абстрактный класс содержит абстрактные методы, которые должны быть реализованы в подклассах. В Python это реализуется с помощью модуля abc.

```python

from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "Гав"

# animal = Animal()  # Ошибка: нельзя создать экземпляр абстрактного класса
dog = Dog()
print(dog.sound())  # Вывод: Гав
```
# 11. Свойства (properties)

Свойства позволяют контролировать доступ к атрибутам класса с помощью декоратора @property.

```python

class MyClass:
    def __init__(self, value):
        self._value = value

    @property
    def value(self):
        return self._value

    @value.setter
    def value(self, new_value):
        if new_value >= 0:
            self._value = new_value
        else:
            raise ValueError("Значение должно быть неотрицательным")

obj = MyClass(10)
print(obj.value)  # Вывод: 10
obj.value = 20  # Изменение значения
print(obj.value)  # Вывод: 20
```
# 12. Методы перегрузки операторов

Перегрузка операторов позволяет изменять поведение стандартных операторов (например, сложение, вычитание) для объектов класса. Это делается с помощью специальных методов.

```python

class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2  # Используется метод __add__
print(v3)  # Вывод: Vector(4, 6)
```
# 13. Контекстные менеджеры

Контекстные менеджеры позволяют управлять ресурсами с помощью конструкции with, что особенно полезно для работы с файлами, сетевыми соединениями и другими ресурсами.

```python

class Resource:
    def __enter__(self):
        print("Ресурс открыт")
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Ресурс закрыт")

with Resource():
    print("Работа с ресурсом")
# Вывод:
# Ресурс открыт
# Работа с ресурсом
# Ресурс закрыт
```
# 14. Документация классов

Python поддерживает встроенную документацию с помощью строковых литералов (docstrings), которые размещаются непосредственно в теле класса или метода.

```python

class MyClass:
    """
    Это пример класса с документацией.
    """

    def my_method(self):
        """
        Это пример метода с документацией.
        """
        pass

print(MyClass.__doc__)  # Вывод: Это пример класса с документацией.
print(MyClass.my_method.__doc__)  # Вывод: Это пример метода с документацией.
```
