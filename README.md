# Golang Development Environment Setting

If you need/want to have Golang development environment in Linux... \(+ vscode and delve\)

## Writer

* SJ Kim
* &lt;bus710@gmail.com&gt;

## Referenece

* Golang Installation - [https://golang.org/doc/install](https://golang.org/doc/install)
* Golang and VSCODE - [https://code.visualstudio.com/docs/languages/go](https://code.visualstudio.com/docs/languages/go)
* Delve Installation - [https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md](https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md)
* Golang Debugging in VSCODE 1 - [https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code)
* Golang Debugging in VSCODE 2 - [https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code](https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code)
* Vim-Go - [https://github.com/fatih/vim-go](https://github.com/fatih/vim-go)
* Vim-Plug - [https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug) 
* Vim-YouCompleteMe - [https://github.com/Valloric/YouCompleteMe](https://github.com/Valloric/YouCompleteMe)
* Vim-Tagbar - [https://github.com/majutsushi/tagbar](https://github.com/majutsushi/tagbar)
* Vim-NerdTree - [https://github.com/scrooloose/nerdtree](https://github.com/scrooloose/nerdtree)
* Vim-Delve - [https://github.com/sebdah/vim-delve](https://github.com/sebdah/vim-delve)

## Environment

* Mint Linux 18.3 64bit \(or equivalent distro\)

---

## Index

* Basic Setup
  * Get Golang
  * Set Golang Environment Variables
  * Set Golang Environment Variables +
  * Write a sample go code
  * Get Delve \(Golang Debugger\)
* Golang and Vim
  * Get Vim
  * Get Vim Extensions
  * Debugging
  * Remote Debugging
* Golang and VSCODE
  * Get VSCODE
  * Open the Sample in Code
  * Debugging
  * Remote Debugging
* Goland
  * Get Goland
  * Get Dep
* Conclusion
* Golang and Qt
  * How to install Qt framwork
  * How to install Golang-Qt project
* Finish

---

## 1. Basic Setup

### Get Golang

```
$ sudo mkdir -p /usr/local/go

For x64

$ wget https://dl.google.com/go/go1.10.linux-amd64.tar.gz
$ sudo tar -xvf go1.10.linux-amd64.tar.gz --strip-components=1 -C /usr/local/go

For ARM64

$ wget https://dl.google.com/go/go1.10.linux-arm64.tar.gz
$ sudo tar -xvf go1.10.linux-arm64.tar.gz --strip-components=1 -C /usr/local/go
```

The download link can be different from the latest stable version.

Please check [https://golang.org/dl/](https://golang.org/dl/)

### Set Golang Environment Variables

Add the lines to $HOME/.bashrc

```
export PATH=$PATH:/usr/local/go/bin
export GOPATH=$HOME/golang
```

And make a directory for 3rd-party packages

```
$ source $HOME/.bashrc
```

### Set Golang Environment Variables +

If you want to have your own go files in somewhere else other than $HOME/golang,

Add the line below to $HOME/.bashrc

```
export GOPATH=$GOPATH:YOUR-GOLANG-WORK-SPACE 

(i.e. export GOPATH=$GOPATH:$HOME/Dropbox/01_repo/gows)
```

And make a directory for your project.

```
$ mkdir -p YOUR-GOLANG-WORK-SPACE/src
$ mkdir -p YOUR-GOLANG-WORK-SPACE/bin
```

Also apply the change of your profile.

```
$ source $HOME/.bashrc
```

### Write a sample go code

Before to get a debugger and IDE, let's test if the basic setup works.

```
$ cd YOUR-GOLANG-WORK-SPACE/src
$ mkdir hello
$ cd hello
$ touch hello.go
$ vi hello.go
```

Then write below code in the file.

```
package main

import "fmt"

func main(){
    fmt.Println("hello")
}
```

After the writing is done, run it in the terminal.

```
go run hello.go
```

### Get Delve \(Golang Debugger\)

Delve is the best debugger for Golang and this will be used with Vim and VSCODE.

```
$ cd $HOME/golang
$ go get -u github.com/derekparker/delve/cmd/dlv
```

The main command - **dlv** is probably located in $HOME/golang/bin.

If your shell cannot find 'dlv' command, you need to source /etc/profile or just re-login.

---

## 2. Golang and Vim

Cannot imagine Golang without Vim.

Neovim would be great but let's use vim here.

### Get Vim

To install Vim in Ubuntu-like system.

```
$ sudo apt install vim
```

### Get Vim Extensions

Now we need to install Vim-Plug, Vim-Go, Vim-Delve. YCM, NerdTree, and TagBar.

Let's get *Vim-Plug* first.

```
$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

Vim itself and Vim-Plug read configuration from a file - vimrc.

```
$ touch $HOME/.vimrc
```

Put few lines in the vimrc file you just made.

```
call plug#begin('~/.vim/plugged')

Plug 'fatih/vim-go', { 'do': ':GoInstallBinaries' }
Plug 'Shougo/vimshell.vim'
Plug 'Shougo/vimproc.vim', { 'do': 'make' }
Plug 'sebdah/vim-delve'
Plug 'Valloric/YouCompleteMe', { 'do': './install.py --go-completer'}
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'majutsushi/tagbar'

call plug#end()
```

Open Vim and type a command as below.

The commands will install the packages as we wrote above.

```
:PlugInstall
```

**TagBar** and **NerdTree** Shortcut.

```
nmap <C-t> :TagbarToggle<CR>
nmap <C-n> :NERDTreeToggle<CR>
```

### Debugging

There are two different kind of commands.

**One for Vim-Delve.**

In Vim, we can use "DlvAddBreakPoint", "DlvClear", "DlvDebug", and so on...

Those can be used to set break and trace points.

**One for Delve.**

In Vim you can type "DlvDebug" and then VimShell window show you **\(dlv\)** prompt.

With \(dlv\) prompt we can use "print", "restart", "continue", "next", and so on...

**Usage**

To find out the usage of Delve, please check the below links.

* [https://github.com/derekparker/delve/tree/master/Documentation/cli](https://github.com/derekparker/delve/tree/master/Documentation/cli)
* [https://blog.gopheracademy.com/advent-2015/debugging-with-delve/](https://blog.gopheracademy.com/advent-2015/debugging-with-delve/)

### Remote Debugging

Delve server in a target gives a lot of benefit though, I would use ssh client to access to the target and run debugging mode..

---

## 3. Golang and VSCODE

VSCODE provides myriad extension packages and visual debugging feature.

### Get VSCODE

[https://code.visualstudio.com/](https://code.visualstudio.com/)

Just download the deb file and run the below command.

```
$ sudo dpkg -i code-*.deb 
$ rm code*
```

### Open the Sample in VSCODE

To install some required vscode extensions, run below in the terminal

```
$ cd YOUR-GOLANG-PROJECT-PATH/src
$ code .
```

Then it will tell you to install extensions.

I recommend to install extensions such as:

* Go
* Gopkgs
* Vim

### Debugging

Since we already installed Delve, VSCODE might provide launch.json for its debugging mode.

### Remote Debugging

...is well explained here.

* [https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code)

---
## 4. Goland  
  
GoLand is JetBrain's Golang exclusive IDE. 
As we know JetBrain offers the best tech and service in that market so that I would recommend to pick this for high productivity without too much effort in dev-env setting (with $$$...)   
  
### Get Goland

It is easy enough to download and install.  
  
First, go to their websize:  
https://www.jetbrains.com/help/go/install-and-set-up-product.html
  
Next, download the **GoLand-YYYY.V.V.tar.gz** file from them and extract, then the **goland.sh** is under the bin directory.    
  
Of course you can run GoLand by calling it from your terminal.
  
...but, wait a second! Let's get Dep first.  
    
### Get Dep
  
Dep is Golang's official dependency manager.  
- Why not **go get**?, this is because we can pick a certain version of a package like NPM or PIP.  
- Also GoLand provides dep-based project management.  
  
You can install dep with below command:  
```  
# curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
```
  
### Start a new go project
  
...Sorry I am too lazy to capture all the screenshots and paste here.  
I believe you can figure it out.   
  
Just couple tips:
- Add a environment variable - GOROOT to point Golang's path in your **.bashrc** like GOPATH (export GOROOT=/usr/local/go/)
- If you want to make a Dep-based projext in GoLand, you should also point where Dep is. If you already installed it, it is **$GOPATH/bin/dep**.   

Ok, now you are really ready to start with GoLand!  
  
---

## Conclusion

We saw the simple process to have Golang SDK and development tools.

Now you are a gopher!

![](/assets/gopher3.png)
  
.  
.  
.  
  
---  
## 5. Golang and Qt

Hold On!
  
After I wrote the main part, I started working on Qt stuff.

Big thanks for *therecipe* who is the golang-qt project's maintainer.

You can find the detail about the project from below links
- https://www.ics.com/blog/getting-started-qt-and-qt-creator-linux
- https://github.com/therecipe/qt/wiki/Installation
- https://github.com/therecipe/qt/wiki/Installation-on-Linux
- https://github.com/therecipe/qt/issues/628

And I just want to write how to install the golang-qt project.

### How to install Qt framwork

First of all, install the required packages.

```
$ sudo apt-get -y install build-essential libglu1-mesa-dev libpulse-dev libglib2.0-dev
```

Then download a script from Qt.  
https://download.qt.io/official_releases/online_installers/qt-unified-linux-x64-online.run

Set the execution flag for it.
```
# chmod 744 ~/Download/qt-unified-*.run
```

Of course run it to install Qt framework but,
- pick Qt 5.10.1 since as of 06/10/2018, Qt 5.11.0 doesn't work with this package.
- install at $HOME/Qt
  
```
# cd
# ./Download/qt-unified-*.run
```
  
### How to install Golang-Qt project
  
Set up some environment variables in your *bashrc*.
  
```
export CGO_CXXFLAGS_ALLOW=".*"
export CGO_LDFLAGS_ALLOW=".*"
export CGO_CFLAGS_ALLOW=".*"

export QT_DIR=$HOME/Qt
export QT_VERSION=5.10.1
export QT_QMAKE_DIR=$HOME/Qt/5.10.1/gcc_64/bin
```

Don't forget run below command to activate the variables.
  
```
# source $HOME/.bashrc
```

Then download Golang-Qt package.

```
# go get -u -v github.com/therecipe/qt/cmd/...
```
  
Finally, install Golang-Qt
  
```
# cd 
# ./golang/bin/qtsetup
```

## Finish
I believe now you are ready to make a GUI app based on Golang and Qt.  
Have fun!
  
