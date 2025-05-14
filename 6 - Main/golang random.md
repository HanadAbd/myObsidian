2024-12-21 14:52

Status:

Tags: [[Go Golang Learning]]

---

you can use the math/rand standard library.

SEEDING IS not necessary for the current versions of the math/rand libary

```
	example := rand.Int()

    fmt.Printf("Any positive integer: %d\n", example)

  

    example = rand.Intn(10)

    fmt.Printf("Any number from 0-9: %d\n", example)

  

    example = rand.Intn(10) - 9

    fmt.Printf("Any number from -10 to -9: %d\n", example)

    float_example := rand.Float64()

    fmt.Printf("Any value from 0 to 1: %v\n", float_example)
```



##### References


----
