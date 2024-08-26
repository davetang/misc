# README

Miscellaneous notes and tips that don't fit in any of my other repos.

## Stuff I forget

Install OpenJDK 11 on Debian/Ubuntu.

```console
sudo apt update
sudo apt install -y openjdk-11-jre
```

Change default shell to Z shell.

```console
chsh -s $(which zsh)
```

## Windows

Use `C:\Users\<UserName>\.wslconfig` to configure advanced settings options globally across all WSL 2 distributions.

```
# Settings apply across all Linux distros running on WSL 2
[wsl2]

# Limits VM memory to use no more than 4 GB, this can be set as whole numbers using GB or MB
memory=24GB
```

Restart machine (because using PowerShell to restart Ubuntu didn't work) and then memory limit should be changed accordingly.

```console
free -h
```

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
