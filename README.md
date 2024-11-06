# Git-summary

Summary of Git commands

Git - система контроля и хранения версий и истории разработки.

GitHub — это веб-сервис для размещения проектов и совместной разработки, основанный на Git.

### Настройка

Имена пользователя и адрес электронной почты, используемые для идентификации автора коммитов, задаются с помощью команды `git config user.name` и `git config user.email`.

`git config —-global user.name “ник гитхаба”` - настройка для пользователя локального репозитория

В Git локальная конфигурация применяется к конкретному репозиторию, тогда как глобальная конфигурация применяется ко всем репозиториям текущего пользователя, если для них нет локальной конфигурации.
 
`git config —-global user.email “почта гитхаба”` - установка почты которая отобразится в коммитах

`git config --global core.editor 'путь до файла IDE.exe'` - установка редактора для коммит-сообщений.

`git config --global alias.last 'log -1 HEAD'` - создать алиасы(псевдонимы для команд гит) и собственные команды (log -1 HEAD)

### Создание репозитория
 
`git init имя проекта` - инициализация репозитория, используется для создания нового локального репозитория в текущей директории.
 
`git clone url-репозитория` - клонирование удаленного репозитория на компьютер и создает локальную копию с историей всех коммитов

`master` — это основная ветка в локальном репозитории, а `origin/main` — это версия основной ветки на удалённом репозитории (обычно именуемом `origin`).

### Внесение изменений
 
`git status ` -выводит все изменения в файлах, которые еще не были индексации (новые файлы и новые изменения в отслеживаемых файлах); показывает состояние файлов в рабочей директории и в области индексации (staging area), указывая, какие файлы были изменены, добавлены или подготовлены для коммита.

`git log` - отображает историю коммитов текущей ветки, включая информацию о каждом коммите, такую как автор, дата и сообщение коммита.
 
`git diff` -выводит различия по текущим изменениям в непроиндексированных файлах

`git add имяФайла` - добавляет файл в индекс и позволяет начинать их отслеживать
`git add .`  - добавляет все файлы в индекс


`git diff —-staged` -показывает различия между проиндексированным файлом и последними коммитами
  
`git reset имяФайла` - удаляет файл из индекса, но не из рабочей директории
  
`git commit -m “сообщение“` - фиксирует изменения из индекса и сохраняет их в историю версий в локальном репозитории (флаг м говорит что будет сообщение); сохраняет изменения, которые были добавлены в область индексации (staging area), в локальный репозиторий.

`git commit -am` - выполняет сохранение всех изменений для отслеживаемых (tracked) файлов (включая неиндексированные изменения), добавляя их в коммит, и позволяет указать сообщение коммита. Она не затрагивает неотслеживаемые (untracked) файлы.

### Работа с файлами
  
`git rm имяФайла` - удаляет выбранный файл из рабочей директории и заносится в индекс как удаленный
  
`git rm —-cached имяФайла` - удаляет выбранный файл из контроля версий, его изменения не отслеживаются, но он останется на месте; удаляет файл только из репозитория, оставляет в файловой системе.
  
`git mv имяФайла новоеИмяФайла` - перемещает и переименовывает выбранный файл, занося в индекс.
  
### Временное сохранение
  
`git stash` или `git stash save 'описание'` - временно сохраняет непроиндексированные измененные файлы, помогает восстановить рабочую директорию с момента последнего коммита. `save “описание”` позволяет добавить описание.


`git stash pop` - восстанавливает последнее временно сохраненное состояние файлов в рабочую директорию и удаляет их из временного хранилища

`git stash apply` - восстанавливает последнее временно сохраненное состояние файлов в рабочую директорию оставляет их во временном хранилище
  
`git stash list` - выводит список всех временных сохранений с помощью git stash.
  
`git stash drop`- сбрасывает последние временно сохраненные изменения
  
### Просмотр истории
  
`git log` - история коммитов для текущей ветки и вся информация о них, последний коммит вверху.
  
