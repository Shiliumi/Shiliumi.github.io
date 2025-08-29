# 头像更换说明

## 如何更换头像

1. **准备头像图片**
   - 建议使用正方形图片（如 200x200 像素）
   - 支持格式：`.webp`, `.jpg`, `.png`, `.gif`
   - 推荐使用 `.webp` 格式以获得更好的加载速度

2. **上传头像文件**
   - 将您的头像文件重命名为 `avatar.webp`（或其他支持的格式）
   - 将文件放入 `static/avatar/` 目录

3. **更新配置**
   - 打开 `config/_default/params.yml` 文件
   - 找到 `avatar:` 配置项（约第49行）
   - 修改为您的头像文件名，例如：
     ```yaml
     avatar: "avatar/avatar.webp"
     ```

4. **重新构建网站**
   - 推送更改到 GitHub
   - GitHub Actions 会自动重新构建并部署您的网站

## 示例

如果您的头像文件名为 `my-photo.jpg`，那么：

1. 将文件放入 `static/avatar/my-photo.jpg`
2. 在 `params.yml` 中设置：
   ```yaml
   avatar: "avatar/my-photo.jpg"
   ```

## 注意事项

- 头像文件路径是相对于 `static/` 目录的
- 文件大小建议控制在 100KB 以内
- 确保图片清晰度适中，避免过大的文件影响加载速度
