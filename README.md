<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nosso Save - Evelyn ❤️</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{
font-family:Segoe UI,Arial,sans-serif;
height:100vh;overflow:hidden;color:#fff;
background:linear-gradient(180deg,#00b4ff,#0077ff,#003e9c);
}
#content,
#letterScreen{

overflow-y:auto;

justify-content:flex-start;

padding-top:80px;
}
.screen{position:absolute;inset:0;display:flex;flex-direction:column;justify-content:center;align-items:center;padding:20px}
.hidden{display:none}
.plumbob-wrap{position:relative}
.plumbob{
width:90px;height:90px;
background:linear-gradient(180deg,#a7ffe4,#3cff9b,#00b56a);
clip-path:polygon(50% 0,100% 50%,50% 100%,0 50%);
animation:float 2s ease-in-out infinite,spin 8s linear infinite;
box-shadow:0 0 20px #00ff88,0 0 60px #00ff88;
}
@keyframes spin{from{transform:rotate(0)}to{transform:rotate(360deg)}}
@keyframes float{50%{transform:translateY(-12px)}}
.bar{width:85%;max-width:340px;height:20px;background:#16315c;border-radius:30px;overflow:hidden;margin-top:15px}
.fill{height:100%;width:0;background:linear-gradient(90deg,#4cff9a,#b8ffd8)}
.card{
width:100%;max-width:390px;
background:rgba(255,255,255,.12);
backdrop-filter:blur(15px);
border-radius:25px;
padding:25px;
box-shadow:0 10px 30px rgba(0,0,0,.3);
text-align:center;
}
.btn{
background:black;color:#fff;border:none;
padding:14px 20px;border-radius:14px;
font-size:16px;font-weight:bold;margin-top:15px
}
.house{
display:grid;grid-template-columns:1fr 1fr;
gap:14px;width:100%;max-width:400px;margin-top:20px
}
.room{
padding:22px;border-radius:18px;
background:rgba(255,255,255,.15);
backdrop-filter:blur(10px);
text-align:center;font-weight:bold
}
.back{
position:fixed;top:15px;left:15px;border:none;
padding:10px 15px;border-radius:12px;z-index:1000
}
.photo{
width:100%;
height:220px;
object-fit:cover;
border-radius:12px;
margin:10px 0;
box-shadow:0 5px 20px rgba(0,0,0,.4);
}
.polaroid{
background:white;
padding:10px;
border-radius:10px;
margin:15px 0;
box-shadow:0 5px 20px rgba(0,0,0,.4);
}

.polaroid img{
width:100%;
height:220px;
object-fit:cover;
border-radius:5px;
}

.polaroid p{
color:black;
margin-top:8px;
font-weight:bold;
text-align:center;
}
.heart{
position:fixed;
animation:rise 8s linear forwards;
pointer-events:none
}
@keyframes rise{
from{transform:translateY(100vh);opacity:1}
to{transform:translateY(-100px);opacity:0}
}
.small{opacity:.9}
</style>
</head>
<body>

<div id="loading" class="screen">
<div class="plumbob-wrap"><div class="plumbob"></div></div>
<h2 style="margin-top:20px">The Sims 4</h2>
<p id="status"
style="
margin-top:15px;
font-size:18px;
font-weight:bold;
text-align:center;
">
Carregando save...
</p>

<div id="tipBox"
style="
margin-top:20px;
max-width:320px;
background:rgba(255,255,255,.12);
padding:15px;
border-radius:15px;
font-size:14px;
line-height:1.5;
text-align:center;
backdrop-filter:blur(10px);
">
💚 Dica: Evelyn é a Sim favorita do criador deste save.
</div>

<div class="bar">
<div id="fill" class="fill"></div>
</div>
</div>

<div id="menu" class="screen hidden">
<div class="card">
<h1>Evelyn ❤️</h1>
<p>Bem-vinda ao nosso mundo.</p>
<h2 style="margin:10px 0">3 anos e 7 meses</h2>
<p class="small">Uma surpresa feita especialmente para você.</p>
<button class="btn" onclick="openHouse()">Entrar no Nosso Mundo</button>
</div>
</div>

<div id="house" class="screen hidden">
<h1>🏡 Nossa Casa</h1>
<p>Escolha um cômodo</p>
<div class="house">
<div class="room" onclick="openRoom('historia')">📖<br>História</div>
<div class="room" onclick="openRoom('fotos')">📸<br>Fotos</div>
<div class="room" onclick="openRoom('memorias')">✨<br>Memórias</div>
<div class="room" onclick="showLetter()">❤️<br>Carta Final</div>
</div>
</div>

<div id="content" class="screen hidden">
<button class="back" onclick="goHome()">←</button>
<div class="card" id="card"></div>
</div>

<div id="letterScreen" class="screen hidden">
<button class="back" onclick="goHome()">←</button>
<div class="card">
<h2>Para Evelyn ❤️</h2>
<br>
<div id="letterText">
Espero que você tenha gostado da surpresa. Sei que foi simples mas pode ter certeza que foi de coração.
Tudo que coloquei aqui foi pensando em nós 2, demorou um tempo para fazer, então espero que curta. Eu te amo muito,
muito mesmo do fundo do meu coração. Espero poder ter muitos mais dias dos namorados com você e porder passar mais anos e
anos contigo, ao teu lado, por enquanto como namorado e futuramente como marido. Você é a garota mais linda do mundo todo. Tudo em você
me deixa bobo. Teu sorriso, teu cabelo, teu corpo todo, seu cheiro maravilhoso e seu jeito de se vertir me deixam loucos.
Não tem o que eu fale aqui nesta carta que possa descrever tudo que sinto por ti. Te amo te amo TE AMO te amo te amo...
Te amoTe amoTe amoTe amoTe amo
Te amo Te amoTe amoTe amoTe amo
Te amo Te amoTe amoTe amoTe amo
Te amo Te amoTe amoTe amoTe amo
Te amo Te amoTe amoTe amoTe amo
Te amo Te amoTe Te amoTe amoTe amo
Te amo Te amo
Te amo Te amo
Te amo 
Te amoTe amoTe amo
Te amo Te amo 
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo 
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo 
Te amo
Te amo 
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amoTe amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amoTe amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo
Te amo 
Te amo
Te amo

</div>
</div>
</div>

<script>
const msgs=[

'Preparando momentos especiais...',
'Organizando nossas fotos...',
'Invocando gatos fofos...',
'Construindo nossa casa...',
'Calculando 3 anos e 7 meses...',
'Desbloqueando conquistas...',
'Preparando surpresa para Evelyn...',
'Quase pronto... ❤️'

];

const tips=[

'💚 Dica: Evelyn é a Sim favorita do criador deste save.',

'🏡 Dica: Casas ficam melhores quando construídas por duas pessoas.',

'❤️ Dica: Este relacionamento já atingiu o nível máximo.',

'✨ Dica: Algumas memórias possuem valor sentimental infinito.',

'🎮 Dica: Este save foi desenvolvido exclusivamente para Evelyn.',

'🌹 Dica: O amor fornece +100 de felicidade diariamente.',

'💍 Dica: O criador deste save pretende continuar jogando por muitos anos.'

];

let p = 0;
let msg = 0;
let tip = 0;

status.innerText = msgs[0];

const timer = setInterval(()=>{

    p += 2;

    fill.style.width = p + '%';

    if(p % 20 === 0){

        if(msg < msgs.length - 1){

            msg++;

            status.innerText =
                msgs[msg];
        }

        tip++;

        document.getElementById("tipBox")
            .innerText =
            tips[tip % tips.length];
    }

    if(p >= 100){

        clearInterval(timer);

        loading.classList.add("hidden");

        menu.classList.remove("hidden");
    }

},250);

function openHouse(){
menu.classList.add('hidden');
house.classList.remove('hidden');
}

function goHome(){
content.classList.add('hidden');
letterScreen.classList.add('hidden');
house.classList.remove('hidden');
}

function openRoom(tipo){
house.classList.add('hidden');
content.classList.remove('hidden');

if(tipo==='historia'){
card.innerHTML=`
<h2>Nossa História</h2><br>
<p>"Você não presta Eduado!!" lembra disso?    Nos conhecemos na escola, e desde então, nossa amizade foi crescendo
e se tornado esse lindo romance que temos hoje. Contigo, por todos esse anos, aprendi coisas que jamais teria aprendido se tudo não tivesse sido da forma como foi.
Desde a escola, nossas casas, faculdade, sitio, praia e todos os nosso cenarios, todos estes fizeram parte da nossa história.</p>
`;
}

if(tipo==='fotos'){
card.innerHTML=`

<h2>Nossas Fotos</h2>

<div class="polaroid">
    <img src="foto1.jpeg">
    <p>Nosso momento ❤️</p>
</div>

<div class="polaroid">
    <img src="foto2.jpeg">
    <p>Mais uma lembrança ✨</p>
</div>

<div class="polaroid">
    <img src="foto3.jpeg">
    <p>Eu e você 🥰</p>
</div>

`;
}

if(tipo==='memorias'){
card.innerHTML=`
<h2>Memórias Favoritas</h2><br>
<p>⭐ Primeiro encontro: Oficial? no ioshi sushi S2</p>
<p>⭐ Momento inesquecível: Toda vez que viajamos juntos no nosso carro, se torna um momento inesquecível.</p>
<p>⭐ Nossa melhor aventura: F1 em araranguá kkkk</p>
<p>⭐ Melhor passa-tempo: Jogar juntos um ao lado do outro ou assistir series.</p>
`;
}
}

function showLetter(){
house.classList.add('hidden');
letterScreen.classList.remove('hidden');
}

setInterval(()=>{
const h=document.createElement('div');
h.className='heart';
h.innerHTML='❤️';
h.style.left=Math.random()*100+'vw';
document.body.appendChild(h);
setTimeout(()=>h.remove(),8000);
},1500);
</script>
</body>
</html>
