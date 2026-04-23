<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>解謎地圖 — 網站原型</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:system-ui,sans-serif;background:#F5F4F0;color:#1a1a1a;font-size:15px}
.nav{background:#fff;border-bottom:1px solid #e5e5e5;padding:0 24px;display:flex;align-items:center;justify-content:space-between;height:56px;position:sticky;top:0;z-index:10}
.logo{font-size:18px;font-weight:600;color:#534AB7;display:flex;align-items:center;gap:8px}
.logo-icon{width:30px;height:30px;background:#EEEDFE;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:15px}
.nav-links{display:flex;gap:4px}
.nav-link{padding:6px 14px;font-size:13px;color:#666;border-radius:20px;cursor:pointer;border:none;background:none;transition:all 0.15s}
.nav-link:hover{background:#f0f0f0;color:#222}
.nav-link.active{background:#EEEDFE;color:#534AB7;font-weight:600}
.hero{background:linear-gradient(135deg,#EEEDFE 0%,#E1F5EE 100%);padding:48px 24px 36px;text-align:center}
.hero h1{font-size:30px;font-weight:700;color:#3C3489;margin-bottom:10px}
.hero p{font-size:15px;color:#5F5E5A;margin-bottom:24px}
.search-wrap{position:relative;display:inline-block}
.search-bar{background:#fff;border:1px solid #ccc;border-radius:24px;padding:10px 20px 10px 40px;font-size:14px;width:360px;outline:none;transition:border 0.2s}
.search-bar:focus{border-color:#7F77DD}
.search-icon{position:absolute;left:14px;top:50%;transform:translateY(-50%);color:#999;font-size:15px}
.filter-bar{background:#fff;border-bottom:1px solid #e5e5e5;padding:12px 24px;display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.filter-label{font-size:12px;color:#999;margin-right:2px}
.tag{padding:5px 13px;border-radius:16px;font-size:12px;border:1px solid #ddd;cursor:pointer;background:#fff;color:#555;transition:all 0.15s}
.tag:hover{border-color:#AFA9EC;color:#534AB7;background:#EEEDFE}
.tag.active{background:#EEEDFE;border-color:#AFA9EC;color:#534AB7;font-weight:600}
.divider{width:1px;height:20px;background:#e5e5e5;margin:0 6px}
.main{padding:28px 24px;max-width:960px;margin:0 auto}
.section-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px}
.section-title{font-size:16px;font-weight:600}
.see-all{font-size:13px;color:#534AB7;cursor:pointer;background:none;border:none;padding:0}
.cards{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:18px;margin-bottom:36px}
.card{background:#fff;border:1px solid #e5e5e5;border-radius:14px;overflow:hidden;cursor:pointer;transition:all 0.18s}
.card:hover{border-color:#AFA9EC;transform:translateY(-2px);box-shadow:0 4px 16px rgba(83,74,183,0.1)}
.card-img{height:140px;position:relative;display:flex;align-items:center;justify-content:center;font-size:48px}
.card-badge{position:absolute;top:10px;right:10px;font-size:11px;padding:3px 10px;border-radius:10px;font-weight:600}
.badge-purple{background:#EEEDFE;color:#534AB7}
.badge-green{background:#EAF3DE;color:#3B6D11}
.badge-amber{background:#FAEEDA;color:#854F0B}
.card-body{padding:14px}
.card-title{font-size:14px;font-weight:600;margin-bottom:5px;line-height:1.4}
.card-meta{font-size:12px;color:#888;margin-bottom:8px;display:flex;gap:10px}
.stars{color:#EF9F27;font-size:14px;letter-spacing:1px;margin-bottom:8px}
.diff-bar{display:flex;align-items:center;gap:8px;margin-bottom:10px}
.diff-label{font-size:11px;color:#aaa;width:36px}
.diff-track{flex:1;height:5px;background:#f0f0f0;border-radius:3px}
.diff-fill{height:100%;border-radius:3px;background:#7F77DD}
.card-tags{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:12px}
.card-tag{font-size:11px;padding:2px 8px;border-radius:10px;background:#f5f5f5;color:#666}
.card-btn{display:block;width:100%;padding:8px;font-size:13px;border-radius:8px;border:1px solid #AFA9EC;background:#EEEDFE;color:#534AB7;cursor:pointer;font-weight:600;text-align:center;transition:background 0.15s}
.card-btn:hover{background:#CECBF6}
.map-section{background:#fff;border:1px solid #e5e5e5;border-radius:14px;overflow:hidden;margin-bottom:32px}
.map-header{padding:14px 18px;border-bottom:1px solid #e5e5e5;display:flex;justify-content:space-between;align-items:center}
.map-area{height:200px;background:#E1F5EE;display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden}
.map-placeholder{text-align:center;color:#0F6E56}
.map-placeholder .icon{font-size:40px;margin-bottom:8px}
.map-placeholder p{font-size:13px}
.pin{position:absolute;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer}
.pin-dot{width:36px;height:36px;background:#534AB7;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#EEEDFE;font-size:12px;font-weight:600;border:3px solid #fff;box-shadow:0 2px 8px rgba(83,74,183,0.3)}
.pin-label{font-size:11px;color:#3C3489;font-weight:600;background:#fff;padding:2px 7px;border-radius:5px;box-shadow:0 1px 4px rgba(0,0,0,0.1);white-space:nowrap}
.ad-slot{background:#f9f9f9;border:1px dashed #ccc;border-radius:10px;height:90px;display:flex;align-items:center;justify-content:center;margin-bottom:28px;color:#bbb;font-size:13px}
.footer{background:#fff;border-top:1px solid #e5e5e5;padding:20px 24px;text-align:center;color:#aaa;font-size:12px}
 
/* tag toggle behavior */
.filter-group .tag.active{background:#EEEDFE;border-color:#AFA9EC;color:#534AB7;font-weight:600}
</style>
</head>
<body>
 
<nav class="nav">
  <div class="logo">
    <div class="logo-icon">🔐</div>
    解謎地圖
  </div>
  <div class="nav-links">
    <button class="nav-link active" onclick="switchTab(this)">密室逃脫</button>
    <button class="nav-link" onclick="switchTab(this)">解謎 App</button>
    <button class="nav-link" onclick="switchTab(this)">桌遊推薦</button>
    <button class="nav-link" onclick="switchTab(this)">地圖</button>
  </div>
</nav>
 
<div class="hero">
  <h1>找到你的下一個解謎挑戰</h1>
  <p>密室逃脫心得、App 推薦、桌遊評測，全都在這裡</p>
  <div class="search-wrap">
    <span class="search-icon">🔍</span>
    <input class="search-bar" type="text" placeholder="搜尋主題、地點、難易度...">
  </div>
</div>
 
<div class="filter-bar">
  <span class="filter-label">縣市</span>
  <div class="filter-group" id="city-group">
    <button class="tag active" onclick="toggleTag(this,'city-group')">全部</button>
    <button class="tag" onclick="toggleTag(this,'city-group')">台北</button>
    <button class="tag" onclick="toggleTag(this,'city-group')">台中</button>
    <button class="tag" onclick="toggleTag(this,'city-group')">高雄</button>
    <button class="tag" onclick="toggleTag(this,'city-group')">台南</button>
    <button class="tag" onclick="toggleTag(this,'city-group')">新竹</button>
  </div>
  <div class="divider"></div>
  <span class="filter-label">星等</span>
  <div class="filter-group" id="star-group">
    <button class="tag active" onclick="toggleTag(this,'star-group')">全部</button>
    <button class="tag" onclick="toggleTag(this,'star-group')">★★★★★</button>
    <button class="tag" onclick="toggleTag(this,'star-group')">★★★★+</button>
  </div>
  <div class="divider"></div>
  <span class="filter-label">難易度</span>
  <div class="filter-group" id="diff-group">
    <button class="tag active" onclick="toggleTag(this,'diff-group')">全部</button>
    <button class="tag" onclick="toggleTag(this,'diff-group')">入門</button>
    <button class="tag" onclick="toggleTag(this,'diff-group')">普通</button>
    <button class="tag" onclick="toggleTag(this,'diff-group')">困難</button>
  </div>
</div>
 
<div class="main">
 
  <!-- 廣告位 -->
  <div class="ad-slot">📢 廣告位置（Google AdSense）</div>
 
  <!-- 密室逃脫心得 -->
  <div class="section-header">
    <div class="section-title">🏠 最新密室逃脫心得</div>
    <button class="see-all">查看全部 →</button>
  </div>
  <div class="cards">
    <div class="card" onclick="alert('跳到完整心得頁面')">
      <div class="card-img" style="background:#EEEDFE">🕵️<span class="card-badge badge-purple">密室逃脫</span></div>
      <div class="card-body">
        <div class="card-title">【台北】謎屋 — 失落的密碼</div>
        <div class="card-meta"><span>📍 台北信義區</span><span>⏱ 60 分鐘</span></div>
        <div class="stars">★★★★★</div>
        <div class="diff-bar">
          <span class="diff-label">難易度</span>
          <div class="diff-track"><div class="diff-fill" style="width:80%"></div></div>
          <span style="font-size:11px;color:#888">4/5</span>
        </div>
        <div class="card-tags">
          <span class="card-tag">台北</span><span class="card-tag">困難</span><span class="card-tag">2–4人</span><span class="card-tag">懸疑</span>
        </div>
        <button class="card-btn">查看完整心得 →</button>
      </div>
    </div>
 
    <div class="card" onclick="alert('跳到完整心得頁面')">
      <div class="card-img" style="background:#E1F5EE">🧪<span class="card-badge badge-green">密室逃脫</span></div>
      <div class="card-body">
        <div class="card-title">【高雄】謎城 — 瘋狂實驗室</div>
        <div class="card-meta"><span>📍 高雄前金區</span><span>⏱ 75 分鐘</span></div>
        <div class="stars">★★★★☆</div>
        <div class="diff-bar">
          <span class="diff-label">難易度</span>
          <div class="diff-track"><div class="diff-fill" style="width:60%"></div></div>
          <span style="font-size:11px;color:#888">3/5</span>
        </div>
        <div class="card-tags">
          <span class="card-tag">高雄</span><span class="card-tag">普通</span><span class="card-tag">2–6人</span><span class="card-tag">科幻</span>
        </div>
        <button class="card-btn">查看完整心得 →</button>
      </div>
    </div>
 
    <div class="card" onclick="alert('跳到完整心得頁面')">
      <div class="card-img" style="background:#FAEEDA">👻<span class="card-badge badge-amber">密室逃脫</span></div>
      <div class="card-body">
        <div class="card-title">【台中】逃脫工廠 — 鬼屋驚魂</div>
        <div class="card-meta"><span>📍 台中西屯區</span><span>⏱ 60 分鐘</span></div>
        <div class="stars">★★★★★</div>
        <div class="diff-bar">
          <span class="diff-label">難易度</span>
          <div class="diff-track"><div class="diff-fill" style="width:90%"></div></div>
          <span style="font-size:11px;color:#888">5/5</span>
        </div>
        <div class="card-tags">
          <span class="card-tag">台中</span><span class="card-tag">困難</span><span class="card-tag">3–5人</span><span class="card-tag">恐怖</span>
        </div>
        <button class="card-btn">查看完整心得 →</button>
      </div>
    </div>
  </div>
 
  <!-- 解謎App -->
  <div class="section-header">
    <div class="section-title">📱 解謎 App 推薦</div>
    <button class="see-all">查看全部 →</button>
  </div>
  <div class="cards">
    <div class="card">
      <div class="card-img" style="background:#EAF3DE">📦<span class="card-badge badge-green">App</span></div>
      <div class="card-body">
        <div class="card-title">The Room — 精緻機械解謎</div>
        <div class="card-meta"><span>📱 iOS / Android</span><span>💰 付費</span></div>
        <div class="stars">★★★★★</div>
        <div class="diff-bar">
          <span class="diff-label">難易度</span>
          <div class="diff-track"><div class="diff-fill" style="width:50%"></div></div>
          <span style="font-size:11px;color:#888">3/5</span>
        </div>
        <div class="card-tags"><span class="card-tag">單人</span><span class="card-tag">普通</span><span class="card-tag">3D解謎</span></div>
        <button class="card-btn">查看評測 + 下載連結 →</button>
      </div>
    </div>
 
    <div class="card">
      <div class="card-img" style="background:#EEEDFE">🌊<span class="card-badge badge-purple">App</span></div>
      <div class="card-body">
        <div class="card-title">Monument Valley — 視覺藝術解謎</div>
        <div class="card-meta"><span>📱 iOS / Android</span><span>💰 付費</span></div>
        <div class="stars">★★★★★</div>
        <div class="diff-bar">
          <span class="diff-label">難易度</span>
          <div class="diff-track"><div class="diff-fill" style="width:35%"></div></div>
          <span style="font-size:11px;color:#888">2/5</span>
        </div>
        <div class="card-tags"><span class="card-tag">單人</span><span class="card-tag">入門</span><span class="card-tag">藝術風格</span></div>
        <button class="card-btn">查看評測 + 下載連結 →</button>
      </div>
    </div>
  </div>
 
  <!-- 地圖 -->
  <div class="section-header">
    <div class="section-title">🗺️ 密室逃脫地圖</div>
    <button class="see-all">查看完整地圖 →</button>
  </div>
  <div class="map-section">
    <div class="map-header">
      <span style="font-size:14px;font-weight:600">台灣密室逃脫分佈圖</span>
      <div style="display:flex;gap:12px;font-size:12px;color:#888">
        <span>🟣 台北 23間</span>
        <span>🟢 台中 15間</span>
        <span>🟠 高雄 12間</span>
      </div>
    </div>
    <div class="map-area">
      <div style="text-align:center;color:#0F6E56;z-index:1">
        <div style="font-size:48px;margin-bottom:8px">🗺️</div>
        <p style="font-size:14px;font-weight:600">互動地圖區塊</p>
        <p style="font-size:12px;margin-top:4px">實際網站會嵌入 Google Maps，可點選查看店家資訊</p>
      </div>
    </div>
  </div>
 
  <!-- 廣告位2 -->
  <div class="ad-slot">📢 廣告位置（Google AdSense）</div>
 
</div>
 
<div class="footer">
  © 2025 解謎地圖 — 以上為網站設計原型預覽
</div>
 
<script>
function switchTab(btn){
  document.querySelectorAll('.nav-link').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
}
function toggleTag(btn, groupId){
  document.querySelectorAll('#'+groupId+' .tag').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
}
</script>
 
</body>
</html>
