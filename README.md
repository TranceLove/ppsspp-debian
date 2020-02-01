This repository (and this README) exists to help those who are using Ubuntu (and deriatives) after 18.10 but still wants to have [ppsspp](https://www.ppsspp.org) on their desktop/laptop/handheld.

(Or alternately, those who want to have updated versions of ppsspp on their Ubuntu, since [the original PPA](https://launchpad.net/~ppsspp/+archive/ubuntu/stable) haven't updated for long)

Original code can be found at [launchpad](https://code.launchpad.net/~ppsspp/ppsspp/+git/debian).

# First thing first: this repository is not supported outside this README.

- __instructions are for `amd64` architecture only - don't ask me for builds for other architectures__. I'm using my own build with a GPD WIN 1
- don't ask me where are the pre-built packages - they don't exist, you need to build your own. You may ask your Linux friend for help though
- don't ask me why (insert name of game here) doesn't work - nobody can guarantee library upgrades after Ubuntu 18.10 will not break ppsspp. Folks at ppsspp won't help either since their focus seems to be on Android and Windows versions, so your best bet is help them to fix the problem
- don't ask me why (insert name of game here) is slow - I use only release tags for building; I don't have time, and I won't work on things I'm not familiar with
- last but not least, __no game requests__ - I don't have any game on hand. I built this just for fun

## Build Instructions

I use [Docker](https://docker.io) for building, but VMs will do too.

0. `docker run -it ubuntu:disco /bin/bash` (tried build with eoan without errors, but I don't have an Ubuntu eoan desktop, so I won't know
1. Install the dependencies required for building: `apt install git curl wget build-essential debhelper clang cmake libfreetype6-dev libglew-dev libqt5opengl5-dev libsdl2-dev libsnappy-dev libzip-dev qt5-qmake qtbase5-dev qttools5-dev-tools zlib1g-dev chrpath`
2. Clone [my own fork of ppsspp](https://github.com/TranceLove/ppsspp) (which only difference is including this repo as a git submodule) or the [official repo](https://github.com/hrydgard/ppsspp)
3. Change to source tree directory, `git submodule update --init --recursive`

If you are using the official repo, please also do this after above line:
`git clone https://github.com/TranceLove/ppsspp-debian debian && cd debian && git checkout 1.9.4 && cd ..`

4. Back to ppsspp's source tree, say `git checkout v1.9.4`. This is their latest release tag as of 1 Feb 2020
5. `dpkg-buildpackage -b -a amd64` and take a coffee break
6. If everything is OK you should have built Debian packages one level above source tree
7. Take the packages you need for installation, depending whether you want dependency with OpenGL or SDL, and whether you want debug builds.

`ppsspp-common` must be installed along. `ppsspp-qt` is a deprecated package and you won't need it - instead, use `ppsspp` (in case you need OpenGL instead of SDL).

Depending the package manager you are using you may be prompted to install additional packages - follow the instructions as necessary.

8. Enjoy!

## License

Original repository doesn't have license attached, so I think I'll follow ppsspp to use GPL 2.0 for this.
