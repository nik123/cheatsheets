# i3wm

i3wm - tiling window manager.

## Window classes

One may use window classes to set specific behaviour for applications. Window class is stored in [WM_CLASS structure](https://tronche.com/gui/x/xlib/ICC/client-to-window-manager/wm-class.html#XClassHint). Steps to get window class:
1. execute `xprop | grep WM_CLASS`.
2. Click on the window. Possible output:

```
WM_CLASS(STRING) = "gnome-terminal-server", "Gnome-terminal"
```

3. The former value is class name, the latter value is window class.

## Custom classes for GTK applications

GTK applications have `--class` property (may be not listed in `--help` output), which allows to set custom class name for new window. One may use it for better control over windows in i3wm:

```
# Run terminal with htop inside on session start.
# And move the terminal to 2nd workspace.
# But do not automatically move any other terminals to 2nd workspace.
exec "gnome-terminal --class=htop_terminal -- htop"
set $terminal_criterion class="htop_terminal"
for_window [$terminal_criterion] move container to workspace $ws2
```
