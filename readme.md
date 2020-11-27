# GOMAXPROCS and Parallelism

Traditionally in earlier version of `Go` the `Go` runtime scheduler managed goroutine execution by leveraging the number of OS threads to attempt goroutine executions simultaneously. The Go runtime manages this against the number of available CPU cores today.

Go can execute thousands of groutines on a single OS thread which if often confused with parallelism. As Rob Pike famously talked of `concurrency is not parallelism`. Concurrency is achieved by breaking a program into subroutines, tasks or goroutines that can be executed independently, blocking ones intercahnged with ones ready fopr compute time.
