# GOMAXPROCS and Parallelism

Traditionally in earlier version of `Go` the `Go` runtime scheduler managed goroutine execution by leveraging the number of OS threads to attempt goroutine executions simultaneously.
