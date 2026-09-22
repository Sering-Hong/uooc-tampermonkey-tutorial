# UOOC + Tampermonkey 开源使用教程

> 本教程介绍如何在 Chrome 中安装 Tampermonkey（篡改猴），安装并使用 Greasy Fork 上的 `UOOC assistant` 用户脚本，以及如何配置 OpenAI 兼容 API 进行辅助答题。
>
> 请遵守所在学校和课程的规则，自动填写答案后必须人工检查，不要盲目提交。

## 相关网站

| 用途 | 链接 |
| --- | --- |
| UOOC 优课联盟 | [https://www.uooc.net.cn/](https://www.uooc.net.cn/) |
| UOOC assistant 脚本页 | [Greasy Fork：UOOC assistant](https://greasyfork.org/zh-CN/scripts/413268-uooc-assistant) |
| 脚本原始安装地址 | [UOOC assistant.user.js](https://update.greasyfork.org/scripts/413268/UOOC%20assistant.user.js) |
| Tampermonkey Chrome 商店 | [Tampermonkey - Chrome Web Store](https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo) |
| Tampermonkey GitHub | [https://github.com/Tampermonkey/tampermonkey](https://github.com/Tampermonkey/tampermonkey) |
| Tampermonkey 官方文档 | [https://www.tampermonkey.net/documentation.php](https://www.tampermonkey.net/documentation.php) |
| Greasy Fork | [https://greasyfork.org/](https://greasyfork.org/) |

Chrome 商店扩展 ID：

```text
dhdgffkkebhmkfjojejmpbldmpobfkfo
```

## 一、准备工作

- Chrome 或其他 Chromium 浏览器
- Tampermonkey 5.x 或更高版本
- UOOC 账号，并登录课程页面
- 可选：OpenAI 兼容格式的 API Key

推荐从 Chrome Web Store 安装 Tampermonkey。

不要加载旧版 `manifest_version: 2` 的离线扩展包。Chrome 153 等新版本会提示：

```text
无法加载清单
不受支持的清单版本
```

这是旧版 MV2 扩展与新版 Chrome 不兼容，不是脚本文件损坏。

## 二、安装 Tampermonkey

1. 打开 [Tampermonkey Chrome 商店页面](https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)。
2. 核对扩展 ID 是否为 `dhdgffkkebhmkfjojejmpbldmpobfkfo`。
3. 点击“添加至 Chrome”。
4. 安装完成后，确认浏览器工具栏中出现 Tampermonkey 图标。
5. 打开 `chrome://extensions/`，确认 Tampermonkey 已启用。

建议在扩展详情页确认：

- 网站访问权限：允许访问所有网站，或至少允许 `www.uooc.net.cn`
- 用户脚本权限：已启用
- 扩展状态：已启用

## 三、安装 UOOC assistant

### 方法 A：通过 Greasy Fork

1. 打开 [UOOC assistant 脚本页](https://greasyfork.org/zh-CN/scripts/413268-uooc-assistant)。
2. 点击“安装此脚本”。
3. Tampermonkey 会显示脚本名称、版本和权限。
4. 确认名称为 `UOOC assistant`、版本为 `1.0.8` 后点击“安装”。

### 方法 B：打开原始脚本

如果 Greasy Fork 页面按钮没有反应，直接打开：

```text
https://update.greasyfork.org/scripts/413268/UOOC%20assistant.user.js
```

浏览器会自动交给 Tampermonkey 处理，然后点击“安装”。

### 检查安装结果

点击 Tampermonkey 图标，或打开：

```text
chrome-extension://dhdgffkkebhmkfjojejmpbldmpobfkfo/options.html#nav=dashboard
```

在“已安装脚本”中应能看到：

```text
UOOC assistant
```

确认脚本开关处于启用状态。

## 四、打开 UOOC 视频页面

脚本支持的地址格式包括：

```text
https://www.uooc.net.cn/home/learn/index*
https://www.uooc.net.cn/home/course/exam/*
https://www.uooc.net.cn/home/exam/*
https://www.uooc.net.cn/exam/*
```

例如：

```text
https://www.uooc.net.cn/home/learn/index#/1785941269/715389488/1639176130/2050742909/737231188/subsection
```

打开页面后刷新，等待课程内容和视频加载。正常情况下，页面顶部或视频区域附近会出现：

- 倍速
- 静音
- 播放
- 连播
- `⚙️` AI 设置
- LLM答题
- 开始答题

## 五、配置 AI 答题

1. 点击控制面板中的 `⚙️`。
2. 填写 `API Base URL`。
3. 填写 API Key。
4. 填写模型名称。
5. 点击保存。
6. 勾选“LLM答题”。

### Base URL 示例

脚本会自动在地址后追加 `/chat/completions`，所以 Base URL 必须包含 `/v1`：

```text
https://api.openai.com/v1
```

最终请求地址相当于：

```text
https://api.openai.com/v1/chat/completions
```

不同服务商的地址和模型名可能不同，请以服务商文档为准。

### 安全提醒

API Key 会保存在浏览器本地，并发送到你填写的 API 地址：

- 不要把 API Key 提交到 GitHub
- 不要把 API Key 写进 README
- 不要使用来路不明的 API 代理
- 建议为脚本单独创建受限额度的 Key

## 六、视频和测验使用

### 视频控制

脚本提供以下快捷键：

| 按键 | 功能 |
| --- | --- |
| `←` | 后退 10 秒 |
| `→` | 视频完成后前进 10 秒 |
| `↑` | 增加音量 |
| `↓` | 降低音量 |
| `空格` | 播放/暂停 |

“连播”开启后，当前视频结束后会尝试寻找下一个视频。

### LLM 答题

1. 进入 UOOC 测评页面。
2. 确认“LLM答题”已勾选。
3. 点击“🤖 开始答题”。
4. 等待脚本提取题目并填入答案。
5. 逐题检查答案。
6. 手动点击“提交试卷”。

脚本当前版本不会自动提交试卷，也不会自动处理所有分页题目。

### 视频内小测验

如果视频页面自带答案数据，脚本可能自动填写视频内出现的小测验。如果没有答案数据，脚本不会凭空生成答案。

## 七、故障排查

### 1. Tampermonkey 提示“不受信任的扩展程序”

优先从 Chrome Web Store 安装官方版本，不要绕过第三方扩展安全警告。

### 2. 加载离线扩展时提示“不支持的清单版本”

该包是旧版 MV2 扩展，与新版 Chrome 不兼容。使用 Chrome Web Store 中的 Tampermonkey 5.x。

### 3. 脚本已安装但页面没有控制面板

打开 UOOC 页面，按 `F12`，在 Console 中执行：

```js
({
  url: location.href,
  jquery: typeof $,
  learnHead: !!document.querySelector('.learn-head'),
  panel: !!document.getElementById('checkbox-container'),
  video: !!document.getElementById('player_html5_api')
})
```

结果含义：

- `jquery: "undefined"`：页面没有 jQuery，脚本可能一直等待。
- `learnHead: false`：页面结构已变化，脚本找不到旧版 `.learn-head`。
- `panel: true`：脚本已创建 UI，可能是面板被折叠或样式遮挡。
- `video: false`：当前还没有加载出视频播放器。

在 Console 筛选：

```text
UOOC助手
```

常见日志：

```text
[UOOC助手] 脚本开始加载...
[UOOC助手] 等待.learn-head元素...
[UOOC助手-AI] 开始提取题目...
```

如果一直停在“等待.learn-head元素”，说明脚本与当前 UOOC 页面结构不匹配。

### 4. 打开考试页后没有“开始答题”按钮

确认：

- 脚本已启用
- 当前 URL 属于脚本支持范围
- 页面已经完成加载
- Console 没有报错
- LLM答题已勾选
- API 配置已保存

如果脚本只在视频页创建控制按钮，而考试页没有按钮，需要根据当前页面结构调整脚本的初始化逻辑。

### 5. AI 请求失败

检查：

- Base URL 是否包含 `/v1`
- API Key 是否有效
- 模型名称是否存在
- 服务商是否允许浏览器跨域请求
- 账户是否有额度

## 八、GitHub 开源仓库建议结构

如果要把本教程发布为 GitHub 开源仓库，建议使用以下结构：

```text
uooc-tampermonkey-tutorial/
├── README.md
├── LICENSE
├── docs/
│   ├── installation.md
│   ├── configuration.md
│   └── troubleshooting.md
└── scripts/
    └── uooc-assistant.user.js
```

`README.md` 可以直接使用本教程内容。

### 推荐仓库标题

```text
UOOC Tampermonkey Assistant Tutorial
```

### 推荐仓库简介

```text
UOOC 优课联盟 + Tampermonkey 用户脚本安装、配置与故障排查教程。
```

### 推荐标签

```text
uooc
tampermonkey
userscript
greasyfork
openai
chrome-extension
```

### 发布到 GitHub

```bash
git init
git add README.md
git commit -m "docs: add UOOC Tampermonkey tutorial"
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

请将 `<username>` 和 `<repo>` 替换为你的 GitHub 用户名和仓库名。

## 九、开源与免责声明

`UOOC assistant` 脚本元数据标注为 MIT License，作者为 `cc & wybbb1`，当前版本为 `1.0.8`。

发布教程或二次开发脚本时：

- 保留原作者信息
- 保留原始 License
- 不要上传 API Key、Cookie、课程数据或个人隐私
- 对修改内容明确标注
- 遵守 Greasy Fork、UOOC 和所在学校的服务条款

本教程仅用于技术学习和自动化操作说明，不保证 AI 答案正确，也不承担因自动提交、账号异常或课程违规造成的责任。
