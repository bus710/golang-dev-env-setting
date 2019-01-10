# Golang Development Environment Setting

If you need/want to have Golang development environment in Linux... \(+ vscode and delve\)

## Writer

* SJ Kim - <bus710@gmail.com>

## Referenece

* Golang Installation - [https://golang.org/doc/install](https://golang.org/doc/install)
* Go modules - [https://github.com/golang/go/wiki/Modules#quick-start](https://github.com/golang/go/wiki/Modules#quick-start)
* Delve Installation - [https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md](https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md)
* Golang and VSCODE - [https://code.visualstudio.com/docs/languages/go](https://code.visualstudio.com/docs/languages/go)
* Golang Debugging in VSCODE 1 - [https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code)
* Golang Debugging in VSCODE 2 - [https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code](https://stackoverflow.com/questions/39058823/how-to-use-delve-debugger-in-visual-studio-code)

## Environment

* Mint Linux 19.1 - 64bit \(or equivalent distro\)

---

## Index

* Basic Setup
  * Get Golang
  * Set Golang Environment Variables
  * Write a Sample Go Code
  * Get Delve \(Golang Debugger\)
* Golang and VSCODE
  * Get VSCODE
  * Open the Sample in Code
  * Config for Debugging
* Conclusion

---

## 1. Basic Setup

### Get Golang

As of Jan 10, 2019, Go 1.12 is beta 1.  
However, 1.12 is being expected to be official at the of the month.  
I will update this document as it is confirmed.
  
Anyway, make a directory for the go binary first.
  
```
$ sudo mkdir -p /usr/local/go
```

And download/extract the binaries as below.

- The download link in the instruction can be different as time goes.  
- If the link doesn't work, please check [https://golang.org/dl/](https://golang.org/dl/)
```
For x64

$ wget https://dl.google.com/go/go1.12beta1.linux-amd64.tar.gz
$ sudo tar -xvf go1.12beta1.linux-amd64.tar.gz --strip-components=1 -C /usr/local/go

For ARM64

$ wget https://dl.google.com/go/go1.12beta1.linux-arm64.tar.gz
$ sudo tar -xvf go1.12beta1.linux-arm64.tar.gz --strip-components=1 -C /usr/local/go
```

This is it! No need to compile at all but some system variables are required.


### Set Golang Environment Variables

To let your system know where the binaries we just installed as long as a debugger's image, we need to add the path of the binaries to PATH variable.  
Also, 3rd-party packages' location needs to be specified as GOPATH.

Add the lines to **$HOME/.bashrc**

```
export PATH=$PATH:/usr/local/go/bin:$HOME/golang/bin
export GOPATH=$HOME/golang
```

Make a directory for 3rd-party packages and update the system variables.

```
$ mkdir $HOME/golang
$ source $HOME/.bashrc
```

### Write a go sample code

Before to get a debugger and IDE, let's test if the basic setup works.

```
$ cd $HOME
$ mkdir hello
$ cd hello
$ go mod init hello
$ touch main.go
$ vi main.go
```

Then write below code in the file.

```
package main

import (
    "fmt"
    "rsc.io/quote"
)

func main() {
    fmt.Println(quote.Hello())
}
```

After the writing is done, run it in the terminal in the same directory to build and test.

```
$ go build
$ ./hello
```

### Get Delve \(Golang Debugger\)

Delve is the best debugger for Golang and this will be used with VSCODE.

```
$ go get -u github.com/derekparker/delve/cmd/dlv
```

The main command - **dlv** is probably located in $HOME/golang/bin.


---

## 2. Golang and VSCODE

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
* Themes you want (zxx light and dracula in my case)

### Config for Debugging


 
---

## Conclusion

We just followed the simple procedure to have Golang SDK and development tools so that it is matter of time to make a simple but yet powerful Go application. 

Now you are a gopher!

![](/assets/gopher3.png)
  
