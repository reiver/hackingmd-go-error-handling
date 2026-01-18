# HACKING: Error Handling in Golang

This `HACKINGS.md` document describes how to deal with **error handling** in the **Go programming-lanuage** (**golang**).

-----

## Do Not

In general, do _not_ use the Go built-in packages for **error handling**.
I.e., in general, do not use the Go built-in [`"errors"`](https://pkg.go.dev/errors) package, and the [`fmt.Errorf()`](https://pkg.go.dev/fmt#Errorf) function from the Go built-in [`"fmt"`](https://pkg.go.dev/fmt) package.

## Do

Instead use the following package for **error handling**:

* https://codeberg.org/reiver/go-erorr

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

* Notice that a `const` was used (rather than a `var`).
* Notice that all _exported_ pre-defined errors started with the prefix `"Err"`.
* Notice that all _un-exported_ pre-defined errors started with the prefix "err". 

## Contextual Errors

Create a contextual error with source-code similar to the following:

```golang
if nil != err {
	return erorr.Wrap(err, "API request failed.",
		field.String("request-uri", requestURI),
		field.String("service", "monitor"),
	)
}
```

* Notice that the original error was passed as the first parameter to `erorr.Wrap()`.
* Notice that a human-legible message was passed at the second parameter to `erorr.Wrap()`.
* Notice that further context about the error was added as key-value pairs with the rest of the parameters passed to `erorr.Wrap()`.

## Alternatives

Here are some alternatives for using the `erorr` package rather than using the Go built-in [`"errors"`](https://pkg.go.dev/errors) package, and the [`fmt.Errorf()`](https://pkg.go.dev/fmt#Errorf) function from the Go built-in [`"fmt"`](https://pkg.go.dev/fmt) package:....

### Alternative for Pre-Defined Errors

Rather than doing something similar to:

```golang
var (
	ErrNilReceiver = errors.New("nil receiver")	
)
```

Instead use the `erorr.Error` type similar to the following:

```golang
const (
	ErrNilReceiver = erorr.Error("nil receiver")	
)
```

* Notice that `const` (rather than a `var`) was used with `erorr.Error`.

### Alteratives for Returning With Fixed Error Message

Rather than doing something similar to:

```golang
	return errors.New("proxy error")
```

Instead use the `erorr.Stamp()` functio similar to the following:

```golang
	return erorr.Stamp("proxy error")
```

Or, better yet:

```golang
	return erorr.Stamp("proxy error"
		field.String("proxy-uri", proxyURL),
	)
```

### Alteratives for Returning With Dynamic Error Message

Rather than doing something similar to:

```golang
	return fmt.Errorf("proxy error: %w", err)
```

Instead use the `erorr.Errorf()` functio similar to the following:

```golang
	return erorr.Errorf("proxy error: %w", err)
```

Or, better yet:

```golang
	return erorr.Wrap(err, "proxy error"
		field.String("proxy-uri", proxyURL),
	)
```

