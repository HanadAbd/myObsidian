2025-01-03 13:18

Status:

Tags: [[Go Golang Learning]]

---
Golan's main claim to fame is it's way of easily handling concurrency and multi threading with go routines. Best used with **channels** to share data across threads as well as **contexts** to manage these Different threads.

**Channels**: Just queues that follow FIFO so pop out the first result added to it.

**Contexts**: Used to manage timeouts, cancelling go routines and sharing values across go routines. 


Best Practices:


### Simple Multi threading example

You can use "sync" and "WaitGroup" to make tokens to give each thread, and main functions wait until it gets each token back, so every thread is complete

```go
package main

import (
    "fmt"
    "sync"
)

func worker(id int, wg *sync.WaitGroup) {
	//defer means this is the last thing the function will do before closing, to ensure this function does this
    defer wg.Done()
    fmt.Printf("Worker %d starting\n", id)
    // simulate work
    fmt.Printf("Worker %d done\n", id)
}

func main() {
    var wg sync.WaitGroup
    for i := 1; i <= 3; i++ {
        wg.Add(1)
        go worker(i, &wg)
    }
    wg.Wait()
    fmt.Println("All workers finished")
}
```

### Handling Channels

**Channels** are queues used to transfer data across go routines. They are created like slices with 

```go
//used to define the channel and size, leave empty to be unedfined
myChan := make(chan string, 1)
go func() {
        // Simulate a task that takes 3 seconds
        time.Sleep(3 * time.Second)
        
        ch <- "Task completed"
}()
//As long as channel is not closed, it will loop through value through channel
for value := range yourChannel {
	res := value
	fmt.Println("This is the value after go routine ",res)
	}

```
### Working with Contexts

**Contexts** are used to manage different go routines by:
- Handling cancelling
- Timing out threads and handling timeouts
- Passing data across go routines.


```go

func main() {

    // Create a context with a 2-second timeout
    ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
    defer cancel() // Release resources when main function exits


    result := doSomething(ctx)
    fmt.Println(result)
}

func doSomething(ctx context.Context) string {
    ch := make(chan string, 1)

    go func(ctx context.Context) {
        //Does which ever come's first, either 3 seconds or timeout, so 
        select {
        case <-time.After(3 * time.Second):
            ch <- "Task completed"
        case <-ctx.Done():
            ch <- "Task canceled"
        }
    }(ctx)

    select {
    case <-ctx.Done():
        return "Operation timed out"
    case res := <-ch:
        return res
    }
}


```



##### References


----
[Exploring Golang Channels](https://medium.com/@ravikumar19997/exploring-the-depths-of-golang-channels-a-comprehensive-guide-53e1a97cafe6)