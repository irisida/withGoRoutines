# GOMAXPROCS and Parallelism

Traditionally in earlier version of `Go` the `Go` runtime scheduler managed goroutine execution by leveraging the number of OS threads to attempt goroutine executions simultaneously. The Go runtime manages this against the number of available CPU cores today.

Go can execute thousands of groutines on a single OS thread which if often confused with parallelism. As Rob Pike famously talked of `concurrency is not parallelism`. Concurrency is achieved by breaking a program into subroutines, tasks or goroutines that can be executed independently, blocking ones intercahnged with ones ready fopr compute time.

## Sample Go-routine

```go
package main

import (
	"fmt"
	"math/rand"
	"sync"
	"time"
)

var wg sync.WaitGroup

func printCounts(label string) {
	pf := fmt.Printf

	//defer the waitgroups call to done
	defer wg.Done()

	// Random wait for demonstration purposes
	for count := 1; count <= 10; count++ {
		sleep := rand.Int63n(3000)                          // get a random number between 0-3000
		time.Sleep(time.Duration(sleep) * time.Millisecond) // sleep for that num of milliseconds
		pf("Count %d from %s\n", count, label)              // print count and for which goroutine
	}
}

func main() {
	p := fmt.Println

	wg.Add(2)

	p("Start Goroutines")

	go printCounts("ONE")
	go printCounts("TWO")

	wg.Wait()
	p("Completed. Terminating program")
}


```
