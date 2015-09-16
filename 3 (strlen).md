# TODO
Какова алгоритмическая сложность (в О-нотации) функции strlen($s) в PHP? Прокомментируйте свой ответ.

# Решение
Ответ: O(1)

[Habrahabr](http://habrahabr.ru/company/mailru/blog/250861/): 
> "strlen() не вычисляет длины строк в PHP, ведь все они уже известны к моменту вызова этого метода. Большинство по возможности вычисляется еще во время компиляции. Длина PHP-строки, отправляемой в память, инкапсулируется в С-структуру, содержащую эту самую строку. Поэтому strlen() просто считывает эту информацию и возвращает как есть. Вероятно, это самая быстрая из PHP-функций, потому что она вообще ничего не вычисляет."

[PHP Source code](http://lxr.php.net/xref/PHP_5_4/Zend/zend_operators.h):
```c
#define Z_STRLEN(zval) (zval).value.str.len
```

[PHP Doc](http://php.net/manual/ru/internals2.variables.intro.php):
```
int len; /* this will always be set for strings */
```