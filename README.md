rollbar
-------

`rollbar` is a Go Rollbar client that makes it easy to report errors to Rollbar
with stacktraces. Errors are sent to Rollbar asynchronously in a background
goroutine.

Because Go's `error` type doesn't include stack information from when it was set
or allocated, `rollbar` uses the stack information from where the error was
reported.

You may also want to look at:

* [stvp/roll](https://github.com/stvp/roll) - Simpler, synchronous (no
  background goroutine) with a nicer API.

Installation
=============

Assuming you have Go correctly installed, including the proper workspace folder structure, run the following command from your project directory:
```
go get github.com/stvp/rollbar
```
Depending on your text editor / IDE / plugins, make sure to paste the setup code before the import statement. Some plugins or environments do not allow unused imports and will immediately delete the import statement if you save before the imported code is actually used. 

Documentation
=============

[API docs on godoc.org](http://godoc.org/github.com/stvp/rollbar)

Usage
=====

```go
package main

import (
  "github.com/stvp/rollbar"
)

func main() {
  rollbar.Token = "MY_TOKEN"
  rollbar.Environment = "production" // defaults to "development"

  result, err := DoSomething()
  if err != nil {
    rollbar.Error(rollbar.ERR, err)
  }

  rollbar.Message("info", "Message body goes here")

  rollbar.Wait()
}
```

Running Tests
=============

Set up a dummy project in Rollbar and pass the access token as an environment
variable to `go test`:

    TOKEN=f0df01587b8f76b2c217af34c479f9ea go test

And verify the reported errors manually in the Rollbar dashboard.

Contributors
============

Thanks, all!

* @kjk
* @nazwa
* @ossareh
* @paulmach
* @Soulou
* @tike

