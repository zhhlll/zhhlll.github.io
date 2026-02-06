<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>SimpFun Minecraft 服务器</title>
  <style>
    body {
      font-family: "Microsoft YaHei", sans-serif;
      background: #e3f2fd;
      margin: 0;
      padding: 20px;
      color: #0d47a1;
    }
    .card {
      max-width: 600px;
      margin: 20px auto;
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.1);
      overflow: hidden;
    }
    .banner {
      width: 100%;
      height: 160px;
      object-fit: cover;
      border-bottom: 1px solid #eee;
    }
    .tab-header {
      display: flex;
      background: #0288d1;
      color: white;
    }
    .tab-btn {
      flex: 1;
      padding: 14px;
      border: none;
      background: transparent;
      color: white;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.3s;
    }
    .tab-btn:hover {
      background: rgba(0,0,0,0.1);
    }
    .tab-btn.active {
      background: rgba(0,0,0,0.2);
    }
    .tab-content {
      display: none;
      padding: 25px;
      text-align: center;
    }
    .tab-content.active {
      display: block;
    }
    h1 {
      margin-top: 0;
      color: #0288d1;
    }
    .server-address {
      background: #e1f5fe;
      padding: 12px;
      border-radius: 8px;
      margin: 15px 0;
      font-family: monospace;
      font-size: 1.1em;
    }
    .version-info {
      background: #fff8e1;
      padding: 10px;
      border-radius: 8px;
      margin: 15px 0;
      font-weight: bold;
      color: #ff6f00;
    }
    .wechat {
      color: #d32f2f;
      font-weight: bold;
      font-size: 1.2em;
    }
    .status {
      margin-top: 20px;
      padding: 10px;
      background: #f1f8e9;
      border-radius: 8px;
    }
    .rules-list, .download-list {
      text-align: left;
      max-width: 500px;
      margin: 15px auto;
      line-height: 1.6;
    }
    .mc-icon {
      width: 64px;
      margin: 10px 0;
      image-rendering: pixelated; /* 保持像素风格 */
    }
    .logo {
      max-height: 60px;
      margin: 10px 0;
    }
    a {
      color: #0288d1;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <div class="card">
    <!-- 🖼️ 顶部 Minecraft Banner（高清官方风格） -->
    < img class="banner" src="https://cdn.jsdelivr.net/gh/mcsrvstat/resources@main/banners/minecraft_1.20.jpg" alt="Minecraft Server Banner">

    <div class="tab-header">
      <button class="tab-btn active" onclick="openTab('home')">🏠 首页</button>
      <button class="tab-btn" onclick="openTab('rules')">📜 规则</button>
      <button class="tab-btn" onclick="openTab('download')">⬇️ 下载</button>
    </div>

    <!-- 首页 -->
    <div id="home" class="tab-content active">
      <h1>⛏️ SimpFun Minecraft 服务器</h1>
      
      <!-- 🎮 Minecraft 像素图标 -->
      < img class="mc-icon" src="https://cdn.jsdelivr.net/gh/mcsrvstat/resources@main/icons/minecraft.png" alt="Minecraft">

      <div class="server-address">play.simpfun.cn:23851</div>
      <div class="version-info">🧱 游戏版本：1.20.1 (Forge)</div>

      <div class="status">
        <p>👥 当前玩家：<span id="players">加载中...</span></p >
        <p>🕒 状态：<span id="status">检测中...</span></p >
      </div>

      <div style="margin-top: 25px;">
        <p>💬 服主微信：<br><span class="wechat">zhonghh1116</span></p >
        <p style="font-size: 0.9em; color: #555;">添加时请备注“Minecraft”</p >
      </div>
    </div>

    <!-- 规则 -->
    <div id="rules" class="tab-content">
      <h1>📜 服务器规则</h1>
      <ul class="rules-list">
        <li>✅ 必须使用 <strong>1.20.1 Forge</strong> 客户端</li>
        <li>🚫 禁止 grief（恶意破坏他人建筑）</li>
        <li>🚫 禁止外挂、作弊、刷物品</li>
        <li>💬 聊天请文明，禁止广告/刷屏</li>
        <li>🔒 领地内可自由建造，公共区域请合作</li>
        <li>❓ 遇到问题先加服主微信咨询</li>
      </ul>
    </div>

    <!-- 下载 -->
    <div id="download" class="tab-content">
      <h1>⬇️ 客户端下载指南</h1>
      <!-- Forge Logo -->
      < img class="logo" src="https://cdn.jsdelivr.net/npm/@mdi/logo-forge.svg" alt="Forge Logo">
      
      <ol class="download-list">
        <li>安装 <a href=" " target="_blank">Java 17</a >（必需）</li>
        <li>下载 <a href="https://files.minecraftforge.net/net/minecraftforge/forge/index_1.20.1.html" target="_blank">Forge 1.20.1 安装器</a ></li>
        <li>运行安装器 → 选择 "Install client"</li>
        <li>打开 Minecraft Launcher → 启动器配置文件选择 <strong>Forge</strong></li>
        <li>加入服务器：<code>play.simpfun.cn:23851</code></li>
      </ol>
      <p style="color:#d32f2f; font-weight:bold; margin-top:15px;">
        ⚠️ 不安装 Forge 无法进入！
      </p >
    </div>
  </div>

  <script>
    function openTab(tabName) {
      document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.getElementById(tabName).classList.add('active');
      event.target.classList.add('active');
    }

    async function updateStatus() {
      try {
        const res = await fetch('https://api.mcsrvstat.us/3/play.simpfun.cn:23851');
        const data = await res.json();
        if (data.online) {
          document.getElementById('players').textContent = `${data.players.online} / ${data.players.max}`;
          document.getElementById('status').innerHTML = '<span style="color:green">🟢 在线</span>';
        } else {
          document.getElementById('players').textContent = '0 / ?';
          document.getElementById('status').innerHTML = '<span style="color:red">🔴 离线</span>';
        }
      } catch (e) {
        document.getElementById('players').textContent = '查询失败';
        document.getElementById('status').innerHTML = '<span style="color:orange">⚠️ 错误</span>';
      }
    }

    updateStatus();
    setInterval(updateStatus, 30000);
  </script>
</body>
</html>
