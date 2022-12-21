# android_ebpf_test
在Windows和macOS上交叉编译Android eBPF程序。  

## 编译命令
注意:
1. 把clang路径改为正确的路径，如果系统PATH中有clang，而且支持target bpf，可以不用NDK中的clang，直接用系统中的clang即可。
2. go generate要放到设置GOARCH和GOOS环境变量之前，否则生成的bpf2go程序无法执行，无法正确编译bpf的c代码。
``` shell
export BPF_CLANG=/c/Users/xing/AppData/Local/Android/Sdk/ndk/25.1.8937393/toolchains/llvm/prebuilt/windows-x86_64/bin/clang.exe
export BPF_CFLAGS="-O2 -g"
go generate
export GOARCH=arm64
export GOOS=android
go build
```
修改自cilium/ebpf的example：[ringbuf](https://github.com/cilium/ebpf/tree/master/examples/ringbuffer)。  
[文章](https://blog.xing.re/2022/12/21/%E4%BD%BF%E7%94%A8cilium-ebpf%E5%BC%80%E5%8F%91Android-eBPF%E7%A8%8B%E5%BA%8F/)
