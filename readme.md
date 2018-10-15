# 从 electron 迁移到 miniblink 的示例

## 1. 迁移的理由 (Why)

`electron` 太大了，解压后占用 120M 以上的硬盘空间。而用 `miniblink` 可以减少到 20M 以上，压缩后文件更是只有 7M 多的大小。

从 `electron` 到 `miniblink` 迁移的成本很低，不需要改源代码，只是把"壳"换一下即可。

## 2. 迁移的步骤 (Step)

1. 从 `github` 上下载最新的编译包
2. 把 `electron` 的 `resources` 文件夹下的内容，拷贝到 `miniblink` 的 `resources` 文件夹中
3. OK 完成，打开 `mini-electron.exe` 运行换"壳"之后的 `app`

通过以上 3 步骤，我们就能把应用从 `electron` 迁移到 `miniblink` 中。然而，我们还有一些事情需要做。

1. `miniblink` 的编译包有很多文件我们用不上，我们得找出我们需要的关键文件
2. `mini-electron.exe` 的图标和文件信息都不是我们想要的，我们需要修改它

## 3. 给个例子 (Example)

### 3.1  下载 miniblink 的编译文件

下载最新的 [miniblink 编译文件](https://github.com/weolar/miniblink49/releases)

例如：我们选择这个版本 `2018-10-11版`，SDK下载地址：https://pan.baidu.com/s/1sGkmAF34vZxXJj8dfekCXA

### 3.2 找出替换 electron 的关键文件

下载后，解压文件，将 `electron` 必要的几个文件或者文件夹拷贝出来。

`miniblink` 替换 `electron` 用到 3 个文件：文件 `node.dll` 和 `mini-electron.exe` 文件夹 resources。

我们把这个几个文件拷贝到 `D:\myApp\` 中：

``` text
- D:\myApp\
  - node.dll
  - `mini-electron.exe`
  - resources\
    - miniblink.asar\
```

### 3.3 从 electron 迁移到 miniblink

拿 [桌面版脑图](https://github.com/NaoTu/DesktopNaotu) 来举例，下载最新的 [桌面版脑图编译文件](https://github.com/NaoTu/DesktopNaotu/releases) 。

我们下载文件 `DesktopNaotu-win32-ia32.zip` ，解压后可以看到 `桌面版脑图` 编译后的目录结构如下：

``` text
- DesktopNaotu-win32-ia32\
  - electron 相关的其他文件(dll,exe,...)
  - resources\
    - app\
    - electron.asar
```

我们把资源文件夹 `resources\` 下的 `electron.asar` 和 `app` 拷贝到，`miniblink` 的 `resources\` 下。

``` text
- D:\myApp\
  - node.dll
  - mini-electron.exe
  - resources\
    - miniblink.asar\
    - app\
    - electron.asar
```

到这一步，可以打开 `mini-electron.exe` ，从 `miniblink` 中打开应用程序了。我们继续优化。

### 3.4 优化应用程序

1. 修改应用程序名称。如：把 `mini-electron.exe` 改为 `DesktopNaotu.exe`
2. 修改图标和文件信息。通过 `reshacker` 来修改，360 可能会提示病毒操作，全部允许即可。
3. 完成，我把示例程序放到 `release` 中，感兴趣的可以下载查看。