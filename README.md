# Personal Image Hosting - 个人图床

📸 基于 GitHub API 的个人图床服务，支持多种上传方式和自动生成链接。

## ✨ 功能特性

- 🖼️ **拖拽上传** - 支持拖拽图片到上传区域
- 📋 **粘贴上传** - 支持 Ctrl+V 粘贴剪贴板中的图片
- 📋 **一键复制** - 自动生成并复制图片链接
- 📱 **移动端友好** - 响应式设计，支持手机访问
- 🔒 **Token 保存** - 本地保存 GitHub Token，无需重复输入
- 📂 **自动分类** - 按日期自动创建目录结构
- 🎨 **美观界面** - 现代化 UI 设计
- 🔄 **动态图库** - 自动获取并展示所有上传的图片

## 🚀 在线访问

访问地址：[https://chaosrealms-ai.github.io/public-resources/](https://chaosrealms-ai.github.io/public-resources/)

## 📖 使用方法

### 方法1：拖拽上传
1. 直接将图片文件拖拽到上传区域
2. 支持多文件同时上传

### 方法2：点击选择
1. 点击上传区域选择图片文件
2. 支持多文件选择

### 方法3：粘贴上传
1. 复制图片到剪贴板（Ctrl+C 或右键复制）
2. 在页面任意位置按 Ctrl+V 粘贴
3. 支持从截图工具、浏览器、文件管理器等复制图片

## 🔧 API 上传方式

### 1. 获取 GitHub Token

首先需要创建 GitHub Personal Access Token：

1. 访问 [GitHub Settings > Tokens](https://github.com/settings/tokens)
2. 点击 "Generate new token (classic)"
3. 选择权限：`repo` (完整的仓库访问权限)
4. 生成并保存 Token

### 2. 使用 GitHub API 上传图片

#### 方法一：使用 curl 命令

```bash
# 上传单张图片
curl -X PUT \
  -H "Authorization: token YOUR_GITHUB_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "Upload image via API",
    "content": "BASE64_ENCODED_IMAGE_CONTENT"
  }' \
  https://api.github.com/repos/ChaosRealms-AI/public-resources/contents/images/2024-07-09/example.png
```

#### 方法二：使用 JavaScript

```javascript
// 上传图片函数
async function uploadImageToGitHub(imageFile, token) {
    const GITHUB_OWNER = 'ChaosRealms-AI';
    const GITHUB_REPO = 'public-resources';
    
    // 生成时间戳文件名
    const now = new Date();
    const timestamp = `${now.getFullYear()}${String(now.getMonth() + 1).padStart(2, '0')}${String(now.getDate()).padStart(2, '0')}_${String(now.getHours()).padStart(2, '0')}${String(now.getMinutes()).padStart(2, '0')}${String(now.getSeconds()).padStart(2, '0')}_${String(now.getMilliseconds()).padStart(3, '0')}`;
    
    const fileName = imageFile.name.replace(/\.[^/.]+$/, "") + "_" + timestamp + "." + imageFile.name.split('.').pop();
    const folder = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, '0')}-${String(now.getDate()).padStart(2, '0')}`;
    const filePath = `images/${folder}/${fileName}`;
    
    // 转换为 Base64
    const base64Content = await fileToBase64(imageFile);
    
    // 上传到 GitHub
    const response = await fetch(`https://api.github.com/repos/${GITHUB_OWNER}/${GITHUB_REPO}/contents/${filePath}`, {
        method: 'PUT',
        headers: {
            'Authorization': `token ${token}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            message: `Upload image: ${fileName}`,
            content: base64Content
        })
    });
    
    if (response.ok) {
        const data = await response.json();
        return `https://raw.githubusercontent.com/${GITHUB_OWNER}/${GITHUB_REPO}/main/${filePath}`;
    } else {
        throw new Error(`Upload failed: ${response.statusText}`);
    }
}

// Base64 转换函数
function fileToBase64(file) {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => {
            const base64 = reader.result.split(',')[1];
            resolve(base64);
        };
        reader.onerror = error => reject(error);
    });
}
```

#### 方法三：使用 Python

```python
import requests
import base64
from datetime import datetime
import os

def upload_image_to_github(image_path, token):
    GITHUB_OWNER = 'ChaosRealms-AI'
    GITHUB_REPO = 'public-resources'
    
    # 生成时间戳文件名
    now = datetime.now()
    timestamp = f"{now.year}{now.month:02d}{now.day:02d}_{now.hour:02d}{now.minute:02d}{now.second:02d}_{now.microsecond//1000:03d}"
    
    file_name = os.path.basename(image_path)
    name_without_ext = os.path.splitext(file_name)[0]
    ext = os.path.splitext(file_name)[1]
    new_file_name = f"{name_without_ext}_{timestamp}{ext}"
    
    folder = f"{now.year}-{now.month:02d}-{now.day:02d}"
    file_path = f"images/{folder}/{new_file_name}"
    
    # 读取并编码图片
    with open(image_path, 'rb') as f:
        content = base64.b64encode(f.read()).decode('utf-8')
    
    # 上传到 GitHub
    url = f"https://api.github.com/repos/{GITHUB_OWNER}/{GITHUB_REPO}/contents/{file_path}"
    headers = {
        'Authorization': f'token {token}',
        'Content-Type': 'application/json'
    }
    data = {
        'message': f'Upload image: {new_file_name}',
        'content': content
    }
    
    response = requests.put(url, headers=headers, json=data)
    
    if response.status_code == 201:
        return f"https://raw.githubusercontent.com/{GITHUB_OWNER}/{GITHUB_REPO}/main/{file_path}"
    else:
        raise Exception(f"Upload failed: {response.text}")

# 使用示例
token = "your_github_token_here"
image_path = "path/to/your/image.png"
try:
    url = upload_image_to_github(image_path, token)
    print(f"Upload successful: {url}")
except Exception as e:
    print(f"Upload failed: {e}")
```

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

## 📁 项目结构

```
public-resources/
├── index.html              # 图床主界面
├── README.md               # 项目说明文档
├── scripts/                # 图床相关脚本
│   ├── README.md          # 脚本说明
│   └── test-paste.html    # 粘贴功能测试页面
├── images/                 # 上传的图片存储目录
│   ├── 2024-07-09/        # 按日期自动分类
│   └── ...
├── logos/                  # 原有的 logo 资源
└── .github/               # GitHub 配置
```

## 🔗 图片访问格式

### 原始链接
```
https://raw.githubusercontent.com/ChaosRealms-AI/public-resources/main/images/2024-07-09/example_20240709_153012_123.png
```

### Markdown 格式
```markdown
![图片描述](https://raw.githubusercontent.com/ChaosRealms-AI/public-resources/main/images/2024-07-09/example_20240709_153012_123.png)
```

### HTML 格式
```html
<img src="https://raw.githubusercontent.com/ChaosRealms-AI/public-resources/main/images/2024-07-09/example_20240709_153012_123.png" alt="图片描述">
```

## 🛠️ 技术实现

- **前端**: HTML5 + CSS3 + JavaScript (ES6+)
- **存储**: GitHub API + GitHub Raw
- **部署**: GitHub Pages
- **功能**: 拖拽上传、粘贴上传、Base64 编码、GitHub API 调用、动态图库

## 📝 注意事项

- 单文件最大 100MB
- 仓库总大小建议不超过 1GB
- API 调用频率限制：5000次/小时（认证用户）
- 图片会按日期自动分类存储
- 文件名自动添加时间戳防止重复

## 🔧 自定义配置

如需修改 GitHub 用户名或仓库名，请编辑 `index.html` 中的配置：

```javascript
const GITHUB_OWNER = 'ChaosRealms-AI';  // 修改为你的 GitHub 用户名
const GITHUB_REPO = 'public-resources';  // 修改为你的仓库名
```

## 📄 许可证

此项目用于个人图床服务，请合理使用。
