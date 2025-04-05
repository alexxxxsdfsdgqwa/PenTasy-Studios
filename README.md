<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>PC Simulador Completo</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      background-color: #1E4DD8;
      font-family: sans-serif;
      user-select: none;
      overflow: hidden;
    }
    #desktop {
      width: 100vw;
      height: 100vh;
      padding: 10px;
      position: relative;
      color: white;
    }
    .icon {
      width: 90px;
      padding: 8px;
      background: rgba(255, 255, 255, 0.2);
      border-radius: 8px;
      text-align: center;
      cursor: pointer;
      margin-bottom: 10px;
      float: left;
      margin-right: 10px;
    }
    .icon:hover {
      background: rgba(255, 255, 255, 0.4);
    }
    .window {
      position: absolute;
      top: 100px;
      left: 100px;
      width: 450px;
      background: white;
      border: 2px solid #000;
      box-shadow: 4px 4px #333;
      display: none;
      z-index: 10;
      max-height: 80vh;
      overflow: auto;
    }
    .titlebar {
      background: #444;
      color: white;
      padding: 8px;
      display: flex;
      justify-content: space-between;
      font-weight: bold;
      cursor: move;
    }
    .content {
      padding: 10px;
      color: black;
    }
    .close-btn {
      background: red;
      color: white;
      border: none;
      padding: 4px 8px;
      cursor: pointer;
    }
    .taskbar {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 40px;
      background: #333;
      color: white;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 10px;
    }
    .taskbar .clock {
      font-size: 14px;
    }
    #gameCanvas, #paintCanvas {
      border: 1px solid black;
      background: #f0f0f0;
    }
    textarea, input, canvas {
      width: 100%;
      box-sizing: border-box;
    }
    .spotify-player {
      background-color: #121212;
      color: white;
      padding: 10px;
      border-radius: 10px;
      font-family: Arial;
    }
    .spotify-player .track {
      margin-bottom: 15px;
      padding: 10px;
      border: 1px solid #333;
      border-radius: 8px;
      background-color: #1e1e1e;
    }
    .spotify-player .track:hover {
      background-color: #2a2a2a;
    }
    .spotify-player strong {
      display: block;
      margin-bottom: 5px;
    }
    .spotify-player audio {
      width: 100%;
      margin-top: 5px;
    }
  </style>
