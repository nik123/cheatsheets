# Misc.

- `git reset --hard` - удалить все незакомиченные изменения

- `git clean -fd` - удалить все файлы, которые не находятся под версионным контролем \+ отменить все unstaged-изменения в файлах, находящихся под версионным контролем.

- `git rm --cached <file>` - удалить файл из-под версионного контроля без его удаления из файловой системы.

- `git reset --hard HEAD~1` - удалить все незакоммиченные изменения и удалить все локальные коммиты (коммиты, не запушенные в центральный репозиторий).

- `git reset --soft HEAD~1` - удалить все локальные коммиты, не затронув файлы.

- `git reset HEAD -- <file>` - убрать файл из изменений, зафиксированных для коммита (unstage file staged for commit).

- `git branch` - показать локальные ветки.

- `git branch -a` - показать локальные и удаленные ветки.

- `git add -u` - внести все unstaged удаленные файлы под версионный контроль (в этом случае нет необходимости повторять команду `git rm filename` для каждого удаленного файла).

- `git log --abbrev-commit` - показывать не полный хэш коммита, а только префикс.

- `git init` - создать репозиторий, в котором можно работать (создавать и изменять файлы).

- `git init --bare` - создать репозиторий без рабочего каталога, то есть в такой репозиторий можно пушить, но в нем нельзя создавать или обновлять файлы.

- `git branch -a` - перечислить все ветки.

- `git rev-parse --show-toplevel` - получить корень репозитория.

# Работа с remote

`git remote show origin` - Информация о remote-репозитории.

`git remote set-url origin [https://github.com/username/repo](https://github.com/username/repo)` - Выставить новый URL для origin-репозитория.

`git remote -v` - Показать список remote-репозиториев.

`git remote add upstream https://github.com/iterative/dvc.org` - Добавить новый remote

# Branches

## Renaming

```sh
# Rename branch locally
git branch -m old_branch new_branch 

# Delete the old branch
git push origin old_branch 

# Push the new branch, set local branch to track the new remote
git push --set-upstream origin new_branch
```

## Deleting

Удалить только ветку в `origin` и оставить локальную ветку нетронутой:

```bash
git push origin --delete BranchToDeleteInRemote
```

Возможны варнинги типа `Your branch is based on 'origin/Chats', but the upstream is gone` - в этом случае нужно переключиться на BranchToDeleteInRemote и выполнить команду `git branch --unset-upstream`

Чтобы удалить ветку локально нужно выполнить команду:

```bash
git branch -d branch-name
```

### Deleting branch which is deleted in remote

Если я локально отслеживаю какую-то ветку и она была удалена в remote, при выполнении команды git remote show origin я увижу что-то такое:

```
refs/remotes/origin/AnimationOnDisappear  stale (use 'git remote prune' to remove)
```

Чтобы увидеть все подобные ветки, нужно выполнить:

```bash
git remote prune origin --dry-run
```

Чтобы удалить все подобные ветки, нужно выполнить:

```bash
git remote prune origin
```

Более простой способ:

```bash
git fetch --prune

# same but shorter:
git fetch -p
```

# Отмена коммитов

Изменение сообщения последнего локального коммита:

```
git commit --amend -m "New commit message"
```

Отмена локального коммита:

```sh
git reset HEAD~1
```

В remote-репозитории:

```sh
git reset HEAD^ --hard
git push <repository_address> -f
```

# Сплющивание коммитов

Сплющить 4 коммита в один:

```sh
git rebase -i HEAD~4
```

Опция `-i` - это сокращение от “interactive”. Откроется текстовый редактор со списком коммитов (последний коммит будет внизу). Пример:

```
pick fda59df commit 1
pick x536897 commit 2
pick c01a668 commit 3
```

Чтобы удалить последние два коммита, нужно выполнить:

```
pick fda59df commit 1
squash x536897 commit 2
squash c01a668 commit 3
```

# Отслеживание изменений только одного из подкаталогов репозитория

```sh
git init repo
cd repo
git remote add -f origin url
```

This creates an empty repository with your remote. Then do:

```sh
git config core.sparsecheckout true
```

Now you need to define which files/folders you want to actually check out. This is done by listing them in .git/info/sparse-checkout, eg:

```sh
echo "some/dir/" >> .git/info/sparse-checkout
echo "another/sub/tree" >> .git/info/sparse-checkout
```

