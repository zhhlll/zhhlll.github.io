index.html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>SimpFun Minecraft 服务器</title>
  <style>
    /* ===== 全局重置 & 字体 ===== */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    @font-face {
      font-family: 'Minecraft';
      src: url('https://cdn.jsdelivr.net/gh/Andrew69/Minecraft-Font@master/Minecraft.woff2') format('woff2');
    }
    body {
      font-family: "Minecraft", "Microsoft YaHei", monospace;
      background: #0c0c16;
      color: #e0f7fa;
      min-height: 100vh;
      overflow-x: hidden;
      position: relative;
    }

    /* ===== 星空背景 ===== */
    canvas#bg {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
    }

    /* ===== 卡片容器 ===== */
    .card {
      max-width: 600px;
      margin: 30px auto;
      background: rgba(13, 19, 33, 0.85);
      backdrop-filter: blur(10px);
      border: 2px solid #00b0ff;
      border-radius: 16px;
      box-shadow: 0 0 30px rgba(0, 176, 255, 0.4);
      overflow: hidden;
      position: relative;
    }

    /* ===== 3D 方块装饰 ===== */
    .cube {
      position: absolute;
      width: 20px;
      height: 20px;
      background: #4caf50;
      transform: rotateX(45deg) rotateY(45deg);
      opacity: 0.7;
      z-index: -1;
    }
    .cube.cube1 { top: 20px; right: 30px; background: #ff9800; animation: float 8s infinite ease-in-out; }
    .cube.cube2 { bottom: 40px; left: 20px; background: #2196f3; animation: float 10s infinite ease-in-out reverse; }
    .cube.cube3 { top: 60%; left: 10%; background: #f44336; animation: float 12s infinite ease-in-out; }

    @keyframes float {
      0%, 100% { transform: rotateX(45deg) rotateY(45deg) translate(0, 0); }
      50% { transform: rotateX(45deg) rotateY(45deg) translate(-10px, -15px); }
    }

    /* ===== 标题 ===== */
    h1 {
      font-size: 2.2em;
      text-align: center;
      margin: 20px 0;
      color: #4dff91;
      text-shadow: 0 0 10px rgba(77, 255, 145, 0.7);
      letter-spacing: 2px;
    }

    /* ===== 选项卡 ===== */
    .tab-header {
      display: flex;
      background: rgba(0, 30, 60, 0.7);
      border-bottom: 2px solid #00b0ff;
    }
    .tab-btn {
      flex: 1;
      padding: 14px;
      border: none;
      background: transparent;
      color: #bbdefb;
      font-family: inherit;
      font-size: 1.1em;
      cursor: pointer;
      transition: all 0.3s;
    }
    .tab-btn:hover {
      background: rgba(0, 100, 200, 0.3);
      color: white;
    }
    .tab-btn.active {
      background: #00b0ff;
      color: #001f3f;
      box-shadow: inset 0 -3px 0 #0069c0;
    }

    /* ===== 内容区 ===== */
    .tab-content {
      display: none;
      padding: 25px;
      text-align: center;
    }
    .tab-content.active {
      display: block;
      animation: fadeIn 0.5s;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* ===== 信息区块 ===== */
    .server-address,
    .version-info,
    .status,
    .wechat-box {
      background: rgba(0, 30, 60, 0.6);
      border: 1px solid #00b0ff;
      border-radius: 10px;
      padding: 12px;
      margin: 15px 0;
      font-family: monospace;
      font-size: 1.1em;
    }
    .server-address {
      color: #4fc3f7;
      font-weight: bold;
    }
    .version-info {
      color: #ffcc80;
    }
    .status {
      color: #a5d6a7;
    }
    .wechat {
      color: #ffab91;
      font-size: 1.3em;
      font-weight: bold;
    }

    /* ===== 列表样式 ===== */
    .rules-list, .download-list {
      text-align: left;
      max-width: 500px;
      margin: 15px auto;
      line-height: 1.7;
      padding-left: 20px;
    }
    .rules-list li, .download-list li {
      margin: 8px 0;
    }

    /* ===== 链接 ===== */
    a {
      color: #4fc3f7;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }

    /* ===== 响应式 ===== */
    @media (max-width: 600px) {
      h1 { font-size: 1.8em; }
      .tab-btn { padding: 12px 8px; font-size: 1em; }
    }
  </style>
</head>
<body>
  <!-- 动态星空背景 -->
  <canvas id="bg"></canvas>

  <!-- 装饰性3D方块 -->
  <div class="cube cube1"></div>
  <div class="cube cube2"></div>
  <div class="cube cube3"></div>

  <div class="card">
    <div class="tab-header">
      <button class="tab-btn active" onclick="openTab('home')">🏠 首页</button>
      <button class="tab-btn" onclick="openTab('rules')">📜 规则</button>
      <button class="tab-btn" onclick="openTab('download')">⬇️ 下载</button>
    </div>

    <!-- 首页 -->
    <div id="home" class="tab-content active">
      <h1>⛏️ SIMPFUN SERVER</h1>
      
      <div class="server-address">play.simpfun.cn:23851</div>
      <div class="version-info">🧱 VERSION: 1.20.1 (FORGE)</div>

      <div class="status">
        👥 PLAYERS: <span id="players">LOADING...</span><br>
        🕒 STATUS: <span id="status">CHECKING...</span>
      </div>

      <div class="wechat-box">
        💬 WECHAT:<br>
        <span class="wechat">zhonghh1116</span>
      </div>
    </div>

    <!-- 规则 -->
    <div id="rules" class="tab-content">
      <h1>📜 RULES</h1>
      <ul class="rules-list">
        <li>✅ MUST USE FORGE 1.20.1 CLIENT</li>
        <li>🚫 NO GRIEFING / CHEATING</li>
        <li>💬 BE RESPECTFUL IN CHAT</li>
        <li>🔒 BUILD FREELY IN YOUR CLAIM</li>
        <li>❓ CONTACT ADMIN IF NEEDED</li>
      </ul>
    </div>

    <!-- 下载 -->
    <div id="download" class="tab-content">
      <h1>⬇️ INSTALL GUIDE</h1>
      <ol class="download-list">
        <li>INSTALL <a href="https://adoptium.net/temurin/releases/?version=17" target="_blank">JAVA 17</a></li>
        <li>DOWNLOAD <a href="https://files.minecraftforge.net/net/minecraftforge/forge/index_1.20.1.html" target="_blank">FORGE 1.20.1</a></li>
        <li>RUN INSTALLER → "Install client"</li>
        <li>LAUNCH MINECRAFT WITH FORGE PROFILE</li>
        <li>JOIN: <code>play.simpfun.cn:23851</code></li>
      </ol>
      <p style="color:#ff8a80; margin-top:15px; font-weight:bold;">
        ⚠️ FORGE REQUIRED!
      </p>
    </div>
  </div>

  <script>
    // ===== 星空背景脚本 =====
    const canvas = document.getElementById('bg');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const stars = [];
    for (let i = 0; i < 150; i++) {
      stars.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        size: Math.random() * 2,
        speed: Math.random() * 0.5 + 0.1,
        opacity: Math.random() * 0.8 + 0.2
      });
    }

    function animateStars() {
      ctx.fillStyle = 'rgba(12, 12, 22, 0.1)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      stars.forEach(star => {
        star.y -= star.speed;
        if (star.y < 0) star.y = canvas.height;
        if (star.x < 0) star.x = canvas.width;
        if (star.x > canvas.width) star.x = 0;

        ctx.beginPath();
        ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(100, 200, 255, ${star.opacity})`;
        ctx.fill();
      });
      requestAnimationFrame(animateStars);
    }
    animateStars();

    window.addEventListener('resize', () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });

    // ===== 选项卡切换 =====
    function openTab(tabName) {
      document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.getElementById(tabName).classList.add('active');
      event.target.classList.add('active');
    }

    // ===== 服务器状态更新 =====
    async function updateStatus() {
      try {
        const res = await fetch('https://api.mcsrvstat.us/3/play.simpfun.cn:23851');
        const data = await res.json();
        if (data.online) {
          document.getElementById('players').textContent = `${data.players.online} / ${data.players.max}`;
          document.getElementById('status').innerHTML = '<span style="color:#a5d6a7">🟢 ONLINE</span>';
        } else {
          document.getElementById('players').textContent = '0 / ?';
          document.getElementById('status').innerHTML = '<span style="color:#ff8a80">🔴 OFFLINE</span>';
        }
      } catch (e) {
        document.getElementById('players').textContent = 'ERROR';
        document.getElementById('status').innerHTML = '<span style="color:#ffb300">⚠️ FAILED</span>';
      }
    }

    updateStatus();
    setInterval(updateStatus, 30000);
  </script>
</body>
</html>
