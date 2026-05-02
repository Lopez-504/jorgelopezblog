+++
title = "CodeBlocks"
date = "2026-05-01T19:47:58-04:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Jorge L."
authorTwitter = "" #do not include @
cover = "nat.jpg"
tags = ["Coding", "Syntax"]
keywords = ["Code blocks", "Programming languages"]
description = "Showcase different code blocks, different highlights and programming languages"
showFullContent = false
readingTime = true
hideComments = false
ShowToc = true
+++

# Code block examples, highlight and different languages

Check [Hugo official doc](https://gohugo.io/content-management/syntax-highlighting/)


solve this path problem, below we're using: /jorgelopezblog/killua1short.jpg

![Killua](/jorgelopezblog/killua1short.jpg "caption=killua having a drink | width=340px")	


## Examples

1. python + monokai

```python {linenos=inline hl_lines=[3,"6-8"] style=monokai}
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        fmt.Println("Value of i:", i)
    }
}
```


2. go + RPGLE

```go {linenos=inline hl_lines=[3,"6-8"] style=RPGLE}
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        fmt.Println("Value of i:", i)
    }
}
```

3. bash + ashen | highlight lines 2,3 

```bash {linenos=inline hl_lines=[2,"3"] style=ashen} 
jorge@jorge-HP-Note:~$ git add .
jorge@jorge-HP-Note:~$ git commit -m "message"
jorge@jorge-HP-Note:~$ git push origin main
```

4. bash + monokai | highlight line 2

```bash {linenos=inline hl_lines=[2] style=monokai}
jorge@jorge-HP-Note:~$ git add .
jorge@jorge-HP-Note:~$ git commit -m "message"
jorge@jorge-HP-Note:~$ git push origin main
```
2. JS + arduino

```javascript {linenos=inline hl_lines=[3,"6-8"] style=arduino}
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        fmt.Println("Value of i:", i)
    }
}
```

## More examples

- some
