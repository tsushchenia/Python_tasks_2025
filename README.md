 1. Метаклассы — контроль над созданием классов
✅ Распространённые задачи:
Автоматическая регистрация классов
Пример: плагин-система, где каждый новый класс регистрируется сам:

python
Копировать
Редактировать
class RegistryMeta(type):
    registry = {}
    def __new__(cls, name, bases, attrs):
        new_cls = super().__new__(cls, name, bases, attrs)
        cls.registry[name] = new_cls
        return new_cls
Принудительное наличие атрибутов/методов

python
Копировать
Редактировать
class InterfaceMeta(type):
    def __new__(cls, name, bases, attrs):
        if 'execute' not in attrs:
            raise TypeError("Класс должен реализовать метод 'execute'")
        return super().__new__(cls, name, bases, attrs)
Валидация структуры классов на этапе создания
Например, проверка типов аннотаций, проверки атрибутов.

🔧 2. Декораторы — обёртки для функций и методов
✅ Частые применения:
Логирование вызова функций

python
Копировать
Редактировать
def log(func):
    def wrapper(*args, **kwargs):
        print(f'Calling {func.__name__}')
        return func(*args, **kwargs)
    return wrapper
Измерение времени выполнения

python
Копировать
Редактировать
def timing(func):
    import time
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f'Time: {time.time() - start}')
        return result
    return wrapper
Кеширование (мемоизация)
(до появления functools.lru_cache)

python
Копировать
Редактировать
cache = {}
def memo(func):
    def wrapper(x):
        if x not in cache:
            cache[x] = func(x)
        return cache[x]
    return wrapper
Проверка прав доступа / авторизация

python
Копировать
Редактировать
def require_admin(func):
    def wrapper(user, *args, **kwargs):
        if not user.is_admin:
            raise PermissionError("Not admin!")
        return func(user, *args, **kwargs)
    return wrapper
📦 3. Дескрипторы — контроль доступа к атрибутам
✅ Распространённые задачи:
Автоматическое преобразование значений
(например, хранение денег в копейках, отображение в рублях)

python
Копировать
Редактировать
class Money:
    def __get__(self, instance, owner):
        return instance._cents / 100
    def __set__(self, instance, value):
        instance._cents = int(value * 100)
Ленивая загрузка (lazy loading)
Загрузка данных из БД/файла при первом доступе.

Валидация данных при установке

python
Копировать
Редактировать
class Positive:
    def __set__(self, instance, value):
        if value < 0:
            raise ValueError("Must be positive")
        instance._value = value
    def __get__(self, instance, owner):
        return instance._value
