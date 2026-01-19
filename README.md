<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>For Disha 🌸</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500&family=Pacifico&display=swap" rel="stylesheet">

<style>
*{margin:0;padding:0;box-sizing:border-box}

body{
  font-family:Poppins,sans-serif;
  background:linear-gradient(#faf7ff,#f2edff);
  min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  overflow:hidden;
}

/* night mode */
body.night{
  background:linear-gradient(#0f1025,#1a1b3a);
  color:#eee;
}

.container{
  width:92%;
  max-width:420px;
  z-index:5;
}

.card{
  background:#fff;
  border-radius:22px;
  padding:28px;
  text-align:center;
  box-shadow:0 18px 35px rgba(0,0,0,.15);
  animation:fadeUp .6s ease;
}

body.night .card{background:#1f2147}

.hidden{display:none}

h1{
  font-family:Pacifico;
  color:#6b5be3;
  margin-bottom:14px;
}

p{
  font-size:14.5px;
  line-height:1.8;
  color:#555;
}

body.night p{color:#ccc}

button{
  margin-top:14px;
  padding:13px;
  width:100%;
  border:none;
  border-radius:28px;
  background:#6b5be3;
  color:white;
  font-size:15px;
  cursor:pointer;
}

button.secondary{
  background:#ede9ff;
  color:#4a3fc9;
}

body.night button.secondary{
  background:#2a2d66;
  color:#c6c4ff;
}

/* animations */
@keyframes fadeUp{
  from{opacity:0;transform:translateY(25px)}
  to{opacity:1;transform:translateY(0)}
}

/* 🌸 FLOWERS (BACKGROUND) */
.petal{
  position:fixed;
  top:-10px;
  font-size:22px;
  opacity:.7;
  animation:fall linear infinite;
  z-index:999;
}
@keyframes fall{
  to{transform:translateY(110vh) rotate(360deg)}
}

/* 💖 HEART SHOWER (BACKGROUND) */
.heart{
  position:fixed;
  top:-20px;
  font-size:28px;
  opacity:.7;
  animation:heartFall linear forwards;
  z-index:999;
}
@keyframes heartFall{
  to{
    transform:translateY(110vh) scale(1.4);
    opacity:0;
  }
}

/* popup */
.correct-pop{
  position:fixed;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%) scale(0);
  background:#ff6fae;
  color:white;
  padding:18px 28px;
  border-radius:30px;
  font-size:17px;
  animation:pop .6s ease forwards;
  z-index:1000;
}
@keyframes pop{
  0%{transform:translate(-50%,-50%) scale(0)}
  70%{transform:translate(-50%,-50%) scale(1.2)}
  100%{transform:translate(-50%,-50%) scale(1)}
}

/* music */
.music{
  position:fixed;
  bottom:16px;
  right:16px;
  background:#fff;
  padding:10px 14px;
  border-radius:22px;
  font-size:13px;
  cursor:pointer;
  box-shadow:0 6px 15px rgba(0,0,0,.2);
  z-index:1000;
}
body.night .music{background:#1f2147;color:#eee}
</style>
</head>

<body>

<audio id="bgm" loop>
  <source src="music.mp3" type="audio/mpeg">
</audio>

<div class="music" onclick="toggleMusic()">🎶 Music</div>

<div class="container">

<!-- INTRO -->
<div class="card" id="s1">
<h1>Hello Disha 🌸</h1>
<p>This isn’t meant to be rushed.<br>Just a soft little journey.</p>
<button onclick="start()">Begin</button>
</div>

<div class="card hidden" id="s2">
<h1>A Thought 💭</h1>
<p>Some people don’t solve problems.<br>They simply stay.</p>
<button onclick="next(2)">Next</button>
</div>

<div class="card hidden" id="s3">
<h1>That Feels Like You</h1>
<p>Quiet presence.<br>Gentle strength.</p>
<button onclick="next(3)">🙂</button>
</div>

<!-- ORIGINAL QUIZ SET -->
<div class="card hidden" id="s4">
<h1>Little Question 🧠</h1>
<p>What matters more?</p>
<button onclick="correct(4)">Being kind</button>
<button class="secondary" onclick="wrong()">Being impressive</button>
</div>

<div class="card hidden" id="s5">
<h1>Another One 🌱</h1>
<p>Does I have someone other prior than u...</p>
<button onclick="correct(5)">neverr 😆;)</button>
<button class="secondary" onclick="wrong()">Yess 😒🤦‍♂️</button>
</div>

<div class="card hidden" id="s6">
<h1>Small Choice 🤍</h1>
<p>Support means…</p>
<button onclick="wrong()">Giving advices</button>
<button class="secondary" onclick="correct(6)">Listening each other</button>
</div>

<!-- PREVIOUSLY REMOVED QUESTIONS (NOW BACK) -->
<div class="card hidden" id="s7">
<h1>Tiny Thought 🧠</h1>
<p>Which one feels closer?</p>
<button onclick="correct(7)">Being there matters 🤍</button>
<button class="secondary" onclick="wrong()">Being right always</button>
</div>

<div class="card hidden" id="s8">
<h1>Another Pause 🌼</h1>
<p>Kindness is often…</p>
<button onclick="correct(8)">Quiet and consistent</button>
<button class="secondary" onclick="wrong()">Loud and visible</button>
</div>

<!-- FINAL -->
<div class="card hidden" id="s9">
<h1>Thank You, Disha 🤍</h1>
<p>
For your patience.<br>
For your calm presence.<br>
For being you.
</p>
<button onclick="final()">😊</button>
<button class="secondary" onclick="restart()">Restart</button>
</div>

</div>

<script>
/* night mode */
const hour=new Date().getHours();
if(hour>=19||hour<6) document.body.classList.add("night");

/* navigation */
function start(){
  const bgm=document.getElementById("bgm");
  bgm.volume=.35;
  bgm.play().catch(()=>{});
  next(1);
}
function next(n){
  document.getElementById("s"+n).classList.add("hidden");
  document.getElementById("s"+(n+1)).classList.remove("hidden");
}

/* popup */
function popup(text){
  const p=document.createElement("div");
  p.className="correct-pop";
  p.innerText=text;
  document.body.appendChild(p);
  setTimeout(()=>p.remove(),1400);
}

/* quiz */
function correct(n){
  popup("Correct 🤍");
  heartShower(25);
  setTimeout(()=>next(n),1000);
}
function wrong(){
  popup("That didn’t feel right 😿🥲");
}

/* 💖 HEART ALWAYS */
function heartShower(count){
  for(let i=0;i<count;i++){
    let h=document.createElement("div");
    h.className="heart";
    h.innerText=["💖","💗","💝","💞","❤️"][Math.floor(Math.random()*5)];
    h.style.left=Math.random()*100+"vw";
    h.style.animationDuration=3+Math.random()*2+"s";
    document.body.appendChild(h);
    setTimeout(()=>h.remove(),5000);
  }
}

/* 🌸 FLOWERS ALWAYS */
for(let i=0;i<18;i++){
  let p=document.createElement("div");
  p.className="petal";
  p.innerText="🌸";
  p.style.left=Math.random()*100+"vw";
  p.style.animationDuration=6+Math.random()*6+"s";
  document.body.appendChild(p);
}

/* music */
function toggleMusic(){
  const bgm=document.getElementById("bgm");
  bgm.paused?bgm.play():bgm.pause();
}

/* final */
function final(){
  popup("Thanks for being there for me 💖💕🤞");
  heartShower(50);
}
function restart(){location.reload();}
</script>

</body>
</html>
