# Golang Development Environment Setting

If you need/want to have Golang development environment in Linux...

## Writer

* SJ Kim
* &lt;bus710@gmail.com&gt;

## Referenece

* [https://golang.org/doc/install](https://golang.org/doc/install)
* [https://code.visualstudio.com/docs/languages/go](https://code.visualstudio.com/docs/languages/go)
* [https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md](https://github.com/derekparker/delve/blob/master/Documentation/installation/linux/install.md)
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

Please check https://golang.org/dl/





