# Tips

小技巧（后续单独放一个官网页面）

* 在任务栏上对已经打开的应用图标滚动鼠标滚轮可以查看所有该应用的窗口
* win + A 展示全部窗口
* 热区很好用

新建模板包

`DEBFULLNAME=shenmo DEBEMAIL="shenmo@spark-app.store" dh_make -n -p $(basename $(pwd))_1.0.0 `

## [缩写对照](./缩写对照表.md)

## gxde-wm-shim 的作用

deepin-wm-dbus ，用来和 GXCC 的 快捷键设置 互动并提供值，用于 dde-dock 的对已打开应用滚轮的互动

kwin的本体在 gxde-kwin，基于 deepin-kwin 修改



## dde-qt-dbus-factory

并非上游版本，为了覆盖掉 Debian 13 的版本实际上是用6.0.0魔改版改版本号到了6.1.0

魔改内容： https://gitee.com/GXDE-OS/dde-qt-dbus-factory/commit/cc9db3d6e4beeb4b7eaae6ff97c9f3062a587795





## 添加 文件管理器菜单

Spec: https://gitee.com/shenmo7192/dde-file-manager-menu-oem



## GXDE-Terminal

* 终端里存的远程管理ip和密码在 ~/.config/deepin/gxde-terminal/server-config.conf

## Dtk5紧凑模式

* `D_DTK_SIZEMODE=1 `环境变量即可

## 全局背景配置位置

`/usr/share/backgrounds/GXDE/dtk2/global/background-" + theme`，~/.local 也会生效

# 坑

## DTK2 

* libdtkcore2其实是指向libdtkcore5的链接
* libdtkcore2-dev其实是依赖libdtkcore5-dev的空包
* libdtkwidget2会通过启动时候put环境变量的方式强制使用dlight主题
* Dtk2 bin在libdtkcore-bin，而dtk5的是libdtkcore5-bin,但是开发包是反过来的，libdtkwidget-dev是libdtkwidget5的，libdtkwidget2-dev才是dtk2的
* libdtkwidget2-dev会把Include装/usr/include/dtk5里
* 如果没有 gxde-qt5integration , Dtk2应用在有Dtk5的环境中会在退出时随机崩溃，所以开发的应用请依赖gxde-qt5integration

## startdde

* 文管和启动器启动应用的dbus在startdde而不是dde-daemon实现
* https://gitee.com/GXDE-OS/startdde 在测试前不可再推构建，默认session怀疑需要改deepin-desktop-schemas,改GXDE 入口无效，建议Kwin测试完毕之后再改，别一个一个改

## dde-daemon/deepin-daemon

* Go 写的，看不懂，改不动，不敢动，为了和dde-daemon区别，使用 deepin-daemon 名
* 新接口请加到 https://gitee.com/GXDE-OS/gxde-daemon ，尽量别碰dde-daemon


## libdmr/libgxmr

单独维护了gxde-movie,文管等依赖改为libgxmr,引入项目也使用libgxmr

但是使用的命名空间还是dmr,函数也用dmr开头

## KWin

### 6.0

* 依赖deepin-app-service提供服务接口，需要dde-dconfig-daemon和editor配置
* 在dock上面滑动鼠标展示所有窗口功能失效
* /usr/share下的decoration.json **并不会** 生效


### 5.24

* dbus-wm要打开否则在dock上面滑动鼠标展示所有窗口功能会失效，控制中心也会失效
* /usr/share下的decoration.json **并不会** 生效
* 代码中指定的标题栏宽度 **不会** 随着缩放变化，几个像素就是几个像素