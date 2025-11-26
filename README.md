# 🛠️ PCB 交互式焊接助手 (PCB Interactive Soldering Helper)

这是一个轻量级、纯前端的 PCB 焊接辅助工具。它能够读取 PCB 设计软件导出的坐标文件（Excel 或 CSV），在网页上生成交互式的 2D 视图，辅助工程师进行样板焊接和贴片。


## ✨ 主要功能

*   **多格式支持**：支持直接导入 **Excel (.xlsx, .xls)** 和 **CSV/TXT** 坐标文件。
*   **智能图形渲染**：
    *   不只是简单的方框，能根据封装名称智能绘制 **SOT-23 (3/5/6脚)**、**SOP**、**QFP**、**阻容感**、**圆柱插件**等形状。
*   **双面焊接支持**：
    *   支持 **顶层 (Top)** 和 **底层 (Bottom)** 快速切换。
    *   切换到底层时，视图会自动进行**水平镜像翻转**，模拟真实的翻板查看体验。
*   **交互式操作**：
    *   **PC端**：鼠标滚轮缩放、拖拽平移。
    *   **移动端**：完美适配手机/平板，支持双指捏合缩放、单指拖动。
    *   **双向定位**：点击左侧列表高亮图上元件，点击图上元件高亮左侧列表。
*   **信息详情**：底部面板显示选中元件的详细信息（位号、值、Name/备注、封装、坐标、角度）。
*   **纯前端运行**：无需后台服务器，数据只在浏览器本地处理，安全保密。

## 📋 数据文件要求

本工具支持大部分 EDA 软件（如 Altium Designer, Protel, KiCad, 立创EDA等）导出的**坐标文件 (Pick and Place)**。

为了确保最佳识别效果，请确保你的 Excel/CSV 包含以下列名（程序会自动模糊匹配，不区分大小写）：

| 关键列 | 说明 | 示例列名 |
| :--- | :--- | :--- |
| **Ref** (必选) | 元件位号 | `Designator`, `Ref`, `Component` |
| **X** (必选) | X轴坐标 | `Mid X`, `Center X`, `X (mm)` |
| **Y** (必选) | Y轴坐标 | `Mid Y`, `Center Y`, `Y (mm)` |
| **Rotation** | 旋转角度 | `Rotation`, `Angle`, `Rot` |
| **Layer** | 层级信息 | `Layer`, `Side` (识别 T/Top 或 B/Bottom) |
| **Value** | 元件值 | `Value` |
| **Name** | 元件型号/备注 | **`Name`**, `Comment`, `Device`, `备注` |
| **Footprint** | 封装名称 | `Footprint`, `Package` |

> **注意**：程序会优先读取 `Name` 列作为备注显示；如果没有 `Name`，则尝试读取 `Comment` 或 `Device`。

## 🚀 如何使用

### 方法一：在线/本地直接打开
1.  下载本项目中的 `index.html` 文件。
2.  确保电脑联网（因为需要加载 SheetJS CDN 解析 Excel）。
3.  双击用浏览器（Chrome, Edge, Safari）打开即可。

### 方法二：部署到 GitHub Pages (推荐)
1.  将 `index.html` 上传到你的 GitHub 仓库。
2.  在仓库 Settings -> Pages 中开启服务。
3.  使用生成的链接，即可在手机、平板上随时随地访问。

### 方法三：离线使用
如果需要在无网络环境使用，请下载 `xlsx.full.min.js` 文件放在同级目录，并修改 HTML 头部引用：
```html
<!-- 把这一行 -->
<script src="https://cdn.sheetjs.com/xlsx-0.20.1/package/dist/xlsx.full.min.js"></script>
<!-- 改为 -->
<script src="./xlsx.full.min.js"></script>
```

## 🎮 操作指南

*   **导入文件**：点击左上角“📂 导入 Excel / CSV”。
*   **切换层级**：在左侧面板选择 “顶层” 或 “底层”。
*   **切换显示**：选择显示 “参数” (Value/Name) 或 “位号” (Ref)。
*   **搜索**：在搜索框输入位号（如 `R1`）或型号（如 `10k`），列表会自动过滤。
*   **复位视图**：如果找不到板子了，点击右上角“全屏适应”按钮。

## 🛠️ 技术栈

*   **HTML5 / CSS3 / JavaScript (ES6)**
*   **Canvas API**：高性能图形渲染。
*   **SheetJS (xlsx)**：强大的 Excel 文件解析库。

## 📝 许可证

MIT License. 只有 HTML 源码是开源的，你导入的 PCB 数据仅在本地浏览器运行，不会上传到任何服务器。

---

**Enjoy soldering! 🛠️**
