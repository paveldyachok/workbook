## Функционал смены языка интерфейса для H-script

#### Файл lang.php

```php
global $langText;
/** EN, RU */
$langText = [
    // Слова которые могут повторно встречатся в проекте, но везде будут иметь один перевод
    'global' => [
        1 => [
            'Enter',
            'Вход'
        ]
    ],
    // Слова разбитые на категории
    'titles' => [
        1 => [
            'Authorization',
            'Авторизация'
        ]
    ]
];
```

#### Запись пути root директории в файле rw.php

```php
$_GS['ql_root_dir'] = __DIR__;
```

#### Функции обработчики

```php
/** LANG FUNCTIONS */

if (file_exists($_GS['ql_root_dir'] . '/lang/lang.php')) require($_GS['ql_root_dir'] . '/lang/lang.php');

$arrNameLangs = ['en', 'ru'];
if (!isset($_COOKIE["qllang"]) or !in_array($_COOKIE["qllang"], $arrNameLangs)) {
    setcookie('qllang', 'ru', time() + 30 * HS2_UNIX_DAY, '/');
} else {
    setcookie('qllang', $_COOKIE["qllang"], time() + 30 * HS2_UNIX_DAY, '/');
}

// $_user['uQlLang'] = $_COOKIE["qllang"];
// cl($_user, '_user');

global $langVar;
switch ($_COOKIE["qllang"]) {
    case 'en':
        $langVar = 0;
        break;
    case 'ru':
        $langVar = 1;
        break;
}

function getLangText($dataArr, $key)
{
	global $langText, $langVar;
    $text = ($langText[$dataArr][$key][$langVar]) ? $langText[$dataArr][$key][$langVar] : $langText[$dataArr][$key][0];
    return $text;
}

function getSelectedLangName()
{
    return $_COOKIE["qllang"];
}
```

#### Вызов функции в шаблоне

```php
{getLangText('global', 1)}
```
