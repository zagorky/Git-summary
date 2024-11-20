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

`git config --global init.defaultbranch имяОсновнойВетки` - настроить имя основной ветки по умолчанию вместо master/main

`git config -l --global` - проверить изменилось ли имя главной ветки, `init.defaultbranch` === `имяОсновнойВетки`, например: `init.defaultbranch=main-or-whatever-you-want`

Про изменение имени ветки на гитхаб более подробно можно прочитать [здесь](https://docs.github.com/ru/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-user-account-settings/managing-the-default-branch-name-for-your-repositories)

### Создание репозитория

`git init` - инициализация репозитория, используется для создания нового локального репозитория в текущей директории; если репозиторий уже был создан ранее - реинициализирует его

`git clone url-репозитория` - клонирование удаленного репозитория на компьютер и создает локальную копию с историей всех коммитов; в локальном репозитории создается папка с таким же именем, как в удаленном

`git clone url-репозитория имяПроекта` - отличается от предыдущей команды тем, что можно установить любое нужное имя проекта, латинскими буквами

`git clone url-репозитория .` - клонирует удаленный репозиторий в папку, из которой вызвана команда

`master` — это основная ветка в локальном репозитории, а `origin/main` — это версия основной ветки на удалённом репозитории (обычно именуемом `origin`).

Имя названия основной ветки можно сменить, подробнее в блоке про [Ветки](#Ветки)

### Внесение изменений

`git status ` -выводит все изменения в файлах, которые еще не были индексации (новые файлы и новые изменения в отслеживаемых файлах); показывает состояние файлов в рабочей директории и в области индексации (staging area), указывая, какие файлы были изменены, добавлены или подготовлены для коммита.

`git log` - отображает историю коммитов текущей ветки, включая информацию о каждом коммите, такую как автор, дата и сообщение коммита.

`git diff` -выводит различия по текущим изменениям в непроиндексированных файлах

`git add имяФайла` - добавляет файл в индекс и позволяет начинать их отслеживать

`git add .` - добавляет все файлы в индекс из папки в которой ты находишься, включая подкаталоги

`git add -A` - добавляет все изменения в индекс из всего текущего репозитория, независимо в какой директории вы находитесь

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

#### Отменить изменения в файловой системе

`git checkout --имяФайла` - отменяет изменения в выбранном файле, которые еще не проиндексированы, то есть до выполнения команды `git add`.

`git checkout .` - отменяет изменения во всех неиндексированных файлах.

! Вернуть контент после `checkout` - невозможно.
! Не работает для новых файлов, которые еще не отслеживались гитом, так как у них нет предыдущей версии.

`git checkout хеш-коммита` - позволяет перемещать указатель текущей ветки на указанный коммит без изменения файлов в рабочей директории.

`git clean -xdf` - удаляет новые файлы, которые еще не отслеживались гитом, из рабочей локальной области.

Флаг `x` - игнорирование правил гита и файла .gitignore.
Флаг `d` - удаление файлов вместе с директориями.
Флаг `f` -  принудительное удаление.

! Просто команда `git clean` ничего не удалит, только с флагом `f` (force) , так как в гите есть правило ничего не удалять без этого флага.
! Вернуть файлы после `git clean -xdf`- невозможно.

#### Отменить изменения после добавления в индекс

`git reset HEAD имяФайла` - удаляет файл из индекса.

То же самое можно сделать в GIT GUI, кликнув на иконку файла в `staged area` и он переместится в `unstaged area`.

После удаления из индекса можно воспользоваться `git checkout` и тд.

#### Отменить изменения в коммите

##### Если контент в коммите - ценный.

`git commit --amend -m “сообщение”` -  обновить предыдущий коммит, можно изменить сообщение последнего коммита и/или контент, работает до отправки коммита в удаленный репозиторий; можно использовать эту команду без `-m “сообщение”`

`git commit --amend --no-edit` позволяет внести изменения в коммит без изменения его сообщения.

##### Если контент в коммите - не ценный.

`git reset HEAD^^ или HEAD~2` - убирает из истории нужное число последних коммитов, работает до отправили коммита в удаленный репозиторий.
^^ или ~2 - означает насколько коммитов назад нужно вернуться.

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/IMG_4094.jpeg)

`git reset хеш-коммита или указатель HEAD` - отменяет все коммиты после выбранного, оставляя все изменения в рабочей директории.

По умолчанию `git reset` используется с флагом `—-mixed` - перебрасывает контент из коммита в рабочую директорию, минуя индекс.

`git reset —-soft хеш-коммита или указатель HEAD` - удаляет контент из коммита и перемещает в индекс; перемещает указатель, но сохраняет изменения в области индексации (staging area).

`git reset —-hard хеш-коммита или указатель HEAD`.
Сбрасывает все изменения и состояние рабочей директории до выбранного коммита, удаляет контент внутри коммитов, далее восстановить контент невозможно.

Если контент нужно удалить навсегда.

`git filter-branch --tree-filter 'rm -f имяФайла' HEAD` - проходит по ветке и удаляет из всех коммитов определенный файл безвозвратно.

#### Отменить изменения в удаленном репозитории

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/IMG_4095.jpeg)

