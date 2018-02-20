# Golang Development Environment Setting

If you need/want to have Golang development environment in Linux... \(+ vscode and delve\)

## Writer

* SJ Kim
* &lt;bus710@gmail.com&gt;

## Referenece

* Golang Installation - [https://golang.org/doc/install](https://golang.org/doc/install)
* Golang and VSCODE - [https://code.visualstudio.com/docs/languages/go](https://code.visualstudio.com/docs/languages/go)
* Delve Installation - [https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md](https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md)
* Golang Debugging in VSCODE - [https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code)
* Golang Debugging in VSCODE [https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code](https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code)
* Vim-Delve - [https://github.com/sebdah/vim-delve](https://github.com/sebdah/vim-delve)
* Vim-Pathogen - [https://github.com/tpope/vim-pathogen](https://github.com/tpope/vim-pathogen)
* Vim-Tagbar - [https://github.com/majutsushi/tagbar](https://github.com/majutsushi/tagbar)
* Vim-NerdTree - [https://github.com/scrooloose/nerdtree](https://github.com/scrooloose/nerdtree)

## Environment

* Mint Linux 18.3 64bit \(or equivalent distro\)

## Index

* Get Golang
* Set Golang Environment Variables
* Set Golang Environment Variables +
* Write a sample go code
* Get Delve \(Golang Debugger\)
* Code Editing 1 - the Easy Way
  * Get VSCODE
  * Open the Sample in Code
  * Debugging
  * Remote Debugging
* Code Editing 2 - the Hard Way
  * Get Vim
  * Get Extensions
  * Debugging
  * Remote Debugging

## Get Golang

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

## Set Golang Environment Variables

Add the lines to /etc/profile

```
export PATH=$PATH:/usr/local/go/bin
export GOROOT=/usr/local/go
export PATH=$PATH:$GOROOT/bin
export GOPATH=$HOME/golang
```

And make a directory for 3rd-party packages

```
$ mkdir -p $HOME/golang/src
$ source /etc/profile
```

## Set Golang Environment Variables +

If you want to have your own go files in somewhere else other than $HOME/golang/src,

Add the line below to $HOME/.profile

```
export GOPATH=$GOPATH:YOUR-GOLANG-PROJECT-PATH
```

And make a directory for your project

```
$ mkdir -p YOUR-GOLANG-PROJECT-PATH/src
$ source $HOME/.profile
```

## Write a sample go code

Before to get a debugger and IDE, let's test if the basic setup works.

```
$ cd YOUR-GOLANG-PROJECT-PATH/src
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

After the writing is done, run it

```
go run hello.go
```

## Get Delve \(Golang Debugger\)

Delve is the best debugger for golang.

```
$ go get -u github.com/derekparker/delve/cmd/dlv
```

## Code Editing 1 - the Easy Way

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

## Code Editing 2 - the Hard Way

Cannot imagine Golang without Vim.

Neovim would be great but let's use vim here.

### Get Vim

To install Vim in Ubuntu-like system.

```
$ sudo apt install vim
```

Vim configuration can be done by having .vimrc in your home directory.

```
$ touch $HOME/.vimrc
```

Also the vimrc file requires few lines of contents.

```
 execute pathogen#infect()
 syntax on
 filetype plugin indent on
```

However, the execute line invokes error before you actually have Pathogen.

Put a double quote \("\) at the front of the execute line if the error message is too annoying.

### Get Extensions

..

### Debugging

..

### Remote Debugging

..

