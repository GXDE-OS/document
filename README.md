# Tips

[缩写对照](./缩写对照表.md)

## 添加 文件管理器菜单

Spec: https://gitee.com/shenmo7192/dde-file-manager-menu-oem

也支持： https://blog.shenmo.tech/post/%E5%9C%A8%E6%B7%B1%E5%BA%A6%E6%96%87%E7%AE%A1%E7%9A%84%E8%BE%83%E4%B8%8A%E7%AB%AF%E5%8A%A0%E5%85%A5%E8%8F%9C%E5%8D%95%E9%A1%B9%E5%92%8C%E5%9C%A8%E6%96%87%E7%AE%A1%E9%A6%96%E9%A1%B5%E6%B7%BB%E5%8A%A0desktop/

## GXDE-Terminal

* 终端里存的远程管理ip和密码在 ~/.config/deepin/deepin-terminal/server-config.conf

## Dtk5紧凑模式

* `D_DTK_SIZEMODE=1 `

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

## dde-daemon

* Go 写的，看不懂，改不动，不敢动
* 新接口请加到 https://gitee.com/GXDE-OS/gxde-daemon ，尽量别碰dde-daemon


## libdmr/libgxmr

单独维护了gxde-movie,文管等依赖改为libgxmr,引入项目也使用libgxmr

但是使用的命名空间还是dmr,函数也用dmr开头

## KWin

### 5.27

* 依赖deepin-app-service提供服务接口，需要dde-dconfig-daemon和editor配置
* 在dock上面滑动鼠标展示所有窗口功能失效
* /usr/share下的decoration.json **并不会** 生效


### 5.24

* dbus-wm要打开否则在dock上面滑动鼠标展示所有窗口功能会失效，控制中心也会失效
* /usr/share下的decoration.json **并不会** 生效
* 代码中指定的标题栏宽度 **不会** 随着缩放变化，几个像素就是几个像素