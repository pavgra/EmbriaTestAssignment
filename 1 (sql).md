# TODO
Напишите SQL-запрос, который выведет список фотографий, с указанием количества комментариев, отсортированные в порядке убывания их количества, у которых меньше 5 пользователей-комментаторов.

# Решение
```sql
CREATE DATABASE dummy;
USE dummy;

CREATE TABLE `photos` (
    `photo_id` int(11) NOT NULL,
    `photo_title` tinytext NOT NULL,
    PRIMARY KEY (`photo_id`)
)
ENGINE=InnoDB DEFAULT CHARSET=cp1251;

CREATE TABLE `comments` (
    `comment_id` int(11) NOT NULL AUTO_INCREMENT,
    `photo_id` int(11) unsigned NOT NULL,
    `user_id` int(11) unsigned NOT NULL,
    `comment_text` text NOT NULL,
    PRIMARY KEY (`comment_id`)
)
ENGINE=InnoDB DEFAULT CHARSET=cp1251;

INSERT INTO photos 
    (`photo_id`, `photo_title`) 
VALUES
    (1, 'mikeescamilla_bike'),
    (2, 'tonyhawk_skateboard'),
    (3, 'kellyslater_surf'),
    (4, 'humzadeas_bridge'),
    (5, 'raskalov_shanghai');

INSERT INTO comments
    (`photo_id`, `user_id`, `comment_text`)
VALUES
    (2, 1, 'his print of me about to drop in on The D'),
    (2, 2, 'I like this photo. I like them all.'),
    (2, 3, 'you are a great man tony'),
    
    (3, 1, 'But seriously italo was scored low in his heat with wiggoly..'),
    (3, 2, 'It\'s just a contest'),
    (3, 3, 'Let\'s see someone recreate that "error"'),
    (3, 4, 'You\'re still the man! Keep up your amazing surfing.'),

    (4, 1, 'Nice'),
    (4, 2, 'Killin it'),
    (4, 2, 'Amazing'),
    (4, 3, 'It\'s like the yellow brick road... but it\'s gold.'),
    (4, 4, 'Great shot'),
    (4, 4, 'Dope'),

    (5, 1, 'welcome back'),
    (5, 2, 'you\'d love it here'),
    (5, 3, 'omg'),
    (5, 4, 'Seriously?'),
    (5, 5, 'Its pretty... until u fall');

SELECT p.photo_title,
  COUNT(c.comment_id) comment_count
FROM photos p
  LEFT JOIN comments c USING (photo_id)
GROUP BY p.photo_id
HAVING COUNT(DISTINCT c.user_id) < 5
ORDER BY comment_count DESC;
```