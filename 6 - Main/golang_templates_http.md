2024-12-21 16:53

Status:

Tags:[[Go Golang Learning]]

---

HTTP:
---

Handlers are responsible for the actual logic and functionality, so using the **writer** and **request** to respond to requests.

```
http.HandleFunc("/home", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Welcome to the home page!")
    })
```

**Request** allows you to read the content of the request. 
**Writer** is what's returned so defining what is returned.

**Mux** or **servemux** is typically used as a router, mapping url's against corresponding handlers.
```
mux := http.NewServeMux()
mux.HandleFunc("/home", homeHandler)

...
http.ListenAndServe("localhost:8080", mux)
```

**Serving static files:**
You can use a "http.FileServer()". we can use mux, our router to say anything thing on "/static/" should serve that file. 

```
// requests to "/static/" serve files from the folder dist/static. Also just for convienece, "/static/" is stripped from the request, so it doesn't end up being ./dist/static/static/css/styles/css

mux.Handle("/static/", http.StripPrefix("/static/", http.FileServer(http.Dir("./dist/static"))))
```
NOTE: The only part that's useful is the file server.


Templates:
---
1. **`{{define "name"}} ... {{end}}`**: Defines a template with a specific name.
2. **`{{template "name" .}}`**: Includes the named template, passing the current data context.
3. **`{{if condition}} ... {{end}}`**: Conditionally includes content based on the evaluation of the condition.
4. **`{{else}}`**: Used within an `if` action to provide an alternative content block.
5. **`{{with pipeline}} ... {{end}}`**: Temporarily redefines the dot (`.`) to the value of the pipeline.
6. **`{{block "name" .}} ... {{end}}`**: Defines a block that can be overridden by other templates.
7. **`{{range .}} . . .  {{end}}`**: Loops through an object each time and populates the fields with the data available there. 


**Templates** are a part of the html/template. They are what you need to read the html files and then server them later:

```
//Getting all templates
var templates = template.Must(template.ParseFiles("templates/edit.html", "templates/view.html"))

//Get the corresponding template name and load it to the writer for what it is to return. With p being any data you want to pass.
err := templates.ExecuteTemplate(w, tmpl+".html", p)
```

**Appearing as raw text:**

That means the content for the writer hasn't been set as  

```
	w.Header().Set("Content-Type", "text/html; charset=utf-8")
```


If we want to pass data like the title, we can do:
--

```
home.html
<h1>{{.Title}} </h1>

main.go
type Page struct {
    Title string
    Body  []byte
}
...
p := &Page{Title: "Home", Body: []byte()}}
err := templates.ExecuteTemplate(w, tmpl+".html", p)
```

Pass any data to example:
--
But doing this is probably better and universally applicable
```
home.html
<h1>{{.Title}} </h1>
<p>{{.Content}}
...

data := map[string]interface{}{
        "Title":   "Home",
        "Content": "Welcome to the home page!",
        ...
    }
err := templates.ExecuteTemplate(w, tmpl+".html", data)
```

**templates within other templates:**

Use the **define** tag to define a template and a given name:
```
header.html
{{ define "header" }}
<header>
    <h2><a href="/home">SummerVille</a></h2>
</header>
{{ end }}
home.html
{{ template "header" . }}
<h1>{{"Home Page"}}</h1>
```

Multiple or no templates within other templates:

You can use the **`range`** function to just loop through and object like {{range .Users}} in order to get every value in there. You can also use as an If statement, if len of object == 0

```
{{ range .Users }}
	{{ template "userCard" . }}
{{ else }}
	<p>No users available.</p>
{{ end }}
```



##### References


----
