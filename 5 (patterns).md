# TODO
Какой паттерн по смыслу ближе всего к принципу действия «триггеров» в базе данных? Прокомментируйте свой ответ.

# Решение
Ответ: observer

Из wiki:
> The observer pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods

Соответственно, можно провести аналогию:

observer pattern | database
--- | ---
subject | row, multiple rows
subject's state change | create, update, delete
observer | trigger
