# macRDP

[English](#english) · [中文](#中文)

## English

macRDP is a free RDP server for your Mac's own desktop: connect from another computer and you
see and control the desktop that is logged in on the Mac, with its sound and clipboard. It is
free to use; the source is not published.

**Requirements**: a Mac with Apple Silicon. Tested on macOS 26 only (it asks for macOS 13 or
later). Intel Macs are not supported.

### Install

1. Download the newest `.dmg` from [Releases](https://github.com/keelos-dev/macRDP-releases/releases)
   and open it.
2. Drag **macRDP** into **Applications**.
3. Open macRDP from Applications and follow the dialogs:
   - choose a user name and password for RDP clients (this need not be your Mac account);
   - allow **Screen Recording** and **Accessibility** in System Settings → Privacy & Security.
     Accessibility is not switched on for you: turn on macRDP's switch in that list yourself.
     macOS 26 asks once more, on the first connection, whether macRDP may capture the screen and
     audio: allow it;
   - optionally turn on Remote Login (SSH), so kRDPclient can open a terminal on this Mac.
4. macRDP now runs in the background and starts at every login. Open the app again at any time
   for its status, a kRDPclient token, password change or uninstall.

### Which client

**kRDPclient is the recommended client**: https://github.com/keelos-dev/kRDPclient-releases
(Windows). In kRDPclient choose "Add keelOS host", enter the Mac's address and a token from the
macRDP app. It gets the picture as hardware-encoded H.264, plus sound and the clipboard.

mstsc (Remote Desktop Connection) and other standard RDP clients can connect too
(`mac-address:3389`, the user name and password you set), **but they have no H.264 channel**:
the picture goes as RemoteFX / bitmaps and is noticeably less smooth. If mstsc feels slow, try
kRDPclient before judging macRDP.

### Known limitations

- A user must be logged in on the Mac: at the login window (after a restart without automatic
  login) nobody can connect. Turn on automatic login in System Settings → Users & Groups.
- The Mac needs a display, or a dummy plug (HDMI headless adapter); with nothing attached macOS
  has no screen to capture.
- Clipboard: text only (no files or images).
- The mouse pointer is part of the picture; there is no client-side pointer yet.
- The RDP password is stored as plain text in a file only your account can read
  (`~/Library/Application Support/macRDP/credentials.json`). Do not reuse an important password.
- No automatic updates: download the new dmg from Releases, drag it over the old app, open it
  once.

### Update

Drag the new macRDP over the one in Applications, then open it: it restarts the background
service with the new version. If Screen Recording or Accessibility stops working afterwards,
switch macRDP off and on again in that list.

### Uninstall

1. Open macRDP and choose "Uninstall the login item".
2. Delete macRDP from Applications and the folder `~/Library/Application Support/macRDP`.
3. Optionally remove macRDP from Screen Recording and Accessibility in System Settings.

Remote Login (SSH) is a macOS setting and is left as it is; turn it off in System Settings →
General → Sharing if you no longer need it.

### Third-party software

macRDP is built on [IronRDP](https://github.com/Devolutions/IronRDP) (MIT / Apache-2.0) and
other open-source Rust crates. Their notices ship with every copy: `THIRD_PARTY.md`,
`LICENSE-IronRDP-MIT` and `THIRD_PARTY-crates.txt` are at the top of the dmg and in
`macRDP.app/Contents/Resources/`.

## 中文

macRDP 是一个免费的 Mac 用 RDP 服务端：从别的电脑连上来，看到、操作的就是这台 Mac 上当前登录
的那个桌面，带声音和剪贴板。免费使用，不开源。

**系统要求**：Apple Silicon 的 Mac。只在 macOS 26 上测过（最低要求 macOS 13）。不支持 Intel Mac。

### 安装

1. 从 [Releases](https://github.com/keelos-dev/macRDP-releases/releases) 下载最新的 `.dmg` 并打开。
2. 把 **macRDP** 拖进「**应用程序**」。
3. 从「应用程序」打开 macRDP，按对话框走：
   - 设一个给 RDP 客户端用的用户名和密码（不必和 Mac 的系统账号一样）；
   - 在「系统设置 → 隐私与安全性」里允许「**屏幕录制**」和「**辅助功能**」。
     「辅助功能」系统不会替你打开：要在列表里自己把 macRDP 的开关打开。
     macOS 26 第一次有人连上时还会再问一次「要采集屏幕和音频」，选允许；
   - 可选：打开远程登录（SSH），这样 kRDPclient 能直接开这台 Mac 的终端。
4. 之后 macRDP 在后台运行，每次登录自动启动。随时再打开 app 可以看状态、生成 kRDPclient
   token、改密码、卸载。

### 用什么客户端

**推荐 kRDPclient**：https://github.com/keelos-dev/kRDPclient-releases （Windows）。
在 kRDPclient 里「添加 keelOS 主机」，填 Mac 的地址和 macRDP app 生成的 token。画面走硬件
编码的 H.264，声音、剪贴板也都有。

mstsc（远程桌面连接）等标准 RDP 客户端也能连（`Mac地址:3389`，用你设的用户名和密码），
**但它们没有 H.264 通道**，画面走 RemoteFX / 位图，流畅度差一截。用 mstsc 觉得卡的话，
请先换 kRDPclient 试试。

### 已知限制

- Mac 上要有用户登录着：停在登录窗口（比如重启后没开自动登录）时连不上。建议在「系统设置 →
  用户与群组」里打开自动登录。
- Mac 要接着显示器，或者插一个假负载（HDMI 欺骗器）；什么都不接时 macOS 没有屏幕可抓。
- 剪贴板只有文本（不支持文件、图片）。
- 鼠标指针是画在画面里的，还没有客户端本地光标。
- RDP 密码以明文保存在只有你的账号能读的文件里
  （`~/Library/Application Support/macRDP/credentials.json`），别用重要的密码。
- 不自动更新：到 Releases 下载新的 dmg，拖进去覆盖旧的，再打开一次即可。

### 更新

把新的 macRDP 拖进「应用程序」覆盖旧的，再打开它：后台服务会换成新版本。之后如果屏幕录制或
辅助功能不起作用，在那个列表里把 macRDP 的开关关掉再打开。

### 卸载

1. 打开 macRDP，选「卸载自启」。
2. 删掉「应用程序」里的 macRDP 和文件夹 `~/Library/Application Support/macRDP`。
3. 可选：在「系统设置」的「屏幕录制」「辅助功能」里把 macRDP 删掉。

远程登录（SSH）是 macOS 自己的设置，卸载时不动它；不需要了就在「系统设置 → 通用 → 共享」里关掉。

### 第三方软件

macRDP 基于 [IronRDP](https://github.com/Devolutions/IronRDP)（MIT / Apache-2.0）和其他开源
Rust crate。它们的声明随每份副本一起发：dmg 根目录和 `macRDP.app/Contents/Resources/` 里的
`THIRD_PARTY.md`、`LICENSE-IronRDP-MIT`、`THIRD_PARTY-crates.txt`。
