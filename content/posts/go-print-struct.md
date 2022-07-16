---
title: "Go Print Struct"
date: 2022-07-16T11:06:46+02:00
draft: false
keyword: english programming golang hacks
featured_image: "/golang.png"
---

While programming with Go, sometimes to debug a problem you'll need to print a whole struct

```go
package main

import "fmt"

func main() {

        type Demo struct {
                MemberStr   string
                MemberInt   int
                MemberFloat float64
        }

        d := Demo{
                MemberStr:   "This is a text",
                MemberInt:   10,
                MemberFloat: 3.145,
        }

        fmt.Println(d)
        fmt.Printf("%v\n", d)
}
```

but the default fmt.Print* result lacks of member name :

```sh
{This is a text 10 3.145}
{This is a text 10 3.145}
```

Adding a single char to the Printf :

```go
        fmt.Printf("%+v\n", d)
```

 makes the magic : 

```sh
{This is a text 10 3.145}
{MemberStr:This is a text MemberInt:10 MemberFloat:3.145}
```

For a prettier format, jus implement the String interface for the desired struct :

```go
package main

import "fmt"

type Demo struct {
	MemberStr   string
	MemberInt   int
	MemberFloat float64
}	

func (d Demo) String() string {
	return fmt.Sprintf("Demo{\n\tMemberStr=%s\n\tMemberInt=%d\n\tMemberFloat=%f\n}", d.MemberStr, d.MemberInt, d.MemberFloat)
}

func main() {

	d := Demo{
		MemberStr:   "This is a text",
		MemberInt:   10,
		MemberFloat: 3.145,
	}

	fmt.Println(d)
	fmt.Printf("%s\n", d)
}
```

and here there is the prettified print : 

```sh
Demo{
	MemberStr=This is a text
	MemberInt=10
	MemberFloat=3.145000
}
Demo{
	MemberStr=This is a text
	MemberInt=10
	MemberFloat=3.145000
}
```