Last but not least, update your empty repo with the state from the remote:

```sh
git pull origin master
```

ВАЖНО: В дальнейшем изменения из удаленного репозитория нужно получать не через git pull а через git pull origin master

# Порождение новой ветки из незакоммиченных изменений

Иногда есть какие-то незакоммиченные изменения, которые желательно закоммитить в новую ветку.

```sh
git stash

git stash branch <branchname>
```

# Получение отсутствующей локально remote-ветки

Допустим, в origin-репозитории появилась новая ветка new_branch и нам необходимо получить ее.

```sh
git fetch origin

git checkout --track origin/new_branch

# Альтернатива второй команды:
git checkout -b new_branch origin/new_branch
```

Первая команда необходима для получения списка удаленных веток. ВАЖНО: при выполнении команды `git fetch` ветки появляются локально, но не выводятся командой `git branch` - такие ветки называются неотслеживаемыми. Чтобы переключиться на новую ветку нужно выполнить вторую команду из списка выше. Если при выполнении команды мы в ветке `my_branch` и в этой ветке есть несколько незапушенных в `origin/my_branch` коммитов, они не попадут в новую ветку new_branch.

# Игнорирование файлов

Допустим, мы хотим игнорировать каталог bin. Чтобы игнорировать все каталоги bin в любом подкаталоге, включая текущий, нужно добавить в gitignore:

```
bin/
```

Иногда бывает, что ныне игнорируемый файл уже находится под git-контролем. Если мы хотим убрать файл, то делаем так:

```sh
git rm -r --cached bin
```

Установить путь к глобальному gitignore-файлу:

```
git config --global core.excludesfile ~/.gitignore_global
```

## Глобальный gitignore

Путь к глобальному gitignore:
```
git config --global core.excludesfile
```

Если ничего не было выведено на экран, значит глобальный gitignore-файл не настроен.

Настроить путь к глобальному gitignore:
```sh
git config --global core.excludesfile '~/.gitignore'
```

# Tags

Самый элементарный способ создания метки:

```sh
git tag <tagname>
```

Команда выше создаст легковесную метку. Кроме того можно создать аннотированную ветку. Подробнее см [в Git Book](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

Протолкнуть ветку в origin можно так:

```sh
git push origin tagname
```

Скачать определенный тэг-коммит:

```sh
git checkout tags tagname
```

# Кириллические имена файлов

У нас в репозитории иногда проскальзывают файлы с русскими именами. В командах git могут показываться неправильно. Например git status может выдать:

```
"\\320\\242\\320\\240\\320\\232211.01.02.00.000.\\320\\241\\320\\221 \\320\\234\\320\\232.doc"

"\\320\\242\\320\\240\\320\\232211.01.02.00.000.\\320\\241\\320\\221 \\320\\234\\320\\232Update.doc"
```

Можно поправить командой `git config --global core.quotepath false`

# Submodules

## Клонирование проекта с подмодулями

Простой способ:

```sh
git clone --recurse-submodules https://github.com/chaconinc/MainProject
```

Если в деталях:

```sh
git clone https://github.com/chaconinc/MainProject

cd MainProject

# Let’s assume that submodule is ‘DbConnector’

cd DbConnector/

git submodule init

git submodule update
```

## Delete submodules

Процесс:

1.  Delete the relevant section from the .gitmodules file.

2.  Stage the .gitmodules changes: git add .gitmodules

3.  Delete the relevant section from .git/config.

4.  Run git rm --cached path\_to\_submodule (no trailing slash).

5.  Run rm -rf .git/modules/path\_to\_submodule (no trailing slash).

6.  Commit git commit -m "Removed submodule"

7.  Delete the now untracked submodule files rm -rf path\_to\_submodule


## Переход на ветку без сабмодуля

Сценарий:
1.  Был на `master`
2.  Создал ветку `feature_branch` и переключился на нее
3.  Добавил в новой ветке сабмодуль `my_submodule`
4.  Переключился обратно на master

В результате git status покажет что-то типа такого:

```sh
On branch master

Untracked files:

  (use "git add <file>..." to include in what will be committed)

    my_submodule/

nothing added to commit but untracked files present (use "git add" to track)
```

Как избавиться от этой ошибки? Можно просто удалить каталог:

```sh
rm -rf my_submodule
```
