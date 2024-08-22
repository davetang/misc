# README

Miscellaneous notes and tips that don't fit in any of my other repos.

## GNU screen

* [Manual](https://www.gnu.org/software/screen/manual/screen.html)
* Default config file `$HOME/.screenrc`
* The `$TERM` [environment variable](https://www.baeldung.com/linux/term-environment-variable) specifies the model of the terminal emulator. Some of the popular terminal types include `xterm`, `xterm-256color`, `vt100`, `gnome-terminal`, and `rxvt-unicode`. Each of these terminal types provides different capabilities.

Prior to starting `screen`

```console
echo $TERM
```
```
xterm-256color
```

In screen, `$TERM` is set to `screen` and syntax highlighting is missing from some tools I use.

```console
echo $TERM
```
```
screen
```

Change setting and restart `screen`.

```console
printf "export TERM=xterm-256color\n" >> $HOME/.screenrc
```

After restarting syntax highlighting is back.

```console
echo $TERM
```
```
screen.xterm-256color
```
