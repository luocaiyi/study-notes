# Start

## Install

1. Download and Install [GO](https://golang.google.cn/dl/)
2. Environment Variables:
    1. `GOROOT` -> GO安装目录
    2. `GOPATH` ->
        1. `src` -> 存放源代码
        2. `pkg` -> 存放依赖包
        3. `bin` -> 存放可执行文件
    3. Others Variables：
        1. `GOOS`, `GOARCH`, `GOPROXY`
        2. 国内用户建议设置 `GOPROXY`：`export GOPROXY=https://goproxy.cn`

## SOME CMD

|CMD|DESC|
|:---:|---|
|bug          | start a bug report |
|**build**    | compile packages and dependencies |
|clean        | remove object files and cached files |
|doc          | show documentation for package or symbol |
|env          | print Go environment information |
|fix          | update packages to use new APIs |
|**fmt**      | gofmt (reformat) package sources |
|generate     | generate Go files by processing source |
|**get**      | add dependencies to current module and install them |
|**install**  | compile and install packages and dependencies |
|list         | list packages or modules |
|**mod**      | module maintenance |
|run          | compile and run Go program |
|**test**     | test packages |
|**tool**     | run specified go tool |
|version      | print Go version |
|vet          | report likely mistakes in packages |

### Go build

- Go 语言不支持动态链接，因此编译时会将所有依赖编译进同一个二进制文件。
- 指定输出目录
  - `go build –o bin/mybinary .`
- 常用环境变量设置编译操作系统和 CPU 架构
  - `GOOS=linux GOARCH=amd64 go build`
- 全支持列表
  - `$GOROOT/src/go/build/syslist.go`

### Go test

Go 语言原生自带测试

```go
import "testing"
func TestIncrease(t *testing.T) {
    t.Log("Start testing")
    increase(1, 2)
}
```

`go test ./… -v` 运行测试

`go test` 命令扫描所有 `*_test.go` 为结尾的文件，惯例是将测试代码与正式代码放在同目录，
如 `foo.go` 的测试代码一般写在 `foo_test.go`

#### Go vet

代码静态检查，发现可能的 bug 或者可疑的构造

- `Print-format` 错误，检查类型不匹配的`print`

    ```go
    str := "hello world!"
    fmt.Printf("%d\n", str)  // 此处'/n' 与 'str' 类型不匹配
    ```

- `Boolean` 错误，检查一直为 `true`、`false` 或者冗余的表达式

    ```go
    fmt.Println(i != 0 || i != 1)
    ```

- `Range` 循环，比如如下代码主协程会先退出，`go routine`无法被执行

    ```go
    words := []string{"foo", "bar", "baz"}
    for _, word := range words {
        go func() {
            fmt.Println(word).
        }()
    }
    ```

- `Unreachable` 的代码，如 `return` 之后的代码
- 其他错误，比如变量自赋值，error 检查滞后等

    ```go
    res, err := http.Get("https://www.spreadsheetdb.io/")
    defer res.Body.Close()
    if err != nil {
        log.Fatal(err)
    }
    ```

## Golang playground

可直接编写和运行 Go 语言程序

官方 [playground](https://play.golang.org/)

国内可直接访问的 [playground](https://goplay.tools/)
