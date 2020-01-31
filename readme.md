[![GoDoc](https://godoc.org/github.com/l-vitaly/php-go/phpgo?status.svg)](https://godoc.org/github.com/l-vitaly/php-go/phpgo)
[![GoDoc](https://godoc.org/github.com/l-vitaly/php-go/zend?status.svg)](https://godoc.org/github.com/l-vitaly/php-go/zend)

### php-go

Write PHP extension using go/golang. Zend API wrapper for go/golang. 

Simple, easy, fun to write PHP extensions.

### Features

* function support
* struct/class support
* constant support
* primitive data type as parameters and return values, (u)int*/float*/string/bool
* complex data type as parameters, map/slice/array
* all can be done by programmatic

### Environment

* Modern Linux/Unix system
* PHP 5.5+/7.x
* go version 1.4+
* php5-dev installed (`apt-get install php5-dev`)
* for MacOS, go 1.8+

### Build & Install

go get:

```
go get github.com/l-vitaly/php-go
cd $GOPATH/src/github.com/l-vitaly/php-go
# adjust PHPCFG path if needed
PHPCFG=`which php-config` make
```

manual:

    mkdir -p $GOPATH/src/github.com/l-vitaly
    git clone https://github.com/l-vitaly/php-go.git $GOPATH/src/github.com/l-vitaly/php-go
    cd $GOPATH/src/github.com/l-vitaly/php-go
    make
    ls -lh php-go/hello.so
    php56 -d extension=./hello.so examples/hello.php


### Examples

```go
// package main is required
package main

import "github.com/l-vitaly/php-go/phpgo"

func foo_in_go() {
}

type Bar struct{}
func NewBar() *Bar{
    return &Bar{}
}

func init() {
    phpgo.InitExtension("mymod", "1.0")

    phpgo.AddFunc("foo_in_php", foo_in_go)
    phpgo.AddClass("bar_in_php", NewBar)
}

// should not run this function
// required for go build though.
func main() { panic("wtf") }
```

### Limitations

* Deadlock in pcntl_fork'ed subprocess when call extension functions. #47


### TODO

- [ ] install with go get 
- [x] improve php7 support
- [ ] namespace support
- [ ] multiple extension support
- [ ] class member access support
- [x] unlimited function/method/class count support
- [x] global ini var support
- [ ] fill phpinfo


Contributing
------------
1. Fork it
2. Create your feature branch (``git checkout -b my-new-feature``)
3. Commit your changes (``git commit -am 'Add some feature'``)
4. Push to the branch (``git push origin my-new-feature``)
5. Create new Pull Request
