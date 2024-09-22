## Table of Contents

- [README](#readme)
  - [Sysadmin](#sysadmin)
  - [Stuff I forget](#stuff-i-forget)
  - [Mullvad Browser](#mullvad-browser)
  - [Windows](#windows)
  - [Zsh](#zsh)
  - [GNU screen](#gnu-screen)
  - [Useful software](#useful-software)
  - [Tips](#tips)
    - [Shell history](#shell-history)
    - [Command not found](#command-not-found)
    - [SSH config](#ssh-config)

# README

Miscellaneous notes and tips that don't fit in any of my other repos.

## Sysadmin

Force reboot on a degraded system.

```console
systemctl reboot
```
```
Call to Reboot failed: Connection timed out
Failed to start reboot.target: Connection timed out
See system logs and 'systemctl status reboot.target' for details.
It is possible to perform action directly, see discussion of --force --force in man:systemctl(1).
```

```console
systemctl status reboot.target
```
```
Failed to get properties: Connection timed out
```

Use double force!

```console
systemctl --force --force reboot
```
```
Rebooting.
```

## Stuff I forget

Mount CDROM; look for `/dev/sr0`.

```console
sudo blkid
sudo mount /dev/sr0 /media/cdrom
```

Unmount and eject.

```console
sudo umount /media/cdrom/
eject
```

Install OpenJDK 11 on Debian/Ubuntu.

```console
sudo apt update
sudo apt install -y openjdk-11-jre
```

Change default shell to Z shell.

```console
chsh -s $(which zsh)
```

## Mullvad Browser

[Disable letterboxing](https://github.com/mullvad/mullvad-browser/issues/152#issuecomment-1944569635):

Enter `about:config` into address bar and edit `privacy.resistFingerprinting.letterboxing`.

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

## Zsh

[Alt + left/right arrow key](https://stackoverflow.com/questions/12382499/looking-for-altleftarrowkey-solution-in-zsh) results in D and C characters. Put the following in `~/.zshrc`:

```
bindkey "^[[1;3C" forward-word
bindkey "^[[1;3D" backward-word
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

## Useful software

*  [Karabiner-Elements](https://github.com/pqrs-org/Karabiner-Elements) is a powerful utility for keyboard customisation on macOS Sierra (10.12) or later. Use it to remap keys and more!

## Tips

### Shell history

If you type `history` you will get the history of commands that was run. If you want to re-run a particular history entry:

```console
!8318
```

Another nice way, is to use Ctrl + R. Press the two keys once and then start typing; use Ctrl + R to cycle through the possible matches.

### Command not found

The `command-not-found` utility is useful for making suggestions when a command is not found. To use it install it and then run update to populate the database.

```console
sudo apt update
sudo apt install -y command-not-found
sudo apt update
ls /var/lib/command-not-found
```
```
commands.db  commands.db.metadata
```

If you are using the Z shell, [add the following](https://unix.stackexchange.com/a/65506) to `~/.zshrc`.

```
[ -f /etc/zsh_command_not_found ] && . /etc/zsh_command_not_found
```

Source `~/.zshrc` and voila!

```console
. ~/.zshrc
pipp
```
```
Command 'pipp' not found, did you mean:
  command 'pcpp' from deb pcc
  command 'pspp' from deb pspp
  command 'pip' from deb python3-pip
  command 'pipx' from deb pipx
  command 'sipp' from deb sip-tester
  command 'pgpp' from deb python3-pglast
  command 'pip3' from deb python3-pip
Try: sudo apt install <deb name>
```

### SSH config

Use a config file if you SSH into a lot of different machines!

```
Host some_alias
 HostName IP or URL
 User username
 IdentityFile private_key
 ServerAliveInterval 240
 Port port_number
```

Then just `ssh some_alias`!
