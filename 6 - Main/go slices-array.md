2024-11-27 13:58

Status:

Tags:[[Go Golang Learning]]

---
This makes a static array.
```
int_arr :=[6]int{}

//Either empty or all 6 values must be defined
int_arr :=[6]int{1,2,3,4,5,6}
```


But if you want to define length with variable

```
//Since make is just creating the space for it, like malloc() so it's intially set to empty and can be made dynamically
int_arr := make([]int,LENGTH)
```


slices are formed by indices so

```
a := "abcdefghi"
a[low : high]
a[1:3]
//so this is slice getting data from indices 1>= to <3 so would be "b,c"
```



##### References

[Slices](https://go.dev/tour/moretypes/7)
[Array](https://go.dev/tour/moretypes/6)

----
