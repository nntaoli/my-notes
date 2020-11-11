## 编译瘦身
------------------
我们可以通过下面的方法将其变小点：

采用：`go build -ldflags "-s -w"` 这种方式编译。

解释一下参数的意思：

    -ldflags： 表示将后面的参数传给连接器（5/6/8l）
    -s：去掉符号信息
    -w：去掉DWARF调试信息

注意：

-s 去掉符号表（这样panic时，stack trace就没有任何文件名/行号信息了，这等价于普通C/C+=程序被strip的效果）

-w 去掉DWARF调试信息，得到的程序就不能用gdb调试了

两个可以分开使用

## 交叉编译
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build    
参数解释：
```
    CGO_ENABLED=0 ;//关闭cgo功能
    GOOS=linux;//操作系统，linux/windows/darwin 
    GOARCH=amd64;//操作系统位数，如64位:GOARCH=amd64，32位:GOARCH=386
```

## windows编译后台进程
> 参数: -H windowsgui  

`go build -ldflags "-H windowsgui"`

## go mod一些配置
#### 设置代理 
> go env -w GOPROXY=https://goproxy.cn,direct
#### 设置第三方包校验域名
> go env -w GOSUMDB=gosum.io+ce6e7565+AY5qEHUk/qmHc5btzW45JVoENfazw8LielDsaI+lEbq6
#### 关闭全局校验
> go env -w GOSUMDB=off
#### 设置私有库,私有库可以跳过代理和校验
> go env -w GOPRIVATE=*.gitlab.com,*.gitee.com
