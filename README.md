
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AnimeFlix TV</title>
  <style>
    *{margin:0;padding:0;box-sizing:border-box}
    body{background:#000;color:#fff;font-family:Arial;overflow-x:hidden;overflow-y:auto;display:block;min-height:100vh}
    #profileScreen{display:flex;flex-direction:column;justify-content:center;align-items:center;min-height:100vh;background:#000;padding:40px 20px;gap:40px}
    #profileScreen h1{font-size:3.5rem;margin-bottom:20px}
    .profiles-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:40px;max-width:1200px}
    .profile{border:4px solid transparent;border-radius:15px;cursor:pointer;transition:.3s;position:relative}
    .profile:hover{border-color:#e50914;transform:scale(1.08)}
    .profile img{width:180px;height:180px;object-fit:cover;border-radius:12px}
    .profile p{margin-top:12px;font-size:1.7rem;text-align:center;font-weight:bold}
    .continue-btn{background:#e50914;color:#fff;padding:20px 70px;border-radius:50px;font-size:2rem;font-weight:bold;cursor:pointer;margin-top:30px;letter-spacing:1px;box-shadow:0 8px 20px rgba(229,9,20,0.4)}
    .hero{height:100vh;background:linear-gradient(to top,rgba(0,0,0,0.8),rgba(0,0,0,0.2)),url('https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhGQiUFAp-9gjuPUAOcIxcjx5rNtk1nTi1j44thfaSQW5Uuaq88IGDV58tFVfjzdC9mXJ9KcThW0VPDbKEwo03KQD5VMltHZsDke2H1m_chZB8_BsqM79GrOVJDTJwHeXMpYqlVm1m7cwVy3qQxOpQkhExoccS65RGVVl6Tg90oSWXB380zrFcuDttJ/s1600/1000063858.webp') center/cover;display:flex;align-items:flex-end;padding:40px;position:relative}
    .hero h1{font-size:6vw;color:#fff;text-shadow:3px 3px 15px #000;margin-bottom:20px}
    .hero p{font-size:1.8vw;max-width:700px;margin-bottom:30px;opacity:0.9}
    .play-btn{background:#fff;color:#000;padding:20px 60px;font-size:2.5vw;border-radius:8px;cursor:pointer;font-weight:bold;margin-right:20px}
    .info-btn{background:rgba(255,255,255,0.3);color:#fff;padding:20px 50px;font-size:2.5vw;border-radius:8px;cursor:pointer}
    .row{padding:60px 4%}
    .row-title{font-size:2.8vw;margin-bottom:20px}
    .row-container{display:flex;gap:12px;overflow-x:auto;padding:10px 0;scrollbar-width:none}
    .row-container::-webkit-scrollbar{display:none}
    .anime-card{min-width:210px;transition:transform .3s;cursor:pointer;position:relative}
    .anime-card:hover{transform:scale(1.1);outline:5px solid #fff}
    .anime-card img{width:100%;height:300px;object-fit:cover;border-radius:10px}
    .anime-card-title{margin-top:10px;font-size:1.4vw;text-align:center}
    .progress-bg{position:absolute;bottom:0;left:0;width:100%;height:5px;background:rgba(0,0,0,0.7)}
    .progress-fill{height:100%;background:#e50914;width:0%;transition:width .4s}
    #detailsScreen{display:none;flex-direction:column;background:#000;min-height:100vh}
    .details-header{padding:40px 4% 20px;display:flex;gap:30px;flex-wrap:wrap}
    .details-cover img{width:300px;border-radius:12px;box-shadow:0 0 30px rgba(0,0,0,0.8)}
    .details-info h1{font-size:4rem;margin-bottom:20px}
    .episodes-list{padding:0 4% 100px}
    .ep-item{display:flex;gap:20px;margin:15px 0;padding:15px;border-radius:10px;background:#111;cursor:pointer;transition:.3s}
    .ep-item:hover{background:#222}
    .ep-thumb img{width:180px;height:100px;object-fit:cover;border-radius:8px}
    .ep-info{flex:1}
    .ep-title{font-size:1.6rem;font-weight:bold}
    .ep-duration{color:#aaa;margin:8px 0}
    .play-icon{background:#e50914;width:60px;height:60px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:2rem}
    #player-area{display:none;position:fixed;top:0;left:0;width:100vw;height:100vh;background:#000;z-index:9999}
    #player{width:100%;height:100%}
    #backBtn{position:absolute;top:20px;right:20px;background:#e50914;color:#fff;padding:15px 30px;border:none;border-radius:10px;font-size:1.8rem;z-index:99999;cursor:pointer}
  </style>
</head>
<body>

<!-- TELA DE PERFIS -->
<div id="profileScreen">
  <h1>Quem está assistindo?</h1>
  <div class="profiles-grid">
    <div class="profile" onclick="selecionarPerfil('Você')">
      <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXlW9F-g4BHvscdOAj-GS3FRrKxDxWEAsoQyy4eVMBclFdkR9_fsmiFmmPH6bXUzUhLPmrPL1XOM7fT4vKfE1ZtD-nBSvCfKdOZwQotIal_e-y6eH_Pbwk1s3B78UJ6KhWCDFBrcla6ORrpW5oFlohMl-AjAtbdDaCbZkrbZJ9znKPfIj29tq0WWvH/s1600/1000063980.jpg">
      <p>Você</p>
    </div>
    <div class="profile" onclick="selecionarPerfil('Irmã')">
      <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiQ1QvowYNVv4ncAxGC4IKkaNrSJupXBz1Vz9x7IrkmyGCOBgVjNwYe2flbRoNYZBz2wJa0KvFMbZd6OEoRrm8KL3fEXcc7Q0fHm7Pu9J8RGVqWIm_D9z0uUCP39YQ0Q9k3BDr8Yyux0hBCVK8DKGlUfmpgnu-7vQyCMyaAMAaGigfLfIyMY75cCb7t/s1600/1000063979.jpg">
      <p>Irmã</p>
    </div>
    <div class="profile" onclick="selecionarPerfil('Amigo')">
      <img src="https://via.placeholder.com/180/333/fff?text=Amigo">
      <p>Amigo</p>
    </div>
    <div class="profile" onclick="selecionarPerfil('Kids')">
      <img src="https://via.placeholder.com/180/FF69B4/fff?text=Kids">
      <p>Kids</p>
    </div>
  </div>
  <div class="continue-btn" id="continueBtn" onclick="continuarComoAtual()">Continuar como Você</div>
</div>

<!-- TELA PRINCIPAL -->
<div id="mainScreen" style="display:none">
  <div class="hero">
    <div>
      <h1>Tengoku Daimakyou</h1>
      <p>Em um Japão pós-apocalíptico...</p>
      <div class="play-btn" onclick="abrirDetalhes('tengoku')">PLAY</div>
      <div class="info-btn" onclick="abrirDetalhes('tengoku')">Mais informações</div>
    </div>
  </div>

  <div class="row" id="continueSection" style="display:none">
    <div class="row-title">Continue Assistindo</div>
    <div class="row-container" id="continueRow"></div>
  </div>

  <div class="row">
    <div class="row-title">Todos os Animes</div>
    <div class="row-container">
      <div class="anime-card" onclick="abrirDetalhes('nyaruko')">
        <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiRIFbcMhIKhx1hiTTV80Cs1Mrg8oAmF3Q4S9aeEXjzT1GtFLGq1jUoW2QOQKam5SYTaJ5-rnrCAuhKn5-o38jVJeyCF7YMMx2aPO1vZZzbxfIIaVGRuoGnpQEkqXezjd-JLGKC9cmqK90fUkyPgRyySb_EEn0jjKIzpbNhKd7fu6d9Ctd0NN80it4n/s1600/1000058388.webp">
        <div class="anime-card-title">Haiyore! Nyaruko-san W</div>
      </div>
      <div class="anime-card" onclick="abrirDetalhes('sorairo')">
        <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhds2w8BH5JQyBbjsW7O_wjOUPGT8QQ0kBm8CSjsRQ7zH3L15N0RF1hPjLM5SljZyAvcc-eDpRn_mBnOpAXL61sW4Gay9UYvgBbHdR2c9I7bUZ-ECLWmvqGKD3xW3Qpl1bwC7K5PU1OAK6KZasEapUcakTgITCH-5nniL1msMCGKqnZjMgF9ZY7YHvp/s1600/1000057391.jpg">
        <div class="anime-card-title">Sorairo Utility</div>
      </div>
      <div class="anime-card" onclick="abrirDetalhes('tengoku')">
        <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhGQiUFAp-9gjuPUAOcIxcjx5rNtk1nTi1j44thfaSQW5Uuaq88IGDV58tFVfjzdC9mXJ9KcThW0VPDbKEwo03KQD5VMltHZsDke2H1m_chZB8_BsqM79GrOVJDTJwHeXMpYqlVm1m7cwVy3qQxOpQkhExoccS65RGVVl6Tg90oSWXB380zrFcuDttJ/s1600/1000063858.webp">
        <div class="anime-card-title">Tengoku Daimakyou</div>
      </div>
      <div class="anime-card" onclick="abrirDetalhes('gimai')">
        <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiyoAUtT_pUC7Hvvzdb7OdqVRYKfmtd3bDl3z-E8Swcg5q2hyu1IZ-4vUgIde5b-zWeo0hsJ-c1kL87LTeirAzLUXRbBTjvHXLnlPXMwdhTxpON05WnmAcwehukaQepyRYunN7THgKLKDo2drscuIXf1knDW64oF1vEr4cLhFBzpnNJVACDT6uMQ48a/s1600/1000063881.jpg">
        <div class="anime-card-title">Gimai Seikatsu</div>
      </div>
      <!-- NOVO ANIME AQUI -->
      <div class="anime-card" onclick="abrirDetalhes('bisque')">
        <img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhOCE7V0lI4XSVQCBrp5R2xDeNFiux3RXDGI1JO8Z_p2o8yARB-gD7eRPyeh3TN0RanbdkrzspaJjl8yfocLVlnusrtyAgF36cdWxsfsgyXjvQdsMFMowEFctC_T6iLMLPVDyCUZ6SxVX7vw-ar8dGtElSHsbOpUPEvSgyCYYzregcQS8BflZIQ581B/s1600/1000063983.jpg">
        <div class="anime-card-title">Sono Bisque Doll wa Koi o Suru</div>
      </div>
    </div>
  </div>
</div>

<!-- TELA DE DETALHES + PLAYER -->
<div id="detailsScreen">
  <div class="details-header">
    <div class="details-cover"><img id="detailsCover"></div>
    <div class="details-info">
      <h1 id="detailsTitle"></h1>
      <p id="detailsDesc"></p>
      <div class="play-btn" style="margin-top:30px;padding:15px 50px" onclick="playEp(0)">PLAY EPISÓDIO 1</div>
    </div>
  </div>
  <div class="episodes-list" id="episodesList"></div>
</div>

<div id="player-area">
  <video id="player" controls autoplay></video>
  <button id="backBtn" onclick="voltarTela()">VOLTAR</button>
</div>

<script>
  const ANIME = {
    nyaruko: { titulo: "Haiyore! Nyaruko-san W", thumb: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiRIFbcMhIKhx1hiTTV80Cs1Mrg8oAmF3Q4S9aeEXjzT1GtFLGq1jUoW2QOQKam5SYTaJ5-rnrCAuhKn5-o38jVJeyCF7YMMx2aPO1vZZzbxfIIaVGRuoGnpQEkqXezjd-JLGKC9cmqK90fUkyPgRyySb_EEn0jjKIzpbNhKd7fu6d9Ctd0NN80it4n/s1600/1000058388.webp", eps: ["https://lightspeedst.net/s6/mp4/haiyore-nyaruko-san-w-dublado/sd/1.mp4","https://lightspeedst.net/s6/mp4/haiyore-nyaruko-san-w-dublado/sd/2.mp4","https://lightspeedst.net/s6/mp4/haiyore-nyaruko-san-w-dublado/sd/3.mp4","https://lightspeedst.net/s6/mp4/haiyore-nyaruko-san-w-dublado/sd/4.mp4","https://lightspeedst.net/s6/mp4/haiyore-nyaruko-san-w-dublado/sd/5.mp4"] },
    sorairo: { titulo: "Sorairo Utility", thumb: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhds2w8BH5JQyBbjsW7O_wjOUPGT8QQ0kBm8CSjsRQ7zH3L15N0RF1hPjLM5SljZyAvcc-eDpRn_mBnOpAXL61sW4Gay9UYvgBbHdR2c9I7bUZ-ECLWmvqGKD3xW3Qpl1bwC7K5PU1OAK6KZasEapUcakTgITCH-5nniL1msMCGKqnZjMgF9ZY7YHvp/s1600/1000057391.jpg", eps: ["https://lightspeedst.net/s7/mp4_temp/sorairo-utility-tv/1/480p.mp4","https://lightspeedst.net/s7/mp4_temp/sorairo-utility-tv/2/480p.mp4","https://lightspeedst.net/s5/mp4_temp/sorairo-utility-tv/3/480p.mp4"] },
    tengoku: { titulo: "Tengoku Daimakyou", thumb: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhGQiUFAp-9gjuPUAOcIxcjx5rNtk1nTi1j44thfaSQW5Uuaq88IGDV58tFVfjzdC9mXJ9KcThW0VPDbKEwo03KQD5VMltHZsDke2H1m_chZB8_BsqM79GrOVJDTJwHeXMpYqlVm1m7cwVy3qQxOpQkhExoccS65RGVVl6Tg90oSWXB380zrFcuDttJ/s1600/1000063858.webp", eps: ["https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/1.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/2.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/3.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/4.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/5.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/6.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/7.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/8.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/9.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/10.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/11.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/12.mp4","https://lightspeedst.net/s6/mp4/tengoku-daimakyou-dublado/hd/13.mp4"] },
    gimai: { titulo: "Gimai Seikatsu", thumb: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiyoAUtT_pUC7Hvvzdb7OdqVRYKfmtd3bDl3z-E8Swcg5q2hyu1IZ-4vUgIde5b-zWeo0hsJ-c1kL87LTeirAzLUXRbBTjvHXLnlPXMwdhTxpON05WnmAcwehukaQepyRYunN7THgKLKDo2drscuIXf1knDW64oF1vEr4cLhFBzpnNJVACDT6uMQ48a/s1600/1000063881.jpg", eps: ["https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/1.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/2.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/3.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/4.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/5.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/6.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/7.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/8.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/9.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/10.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/11.mp4","https://lightspeedst.net/s7/mp4/gimai-seikatsu/hd/12.mp4"] },
    bisque: { 
      titulo: "Sono Bisque Doll wa Koi o Suru",
      thumb: "https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhOCE7V0lI4XSVQCBrp5R2xDeNFiux3RXDGI1JO8Z_p2o8yARB-gD7eRPyeh3TN0RanbdkrzspaJjl8yfocLVlnusrtyAgF36cdWxsfsgyXjvQdsMFMowEFctC_T6iLMLPVDyCUZ6SxVX7vw-ar8dGtElSHsbOpUPEvSgyCYYzregcQS8BflZIQ581B/s1600/1000063983.jpg",
      eps: [
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/1.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/2.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/3.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/4.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/5.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/6.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/7.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/8.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/9.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/10.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/11.mp4",
        "https://lightspeedst.net/s1/mp4/sono-bisque-doll-wa-koi-wo-suru-dublado/sd/12.mp4"
      ]
    }
  };

  // resto do script 100% igual ao anterior (perfil, continue assistindo, player, tudo funcionando)

  let perfilAtual = localStorage.getItem('perfilAtual') || 'Você';
  let animeAtual = '';
  document.getElementById('continueBtn').textContent = `Continuar como ${perfilAtual}`;

  function continuarComoAtual() {
    document.getElementById('profileScreen').style.display = 'none';
    document.getElementById('mainScreen').style.display = 'block';
    carregarContinueAssistindo();
  }

  function selecionarPerfil(nome) {
    perfilAtual = nome;
    localStorage.setItem('perfilAtual', nome);
    document.getElementById('continueBtn').textContent = `Continuar como ${nome}`;
    continuarComoAtual();
  }

  function abrirDetalhes(id) {
    animeAtual = id;
    const a = ANIME[id];
    document.getElementById('mainScreen').style.display = 'none';
    document.getElementById('detailsScreen').style.display = 'flex';
    document.getElementById('detailsCover').src = a.thumb;
    document.getElementById('detailsTitle').textContent = a.titulo;
    document.getElementById('detailsDesc').textContent = `Dublado • ${a.eps.length} episódios`;

    const lista = document.getElementById('episodesList');
    lista.innerHTML = '<div style="font-size:2.5rem;margin:30px 0;color:#fff">Episódios</div>';

    a.eps.forEach((url, i) => {
      const div = document.createElement('div');
      div.className = 'ep-item';
      div.innerHTML = `
        <div class="ep-thumb"><img src="${a.thumb}"></div>
        <div class="ep-info">
          <div class="ep-title">${i+1}. Episódio ${i+1}</div>
          <div class="ep-duration">~50min</div>
          <div class="ep-desc">Episódio ${i+1} dublado</div>
        </div>
        <div class="play-icon" onclick="event.stopPropagation(); playEp(${i});">▶</div>
      `;
      div.onclick = () => playEp(i);
      lista.appendChild(div);
    });
  }

  function playEp(ep) {
    const video = document.getElementById('player');
    video.src = ANIME[animeAtual].eps[ep];
    document.getElementById('detailsScreen').style.display = 'none';
    document.getElementById('player-area').style.display = 'block';
    video.play();
    saveProgress(animeAtual, ep, 0);
    video.ontimeupdate = () => {
      const p = Math.round((video.currentTime / video.duration || 0) * 100);
      if (p > 1 && p < 95) saveProgress(animeAtual, ep, p);
    };
    if (video.requestFullscreen) video.requestFullscreen();
  }

  function voltarTela() {
    const video = document.getElementById('player');
    video.pause();
    if (document.exitFullscreen) document.exitFullscreen();
    document.getElementById('player-area').style.display = 'none';
    document.getElementById('detailsScreen').style.display = 'flex';
  }

  function saveProgress(id, ep, percent) {
    const key = 'continue_' + perfilAtual;
    let lista = JSON.parse(localStorage.getItem(key) || '[]');
    lista = lista.filter(x => x.id !== id);
    lista.unshift({id, ep, percent, titulo: ANIME[id].titulo, thumb: ANIME[id].thumb});
    if (lista.length > 15) lista.pop();
    localStorage.setItem(key, JSON.stringify(lista));
    carregarContinueAssistindo();
  }

  function carregarContinueAssistindo() {
    if (!perfilAtual) return;
    const key = 'continue_' + perfilAtual;
    const lista = JSON.parse(localStorage.getItem(key) || '[]');
    const row = document.getElementById('continueRow');
    const sec = document.getElementById('continueSection');
    row.innerHTML = '';
    if (lista.length === 0) { sec.style.display = 'none'; return; }
    sec.style.display = 'block';
    lista.forEach(item => {
      const card = document.createElement('div');
      card.className = 'anime-card';
      card.innerHTML = `<img src="${item.thumb}"><div class="anime-card-title">${item.titulo}<br><small>Ep ${Number(item.ep)+1} – ${item.percent}%</small></div>
        <div class="progress-bg"><div class="progress-fill" style="width:${item.percent}%"></div></div>`;
      card.onclick = () => abrirDetalhes(item.id);
      row.appendChild(card);
    });
  }

  document.getElementById('player').addEventListener('ended', () => {
    const src = document.getElementById('player').src;
    const id = Object.keys(ANIME).find(k => src.includes(k));
    if (id) {
      const idx = ANIME[id].eps.indexOf(src);
      if (idx < ANIME[id].eps.length - 1) playEp(idx + 1);
    }
  });
</script>
</body>
</html>
