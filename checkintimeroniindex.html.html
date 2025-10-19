<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Check-in - Time Roni</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
<style>
body {
  font-family: "Poppins", Arial, sans-serif;
  background-color: #000;
  color: #fff;
  padding: 20px;
  max-width: 450px;
  margin: auto;
  text-align: center;
}
img.logo {
  width: 120px; height: auto;
  display: block;
  margin: 0 auto 20px auto;
  border-radius: 50%;
  box-shadow: 0 0 20px rgba(255, 140, 0, 0.4);
}
h1 { font-size: 1.6em; margin-bottom: 20px; font-weight: 600; color: #fff; }
form {
  background: #111; padding: 20px; border-radius: 12px;
  box-shadow: 0 0 20px rgba(255, 140, 0, 0.15); margin-bottom: 20px;
}
input { width: 100%; padding: 14px; margin-top: 10px; border: none; border-radius: 8px; font-size: 16px; background-color: #1b1b1b; color: #fff; outline: none; }
input::placeholder { color: #aaa; }
button { width: 100%; padding: 14px; margin-top: 20px; background-color: #ff6600; color: #fff; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; letter-spacing: 0.5px; cursor: pointer; transition: all 0.3s ease; }
button:hover { background-color: #e85c00; transform: scale(1.02); }
.mensagem { margin-top: 20px; font-size: 15px; font-weight: 500; color: #ffa94d; min-height: 40px; }
#map { height: 250px; margin-top: 20px; border-radius: 12px; border: 2px solid #ff6600; }
#adminLogin, #adminArea { background-color: #111; padding: 20px; border-radius: 12px; margin-top: 30px; box-shadow: 0 0 15px rgba(255, 140, 0, 0.2); }
#adminLogin h2, #adminArea h2 { font-size: 18px; color: #ffa94d; }
ul { list-style: none; padding: 0; margin-top: 15px; text-align: left; max-height: 300px; overflow-y: auto; }
li { padding: 8px; border-bottom: 1px solid rgba(255, 255, 255, 0.1); font-size: 14px; color: #eee; }
#btnLimpar { background-color: #ff3b3b; margin-top: 15px; }
#btnLimpar:hover { background-color: #d32f2f; }
@media (max-width: 480px) { body { padding: 15px; } h1 { font-size: 1.4em; } button { font-size: 16px; } }
</style>
</head>
<body>

<img src="https://drive.google.com/uc?export=view&id=1cbqdD0qjJB2B1UNr4vOyVrbW2V0Am-ly" alt="Time Roni" class="logo">
<h1>Check-in - Time Roni</h1>

<form id="formCheckin">
  <input type="text" id="nome" placeholder="Digite seu nome" required>
  <button type="submit" id="btnCheckin">Fazer Check-in</button>
</form>

<div class="mensagem" id="mensagem"></div>
<div id="map"></div>

<div id="adminLogin">
  <h2>Área do administrador</h2>
  <input type="password" id="senhaAdmin" placeholder="Digite a senha">
  <button id="btnEntrarAdmin">Entrar</button>
</div>

<div id="adminArea" style="display:none;">
  <h2>Histórico de Check-ins</h2>
  <ul id="historico"></ul>
  <button id="btnLimpar">🗑️ Limpar histórico</button>
</div>

<!-- Som de notificação -->
<audio id="audioNotificacao" src="https://www.soundjay.com/button/beep-07.mp3" preload="auto"></audio>

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
<script>
const form = document.getElementById('formCheckin');
const mensagem = document.getElementById('mensagem');
const historicoUl = document.getElementById('historico');
const adminArea = document.getElementById('adminArea');
const btnEntrarAdmin = document.getElementById('btnEntrarAdmin');
const senhaAdmin = document.getElementById('senhaAdmin');
const btnLimpar = document.getElementById('btnLimpar');
const btnCheckin = document.getElementById('btnCheckin');
const audioNotificacao = document.getElementById('audioNotificacao');

const SENHA_CORRETA = "rony2025";

const stands = [
  { nome: "Alto", lat: -23.6286481, lon: -46.6720000, raio: 100 },
  { nome: "Astro", lat: -23.5155317, lon: -46.6973858, raio: 100 },
  { nome: "Barra Funda", lat: -23.5267792, lon: -46.6516253, raio: 100 },
  { nome: "Next Guarulhos", lat: -23.4630000, lon: -46.5200000, raio: 100 },
  { nome: "Jaguaré", lat: -23.5310000, lon: -46.7080000, raio: 100 },
  { nome: "Mooca", lat: -23.5465000, lon: -46.6105000, raio: 100 },
  { nome: "Pirituba", lat: -23.4980000, lon: -46.7860000, raio: 100 },
  { nome: "Sacomã", lat: -23.5030000, lon: -46.7110000, raio: 100 },
  { nome: "Belenzinho", lat: -23.5480000, lon: -46.6190000, raio: 100 }
];

let checkins = JSON.parse(localStorage.getItem('checkins')) || [];
function atualizarLista() {
  historicoUl.innerHTML = '';
  checkins.forEach(item => {
    const li = document.createElement('li');
    li.textContent = `${item.nome} — ${item.hora} (${item.local})`;
    historicoUl.appendChild(li);
  });
}

function calcularDistancia(lat1, lon1, lat2, lon2) {
  const R = 6371e3;
  const rad = Math.PI / 180;
  const dLat = (lat2 - lat1) * rad;
  const dLon = (lon2 - lon1) * rad;
  const a = Math.sin(dLat/2)**2 + Math.cos(lat1*rad)*Math.cos(lat2*rad)*Math.sin(dLon/2)**2;
  const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
  return R * c;
}

// Inicializa mapa
const map = L.map('map').setView([-23.55, -46.65], 11);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', { attribution: '' }).addTo(map);

// Stands
const standMarkers = stands.map(s => {
  const circle = L.circle([s.lat, s.lon], { color:'#ff6600', fillColor:'#ff6600', fillOpacity:0.3, radius:s.raio }).addTo(map).bindPopup(s.nome);
  return { ...s, circle };
});

// Usuário
let userMarker = null;
let pulsando = false;
let notificou = false;

function atualizarPosicao() {
  if (!navigator.geolocation) return;
  navigator.geolocation.getCurrentPosition(pos => {
    const { latitude, longitude } = pos.coords;
    if (!userMarker) {
      userMarker = L.circleMarker([latitude, longitude], { radius: 10, color:'#00ff00', fillColor:'#00ff00', fillOpacity:1 }).addTo(map);
    } else {
      userMarker.setLatLng([latitude, longitude]);
    }
    map.setView([latitude, longitude], 14);

    // Checa se está dentro de stand
    let dentro = false;
    standMarkers.forEach(s => {
      const dist = calcularDistancia(latitude, longitude, s.lat, s.lon);
      if (dist <= s.raio) { dentro = true; s.circle.setStyle({ color:'lime', fillColor:'lime' }); }
      else s.circle.setStyle({ color:'#ff6600', fillColor:'#ff6600' });
    });

    // Feedback pulsante e som
    if (dentro) {
      mensagem.style.color = "#00ff99";
      mensagem.innerText = "✅ Você está pronto para check-in!";
      if (!notificou) { audioNotificacao.play(); notificou = true; }
      if (!pulsando) {
        pulsando = true;
        let crescente = true;
        const pulsar = setInterval(() => {
          if (!pulsando) { clearInterval(pulsar); return; }
          userMarker.setStyle({ fillOpacity: crescente ? 0.3 : 1 });
          crescente = !crescente;
        }, 500);
      }
    } else {
      mensagem.style.color = "#ff5555";
      mensagem.innerText = "❌ Você não está dentro de um stand autorizado.";
      pulsando = false;
      notificou = false;
      if (userMarker) userMarker.setStyle({ fillOpacity:1 });
    }
  });
}
setInterval(atualizarPosicao, 3000);

// Check-in
form.addEventListener('submit', function(e) {
  e.preventDefault();
  const nome = document.getElementById('nome').value.trim();
  if (!nome) return;
  if (!navigator.geolocation) { mensagem.innerText = "❌ Seu dispositivo não suporta geolocalização."; return; }

  mensagem.style.color = "#ffa94d";
  mensagem.innerText = "📍 Verificando sua localização...";
  btnCheckin.disabled = true;

  navigator.geolocation.getCurrentPosition(pos => {
    btnCheckin.disabled = false;
    const { latitude, longitude } = pos.coords;
    let dentro = false;
    let standEncontrado = '';

    for (const s of stands) {
      const dist = calcularDistancia(latitude, longitude, s.lat, s.lon);
      if (dist <= s.raio) { dentro = true; standEncontrado = s.nome; break; }
    }

    if (dentro) {
      const agora = new Date();
      const horaFormatada = agora.toLocaleString('pt-BR', { dateStyle:'short', timeStyle:'short' });
      const novoCheckin = { nome, hora:horaFormatada, local: standEncontrado };
      checkins.push(novoCheckin);
      localStorage.setItem('checkins', JSON.stringify(checkins));
      atualizarLista();
      mensagem.style.color = "#00ff99";
      mensagem.innerText = `✅ Check-in realizado por ${nome} no stand ${standEncontrado} às ${horaFormatada}`;
      document.getElementById('nome').value = '';
    } else {
      mensagem.style.color = "#ff5555";
      mensagem.innerText = "❌ Você não está dentro de um stand autorizado. Aproxime-se e tente novamente.";
    }
  }, () => {
    btnCheckin.disabled = false;
    mensagem.style.color = "#ff5555";
    mensagem.innerText = "⚠️ Não foi possível obter sua localização. Verifique se o GPS está ativo.";
  }, { enableHighAccuracy:true, timeout:10000 });
});

// Admin
btnEntrarAdmin.addEventListener('click', () => {
  if (senhaAdmin.value === SENHA_CORRETA) { adminArea.style.display = 'block'; atualizarLista(); senhaAdmin.value=''; }
  else alert('❌ Senha incorreta!');
});
btnLimpar.addEventListener('click', () => {
  if (confirm('Tem certeza que deseja limpar o histórico de check-ins?')) {
    checkins=[]; localStorage.removeItem('checkins'); atualizarLista();
  }
});
setInterval(()=>{ if(adminArea.style.display==='block') atualizarLista(); },5000);
</script>
</body>
</html>
