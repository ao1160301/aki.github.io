## 演示图片（一）

![](https://mig01.996399.xyz/20250422111659050.png)

### 代码
```
/**
 *  自定义网站配置 
 */
const config = {
  title: "SUOU AKI 导航", // 网站标题
  subtitle: "周防秋", // 网站副标题
  logo_icon: "aki", // 网站图标（使用semantic-ui图标）
  hitokoto: false, // 是否启用一言功能
  search: true, // 是否启用搜索功能
  search_engine: [ // 搜索引擎选项
    { name: "必 应", template: "https://www.bing.com/search?q=$s" }
  ],
  selling_ads: false, // 是否显示域名出售信息（已禁用）
  lists: [ // 导航链接列表
    {
      name: "服务站点",
      icon: "blog",
      list: [
        { url: "https://mail.suouaki.me/", name: "ZMAIL-24小时匿名邮箱", desc: "临时接码服务" },
        { url: "https://mail.996399.xyz/", name: "ZMAIL-24小时匿名邮箱", desc: "@nanahira.ggff.net临时接码服务" },
        { url: "https://24mail.996399.xyz/", name: "ZMAIL-24小时匿名邮箱", desc: "@wotoha.dpdns.org临时接码服务" },
        { url: "https://img.996399.xyz/", name: "无限空间免费图床服务，最高支持30MB文件", desc: "登陆密码:admin" },
        { url: "https://moemail.996399.xyz/", name: "萌萌哒永久邮箱服务", desc: "超多域名后缀可选，未释放权限，需联系站主" },
        { url: "https://rarara.ggff.net/moe", name: "萌萌哒永久邮箱服务", desc: "单域名后缀，释放权限" },
        { url: "https://now.momobako.me/", name: "NewsNow热点资讯一览", desc: "热点资讯" },
        { url: "https://bako.996399.xyz/", name: "SUOUAKI BLOG", desc: "pages站点" },
        { url: "http://momobako.atwebpages.com/", name: "桃箱 BLOG", desc: "个人站点" },
        { url: "http://blog.momobako.me/", name: "momobako blog", desc: "GitHub pages站点" },
        { url: "http://momobako.endl.site/", name: "个人站点", desc: "开发中" }
      ]
    },
    {
      name: "社交",
      icon: "users",
      list: [
        { url: "https://www.youtube.com/@aki_suou", name: "aki_suou", desc: "YouTube频道" },
        { url: "https://x.com/ccMj2Urwo295132", name: "推特", desc: "X" },
        { url: "https://www.nicovideo.jp/user/128373082", name: "nicovideo", desc: "周防アキ" },
        { url: "https://discord.gg/ARdVRfm7", name: "discord", desc: "在用" },
        { url: "https://t.me/momo_bako", name: "Telegram", desc: "个人活跃地" },
        { url: "https://www.instagram.com/haisa_kura/", name: "instagram", desc: "个目前使用账号" },
        { url: "https://www.facebook.com/tara.ai.106068?mibextid=ZbWKwL", name: "facebook", desc: "目前使用账号" }
      ]
    }
  ]
};

/**
 *  工具函数：生成HTML元素
 *  @param tag HTML标签名
 *  @param attrs 属性数组
 *  @param content 内容
 */
const el = (tag, attrs, content) => `<${tag} ${attrs.join(" ")}>${content}</${tag}>`;

/**
 *  处理HTTP请求
 */
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});

async function handleRequest(request) {
  return new Response(renderHTML(renderIndex()), {
    headers: { 'content-type': 'text/html;charset=UTF-8' }
  });
}

/**
 *  获取网站的favicon
 *  @param url 网站URL
 */
function getFavicon(url) {
  const domain = url.replace(/^https?:\/\//, '').split('/')[0];
  return `https://www.google.com/s2/favicons?domain=${domain}&sz=32`;
}

/**
 *  渲染页面主体
 */
function renderIndex() {
  const footer = el('footer', [], el('div', ['class="footer"'], ' 有问题联系:aki@suouaki.me ' + el('a', ['class="ui label"'], el('i', ['class="balance scale icon"'], "") + 'MIT License')));
  return renderHeader() + renderMain() + footer;
}

/**
 *  渲染头部（包含标题和搜索框）
 */
