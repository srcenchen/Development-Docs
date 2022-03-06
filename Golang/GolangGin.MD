# Golang gin
## 简介
Gin is a web framework written in Go (Golang). It features a martini-like API with performance that is up to 40 times faster thanks to httprouter. If you need performance and good productivity, you will love Gin.  
总而言之，快，简单
## 引入依赖
下载包  
``` shell
$ go get -u github.com/gin-gonic/gin
```
在你的代码中引入包  
``` golang
import "github.com/gin-gonic/gin"
```
## 简单的例子
``` golang
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()
	r.GET("/ping", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": c.Query("key"),//获取"?key="的内容
		})
	})
    // 这里也可以写 POST,Put啥的
	r.Run(":8081") // listen and serve on 0.0.0.0:8081 (for windows "localhost:8081")
}
```
