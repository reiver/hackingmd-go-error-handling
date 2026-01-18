# HACKING: Error Handling in Golang

In general, do _not_ use the Go built-in packages for **error handling**.
I.e., in general, do not use the Go built-in [`"errors"`](https://pkg.go.dev/errors) package, and the [`fmt.Errorf()`](https://pkg.go.dev/fmt#Errorf) function from the Go built-in [`"fmt"`](https://pkg.go.dev/fmt) package.

Instead use the following package for **error handling**:

* https://codeberg.org/reiver/go-erorr
