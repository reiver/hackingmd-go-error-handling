# HACKING: Error Handling in Golang

This `HACKINGS.md` document describes how to deal with **error handling** in the **Go programming-lanuage** (**golang**).

-----

## Do Not

In general, do _not_ use the Go built-in packages for **error handling**.
I.e., in general, do not use the Go built-in [`"errors"`](https://pkg.go.dev/errors) package, and the [`fmt.Errorf()`](https://pkg.go.dev/fmt#Errorf) function from the Go built-in [`"fmt"`](https://pkg.go.dev/fmt) package.

## Do

Instead use the following package for **error handling**:

* https://codeberg.org/reiver/go-erorr

## Alternatives

* Instead of using the [`errors.New()`](https://pkg.go.dev/errors#New) function in the Go built-in [`"errors"`](https://pkg.go.dev/errors) package, use the `erorr.Error` type.
  * Pre-Defined errors created using the the `erorr.Error` type **MUST** be created using a `const` (rather than a `var`).
* Instead of using the [`fmt.Errorf()`](https://pkg.go.dev/fmt#Errorf) function from the Go built-in [`"fmt"`](https://pkg.go.dev/fmt) package, use the `erorr.Errorf()` or `erorr.Wrap()` functions.

## Pre-Defined Errors

Pre-Defined errors in the source-code MUST be created with source-code similar to the following:

```golang
const (
	ErrNilReceiver = erorr.Error("nil receiver")
	ErrNotFound    = erorr.Error("not found")
	ErrUndefined   = erorr.Error("undefined")
)

const (
	errBadFormat = erorr.Error("bad format") 
	errTimeOut   = erorr.Error("time-out")
)

```

Notice that a `const` was used (rather than a `var`).

