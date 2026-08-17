# zhouseeie.github.io 博客结构模板

这是墨客项目提供的独立 Jekyll 文件模板。它不会被 App 自动上传，也不会在设置中初始化；请按需把文件手动复制到自己的博客仓库根目录。

目录和文件位置参考现有博客仓库：

```text
博客仓库根目录/
├── CNAME              # 可选：自定义域名；请使用你自己的内容
├── README.md          # 仓库说明，不是博客首页
├── _config.yml        # Jekyll 配置
├── _files/            # 图片等博客文件资源
├── _layouts/          # Jekyll 布局
│   ├── default.html
│   └── post.html
├── _includes/         # 可选页面片段
│   └── giscus.html     # GitHub Discussions 评论组件
├── _posts/            # 文章，文件名 YYYY-MM-DD-title.md
├── assets/
│   └── css/style.css  # 网站样式
├── index.md           # 博客首页，必须位于根目录
└── intro.html         # 个人主页/介绍页，位于根目录
```

约定：

- `README.md` 只写仓库说明，不代替 `index.md`。
- `index.md` 是网站首页，放在仓库根目录。
- `intro.html` 是个人主页/自我介绍页，放在仓库根目录。
- `_posts/` 只放带日期的文章。
- `_files/` 用于图片等博客文件资源；正文中使用相对路径引用。
- `_layouts/` 只放 Jekyll 布局，不能改名为 `layouts/`。
- `_includes/giscus.html` 是 GitHub Discussions 评论组件，只在文章详情页加载；评论配置未填写完整前不会输出评论组件。
- 评论默认关闭。需要评论时，在 GitHub 仓库启用 Discussions，然后访问 [giscus.app](https://giscus.app/) 选择仓库和分类，复制生成的 `repo-id`、`category-id` 等值到 `_config.yml`，最后将 `comments.enabled` 改为 `true`。
- giscus 要求博客仓库公开并启用 GitHub Discussions；访客需要使用 GitHub 账号登录后才能发表评论。评论、回复、删除、隐藏、锁定和审核都在 GitHub Discussions 中完成。
- 推荐使用 `mapping: pathname`，它会把每篇文章的页面路径绑定到对应 Discussion；不要随意改变文章 URL，否则可能生成新的讨论串。
- 站长删除评论时，直接打开对应的 GitHub Discussion，在评论菜单中删除或隐藏；需要停止继续评论时可以锁定整个 Discussion。
- `CNAME` 不在模板中提供占位内容，避免误配置；有自定义域名时再复制你自己的 CNAME。

网站视觉样式只在 `assets/css/style.css` 中维护：黑白、宋体/serif、文字为主、无阴影无圆角、细分割线。

## 文字排版设置

在 `_config.yml` 的 `typography` 中调整博客正文：

```yaml
typography:
  writing_mode: horizontal-tb # 横排；也可用 vertical-rl 或 vertical-lr
  text_orientation: mixed      # 竖排时中西文方向
  letter_spacing: 0em          # 字符间距，例如 0.02em 或 -0.01em
  line_height: 1.9             # 行距
  content_width: 1440px         # 页面正文最大宽度
```

`writing_mode: vertical-rl` 会让文章正文从右向左竖排，`vertical-lr` 会从左向右竖排；导航、页脚和评论区仍保持横向，避免整页操作困难。修改后重新构建 Jekyll 网站即可生效。