function renderHeader() {
  const title = el('h1', ['class="ui inverted header"'],
    el('i', [`class="${config.logo_icon} icon"`], "") +
    el('div', ['class="content"'], config.title +
      el('div', ['class="sub header"'], config.subtitle)
    )
  );

  const input = el('div', ['class="ui right icon fluid large input"'],
    el('input', ['id="searchinput"', 'type="search"', 'placeholder="搜索你想要知道的……"', 'autocomplete="off"'], "") +
    el('i', ['class="inverted circular search link icon"'], "")
  );

  return el('header', [],
    el('div', ['id="head"', 'class="ui inverted vertical masthead segment"'],
      el('div', ['id="title"', 'class="ui text container"'],
        title + (config.search ? el('div', ['class="search-container"'], input) : "")
      )
    )
  );
}

/**
 *  渲染主要内容（站点和社交卡片）
 */
function renderMain() {
  const main = config.lists.map((item) => {
    const card = (url, name, desc) => el('a', ['class="card"', `href="${url}"`, 'target="_blank"'],
      el('div', ['class="content"'],
        el('img', ['class="left floated avatar ui image"', `src="${getFavicon(url)}"`], "") +
        el('div', ['class="header"'], name) +
        el('div', ['class="meta"'], desc)
      )
    );
    const divider = el('h4', ['class="ui horizontal divider header"'],
      el('i', [`class="${item.icon} icon"`], "") + item.name
    );

    const content = el('div', ['class="ui four stackable cards"'],
      item.list.map((link) => card(link.url, link.name, link.desc)).join("")
    );

    return `<div class="section-bg">${divider + content}</div>`;
  }).join("");

  return `<main>${main}</main>`;
}

/**
 *  渲染完整HTML页面
 */
function renderHTML(index) {
  return `<!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>${config.title} - ${config.subtitle}</title>
      <link href="https://cdn.jsdelivr.net/npm/semantic-ui-css@2.4.1/semantic.min.css" rel="stylesheet">
      <link href="https://cdn.jsdelivr.net/gh/sleepwood/cf-worker-dir@0.1.1/style.min.css" rel="stylesheet">
      <script src="https://cdn.jsdelivr.net/npm/jquery@3.4.1/dist/jquery.min.js"></script>
      <script src="https://cdn.jsdelivr.net/npm/semantic-ui-css@2.4.1/semantic.min.js"></script>
      <style>
        html, body {
          margin: 0;
          padding: 0;
          width: 100vw;
          height: 100vh;
          overflow-x: hidden;
        }
        body {
          min-height: 100vh;
          width: 100vw;
          margin: 0;
          padding: 0;
          background-image: url('https://mig01.996399.xyz/The%20Hungry%20Lamb%202024_12_15%201_09_15.png');
          background-size: cover;
          background-position: center;
          background-attachment: fixed;
        }
        header, footer {
          background: rgba(0, 0, 0, 0.85) !important; /* 导航和页脚半透明黑色背景 */
          box-shadow: none !important;
          width: 100vw;
          padding: 20px 0;
        }
        .ui.inverted.segment, .ui.segment, .ui.basic.segment, .ui.text.container, .ui.container {
          background: transparent !important;
          border-radius: 0 !important;
          box-shadow: none !important;
          margin: 0 !important;
          padding: 0 !important;
          width: 100vw !important;
          max-width: 100vw !important;
        }
        main {
          width: 100vw !important;
          margin: 0 !important;
          padding: 0 !important;
        }
        .section-bg {
          background: transparent !important; /* 中间部分完全透明 */
          border-radius: 16px;
          margin: 32px auto;
          padding: 32px 20px;
          width: 96vw;
          max-width: 1800px;
          box-shadow: none;
        }
        .ui.inverted.header {
          font-size: 3em !important;
        }
        .ui.inverted.header .content {
          color: white !important; /* 主标题颜色改为白色 */
        }
        body, .ui.menu, .ui.segment, .ui.card, .ui.divider, .footer, .ui.input input, .sub.header {
          color: #ff69b4 !important; /* 保持粉色主题 */
        }
        .search-container {
          width: 100vw;
          display: flex;
          align-items: center;
          margin: 30px 0;
          justify-content: center;
          background: rgba(0, 0, 0, 0.3);
          border-radius: 8px;
          padding: 20px 0;
        }
        .ui.input {
          width: 100%;
          max-width: 800px; /* 搜索框最大宽度 */
        }
        .ui.four.stackable.cards {
          margin: 0 -10px;
          width: 100%;
          display: flex;
          flex-wrap: wrap;
          justify-content: center;
        }
        .ui.card {
          margin: 10px !important;
          background: rgba(255, 255, 255, 0.1) !important; /* 卡片轻微透明效果 */
        }
        footer {
          width: 100vw;
          padding: 20px;
          text-align: center;
        }
      </style>
  </head>
  <body>
    ${index}
    <script>
      $('.search').on('click', function (e) {
        var url = "${config.search_engine[0].template}"; // 默认使用第一个搜索引擎
        url = url.replace(/\\$s/, $('#searchinput').val());
        window.open(url);
      });
      $("#searchinput").bind("keypress", function(){
        if (event.keyCode == 13){
          $(".search").click();
        }
      });
    </script>
  </body>
  </html>`;
}
```

***

### 部署方法
1.创建worker名称自定义
2.修改代码->复制代码->部署
3.访问分配的网址，就可以了
   - 可以使用自己的域名
#### 使用方法
16行添加导航标签

```
{ url: "网址", name: "名称", desc: "介绍" },

