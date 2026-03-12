<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Starship Alves Empire Dashboard 🚀</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      background: #000;
      color: #e0e0e0;
      margin: 0;
      padding: 0;
      min-height: 100vh;
      overflow-y: auto;
      overflow-x: hidden;
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
    }
    body::before {
      content: "";
      position: fixed;
      inset: 0;
      background: radial-gradient(ellipse at bottom, #0b001f 0%, #000 100%);
      z-index: -3;
    }
    .stars {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: -2;
      background-image:
        radial-gradient(2px 2px at 20% 30%, #eee, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 80% 70%, #fff, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 50% 10%, #ddd, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 10% 90%, #eee, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 60% 50%, #fff, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 40% 80%, #ddd, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 90% 20%, #eee, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 30% 60%, #fff, rgba(0,0,0,0));
      background-repeat: repeat;
      background-size: 200px 200px, 300px 300px, 250px 250px, 400px 400px, 350px 350px, 280px 280px, 320px 320px, 270px 270px;
      opacity: 0.6;
      animation: drift 120s linear infinite;
    }
    .stars::before {
      content: "";
      position: absolute;
      inset: 0;
      background-image:
        radial-gradient(1px 1px at 15% 45%, #ccc, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 85% 55%, #ddd, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 55% 25%, #eee, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 25% 75%, #fff, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 70% 40%, #ddd, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 35% 85%, #eee, rgba(0,0,0,0));
      background-repeat: repeat;
      background-size: 150px 150px, 220px 220px, 180px 180px, 260px 260px, 200px 200px, 240px 240px;
      opacity: 0.4;
      animation: twinkle 8s infinite alternate, drift 180s linear infinite reverse;
    }
    .stars::after {
      content: "";
      position: absolute;
      inset: 0;
      background-image:
        radial-gradient(1px 1px at 5% 15%, #bbb, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 95% 85%, #ccc, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 45% 65%, #ddd, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 75% 35%, #eee, rgba(0,0,0,0));
      background-repeat: repeat;
      background-size: 100px 100px, 140px 140px, 120px 120px, 160px 160px;
      opacity: 0.3;
      animation: twinkle 10s infinite alternate, drift 150s linear infinite;
    }
    @keyframes twinkle { 0%, 100% { opacity: 0.3; } 50% { opacity: 0.8; } }
    @keyframes drift { from { transform: translateY(0); } to { transform: translateY(-400px); } }

    .container {
      width: 94%;
      max-width: 1200px;
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 0 80px;
    }
    .grid, .top-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 40px;
      width: 100%;
      margin: 0 auto;
      padding: 0 10px;
    }
    .top-grid { margin-bottom: 40px; }
    .channel, .header-cell, .placeholder-channel {
      background: rgba(22, 27, 34, 0.75);
      border: 1px solid #30363d;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 8px 30px rgba(0,0,0,0.8);
      backdrop-filter: blur(8px);
      min-height: 240px;
      display: flex;
      align-items: flex-start;
      gap: 30px;
      position: relative;
    }
    .header-cell {
      justify-content: center;
      align-items: center;
      min-height: auto;
      padding: 20px;
      cursor: pointer;
      position: relative;
    }
    .header-logo-container {
      position: relative;
      display: inline-block;
    }
    .header-logo {
      width: 360px;
      height: 360px;
      border-radius: 50%;
      object-fit: cover;
      border: 8px solid #30363d;
      box-shadow: 0 12px 50px rgba(88,166,255,0.5);
      transition: opacity 0.3s;
    }
    .choose-main-overlay {
      position: absolute;
      inset: 0;
      background: rgba(0,0,0,0.6);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 0;
      transition: opacity 0.3s;
      pointer-events: none;
      color: #ccc;
      font-size: 1.4rem;
      font-weight: bold;
      text-align: center;
      padding: 20px;
    }
    .header-logo-container:hover .choose-main-overlay {
      opacity: 1;
    }
    .logo {
      width: 160px;
      height: 160px;
      border-radius: 50%;
      object-fit: cover;
      border: 6px solid #30363d;
      flex-shrink: 0;
    }
    .emoji-logo {
      width: 160px;
      height: 160px;
      border-radius: 50%;
      border: 6px solid #30363d;
      flex-shrink: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 100px;
    }
    .stats-group {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      gap: 16px;
    }
    .stats {
      font-size: clamp(2.0rem, 5.5vw, 2.8rem);
      font-weight: bold;
      display: flex;
      align-items: center;
      gap: 16px;
    }
    .subs, .subs span { color: #a27ccc !important; }
    .views, .views span { color: #558ce6 !important; }
    .videos { color: #696969; }
    .days-number {
      font-size: 2.4rem;
      font-weight: bold;
      letter-spacing: 1px;
      text-align: center;
    }
    .placeholder-channel {
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: #666;
      opacity: 0.8;
      cursor: pointer;
    }
    .add-channel-text {
      margin-top: 20px;
      font-size: 1.8rem;
      font-weight: bold;
      text-align: center;
    }
    .edit-icon {
      position: absolute;
      top: 12px;
      right: 12px;
      font-size: 1.6rem;
      cursor: pointer;
      color: #888;
      background: rgba(0,0,0,0.5);
      border-radius: 50%;
      width: 32px;
      height: 32px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .edit-icon:hover {
      color: #fff;
      background: #555;
    }
    .footer {
      margin-top: 60px;
      padding: 20px;
      text-align: center;
      color: #666;
      font-size: 1rem;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-wrap: wrap;
      gap: 12px;
    }
    .footer a {
      color: #a27ccc;
      text-decoration: none;
    }
    .footer a:hover { text-decoration: underline; }
    .footer button {
      background: transparent;
      border: none;
      color: #666;
      font-size: 0.95rem;
      cursor: pointer;
      padding: 0 8px;
      text-decoration: underline;
    }
    .footer button:hover { color: #a27ccc; }

    /* Modal styles */
    #api-modal, #channel-modal, #main-select-modal {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.8);
      z-index: 999;
      align-items: center;
      justify-content: center;
    }
    .modal-content {
      background: #111;
      border: 1px solid #444;
      border-radius: 16px;
      padding: 32px;
      max-width: 500px;
      width: 90%;
      color: #eee;
      position: relative;
    }
    .close-btn {
      position: absolute;
      top: 12px;
      right: 16px;
      font-size: 2rem;
      cursor: pointer;
      color: #888;
    }
    input, button, select {
      padding: 12px;
      margin: 8px 0;
      width: 100%;
      border-radius: 8px;
      border: 1px solid #444;
      background: #222;
      color: #eee;
      font-size: 1.1rem;
    }
    button {
      background: #a27ccc;
      border: none;
      cursor: pointer;
    }
    button:hover { background: #b38dd1; }
  </style>
</head>
<body>
  <div class="stars"></div>
  <div class="container">
    <div class="top-grid" id="top-grid"></div>
    <div class="grid" id="channel-grid"></div>
    <div class="footer">
      Created by <a href="https://www.youtube.com/@StarshipAlves" target="_blank">@StarshipAlves</a>
      <button onclick="document.getElementById('api-modal').style.display='flex'">Add / Edit API Key</button>
      <button onclick="fetchData()">Refresh Data</button>
    </div>
  </div>

  <!-- API Key Modal -->
  <div id="api-modal">
    <div class="modal-content">
      <span class="close-btn" onclick="document.getElementById('api-modal').style.display='none'">×</span>
      <h2>API Key Setup</h2>
      <p style="color:#aaa;">
        Enter your YouTube Data API v3 key.<br>
        Get one free: <a href="https://console.cloud.google.com/apis/library/youtube.googleapis.com" target="_blank" style="color:#a27ccc;">console.cloud.google.com</a>
      </p>
      <input type="text" id="api-key-input" placeholder="AIzaSy...">
      <button onclick="saveApiKey()">Save</button>
      <p id="api-error" style="color:#ff5555;"></p>
    </div>
  </div>

  <!-- Add/Edit Channel Modal -->
  <div id="channel-modal">
    <div class="modal-content">
      <span class="close-btn" onclick="document.getElementById('channel-modal').style.display='none'">×</span>
      <h2 id="modal-title">Add Channel</h2>
      <input type="text" id="ch-name" placeholder="Channel Name">
      <input type="text" id="ch-id" placeholder="Channel ID (UC...)">
      <input type="text" id="ch-logo" placeholder="Custom logo URL (optional)">
      <button onclick="saveChannel()">Save</button>
      <p id="ch-error" style="color:#ff5555;"></p>
    </div>
  </div>

  <!-- Main Logo Selector Modal -->
  <div id="main-select-modal">
    <div class="modal-content">
      <span class="close-btn" onclick="document.getElementById('main-select-modal').style.display='none'">×</span>
      <h2>Choose Channel for Large Logo</h2>
      <p style="color:#aaa;">Select which channel should appear big at the top:</p>
      <select id="main-channel-select">
        <option value="">-- None --</option>
      </select>
      <button onclick="saveMainChannel()">Set as Large Logo</button>
    </div>
  </div>

  <script>
    let channels = JSON.parse(localStorage.getItem('myChannels')) || [];
    let apiKey = localStorage.getItem('youtubeApiKey') || '';
    let mainChannelId = localStorage.getItem('mainChannelId') || null;

    function saveApiKey() {
      const key = document.getElementById('api-key-input').value.trim();
      if (key && key.startsWith('AIzaSy')) {
        localStorage.setItem('youtubeApiKey', key);
        apiKey = key;
        document.getElementById('api-modal').style.display = 'none';
        fetchData();
      } else {
        document.getElementById('api-error').textContent = 'Invalid key format';
      }
    }

    let editingIndex = -1;

    function openAddChannel(index = -1) {
      editingIndex = index;
      document.getElementById('modal-title').textContent = index === -1 ? 'Add Channel' : 'Edit Channel';
      if (index >= 0) {
        const ch = channels[index];
        document.getElementById('ch-name').value = ch.name || '';
        document.getElementById('ch-id').value = ch.id || '';
        document.getElementById('ch-logo').value = ch.customLogo || '';
      } else {
        document.getElementById('ch-name').value = '';
        document.getElementById('ch-id').value = '';
        document.getElementById('ch-logo').value = '';
      }
      document.getElementById('channel-modal').style.display = 'flex';
    }

    function saveChannel() {
      const name = document.getElementById('ch-name').value.trim();
      const id = document.getElementById('ch-id').value.trim();
      const logo = document.getElementById('ch-logo').value.trim();

      if (!name || !id || !id.startsWith('UC')) {
        document.getElementById('ch-error').textContent = 'Name and valid Channel ID required';
        return;
      }

      const channel = { name, id, customLogo: logo || null };

      if (editingIndex >= 0) {
        channels[editingIndex] = channel;
      } else {
        channels.push(channel);
      }

      localStorage.setItem('myChannels', JSON.stringify(channels));
      document.getElementById('channel-modal').style.display = 'none';
      fetchData();
    }

    function openMainSelect() {
      const select = document.getElementById('main-channel-select');
      select.innerHTML = '<option value="">-- None --</option>';
      channels.forEach(ch => {
        const opt = document.createElement('option');
        opt.value = ch.id;
        opt.textContent = `${ch.name} (${ch.id})`;
        if (ch.id === mainChannelId) opt.selected = true;
        select.appendChild(opt);
      });
      document.getElementById('main-select-modal').style.display = 'flex';
    }

    function saveMainChannel() {
      const selectedId = document.getElementById('main-channel-select').value;
      if (selectedId) {
        localStorage.setItem('mainChannelId', selectedId);
        mainChannelId = selectedId;
      } else {
        localStorage.removeItem('mainChannelId');
        mainChannelId = null;
      }
      document.getElementById('main-select-modal').style.display = 'none';
      fetchData();
    }

    async function fetchData() {
      const grid = document.getElementById('channel-grid');
      const topGrid = document.getElementById('top-grid');
      grid.innerHTML = '<p style="text-align:center; color:#8b949e; font-size:1.2rem;">Loading...</p>';
      topGrid.innerHTML = '';

      if (!apiKey) {
        grid.innerHTML = '<p style="text-align:center; color:#ff5555; font-size:1.4rem;">Add your API key at the bottom</p>';
        return;
      }

      try {
        const ids = channels.map(c => c.id).join(',');
        let mainLogoUrl = 'https://via.placeholder.com/360x360/111/eee?text=CHOOSE+CHANNEL+FOR+LARGE+LOGO';

        let channelData = [];
        if (ids) {
          const chRes = await fetch(
            `https://www.googleapis.com/youtube/v3/channels?part=statistics,snippet,contentDetails&id=${ids}&key=${apiKey}`
          );
          if (!chRes.ok) throw new Error(`API error: ${chRes.status}`);
          const chData = await chRes.json();

          channelData = await Promise.all(chData.items.map(async (item, idx) => {
            const ch = channels[idx];
            const logo = ch.customLogo || item.snippet?.thumbnails?.medium?.url || 'https://via.placeholder.com/160?text=Logo';

            if (ch.id === mainChannelId) mainLogoUrl = logo;

            let daysSince = '—', daysColor = '#555555';
            const uploadsId = item.contentDetails?.relatedPlaylists?.uploads;
            if (uploadsId) {
              const plRes = await fetch(
                `https://www.googleapis.com/youtube/v3/playlistItems?part=snippet&maxResults=1&order=date&playlistId=${uploadsId}&key=${apiKey}`
              );
              if (plRes.ok) {
                const plData = await plRes.json();
                if (plData.items?.length) {
                  const diffDays = Math.floor((new Date() - new Date(plData.items[0].snippet.publishedAt)) / 86400000);
                  if (diffDays >= 0) {
                    daysSince = diffDays;
                    daysColor = diffDays <= 3 ? '#00ff00' : diffDays <= 7 ? '#ffff00' : '#ff0000';
                  }
                }
              }
            }

            return { ...ch, logo, subs: parseInt(item.statistics?.subscriberCount||0), views: parseInt(item.statistics?.viewCount||0), videos: parseInt(item.statistics?.videoCount||0), daysSince, daysColor };
          }));
        }

        renderTop(mainLogoUrl, channelData);
        renderChannels(channelData);

      } catch (err) {
        grid.innerHTML = `<p style="text-align:center; color:#ff5555; font-size:1.4rem;">Error: ${err.message}</p>`;
      }
    }

    function renderTop(mainLogoUrl, channelData) {
      const topGrid = document.getElementById('top-grid');
      topGrid.innerHTML = '';

      const headerDiv = document.createElement('div');
      headerDiv.className = 'header-cell';
      headerDiv.innerHTML = `
        <div class="header-logo-container" onclick="document.getElementById('main-select-modal').style.display='flex'">
          <img class="header-logo" src="${mainLogoUrl}" alt="Main Logo">
          <div class="choose-main-overlay">
            + CHOOSE CHANNEL ID FOR LARGE LOGO
          </div>
        </div>
      `;
      topGrid.appendChild(headerDiv);

      const totalSubs   = channelData.reduce((sum, ch) => sum + (ch.subs   || 0), 0);
      const totalViews  = channelData.reduce((sum, ch) => sum + (ch.views  || 0), 0);
      const totalVideos = channelData.reduce((sum, ch) => sum + (ch.videos || 0), 0);

      const totalDiv = document.createElement('div');
      totalDiv.className = 'channel';
      totalDiv.innerHTML = `
        <div class="emoji-logo">🚀</div>
        <div class="stats-group">
          <div class="stats subs"><span>👤</span> ${totalSubs.toLocaleString()}</div>
          <div class="stats views"><span>👁</span> ${totalViews.toLocaleString()}</div>
          <div class="stats videos"><span>🎬</span> ${totalVideos.toLocaleString()}</div>
        </div>
      `;
      topGrid.appendChild(totalDiv);
    }

    function renderChannels(data) {
      const grid = document.getElementById('channel-grid');
      grid.innerHTML = '';

      data.forEach((ch, i) => {
        const div = document.createElement('div');
        div.className = 'channel';
        div.innerHTML = `
          <span class="edit-icon" onclick="openAddChannel(${i})">✏️</span>
          <div style="display:flex;flex-direction:column;align-items:center;min-width:160px;gap:10px;">
            <img class="logo" src="${ch.logo}" alt="${ch.name}" onerror="this.src='https://via.placeholder.com/160?text=Logo';">
            <div class="days-number" style="color:${ch.daysColor};">📅 ${ch.daysSince}</div>
          </div>
          <div class="stats-group">
            <div class="stats subs"><span>👤</span> ${ch.subs.toLocaleString()}</div>
            <div class="stats views"><span>👁</span> ${ch.views.toLocaleString()}</div>
            <div class="stats videos"><span>🎬</span> ${ch.videos.toLocaleString()}</div>
          </div>
        `;
        grid.appendChild(div);
      });

      const placeholdersNeeded = 12 - data.length;
      for (let i = 0; i < placeholdersNeeded; i++) {
        const ph = document.createElement('div');
        ph.className = 'placeholder-channel channel';
        ph.innerHTML = `
          <div style="cursor:pointer;" onclick="document.getElementById('channel-modal').style.display='flex'">
            <div style="font-size:5rem; opacity:0.6;">+</div>
            <div class="add-channel-text">ADD CHANNEL</div>
          </div>
        `;
        grid.appendChild(ph);
      }
    }

    window.onload = () => {
      fetchData();
    };
  </script>
</body>
</html>
