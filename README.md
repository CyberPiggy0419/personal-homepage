# 朱赫逍凌 · 个人主页 / Personal Homepage

一个可直接部署到 **GitHub Pages** 的静态个人主页：中英双语切换、浅色/深色主题、主页展示简历信息，第二页展示图片。纯 HTML/CSS/JS，无构建步骤、无外部依赖。

打开 `index.html` 即可预览（双击也行，file:// 下功能完整）。

---

## 一、文件结构 / Files

```
personal-homepage/
├── index.html            站点本体：两个页面（主页 / 图片）、双语、主题、路由
├── site.config.js        ← 只改这里就能接入你的 GitHub
├── assets/
│   ├── peppa-pig.png     小猪佩奇原图（1700×1360，来自桌面「小猪佩奇」文件夹）
│   ├── peppa-pig.webp    同图的 WebP 版（网页优先加载它）
│   └── favicon.png       浏览器标签页图标（从原图裁出的猪头）
├── .nojekyll             告诉 GitHub Pages 不要用 Jekyll 处理（保留即可）
└── README.md
```

## 二、先填配置 / Configure

打开 `site.config.js`：

```js
window.SITE_CONFIG = {
  githubUsername: "your-github-username", // ← 必填：你的 GitHub 用户名
  githubRepo: "personal-homepage",        // 仓库名；用 <用户名>.github.io 时填 ""
  email: "gezell1q@sjtu.edu.cn",
  showPhone: true,                        // 公开网页不想显示手机号就改成 false
  siteUrl: ""                             // 可选，例如 "https://xxx.github.io/"
};
```

填好 `githubUsername` 后，页面上所有 GitHub 链接（顶部按钮、页脚）自动指向你的主页。
**注意**：手机号会公开显示在页面上，不想公开把 `showPhone` 改成 `false` 即可。

## 三、部署到 GitHub Pages / Deploy

### 方式 A：项目仓库（地址形如 `https://<用户名>.github.io/personal-homepage/`）

```bash
cd personal-homepage
git init
git add .
git commit -m "Add personal homepage"
git branch -M main
git remote add origin https://github.com/<你的用户名>/personal-homepage.git
git push -u origin main
```

推送后：仓库 → **Settings → Pages** → Source 选 `Deploy from a branch`，Branch 选 `main` / `(root)`，Save。
等 1~2 分钟，访问 `https://<你的用户名>.github.io/personal-homepage/`。
（此方式下 `site.config.js` 的 `githubRepo` 保持 `"personal-homepage"`。）

### 方式 B：用户主页（地址形如 `https://<用户名>.github.io/`）

仓库名必须叫 `<你的用户名>.github.io`，把文件放在**根目录**：

```bash
cd personal-homepage
git init
git add .
git commit -m "Add personal homepage"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<你的用户名>.github.io.git
git push -u origin main
```

然后访问 `https://<你的用户名>.github.io/`。此方式下 `site.config.js` 里 `githubRepo` 填 `""`。

### 方式 C：只想先本地看

直接双击 `index.html`，或者 `python -m http.server 8000` 后访问 http://127.0.0.1:8000/ 。

## 四、日常修改 / Editing

| 想改什么 | 改哪里 |
|---|---|
| 中英文字 | `index.html` 里：中文写在标签里，英文写在同一个标签的 `data-en="..."` 属性里，例如 `<p data-en="Education">教育背景</p>` |
| GitHub 用户名、邮箱、是否显示手机号 | `site.config.js` |
| 图片页的图片 | `index.html` 底部脚本里的 `pictures` 数组，照着加一项：`{ webp, png, w, h, zh, en, note, altZh, altEn }`（`webp` 可省） |
| 配色 | `index.html` 顶部 `<style>` 的 `:root` 变量（`--accent` 是交大红 `#9e1b32`） |

加新图片时把文件丢进 `assets/`，然后在 `pictures` 数组里补一项即可；只有一张图时会自动放大显示，多张会自动排成网格。

## 五、功能说明 / Features

- **双语切换**：右上角 `中 / EN`，选择记在 localStorage；也支持链接直达 `?lang=en`、`?lang=zh`。
- **深浅主题**：右上角太阳/月亮按钮，默认跟随系统，选择记在 localStorage；支持 `?theme=dark` / `?theme=light`。
- **两个页面**：`#/home`（简历主页）与 `#/gallery`（图片页），浏览器前进/后退可用。
- **图片放大**：图片页点击图片全屏查看，`Esc` 或点空白关闭。
- **响应式**：320px ~ 桌面宽度均已验证无横向溢出；移动端按钮≥44px 可点。
- **无障碍**：键盘可操作，焦点可见，`prefers-reduced-motion` 下关闭动画，跳转到正文链接。
- **SEO/分享**：`<title>` 与描述随语言/页面切换自动更新。

## 六、隐私提醒 / Privacy note

这是**公开**网页：手机号、出生日期、政治面貌、院校等信息都会被搜索引擎和任何人看到。
若之后要隐藏某一项，删除 `index.html` 里对应的那一行即可（手机号也可用 `site.config.js` 的 `showPhone: false` 一键隐藏）。
