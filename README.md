# Golang Development Environment Setting

If you need/want to have Golang development environment in Linux... \(+ vscode and delve\)

## Writer

* SJ Kim
* &lt;bus710@gmail.com&gt;

## Referenece

* [https://golang.org/doc/install](https://golang.org/doc/install)
* [https://code.visualstudio.com/docs/languages/go](https://code.visualstudio.com/docs/languages/go)
* [https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md](https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md)
* https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code
* [https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code](https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code)

## Environment

* Mint Linux 18.3 64bit \(or equivalent distro\)

## Index

* a
* b
* c

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

## Get VSCODE

https://code.visualstudio.com/

Just download the deb file and run the below command.

```
$ sudo dpkg -i code-*.deb 
$ rm code*
```

## Open the Sample in Code

To install some required vscode extensions, run below in the terminal

```
$ cd YOUR-GOLANG-PROJECT-PATH/src
$ code .
```

Then it will tell you to install vscode-go.

## Debugging

Since we already installed Delve, VSCODE might provide launch.json for its debugging mode.

## Remote Debugging

...is well explained here.

* https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code



