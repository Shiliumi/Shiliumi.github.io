# 博客搜索功能配置说明

## 🔍 搜索功能已启用

您的博客已经成功配置了搜索功能！搜索按钮会出现在顶部导航栏的右侧。

## 📋 当前配置状态

### ✅ 已完成的配置：
1. **Hugo配置**：已启用Algolia输出格式
2. **搜索索引**：会自动生成`algolia.json`文件
3. **搜索界面**：已启用搜索按钮和搜索弹窗
4. **中文支持**：搜索界面已本地化

### 🔧 需要完善的配置：

目前使用的是演示配置，要获得完整的搜索功能，需要：

#### 1. 注册Algolia账号
- 访问 [Algolia官网](https://www.algolia.com/)
- 注册免费账号（每月10,000次搜索免费）

#### 2. 创建搜索索引
- 在Algolia控制台创建新的应用
- 创建搜索索引（例如：`blog_posts`）
- 获取Application ID和Search-Only API Key

#### 3. 更新配置文件
在`config/_default/params.yml`中更新：
```yaml
algolia_search:
  enable: true
  appID: "你的Application ID"
  apiKey: "你的Search-Only API Key"  # 注意：只能使用Search-Only Key！
  indexName: "你的索引名称"
  hits:
    per_page: 10
```

#### 4. 上传搜索数据
有几种方式上传搜索数据：

**方式1：使用atomic-algolia（推荐）**
```bash
npm install atomic-algolia
npx atomic-algolia
```

**方式2：使用GitHub Actions自动化**
创建`.github/workflows/algolia.yml`：
```yaml
name: Update Algolia Index
on:
  push:
    branches: [ main ]
jobs:
  algolia:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Upload to Algolia
        uses: wangchucheng/algolia-uploader@master
        with:
          app_id: ${{ secrets.ALGOLIA_APP_ID }}
          admin_key: ${{ secrets.ALGOLIA_ADMIN_KEY }}
          index_name: ${{ secrets.ALGOLIA_INDEX_NAME }}
          index_file_path: public/algolia.json
```

## 🎯 搜索功能特点

- **实时搜索**：输入即搜索，无需按回车
- **高亮显示**：搜索结果中关键词会高亮显示
- **多语言支持**：支持中文、日文、英文内容搜索
- **智能排序**：按相关性排序搜索结果
- **美观界面**：与博客主题完美融合的搜索界面

## 🚀 使用方法

1. **打开搜索**：点击导航栏右侧的搜索图标
2. **输入关键词**：在搜索框中输入要搜索的内容
3. **查看结果**：搜索结果会实时显示
4. **点击访问**：点击搜索结果跳转到对应文章

## 📝 注意事项

- 搜索索引会在每次Hugo构建时自动更新
- 只有发布的文章（draft: false）会被索引
- 搜索内容包括文章标题、内容、标签和分类
- 建议定期更新Algolia索引以保持搜索结果最新

## 🔒 安全提醒

- **绝对不要**在配置文件中使用Admin API Key
- **只能使用**Search-Only API Key
- **不要**将敏感密钥提交到公开的Git仓库
- 建议使用环境变量或GitHub Secrets存储密钥
