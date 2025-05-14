2025-03-16 13:42

Status:

Tags: [[Go Golang Learning]]
[[Golang Authentication and Secrets]]

---

#### **Summary**

- How to create request forms in front end
- How to handle requests in the back end


#### **Creating requests**

We can create requests with both html forms, (or html in general with Ajax) or with some API manager application like bruno or Post man.


###### **HTML Request**

The initial login, is always done with a POST request, so that the information isn't viewable in some URL and is handled by the server via some authentication service that will return an **authentication token** as **JWT or JSON Web Token** that will be sent with each request


``` html
<h2>Login</h2>
    <form action="/login" method="POST">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required>
        <br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required>
        <br>
        <button type="submit">Login</button>
    </form>

```


#### **Handling requests in backend**


Typically backend request handlers are wrapped with a middle ware verification, to see 1. if user is even authorised in the first place and 2. if it has access to this particular request anyway e.g. is admin, is member of this workspace etc.

You can also have session management, such as a Redis database where you can pull information regarding a user (seeing their identity and information) and if user isn't in that database, can be updated to include those details

So authenticate first with **Authentication token** and then **Authorise** with session details to see if it has access. Depending on how it fails this, you can have different returns and if it passes, it can continue to doing the main request handling  


##### References
----
