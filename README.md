<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Siempre tú</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>

html, body {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
    background: radial-gradient(circle at bottom, #020111 0%, #000000 80%);
    font-family: Arial, Helvetica, sans-serif;
}

canvas{
    position: absolute;
    width: 100%;
    height: 100%;
}

#principal{
    position: absolute;
    top: 28%;
    width: 100%;
    text-align: center;
    font-size: 40px;
    color: #ff74d4;
    font-weight: bold;
    text-shadow: 0 0 30px #ff74d4;
    animation: pulso 2s infinite alternate;
}

.texto{
    position: absolute;
    color: #ffc6ff;
    font-size: 18px;
    animation: subir linear forwards;
    text-shadow: 0 0 12px pink;
    white-space: nowrap;
}

@keyframes subir{
    from { transform: translateY(100vh); opacity: 0; }
    10% { opacity: 1; }
    to { transform: translateY(-100px); opacity: 0; }
}

@keyframes pulso{
    from{ transform: scale(1); }
    to{ transform: scale(1.1); }
}

</style>
</head>

<body>

<canvas id="fondo"></canvas>
<div id="principal">Siempre tú 💍</div>

<script>

const canvas = document.getElementById("fondo");
const ctx = canvas.getContext("2d");

function ajustar(){
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
ajustar();
window.onresize = ajustar;

// ESTRELLAS
let estrellas = [];
for(let i=0;i<220;i++){
    estrellas.push({
        x: Math.random()*canvas.width,
        y: Math.random()*canvas.height,
        r: Math.random()*1.4 + 0.3,
        vel: Math.random()*0.3 + 0.1
    });
}

function animarEstrellas(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle = "white";
    estrellas.forEach(e=>{
        ctx.beginPath();
        ctx.arc(e.x, e.y, e.r, 0, Math.PI*2);
        ctx.fill();
        e.y += e.vel;
        if(e.y > canvas.height) e.y = 0;
    });
    requestAnimationFrame(animarEstrellas);
}
animarEstrellas();

// APODOS
const apodos = [
    "Niña ❤️",
    "Linda ✨",
    "Estoy orgulloso de ti 🥰",
    " Eres una reina👑",
    "eres fuerte  💕",
    "bonita 💖",
    "Chula 💗",
    " 💞"
];

function crearTexto(){
    let t = document.createElement("div");
    t.className = "texto";
    t.innerText = apodos[Math.floor(Math.random()*apodos.length)];
    t.style.left = Math.random()*window.innerWidth + "px";
    t.style.fontSize = (16 + Math.random()*14) + "px";
    t.style.animationDuration = (8 + Math.random()*4) + "s";
    document.body.appendChild(t);
    setTimeout(()=>t.remove(),14000);
}

setInterval(crearTexto, 850);

</script>

</body>
</html>
