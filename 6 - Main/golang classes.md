2025-02-24 21:47

Status:

Tags: [[Go Golang Learning]]

---

Summary:

No classes like for other languages, but can use struct, methods on structs and interfaces


### Structs and struct methods

You can make complex data types with struct are comprised of other data types.

You can also apply methods specific to that struct

```
type Node struct {
    Name string
}

//defines the method Print on that struct
func (n *Node) Print() {
    fmt.Printf("\nNode: %s\n", n.Name)
}

func main(){
	n := Node{Name: "node1"}
	n.Print()
}
```

### Interfaces



##### References
----
