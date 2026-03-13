<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Evolução de Criatura</title>

<style>

body{
margin:0;
font-family:Arial;
background:#0f0f0f;
color:white;
text-align:center;
}

h2{
margin-top:10px;
}

#ui{
margin:10px;
font-size:20px;
}

#game{
width:700px;
height:450px;
background:#1c1c1c;
margin:auto;
position:relative;
border-radius:12px;
overflow:hidden;
box-shadow:0 10px 30px rgba(0,0,0,0.7);
}

#player{
position:absolute;
font-size:28px;
transition:0.05s;
}

.dna{
position:absolute;
font-size:20px;
}

</style>
</head>

<body>

<h2>🧬 Evolução da Criatura</h2>

<div id="ui">
DNA: <span id="dna">0</span>
</div>

<div id="game">
<div id="player">🐛</div>
</div>

<script>

const player = document.getElementById("player")
const game = document.getElementById("game")

let x = 100
let y = 100
let speed = 3

let dna = 0
let nivel = 0

const criaturas = ["🐛","🦎","🐺","🦁","🐉"]

let keys = {}

document.addEventListener("keydown",e=>{
keys[e.key]=true
})

document.addEventListener("keyup",e=>{
keys[e.key]=false
})

function mover(){

if(keys["ArrowRight"]||keys["d"]){
x+=speed
player.innerText="🐞"
}

if(keys["ArrowLeft"]||keys["a"]){
x-=speed
player.innerText="🐜"
}

if(keys["ArrowUp"]||keys["w"]){
y-=speed
player.innerText="🐛"
}

if(keys["ArrowDown"]||keys["s"]){
y+=speed
player.innerText="🐌"
}

if(x<0)x=0
if(y<0)y=0
if(x>670)x=670
if(y>420)y=420

player.style.left=x+"px"
player.style.top=y+"px"

checarDNA()

requestAnimationFrame(mover)

}

mover()

function spawnDNA(){

let d=document.createElement("div")

d.className="dna"
d.innerText="🧬"

let dx=Math.random()*680
let dy=Math.random()*430

d.style.left=dx+"px"
d.style.top=dy+"px"

game.appendChild(d)

}

setInterval(spawnDNA,1200)

function checarDNA(){

let dnas=document.querySelectorAll(".dna")

dnas.forEach(d=>{

let dx=d.offsetLeft
let dy=d.offsetTop

if(Math.abs(dx-x)<25 && Math.abs(dy-y)<25){

d.remove()

dna++

document.getElementById("dna").innerText=dna

evoluir()

}

})

}

function evoluir(){

if(nivel==0 && dna>=10){
nivel=1
player.innerText=criaturas[nivel]
speed=3.5
}

if(nivel==1 && dna>=25){
nivel=2
player.innerText=criaturas[nivel]
speed=4
}

if(nivel==2 && dna>=50){
nivel=3
player.innerText=criaturas[nivel]
speed=4.5
}

if(nivel==3 && dna>=80){
nivel=4
player.innerText=criaturas[nivel]
speed=5
}

}

</script>

</body>
</html>
