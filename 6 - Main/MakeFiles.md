2025-03-13 11:57

Status:

Tags: [[Programming]]

---
#### **Summary:**

"Makefile" is simply a shell script that you can use to build an application, similar to running npm start but not exclusive to JavaScript and TypeScript

##### **Creating Makefile:**

Create the file called "Makefile" and in the terminal, just run the command "Make"

```bash
#Makefile
say_hello:
    echo "Hello World"
```

Each *target* e.g. `say_hello` is similar to a function with typically, on the first target being called.

##### **Running Multiple or 1 target**

To call multiple at once initially, you can use the `all` target e.g.

```bash
all: say_hello say_goodbye 

say_hello:
    echo "Hello World"
say_goodbye:
    echo "Goodbye World"

```




##### References
----
