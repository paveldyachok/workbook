### Полезные ссылки

* [Документация](https://git-scm.com/book/ru/v2 "")
* [Git Wizardry на Хабре](https://habrahabr.ru/post/60347/ "")
* [Интерактивный тур по основам Git](https://githowto.com/ru "")

### Основные команды

`git --version` - выводит информацию об установленной версии git

`git config --global user.name "..."`, `git config --global user.email "..."` - 
установка глобальных данных пользователя git 

`git init` - инициализация git-проекта, создаёт скрытую папку с системными файлами git

`git add` - индексация, добавление на коммит кандидат

> Возможные параметры:

> `.` - добавление всех файлов в данной директории

> `*` - добавление всех файлов проекта

> `file name` - указание конкретного файла



---

#### Копирование файлов между ветками

Итак, представим, что для переноса функционала **mega-feature** в **master**, необходимо добавить из ветки develop-mega-feature следующие новые файлы: *megafeature/implementation.code*, *megafeature/description.txt* и следующий модифицированный файл *projectfeatures.code*. 

Находясь в ветке **master**, выполняем: 

`git checkout develop-mega-feature  megafeature/implementation.code  megafeature/description.txt  projectfeatures.code`

в качестве аргументов указываем ветку, из которой собираемся добавлять функционал и список файлов, относящихся к функционалу **mega-feature**.

[Оригинал статьи](https://habrahabr.ru/sandbox/42371/ "")

---