# Debian configurations guide
Mainly will focus on Pop OS distro since curretly trying to setup that distro.

# Recommended Package to Install
```bash
   sudo apt-get install -y \
   byobu git \
   gnome-tweaks \
   google-chrome-stable
   virt-manager qemu
```

Add user to libvirt group.
```bash
sudo usermod -G libvirt -a $USER
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

# Notes

## Network Configuration
Configure network interface using terminal ui.
```bash
sudo nmtui
```

## SSH and SSH Agent

Gen rsa key
```bash
ssh-keygen -t rsa
```

Add key to agent. (-t timeout)
```bash
ssh-agent -t 3600 <path_to_key>
```
