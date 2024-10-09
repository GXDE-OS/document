

# 坑

## DTK2 

* libdtkcore2其实是指向libdtkcore5的链接
* libdtkcore2-dev其实是依赖libdtkcore5-dev的空包
* libdtkwidget2会通过启动时候put环境变量的方式强制使用dlight主题

## startdde

* 文管和启动器启动应用的dbus在startdde而不是dde-daemon实现
* https://gitee.com/GXDE-OS/startdde 在测试前不可再推构建，默认session怀疑需要改deepin-desktop-schemas,改GXDE 入口无效，建议Kwin测试完毕之后再改，别一个一个改

## KWin

### 5.27

* 依赖deepin-app-service提供服务接口，需要dde-dconfig-daemon和editor配置
* dbus-wm要打开否则在dock上面滑动鼠标展示所有窗口功能会失效，控制中心也会失效
* /usr/share下的decoration.json **并不会** 生效
* （待测试）代码中指定的标题栏宽度 **不会** 随着缩放变化，几个像素就是几个像素

### 5.24

* dbus-wm要打开否则在dock上面滑动鼠标展示所有窗口功能会失效，控制中心也会失效
* /usr/share下的decoration.json **并不会** 生效
* 代码中指定的标题栏宽度 **不会** 随着缩放变化，几个像素就是几个像素