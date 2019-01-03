#### Получение данных из input'ов без формы

[stackoverflow](https://ru.stackoverflow.com/questions/247752/%D0%9F%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%B8%D0%B7-input%D0%BE%D0%B2-%D0%B1%D0%B5%D0%B7-%D1%84%D0%BE%D1%80%D0%BC%D1%8B)

```html
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

#### Получение ID выбранной в select опции и поиск индекса в массиве объектов по свойству ID

```js
nasosVariants.onchange = function () {
    const selectID = this.selectedOptions[0].id;
    const index = dataNasos.arrNasosiv.findIndex(x => x.id == selectID);
}
```

#### Регулярка, оставляем в строке только цифры и "-" далее преобразуем в массив

```js
let arrRange = key.match(/[-\d]+/g)[0].split('-');
```


#### Обработка нажатия кнопок клавиатуры

```js
var mainCharsArr = [8, 37, 39];
var numbersCharsArr = [48, 49, 50, 51, 52, 53, 54, 55, 56, 57];
document.onkeypress = function (key) {
    // console.log(key.which);
    var charsLimit, charsArr, allowableCharsArr, maxValue = false;

    var classList = key.target.classList;
    for (const className of classList) {
        switch (className) {
            case 'zahalVidstan':
                charsLimit = 4;
                maxValue = 1000;
                // charsArr = [43, 120, 1093, 42, 46, 44];
                allowableCharsArr = mainCharsArr.concat(numbersCharsArr);
                break;
        }
    }

    // ограничение количества введённых символов
    if (charsLimit && key.target.value.length >= charsLimit) {
        return false;
    }

    // проверка на допустимые символы
    if (allowableCharsArr && $.inArray(key.which, allowableCharsArr) == -1) {
        return false;
    }

    // получаем значение из разных видов полей
    let val = '';
    switch (key.target.localName) {
        case 'input':
            val = key.target.value;
            break;
        default:
            val = key.target.innerText;
            break;
    }
    
    // проверка на максимальное значение
    if (maxValue && parseInt(val + '' + key.key) > maxValue) {
        return false;
    }
};
```

#### Запрет ввода кириллицы

```js
// ONLY LATIN CHARACTERS
var inputElements = kycBlock.querySelectorAll('.fieldsBlock input');
for (const i of inputElements) {
    i.onkeydown = function(e) {
        var reg = /[а-яА-ЯёЁ]/g;
        if (e.key.search(reg) != -1) {
            return false;
        }
    }
}
```

#### Копирование в буфер обмена по клику

```html
<p id="bisnesPartnerUrl" class="refUrl">http://.../?ref={$user.uLogin}</p>
<img src="{$img_path}img/copy-content.png" alt="copy" onclick="copyClipboard('bisnesPartnerUrl')">
```

```js
function copyClipboard(nameID) {
    var url = document.getElementById(nameID).innerHTML;
    var el = document.createElement('textarea');
    el.value = url;
    document.body.appendChild(el);
    el.select();
    document.execCommand('copy');
    document.body.removeChild(el);
}
```

#### Переключатель блоков (NBT, cabinet)

```js
/** SWITCH INVEST VARIANTS */
if (target = document.getElementById('investVarBlock')) {
    var spans = target.querySelectorAll('.investSelect span');
    for (const i of spans) {
        i.addEventListener('click', function () {
            delActiveVar(target.querySelectorAll('.varBlock'), 'activeVar');
            var selectVar = target.querySelector('#' + this.dataset.target);
            selectVar.classList.add('activeVar');

            delActiveVar(spans, 'activeSelect');
            i.classList.add('activeSelect');
        });
    }

    function delActiveVar(elementsArr, className) {
        for (const i of elementsArr) {
            i.classList.remove(className);
        }
    }
}
```

#### Отслеживание изменений в DOM
[статья](https://habr.com/company/ruvds/blog/351256/)

```js
var nasosVariants = document.querySelector('.nasosVariants');

// Функция которая вызывается при изменеиях childList в элементе nasosVariants
function resetSelectedParams() {
    // code..
}

new MutationObserver(resetSelectedParams).observe(nasosVariants, {
    childList: true
});
```
