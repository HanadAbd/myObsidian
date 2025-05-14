2024-12-16 12:02

Status:

Tags:

---
Enums are just custom data types that can be made

```
WEEK = MON|TUE|WED|THU|FRI|SAT|SUN
```
so any value of type "WEEK" can only have those 7 possible values. This can be used to confrim types, conditions and only apply what's necessary to that given type.

Enum example in Golang:
---

```
const (
    MON = iota
    TUE
    WED
    THU
    FRI
    SAT
    SUN
)
```
In this case we use "iota" which is used in const declrations to provide an incrementing identifier, so MON =0. So if day1 == day2{} and both are the same day, they'll refer to the same identifier.

iota resets after the end of each iota declerations

You could define them manually e.g:

```
MON = "MON"
```

but it's probably not worth the effort

Improvements with types:
--
We can assign it a type by making one for it like:
```
type Weekday int
```

and we can have different type declarations for different const declarations .




##### References


----
