# findxap

Findxap searches or run an application in a specified virtual desktop.

Example:

Run firefox on the second virtual desktop ( The vd numeration starts at 0 )

`findapp 1 firefox`

## Requirements

Findxap uses the X Windows Manager to list and deal with applications. It is usually in
the *wmctrl* package.

### Debian, Ubuntu and derivatives

`sudo apt-get install wmctrl`

### Other Distributions

There should be a package called *wmctrl* in your distribution. Feedback welcome.

## Download

You must download the source using git:

`git clone https://github.com/frankiejol/findxap`

## Installation

The file findxap should be installed in one of the bin directories of your system
Typing this in the source directory will put it in */usr/local/bin/*:

`cd findxap
sudo make`

## Usage

### Command

findxap -d desktop -n program argument1 argument2 ...

- -d X : Desktop number. Desktop where the program is sent
- -n : Don't go to the desktop (optional, default = yes )

Examples:

Find application audacity

`$ findxap audacity`

Send firefox to desktop 1

`$ findxap -d 1 firefox`

Send thunderbird to desktop 3 but don't follow it

`$ findxap -d 3 -n thunderbird`

### Hotkeys

You can define hotkeys so the applications are sent to the desired virtual desktop.

This is an example for Gnome-shell tested on Ubuntu. It configures Firefox and Thunderbird:

- <Super>F : Runs Firefox on Desktop 1
- <Super>U : Runs Thunderbir on Desktop 2

`$ dconf load /org/gnome/ <<EOC
[settings-daemon/plugins/media-keys]
custom-keybindings=['/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom0/', '/org/gnome/settings-daemon/plugins/media-keys/custom-keybindings/custom1/']


[settings-daemon/plugins/media-keys/custom-keybindings/custom1]
binding='<Super>u'
command='findxap -d 2 -n thunderbird'
name='thunderbird'

[settings-daemon/plugins/media-keys/custom-keybindings/custom0]
binding='<Super>f'
command='findxap -d 1 firefox'
name='firefox'

EOC