`git revert хеш-коммита` - создает новый коммит, который создает обратные изменения тому коммита, который мы хотим удалить. По умолчанию сообщение коммита будет `revert “сообщение удаляемого коммита”`.

Открывается редактор vim. Для того, чтобы отредактировать сообщение - нажать `insert`. Для выхода из режима редактирования нажать `escape`.
Сохранить изменения `:wq`. Записывает изменения на диск. Выйти не записывая изменения `:q!`.

Можно сделать `revert` на `revert-коммит`, так как это такой же коммит, но с зеркальным контентом.

Не удаляет коммит из истории, а создает новый коммит с обратными изменениями.

### Ветки

Размер файла, представляющего ветку в Git составляет 41 байт.

`git checkout -b 'названиеНовойВетки'` - создает новую ветку и переключает на нее.

`git checkout имяВетки ` - переключение на указанную ветку.

`git branch` - выводит список локальных веток.

`git branch --all` - выводит список всех (локальных и удаленных) веток.

`git branch имяВетки` - создают новую ветку, не переключаясь на нее.

`git switch -c имяВетки` - создает и переключает на новую ветку и обновляет рабочую директорию. (аналог git checkout -b имяВетки)

`git branch -d имяВетки` - удаляет выбранную ветку; работает с локальными ветками (только если они слиты с другими или не содержит уникальных изменений).

`git branch -D имяВетки` - принудительно удаляет выбранную локальную ветку, даже если она не была слита и содержит уникальные изменения. Может привести к потере данных

#### Изменение имени ветки

`git branch -m имяОсновнойВетки` - позволяет изменить имя основной ветки.
Если необходимо глобально изменять имя главной ветки всегда, это можно сделать в настройках конфигурации. Подробнее в блоке [Настройки](#настройки)

### Слияние веток

`Fast-forward Merge` - перемещение указателя HEAD на последний коммит другой ветки, если в текущей ветве нет изменений после точки расхождения.

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103152948.png)

`Non Fast-forward Merge` - создает дополнительный коммит слияния, который собирает в себе изменения из двух веток, на который переносится указатель HEAD.

Открывается vim для и предлагает отредактировать автоматически сгенерированный текст `merge branch 'имя ветки'` результирующего коммита.

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103152908.png)

`HEAD` - указатель на текущую ветку, указывает на последний коммит в текущей ветке; если веток несколько, HEAD указывает на коммит в активной ветке; при слиянии можно перемещать HEAD на новый коммит слияния.

`git merge имяВетки` - вносит изменения из указанной ветки в текущую (Fast-forward Merge), присоединяет коммиты из указанной ветки в текущую и сдвигает указатель HEAD на последний коммит.

`git merge удаленныйРепозиторий или имяВетки` - вносит изменения из удаленного репозитория в локальный, перед этой командой нужно делать git fetch.

`git merge --abort` - прервать слияние и вернуть все как было (при наличии конфликтов).

Когда выполняется `git merge` без конфликтов и без возвомжности fast-forward слияния, изменения из указанной ветки объединяются с текущей веткой, создавая новый коммит слияния (merge commit), который сохраняет всю историю изменений.

### Синхронизация с удаленным репозиторием

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103165017.png)

`git fetch удаленныйРепозиторий` - скачивает всю историю с удаленного репозитория (синхронизирует два репозитория, но не вносит изменения в файловую систему, для внесения изменений git merge)

`git push удаленныйРепозиторий или имяВетки` - загружает данные из локальной ветки в удаленный репозиторий; отправляет данные в удаленный репозиторий.

`git push -u origin имяВетки` - команда `git push -u origin my-branch` устанавливает `имяВетки` как отслеживаемую ветку для удалённой ветки `origin/имяВетки`; после этого, при использовании `git push` без дополнительных параметров, Git будет знать, какую ветку нужно обновлять.

