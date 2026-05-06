# Wayland适配笔记
## WM选择问题
根据现有的工具链和软件包，最好选择`deepin-kwin_wayland`会话而不是当前的Mutter作为WM。

举个例子，GXDE截图在Wayland下会依赖KWayland，否则不会工作。
