# Debian configurations guide
Mainly will focus on Pop OS distro since curretly trying to setup that distro.

# Recommended Package to Install
```bash
   sudo apt-get install -y \
   byobu git \
   gnome-tweaks \
   google-chrome-stable
```

# Setup App Configuration
Clone dotfiles repo at https://github.com/farhanmustar/dotfiles.git.
Follow the dotfiles readme.

# Remote Desktop Configuration (RDP)
```bash
   sudo apt-get install xrdp
   sudo adduser xrdp ssl-cert
   sudo systemctl restart xrdp
```

# Vim 8 for Older System
Older ubuntu system such as ubuntu 14.04 trusty does not have vim 8.0. Use thirdparty ppa.
```bash
  sudo add-apt-repository ppa:jonathonf/vim
  sudo apt-get update
  sudo apt-get install vim
```

# Universal Ctags
Install universal ctags. TODO: use ppa?
```bash
  git clone https://github.com/universal-ctags/ctags.git
  cd ctags
  ./autogen.sh
  ./configure --prefix=/where/you/want # defaults to /usr/local
  make
  make install # may require extra privileges depending on where to install
```

# Ripgrep
Install ripgrep. TODO: this is not supoorted in ubuntu 14.04
```bash
  sudo add-apt-repository ppa:x4121/ripgrep
  sudo apt-get update
```

<!-- TODO: migrate all to fedora -->
# Kdenlive (Fedora)
* Allow rpm fusion
```bash
  sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm  
  sudo dnf install kdenlive
```

# Virtualization
* Fedora already install qemu kvm and libvirt by default and can be managed using `gnome-boxes`.
* Use cockpit to manage using web app.
