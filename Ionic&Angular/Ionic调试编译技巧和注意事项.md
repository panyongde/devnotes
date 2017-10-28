# 添加插件遇到的问题

很多 native 插件都可以按照官方文档添加，比如定位插件：

```shell
$ cordova plugin add cordova-plugin-geolocation --variable GEOLOCATION_USAGE_DESCRIPTION="To locate you"
$ cnpm install --save @ionic-native/geolocation
```

但近段安装支付宝插件老是报错：

```
Error: Failed to fetch plugin git+https://github.com/pipitang/cordova-alipay-base.git via git.
Either there is a connection problems, or plugin spec is incorrect:
	Error: git: Command failed with exit code 128 Error output:
Cloning into '/tmp/git/1508832108216'...
fatal: Unable to find remote helper for 'git+https'

```

如果在后面家 `--nofetch` 就能成功，npm install 不行，就改为 cnpm install

```shell
$ ionic cordova plugin add cordova-alipay-base --variable ALI_PID=2017101209250000 --nofetch
$ cnpm install --save @ionic-native/alipay
```

如果不成功，直接从github安装：

```shell
cordova plugin add https://github.com/pipitang/cordova-alipay-base --variable ALI_PID=2017101209250000 --nofetch
$ cnpm install --save @ionic-native/alipay
```

# 调试和发布

## Android 调试和发布

要干净调试和和发布程序，先删掉 `node_modules`、 `platforms`、 `plugins` 和 `www` 四个文件夹。

然后执行以下命令：

```shell
# 生成 node_modules
$ cnpm install

# 生成 www
$ cnpm serve

# 生成 platforms 和 plugins
$ cordova platform add android --nofetch #必须用nofetch

# 模拟器或真机调试，需要县打开模拟器或插入真机，用以下命令测试是否找到
$ adb devices

# 模拟器或真机运行 app
$ cordova run android -l

# 发布 release 版本
# 1、把签名文件放到 platforms/android 目录下然后执行
$ cordova build android --release --prod
```

## Ios 调试和发布

要干净调试和和发布程序，先删掉 `node_modules`、 `platforms`、 `plugins` 和 `www` 四个文件夹。

然后执行以下命令

```shell
# 生成 node_modules
$ cnpm install

# 生成 www
$ cnpm serve

# 生成 platforms 和 plugins
$ cordova platform add ios --nofetch #必须用nofetch

# 模拟器或真机调试，目前还没解决

# 发布
# 修改 platforms/ios 目录为可读写权限
$ sudo chmod -R 777 platforms/ios

# 双击 xcode 项目文件，打开xcode
# 修改签名
# 发布机型为 General device
# 点击菜单 build-achieve 生成
```

## 添加平台执行时卡住或者出错可能的问题

因为添加平台需要远程下载插件，有时因为网络问题，比如加载国外资源（github等）比较慢，或者连接不上，都可能出现以上问题。解决方案时把更改 npm 使用国内的淘宝源。

```shell
# 检查目前 npm 使用的源，默认一般是官方源
$ npm conifg get registry
# 如果是官方源，会显示：https://www.npmjs.com/
# 更换为淘宝源
$ npm config set registry https://registry.npm.taobao.org
```

然后再执行添加平台的命令

```shell
$ cordova platform add android --nofetch #必须用nofetch
```

