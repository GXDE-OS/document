# Wayland适配笔记
## 现有XCB程序在Wayland上的适配问题
现有X11程序可能在Wayland上错综复杂，有可能其表现不尽人意是由几个库共同作用导致的，在排查时，建议同时排查以下库的源码：
* 当前要适配的Wayland窗体管理器的源码
* DTK2
  * gxde-qt5integration
  * dtk2widget
  * dde-qt6platform-plugins
* deepin-daemon
* GXDE API(可选）
* GXDE-WM-Shim（可选）
* DWayland相关（可选，通常不需要）
  * qt6-wayland
  * dwayland

举个例子：`gxde-desktop-panel`在Treeland下无法显示图标：
```
DTreelandPlatformInterface::iconThemeName()
  → 返回未初始化的 m_iconThemeName = ""
  → 原因: PersonalizationManager 竞态条件
    - initContext() 在 activeChanged 信号中调用
    - 如果 PersonalizationManager 在 DTreelandPlatformInterface 构造前已 active，
      信号在 connect() 之前已发射，initContext() 永远不会被调用
```

## WM选择问题
根据现有的工具链和软件包，最好选择`deepin-kwin_wayland`会话而不是当前的Mutter作为WM。

举个例子，GXDE截图在Wayland下会依赖KWayland，否则不会工作。
