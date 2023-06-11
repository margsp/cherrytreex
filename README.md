# CherryTree
A hierarchical note taking application, featuring rich text and syntax highlighting, storing data in a single XML or SQLite file.
The project home page is [giuspen.net/cherrytree](https://www.giuspen.net/cherrytree/).

## Building Cherrytree on Windows

Install MSYS2: https://www.msys2.org/ (we cover here the packages for 64 bit installation)

Launch 'MSYS2 MinGW 64-bit' terminal (there are 3 different terminals, make sure it is 64-bit otherwise it will cause issues)

Run the following command multiple times there until there are no more updates:
```sh
pacman -Syuu
```

Install required packages to build cherrytree:
```sh
# toolchain, cmake, ninja
pacman -S --needed --noconfirm mingw-w64-x86_64-toolchain mingw-w64-x86_64-cmake mingw-w64-x86_64-ninja
# gtkmm3, gtksourceviewmm3, libxml++2.6, sqlite3
pacman -S --needed --noconfirm mingw-w64-x86_64-gtkmm3 mingw-w64-x86_64-gtksourceviewmm3 mingw-w64-x86_64-libxml++2.6 mingw-w64-x86_64-sqlite3
# gspell, curl, uchardet, fribidi, fmt, spdlog
pacman -S --needed --noconfirm mingw-w64-x86_64-gspell mingw-w64-x86_64-curl mingw-w64-x86_64-uchardet mingw-w64-x86_64-fribidi mingw-w64-x86_64-fmt mingw-w64-x86_64-spdlog
# latex, dvipng, gettext, git, nano
pacman -S --needed --noconfirm mingw-w64-x86_64-texlive-core mingw-w64-x86_64-gettext git nano
```

use native windows theme
```sh
mkdir /etc/gtk-3.0
nano /etc/gtk-3.0/settings.ini
```
```ini
[Settings]
gtk-theme-name=win32
```
console settings
```sh
nano ~/.bashrc
```
```sh
CHERRYTREE_CONFIG_FOLDER="C:/Users/${USER}/AppData/Local/cherrytree"
[ -d ${CHERRYTREE_CONFIG_FOLDER} ] || mkdir -p ${CHERRYTREE_CONFIG_FOLDER}
alias l="ls -lah --color"
alias g=git
bind '"\e[A":history-search-backward'
bind '"\e[B":history-search-forward'
```

Get cherrytree source, compile and run:
```sh
git clone https://github.com/giuspen/cherrytree.git
cd cherrytree
git submodule update --init
./build.sh notests
./build/cherrytree.exe
```

Troubleshooting:
- Cannot build: make sure to start 64-bit terminal
- Cannot build: remove `cherrytree/build` folder and start `build.sh` script again
- Cannot start cherrytree: you either have to run cherrytree from the msys2 mingw64 terminal or copy and replace cherrytree in `cherrytree_0.99.X_win64_portable` folder (downloaded from the site) by the new one, so dependencies are fulfilled