`git pull` - загружает историю из удаленного репозитория и объединяет ее с локальной
(pull = fetch + merge, но можно настроить на rebase, вместо merge).

`git remote add origin url-удаленногоРепозитория` - добавление удаленного репозитория.

`git push --set-upstream origin master` - отправить текущую ветку в удаленный репозиторий и устанавливает ее как отслеживаемую.

`git remote -v` - отображает URLs удалённых репозиториев и указывает используемый протокол (например, HTTPS или SSH)

`git remote remove origin` - удаление ссылки на удаленный репозиторий из конфигурации Git.

При потере старого репозитория: для замены или восстановления удаленного репозитория.
`git remote -v` - проверить текущие удаленные репозитории
`git remote remove origin` - удалить ссылку на старый репозиторий.
`git remote add url-удаленногоРепозитория` - добавить новый удаленный репозиторий.
`git push --set-upstream origin master` - установить новый репозиторий как отслеживаемый и отправить данные.

### REBASE

Подробный гайд по этой команде https://eternalrival.notion.site/Rebase-tutorial-694c542f037a49b8ac5dc472defb25ea

Rebase - изменение базы коммита; подтягивает изменения, внесенные в одной ветке в другую, синхронизируя их, создавая линейную историю разработки; рекомендуется делать на небольших ветках, но не в master/origin ветке, так как это может помешать при совместной разработке.
![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103155957.png)
![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103160046.png)

`git rebase -i` (интерактивный rebase) позволяет управлять историей коммитов, в том числе изменять, удалять и объединять коммиты. Открывается редактор для выбора что нужно сделать с указанным коммитом.

При выполнении git rebase без конфликтов история текущей ветки переписывается, начиная с коммита, на который происходит слияние, и до текущего состояния ветки; это накладывает изменения текущей ветки поверх изменений целевой ветки, создавая линейную историю; если возникают конфликты, их необходимо разрешить вручную.

Rebase построен на совокупности cherry-pick'ов - он использует cherry-pick для последовательного применения коммитов из текущей ветки к целевой.

`cherry-pick ` - это команда для копирования коммита из одной ветки в другую. При этом создаётся новый коммит, который содержит те же изменения, что и оригинальный, но с новым хешом; конфликты могут возникать, если изменения из переноса конфликтуют с текущим состоянием ветки.

### Сохранение данных при переключении веток

#### Переключение веток через временный коммит

Порядок действий:
`git add -A` - добавляем все в индекс
`git commit -m "имяВременногоКоммита"` - создаем коммит
`git checkout имяВетки` - переключаемся на другую ветку / возвращаемся в изначальную
`git reset HEAD~1 --soft` - отменяем последний коммит с сохранением файлов в директории
Продолжаем работу
`git add -A` - снова добавляем всей файлы в индекс, после завершения работы
`git commit -m "имяИтоговогоКоммита" --amend` - изменяем сообщение последнего коммита

#### Переключение веток через git stash

Порядок действий:
`git stash` - сохраняем изменения в хранилище временных изменений
`git checkout имяВетки` - переключаемся на другую ветку / возвращаемся в изначальную
`git stash pop` - возвращаем сохраненные изменения из временного хранилища и удаляем последний stash из стека

Либо, если нужно сохранить stash, вариант без удаления из стека

`git stash push -m 'имя'` - сохраняем именованные изменения в хранилище
`git checkout имяВетки` - переключаемся на другую ветку / возвращаемся в изначальную
`git stash list` - выводим список сохраненных изменений
`git show stash@{0}` - посмотреть содержимое определенного stash
`git stash apply` - возвращаем сохраненные изменения в рабочую директорию, не удаляя stash из стека

Данные решения подходят для редкого переключения между ветками; если в проекте нет кодогенерации, либо, если она быстрая;

#### Переключение между ветками через WorkTree

WorkTree - создает копию проекта, позволяет централизованно управлять репозиторием.
Подходит если:

- Если кодогенерация занимает от нескольких минут и более,
- Необходимо делать коммиты в разные ветки часто
- Регулярное переключение между ветками

Порядок действий:
`git worktree add путьКПапке имяВетки` - создаем worktree, в этой папке будет лежать копия проекта с соответствующей веткой.
`git worktree list` - посмотреть список worktree, проверить что все создано.
Работаем в этой ветке
`git add -A` - добавляем все файлы в индекс, после завершения работы
`git commit -m "имяКоммита"` - создаем коммит
Продолжаем работать
`git worktree remove путь` - удалить worktree после завершения работы

