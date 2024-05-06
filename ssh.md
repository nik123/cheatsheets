# SSH

Если не знаешь что такое ssh, то тебе не нужен документ.

Other cheatsheets:
1. https://www.wagner.pp.ru/fossil/advice/doc/trunk/ssh.md

# Копирование файлов

## SCP

С сервера на клиент:

```
scp your_username@remotehost.edu:foobar.txt /some/local/directory
```

С клиента на сервер:

```
scp foobar.txt your_username@remotehost.edu:/some/remote/directory
```

Дополнительные параметры:

- `-P 11022` - указать порт.

## rsync

Cинтаксис: `rsync [-опции] src dest`, т.е. если надо скопировать с
сервера на хост, то нужно что-то типа `rsync -rv user@host:/remote/path/ /local/path/`

Опция `--exclude` позволяет игнорировать файлы и каталоги, попадающий под
указанный шаблон. Пример:

```
rsync -rv /local/path/ user@host:/remote/path/ --exclude __pycache__/ --exclude venv/ --exclude log_dir/ --exclude ".*"
```

Если ssh висит на нестандартном порту:

```
rsync -rv -e "ssh -p 11022" /local/path/ user@host:/remote/path/ --exclude __pycache__/ --exclude venv/ --exclude log_dir/ --exclude ".*"
```

Доп. опции:
- Есть опция `--delete`, которая удаляет "лишние" файлы в каталоге назначения.
- Есть опция `--progress` для отображения прогресса.

# Аутентификация по ключам

Игнорировать ключи в каталоге `~/.ssh`:

```
ssh -o IdentitiesOnly=yes -i identity_file user@host
```

Генерация ключа на локальной машине:

```
ssh-keygen -t ed25519 -C "your_email@example.com"

ssh-keygen -t rsa -b 4096 -C "your_email@example.com*"
```

Будут созданы приватный и публичный ключи. Публичный ключ надо каким-то
образом отправить на сервер.

Добавление публичного ключа **на сервере**:

```
cat id_rsa.pub >> .ssh/authorized_keys
```

## Логин из Linux

Запускаем ssh-агент и добавляем ключ:

```
eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_rsa
```

**Важно:** на убунте (16.04) сталкивался с такой проблемой, что ssh-add
приходится выполнять при каждой новой сессии терминала. Проблему можно
решить, создав `*.pub` файл в том же каталоге.

## Логин из MacOS

На MacOS есть два способа: непосредственно через ключ или добавив его в
Keychain

### Без добавления в Keychain

Команда на MacOS:

```
ssh -i /path/to/private/key user@host
```

### С сохранением в Keychain

Составлено по [инструкции Github](https://help.github.com/articles/connecting-to-github-with-ssh/)

Запустить ssh-agent в фоне:

```
eval "$(ssh-agent -s)"
```

На MacOS Sierra 10.12.2 и выше нужно изменить файл `~/.ssh/config`:

```
Host hostname
AddKeysToAgent yes
UseKeychain yes
IdentityFile ~/.ssh/id_rsa
```

Можно заходить:

```
ssh user@hostname
```

# ssh-copy-id

`ssh-copy-id` - утилита для добавления публичных ключей на remote host.

```
ssh-copy-id -f -i key.pub user@server
```

Опция `-f` нужна т.к. по умолчанию `ssh-copy-id` пытается проверить есть ли уже ключи на сервер и делает это пытаясь залогиниться. Если добавляется чужой открытый ключ, то `ssh-copy-id` залогиниться с ключами текущего пользователя и решит что ключи другого пользователя добавлять не нужно.

# SSHFS

ssfs - монтирование удаленных ФС через ssh-соединение

## На MacOS

Для установки sshfs нужно установить пакеты [osxfuse и sshfs](https://osxfuse.github.io/)

Пример команды на OS X:

```
sshfs -o defer_permissions user@host:/var/www/html /path/to/mount/dir
```

`path_to_mount_dir` - путь к каталогу для монтирования. Каталог должен
существовать.

Для демонтирования файловой системы:

```
umount -f path_to_mount_dir
```

## На Ubuntu

Монтирование:

```
sshfs user@host:/remote/dir /path/to/mount
```

Размонтирование, почему-то требует рут:

```
sudo umount -f /path/to/mount
```

# Прокси через ssh

Поднимаем свой кулхацкер-сервер и настраиваем на нем ssh

2. На локалхосте выполняем

```
ssh -D 8123 -f -C -q -N paveldurov@serverip
```

Ключ `-f` запускает процесс в фоне, поэтому мы можем спокойно закрыть
терминал после выполнения команды.

3. Проверяем, что все работает:

```
ps aux | grep ssh
```

Если все норм, то среди прочего в выводе должно быть что-то типа:

```
19787 0,0 0,0 4306952 696 ?? Ss 12:04 0:00.08 ssh -D 8123 -f -C -q -N
```

4. В настройках прокси Телеграма/Firefox указываем SOCKS5-прокси `127.0.0.1:8123`

# Проброс портов

Проброс портов с локальной машины

Допустим, у нас подключен Jupyter на внешнем сервере и все порты, кроме
22 (ssh по умолчанию), закрыты на сервере. Как подключиться к
веб-интерфейсу Jupyter, запущенному на сервере.

На **клиенте** выполняем:

```
ssh -L 9000:localhost:8888 user@host
```

После логина запускаем jupyter-notebook:

```
jupyter-notebook --no-browser
```

В логе запуска появится ссылка вида `http://localhost:8888/*`. Копируем
её, вставляем в браузер, **заменив порт 8888 на 9000**.

Если нужно пробросить сразу несколько портов:

```
ssh -L 9000:localhost:8888 -L 9001:localhost:6006 user@host
```

# Разное

Не сохранять имя в `known_hosts`:

```
ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null user@host
```

Показать все добавленные ключи:

```
$ssh-add -l
```

SSH agent forwarding via command line options:
```
ssh -A user@host
```
