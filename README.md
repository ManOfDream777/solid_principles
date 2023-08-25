# SOLID

## 1. SRP - Single Responsibility Principle
```python

class User:
    def __init__(self, username, email):
        self.username = username
        self.email = email

    def save(self):
        # Логика сохранения пользователя в базе данных
        pass


class EmailSender:
    def send_email(self, user, message):
        # Логика отправки электронной почты пользователю
        pass


class ReportGenerator:
    def generate_report(self, user):
        # Логика генерации отчета пользователя
        pass
```

### Принцип заключается в том, что каждый класс должен иметь ТОЛЬКО функционал, под который этот класс был придуман

## 2. OCP - Open/Closed Principle
```python

from abc import ABC, abstractmethod
from math import pi


class Shape(ABC):
    @abstractmethod
    def calculate_area(self):
        pass


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def calculate_area(self):
        return self.width * self.height


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def calculate_area(self):
        return pi * self.radius ** 2


class AreaCalculator:
    def calculate_total_area(self, shapes):
        total_area = 0
        for shape in shapes:
            total_area += shape.calculate_area()
        return total_area
```

### Принцип заключается в том, что класс должен быть открыт для расширения, но закрыт для изменения. То есть, выпуская код в production, класс не должен быть изменен (чтобы не нарушать уже готовую функциональность), но может быть расширен функционалом использую наследование

## 3. LSP - Liskov Substitution Principle

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def set_width(self, width):
        self.width = width

    def set_height(self, height):
        self.height = height

    def get_area(self):
        return self.width * self.height


class Square(Rectangle):
    def set_width(self, width):
        self.width = width
        self.height = width

    def set_height(self, height):
        self.width = height
        self.height = height
```
### Принцип заключается, что дочерний класс, не должен нарушать логику работы родительского класса

## 4. ISP - Interface Segregation Principle

```python
from abc import ABC, abstractmethod


class InputDevice(ABC):
    @abstractmethod
    def read_input(self):
        pass


class OutputDevice(ABC):
    @abstractmethod
    def write_output(self, data):
        pass


class Keyboard(InputDevice):
    def read_input(self):
        # Логика чтения ввода с клавиатуры
        pass


class Mouse(InputDevice):
    def read_input(self):
        # Логика чтения ввода с мыши
        pass


class Monitor(OutputDevice):
    def write_output(self, data):
        # Логика вывода данных на монитор
        pass


class Printer(OutputDevice):
    def write_output(self, data):
        # Логика вывода данных на принтер
        pass
```

### Принцип заключается в том, что интерфейс не должен иметь лишние атрибуты или методы, для переопределения их в дочернем классе

## 5. DIP - Dependency Inversion Principle

```python
from abc import ABC, abstractmethod


class Notification(ABC):
    @abstractmethod
    def send_notification(self, message):
        pass


class EmailSender(Notification):
    def send_notification(self, message):
        # Логика отправки уведомления по электронной почте
        pass


class SMSNotification(Notification):
    def send_notification(self, message):
        # Логика отправки уведомления по SMS
        pass


class User:
    def __init__(self, username, email):
        self.username = username
        self.email = email
        self.notification_service = EmailSender()

    def send_notification(self, message):
        self.notification_service.send_notification(message)
```

### Принцип заключается в том, что высокоуровневые модули, не должны зависеть от низкоуровневых модулей. <br> Низкоуровневый модуль - абстракция, высокоуровневый модуль - конкретная реализация. <br> То есть, использование этого принципа, позволяет расширять или изменять функционал низкоуровневых модулей, без изменения высокоуровневых модулей 