### Конфликты

Конфликт - ситуация, когда в файле на одних и тех же строках разный контент в разных ветках.
![img](https://github.com/zagorky/Git-summary/blob/main/imgs/Pasted%20image%2020241103153414.png)

###### Варианты решений:

1. Исправить конфликт вручную -> git add -> сделать коммит
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

`git revert хеш-коммита` - отменить конкретный коммит.

### Теги

Тег можно использовать вместо хеша коммита при работе с некоторыми командами(checkout, push, reset); тег указывает на определенный коммит.

`git tag имяТега` - присвоение тега текущему коммиту, если в команде не указан хеш-коммита.

`git tag -list` - выводит список всех тегов.

`git push --tags` - отправка в удаленный репозиторий все теги.

`git checkout имяТега` - переключение между тегами

### Git GUI & Git Gitk

###### Git GUI- это расширенный git bash.

`git gui&` - запуск через терминал.

Вносим изменения в какой либо файл, который отлеживается гит.

После изменения файла нажимаем `rescan`, чтобы git GUI обновил список отслеживаемых файлов и показал изменения.
Слева сверху в `unstated changes` начинает отображаться измененный файл.
Справа сверху в `modified not staged` отображаются сами изменения. Красный- удаленные данные, зеленый - новые данные.

Для коммита изменений нажимаем на ИКОНКУ файла, он переносится в `staged changes`. В поле `commit messages` пишем текст коммита. Нажимает `commit`.

###### Gitk - предназначен для просмотра истории

### Папка .git

Папка .git- является скрытой.
Внутри папки .git:
`[hooks]`- папка, хранит скрипты, выполняемые при определенных операциях Git (например, для выполнения проверок перед коммитом).
`[objects]` - папка, хранит объекты коммитов, блобы и деревья; хранит папки (директории), в них хранятся блобы, в которых хранится контент в бинарном виде.
`HEAD` - файл, ссылку на текущую ветку и последний коммит в ней.
`[refs]` - папка, хранит ветки, содержит в себе папки `heads` -> `master` -> `ссылку на последний коммит`
`index` - файл, хранит промежуточную информацию об изменениях, далее она идет в коммит

COMMIT - ссылаются на объект дерева, который хранит имена и пути файлов, а также ссылки на родительские коммиты; могут содержать измененные файлы и директории. Каждый коммит ссылается на предыдущий, кроме первого, его ссылка является null.

Хеш код коммита - это результат хеш- функции sha1, возвращает 40 цифр в 16-ричной системе счисления. Первые 2 цифры - название директории, остальные 38 - название файла.

TREE - содержат имена файлов и названия директорий в которых они хранятся, при коммите (пути); ссылаются на блобы;

Название файла и контент файла хранятся отдельно.

BLOB - binary large object - минимальная атомарная ячейка хранения информации. Хранит слепки файла и содержимое.

При вызове функции sha1 git проходит по всему контенту файла и хеширует контент в блобы, присваивая им хеш- код -> формируется дерево -> формируется коммит.

### Файл .gitignore

![img](https://github.com/zagorky/Git-summary/blob/main/imgs/IMG_4096.jpeg)

Файл .gitignore - скрытый, используется для исключения определённых файлов и директорий из отслеживания в Git, что позволяет избежать коммита временных или конфиденциальных данных.

Синтаксис:
 `*.log` - отсортировать файлы по определенному расширению (в примере расширение .log) и скрыть от гит.

`!errors.log` - сделать исключение для файла errors.log, символ ! отменяет исключение.

`/DIR` - скрыть директорию, которая находится в корне репозитория.

`build/` - скрыть все файлы внутри директории.

Для скрытия файлов нужно вписать имя файла в файла .gitignore

### Источники

1. [Шпаргалка по Git от GitHub] (https://training.github.com/downloads/ru/github-git-cheat-sheet/)
2. [Version Control with Git ](https://learn.epam.com/catalog/detailsPage?id=601f195a-d408-4439-a16d-0630ed2a412e)
3. [Гайд по rebase ](https://eternalrival.notion.site/Rebase-tutorial-694c542f037a49b8ac5dc472defb25ea)
4. [Изменение имени ветки на гитхаб] (https://docs.github.com/ru/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-user-account-settings/managing-the-default-branch-name-for-your-repositories)
5. [Git WorkTree](https://habr.com/ru/articles/826260/)