</head>
<body>
  <div id="desktop">
    <div class="icon" onclick="abrirJanela('bloco')">📝<br>Notas</div>
    <div class="icon" onclick="abrirJanela('internet')">🌐<br>Navegador</div>
    <div class="icon" onclick="abrirJanela('jogo')">🎮<br>Jogo</div>
    <div class="icon" onclick="abrirJanela('paint')">🎨<br>Paint</div>
    <div class="icon" onclick="abrirJanela('musica')">🎵<br>Spotify</div>
    <div class="icon" onclick="abrirJanela('arquivos')">📁<br>Arquivos</div>

    <div class="window" id="bloco">
      <div class="titlebar">Bloco de Notas <button class="close-btn" onclick="fecharJanela('bloco')">X</button></div>
      <div class="content">
        <textarea rows="10"></textarea>
      </div>
    </div>

    <div class="window" id="internet">
      <div class="titlebar">Navegador <button class="close-btn" onclick="fecharJanela('internet')">X</button></div>
      <div class="content">
        <input id="url" placeholder="Digite algo como google.com">
        <button onclick="navegar()">Ir</button>
        <div id="navegador" style="margin-top: 10px;"></div>
      </div>
    </div>

    <div class="window" id="jogo">
      <div class="titlebar">Joguinho <button class="close-btn" onclick="fecharJanela('jogo')">X</button></div>
      <div class="content">
        <canvas id="gameCanvas" width="300" height="200"></canvas>
        <p>Pontos: <span id="score">0</span></p>
      </div>
    </div>

    <div class="window" id="paint">
      <div class="titlebar">Paint <button class="close-btn" onclick="fecharJanela('paint')">X</button></div>
      <div class="content">
        <canvas id="paintCanvas" width="400" height="250"></canvas>
      </div>
    </div>

    <div class="window" id="musica">
      <div class="titlebar">Spotify Simulado <button class="close-btn" onclick="fecharJanela('musica')">X</button></div>
      <div class="content">
        <div class="spotify-player">
          <div class="track">
            <strong>NUNCA MUDA (Slowed)</strong>
            <em>Spizz*</em>
            <audio controls>
              <source src="https://files.catbox.moe/icrqy5.mp3" type="audio/mpeg">
            </audio>
          </div>
          <div class="track">
            <strong>MONTAGEM LADRÃO (Slowed)</strong>
            <em>Desconhecido</em>
            <audio controls>
              <source src="https://files.catbox.moe/emfblf.mp3" type="audio/mpeg">
            </audio>
          </div>
          <div class="track">
            <strong>Funk de Beleza (Slowed)</strong>
            <em>Desconhecido</em>
            <audio controls>
              <source src="https://files.catbox.moe/smy2fb.mp3" type="audio/mpeg">
            </audio>
          </div>
        </div>
      </div>
    </div>

    <div class="window" id="arquivos">
      <div class="titlebar">Explorador de Arquivos <button class="close-btn" onclick="fecharJanela('arquivos')">X</button></div>
      <div class="content">
        <ul>
          <li>📄 documento.txt</li>
          <li>📷 imagem.png</li>
          <li>🎵 NUNCA MUDA (Slowed).mp3</li>
          <li>🎵 MONTAGEM LADRÃO (Slowed).mp3</li>
          <li>🎵 Funk de Beleza (Slowed).mp3</li>
        </ul>
      </div>
    </div>

    <div class="taskbar">
      <div>Menu Iniciar</div>
      <div class="clock" id="relogio"></div>
    </div>
  </div>

  <script>
    function abrirJanela(id) {
      document.getElementById(id).style.display = 'block';
    }
    function fecharJanela(id) {
      document.getElementById(id).style.display = 'none';
    }

    function atualizarRelogio() {
      const agora = new Date();
      const horas = agora.getHours().toString().padStart(2, '0');
      const minutos = agora.getMinutes().toString().padStart(2, '0');
      const segundos = agora.getSeconds().toString().padStart(2, '0');
      document.getElementById("relogio").textContent = `${horas}:${minutos}:${segundos}`;
    }
    setInterval(atualizarRelogio, 1000);
    atualizarRelogio();

    function navegar() {
      const url = document.getElementById("url").value.toLowerCase();
      const navegador = document.getElementById("navegador");
      if (url.includes("google")) {
        navegador.innerHTML = "<h3>Google</h3><input placeholder='Pesquisar no Google...'>";
      } else if (url.includes("youtube")) {
        navegador.innerHTML = "<h3>YouTube</h3><p>Vídeos fictícios carregando...</p>";
      } else {
        navegador.innerHTML = `<p>Site '${url}' não encontrado.</p>`;
      }
    }

    // Jogo: clique no círculo
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");
    let x = 50, y = 50, score = 0;

    function desenharCirculo() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.beginPath();
      ctx.arc(x, y, 20, 0, Math.PI * 2);
      ctx.fillStyle = "red";
      ctx.fill();
      ctx.closePath();
    }
    canvas.addEventListener("click", function (e) {
      const rect = canvas.getBoundingClientRect();
      const clickX = e.clientX - rect.left;
      const clickY = e.clientY - rect.top;
      const dist = Math.sqrt((clickX - x) ** 2 + (clickY - y) ** 2);
      if (dist < 20) {
        score++;
        document.getElementById("score").textContent = score;
        x = Math.random() * 260 + 20;
        y = Math.random() * 160 + 20;
        desenharCirculo();
      }
    });
    desenharCirculo();

    // Paint
    const paintCanvas = document.getElementById("paintCanvas");
    const pctx = paintCanvas.getContext("2d");
    let pintando = false;
    paintCanvas.addEventListener("mousedown", () => pintando = true);
    paintCanvas.addEventListener("mouseup", () => pintando = false);
    paintCanvas.addEventListener("mousemove", e => {
      if (pintando) {
        const rect = paintCanvas.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        pctx.fillStyle = "black";
        pctx.fillRect(x, y, 2, 2);
      }
    });
  </script>
</body>
</html>
