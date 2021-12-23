Реализовать приложение с одной точкой входа index.php и в зависимости от 
url вызывать соотвествующий контроллер и его метод. Например, сделаем чтобы когда мы переходим
на адрес test-site.local/test-uri мы должны попасть на TestController и выполнить метод indexAction().

index.php:
```php
$uriMap = [
	'/test-uri' => [TestController::class, 'indexAction']
];


if (isset($uriMap[$_SERVER['REQUEST_URI']]])) {
	[$nameClass, $action] = $uriMap[$_SERVER['REQUEST_URI']];
	$controller = new $nameClass();
	$nameClass->$action();
} else {
	http_response_code(404);
	echo 'Page not found';
	die();
}
```

src/Controller/TestController.php:
```php
class TestController {
	public function indexAction() 
	{
		echo "I am in TestController";
	}
}
```

Реализовать логику для таких URL:
/ => IndexController, indexAction
/news => NewsController, indexAction
/news/edit => NewsController, editAction
/albums => AlbumsController, indexAction
