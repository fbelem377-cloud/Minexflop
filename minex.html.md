minex.html  
<!DOCTYPE html>  
<html>  
<head>  
<meta charset="UTF-8">  
<title>MineX PRO</title>  
  
<style>  
body{  
margin:0;  
font-family:Arial;  
background:#0b0f1a;  
color:white;  
text-align:center;  
}  
  
.container{  
padding:20px;  
max-width:500px;  
margin:auto;  
}  
  
.card{  
background:#141b2d;  
padding:15px;  
margin:10px;  
border-radius:15px;  
box-shadow:0 0 10px #00ffcc33;  
}  
  
button{  
padding:12px;  
margin:5px;  
border:none;  
border-radius:10px;  
background:#00ffcc;  
color:black;  
font-weight:bold;  
cursor:pointer;  
width:90%;  
}  
  
button:hover{  
background:#00c9a7;  
}  
  
button:disabled {  
background: #004c3e;  
color: #888;  
cursor: not-allowed;  
}  
</style>  
  
</head>  
  
<body>  
  
<div class="container">  
  
<h1>⛏️ MineX PRO</h1>  
  
<div class="card">  
💎 MINEX: <span id="minex">0</span><br>  
👛 Wallet: <span id="wallet">0</span><br>  
⚡ Energía: <span id="energy">100</span><br>  
⛏️ Pico: <span id="pick">1</span>  
</div>  
  
<div class="card">  
<p id="log">Bienvenido a MineX</p>  
</div>  
  
<div class="card">  
<button id="mineBtn" onclick="mine()">⛏️ MINAR</button>  
<button onclick="upgrade()">🔧 MEJORAR PICO (500 MINEX)</button>  
<button onclick="convert()">💰 CONVERTIR 1000 → WALLET</button>  
<button onclick="redeem()">🎁 CANJEAR (10 WALLET)</button>  
</div>  
  
</div>  
  
<script>  
// Convert to integers so addition works correctly  
let minex = parseInt(localStorage.getItem("minex"), 10) || 0;  
let wallet = parseInt(localStorage.getItem("wallet"), 10) || 0;  
let energy = parseInt(localStorage.getItem("energy"), 10) || 100;  
let pick = parseInt(localStorage.getItem("pick"), 10) || 1;  
  
function update(){  
document.getElementById("minex").innerText = minex;  
document.getElementById("wallet").innerText = wallet;  
document.getElementById("energy").innerText = energy;  
document.getElementById("pick").innerText = pick;  
  
localStorage.setItem("minex", minex);  
localStorage.setItem("wallet", wallet);  
localStorage.setItem("energy", energy);  
localStorage.setItem("pick", pick);  
}  
  
function log(text){  
document.getElementById("log").innerText = text;  
}  
  
function mine(){  
if(energy <= 0){  
log("❌ Sin energía");  
return;  
}  
  
energy--;  
  
// Random chance (0 to 100)  
let r = Math.random() * 100;  
  
if(r > 95){  
minex += 100 * pick;  
log("💎 ¡Diamante!");  
}  
else if(r > 75){  
minex += 30 * pick;  
log("🥇 Oro encontrado");  
}  
else{  
minex += 10 * pick;  
log("🪨 Piedra");  
}  
  
update();  
}  
  
function upgrade(){  
if(minex >= 500){  
minex -= 500;  
pick++;  
log("🔧 Pico mejorado");  
update();  
}  
else{  
log("❌ No tienes suficiente MINEX");  
}  
}  
  
function convert(){  
if(minex >= 1000){  
minex -= 1000;  
wallet++;  
log("💰 Convertido a wallet");  
update();  
}  
else{  
log("❌ No tienes suficiente MINEX");  
}  
}  
  
function redeem(){  
if(wallet >= 10){  
wallet -= 10;  
log("🎁 Canje solicitado (simulado)");  
update();  
}  
else{  
log("❌ Necesitas 10 wallet");  
}  
}  
  
// Energy regeneration system  
setInterval(() => {  
if (energy < 100) {  
energy++;  
update();  
}  
}, 3000); // Recovers 1 energy every 3 seconds  
  
update();  
  
</script>  
  
</body>  
</html>  
