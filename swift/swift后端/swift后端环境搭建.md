## 用的是[Prefect](https://github.com/PerfectlySoft/Perfect)

## Swift兼容性

本项目目前使用Swift 4.0工具链（Ubuntu）或Xcode 9编译。

## 编译运行

下列命令行可以克隆并在8080和8181端口编译并启动 HTTP 服务器：

```
git clone https://github.com/PerfectlySoft/PerfectTemplate.git
cd PerfectTemplate
swift build
.build/debug/PerfectTemplate
```

如果没有问题，输出应该看起来像是这样：

```
[INFO] Starting HTTP server localhost on 0.0.0.0:8181
[INFO] Starting HTTP server localhost on 0.0.0.0:8080
```

这表明服务器已经准备好并且等待连接了。请访问[http://localhost:8181/](http://127.0.0.1:8181/) 来查看欢迎信息。在终端命令行上输入control-c组合键即可停止Web服务。

## 快速上手

模板项目包含了一个简单的“你好，世界！”页面，能够压缩传输内容并同时启动多个服务器。

```
import PerfectLib
import PerfectHTTP
import PerfectHTTPServer

// 页面控制器
// 以下“页面句柄”可以直接引用和配置
func handler(data: [String:Any]) throws -> RequestHandler {
    return {
        request, response in
        // 响应一个简单的页面
        response.setHeader(.contentType, value: "text/html")
        response.appendBody(string: "<html><head><meta http-equiv='content-type' content='text/html;charset=utf-8'><title>你好，世界！</title></head><body>你好，世界！</body></html>")
        // 在页面内容完成后必须主动调用 response.completed() 完成响应
        response.completed()
    }
}

// 同时配置启动两个服务器
// 以下配置例子显示了如何同时启动一个以上的服务器
// 使用一个字典数据作为配置文件

let port1 = 8080, port2 = 8181

let confData = [
    "servers": [
        // 1号服务器配置
        //  * <host>:<port>/ 服务器下显示“你好，世界！”
        //  * 提供 "./webroot" 下的文件访问，该文件夹必须设置在当前工作目录下
        //  * 执行页面和传输压缩
        [
            "name":"localhost",
            "port":port1,
            "routes":[
                ["method":"get", "uri":"/", "handler":handler],
                ["method":"get", "uri":"/**", "handler":PerfectHTTPServer.HTTPHandler.staticFiles,
                 "documentRoot":"./webroot",
                 "allowResponseFilters":true]
            ],
            "filters":[
                [
                "type":"response",
                "priority":"high",
                "name":PerfectHTTPServer.HTTPFilter.contentCompression,
                ]
            ]
        ],
        // 2号服务器配置数据
        //  * 将数据重定向返回给1号服务器
        [
            "name":"localhost",
            "port":port2,
            "routes":[
                ["method":"get", "uri":"/**", "handler":PerfectHTTPServer.HTTPHandler.redirect,
                 "base":"http://localhost:\(port1)"]
            ]
        ]
    ]
]

do {
    // 使用配置信息启动服务器
    try HTTPServer.launch(configurationData: confData)
} catch {
    fatalError("\(error)") // 启动异常
}
```