`git log —-follow имяФайла` - история изменений конкретного файла
  
`git diff имяПервойВетки … имяВторойВетки` - показывает разницу между содержанием коммитов двух веток
  
`git show коммит `- выводит изменения, внесённые конкретным коммитом, а также информацию о самом коммите, такую как автор, дата и сообщение коммита.

`git blame имяФайла` - посмотреть кто редактировал файл, с указанием каждой строки

`git bisect` - ищет определенный коммит бинарным поиском, чтобы найти коммит, который вызвал ошибку 
  

### Откат коммитов

###### Отменить изменения в файловой системе

`git checkout —- имяФайла` - отменяет изменения в выбранном файле , которые еще не проиндексированы, то есть до выполнения команды `git add`

`git checkout .` - отменяет изменения во всех не проиндексированных файлах

! Вернуть контент после `checkout` - невозможно.
! Не работает для новых файлов, которые еще не отслеживались гитом, так как у них нет предыдущей версии.

`git checkout хеш-коммита` - позволяет перемещать указатель текущей ветки на указанный коммит без изменения файлов в рабочей директории.

`git clean -xdf` - удаляет новые файлы, которые еще не отслеживались гитом, из рабочей локальной области.

Флаг `x` - игнорирование правил гита и файла гит игнор
Флаг `d` - удаление файлов вместе с директориями
Флаг `f` -  усиление, что то вроде `!important` в `css`

! Просто команда `git clean` ничего не удалит, только с флагом `f` (force) , так как в гите есть правило ничего не удалять без этого флага
! Вернуть файлы после `git clean -xdf`- невозможно

###### Отменить изменения после добавления в индекс

`git reset HEAD имяФайла` - удаляет файл из индекса

То же самое можно сделать в GIT GUI, кликнув на иконку файла в `staged area` и он переместится в `unstaged area`.

После удаления из индекса можно воспользоваться `git checkout` и тд.

###### Отменить изменения в коммите

Если контент в коммите - ценный

`git commit —- ammend -m “сообщение”` -  обновить предыдущий коммит, можно изменить сообщение последнего коммита и контент, работает до отправки коммита в удаленный репозиторий

`--no-edit` позволяет внести изменения в коммит без изменения его сообщения.

Если контент в коммите - не ценный

`git reset HEAD^^ или (HEAD~2)` - убирает из истории нужное число последних коммитов, работает до отправили коммита в удаленный репозиторий
^^ или ~2 - означает насколько коммитов назад нужно вернуться

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/IMG_4094.jpeg)

