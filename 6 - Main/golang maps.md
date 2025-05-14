O2024-12-21 15:09

Status:

Tags: [[Go Golang Learning]]

---
Maps or dicts in general take a "Key" and "Value". So for every corresponding key, there's a value.

You can make maps with either:

```
var make_map = make(map[string]int)

//If you don't make it, you will need to intially assign a value to it
var var_map = map[string]int{"Hanad": 21}
```


Just like you can use objects/dicts in javascript, you can do the same once defining the type.

```
myObject := map[string]int{
        "Hanad": 21,
        "Caaisha":17
    }
```

to access the values within the map. to use a for loop that gets the key and value

```
for key, value := range var_map {

        fmt.Printf("Key: %s Val: %d\n", key, value)

    }
```

It's the same approach for [[go slices-array]] "for x,y := range myArr" get's the index for x, and value for y. That's because it's the same thing but you can define the index to enforce uniqueness. 



##### References


----
