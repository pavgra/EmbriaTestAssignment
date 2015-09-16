# TODO
Имеется переменная $url содержащая адрес веб-страницы и вызов preg_match($regexp, $url, $matches). Какое значение переменной $regexp приведет к тому, что в $matches будет 2 элемента, причем второй элемент будет содержать только домен?

#Решение

```php
	// Проблема с тем, что доменная зона может быть составной, например, 'co.uk'
	// Поэтому (и не только) не придумал ничего лучше, чем перечисление возможных вариантов доменных зон
	// С другой стороны, перечисление, хоть и менее красивый, но более точный и справедливый метод
	// (вот тут, например, https://gist.github.com/gruber/8891611, используют перечисление, и кол-во звездочек очень даже)
	$regexp = '/(?<=^|http:\/\/|https:\/\/)[A-Za-z0-9-]*?\.?([A-Za-z0-9-]+)\.(?:com|ru|co\.uk|com\.au)(?:[^A-Za-z]|$)/m';
	$urlList = [
		'https://mail.google.co.uk/mail/u/0/#inbox/14fd0b253b7b1cd2?projector=1',
		'https://mail.google.com',
		'http://mail.google.com',
		'http://google.com',
		'http://www.google.com/',
		'mail.google.com',
		'google.com',
		'www.google.com',
		'www.google.co.uk'
	];
	$matches = [];

	foreach ($urlList as $url) {
		preg_match($regexp, $url, $matches);
		var_dump($matches[1]);
	}
```