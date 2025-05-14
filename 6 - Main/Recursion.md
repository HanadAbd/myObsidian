2024-12-12 11:21

Status:

Tags:[[Computer Science Principals]]


---
Usually used in place of typical iteration by using function calls to repeat some functionality. Anything can be written in recursion can be written iteratively and vice versa (And in terms of execution, they are basically the same)
IDEAL FOR DIVIDE AND CONQUER algorithms and functions

Key ideas for recursion are:

- A counter or some sort of mechanism do differentiate non-base case from base case,
- A base case, so a case it ends up and returns the appropriate value needed.
- return the function but with the arguments updated with some functionality

```
function doRecursion(data_being_changed any,counter int) int{
	//Basecase
	if counter <=1{
		return int
	}
	data_after:=doSomething(int)
	return (doRecursion(data_after,counter-1))
}
```

So:
1. BASE CASE (How it ends)
2. RECURSIVE CASE (How it calls itself and approaches base case)
3. GENERAL FUNCTIONALITY

##### References


----
