# Ubuntu configuration guide

Older ubuntu system such as ubuntu 14.04 trusty does not have vim 8.0. Use thirdparty ppa.
```bash
  sudo add-apt-repository ppa:jonathonf/vim
  sudo apt-get update
  sudo apt-get install vim
```

Install universal ctags. TODO: use ppa?
```bash
  git clone https://github.com/universal-ctags/ctags.git
  cd ctags
  ./autogen.sh
  ./configure --prefix=/where/you/want # defaults to /usr/local
  make
  make install # may require extra privileges depending on where to install
```

Install ripgrep. TODO: this is not supoorted in ubuntu 14.04
```bash
  sudo add-apt-repository ppa:x4121/ripgrep
  sudo apt-get update
```
