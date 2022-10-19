# Debian configurations guide
Mainly will focus on Pop OS distro since curretly trying to setup that distro.

# Recommended Package to Install
```bash
   sudo apt-get install -y \
   byobu git \
   flameshot \
   remmina \
   cpu-x \
   gnome-tweaks gnome-shell-extensions chrome-gnome-shell \
   network-manager-l2tp network-manager-l2tp-gnome \
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

# Setup Dotfiles
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

# Wezterm terminal
Download deb file, find other version [here](https://wezfurlong.org/wezterm/install/linux.html) .
```bash
wget https://github.com/wez/wezterm/releases/download/20220905-102802-7d4b8249/wezterm-20220905-102802-7d4b8249.Ubuntu22.04.deb
```
Install the deb.
```bash
sudo apt install -y ./<path_to_deb_file>
```

# Chrome Unstable
Chrome seems to crash alot. Now trying the flatpack version.
# TODO: confirm already the flatpack version is more stable
# TODO: add flatpack install commmand for installing flatpack pkg.

# Zenmap for ip scanner
Currenlty dont have easy way to install from terminal.
Use popshop to install. search zenmap.

# Remote Desktop Configuration (RDP server)
```bash
   sudo apt-get install xrdp
   sudo adduser xrdp ssl-cert
   sudo systemctl restart xrdp
```

# Gif Recorder
For now use peek, have not found one that is in default repo.
```bash
sudo add-apt-repository ppa:peek-developers/stable
sudo apt update
sudo apt install peek
```

# Recording and Streaming
```bash
sudo apt install obs-studio
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

# Gaming
Pop OS got two iso, one for nvdia one for others. need to install the correct one.
## Lutris
* TODO: expore this software.

# Logitech  Devices
Use solaar to configure them.
```bash
sudo apt install solaar
```

# Notes

## Network Configuration
Configure network interface using terminal ui.
```bash
sudo nmtui
```

Virtual machine manager network config can be configure at Edit > Connection Details.
Alternatively change by settings running the following command. (last two line to restart).
```bash
virsh net-edit default
virsh net-destroy default
virsh net-start default
```
virsh is cli for virtual machine config.

## SSH Key and SSH Agent
NOTE: Pop OS use seahorse to manage password and keys.
Can generate directly from seahorse.

Gen rsa key. Public key will be placed together with suffix .pub.
```bash
ssh-keygen -t rsa
```

Add key to agent. (-t timeout)
```bash
ssh-agent -t 3600 <path_to_key>
```
or
```bash
ssh-add <path_to_key>
```
Remove user added keys (not added from seahorse).
```bash
ssh-add -D
```

## SSH Client
Use `-A` to forward ssh ageant to remote connection.
```bash
ssh -A user@remoteurl
```

## Synaptic touchpad device
For synaptic touchpad we have manufacturer driver that make the touchpad more responsive.
Check device type.
```bash
xinput --list
```
Install device driver.
```bash
sudo apt install xserver-xorg-input-synaptics
```
Temp config the settings like this.
List props
```bash
xinput --list-props <deviceID/name>
```
Set prop (temp)
```bash
xinput --set-prop <deviceID/name> <propID> <val1> [<val2> ...]
```
Make it persistent refer [here](https://www.x.org/releases/X11R7.6/doc/man/man4/synaptics.4.xhtml#heading4) 
copy or modify config from `./etc/X11/xorg.conf.d/99-synaptics.conf` to `/etc/X11/xorg.conf.d/`
```bash
sudo cp ./etc/X11/xorg.conf.d/99-synaptics.conf /etc/X11/xorg.conf.d/
```
Hint:
Synaptic scrolling distance set to -ve value to invert scroll direction.

## Reject touchpad tap while typing
syndaemon can be use to reject touchpad tap when typing.
currently just use startup application.
add the following bash script to `/usr/bin/syndaemon_restart` 
```bash
#!/usr/bin/bash

killall syndaemon || true
syndaemon -i 3 -KRdt
```
Allow execution
```bash
sudo chmod +x /usr/bin/syndaemon_restart
```
Search statup application and add `/usr/bin/syndaemon_restart` .

## Touchpad Issues.
Recommended to add them as shortcut command if keep happening.
Sometimes cannot move cursor at all. Try this to recover.
```bash
echo -n rescan | sudo tee  /sys/bus/serio/devices/serio1/drvctl
```
Sometimes cannot scroll. Try this to recover.
```bash
sudo modprobe -r psmouse
sudo modprobe psmouse
```

## Windows Virtual Machine Performance Improvement
Install virtio driver [here](https://pve.proxmox.com/wiki/Windows_VirtIO_Drivers)
to improve performance.

TODO: other os might also benefit from installing virtio driver.
TODO: refer [here](https://github.com/bearlike/my-popos-setup) for setup ref.
