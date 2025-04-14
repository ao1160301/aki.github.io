## 预览效果图，有空再编写


## 仓库结构（其实看我的仓库结构，还有代码就已经会了）

```
momobako22.github.io/
├── music/
│   ├── audio/                    # 存储 MP3 音频文件
│   │   ├── song1.mp3
│   │   ├── song2.mp3
│   │   └── ...                   # 其他音频文件
│   ├── images/                   # 存储图片文件（如封面）
│   │   ├── song1-cover.jpg
│   │   ├── song2-cover.jpg
│   │   └── ...                   # 其他图片文件
│   ├── index.html                # 主页（可选，用于导航）
│   ├── songs.html                # 歌曲总览页面（已存在）
│   ├── song1.html                # 单曲页面（已提供）
│   ├── multi-songs.html          # 新增的多曲预览页面
│   └── styles/                   # 存储 CSS 文件（可选，用于统一样式）
│       └── main.css
├── README.md                     # 仓库说明文件
└── .gitignore                    # Git 忽略文件
```


## 代码展示；`multi-songs.html`
---

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>多首歌曲预览</title>
    <style>
        body {
            font-family: Arial, 'Microsoft YaHei', sans-serif;
            margin: 40px;
            background-color: #f9f9f9;
        }
        h1 {
            color: #333;
            text-align: center;
        }
        .song-container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
        }
        .song-card {
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            padding: 20px;
            width: 300px;
            text-align: center;
        }
        .song-card img {
            max-width: 100%;
            height: auto;
            border-radius: 8px;
            margin-bottom: 10px;
        }
        .song-card h2 {
            font-size: 1.2em;
            color: #333;
            margin: 10px 0;
        }
        .song-card p {
            font-size: 0.9em;
            color: #666;
            margin: 5px 0;
        }
        audio {
            width: 100%;
            margin: 10px 0;
        }
        a {
            color: #007bff;
            text-decoration: none;
            display: inline-block;
            margin-top: 20px;
        }
        a:hover {
            text-decoration: underline;
        }
        @media (max-width: 600px) {
            .song-card {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <h1>多首歌曲预览</h1>
    <div class="song-container">
        <!-- 歌曲 1 -->
        <div class="song-card">
            <img src="images/song1-cover.jpg" alt="歌曲 1 封面" onerror="this.style.display='none'">
            <h2>歌曲标题 1</h2>
            <p><strong>简介：</strong> 这是一首充满情感的歌曲，适合放松心情。</p>
            <p><strong>描述：</strong> 歌曲以柔和的旋律和温暖的歌词为主，灵感来源于生活中的点滴感动。</p>
            <audio controls>
                <source src="audio/song1.mp3" type="audio/mpeg">
                您的浏览器不支持音频播放。
            </audio>
        </div>
        <!-- 歌曲 2 -->
        <div class="song-card">
            <img src="images/song2-cover.jpg" alt="歌曲 2 封面" onerror="this.style.display='none'">
            <h2>歌曲标题 2</h2>
            <p><strong>简介：</strong> 一首节奏明快的流行歌曲，带来活力。</p>
            <p><strong>描述：</strong> 这首歌结合了现代电子音乐元素，适合派对或运动时聆听。</p>
            <audio controls>
                <source src="audio/song2.mp3" type="audio/mpeg">
                您的浏览器不支持音频播放。
            </audio>
        </div>
        <!-- 可根据需要添加更多歌曲 -->
    </div>
    <p><a href="songs.html">返回歌曲总览</a></p>
</body>
</html>
```

### 效果展示
![](https://1.momobako.ip-ddns.com//20250414175517394.png)


## 代码展示；`songs.html`**导航用的**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- 设置字符编码 -->
    <meta charset="UTF-8">
    <!-- 响应式设计 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- 页面标题 -->
    <title>所有音乐预览</title>
    <!-- CSS 美化 -->
    <style>
        body { 
            font-family: Arial, sans-serif; 
            margin: 40px; 
        }
        h1 { 
            color: #333; 
        }
        h2 { 
            margin-top: 30px; 
        }
        audio { 
            margin: 20px 0; 
            width: 100%; /* 适配屏幕 */
        }
        a { 
            color: #007bff; 
            text-decoration: none; 
        }
        a:hover { 
            text-decoration: underline; 
        }
    </style>
</head>
<body>
    <!-- 主标题 -->
    <h1>音乐</h1>
    <!-- Song 1 -->
    <h2>①【お見舞いフェラ～射精～よしよし抱っこ】</h2>
    <audio controls>
        <!-- 音频文件路径，指向仓库中的 song1.mp3 -->
        <source src="audio/RJ01095590/①【お見舞いフェラ～射精～よしよし抱っこ】.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 2 -->
    <h2>Song 2 - Vocal Track</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 3 -->
    <h2>Song 3 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song3.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 5 -->
    <h2>Song 5 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 6 -->
    <h2>Song 6 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song  -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 6 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- Song 4 -->
    <h2>Song 4 - Instrumental</h2>
    <audio controls>
        <!-- 音频文件路径 -->
        <source src="song4.mp3" type="audio/mpeg">
        Your browser does not support the audio tag.
    </audio>
    <!-- 返回导航 -->
    <p><a href="index.html">Back to Gallery</a></p>
</body>
</html>

```

### 效果图；
![](https://1.momobako.ip-ddns.com//20250414180959988.png)

## 结语
`其实用的就这么多，其实俩代码文件就可以了。`



