
# scrunt

**SCRUNT** - Simple Coordinated Regular Update Nexus Tool

an easy way to automate your update routine.

## what is scrunt?
1. runs your system package manager (currently supports pacman, apt, dnf, yum, and zypper)
2. runs flatpak and/or snap updates if enabled
3. checks which packages are being upgraded or installed
4. executes any matching hooks in `~/.config/scrunt/hooks/`. comes with some premade, and you can add your own.
5. ends with fastfetch if enabled

# install scrunt

### dependencies
- `dialog` (required for setup)
- `bash`, `sudo`, and a package manager

optional:
- `timeshift` or `snapper` for pre-update snapshots
- `fastfetch` to display when done

### from source

```bash
git clone https://github.com/mrwrzr/scrunt
cd scrunt
sudo cp scrunt scrunt-wizard /usr/local/bin/
scrunt
```

first run should automatically launch setup dialog.

# setting up scrunt

setup tool asks for:
1. package manager (auto-detected, confirm or override)
2. (on arch-based:) AUR helper (yay/paru supported)
3. flatpak/snap confirmation if detected
4. auto-confirm behavior: if yes, uses `--noconfirm / -y` flags by default
5. create package list and/or snapshot: optional, recommended for troubleshooting
6. fastfetch: you can choose to display it after updates finish

it comes with the option to create hooks for detected packages:
- vencord (runs the installer to re-patch after a discord update)
- nvidia drivers (rebuild initramfs)
- vmware (rebuild modules)
potentially more to come.

you can also add your own custom hooks for any other packages. they can be any command. runs in your user context unless you use `sudo` inside it.

# how to scrunt

`scrunt`
update and run hooks with your current configuration

`scrunt --huh`
show upgradable packages without taking action

`scrunt --tog`
use the opposite of your current confirmation setting for one run

`scrunt --config`
edit settings

`scrunt --help`
show list of available flags

## configuring your scrunt

| option | values | desc |
|--------|--------|-------------|
| `PM` | pacman, apt, dnf, yum, zypper | package manager |
| `AUR_HELPER` | paru, yay, (empty) | AUR helper (arch-based) |
| `FLATPAK` | true, false | update flatpak apps |
| `SNAP` | true, false | update snap packages |
| `SAVE_PACKAGE_LIST` | true,false | save list of upgraded packages |
| `CREATE_SNAPSHOT` | true,false | create system snapshot before updates |
| `CONFIRM_UPDATE` | true, false | if false, uses `--noconfirm`/`-y` |
| `FASTFETCH` | true, false | show fastfetch after updates |

## hooks

hooks are executable bash scripts in `~/.config/scrunt/hooks/` to run before or after an associated package has been updated. name each file after the package it watches.

# uninstall

```
sudo rm /usr/local/bin/scrunt /usr/local/bin/scrunt-wizard
rm -rf ~/.config/scrunt
```
# contribution

pull requests welcome and encouraged.
unsure how actively this will be maintained. just wanted to put it somewhere.

# license

gplv3

# to-do
- test on fresh systems with various distros installed
- add --version flag
- add support for nixOS and other package managers
- add premade hooks for more packages (several need service restarts to take effect, etc.)
- add pre-install option to backup specified .config files
- add pre-install scripting for updating dotfiles via git
- add support for pikaur and aurutils
