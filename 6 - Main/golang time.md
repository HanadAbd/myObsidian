2025-01-05 15:52

Status:

Tags: [[Go Golang Learning]]

---

Mainly managed through the **"time"** standard library.


```go
    currentTime := time.Now()
    
	fmt.Println("Current Time in String: ", currentTime.String())
    fmt.Println("MM-DD-YYYY : ", currentTime.Format("01-02-2006"))
    fmt.Println("YYYY-MM-DD : ", currentTime.Format("2006-01-02"))
    fmt.Println("YYYY.MM.DD : ", currentTime.Format("2006.01.02 15:04:05"))
    fmt.Println("YYYY#MM#DD {Special Character} : ", currentTime.Format("2006#01#02"))
    fmt.Println("YYYY-MM-DD hh:mm:ss : ", currentTime.Format("2006-01-02 15:04:05"))
    fmt.Println("Time with MicroSeconds: ", currentTime.Format("2006-01-02 15:04:05.000000"))
    fmt.Println("Time with NanoSeconds: ", currentTime.Format("2006-01-02 15:04:05.000000000"))
    fmt.Println("ShortNum Month : ", currentTime.Format("2006-1-02"))
    fmt.Println("LongMonth : ", currentTime.Format("2006-January-02"))
    fmt.Println("ShortMonth : ", currentTime.Format("2006-Jan-02"))
    fmt.Println("ShortYear : ", currentTime.Format("06-Jan-02"))
    fmt.Println("LongWeekDay : ", currentTime.Format("2006-01-02 15:04:05 Monday"))
    fmt.Println("ShortWeek Day : ", currentTime.Format("2006-01-02 Mon"))
    fmt.Println("ShortDay : ", currentTime.Format("Mon 2006-01-2"))
    fmt.Println("Short Hour Minute Second: ", currentTime.Format("2006-01-02 3:4:5"))
    fmt.Println("Short Hour Minute Second: ", currentTime.Format("2006-01-02 3:4:5 PM"))
    fmt.Println("Short Hour Minute Second: ", currentTime.Format("2006-01-02 3:4:5 pm"))
```


Making a timer/ticker:
---

A **ticker** is it's own object that you can make with **time.NewTicker(time.duration)**. It has a channel that is enqueued at interval set.

Just like any channel, you can use a select list to dequeue a element and then do something at that tick.

``` go
blip := 2 * time.Second
ticker := time.NewTicker(blip)
defer ticker.Stop()
for {
	select {
    case <-ticker.C:
	    fmt.Printf("Tick at %v\n", time.Now().Format("2006-01-02 15:04:05"))
	}
}
```

Tracking performance:
---

You can use **time.Now() to get current time** and time.Since() to time elapsed since another value
```go
start := time.Now()
    for i := 0; i < 5; i++ {
        time.Sleep(1 * time.Second)
    }
    elapsed := time.Since(start)
    fmt.Println("Time taken: ", elapsed)
```

Comparing time's against each other:
--

You can use **time.After( {timeVar} )** and **time.Before( {timeVar} )** to compare times to see if it's more or less.


String to time, time to string:
---
Main things are the **time.Parse()** where you an pass the layout and the time string, or **time.ParseDuration()** where you pass the time duration e.g. "2s"

You can also use **.string()** to convert it into a string with 0 being 0 seconds

```
example := time.Now()
str_example := example.Format("2006-01-02 15:04:05")
fmt.Printf("%v\n", str_example)
var exam, _ = time.Parse("2006-01-02 15:04:05", str_example)
	fmt.Printf("%v\n", exam)
```


## Changing current time:


`time.Now().AddDate(0, 0, -3)` to get 3 days ago

`time.Now().Add(10 * time.Hour)` to get the Next 3 hours

`time.Now().Truncate(24 * time.Hour)` to get the current day at 00:00:00

##### References


----
