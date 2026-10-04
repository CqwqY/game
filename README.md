# 花草中学 · 官网

单文件官网（`index.html`），挂在 GitHub Pages：<https://game.caiyz.dpdns.org>

## 改内容

**所有文案、下载链接、图标都在 `index.html` 顶部的 `SITE` 对象里**，不用改 HTML 结构：

| 字段 | 管什么 |
| --- | --- |
| `name` / `lede` / `version` / `updated` | 站名、副标题、版本号、更新时间 |
| `android.url` | 安卓 APK 直链（留空按钮显示「准备中」） |
| `web.url` | 网页版地址 |
| `shot.src` / `shot.alt` / `shot.caption` | 首屏下方的游戏截图 |
| `features[]` | 特色卡片（`icon` 字段填 24×24 的 SVG 内部内容） |
| `steps[]` | 安卓安装说明步骤 |

## 图片

`assets/` 下的图都是 WebP：

- `screenshot.webp`（1600px 宽）—— 首屏大图
- `screenshot-thumb.webp`（960px 宽）—— 分享卡片（`og:image`）

⚠ `og:image` 必须是**绝对 URL**，分享平台不解析相对路径。换域名时记得同步改
`SITE.shot.thumb` 与 `<meta property="og:image">`，并更新根目录 `CNAME`。

## 换游戏截图

```bash
# 从截图生成两种尺寸（WebP 体积约为 PNG 的 1/13）
python -c "from PIL import Image; im=Image.open('shot.png').convert('RGB'); \
im.resize((1600,536), Image.LANCZOS).save('assets/screenshot.webp','WEBP',quality=82,method=6); \
im.resize((960,322),  Image.LANCZOS).save('assets/screenshot-thumb.webp','WEBP',quality=78,method=6)"
```

改完尺寸要同步改 `<img>` 的 `width`/`height` 属性（比例不对浏览器会先按错高度占位，加载完页面跳一下）。

## 其他文件

- `CNAME` — 自定义域名（`game.caiyz.dpdns.org`），别删
- `app-debug.apk` — 安卓安装包
- `0bf956ae6cd31621a7d2702edcf72f91.txt` — 校验文件，保留
