## Go Tutorial
### Download and install go compiler and an IDE
### Follow this [tutorial](https://go.dev/doc/tutorial/getting-started) for using golang
### YouTube vide for reference [here](https://www.youtube.com/watch?v=ty49_v1tV44&ab_channel=Telusko)

### Go is a compiled language.
### unsued package and variables will throw error.

#### fmt is a format package
#### main is where the code execution starts
#### each file can be defined under a package name for reuse

    package main

    import "fmt"

    func main() {
        fmt.Println("Hello World!")
    }

## Topics Discussed
### variable declaration and usage 
    result := 5
    var result = 5
    var result int = 5

    const result = 5

### loops - Go does all kinds of looping with 'for' 
#### need to start the curly bracket from the same line as the function name
    //Infinite loop
    for {
        fmt.Println("Hello")
    }

    //Finite loop - Method 1
    i := 0
    for i<=5 {
        fmt.Println("Hello")
        i++
    }

    //Finite loop -  Method 2
     
    for i := 0 ; i<=5 ; i++{
        fmt.Println("Hello")
    }

### funtions

    func add(x int, y int) int {
        var out = x + y
        return out
    }

    func add(x int, y int) (int,int) {
        var add = x + y
        var sub = x - y
        return out,sub
    }

    func add(x int, y int) (add,sub int) {
        add = x + y
        sub = x - y
        return
    }

### Package level variables and function level variables in Go


### Exported funtions - function of one package that can be used in other packages
#### Only functions which start will Uppercase letter are exported.


### Math package
    package main
    import (
        "fmt"
        "math
    )

    func main(){
        var num float = 64

        result := math.Sqrt(64)

        fmt.Println(result)
    }

### Formatted printing in Go
    fmt.Printf("The output is %.2g Thank you ",result)

### if else and switch
    if num < 5 {
        fmt.Println("Hi")
    } else if num ==5 {
        fmt.Println("Welcome")
    } else {
        fmt.Println("Bye")
    }


    switch num {
        case 1:
            fmt.Println("1")
        case 2:
            fmt.Println("2")
        default:
            fmt.Println("None")
    }

#### We don't have to use break statements with switch in Go

### Time package in Go

    import (
        "fmt"
        "time"
    )

    func main(){
        day := time.Now().Weekday()
        fmt.Println(day)
    }

<br/>

### Gin is a high-performance micro-framework that can be used to build web applications and microservices. It makes it simple to build a request handling pipeline from modular, reusable pieces.
### [Tutorial](https://www.youtube.com/watch?v=qR0WnWL2o1Q&list=RDLVqR0WnWL2o1Q&start_radio=1&rv=qR0WnWL2o1Q&t=11&ab_channel=PragmaticReviews)

#### Install gin library
    go get github.com/gin-gonic/gin

#### Or we can also do
    go mod init <module>
    go mod tidy

### Server code
    package main

    import "github.com/gin-gonic/gin"

    func main(){
        server := gin.Default()

        server.GET("/test",func(ctx *gin.Context) {
            ctx.JSON(200,gin.H{
                "message":"OK!!",
            })
        })

        server.Run(":8080")
    }

### [Go Database access](https://go.dev/doc/tutorial/database-access)