# GIT - Полезные команды

## Основные команды

`git --version` - выводит информацию об установленной версии git

`git config --global user.name "..."`, `git config --global user.email "..."` - установка глобальных данных пользователя git

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

`git commit --amend -m "Новое сообщение коммита"`  - дополняет последний коммит, добавляя в него "свежие" изменения. Также, меняет сообщение последнего коммита. Новый коммит не создается!

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

`git checkout` Используется для перемещения между коммитами, версиями отдельных файлов и ветками.

+ параметры:

> `3452364...` - переходит к коммиту с хэшем 3452364...
>
> `master` - возврат к исходному состоянию по названию ветви
>
> `newbranch` - переключает на ветвь newbranch
>
> `-b newbranch` - создаёт новую ветвь с названием newbranch и перейдёт на неё 
>
> `newbranch name.md` - скопирует файл _name.md_ из ветви _newbranch_ в ветвь из которой была вызвана данная команда

`git branch` - показывает все активные ветви в локальном репозитории

`git branch -d название_ветки`  - удаления ветки

`git merge dev` - сливает \(объединяет\) ветвь dev с той из которой была выполнена команда

`git rebase dev` - похожа на merge, но не запоминает истории коммитов \(не создаёт новый коммит\), не рекомендуется делать в главной ветви

`git rebase -i`  - интерактивный rebase. 

Кто можно сделать с помощью интерактивного rebase:

> Поменять коммиты местами
>
> Поменять название коммита / коммитов
>
> Объединить два коммита в один
>
> Добавить изменения в существующий коммит
>
> Разделить коммит на несколько коммитов
>
> ...

`git cherry-pick`  - используется тогда, когда нам надо "взять" один или несколько коммитов из другой ветки в нашу ветку.

> --edit - можно изменить название коммита при переносе
>
> --no-commit - переносим изменения из коммита но не делаем новый, оставляем изменения в отслеживаемой зоне. Так же с таким параметром можно перенести несколько коммитов.
>
> git cherry-pick -x хэш\_коммита - указывает в сообщении коммита хэш того коммита, из которого мы сделали cherry-pick
>
> git cherry-pick --signoff хэш\_коммита - указывает в сообщении коммита имя того пользователя, кто совершил cherry-pick

 `git diff`  показывает разницу между текущим **неотслеживаемым** состоянием и последним снимком

+ параметры:

> --staged - между текущим **отслеживаемым**
>
> COMMIT\_ID - между текущим и указаным снимком

`git reset [--soft | --mixed | --hard] [commit]` - отменяет изменения в проекте.

> --soft - возвращает проект к указанному коммиту, при этом переводит все коммиты после указанного в отслеживаемую \(staged\) зону;
>
> --mixed - \(по умолчанию\) возвращает проект к указанному коммиту, при этом переводит все коммиты после указанного в неотслеживаемую \(unstaged\) зону;
>
> --hard - Возвращает проект к указанному коммиту, при этом полностью удаляет все коммиты после указанного. Самая "сильная" вариация git reset. Удаляет коммиты безвозвратно!

Вместо указания коммита можно указывать `HEAD^^` или `HEAD~2`  - в данном случае будет сдвинуто на два снимка назад.

`git stash`  - берет изменённое состояние вашей рабочей директории, то есть изменённые отслеживаемые файлы и проиндексированные изменения, и сохраняет их в хранилище незавершённых изменений, которые вы можете в любое время применить обратно. [Подробнее](https://git-scm.com/book/ru/v2/%D0%98%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-Git-%D0%9F%D1%80%D0%B8%D0%B1%D0%B5%D1%80%D0%B5%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B8-%D0%BE%D1%87%D0%B8%D1%81%D1%82%D0%BA%D0%B0)

`git stash list`  - посмотр списка спрятанных изменений

`git stash pop`  - возвращает последние спрятанные изменения и сразу удаляет изменения их хранилища stash

`git stash apply`  - возвращает последние спрятанные изменения

`git stash apply stash@{2}`  - вернёт изменение из списка с индексом 2

`git stash drop stash@{2}`  - удаляет изменения с индексом 2 из хранилища stash 

### Работа с удалённым репозиторием

`git remote`  - команда для настройки и просмотра удаленных репозиториев.

> -v  - просмотр списка существующих удаленных репозиториев

`git remote add НАЗВАНИЕ_РЕПОЗИТОРИЯ`_`АДРЕС_РЕПОЗИТОРИЯ`  -_ добавить новый удаленный репозиторий, который находится по указанному адресу. При этом, на нашем компьютере к удаленному репозиторию мы будем обращаться по его названию.

`git remote remove НАЗВАНИЕ_РЕПОЗИТОРИЯ`  - удалить репозиторий с указанным названием

`git branch -r`  - показывает ссылки на состояние веток в удалённых репозиториях

Создаем удаленный репозиторий, указывая имя учетной записи, "demo" - название будующего репозитория:

```text
curl -u 'USER_NAME' https://api.github.com/user/repos -d'{"name":"demo"}'
```

Выгружаем проект:

```text
git remote add origin https://github.com/USER_NAME/demo.git
git push -u origin master
```

#### Для заливки готового репозитория

`git clone http://www.git...` - клонирует проект в локальную дерикторию со всеми коммитами

`git pull` - выкачивает изменения из удалённого репозитория

> `origin dev` - выкачивает изменения из ветви dev
>
> `--rebase origin master` - выкачает все изменения из ветви master и наложит их таким образом, как будто изменений небыло. А после, поверх всех коммитов запишет локальные изменения.

`git push` - записывает все изменения на удалённый репозиторий

> `origin newbranch` - создаёт новую ветвь на удалённом репозитории

### Копирование файлов между ветками

Итак, представим, что для переноса функционала **mega-feature** в **master**, необходимо добавить из ветки develop-mega-feature следующие новые файлы: _megafeature/implementation.code_, _megafeature/description.txt_ и следующий модифицированный файл _projectfeatures.code_.

Находясь в ветке **master**, выполняем:

`git checkout develop-mega-feature megafeature/implementation.code megafeature/description.txt projectfeatures.code`

в качестве аргументов указываем ветку, из которой собираемся добавлять функционал и список файлов, относящихся к функционалу **mega-feature**.

[Оригинал статьи](https://habrahabr.ru/sandbox/42371/)

## Полезные ссылки

* [Документация](https://git-scm.com/book/ru/v2)
* [Команды Git](https://git-scm.com/book/ru/v2/Appendix-C%3A-%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%8B-Git-%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%B8-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F)
* [Ежедневная работа с Git](https://habrahabr.ru/post/174467/)
* [Git Wizardry на Хабре](https://habrahabr.ru/post/60347/)
* [Интерактивный тур по основам Git](https://githowto.com/ru)
* [Шпаргалка по Git](http://dev-lab.info/2013/08/%D1%88%D0%BF%D0%B0%D1%80%D0%B3%D0%B0%D0%BB%D0%BA%D0%B0-%D0%BF%D0%BE-git-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5-%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%8B-%D1%81%D0%BB%D0%B8%D1%8F%D0%BD/)

