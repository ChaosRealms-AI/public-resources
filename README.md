# Personal Image Hosting - 个人图床

📸 基于 GitHub API 的个人图床服务，支持拖拽上传、自动生成链接。

## ✨ 功能特性

- 🖼️ **拖拽上传** - 支持拖拽图片到上传区域
- 📋 **一键复制** - 自动生成并复制图片链接
- 📱 **移动端友好** - 响应式设计，支持手机访问
- 🔒 **Token 保存** - 本地保存 GitHub Token，无需重复输入
- 📂 **自动分类** - 按日期自动创建目录结构
- 🎨 **美观界面** - 现代化 UI 设计

## 🚀 在线访问

访问地址：[https://chaosrealms-ai.github.io/public-resources/](https://chaosrealms-ai.github.io/public-resources/)

## ⚙️ 使用步骤

### 1. 获取 GitHub Token
1. 访问：[https://github.com/settings/tokens](https://github.com/settings/tokens)
2. 点击 **"Generate new token"** → **"Generate new token (classic)"**
3. 设置权限：
   - ✅ **repo** (完整的仓库访问权限)
4. 复制生成的 token

### 2. 配置 Token
1. 打开图床网站
2. 在 Token 输入框中粘贴你的 GitHub Token
3. Token 会自动保存到本地浏览器

### 3. 上传图片
1. 拖拽图片到上传区域，或点击选择文件
2. 等待上传完成
3. 复制生成的图片链接

## 📁 目录结构

```
public-resources/
├── images/           # 上传的图片存储目录
│   ├── 2025-01-09/  # 按日期自动分类
│   └── ...
├── logos/           # 原有的 logo 资源
├── index.html       # 图床主界面
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
- **功能**: 拖拽上传、Base64 编码、GitHub API 调用

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
