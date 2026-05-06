<!DOCTYPE html>
<html>
<head>
<title>🔥 SOUROV GOD AURA GAME PRO MAX</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
    margin:0;
    font-family:Arial;
    background:#020617;
    color:white;
    max-width:420px;
    margin:auto;
}

/* LOGIN */
#loginPage{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}

.box{
    background:rgba(255,255,255,0.06);
    padding:30px;
    border-radius:20px;
    text-align:center;
}

input{
    padding:10px;
    margin:8px;
    width:220px;
    border:none;
    border-radius:10px;
}

button{
    padding:10px 18px;
    border:none;
    border-radius:10px;
    background:cyan;
    font-weight:bold;
    cursor:pointer;
}

/* DASHBOARD */
#dashboard{display:none;}

header{
    text-align:center;
    padding:15px;
    background:#111827;
}

nav{display:flex;}

nav button{
    flex:1;
    padding:10px;
    border:none;
    background:#111827;
    color:white;
}

.page{display:none;padding:15px;}
.active{display:block;}

.card{
    background:rgba(255,255,255,0.05);
    margin:10px;
    padding:20px;
    border-radius:15px;
    text-align:center;
}

/* GAME */
#game{
    display:none;
    position:fixed;
    top:0;
    left:0;
    width:100%;
    height:100%;
    background:black;
    overflow:hidden;
}

/* HUD */
#hud{
    position:fixed;
    top:10px;
    left:10px;
    font-size:14px;
    z-index:10;
}

/* ROCKET */
#rocket{
    width:40px;
    height:60px;
    position:absolute;
    bottom:20px;
    left:45%;
}

#rocket img{width:40px;height:60px;}

/* UFO */
.ufo{
    width:40px;
    height:40px;
    position:absolute;
}

/* BOSS UFO */
.boss{
    width:70px;
    height:70px;
    position:absolute;
}

/* BULLET */
.bullet{
    width:5px;
    height:15px;
    background:yellow;
    position:absolute;
}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="loginPage">
    <div class="box">
        <h2>⚡ GOD LOGIN</h2>
        <input id="user" placeholder="Username">
        <input id="pass" type="password" placeholder="Password">
        <button onclick="login()">ENTER 🚀</button>
    </div>
</div>

<!-- DASHBOARD -->
<div id="dashboard">

<header>🔥 SOUROV GOD AURA APP</header>

<nav>
    <button onclick="show('home')">Home</button>
    <button onclick="show('profile')">Profile</button>
    <button onclick="show('portfolio')">Portfolio</button>
</nav>

<div id="home" class="page active">
    <div class="card">
        <h2>Welcome Boss 😎</h2>
        <button onclick="openGame()" style="background:lime;">
            🎮 ENTER THE GAME
        </button>
    </div>
</div>

<div id="profile" class="page">
    <div class="card">
        <h2>👤 Profile</h2>

        <img src="https://i.postimg.cc/FRjSP1hD/653712939-944444041866038-5160397991737255450-n.jpg"
        style="width:120px;height:120px;border-radius:50%;
        border:3px solid cyan;">

        <p>Sourov</p>

        <a href="https://www.facebook.com/so.ur.ov.922939" style="color:cyan;">Facebook</a><br><br>
        <a href="https://www.youtube.com/@souroviislam555" style="color:cyan;">YouTube</a>
    </div>
</div>

<div id="portfolio" class="page">
    <div class="card">
        <p>🎮 Game Dev</p>
        <p>🌐 Web Dev</p>
    </div>
</div>

</div>

<!-- GAME -->
<div id="game">

<div id="hud">
🏆 Score: <span id="score">0</span> |
❤️ Life: <span id="life">3</span>
</div>

<div id="rocket">
    <img src="https://i.postimg.cc/VknDyssr/images.jpg">
</div>

</div>

<!-- SOUND -->
<audio id="shootSound" src="https://www.soundjay.com/buttons/sounds/button-3.mp3"></audio>
<audio id="hitSound" src="https://www.soundjay.com/explosion/sounds/explosion-01.mp3"></audio>

<script>

let game=document.getElementById("game");
let rocket=document.getElementById("rocket");

let score=0;
let life=3;
let gameStarted=false;
let bossSpawned=false;

