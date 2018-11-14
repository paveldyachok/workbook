#### Получение данных из input'ов без формы

[stackoverflow](https://ru.stackoverflow.com/questions/247752/%D0%9F%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%B8%D0%B7-input%D0%BE%D0%B2-%D0%B1%D0%B5%D0%B7-%D1%84%D0%BE%D1%80%D0%BC%D1%8B)

```js
<a href="#" onclick="document.getElementById('myform').submit(); return false;">Отправить</a>
```

#### Для экранирования специальных знаков (-, /, \, ^, $, *, +, ?, ., (, ), |, [, ], {, })

[stackoverflow](https://ru.stackoverflow.com/questions/434779/%D0%97%D0%B0%D0%BC%D0%B5%D0%BD%D0%B0-%D0%B2%D1%8B%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F-%D1%81%D0%BE%D0%B4%D0%B5%D1%80%D0%B6%D0%B0%D1%89%D0%B5%D0%B3%D0%BE-%D0%BA%D1%80%D1%83%D0%B3%D0%BB%D1%8B%D0%B5-%D1%81%D0%BA%D0%BE%D0%B1%D0%BA%D0%B8-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E-replace)

```js
function formatText(str) {
    let searchText = ' ' + str;
    RegExp.escape = function(text) {
        return (text + '').replace( /[.?*+^$[\]\\(){}|-]/g, "\\$&" );
    };
    return RegExp.escape(searchText);
}
```

Вызов:
```js
let text = formatText(el.target.dataset.val);
commentText.innerHTML = commentText.innerHTML.replace(new RegExp(text,'g'), '');
```