`git reset коммит или указатель HEAD
Отменяет все коммиты после выбранного, оставляя все изменения в рабочей директории

По умолчанию `git reset` используется с флагом `—-mixed` - перебрасывает контент из коммита в рабочую директорию, минуя индекс

`git reset —-soft` `коммит или указатель HEAD` - удаляет контент из коммита и перебрасывает в индекс; перемещает указатель, но сохраняет изменения в области индексации (staging area).

`git reset —-hard коммит или указатель HEAD`
Сбрасывает все изменения и состояние рабочей директории до выбранного коммита, удаляет контент внутри коммитов, далее восстановить контент невозможно

Если контент нужно удалить навсегда

`git filter-branch --tree-filter 'rm -f имяФайла' HEAD` - проходит по ветке и удаляет из всех коммитов определенный файл безвозвратно

###### Отменить изменения в удаленном репозитории

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/IMG_4095.jpeg)

`git revert хеш-коммита` - создает новый коммит, который создает обратные изменения тому коммита, который мы хотим удалить. По умолчанию сообщение коммита будет `revert “ сообщение удаляемого коммита”`.

Открывается редактор vim. Для того, чтобы отредактировать сообщение - нажать `insert`. Для выхода из режима редактирования нажать `escape`.
Сохранить изменения `:wq`. Записывает изменения на диск. Выйти не записывая изменения `:q!`.

Можно сделать `revert` на `revert-коммит`, так как это такой же коммит, но с зеркальным контентом.

Не удаляет коммит из истории.

### Ветки

Вес файла ветки === 41 байт

`git checkout -b 'названиеНовойВетки'` - создает новую ветку и переключает на нее

`git checkout имяВетки ` - переключение между ветками

`git branch или git branch --all`
Выводит список веток

`git branch имяВетки`
Создают новую ветку

`git switch -c имяВетки`
Переключается на выбранную ветку и обновляет рабочую директорию

`git branch -d имяВетки`
Удаляет выбранную ветку

### Слияние веток

`Fast-forward Merge` - перемещение указателя HEAD на последний коммит другой ветки.

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103152948.png)

`Non Fast-forward Merge` - создает дополнительный коммит, который собирает в себе изменения из двух веток, на который переносится указатель HEAD.

Открывается vim и предлагает отредактировать автоматически сгенерированный текст `merge branch 'имя ветки'` результирующего коммита.

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103152908.png)

`HEAD` - указатель - указывает на последний коммит по умолчанию, если несколько веток - HEAD столько же; можно перемещать при merge (слиянии);

`git merge имяВетки` - вносит изменения из указанной ветки в текущую (Fast-forward Merge), присоединяет коммиты из указанной ветки в текущую и перемещает указатель HEAD на последний коммит

`git merge удаленныйРепозиторий или имяВетки` - вносит изменения из удаленного репозитория в локальный.

`git merge --abort` - прервать сляние и вернуть все как было.

Когда выполняется `git merge` без конфликтов, изменения из указанной ветки объединяются с текущей веткой, создавая новый коммит слияния (merge commit), который сохраняет всю историю изменений.

### Синхронизация с удаленным репозиторием

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103165017.png)

`git fetch удаленныйРепозиторий` - скачивает всю историю с удаленного репозитория (синхронизирует два репозитория, но не вносит изменения в файловую систему, для внесения изменений git merge)

`git push удаленныйРепозиторий или имяВетки` - загружает данные из локальной ветки в удаленный репозиторий. Отправляет данные в удаленный репозиторий.

`git push -u origin имяВетки` - команда `git push -u origin my-branch` устанавливает `имяВетки` как отслеживаемую ветку для удалённой ветки `origin/имяВетки`. После этого, при использовании `git push` без дополнительных параметров, Git будет знать, какую ветку нужно обновлять.

`git pull` - загружает историю из удаленного репозитория и объединяет ее с локальной
(Pull=fetch+merge)

`git remote add url-удаленногоРепозитория` - добавление удаленного репозитория

`git push --set-upstream origin master` - отправить текущую ветку для установки нового удаленного репозитория

`git remote -v` - отображает URLs удалённых репозиториев и указывает используемый протокол (например, HTTPS или SSH)

`git remote remove origin` - удаление привязки удаленного репозитория

При потере старого репозитория:
`git remote -v`
`git remote remove origin`
`git remote add url-удаленногоРепозитория`
`git push --set-upstream origin master`

### REBASE

Подробный гайд по этой команде https://eternalrival.notion.site/Rebase-tutorial-694c542f037a49b8ac5dc472defb25ea

Rebase - изменение базы коммита; подтягивает изменения, внесенные в одной ветке в другую, синхронизируя их; рекомендуется делать на небольших ветках, но не в master/origin ветке.
![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103155957.png)
![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103160046.png)

`git rebase -i` (интерактивный rebase) позволяет управлять историей коммитов, в том числе изменять, удалять и объединять коммиты.

При выполнении `git rebase` без конфликтов история текущей ветки переписывается путем создания новых коммитов, начиная с конца указанной ветки. Это позволяет наложить коммиты текущей ветки поверх указанной, создавая линейную историю.

Rebase построен на совокупности cherry-pick'ов

`cherry-pick ` - копирование коммита из одной ветки в другую, не вызывает конфликтов так как у скопированного коммита и оригинала одинаковый хеш-код, позволяет перенести отдельный коммит из одной ветки в другую, сохраняя изменения, внесённые в этом коммите.

### Конфликты

Конфликт - в файле на одних и тех же строках разный контент.
![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103153414.png)

###### Варианты решений:

1. Исправить конфликт вручную -> сделать коммит
2. Прервать слияние командой `git merge --abort`

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103154348.png)

###### Избегание конфликтов:

1. Частые коммиты
2. Не редактировать пробелы, табуляции, переносы
3. Частые слияния

###### Если изменения незначительные

`git checkout --Xours` - решить конфликт в пользу своего кода

`git checkout --Xtheirs` - решить конфликт в пользу чужого кода

`git diff` - решение конфликта вручную в командной строке

`git revert хеш-коммита` - отменить слияние

### Теги

Тег можно использовать вместо хеша коммита.

`git tag имяТега` - присвоение тега какому либо коммиту.

`git tag -list` - выводит список тегов.

`git push --tags` - отправка в удаленный репозиторий только коммитов с тегами.

`git checkout имяТега` - переключение между тегами

### Git GUI & Git Gitk

###### Git GUI- это расширенный git bash.

`git gui&`
Запуск

Вносим изменения в какой либо файл, который отлеживается гит.

После изменения файла нажимаем `rescan`.
Слева сверху в `unstated changes` начинает отображаться измененный файл.
Справа сверху в `modified not staged` отображаются сами изменения. Красный- удаленные данные, зеленый - новые данные.

Для коммита изменений нажимаем на ИКОНКУ файла, он переносится в `staged changes`. В поле `commit messages` пишет текст коммита. Нажимает `commit`.

###### Gitk - предназначен для просмотра истории

### Папка .git

Папка .git- является скрытой.
Внутри папки .git:
`[hooks]`- папка, хранит скрипты
`[objects]` - папка, хранит объекты коммитов, хранит папки (директории), в них хранятся блобы, в которых хранится контент в бинарном виде.
`HEAD` - файл, ссылку на текущую ветку
`[refs]` - папка, хранит ветки, содержит в себе папки `heads` -> `master` -> `ссылку на последний коммит`
`index` - файл, хранит промежуточную информацию об изменениях, далее она идет в коммит

COMMIT - ссылаются на деревья, могут содержать измененные файлы и директории. Каждый коммит ссылается на предыдущий, кроме первого, его ссылка является null.

Хеш код коммита - это результат хеш- функции sha1, возвращает 40 цифр в 16-ричной системе счисления. Первые 2 цифры - название директории, остальные 38 - название файла.

TREE - содержат имена файлов и названия директорий в которых они хранятся, при коммите (пути); ссылаются на блобы;

Название файла и контент файла хранятся отдельно.

BLOB - binary large object - минимальная атомарная ячейка хранения информации. Хранит слепки файла.

При вызове функции sha1 git проходит по всему контенту файла и хеширует контент в блобы, присваивая им хеш- код -> формируется дерево -> формируется коммит.

### Файл .gitignore

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/IMG_4096.jpeg)

Файл .gitignore - скрытый, используется для исключения определённых файлов и директорий из отслеживания в Git, что позволяет избежать коммита временных, временных или конфиденциальных данных.

Синтаксис:
 `*.log` - отсортировать файлы по определенному расширению (в примере расширение .log) и скрыть от гит

`!errors.log` - сделать исключение для файла errors.log

`/DIR` - скрыть директорию

`build/` - скрыть все файлы директории

Для скрытия файлов нужно вписать имя файла в файла .gitignore

### Источники

1. Шпаргалка по Git от GitHub https://training.github.com/downloads/ru/github-git-cheat-sheet/
2. Version Control with Git https://learn.epam.com/catalog/detailsPage?id=601f195a-d408-4439-a16d-0630ed2a412e
3. Гайд по rebase https://eternalrival.notion.site/Rebase-tutorial-694c542f037a49b8ac5dc472defb25ea
