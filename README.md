<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ENRACOON GAME</title>

<style>
body{
margin:0;
background:black;
color:#00ff66;
font-family:monospace;
overflow:hidden;
}

canvas{
position:fixed;
top:0;
left:0;
z-index:-1;
}

.screen{
display:none;
height:100vh;
justify-content:center;
align-items:center;
flex-direction:column;
}

.active{display:flex;}

input,button{
padding:10px;
margin:5px;
background:black;
color:#00ff66;
border:1px solid #00ff66;
}

.files{
border:1px solid #00ff66;
padding:15px;
width:300px;
}

.file{
cursor:pointer;
margin:5px 0;
}
.file:hover{background:#003300}

.window{
display:none;
position:fixed;
top:50%;
left:50%;
transform:translate(-50%,-50%);
width:500px;
background:black;
border:2px solid #00ff66;
padding:15px;
white-space:pre-wrap;
}

.close{
color:red;
cursor:pointer;
float:right;
}
</style>
</head>

<body>

<canvas id="matrix"></canvas>

<!-- LEVEL 1 -->
<div id="l1" class="screen active">
<h2>ENRACOON SYSTEM</h2>
<p>ENTER PASSWORD</p>
<input id="pass">
<button onclick="login()">ENTER</button>
</div>

<!-- LEVEL 2 -->
<div id="l2" class="screen">

<h3>FILE SYSTEM</h3>

<div class="files">
<div class="file" onclick="openFile('A')">ORANGE.log</div>
<div class="file" onclick="openFile('B')">TANGERINE.dat</div>
<div class="file" onclick="openFile('C')">RACCOON.txt</div>
</div>

<br>

<input id="code" placeholder="final code">
<button onclick="check()">UNLOCK</button>
</div>

<!-- LEVEL 3 -->
<div id="l3" class="screen">
<h2>ACCESS GRANTED</h2>
<p>SYSTEM CORE FOUND</p>
</div>

<!-- WINDOW -->
<div id="win" class="window">
<span class="close" onclick="closeWin()">X</span>
<div id="content"></div>
</div>

<script>

/* PASSWORD */
function login(){
if(document.getElementById("pass").value==="WHAT404"){
show("l2");
}
}

/* SWITCH */
function show(id){
document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
document.getElementById(id).classList.add('active');
}

/* FILES */
function openFile(id){

let data="";

if(id==="A"){
data=`ORANGE LOG
-----------
Status: unstable fruit signal
Code: A1-774

Hint: orange is watching`;
}

if(id==="B"){
data=`TANGERINE DATA
--------------
Error 404 detected
Code: B2-404

Hint: system glitch inside fruit`;
}

if(id==="C"){
data=`RACCOON FILE
------------
AI ACTIVE
Code: C3-911

Hint: raccoon learns from you`;
}

document.getElementById("content").innerText=data;
document.getElementById("win").style.display="block";
}

function closeWin(){
document.getElementById("win").style.display="none";
}

/* FINAL CODE */
function check(){
if(document.getElementById("code").value==="A1-774-B2-404-C3-911"){
show("l3");
}
}

/* MATRIX */
const c=document.getElementById("matrix");
const ctx=c.getContext("2d");

c.width=window.innerWidth;
c.height=window.innerHeight;

let letters="ENRACOON0101MANDARIN";
let font=14;
let cols=Math.floor(c.width/font);
let drops=Array(cols).fill(1);

function draw(){
ctx.fillStyle="rgba(0,0,0,0.08)";
ctx.fillRect(0,0,c.width,c.height);

ctx.fillStyle="#00ff66";
ctx.font=font+"px monospace";

for(let i=0;i<drops.length;i++){
let t=letters[Math.floor(Math.random()*letters.length)];
ctx.fillText(t,i*font,drops[i]*font);

if(drops[i]*font>c.height && Math.random()>0.975){
drops[i]=0;
}
drops[i]++;
}
}

setInterval(draw,33);

window.onresize=()=>{
c.width=window.innerWidth;
c.height=window.innerHeight;
cols=Math.floor(c.width/font);
drops=Array(cols).fill(1);
};

</script>

</body>
</html>
