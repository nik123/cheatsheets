# Запуск

Присоединиться к сессии tmux:

```
tmux attach-session -t nik
```

Создать новую сессию с именем nik или присоединиться к сессии если она уже существует:

```
tmux new-session -A -s nik
```

Показать доступные сессии:

```
tmux list-session
```

Убить сессию:

```
tmux kill-session -t nik
```

Команды:
- Ctrl+b d — отключиться от сессии
- Ctrl+b [ - перейти в режим скроллинга; при включении этого режима можно скроллиться вверх-вниз клавишами-стрелками.
- Ctrl+b shft+d - показать список подключенных клиентов. Полезно если хочется удалить каких-то клиентов (https://stackoverflow.com/questions/7814612/is-there-any-way-to-redraw-tmux-window-when-switching-smaller-monitor-to-bigger )

# Окна и панели (panes)

Окна:
- Ctrl+b c — создать окно
- Ctrl+b & – закрыть окно.
- Ctrl+b 0...9 — перейти в окно 0...9
- Ctrl+b p — перейти в предыдущее окно
- Ctrl+b n — перейти в следующее окно


Изменение порядка окон:
```
swap-window -s 3 -t 1
```

Панели (panes, splits)
- Ctrl+b % - vertical split
- Ctrl+b "  - horizontal split
- Ctrl+b x - kill panel
- Ctrl+b q - показать номера панелей
- Ctrl+b :kill-pane -t 2 - убить панель под номером 2
- Ctrl+b left - передвинуть курсор на панель слева
- Ctrl+b space - сменить layout панелей (с вертикального сплита на горизонтальный)
- Ctr+b { или ctrl+b } - поменять панели местами
- Ctrl+b esc-5 - сделать панели одинаковыми по высоте
- break-pane -s <panel-num> -t <window-num>: - перенести активную панель в новое окно

Изменение размеров панели - нажать “ctrl + b” потом двоеточие (как в vim) и:
- resize-pane -D (Resizes the current pane down)
- resize-pane -U (Resizes the current pane upward)
- resize-pane -L (Resizes the current pane left)
- resize-pane -R (Resizes the current pane right)
- resize-pane -D 20 (Resizes the current pane down by 20 cells)
- resize-pane -U 20 (Resizes the current pane upward by 20 cells)
- resize-pane -L 20 (Resizes the current pane left by 20 cells)
- resize-pane -R 20 (Resizes the current pane right by 20 cells)

# Копирование

## Select and copy text

Selecting and copying text in tmux:
1. Enable vi copy mode in tmux config: `set-window-option -g mode-keys vi`.
2. Enter vi copy mode: `ctrl+[`.
3. Move around with vi navigation keys.
4. Begin selection with `Space`.
5. Copy selection with `Enter`.
6. Past with `:paste-buffer` in command mode.

## vim + ssh

**Проблема:**
- Дано: Ubuntu -> gnome terminal -> ssh -> tmux -> vim
- Надо: как блок текста выделить и скопировать на локальную машину?

Решение:
1. Открываем терминал на убунте
2. Подключаемся к серверу через ssh с опцией -Y
3. Выделяем блок в VIM (V и стрелки)
4. Нажимаем последовательно " + y

**Важно:** это не будет работать, если vim собран без поддержки иксов

# Midnight commander

Сценарий: ssh connection -> tmux -> mc

В этом случае выделение файлов (shift + стрелка вниз/вверх) не работает. Как избежать:
1. Если клиент - MacOS, то работает ctrl+T
2. Если клиент - Linux, то работает Insert

# Разное

Экспортировать переменные окружения из внешней оболочки:

```
eval "$(tmux show-environment -s)"
```

