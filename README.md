<!DOCTYPE html>
<html>
<head>
<title>🔥 SOUROV GOD AURA APP</title>

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

/* DASHBOARD (UNCHANGED) */
#dashboard{display:none;}

header{
    text-align:center;
    padding:15px;
    background:#111827;
}

nav{
    display:flex;
}

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

#rocket{
    width:40px;
    height:60px;
    position:absolute;
    bottom:20px;
    left:45%;
}

#rocket img{
    width:40px;
    height:60px;
}

.ufo{
    width:40px;
    height:40px;
    position:absolute;
}

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

<!-- HOME -->
<div id="home" class="page active">
    <div class="card">
        <h2>Welcome Boss 😎</h2>
        <p>God Mode Activated ⚡</p>

        <!-- GAME BUTTON -->
        <button onclick="openGame()" style="margin-top:10px;background:lime;">
            🎮 ENTER THE GAME
        </button>

    </div>
</div>

<!-- PROFILE -->
<div id="profile" class="page">
    <div class="card">

        <h2>👤 Profile</h2>

        <img src="https://i.postimg.cc/FRjSP1hD/653712939-944444041866038-5160397991737255450-n.jpg"
        style="width:120px;height:120px;border-radius:50%;
        border:3px solid cyan;">

        <p>🧑 Name: Sourov</p>
        <p>⚡ Status: GOD DEV 🔥</p>

        <a href="https://www.facebook.com/so.ur.ov.922939"
        style="color:cyan;">📘 Facebook</a><br><br>

        <a href="https://www.youtube.com/@souroviislam555"
        style="color:cyan;">📺 YouTube</a>

    </div>
</div>

<!-- PORTFOLIO -->
<div id="portfolio" class="page">
    <div class="card">
        <h3>💼 Portfolio</h3>
        <p>🎮 Game Dev (Coming Soon)</p>
        <p>🌐 Web Dev</p>
    </div>
</div>

</div>

<!-- GAME SCREEN -->
<div id="game">

<div id="rocket">
    <img src="https://i.postimg.cc/VknDyssr/images.jpg">
</div>

</div>

<script>

let game=document.getElementById("game");
let rocket=document.getElementById("rocket");

let score=0;
let life=3;
let gameStarted=false;

/* LOGIN */
function login(){
let u=document.getElementById("user").value;
let p=document.getElementById("pass").value;

if(u==="sourov" && p==="sourov"){
document.getElementById("loginPage").style.display="none";
document.getElementById("dashboard").style.display="block";
}else{
alert("Wrong login 😒");
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

/* SHOOT */
function shoot(){
if(!gameStarted) return;

let b=document.createElement("div");
b.classList.add("bullet");

b.style.left=(rocket.offsetLeft+18)+"px";
b.style.bottom="80px";

game.appendChild(b);

let move=setInterval(()=>{

b.style.bottom=(parseInt(b.style.bottom)+12)+"px";

if(parseInt(b.style.bottom)>window.innerHeight){
b.remove();
clearInterval(move);
}

},20);
}

/* AUTO FIRE */
function autoFire(){
setInterval(()=>shoot(),350);
}

/* UFO */
function spawn(){
setInterval(()=>{

if(!gameStarted) return;

let ufo=document.createElement("img");
ufo.src="https://i.postimg.cc/Pr8Bxjrq/images.png";
ufo.className="ufo";

ufo.style.left=Math.random()*(window.innerWidth-40)+"px";
ufo.style.top="0px";

game.appendChild(ufo);

let fall=setInterval(()=>{

ufo.style.top=(ufo.offsetTop+5)+"px";

if(ufo.offsetTop>window.innerHeight){
ufo.remove();
clearInterval(fall);
}

},30);

},1200);
}

/* START GAME */
function startGame(){
gameStarted=true;
autoFire();
spawn();
}

</script>

</body>
</html>
