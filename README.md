# GXDE 文档

## 坑

### DTK2 

* libdtkcore2其实是指向libdtkcore5的链接
* libdtkcore2-dev其实是依赖libdtkcore5-dev的空包
* libdtkwidget2会通过启动时候put环境变量的方式强制使用dlight主题

### KWin

#### 5.27

* 依赖deepin-app-service提供服务接口，需要dde-dconfig-daemon和editor配置

#### 5.24和以上

* dbus-wm要打开否则在dock上面滑动鼠标展示所有窗口功能会失效，控制中心也会失效
* /usr/share下的decoration.json **并不会** 生效