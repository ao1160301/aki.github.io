一、准备工作
---
创建 `GitHub`账户和仓库：
如果没有 **GitHub **账户，访问 [github.com](https://github.com/) 注册。
登录后，点击右上角的` “+”` 号，选择 `New repository`。
填写仓库名称（如 `media-hosting`），选择公开（`Public`）或私有（`Private`），勾选` Add a README file`，然后点击 `Create repository`。
支持的文件格式：
视频：推荐 `MP4（H.264 编码），也支持 MOV、WebM`。
音乐：推荐 `MP3，也支持 WAV、OGG`。
建议优化文件大小**（视频 <25MB，音频 <10MB）**，以减少加载时间。
工具（可选）：
视频压缩：**HandBrake（免费）**。
音频压缩：**Audacity（免费）**。
文本编辑器（如` VS Code`）用于编写` HTML` 文件。

---

## 二、视频文件预览的详细操作步骤

### 方法 1：通过``` GitHub Pages ``预览视频
上传视频文件：
打开你的 GitHub 仓库页面（例如** https://github.com/username/media-hosting**）。
点击 `Add file` > `Upload files`。
拖放或选择你的视频文件（如 `my-video.mp4`），上传后点击 `Commit changes`（可保留默认提交信息）。
**如果文件较大（>50MB），需使用 Git LFS：
安装 Git LFS（参考 [Git LFS 官网](https://git-lfs.github.com/)）。**
在本地仓库运行：

```bash
git lfs install
git lfs track "*.mp4"
git add .gitattributes my-video.mp4
git commit -m "Add video with LFS"
git push origin main
```

创建 `HTML` 文件用于预览：
在仓库页面，点击 `Add file `> `Create new file`。
文件名命名为` index.html`，输入以下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video Preview</title>
</head>
<body>
    <h1>My Video</h1>
    <video controls width="600">
        <source src="my-video.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
</body>
</html>
```
---

如果使用了` Git LFS`，`src` 需要改为 `LFS` 的` Raw `链接，例如：

```html
<source src="https://media.githubusercontent.com/media/username/media-hosting/main/my-video.mp4" type="video/mp4">
```

点击 `Commit new file`（选择直接提交到 `main `分支）。
启用 GitHub Pages：
进入仓库，点击 `Settings `> 左侧菜单的` Pages`。
在 `Source `下，选择分支为` main`，文件夹为` / (root)`，点击` Save`。
等待几分钟，`GitHub `会生成一个 `URL`（如 **https://username.github.io/media-hosting/**）。
访问预览：
打开生成的` GitHub Pages` 链接，页面会显示视频播放器，支持播放、暂停、音量调节等。
如果视频不播放，检查：
文件路径是否正确（`my-video.mp4` 需与仓库中一致）。
浏览器是否支持格式（推荐` Chrome `或` Firefox`）。
LFS 文件是否正确引用了` media.githubusercontent.com` 链接。
### 方法 2：通过 Raw 链接预览视频
获取视频的 Raw 链接：
在仓库页面，点击视频文件（如 my-video.mp4）。
点击右上角的 Raw 按钮，浏览器会跳转到类似以下链接：

```
https://raw.githubusercontent.com/username/media-hosting/main/my-video.mp4
```

---
如果使用 Git LFS，链接格式为：

```
https://media.githubusercontent.com/media/username/media-hosting/main/my-video.mp4
```

---
直接预览：
复制 `Raw `链接，粘贴到浏览器地址栏。
浏览器（如 `Chrome、Firefox`）通常会显示内置播放器，直接播放视频。
嵌入到其他页面（可选）：
创建一个 `HTML` 文件（或添加到现有网页），嵌入` Raw `链接：

```html
<video controls>
    <source src="https://raw.githubusercontent.com/username/media-hosting/main/my-video.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>
```

---
上传 `HTML `到` GitHub Pages` 或其他网站，即可分享预览。

## 三、音乐文件预览的详细操作步骤

### 方法 1：通过 GitHub Pages 预览音乐
上传音乐文件：
打开仓库页面，点击 Add file > Upload files。
拖放或选择音乐文件（如 my-audio.mp3），上传后点击 Commit changes。
如果文件较大（>50MB），参考视频部分的 Git LFS 设置，替换 *.mp4 为 *.mp3。
创建 HTML 文件用于预览：
点击 Add file > Create new file，命名为 audio.html（或任意名称）。
输入以下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Audio Preview</title>
</head>
<body>
    <h1>My Audio</h1>
    <audio controls>
        <source src="my-audio.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>
</body>
</html>
```

**如果使用 Git LFS，src 改为**：

```html
<source src="https://media.githubusercontent.com/media/username/media-hosting/main/my-audio.mp3" type="audio/mpeg">
```

---
点击 **Commit new file**。
启用** GitHub Pages**（如果尚未启用）：
同视频方法，在 Settings > Pages 中启用 main 分支。
`GitHub Pages` 链接生成后，访问 `https://username.github.io/media-hosting/audio.html`。
访问预览：
打开 `GitHub Pages` 链接，页面会显示音频播放器，支持播放、暂停、进度条等。
如果无法播放，检查文件路径、格式（MP3 最兼容）或浏览器。
方法 2：通过 `Raw` 链接预览音乐
获取音乐的` Raw `链接：
在仓库页面，点击音乐文件（如` my-audio.mp3`）。
点击 Raw 按钮，获取链接：

```
https://raw.githubusercontent.com/username/media-hosting/main/my-audio.mp3
```

---
`Git LFS `文件链接：

```
https://media.githubusercontent.com/media/username/media-hosting/main/my-audio.mp3
```

---
**直接预览：**
将 `Raw `链接粘贴到浏览器地址栏。
浏览器会显示简单的播放界面（通常是进度条和播放/暂停按钮）。
嵌入到其他页面（可选）：
在 HTML 文件中嵌入：

```html
<audio controls>
    <source src="https://raw.githubusercontent.com/username/media-hosting/main/my-audio.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>
```

---
上传到 `GitHub Pages` 或其他网站以分享。
##  四、优化与注意事项
文件优化：
 - 视频：使用 HandBrake 压缩到 720p、H.264 编码，降低比特率（如 2Mbps）。
 - 音乐：使用 Audacity 导出为 128kbps MP3，平衡质量和大小。
    - 小文件（<10MB）加载更快，适合 GitHub 带宽限制。

GitHub 限制：
**免费账户的 Git LFS 提供 1GB 存储和 1GB 带宽/月，超限需付费（[参考 GitHub 定价](https://github.com/pricing)）。
单文件大小上限为 100MB（非 LFS），LFS 支持最大 2GB。**
大量媒体文件可能被视为滥用，建议仅用于项目相关内容。
浏览器兼容性：
推荐` Chrome、Firefox、Edge，Safari `对某些格式（如 `WebM`）支持较差。
测试 Raw 链接，确保播放器正常显示。
版权与隐私：
确保视频和音乐为原创或有授权，公开仓库内容对所有人可见。
如果需要限制访问，使用私有仓库（需 GitHub Pro 或 Team 订阅）。
带宽与性能：
高流量访问可能导致 Raw 链接或 GitHub Pages 加载缓慢。
考虑将大文件托管到专业平台（如 YouTube、SoundCloud），在 GitHub 上嵌入链接。

---
## 五、替代方案（推荐）
GitHub 并非为媒体托管优化，预览体验有限。如果需要更专业的效果，建议：
视频：
上传到 YouTube 或 Vimeo，获取嵌入代码：
```html
<iframe src="https://www.youtube.com/embed/VIDEO_ID" width="560" height="315" frameborder="0" allowfullscreen></iframe>
```
在 `GitHub `的 `README.md `或` GitHub Pages `中添加。
音乐：
上传到 `SoundCloud`，获取嵌入代码：
```html
<iframe src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/TRACK_ID" width="100%" height="166"></iframe>
```
同样嵌入到` GitHub `项目。
其他图床：
Imgur（短视频）、Cloudinary（视频和图片）、ImageKit（轻量级）等，提供内置播放器和流式传输。

---
## 六、示例仓库结构
完成后的仓库可能如下：

```
media-hosting/
├── my-video.mp4
├── my-audio.mp3
├── index.html  (视频预览页面)
├── audio.html  (音乐预览页面)
└── README.md
```

---

README.md 可添加说明：

```markdown
 # Media Hosting
- [Watch Video](https://username.github.io/media-hosting/)
- [Listen Audio](https://username.github.io/media-hosting/audio.html)
```

## 七、故障排查

视频/音频不播放：
检查文件路径是否正确（大小写敏感）。
确保格式兼容（MP4、MP3 最安全）。
确认 Raw 链接是否有效（LFS 文件需用** media.githubusercontent.com**）。
**GitHub Pages** 未更新：
等待 1-2 分钟，或检查 Settings > Pages 的分支设置。
文件过大：
使用 Git LFS，或压缩文件，或切换到 YouTube/SoundCloud。
## 八、总结
视频预览：上传 MP4 到仓库，通过 GitHub Pages（HTML + <video>）或 Raw 链接实现播放，适合小文件。
音乐预览：上传 MP3，通过 GitHub Pages（HTML + <audio>）或 Raw 链接播放，体验类似。
推荐：GitHub 适合轻量级项目演示，专业媒体托管建议用 YouTube（视频）或 SoundCloud（音乐）。


---

# 扩展

一、一个Pages链接预览多个视频
---
`GitHub `仓库的灵活性：
一个仓库可以存储多个文件，包括多个视频文件（`MP4、MOV、WebM `等）。
你可以通过 `GitHub Pages` 创建多个` HTML` 页面，或者一个页面嵌入多个视频播放器，来展示所有视频。
或者使用每个视频的 `Raw `链接，单独或批量分享以供预览。
无明确限制：
`GitHub` 没有规定一个仓库只能预览一个视频，限制主要来自文件大小、带宽和存储容量（尤其是使用 `Git LFS` 时）。

二、在同一个仓库预览多个视频的详细方法
---
方法 1：通过 `GitHub Pages `预览多个视频
上传多个视频文件：
打开你的` GitHub `仓库（例如 `https://github.com/username/media-hosting`）。
点击 Add file > Upload files。
选择多个视频文件（如 `video1.mp4、video2.mp4、video3.mp4`），上传后点击` Commit changes`。
如果文件较大`（>50MB）`，使用 `Git LFS`：
安装 `Git LFS`（参考 [Git LFS 官网](https://git-lfs.github.com/)）。
在本地仓库运行：

```bash
git lfs install
git lfs track "*.mp4"
git add .gitattributes video1.mp4 video2.mp4 video3.mp4
git commit -m "Add videos with LFS"
git push origin main
```

创建` HTML` 文件展示多个视频：
选项 1：单一页面展示所有视频：
点击 `Add file > Create new file，命名为 index.html。`
输入以下代码，嵌入多个视频：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multiple Video Previews</title>
</head>
<body>
    <h1>My Video Gallery</h1>
    <h2>Video 1</h2>
    <video controls width="600">
        <source src="video1.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <h2>Video 2</h2>
    <video controls width="600">
        <source src="video2.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <h2>Video 3</h2>
    <video controls width="600">
        <source src="video3.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
</body>
</html>
```

---
如果使用` Git LFS`，将 `src `替换为对应的` Raw `链接，例如：

```html
<source src="https://media.githubusercontent.com/media/username/media-hosting/main/video1.mp4" type="video/mp4">
```

点击 `Commit new file。`
选项 2：为每个视频创建单独页面：
为每个视频创建独立的 `HTML `文件。例如，创建 `video1.html`：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video 1 Preview</title>
</head>
<body>
    <h1>Video 1</h1>
    <video controls width="600">
        <source src="video1.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <a href="index.html">Back to Gallery</a>
</body>
</html>
```

类似地创建 **video2.html、video3.html，**并更新` index.html `作为导航页面：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video Gallery</title>
</head>
<body>
    <h1>My Video Gallery</h1>
    <ul>
        <li><a href="video1.html">Video 1</a></li>
        <li><a href="video2.html">Video 2</a></li>
        <li><a href="video3.html">Video 3</a></li>
    </ul>
</body>
</html>
```

提交所有文件。
启用`**GitHub Pages**：
进入仓库的** Settings > Pages**。
在 `Source `下选择 `main `分支，文件夹为` / (root)`，点击` Save`。
等待几分钟，获取 GitHub Pages 链接（如 https://username.github.io/media-hosting/）。
访问预览：
打开 **GitHub Pages** 链接：
如果用单一页面（index.html），所有视频会显示在同一页面，各自有播放器。
如果用多个页面，访问 index.html 导航到各视频页面（如 https://username.github.io/media-hosting/video1.html）。
确保视频路径正确，浏览器支持 MP4 格式。
方法 2：通过 Raw 链接预览多个视频
获取每个视频的 Raw 链接：
在仓库页面，依次点击每个视频文件（如 video1.mp4、video2.mp4）。
点击 Raw 按钮，复制链接：

```
https://raw.githubusercontent.com/username/media-hosting/main/video1.mp4
https://raw.githubusercontent.com/username/media-hosting/main/video2.mp4
https://raw.githubusercontent.com/username/media-hosting/main/video3.mp4
```

如果使用 Git LFS，链接为：
```

https://media.githubusercontent.com/media/username/media-hosting/main/video1.mp4
```

直接预览：
将每个 Raw 链接粘贴到浏览器地址栏，浏览器会显示单独的播放器播放对应视频。
可以将链接分享给他人，点击即可预览。
嵌入到页面（可选）：
创建一个 **HTML **文件（如** index.html**），嵌入多个` Raw `链接：

```
html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multiple Video Previews</title>
</head>
<body>
    <h1>My Video Gallery</h1>
    <h2>Video 1</h2>
    <video controls width="600">
        <source src="https://raw.githubusercontent.com/username/media-hosting/main/video1.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <h2>Video 2</h2>
    <video controls width="600">
        <source src="https://raw.githubusercontent.com/username/media-hosting/main/video2.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    <h2>Video 3</h2>
    <video controls width="600">
        <source src="https://raw.githubusercontent.com/username/media-hosting/main/video3.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
</body>
</html>
```

上传到仓库并启用 **GitHub Pages**，或者嵌入到其他网站。
批量分享：
将所有 Raw 链接整理到一个文档或** README.md **中，例如：
```markdown
# My Videos
- [Video 1](https://raw.githubusercontent.com/username/media-hosting/main/video1.mp4)
- [Video 2](https://raw.githubusercontent.com/username/media-hosting/main/video2.mp4)
- [Video 3](https://raw.githubusercontent.com/username/media-hosting/main/video3.mp4)
```
用户点击链接即可逐个预览。
## 三、音乐文件与多视频类似
音乐文件（**MP3、WAV** 等）的预览方法与视频几乎相同，`替换 <video> 标签为 <audio> 标签`。
例如，在 `index.html `中嵌入多个音频：

---

```
html
<h2>Audio 1</h2>
<audio controls>
    <source src="audio1.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>
<h2>Audio 2</h2>
<audio controls>
    <source src="audio2.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>
```

Raw 链接同样适用，每个音频文件可单独预览。
## 四、示例仓库结构
一个支持多个视频和音乐预览的仓库可能如下：

---

```
media-hosting/
├── videos/
│   ├── video1.mp4
│   ├── video2.mp4
│   ├── video3.mp4
├── audios/
│   ├── audio1.mp3
│   ├── audio2.mp3
├── index.html  (主页面，展示所有视频和音频)
├── video1.html (可选，单独视频页面)
├── video2.html
├── video3.html
└── README.md
```

---
index.html 示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Media Gallery</title>
</head>
<body>
    <h1>My Media Gallery</h1>
    <h2>Videos</h2>
    <video controls width="600">
        <source src="videos/video1.mp4" type="video/mp4">
    </video>
    <video controls width="600">
        <source src="videos/video2.mp4" type="video/mp4">
    </video>
    <h2>Audios</h2>
    <audio controls>
        <source src="audios/audio1.mp3" type="audio/mpeg">
    </audio>
    <audio controls>
        <source src="audios/audio2.mp3" type="audio/mpeg">
    </audio>
</body>
</html>
```

---
## 五、注意事项与限制
文件大小与数量：
GitHub 单文件上限为 100MB（非 LFS），LFS 支持最大 2GB。
免费账户的 Git LFS 提供 1GB 存储和 1GB 带宽/月，多个大文件可能快速耗尽配额。
建议压缩视频（用 HandBrake 转为 720p、2Mbps）和音频（Audacity 转为 128kbps MP3）。
带宽限制：
多个视频同时访问可能导致 Raw 链接或 **GitHub Pages** 加载缓慢。
高流量项目建议使用` YouTube、Vimeo`（视频）或 **SoundCloud**（音频）等专业平台。
GitHub 政策：
GitHub 不鼓励将仓库用作图床，过多媒体文件可能被视为滥用，导致限制。
建议将视频和音频用于项目文档或演示，而非纯粹存储。
性能优化：
使用子文件夹（如` videos/、audios/`）组织文件，保持仓库清晰。
在 `HTML `中设置合理宽度（如 width="600"），避免页面过载。
版权与隐私：
确保所有文件为原创或有授权，公开仓库内容对所有人可见。
私有仓库（需** GitHub Pro**）可限制访问。

---

## 六、替代方案
如果需要预览大量视频或追求更好体验：
**YouTube/Vimeo：**
上传视频，获取嵌入代码，添加到`` GitHub Pages 或 README``：

```html
<iframe src="https://www.youtube.com/embed/VIDEO_ID" width="560" height="315" frameborder="0" allowfullscreen></iframe>
```

Cloudinary/ImageKit：
专业图床，支持多个视频和音频，内置播放器，提供流式传输。
**SoundCloud：**
适合音频，嵌入到 `GitHub Pages：`

```html
<iframe src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/TRACK_ID" width="100%" height="166"></iframe>

```
## 七、总结
**一个 GitHub 仓库 可以预览多个视频和音乐，通过 GitHub Pages（单一页面或多页面）或 Raw 链接实现。
推荐方法：上传所有视频到仓库，使用 index.html 嵌入多个 <video> 标签，通过 GitHub Pages 访问。
限制：受文件大小、带宽和 GitHub 政策约束，适合轻量级项目。**