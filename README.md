# 🧾 发票报销打印拼版工具

> 把出差报销的 PDF / 图片发票一次性拖进来，自动拼成每页 2 / 4 / 6 / 9 张，预览后一键打印。

**👉 [点击直接在线使用](http://39.101.172.168:8181/other/expense-report.html)** — 无需下载，浏览器打开即用（Cmd/Ctrl+点击可新标签页打开）

⭐ **觉得好用？给个 Star 支持一下！**

---

## ✨ 特性

| 功能 | 说明 |
|------|------|
| 📄 多格式支持 | PDF / JPG / PNG / WEBP / GIF / BMP 混合上传 |
| 📑 PDF 自动拆页 | 多页 PDF 自动拆成单张，逐张参与排版 |
| 🔢 灵活排版 | 1×2 / 2×2 / 2×3 / 3×3 预设，或自定义任意行列 |
| 🔄 自动旋转贴合 | 横版发票放进竖版单元格时自动旋转 90°，最大化利用纸面 |
| ✋ 拖拽排序 | 缩略图拖拽调整顺序，单张可旋转、删除 |
| 📐 纸张方向 | A4 纵向 / 横向一键切换 |
| 🎚️ 间距可调 | 0 / 2 / 4 / 6mm，分割线可开关 |
| 🖨️ 打印干净 | `@media print` 隐藏所有控件，只输出拼好的 A4 页 |
| 🔒 隐私安全 | 完全本地处理，发票不上传任何服务器 |

---

## 🚀 快速开始

**方式一：在线使用（推荐）**

http://39.101.172.168:8181/other/expense-report.html

**方式二：本地打开**

```bash
# 推荐 Chrome / Edge / Safari 最新版
open expense-report.html
```

---

## 📖 使用步骤

1. 把 PDF / 图片 **拖进上传区**，或点击选择文件
2. 顶部工具栏选 **每页张数、纸张方向、间距**
3. 文件列表里拖拽缩略图调整顺序，点 `↻` 旋转、`×` 移除
4. 下方 **实时预览**，所见即所得
5. 点「**打印**」，系统对话框里注意：
   - 边距选 → **无**
   - 页眉和页脚 → **取消勾选**
   - 缩放 → **默认** 或 **实际大小**

---

## 🔧 技术细节

<details>
<summary><b>依赖</b></summary>

唯一外部依赖是 [PDF.js](https://github.com/mozilla/pdf.js) `4.7.76`（ESM），通过 CDN 加载：
- `pdf.min.mjs` / `pdf.worker.min.mjs` → cdnjs
- `cmaps/` / `standard_fonts/` → jsdelivr npm 镜像

首次加载需联网，之后浏览器会缓存。
</details>

<details>
<summary><b>为什么用 PDF.js 4.x</b></summary>

中国「全电发票」（2022 年后）使用字体子集，PDF.js 3.x 渲染会丢字——背景、印章、二维码正常，文字消失。4.x 对嵌入字体编码支持显著改善。
</details>

<details>
<summary><b>CMap 配置</b></summary>

CJK PDF 需要 cMap 字符映射数据。通过 `cMapUrl` + `cMapPacked: true` + `standardFontDataUrl` 配置。注意 cdnjs 不提供 cmaps 目录（返回 403），需要走 jsdelivr。
</details>

<details>
<summary><b>渲染与打印优化</b></summary>

- 透明背景：渲染前 canvas 填白，避免 JPEG 导出时透明区变黑
- 分辨率：按目标 DPI 反推 scale（默认 200），clamp 长边 ≤ 12000px
- 输出格式：优先 PNG（文字锐利），> 8MB 时回落 JPEG 0.95
- 旋转：实时计算单元格 mm 尺寸，90°/270° 时交换 wrapper 宽高贴合
</details>

---

## 🌐 浏览器兼容性

| 浏览器 | 支持 |
|--------|------|
| Chrome / Edge（最新版） | ✅ |
| Safari（最新版） | ✅ |
| Firefox（最新版） | ✅ |
| IE / 旧版 Edge | ❌ |

---

## 🔒 隐私说明

- ✅ 完全在本地浏览器内运行，**发票不上传任何服务器**
- ✅ 无分析、无追踪、无埋点
- ✅ 仅从 CDN 加载 PDF.js 库（不发送 PDF 内容）
- ✅ `.gitignore` 默认排除 `*.pdf` 和图片，防止误提交

---

## ⚠️ 已知限制

- 部分 OFD 转 PDF 的发票若编码异常，文字可能渲染不完整 → 截图转 PNG 可绕过
- 几百张发票时数据 URL 可能过大导致打印卡顿 → 建议分批处理
- 浏览器原生打印无精确色彩管理 → 不建议用于需要色彩还原的票据

---

## ⭐ Star

如果这个工具帮你省了打印发票的时间，请点个 **Star** ⭐ 让更多人看到！

---

## 📄 License

MIT
