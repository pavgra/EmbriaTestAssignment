# TODO
Есть новостной сайт, с нагрузкой до 20000 запросов в минуту. Запросы равномерно распределяются по 5 серверам приложений. Данные хранятся на отдельном MySQL сервере, а на каждом сервере приложений поднят MySQL и между ними настроена Master-slave репликация. Необходимо собирать статистику по количеству просмотров каждой новостной статьи (шаг - 10 минут) и выводить ее в панели управления. Нужно учитывать, что при просмотре статьи происходит обращение только к локальному серверу БД. Опишите как бы вы подошли к решению данной задачи.

# Решение
Навскидку, я бы поставил redis на каждый сервер приложений и при каждом просмотре статьи делал бы:
```
INCR article_unique_key
```

А далле job на каждые десять минут, который бы сохранял текущие значения из redis-а и удалял соответствующий ключ:
```
GET article_unique_key
DEL article_unique_key
```

Сораненные значения отправлять на master в таблицу вида:
```sql
CREATE TABLE article_stat (
	article_stat_id SERIAL,
    article_id INT NOT NULL,
	server_id SMALLINT UNSIGNED NOT NULL,
	datetime DATETIME NOT NULL,
	value MEDIUMINT UNSIGNED NOT NULL,
    PRIMARY KEY (article_stat_id)
)
```