# Personal Image Hosting - 个人图床

📸 基于 GitHub API 的个人图床服务，支持拖拽上传、自动生成链接。

## ✨ 功能特性

- 🖼️ **拖拽上传** - 支持拖拽图片到上传区域
- 📋 **粘贴上传** - 支持 Ctrl+V 粘贴剪贴板中的图片
- 📋 **一键复制** - 自动生成并复制图片链接
- 📱 **移动端友好** - 响应式设计，支持手机访问
- 🔒 **Token 保存** - 本地保存 GitHub Token，无需重复输入
- 📂 **自动分类** - 按日期自动创建目录结构
- 🎨 **美观界面** - 现代化 UI 设计

## 🚀 在线访问

访问地址：[https://chaosrealms-ai.github.io/public-resources/](https://chaosrealms-ai.github.io/public-resources/)

## 📖 使用方法

### 方法1：拖拽上传
1. 直接将图片文件拖拽到上传区域
2. 支持多文件同时上传

### 方法2：点击选择
1. 点击上传区域选择图片文件
2. 支持多文件选择

### 方法3：粘贴上传（新增功能）
1. 复制图片到剪贴板（Ctrl+C 或右键复制）
2. 在页面任意位置按 Ctrl+V 粘贴
3. 支持从截图工具、浏览器、文件管理器等复制图片


## ⚙️ 快速配置 Token

### 方法1：浏览器控制台（推荐）
1. 打开图床网站
2. 按 F12 打开开发者工具
3. 切换到 Console 标签
4. 复制并粘贴以下代码：

```javascript
(function() {
    const TOKEN = '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';
    const tokenInput = document.getElementById('github-token');
    if (tokenInput) {
        tokenInput.value = TOKEN;
        localStorage.setItem('github-token', TOKEN);
        alert('Token 已自动配置完成！');
    }
})();
```

### 方法2：手动配置
1. 访问：[https://github.com/settings/tokens](https://github.com/settings/tokens)
2. 创建具有 `repo` 权限的 Token
3. 在图床页面输入 Token

## 📁 目录结构

```
public-resources/
├── images/           # 上传的图片存储目录
│   ├── 2025-01-09/  # 按日期自动分类
│   └── ...
├── logos/           # 原有的 logo 资源
├── index.html       # 图床主界面
├── token-helper.js  # Token 配置助手脚本
└── README.md        # 项目说明
```

## 🔗 图片访问格式

### 原始链接
```
https://raw.githubusercontent.com/ChaosRealms-AI/public-resources/main/images/2025-01-09/example.png
```

### Markdown 格式
```markdown
![图片描述](https://raw.githubusercontent.com/ChaosRealms-AI/public-resources/main/images/2025-01-09/example.png)
```

### HTML 格式
```html
<img src="https://raw.githubusercontent.com/ChaosRealms-AI/public-resources/main/images/2025-01-09/example.png" alt="图片描述">
```

## 🛠️ 技术实现

- **前端**: HTML5 + CSS3 + JavaScript (ES6+)
- **存储**: GitHub API + GitHub Raw
- **部署**: GitHub Pages
- **功能**: 拖拽上传、粘贴上传、Base64 编码、GitHub API 调用

## 📝 注意事项

- 单文件最大 100MB
- 仓库总大小建议不超过 1GB
- API 调用频率限制：5000次/小时（认证用户）
- 图片会按日期自动分类存储

## 🔧 自定义配置

如需修改 GitHub 用户名或仓库名，请编辑 `index.html` 中的配置：

```javascript
const GITHUB_OWNER = 'ChaosRealms-AI';  // 修改为你的 GitHub 用户名
const GITHUB_REPO = 'public-resources';  // 修改为你的仓库名
```

## 📄 许可证

此项目用于个人图床服务，请合理使用。
