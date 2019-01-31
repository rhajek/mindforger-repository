# Installation <!-- Metadata: type: Outline; tags: basics; created: 2018-03-20 16:19:07; reads: 615; read: 2018-09-23 14:46:39; revision: 615; modified: 2018-09-23 14:46:39; importance: 3/5; urgency: 3/5; -->
Install:

* [Ubuntu](#ubuntu-)
* [Debian](#debian-)
* [Fedora](#fedora-)
* [Arch Linux](#arch-linux-)
* [macOS](#macos-)
* [Windows WSL](#wsl-)

Build:

* [build on Ubuntu](#build-on-ubuntu-)
* [build on Debian](#build-on-debian-)
* [build on Fedora](#build-on-fedora-)
* [build on macOS](#build-on-macos-)
* [build on Windows Subsystem for Linux (WSL)](#build-on-wsl-)

Docker:

* [build and run container](#build-and-run-in-container-)

Tarball:

* [download tarball](https://github.com/dvorka/mindforger/releases)

> _Unfortunately links above must have trailing '-' to workaround GitHub MD to HTML rendering bug. Therefore these links are broken in Markdown editors (including MF)._
# Install a package <!-- Metadata: type: Note; created: 2018-04-24 14:32:49; reads: 39; read: 2018-09-23 13:45:38; revision: 18; modified: 2018-09-22 11:30:41; -->
Install MindForger using a package.
## Ubuntu <!-- Metadata: type: Note; created: 2018-04-23 20:47:41; reads: 52; read: 2018-05-17 09:46:57; revision: 20; modified: 2018-05-17 09:46:57; -->
Install MindForger from **PPA**.
Add [my Lauchpad hosted PPA](https://launchpad.net/~ultradvorka/+archive/ubuntu/productivity) and install MindForger:

```
# add PPA to trusted repositories
sudo add-apt-repository ppa:ultradvorka/productivity

# update sources
sudo apt update

# install MindForger
sudo apt install mindforger
```
## Debian <!-- Metadata: type: Note; created: 2018-04-25 17:04:57; reads: 33; read: 2018-09-23 14:27:25; revision: 16; modified: 2018-05-17 09:47:13; -->
Install MindForger from **PPA**.
Add [my PPA](http://www.mindforger.com/debian), trust [GPG key](http://www.mindforger.com/gpgpubkey.txt) and 
install MindForger:

```bash
# add PPA to APT sources:
sudo bash -c 'echo -e "\ndeb https://www.mindforger.com/debian stretch main" > /etc/apt/sources.list.d/mindforger.list'

# import PPA's GPG key
wget -qO - http://www.mindforger.com/gpgpubkey.txt | sudo apt-key add -

# update sources
sudo apt update

# install MindForger
sudo apt install mindforger
```

See also http://www.mindforger.com/debian/
## Fedora <!-- Metadata: type: Note; created: 2018-04-25 19:50:19; reads: 42; read: 2018-09-23 13:47:44; revision: 19; modified: 2018-05-17 09:47:19; -->
Install MindForger on Fedora (tested on FC 27):

* [download RPM](https://github.com/dvorka/mindforger/releases) from GitHub releases

Install RPM:

```
sudo dnf install mindforger-MAJOR.MINOR.REVISION.rpm
```

## Arch Linux <!-- Metadata: type: Note; created: 2018-06-12 19:47:21; reads: 18; read: 2018-09-23 14:27:27; revision: 7; modified: 2018-06-12 19:50:48; -->
Install MindForger from Arch User Repository (AUR):

* https://aur.archlinux.org/packages/mindforger/

## macOS <!-- Metadata: type: Note; created: 2018-06-12 19:47:21; reads: 18; read: 2018-06-12 19:50:48; revision: 7; modified: 2018-06-12 19:50:48; -->
Install MindForger on macOS (tested on `Sierra 10.12`):

Install Mindforger using Homebrew:
```
brew cask install mindforger
```

* [download .dmg](https://github.com/dvorka/mindforger/releases) from GitHub releases

Install `.dmg`:

* Open/mount `.dmg`
* Drag and drop/copy `mindforger` from `.dmg` to `Applications`
* Run `MindForger`

MindForger creates copy of the documentation in your home directory (`~/mindforger-repository`) and opens it as default repository.
## WSL <!-- Metadata: type: Note; created: 2018-07-11 15:40:38; reads: 22; read: 2018-07-16 17:35:23; revision: 8; modified: 2018-07-16 17:35:23; -->
Install [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (WSL) and check that you have Ubuntu 16.04 or newer:

```
lsb_release -a
  ...
  Release:        16.04
  Codename:       xenial
```
If not, then run `sudo do-release-upgrade`.

Install and start an X server for Windows like [Xming](https://sourceforge.net/projects/xming/).

---

Install MindForger from PPA. Add [my PPA](http://www.mindforger.com/debian) to Apt, trust [GPG key](http://www.mindforger.com/gpgpubkey.txt),
install MindForger and run it:

```sh
# add PPA to trusted repositories
sudo add-apt-repository ppa:ultradvorka/productivity

# update sources
sudo apt update

# install MindForger
sudo apt install mindforger

# run MindForger
DISPLAY=:0.0 mindforger
```
# Build from source code <!-- Metadata: type: Note; created: 2018-03-20 16:19:07; reads: 55; read: 2018-09-23 13:46:02; revision: 7; modified: 2018-09-22 11:30:51; -->
Build MindForger from source code.
## Build on Ubuntu <!-- Metadata: type: Note; created: 2018-03-20 16:19:07; reads: 103; read: 2018-09-23 14:27:23; revision: 44; modified: 2018-07-10 10:22:28; -->
Build MindForger on Ubuntu 16.04 or later.

Install build tools:

```sh
sudo apt-get install build-essential zlib1g-dev libqt5webkit5-dev qttools5-dev-tools qt5-default ccache
```

Get [source code](https://github.com/dvorka/mindforger):

```
# clone MindForger repository
git clone https://github.com/dvorka/mindforger.git
# update repository sub-modules
cd mindforger
git submodule init
git submodule update
```

Build dependencies:

```
# build Discount
cd deps/discount
./configure.sh
make
```

Compile and install from Git repository root directory:

```sh
qmake -r mindforger.pro
# consider speeding up compilation by increasing the number of CPU cores to use e.g. make -j8
make
sudo make install
```

Install [documentation and stencils](https://github.com/dvorka/mindforger-repository):

```
# clone MindForger documentation repository to home directory (location and directory name matters)
cd ~
git clone https://github.com/dvorka/mindforger-repository.git

# verify MindForger repository installation
ls mindforger-repository
  limbo  memory  mind  stencils
```

Run MindForger:

```
mindforger
```

## Build on Debian <!-- Metadata: type: Note; created: 2018-04-25 17:18:23; reads: 56; read: 2018-09-23 14:27:20; revision: 13; modified: 2018-06-05 08:11:36; -->
Build MindForger on Debian Stretch or later.

Install build tools:

```sh
sudo apt-get install build-essential zlib1g-dev libqt5webkit5-dev qttools5-dev-tools qt5-default ccache
```

Get [source code](https://github.com/dvorka/mindforger):

```
# clone MindForger repository
git clone https://github.com/dvorka/mindforger.git
# update repository sub-modules
git submodule init
git submodule update
```

Build dependencies:

```
# build Discount
cd deps/discount
./configure.sh
make
```

Compile and install from Git repository root directory:

```sh
qmake -r mindforger.pro
# consider speeding up compilation by increasing the number of CPU cores to use e.g. make -j8
make
sudo make install
```

Install [documentation and stencils](https://github.com/dvorka/mindforger-repository):

```
# clone MindForger documentation repository to home directory (location and directory name matters)
cd ~
git clone https://github.com/dvorka/mindforger-repository.git

# verify MindForger repository installation
ls mindforger-repository
  limbo  memory  mind  stencils
```

Run MindForger:

```
mindforger
```
## Build on Fedora <!-- Metadata: type: Note; created: 2018-04-26 09:04:14; reads: 46; read: 2018-09-23 13:47:48; revision: 13; modified: 2018-06-05 08:11:45; -->
Build MindForger on Fedora.

Install build tools:

```sh
sudo dnf install zlib-devel qt-devel qt5-devel ccache
```

Get source code:

```
# clone MindForger repository
git clone https://github.com/dvorka/mindforger.git
# update repository sub-modules                                            
git submodule init
git submodule update
```

Build dependencies:

```
# build Discount
cd deps/discount
./configure.sh
make
```

Compile and install from Git repository root directory:

```sh
qmake-qt5 -r mindforger.pro
# consider speeding up compilation by increasing the number of CPU cores to use e.g. make -j8
make
sudo make install
```

Install [documentation and stencils](https://github.com/dvorka/mindforger-repository):

```
# clone MindForger documentation repository to home directory (location and directory name matters)
cd ~
git clone https://github.com/dvorka/mindforger-repository.git

# verify MindForger repository installation
ls mindforger-repository
  limbo  memory  mind  stencils
```

Run MindForger:

```
mindforger
```
## Build on macOS <!-- Metadata: type: Note; created: 2018-06-04 21:07:57; reads: 61; read: 2018-09-23 13:47:49; revision: 49; modified: 2018-07-10 10:04:02; -->
Build MindForger on macOS Sierra 10.12+.

Open `Terminal` and install [Xcode](https://developer.apple.com/) command line tools:

```sh
xcode-select --install
```

Install [Homebrew](https://brew.sh) package manager:

```sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew doctor
```

Install build tools and dependencies:

```sh
brew install ccache qt
```

Add them to `PATH` (if they already not present):

```sh
# add newly installed deps to path
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bashr_profile
echo 'export PATH="/usr/local/opt/qt/bin:$PATH"' >> ~/.bashr_profile

# apply changes
. ~/.bash_profile
```

Get [source code](https://github.com/dvorka/mindforger):

```sh
git clone https://github.com/dvorka/mindforger.git
git submodule init
git submodule update
```

Build dependencies:

```sh
# build Discount
cd mindforger/deps/discount
./configure.sh
make
```

Compile MindForger from Git repository root directory:

```sh
qmake -r mindforger.pro
# consider adding -j parameter with the number of CPU cores to use e.g. make -j 8
make
```

Optionally install MindForger:

```
cd app && cp -rvf mindforger.app /Applications
```

Install [documentation and stencils](https://github.com/dvorka/mindforger-repository):

```
# clone MindForger documentation repository to home directory - location and directory name matters
cd ~
git clone https://github.com/dvorka/mindforger-repository.git

# verify MindForger repository installation
ls ~/mindforger-repository
  limbo  memory  mind  stencils
```

Run MindForger either as application or using command line:

```
/Applications/mindforger.app/contents/MacOS/mindforger
```

---

**IMPORTANT**: in case that there is a problem with HTML preview ~ **nothing** is shown for a note:

* **uinstall** Qt installed using brew (`brew remove qt`)
* **install** Qt from https://www.qt.io/download 
* use `qmake` from the official distribution to **build** MindForger (as described above)

Brew approach is simpler, faster and usually works - this is why it is used by default.

## Build on WSL <!-- Metadata: type: Note; created: 2018-07-10 10:20:59; reads: 24; read: 2018-09-23 14:27:18; revision: 6; modified: 2018-07-16 17:35:03; -->
Build MindForger on [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (WSL).

Install build tools:

```sh
sudo apt-get install build-essential zlib1g-dev libqt5webkit5-dev qttools5-dev-tools qt5-default ccache
```

Update `gcc` and `g++` to version 5 (at least):

```sh
# adds the the test toolchain which includes gcc-5 and g++5 
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install gcc-5 g++-5
# substitute gcc-5 for gcc and g++-5 for g++ (current version)
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 60 --slave /usr/bin/g++ g++ /usr/bin/g++-5
```

Get [source code](https://github.com/dvorka/mindforger):

```sh
# clone MindForger repository
git clone https://github.com/dvorka/mindforger.git
# update repository sub-modules
cd mindforger
git submodule init
git submodule update
```

Build dependencies:

```sh
# build Discount
cd deps/discount
./configure.sh
make
```

Compile and install from Git repository root directory:

```sh
qmake -r mindforger.pro
# consider speeding up compilation by increasing the number of CPU cores to use e.g. make -j8
make
sudo make install
```

Install [documentation and stencils](https://github.com/dvorka/mindforger-repository):

```sh
# clone MindForger documentation repository to home directory (location and directory name matters)
cd ~
git clone https://github.com/dvorka/mindforger-repository.git

# verify MindForger repository installation
ls mindforger-repository
  limbo  memory  mind  stencils
```

Run MindForger and start your XServer for Windows (e.g. [Xming](https://sourceforge.net/projects/xming/))

```sh
DISPLAY=:0.0 mindforger
```

# Docker <!-- Metadata: type: Note; created: 2018-09-23 13:45:53; reads: 14; read: 2018-09-23 13:49:01; revision: 5; modified: 2018-09-23 13:49:01; -->
Run MindForger in Docker container.
## Build and run in container <!-- Metadata: type: Note; created: 2018-09-23 13:46:37; reads: 63; read: 2018-09-23 14:46:39; revision: 59; modified: 2018-09-23 14:46:39; -->
Build [Docker](https://www.docker.com/) image and run MindForger in Docker container.

Build image:

```
mkdir mindforger

# download Dockerfile
curl https://raw.githubusercontent.com/dvorka/mindforger/master/build/docker/mindforger/Dockerfile > mindforger/Dockerfile

# build image
docker build -t mindforger:latest mindforger
```

Run container:

```
# allow access to X server (UNSECURE, but simple):
xhost +local:root

# run image
docker run -it --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" mindforger:latest mindforger

# determine and remember container ID
docker ps -l -q > ~/.mindforger.docker
```

Run MindForger by starting container:

```
# start (stopped) container
docker start $(cat ~/.mindforger.docker)
```

Check also https://github.com/dvorka/mindforger/tree/master/build/docker for handy scripts.

