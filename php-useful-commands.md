### Полезные ссылки

* [Документация](https://git-scm.com/book/ru/v2)
* [Команды Git](https://git-scm.com/book/ru/v2/Appendix-C%3A-%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%8B-Git-%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%B8-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F)
* [Ежедневная работа с Git](https://habrahabr.ru/post/174467/)
* [Git Wizardry на Хабре](https://habrahabr.ru/post/60347/)
* [Интерактивный тур по основам Git](https://githowto.com/ru)
* [Шпаргалка по Git](http://dev-lab.info/2013/08/%D1%88%D0%BF%D0%B0%D1%80%D0%B3%D0%B0%D0%BB%D0%BA%D0%B0-%D0%BF%D0%BE-git-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5-%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%8B-%D1%81%D0%BB%D0%B8%D1%8F%D0%BD/)

### Основные команды

`git --version` - выводит информацию об установленной версии git

`git config --global user.name "..."`, `git config --global user.email "..."` -   
установка глобальных данных пользователя git

`git init` - инициализация git-проекта, создаёт скрытую папку с системными файлами git

`git add` - индексация, добавление на коммит кандидат

> Возможные параметры:
>
> `.` - добавление всех файлов в данной директории
>
> `*` - добавление всех файлов проекта
>
> `file name` - указание конкретного файла

`git commit -m "Commit description"` - выполнение коммита с описанием.

`gitk` - графический просмотрщик коммитов.

`git status` - проверка статуса репозитория.

`git log` - история коммитов с комментариями.

> Возможные параметры:
>
> `--pretty=oneline` - в одну сторку
>
> `--pretty=oneline --mar-count=3` - только три строки
>
> `--pretty=oneline --all` - все коммиты
>
> `--pretty=oneline --autor="Pavel ..."` - выборка по автору
>
> `--pretty=format:"%h - %s : %ad [ %an ]"` - выборка в установленном формате

`git checkout` + параметры:

> `3452364...` - переходит к коммиту с хэшем 3452364...
>
> `master` - возврат к исходному состоянию по названию ветви
>
> `newbranch` - переключает на ветвь newbranch
>
> `-b newbranch` - создаёт новую ветвь с названием newbranch и перейдёт на неё
> `newbranch name.md` - скопирует файл _name.md_ из ветви `newbranch` в ветвь из которой была вызвана данная команда

`git branch` - показывает все активные ветви в локальном  репозитории 

`git merge dev` - сливает (объединяет) ветвь dev с той из которой была выполнена команда

`git rebase dev` - похожа на merge, но не запоминает истории коммитов, не рекомендуется делать в главной ветви

#### Работа с удалённым репозиторием 

`git clone http://www.git...` - клонирует проект в локальную дерикторию со всеми коммитами

`git pull` - выкачивает изменения из удалённого репозитория

> `origin dev` -  выкачивает изменения из ветви dev
>
> `--rebase origin master` - выкачает все изменения из ветви master и наложит их таким образом, как будто изменений небыло. А после, поверх всех коммитов запишет локальные изменения.

`git push` - записывает все изменения на удалённый репозиторий

> `origin newbranch` - создаёт новую ветвь на удалённом репозитории

---

#### Копирование файлов между ветками

Итак, представим, что для переноса функционала **mega-feature** в **master**, необходимо добавить из ветки develop-mega-feature следующие новые файлы: _megafeature/implementation.code_, _megafeature/description.txt_ и следующий модифицированный файл _projectfeatures.code_.

Находясь в ветке **master**, выполняем:

`git checkout develop-mega-feature  megafeature/implementation.code  megafeature/description.txt  projectfeatures.code`

в качестве аргументов указываем ветку, из которой собираемся добавлять функционал и список файлов, относящихся к функционалу **mega-feature**.

[Оригинал статьи](https://habrahabr.ru/sandbox/42371/)

---


