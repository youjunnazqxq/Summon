# Summon

<p align="center"><img src="assets/brand/summon-128.png" alt="Summon 图标" width="96" /></p>

Summon 是面向 Windows 的常驻桌面工具，把应用启动、文件与网站入口、剪贴板历史和常用文字备忘录集中到鼠标附近的轮盘菜单中。

按下快捷键，移动鼠标选择方向，点击即可打开目标。菜单支持自定义层级、拖动操作和轻微的移动／按压反馈。

## 下载与安装

前往 [Releases](https://github.com/youjunnazqxq/Summon/releases) 下载 `Windows Pie Menu-0.1.0 Setup.exe`，双击安装。当前发布目标为 **Windows x64**，建议使用 Windows 10 或 Windows 11；macOS、Linux 和 Windows ARM64 尚未提供安装包。

安装包暂时保留内部产品名 `Windows Pie Menu`，界面与托盘显示 Summon。

## 主要功能

| 功能 | 用途 |
| --- | --- |
| 轮盘启动器 | 按方向选择应用、网站、URI、文件、文件夹或内置功能，支持多级子菜单。 |
| 菜单编辑器 | 在设置中调整名称、图标、顺序和层级，拖动整理菜单，管理启用状态。 |
| 剪贴板历史 | 保存复制的文本、图片与文件，搜索、收藏、置顶并恢复到系统剪贴板。 |
| 文字备忘录 | 管理常用文字，支持标签、缩写调用、搜索、记录颜色和内容隐藏。 |
| 快捷键与外观设置 | 录制快捷键、调整轮盘尺寸和动效，配置剪贴板采集及保留策略。 |

## 快速开始

1. 启动 Summon，确认系统托盘中出现应用图标。
2. 按 **Ctrl + Space** 在鼠标所在位置呼出轮盘，也可单击托盘图标。
3. 移动鼠标选择方向，左键确认；外围图标之外的同一扇区也可选择。
4. 点击子菜单进入下一层，点击中心或父菜单返回节点返回；根菜单点击中心关闭轮盘。
5. 按 **Esc** 取消并关闭轮盘。关闭轮盘后应用继续常驻，退出请使用托盘右键菜单。
6. 通过轮盘的设置入口编辑菜单、调整快捷键和配置其他功能。

备忘录默认调用组合为 **Ctrl + Win**。先为标签设置缩写，在受支持的输入框中输入并确认缩写上屏，再按调用组合选择记录；无法可靠读取或插入时会打开管理窗口。输入法候选中的未确认拼音不作为缩写。

更完整的操作与数据说明见 [使用指南](docs/user-guide.md)。

## 数据说明

菜单、设置、剪贴板历史和备忘录保存在本机；安装包不包含开发者的个人记录。默认应用数据目录为 `%APPDATA%\Summon`，剪贴板可在设置中修改存储位置。Electron 缓存使用 `%APPDATA%\Windows Pie Menu`。

安装新版会继续读取本机已有数据。不要把安装或升级当作清空数据；删除数据目录会丢失相应记录。备忘录的内容隐藏用于界面遮挡，不能代替设备访问保护。

## 开发与构建

使用 Electron、Vue 3、TypeScript 和 Windows 原生 C# 辅助组件。开发需要 Windows x64、Node.js 22 或更新版本、npm，以及 Windows .NET Framework 的 C# 编译器：`%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\csc.exe`。

```powershell
npm ci
npm start
```

检查与构建：

```powershell
npm run typecheck
npm test
npm run package
npm run make
```

`package` 生成完整应用目录，`make` 生成 Windows 安装程序。编译原生组件前，请退出正在使用同一开发目录的 Summon 实例，避免文件被占用。

| 目录 | 内容 |
| --- | --- |
| `src/menu-renderer`、`src/menu` | 运行时轮盘、菜单模型与动作执行。 |
| `src/clipboard` | 剪贴板采集、持久化、恢复与面板。 |
| `src/text-memo` | 备忘录库、缩写调用与输入处理。 |
| `src/settings` | 设置、快捷键录制与菜单编辑。 |
| `src/main`、`src/preload`、`src/common` | 桌面窗口、托盘与共享接口。 |
| `native`、`tests`、`scripts` | Windows 辅助组件、测试和构建脚本。 |

## 当前版本

`v0.1.0` 为早期版本。轮盘的实际窗口验收覆盖单显示器、150% 显示缩放及多种轮盘尺寸；多显示器与其他 DPI 组合仍需进一步验证。不同应用和输入法对备忘录读取／插入的支持可能不同。

剪贴板当前不提供 OCR，Summon 不提供云同步。问题反馈请在 [Issues](https://github.com/youjunnazqxq/Summon/issues) 中说明版本、Windows 版本和复现步骤，并避免附上私人剪贴板或备忘录内容。
