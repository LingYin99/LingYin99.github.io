# GitHub 个人主页设置操作手册

本项目是一套纯静态网站，不需要服务器或数据库。GitHub Pages 会直接发布仓库中的 `HTML`、`CSS`、`JavaScript`、图片和 PDF 文件。

## 一、发布方式选择

推荐使用“用户主页仓库”：

- GitHub 用户名假设为 `yourname`
- 仓库必须命名为 `yourname.github.io`
- 发布后的主页地址为 `https://yourname.github.io/`
- 每个 GitHub 账号只能有一个这种用户主页

也可以使用普通项目仓库，例如仓库名为 `academic-homepage`：

- 发布地址为 `https://yourname.github.io/academic-homepage/`
- 一个账号可以发布多个项目站点

本项目全部使用相对路径，两种方式都可以正常工作。建议个人主页采用第一种。

## 二、发布前检查

确认 `github主页` 文件夹至少包含：

```text
index.html
models.html
.nojekyll
assets/
  css/style.css
  js/main.js
  images/
  papers/
```

在 PowerShell 中进入项目目录并本地预览：

```powershell
cd "D:\E\科研\网站整理\github主页"
python -m http.server 8000
```

浏览器打开：

```text
http://localhost:8000/
```

按 `Ctrl+C` 停止本地服务器。

## 三、在 GitHub 创建仓库

1. 登录 GitHub。
2. 点击右上角 `+`，选择 `New repository`。
3. 仓库名填写 `<你的GitHub用户名>.github.io`。
4. 建议选择 `Public`。
5. 不要勾选自动创建 README、`.gitignore` 或 License，避免首次推送冲突。
6. 点击 `Create repository`。

## 四、上传本地网站

将下方 `<你的GitHub用户名>` 替换为真实用户名，然后在 PowerShell 执行：

```powershell
cd "D:\E\科研\网站整理\github主页"
git init
git branch -M main
git add .
git commit -m "Initial academic homepage"
git remote add origin https://github.com/<你的GitHub用户名>/<你的GitHub用户名>.github.io.git
git push -u origin main
```

如果 Git 尚未配置姓名和邮箱，先执行：

```powershell
git config --global user.name "你的姓名或GitHub用户名"
git config --global user.email "你的GitHub邮箱"
```

如果使用 SSH，将远程地址改为：

```powershell
git remote add origin git@github.com:<你的GitHub用户名>/<你的GitHub用户名>.github.io.git
```

## 五、启用 GitHub Pages

1. 打开刚创建的 GitHub 仓库。
2. 点击仓库顶部的 `Settings`。
3. 在左侧 `Code and automation` 中点击 `Pages`。
4. 在 `Build and deployment` 下，将 `Source` 设为 `Deploy from a branch`。
5. `Branch` 选择 `main`。
6. 文件夹选择 `/(root)`。
7. 点击 `Save`。

首次发布通常需要等待数分钟。完成后，Pages 设置页会显示网站地址：

```text
https://<你的GitHub用户名>.github.io/
```

## 六、后续更新网站

每次修改并本地检查后，执行：

```powershell
cd "D:\E\科研\网站整理\github主页"
git status
git add .
git commit -m "Update homepage content"
git push
```

推送到 `main` 后，GitHub Pages 会自动重新发布。一般不需要再次修改 Pages 设置。

## 七、当前页面入口

- `index.html`：个人简介、工作与学习经历、代表性论文
- `models.html`：开源模型库
- `assets/css/style.css`：全站样式
- `assets/js/main.js`：手机端导航
- `assets/images/profile/ling-yin-web.jpg`：网页使用的轻量个人照片
- `assets/images/profile/ling-yin.jpg`：高清原图，仅本地保留，已通过 `.gitignore` 排除

## 八、常见问题

### 1. 打开网站显示 404

- 检查仓库名是否严格为 `<用户名>.github.io`。
- 检查 Pages 发布分支是否为 `main`，目录是否为 `/(root)`。
- 检查仓库根目录是否存在小写的 `index.html`。
- 首次发布后等待几分钟再刷新。

### 2. 页面能打开，但图片或样式丢失

- GitHub Pages 区分文件名大小写，`Photo.jpg` 和 `photo.jpg` 是两个文件。
- 不要使用 `D:\...` 形式的本机绝对路径。
- 页面中应使用 `assets/...` 形式的相对路径。
- 上传时必须把整个 `assets` 文件夹一并提交。

### 3. 点击模型页后地址错误

当前页面使用 `models.html` 和 `index.html#profile` 等相对链接，个人主页仓库和普通项目仓库都可以正常跳转。不要把它们改成以 `/` 开头的站点根路径。

### 4. 修改后网站没有更新

- 确认修改已经执行 `git add`、`git commit` 和 `git push`。
- 打开仓库的 `Actions` 或 `Settings → Pages` 检查部署状态。
- 浏览器使用 `Ctrl+F5` 强制刷新缓存。

### 5. 照片加载较慢

页面已使用 1200 像素高的轻量照片，高清原图仅在本地保留，不会随普通 `git add .` 上传。

### 6. 是否需要购买域名

不需要。GitHub 免费提供 `github.io` 地址。如果以后需要自定义域名，可以在 `Settings → Pages → Custom domain` 中配置。

## 九、发布前最终核对

- 首页三个模块内容完整。
- 39 篇代表性论文编号正确。
- 邮箱、Google Scholar、论文和 GitHub 链接可以打开。
- 个人照片和三个单位徽标正常显示。
- 7 个模型卡片都有名称、简介、图片和 GitHub 链接。
- 电脑和手机页面均无横向滚动条。
- 仓库中不存在密码、令牌或其他隐私文件。
