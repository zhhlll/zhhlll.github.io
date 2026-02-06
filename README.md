index.html
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
      margin: 40px auto;
      background: white;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.1);
      text-align: center;
    }
    h1 {
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
  </style>
</head>
<body>
  <div class="card">
    <h1>⛏️ SimpFun Minecraft 服务器</h1>
    
    <div class="server-address">play.simpfun.cn:23851</div>

    <div class="status">
      <p>👥 当前玩家：<span id="players">加载中...</span></p>
      <p>🕒 状态：<span id="status">检测中...</span></p>
    </div>

    <div style="margin-top: 25px;">
      <p>💬 服主微信：<br><span class="wechat">zhonghh1116</span></p>
      <p style="font-size: 0.9em; color: #555;">添加时请备注“Minecraft”</p>
    </div>
  </div>

  <script>
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
