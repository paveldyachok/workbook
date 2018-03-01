\#PHP - Отлов ошибок. Выводит значение любой переменной в удобочитаемом виде.

```php
function d($value = null, $die = 1){
    echo 'Debug: <br><pre>';
    print_r($value);
    echo '</pre>';

    if ($die) die;
}
```

#PHP - переопределение обработчика ошибок
В начале файла добавляем:
set_error_handler("myError"); 