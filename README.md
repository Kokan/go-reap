# go-reap

Provides a super simple set of functions for reaping child processes. This is
useful for running applications as PID 1 in a Docker container.

This should be supported on all UNIX flavors, but is not supported on Windows.
Windows has a stub implementation that's safe to call, as well as an API to
check if reaping is supported so that you can produce an error in your
application code.

Documentation
=============

The full documentation is available on [Godoc](http://godoc.org/github.com/hashicorp/go-reap).

Example
=======

Below is a simple example of usage

```go
// Reap children with no feedback.
if reap.IsSupported() {
	go ReapChildren(nil, nil)
}

// Get feedback on reaped children and errors.
if reap.IsSupported() {
	pids := make(reap.PidCh, 1)
	errors := make(reap.ErrorCh, 1)
	go ReapChildren(pids, errors)
}
```

