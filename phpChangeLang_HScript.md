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

global $arrNameLangs;
$arrNameLangs = ['en', 'ru'];

if (!isset($_COOKIE["qllang"]) or !in_array($_COOKIE["qllang"], $arrNameLangs)) {
    setcookie('qllang', 'ru', time() + 30 * HS2_UNIX_DAY, '/');
} else {
    setcookie('qllang', $_COOKIE["qllang"], time() + 30 * HS2_UNIX_DAY, '/');
}

// global $_user;
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

$langsArr = [$_COOKIE["qllang"]];
foreach ($arrNameLangs as $value) {
	if ($value != $_COOKIE["qllang"]) {
		array_push($langsArr, $value);
	}
}
setPage('langsArr', $langsArr);

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

#### Получение необходимого перевода в шаблоне

```php
{getLangText('global', 1)}
```

#### Обработчик переключения языков module/custom/qllang.php

```php
require_once('module/auth.php');
global $db;
global $arrNameLangs; // module/lib.php

// cl($arrNameLangs, '$arrNameLangs');

// LANG MODE
if (isset($_GET['qllang']) and in_array($_GET['qllang'], $arrNameLangs)) {
    $_user['uQlLang'] = $_GET['qllang'];
    setcookie('qllang', $_GET['qllang'], time() + 30 * HS2_UNIX_DAY, '/');
    // if (_uid()) $db->update('Users', array('uQlLang' => $_GET['qllang']), '', 'uID=?d', array(_uid()));
}

header('Location: ' . $_SERVER['HTTP_REFERER'] );
exit();
```

#### Добавляем маршрутизацию в _config.php

```php
'custom/qllang' => array('setlang'),
```

#### Переключатель языков в шаблоне

```php
<div class="col-6 languageBlock">
<li class="nav-item dropdown">
    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown1" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">{$langsArr[0]}</a>
    <div class="dropdown-menu" aria-labelledby="navbarDropdown1">
	<a class="dropdown-item" href="/setlang?qllang={$langsArr[1]}">{$langsArr[1]}</a>
	{* <a class="dropdown-item" href="#">UK</a> *}
    </div>
</li>
</div>
```
