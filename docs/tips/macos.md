<!-- 标题随意，但是要简洁明了，不要太长。 -->
# MacOS 解决方案

<!-- 内容随意，但是要保证逻辑清晰、可读性强。 -->

## C++

在大一的程序设计课程中，老师推荐的 C++ IDE 是 `dev-c++` 和 `codeblock`。codeblock 有 MacOS 版本，但是长期没有得到维护，使用体验很差。在此解决方案有：

* CLion：Jetbrains 旗下强大的编译器，可以使用 Github 学生认证获得免费的激活码，更加适合比较大的工程，不适合 OJ 代码的编写。
* Xcode：Apple 旗下的 IDEA，可以编写 C++ 程序，但是起体量比较大（10G左右），更加适合比较大的工程，更加适合 Swift 或者 Object-C 的开发，不适合 OJ 代码的编写。
* VSCode + Makefile：==强烈推荐==。
    * VSCode 是微软免费的编辑软件，其本身的应用商城包含了大量的第三方插件。
    * Makefile 像一个脚本，可以指定运行的流程从而编写代码。
    * 利用 VSCode 底部调用的 MacOS 的 terminal，使用 `make` 命令就可以生成可执行文件。

提供一个可用的 Makefile 文件。将此 Makefile 文件命名为 `Makefile`，并且放到于自己原代码相同的文件夹下。注意，此文件夹下只能包含一个 `*.cpp` 或者 `*.c` 的文件。

```makefile
CC      = gcc
CXX     = g++
LINK    = g++
CFLAGS  = -g -Wall -O2
TARGET  = t6
SRCS    = $(wildcard *.cpp)
SRCS    += $(wildcard *.c)
CXX_OBJS    = $(patsubst %.cpp, %.o, $(wildcard *.cpp))
C_OBJS  = $(patsubst %.c, %.o, $(wildcard *.c))

all:$(TARGET)

$(TARGET):$(CXX_OBJS) $(C_OBJS)
	$(LINK) $(CFLAGS) -o $@ $^
	rm -rf *.o
%.o: %.cpp
	$(CXX) $(CFLAGS) -c -o $@ $<
%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<
.PHONY:clean
clean:
	rm -rf *.o $(TARGET) $(CXX_OBJS) $(C_OBJS)
```

然后在终端（terminal）中在此文件夹下执行 `make` 即可。

## 虚拟机（VM）

在数字逻辑课程中我们会使用 Quartus，在路由器的实验课程中我们会用到华为的 eNSP，这些软件都没有提供 MacOS 的版本，并且没有替代品。所以这个适合需要一个虚拟机，在上面安装 Windows 之后就可以使用这些软件了。MacOS 上比较好用的虚拟机有 VM Fusion（需要激活码，可以在 tb 上找找，Windows 的镜像安装文件也是一样）。

如果 MacOS 内存有限，可以购买外接 SSD，将虚拟机安装地址设置在 SSD 上，实际使用没有卡顿。 