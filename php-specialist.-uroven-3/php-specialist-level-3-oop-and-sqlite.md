# ООП с SQLite, XML

## Практическое использование ООП с базой данных SQLite

SQLite - это билиотека, на основе которой можно создать базу данных **без сервера**. Подходит для небольших проектов как веб, так и стационарных. Все данные хранятся в одном файле. Экранирование строк через двойной апостроф.

### Создание, открытие и закрытие базы данных <a id="coc"></a>

```php
// Создаём или открываем базу данных test.db
$db = new SQLite3("test.db");
// Закрываем базу данных без удаления объекта
$db->close();
// Открываем другую базу данных для работы
$db->open("another.db");
// Удаляем объект
unset($db);
```

### Выполнение запроса

```php
// Экранирование строк
$name = $db->escapeString($name);
// Для запросов без выборки данных
$sql = "INSERT INTO users (name, age) VALUES ('$name', 25)";
// Возвращает значение булева типа
$result = $db->exec($sql);
// Количество изменённых записей
echo $db->changes();
// Отслеживание ошибок
echo $db->lastErrorMsg();
```

### Выборка данных

```php
$sql = "SELECT name, age FROM users";

// В случае неудачи возвращает false
$result = $db->querySingle($sql);
// В $result - значение первого поля первой записи
$result = $db->querySingle($sql, true);
// В $result - массив значений первой записи

// Стандартная выборка
$result = $db->query($sql);
// Обработка выборки
$row = $result->fetchArray(); // SQLITE3_BOTH
// Получаем ассоциативный массив
$row = $result->fetchArray(SQLITE3_ASSOC);
// Получаем индесированный массив
$row = $result->fetchArray(SQLITE3_NUM);
```

В данном случае в переменную `$row` запишется таблица массивов. Для того чтобы перевести её в один массив выполняем перебор строк таблицы `$row` и записываем каждую строку в массив `$date`:

```php
$date = [];
while ($row = $result->fetchArray(SQLITE3_ASSOC)) {
    $date[] = $row;
}
```

## PHP и XML

XML \(Extensible Markup Language\) - расширяемый язык разметки. Используется для хранения структурированных данных, обмена информацией между программами, создания на его основе других, более специализированных, языков разметки.

Обеспечивает совместимость при передаче структурированных данных между разными системами обработки информации.

Для описание структуры документа используються:

* DTD – Document Type Definition - чаще используеться в HTML
* XML Схемы - более новая система валидации

### Средства PHP для работы с XML документом

* SAX \(Simple API for XML\) - чтение XML-документа

```php
// Создание парсера
$sax = xml_parser_create("utf-8");

// Декларация функций обработки событий
function onStart($parser, $tag, $attributes){
    // Пример
    if ($tag != "CATALOG" and $tag != "BOOK") {
        echo "<td>";
    }
    if ($tag == "BOOK") {
        echo "<tr>";
    }
}
function onEnd($parser, $tag){
    // Пример
    if ($tag != "CATALOG" and $tag != "BOOK") {
        echo "</td>";
    }
    if ($tag == "BOOK") {
        echo "</tr>";
    }
}
function onText($parser, $text){
    // Пример
    echo $text;
}

// Регистрация функций как обработчиков событий
xml_set_element_handler($sax, "onStart", "onEnd");
xml_set_character_data_handler($sax, "onText");

// Запуск парсера
xml_parse($sax, "XML строка!"); // Не работает с файлами, только строки!!
// Можно использовать функцию file_get_contents();
xml_parse($sax, file_get_contents("catalog.xml"));

// Обработка ошибок
echo xml_error_string(xml_get_error_code($sax));
```

* DOM \(Document Object Model\) - чтение, модификация и создание новых XML документов

Самый ресурсоёмкий, весь документ зачитывается в память и строится дерево узлов. Идея DOM: всё что есть в документе - это узел \(даже комментарий, табуляции и переносы строк\). Узлы в ООП являются объектами. Существуют типы узлов документа: ELEMENT, ATTRIBUTE, TEXT, COMMENT, DocumentType.

```php
// Создание объекта, экземпляра класса DomDocument
$dom = new DomDocument();
// Загрузка документа
$dom->load("catalog.xml");
// Получение коневого элемента
$root = $dom->documentElement; // тут будет каталог объектов
// Получение типа узла
echo $root->nodeType; // 1
// Получение коллекции дочерних узлов (экземпляр класса DomNodeList)
$children = $root->childNodes; // сразу кидать в foreach
// Получение текстового содержимого узла
$content = $root->textContent; // получим весь текст
// Получение коллекции элементов с определённым именем
$books = $dom->getElementsByTagName("book");

// Создание/изменение XML-документа

// Создание объекта, экземпляра класса DomDocument
$dom = new DomDocument("1.0", "utf-8");
// Получение коневого элемента
$root = $dom->documentElement;
// Создание новых элементов
$book = $dom->createElement("book");
$title = $dom->createElement("title");
// Создание текстового узла
$text = $dom->createTextNode("Название книги");
// Другой вариант создания нового элемента
$author = $dom->createElement("author", "Автор книги"); // в таком случае не нужно выполнять $title->appendChild($text);
// Добавление узлов к узлам
$title->appendChild($text);
$book->appendChild($title);
$root->appendChild($book);
// Добавляем узел к узлу перед другим узлом
$book->insertBefore($author, $title);

// Создаём секцию CDATA (обёртка для текста, в таком тексте можно использовать любые символы)
$description = $dom->createElement("description");
$cdata = $dom->createCDATASection("...описание книги...");
$description->appendChild($cdata);
$book->appendChild($description);

// Сохраняем документ
$dom->save("catalog.xml");
```

* SimpleXML - разработан php для чтение и модификация XML-документов
* XMLReader и XMLWriter - чтение и модификация XML-документов
* XSL/T \(Extensible StylesheetLanguage Transformations\) - преобразование XML-документов в другие форматы

