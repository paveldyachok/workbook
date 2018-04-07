#### PHP - Отлов ошибок

Выводит значение любой переменной в удобочитаемом виде.

```php
function d($value = null, $die = 1){
    echo 'Debug: <br><pre>';
    print_r($value);
    echo '</pre>';

    if ($die) die;
}
```

---

#### PHP - Обработка ошибок

В начале файла добавляем **перехватчик ошибок**:

```php
set_error_handler("myError");
```

Где `myError` имя функции которая будет выполнятся при возникновении ошибок.

**Функция перехвата ошибок:**

```php
// $no - номер ошибки
// $msg - сообщение об ошибки
// $file - адрес файла
// $line - номер строки на которой произошла ошибка

function myError($no, $msg, $file, $line){
    echo $msg

    // Логгируем пользовательские ошибки
    switch($no){
        case E_USER_ERROR:
        case E_USER_WARNING:
        case E_USER_NOTICE:
          error_log("$msg\n", 3, "error.log");
    }
}
```

**Отлавливаем ошибки:**

```php
if ($error){
    trigger_error("Что-то случилось", E_USER_ERROR);
}
```

Где в "Что-то случилось" прописываем что могло случиться при выполнении непосредственно в той функции, где мы расположили данный отлов.

#### Проверка на отправку HTML-формы методом POST

```php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {}
```

#### Отправка на e-mail

[stackoverflow](https://ru.stackoverflow.com/questions/31874/%D0%9E%D1%82%D0%BF%D1%80%D0%B0%D0%B2%D0%BA%D0%B0-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80)

Форма:

```php
<form action="mail.php" method="post">
<textarea name="mess"></textarea>
<input type="text" name="email">
<input type="submit" value="send">
</form>
```

mail.php

```php
if(isset($_POST['mess'])){
    //проверки на правильность данных

    $admin_mail = 'your@email.ru';
    $subj = 'Новое сообщение';
    $mess = htmlspecialchars($_POST['mess']);
    $headers = 'From: site@mail.ru' . PHP_EOL;
    $headers .= 'Content-type: text/plain; charset=utf-8' . PHP_EOL;

    if(mail($admin_mail, $subj, $mess, $headers)){
        //сообщение было выслано
    }
    else{
        //ошибка при отправке
    }
}
```



