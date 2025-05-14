2025-01-16 17:15

Status:

Tags:

---
**Summary:**

Just an overview for how unit testing is done in Golang, best standards as well as how to run these tests in a successful manner with both github and docker.

- Making a test file
- Important rules for testing
- Commainds 
## Rules for testing
---
- It needs to be in a file with a name like `xxx_test.go` and in the same package as you're testing
- The test function must start with the word `Test`
- The test function takes one argument only `t *testing.T`
- To use the `*testing.T` type, you need to `import "testing"`, 

## Commands for testing
---
```go
//testing testfiles in root directory
go test .
//For testing 1 package
go test ./<package>
//Testing every test file root and subdirectory
go test ./...
//Testing everything including package dependencies
go test all



```



### Making a Test file

Ensuring it's in the correct package location and right name.

```go
package main
import "testing"

//testing.T is used to define how it is tested
func TestFooer(t *testing.T) {
    result := returnFooIfOdd(3)
    if result != "Foo" {
    t.Errorf("Result was incorrect, got: %s, want: %s.", result, "Foo")
    }
}
```


In order to test multiple different variables and scenarios, you can use Table Driven Approach


```go
func TestFooerTableDriven(t *testing.T) {
      // Defining the columns of the table
        var tests = []struct {
	        name string
            input int
            want  string
        }{
            // the table itself
            {"9 should be Foo", 9, "Foo"},
            {"3 should be Foo", 3, "Foo"},
            {"1 is not Foo", 1, "1"},
            {"0 should be Foo", 0, "Foo"},
        }
      // The execution loop
        for _, tt := range tests {
            t.Run(tt.name, func(t *testing.T) {
                ans := Fooer(tt.input)
                if ans != tt.want {
                    t.Errorf("got %s, want %s", ans, tt.want)
                }
            })
        }
    }
```

with `t.Run(NameOfTheTest, subTest())`, it runs sub tests against your list of tests.

### Types of Responses

- `t.Log or t.Logf` Simply a log, no worry or concern
- `t.Error or t.Errorf` Returns an error and states the test has *failed*
- `t.Fatal or t.Fatalf` Returns a statement, ends test and states has *failed*

##### References
----