```
每个分类导航标签`必须要`用“,”
每个分类导航标签结尾`不`用“,”


5~7行自定义主标题
```
  title: "SUOU AKI 导航", // 网站标题
  subtitle: "周防秋", // 网站副标题
  logo_icon: "aki", // 网站图标（使用semantic-ui图标）

```

***

## 演示图片（二）

![](https://mig01.996399.xyz/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-04-22%20104259.png)

### 代码
```
const HTML_CONTENT = `<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Card Tab</title>
<style>
html, body {
    height: 100%;
    margin: 0;
    padding: 0;
}
body {
    font-family: Arial, sans-serif;
    background-color: #d8eac4;
    background-image: url('https://mig01.996399.xyz/The%20Hungry%20Lamb%202024_12_15%201_09_15.png');
    background-size: 100% 100%; /* 强制拉伸到全屏幕 */
    background-position: center;
    background-repeat: no-repeat;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    transition: background-color 0.3s ease;
    min-height: 100vh; /* 确保内容区域至少占满屏幕 */
}
.card-container {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 10px;
}
.card {
    display: flex;
    flex-direction: column;
    position: relative;
    background-color: #a0c9e5;
    padding: 10px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    cursor: grab;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    width: 200px;
    height: auto;
}

.card-top {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
}

.card-icon {
    width: 24px;
    height: 24px;
    margin-right: 10px;
}

.card-title {
    font-size: 16px;
    font-weight: bold;
}

.card-url {
    color: #555;
    font-size: 12px;
    word-break: break-all;
}

.card.dragging {
    opacity: 0.8;
    transform: scale(1.05);
    cursor: grabbing;
}
.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}
.delete-btn {
    position: absolute;
    top: -10px;
    right: -10px;
    background-color: red;
    color: white;
    border: none;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    text-align: center;
    font-size: 14px;
    line-height: 20px;
    cursor: pointer;
    display: none;
}
.admin-controls {
    position: fixed;
    top: 10px;
    right: 10px;
    font-size: 60%;
}
.admin-controls input {
    padding: 5px;
    font-size: 60%;
}
.admin-controls button {
    padding: 5px 10px;
    font-size: 60%;
    margin-left: 10px;
}
.add-remove-controls {
    display: none;
    margin-top: 10px;
}
.round-btn {
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    text-align: center;
    font-size: 24px;
    line-height: 40px;
    cursor: pointer;
    margin: 0 10px;
}
#theme-toggle {
    position: fixed;
    bottom: 10px;
    left: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    text-align: center;
    font-size: 24px;
    line-height: 40px;
    cursor: pointer;
}
#dialog-overlay {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    justify-content: center;
    align-items: center;
}
#dialog-box {
    background: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
#dialog-box label {
    display: block;
    margin-bottom: 5px;
}
#dialog-box input, #dialog-box select {
    width: 100%;
    padding: 5px;
    margin-bottom: 10px;
}
#dialog-box button {
    padding: 5px 10px;
    margin-right: 10px;
}

.section {
    margin-bottom: 20px;
}

.section-title {
    font-size: 24px;
    font-weight: bold;
    color: #333;
    margin-bottom: 10px;
}
</style>
</head>
<body>
<h1>SUOU AKI导航</h1>

<div class="admin-controls">
<input type="password" id="admin-password" placeholder="输入密码">
<button id="admin-mode-btn" onclick="toggleAdminMode()">进入管理模式</button>
</div>

<div class="add-remove-controls">
<button class="round-btn" onclick="showAddDialog()">+</button>
<button class="round-btn" onclick="toggleRemoveMode()">-</button>
</div>

<div id="sections-container">
<!-- 分类将在这里动态生成 -->
</div>

<button id="theme-toggle" onclick="toggleTheme()">◑</button>

<div id="dialog-overlay">
<div id="dialog-box">
<label for="name-input">名称</label>
<input type="text" id="name-input">
<label for="url-input">地址</label>
<input type="text" id="url-input">
<label for="category-select">选择分类</label>
<select id="category-select">
<!-- 分类选项将在这里动态生成 -->
</select>
<button onclick="addLink()">确定</button>
<button onclick="hideAddDialog()">取消</button>
</div>
</div>
<div class="copyright">
    <!--    请不要删除 -->
    <p><a href="https://dir.momobako.me/" target="_blank">更多</a>
</div>

<script>
let isAdmin = false; 
let removeMode = false; 
let isDarkTheme = false; 
let links = []; 
const categories = {
"常用网站": [],                   // **编辑自己的网站分类**
"工具导航": [],
"游戏娱乐": [],
"影音视听": [],
"技术论坛": []
};

async function loadLinks() {
const response = await fetch('/api/getLinks?userId=testUser');
links = await response.json();

Object.keys(categories).forEach(key => {
categories[key] = [];
});

links.forEach(link => {
if (categories[link.category]) {
categories[link.category].push(link);
}
});

loadSections();
updateCategorySelect();
// applyTheme();
}

function loadSections() {
const container = document.getElementById('sections-container');
container.innerHTML = '';

Object.keys(categories).forEach(category => {
const section = document.createElement('div');
section.className = 'section';

const title = document.createElement('div');
title.className = 'section-title';
title.textContent = category;

const cardContainer = document.createElement('div');
cardContainer.className = 'card-container';
cardContainer.id = category;

section.appendChild(title);
section.appendChild(cardContainer);

categories[category].forEach(link => {
createCard(link, cardContainer);
});

container.appendChild(section);
});
}

function createCard(link, container) {
const card = document.createElement('div');
card.className = 'card';
card.setAttribute('draggable', isAdmin);

const cardTop = document.createElement('div');
cardTop.className = 'card-top';

const icon = document.createElement('img');
icon.className = 'card-icon';
// icon.src = 'https://www.google.com/s2/favicons?domain=' + link.url;
icon.src = 'https://favicon.zhusl.com/ico?url=' + link.url;
icon.alt = 'Website Icon';

const title = document.createElement('div');
title.className = 'card-title';
title.textContent = link.name;

cardTop.appendChild(icon);
cardTop.appendChild(title);

const url = document.createElement('div');
url.className = 'card-url';
url.textContent = link.url;

card.appendChild(cardTop);
card.appendChild(url);

//  URL 检查和修正
function correctUrl(url) {
if (url.startsWith('http://') || url.startsWith('https://')) {
return url;
} else {
return 'http://' + url;
}
}

let correctedUrl = correctUrl(link.url);

if (!isAdmin) {
card.addEventListener('click', () => {
window.open(correctedUrl, '_blank');
});
}

const deleteBtn = document.createElement('button');
deleteBtn.textContent = '–';
deleteBtn.className = 'delete-btn';
deleteBtn.onclick = function (event) {
event.stopPropagation();
removeCard(card);
};
card.appendChild(deleteBtn);

if (isDarkTheme) {
card.style.backgroundColor = '#1e1e1e';
card.style.color = '#ffffff';
card.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.5)';
} else {
card.style.backgroundColor = '#a0c9e5';
card.style.color = '#333';
card.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.1)';
}

card.addEventListener('dragstart', dragStart);
card.addEventListener('dragover', dragOver);
card.addEventListener('dragend', dragEnd);
card.addEventListener('drop', drop);

if (isAdmin && removeMode) {
deleteBtn.style.display = 'block';
}

container.appendChild(card);
}

function updateCategorySelect() {
const categorySelect = document.getElementById('category-select');
categorySelect.innerHTML = '';

Object.keys(categories).forEach(category => {
const option = document.createElement('option');
option.value = category;
option.textContent = category;
categorySelect.appendChild(option);
});
}

async function saveLinks() {
let links = [];
for (const category in categories) {
links = links.concat(categories[category]);
}

await fetch('/api/saveOrder', {
method: 'POST',
headers: { 'Content-Type': 'application/json' },
body: JSON.stringify({ userId: 'testUser', links }),
});
}

function addLink() {
const name = document.getElementById('name-input').value;
const url = document.getElementById('url-input').value;
const category = document.getElementById('category-select').value;

if (name && url && category) {
const newLink = { name, url, category };

if (!categories[category]) {
categories[category] = [];
}
categories[category].push(newLink);

const container = document.getElementById(category);
createCard(newLink, container);

saveLinks();

document.getElementById('name-input').value = '';
document.getElementById('url-input').value = '';
hideAddDialog();
}
}

function removeCard(card) {
const url = card.querySelector('.card-url').textContent;
let category;
for (const key in categories) {
const index = categories[key].findIndex(link => link.url === url);
if (index !== -1) {
categories[key].splice(index, 1);
category = key;
break;
}
}
card.remove();

saveLinks();
}

let draggedCard = null;

function dragStart(event) {
if (!isAdmin) return;
draggedCard = event.target;
draggedCard.classList.add('dragging');
event.dataTransfer.effectAllowed = "move";
}

function dragOver(event) {
if (!isAdmin) return;
event.preventDefault();
const target = event.target.closest('.card');
if (target && target !== draggedCard) {
const container = target.parentElement;
const mousePositionX = event.clientX;
const targetRect = target.getBoundingClientRect();

if (mousePositionX < targetRect.left + targetRect.width / 2) {
container.insertBefore(draggedCard, target);
} else {
container.insertBefore(draggedCard, target.nextSibling);
}
}
}

function drop(event) {
if (!isAdmin) return;
event.preventDefault();
draggedCard.classList.remove('dragging');
draggedCard = null;
saveCardOrder();
}

// function dragEnd(event) {
// draggedCard.classList.remove('dragging');
function dragEnd(event) {
if (draggedCard) {
draggedCard.classList.remove('dragging');
}
}

async function saveCardOrder() {
if (!isAdmin) return;
const containers = document.querySelectorAll('.card-container');
let newLinks = [];

containers.forEach(container => {
const category = container.id;
categories[category] = [];
[...container.children].forEach(card => {
const url = card.querySelector('.card-url').textContent;
const name = card.querySelector('.card-title').textContent;
const link = { name, url, category };
categories[category].push(link);
newLinks.push(link);
});
});

links = newLinks;

await fetch('/api/saveOrder', {
method: 'POST',
headers: { 'Content-Type': 'application/json' },
body: JSON.stringify({ userId: 'testUser', links: newLinks }),
});
}


function toggleAdminMode() {
const passwordInput = document.getElementById('admin-password');
const adminBtn = document.getElementById('admin-mode-btn');
const addRemoveControls = document.querySelector('.add-remove-controls');

if (!isAdmin) {
verifyPassword(passwordInput.value)
.then(isValid => {
if (isValid) {
isAdmin = true;
adminBtn.textContent = "退出管理模式";
alert('已进入管理模式');
addRemoveControls.style.display = 'block';
reloadCardsAsAdmin();
} else {
alert('密码错误');
}
});
} else {
isAdmin = false;
removeMode = false;
adminBtn.textContent = "进入管理模式";
alert('已退出管理模式');
addRemoveControls.style.display = 'none';
const deleteButtons = document.querySelectorAll('.delete-btn');
deleteButtons.forEach(btn => btn.style.display = 'none');
reloadCardsAsAdmin();
}

passwordInput.value = '';
}

function reloadCardsAsAdmin() {
document.querySelectorAll('.card-container').forEach(container => {
container.innerHTML = '';
});
loadLinks().then(() => {
if (isDarkTheme) {
applyDarkTheme();
}
});
}

function applyDarkTheme() {
document.body.style.backgroundColor = '#121212';
document.body.style.color = '#ffffff';
const cards = document.querySelectorAll('.card');
cards.forEach(card => {
card.style.backgroundColor = '#1e1e1e';
card.style.color = '#ffffff';
card.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.5)';
});
}

function showAddDialog() {
document.getElementById('dialog-overlay').style.display = 'flex';
}

function hideAddDialog() {
document.getElementById('dialog-overlay').style.display = 'none';
}


function toggleRemoveMode() {
removeMode = !removeMode;
const deleteButtons = document.querySelectorAll('.delete-btn');
deleteButtons.forEach(btn => {
btn.style.display = removeMode ? 'block' : 'none';
});
}

function toggleTheme() {
isDarkTheme = !isDarkTheme;
// 设置暗色主题和亮色主题的背景色
document.body.style.backgroundColor = isDarkTheme ? '#121212' : '#d8eac4';
// 设置暗色主题和亮色主题的文本颜色
document.body.style.color = isDarkTheme ? '#ffffff' : '#333';

const cards = document.querySelectorAll('.card');
cards.forEach(card => {
// 卡片背景和文本颜色设置
card.style.backgroundColor = isDarkTheme ? '#1e1e1e' : '#a0c9e5';
card.style.color = isDarkTheme ? '#ffffff' : '#333';
// 卡片阴影的设置，增强暗色主题的阴影
card.style.boxShadow = isDarkTheme
? '0 4px 8px rgba(0, 0, 0, 0.5)'
: '0 4px 8px rgba(0, 0, 0, 0.1)';
});

const dialogBox = document.getElementById('dialog-box');
// 对话框背景和文本颜色设置
dialogBox.style.backgroundColor = isDarkTheme ? '#1e1e1e' : '#ffffff';
dialogBox.style.color = isDarkTheme ? '#ffffff' : '#333';

const inputs = dialogBox.querySelectorAll('input, select');
inputs.forEach(input => {
// 输入框背景和文本颜色设置
input.style.backgroundColor = isDarkTheme ? '#333333' : '#ffffff';
input.style.color = isDarkTheme ? '#ffffff' : '#333';
});
}


async function verifyPassword(inputPassword) {
const response = await fetch('/api/verifyPassword', {
method: 'POST',
headers: { 'Content-Type': 'application/json' },
body: JSON.stringify({ password: inputPassword }),
});
const result = await response.json();
return result.valid;
}

loadLinks();
</script>
</body>
</html>
`;

