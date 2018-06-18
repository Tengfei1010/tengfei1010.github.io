---
title:  How to build golang on Ubuntu16.04
tags:
  - Linux
  - Golang
---

Here's how to build How to build golang on Ubuntu16.04.

<!--more-->

#### 1. Install requirements

```
$ sudo apt install build-essential
```

#### 2.Install go1.8 binary

```bash
  $ cd ${TOOLS}
  $ wget   https://dl.google.com/go/go1.8.linux-amd64.tar.gz
  $ tar -zxvf go1.8.linux-amd64.tar.gz
  $ mv go1.8.linux-amd64 go1.8
  # add go1.8 path ~/.bashrc
  export GOROOT=${TOOLS}/go1.8
  export GOPATH=${DEVELOP}/GoStudy
  export GOROOT_BOOTSTRAP=${TOOLS}/go1.8
  export PATH=$PATH:$GOPATH/bin:$GOROOT/bin
```

#### 3. Get Golang src code and build
Here we build golang 1.10 version. You can select your build version.
```bash
  $ cd ${DEVELOP}
  $ git clone https://github.com/golang/go.git
  $ cd go && git checkout -b v1.10 go1.10
  $ cd src
  $  ./all.bash
```

#### 4. Add New Golang to .bashrc

```bash
export GOROOT=${DEVELOP}/go
export GOPATH=${DEVELOP}/GoStudy
export GOROOT_BOOTSTRAP=${DEVELOP}/go
export PATH=$PATH:$GOPATH/bin:$GOROOT/bin
```

<b>Enjoy it ~  \*^_^\* <b/>
