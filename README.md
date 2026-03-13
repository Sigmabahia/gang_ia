<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Voz para Texto</title>

<style>

body{
font-family: Arial, sans-serif;
background: linear-gradient(135deg,#1e1e2f,#111);
color:white;
display:flex;
flex-direction:column;
align-items:center;
justify-content:center;
height:100vh;
margin:0;
}

.container{
background:#1f1f1f;
padding:30px;
border-radius:15px;
width:500px;
max-width:90%;
box-shadow:0 10px 30px rgba(0,0,0,0.5);
text-align:center;
}

h1{
margin-bottom:20px;
}

textarea{
width:100%;
height:150px;
border:none;
border-radius:10px;
padding:15px;
font-size:16px;
resize:none;
outline:none;
}

button{
margin-top:15px;
padding:12px 20px;
font-size:16px;
border:none;
border-radius:8px;
cursor:pointer;
background:#6c5ce7;
color:white;
}

button:hover{
background:#5848c2;
}

.status{
margin-top:10px;
font-size:14px;
color:#aaa;
}

</style>
</head>

<body>

<div class="container">

<h1>🎤 Voz para Texto</h1>

<textarea id="texto" placeholder="O que você falar vai aparecer aqui..."></textarea>

<br>

<button onclick="iniciar()">Começar a falar</button>
<button onclick="parar()">Parar</button>

<div class="status" id="status">Microfone parado</div>

</div>

<script>

let recognition

function iniciar(){

const SpeechRecognition =
window.SpeechRecognition ||
window.webkitSpeechRecognition

recognition = new SpeechRecognition()

recognition.lang = "pt-BR"
recognition.continuous = true
recognition.interimResults = false

recognition.onstart = () =>{
document.getElementById("status").innerText = "🎤 Escutando..."
}

recognition.onresult = (event)=>{

let texto = ""

for(let i = event.resultIndex; i < event.results.length; i++){

texto += event.results[i][0].transcript

}

document.getElementById("texto").value += texto + " "

}

recognition.onerror = (event)=>{
document.getElementById("status").innerText = "Erro: " + event.error
}

recognition.start()

}

function parar(){

if(recognition){
recognition.stop()
document.getElementById("status").innerText = "Microfone parado"
}

}

</script>

</body>
</html>