export default {
async fetch(request, env) {
const url = new URL(request.url);

if (url.pathname === '/') {
return new Response(HTML_CONTENT, {
headers: { 'Content-Type': 'text/html' }
});
}

if (url.pathname === '/api/getLinks') {
const userId = url.searchParams.get('userId');
const links = await env.CARD_ORDER.get(userId); 
return new Response(links || JSON.stringify([]), { status: 200 });
}

if (url.pathname === '/api/saveOrder' && request.method === 'POST') {
const { userId, links } = await request.json();
await env.CARD_ORDER.put(userId, JSON.stringify(links));
return new Response(JSON.stringify({ success: true }), { status: 200 });
}

if (url.pathname === '/api/verifyPassword' && request.method === 'POST') { 
const { password } = await request.json();
const isValid = password === env.ADMIN_PASSWORD; // 从环境变量中获取密码
return new Response(JSON.stringify({ valid: isValid }), {
status: isValid ? 200 : 403,
headers: { 'Content-Type': 'application/json' },
});
}

return new Response('Not Found', { status: 404 });
}
};

```
### 部署方法
  - 直接复制到worker里
  -  名称自定义
  - 创建KV空间
     - KV名称`随意`
  - 找到刚刚创建的worker项目->`设置`->`绑定`
     - 选择KV **名称**输入`CARD_ORDER`选择刚创建的KV空间
  -  在`设置`->`机密/变量`
     -  选择添加->类型`文本`->名称`ADMIN_PASSWORD`->值`自定义管理员密码`（只支持数字）


 #### 使用方法