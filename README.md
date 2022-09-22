# Debian configurations guide
Mainly will focus on Pop OS distro since curretly trying to setup that distro.

# Recommended Package to Install
```bash
   sudo apt-get install -y \
   byobu git \
   flameshot \
   gnome-tweaks gnome-shell-extensions chrome-gnome-shell
   google-chrome-stable \
   virt-manager qemu
```

Add user to libvirt group.
```bash
sudo usermod -G libvirt -a $USER
```

<!-- TODO: explore https://github.com/pop-os/touchegg#installation -->
Gnome extensions urls
```bash
```

# Setup App Configuration
Clone dotfiles repo at https://github.com/farhanmustar/dotfiles.git.
Follow the dotfiles readme.

# Fingerprint Reader Configuration
<!-- source from https://rcarrillo.dev/enable-fingerprint-scanner-on-pop-os-21-10/ -->
Install required apps
```bash
sudo apt-get install fprintd libpam-fprintd
```
Enroll the finger.
```bash
fprintd-enroll
```
update PAM to use fingerprint scanner. (press space to toggle checkbox)
```bash
sudo pam-auth-update
```

# Wezterm terminal
Download deb file, find other version [here](https://wezfurlong.org/wezterm/install/linux.html) .
```bash
wget https://github.com/wez/wezterm/releases/download/20220905-102802-7d4b8249/wezterm-20220905-102802-7d4b8249.Ubuntu22.04.deb
```
Install the deb.
```bash
sudo apt install -y ./<path_to_deb_file>
```

# Zenmap for ip scanner
Currenlty dont have easy way to install from terminal.
Use popshop to install. search zenmap.

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
Virtual machine manager bridge configurations can be change by
running the following command.
```bash
virsh net-edit default
```

## SSH Key and SSH Agent

Gen rsa key. Public key will be placed together with suffix .pub.
```bash
ssh-keygen -t rsa
```

Add key to agent. (-t timeout)
```bash
ssh-agent -t 3600 <path_to_key>
```

## SSH Client
Use `-A` to forward ssh ageant to remote connection.
```bash
ssh -A user@remoteurl
```
