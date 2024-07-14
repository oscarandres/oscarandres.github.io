---
meta:
  title: "Serving html pages with Go"
  description: "How to server html pages with go"
  keywords: "go, golang, html, serve, start with go, hello world, hello world page with go, hello world page with golang"
---

# Serving html pages with Go

## Create and html file
```html
<!doctype html>
<html>
    <head>
        <title>Hello World</title>
    </head>
    <body>
        <h1>Hello World!</h1>
        <p>Example paragraph.</p>
        <p>
            <img
                src="https://oscarandres.github.io/_media/oscarandres.jpeg"
                alt="Nice picture"
            />
        </p>
        <p>
            <a href="https://oscarandres.github.io">My web page</a>
        </p>
    </body>
</html>
```
## Write a handle function to serve file
```go
func serveHelloWorld(writer http.ResponseWriter, request *http.Request) {
	fmt.Println(request.URL.Path)
	http.ServeFile(writer, request, "./hello-world.html")
}
```

So, lets take a look to this code, this function expects two parameters: 
- `writer` a [http.ResponseWriter](https://pkg.go.dev/net/http#ResponseWriter) interface used to construct an HTTP response to be sent to the client
- `request` a *[http.Request](https://pkg.go.dev/net/http#Request) pointer representing the incoming HTTP request from the client.
They are used on the line:
- `http.ServeFile(w, r, "./hello-world.html")` serves the file `hello-world.html` as a response to the client

?>  Notice that `hello-world.html` is on the current working directory

## Register the handle function on server
```go
func main() {
	fmt.Println("serving on http://localhost:80")
	http.HandleFunc("/", serveHelloWorld)
	log.Fatal(http.ListenAndServe(":80", nil))
}
```
In this block code `http.HandleFunc("/", serveHelloWorld)` registers the function `serveHelloWorld` as the handler for the root path (`/`). This means that any HTTP request to the root path will be forwarded to the `serveHelloWorld` function.

## The full file look like this:

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {
	fmt.Println("serving on http://localhost:80")
	http.HandleFunc("/", serveHelloWorld)
	log.Fatal(http.ListenAndServe(":80", nil))
}

func serveHelloWorld(writer http.ResponseWriter, request *http.Request) {
	fmt.Println(request.URL.Path)
	http.ServeFile(writer, request, "./hello-world.html")
}

func serveFiles(w http.ResponseWriter, r *http.Request) {
	fmt.Println(r.URL.Path)
	http.ServeFile(w, r, "./hello-world.html")
}
```
## Finally run the code
Now you when you run this command:
```bash
go run .
```
You will receive this response on the console:
```bash
serving on http://localhost:80
```
Now when you browse to http://localhost:80 you will see something like this:
![page screenshot](./_media/img.png)