/* LOGIN */
function login(){
let u=document.getElementById("user").value;
let p=document.getElementById("pass").value;

if(u==="sourov" && p==="sourov"){
document.getElementById("loginPage").style.display="none";
document.getElementById("dashboard").style.display="block";
}else{
alert("Wrong 😒");
}
}

/* NAV */
function show(id){
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* OPEN GAME */
function openGame(){
game.style.display="block";
startGame();
}

/* MOVE */
document.addEventListener("keydown",(e)=>{
if(!gameStarted) return;

let left=rocket.offsetLeft;

if(e.key==="ArrowLeft" && left>0){
rocket.style.left=(left-20)+"px";
}

if(e.key==="ArrowRight" && left<window.innerWidth-40){
rocket.style.left=(left+20)+"px";
}
});

/* SHOOT SOUND */
function playShoot(){
document.getElementById("shootSound").play();
}

/* HIT SOUND */
function playHit(){
document.getElementById("hitSound").play();
}

/* SHOOT */
function shoot(){

if(!gameStarted) return;

playShoot();

let b=document.createElement("div");
b.classList.add("bullet");

b.style.left=(rocket.offsetLeft+18)+"px";
b.style.bottom="80px";

game.appendChild(b);

let move=setInterval(()=>{

b.style.bottom=(parseInt(b.style.bottom)+12)+"px";

document.querySelectorAll(".ufo,.boss").forEach(ufo=>{
if(collide(b,ufo)){
ufo.remove();
b.remove();

score++;
document.getElementById("score").innerText=score;

playHit();
}
});

if(parseInt(b.style.bottom)>window.innerHeight){
b.remove();
clearInterval(move);
}

},20);
}

/* AUTO FIRE */
setInterval(()=>shoot(),300);

/* UFO */
function spawn(){

setInterval(()=>{

if(!gameStarted) return;

/* BOSS UFO (AI) */
if(score>10 && !bossSpawned){
bossSpawned=true;

let boss=document.createElement("img");
boss.src="https://i.postimg.cc/Pr8Bxjrq/images.png";
boss.className="boss";

boss.style.left="100px";
boss.style.top="0px";

game.appendChild(boss);

setInterval(()=>{

let rx=rocket.offsetLeft;
let bx=boss.offsetLeft;

if(rx>bx) boss.style.left=(bx+2)+"px";
if(rx<bx) boss.style.left=(bx-2)+"px";

boss.style.top=(boss.offsetTop+1)+"px";

if(collide(boss,rocket)){
damage();
}

},30);
}

/* NORMAL UFO */
let ufo=document.createElement("img");
ufo.src="https://i.postimg.cc/Pr8Bxjrq/images.png";
ufo.className="ufo";

ufo.style.left=Math.random()*(window.innerWidth-40)+"px";
ufo.style.top="0px";

game.appendChild(ufo);

let fall=setInterval(()=>{

ufo.style.top=(ufo.offsetTop+5)+"px";

if(collide(ufo,rocket)){
damage();
ufo.remove();
clearInterval(fall);
}

if(ufo.offsetTop>window.innerHeight){
ufo.remove();
clearInterval(fall);
}

},30);

},1200);
}

/* DAMAGE */
function damage(){
life--;
document.getElementById("life").innerText=life;
playHit();

if(life<=0){
endGame();
}
}

/* GAME OVER */
function endGame(){
gameStarted=false;

document.body.innerHTML+=`
<div style="position:fixed;top:0;left:0;width:100%;height:100%;
background:black;color:red;display:flex;
flex-direction:column;justify-content:center;
align-items:center;font-size:30px;z-index:9999;">
💀 GAME OVER<br><br>
🏆 Score: ${score}<br><br>
<button onclick="location.reload()" style="padding:10px 20px;background:lime;border:none;">
RESTART 🔁
</button>
</div>`;
}

/* COLLISION */
function collide(a,b){
if(!a||!b) return false;

let r1=a.getBoundingClientRect();
let r2=b.getBoundingClientRect();

return !(r1.top>r2.bottom||r1.bottom<r2.top||r1.left>r2.right||r1.right<r2.left);
}

/* START */
function startGame(){
gameStarted=true;
spawn();
}

</script>

</body>
</html>
