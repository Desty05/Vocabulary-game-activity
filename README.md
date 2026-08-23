<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tug of Words - What Are You Doing?</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Poppins:wght@400;500;600;700;800&display=swap');

:root{
  --blue:#4f7cff; --blue2:#315fe8; --red:#ff6574; --red2:#e83f55;
  --yellow:#ffd95a; --green:#42c98a; --ink:#25304a; --muted:#69738a;
  --bg:#f5f7ff; --white:#fff; --line:#e6eaf5;
}
*{box-sizing:border-box}
body{
  margin:0; min-height:100vh; font-family:Poppins,sans-serif; color:var(--ink);
  background:radial-gradient(circle at 10% 10%,#fff 0 14%,transparent 15%),
             radial-gradient(circle at 90% 20%,#eef2ff 0 18%,transparent 19%),
             linear-gradient(135deg,#f8faff,#eef3ff);
}
button,input{font:inherit}
button{cursor:pointer;border:0}
.app{width:min(1180px,94%);margin:auto;padding:22px 0 35px}
.topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:15px}
.brand{display:flex;align-items:center;gap:10px;font-family:Fredoka;font-size:24px;font-weight:700}
.logo{width:44px;height:44px;border-radius:14px;background:#fff;display:grid;place-items:center;box-shadow:0 8px 25px #354c8a18;font-size:25px}
.sound-btn,.mini-btn{background:#fff;border:2px solid var(--line);border-radius:13px;padding:9px 13px;color:var(--ink);font-weight:700}
.screen{display:none}.screen.active{display:block}
.card{background:#ffffffed;border:1px solid #fff;border-radius:30px;box-shadow:0 20px 60px #263b7417;padding:34px}
.hero{min-height:650px;display:grid;place-items:center;text-align:center;overflow:hidden;position:relative}
.hero:before,.hero:after{content:"";position:absolute;border-radius:50%;opacity:.45}
.hero:before{width:260px;height:260px;background:#dfe8ff;left:-90px;top:-80px}
.hero:after{width:300px;height:300px;background:#fff0b5;right:-110px;bottom:-120px}
.hero-content{position:relative;z-index:1;max-width:780px}
.badge{display:inline-flex;padding:8px 14px;border-radius:999px;background:#eef3ff;color:var(--blue2);font-weight:800;font-size:13px}
h1{font-family:Fredoka;font-size:clamp(48px,8vw,86px);line-height:.95;margin:18px 0 10px}
.gradient{background:linear-gradient(90deg,var(--blue2),#8a5cff,var(--red2));-webkit-background-clip:text;background-clip:text;color:transparent}
.subtitle{font-size:18px;color:var(--muted);max-width:650px;margin:0 auto 28px}
.rope-demo{height:150px;display:flex;align-items:center;justify-content:center;gap:30px;margin:20px 0}
.kid{font-size:80px;filter:drop-shadow(0 8px 5px #00000012)}
.rope{height:13px;width:min(460px,48vw);background:#b87938;border-radius:20px;position:relative;box-shadow:inset 0 2px #d99a59}
.rope:after{content:"🏁";position:absolute;left:50%;top:50%;transform:translate(-50%,-55%);font-size:28px;background:#fff;padding:2px 8px;border-radius:12px}
.btn{padding:14px 24px;border-radius:16px;font-weight:800;transition:.2s;box-shadow:0 8px 18px #29457b1c}
.btn:hover{transform:translateY(-2px)}
.btn-primary{background:var(--blue);color:#fff}.btn-secondary{background:#fff;border:2px solid var(--line);color:var(--ink)}
.btn-red{background:var(--red);color:#fff}
.btn-green{background:var(--green);color:#fff}
.actions{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}

.setup{max-width:850px;margin:auto;text-align:center}
.section-title{font-family:Fredoka;font-size:38px;margin:4px 0 8px}
.muted{color:var(--muted)}
.players-form{display:grid;grid-template-columns:1fr 1fr;gap:18px;margin:28px 0}
.player-input{padding:22px;border-radius:22px;text-align:left;background:#f8faff;border:2px solid var(--line)}
.player-input.blue{border-color:#bfd0ff}.player-input.red{border-color:#ffc1c8}
.player-label{font-weight:800;display:flex;align-items:center;gap:9px;margin-bottom:10px}
input[type=text]{width:100%;padding:13px 15px;border-radius:13px;border:2px solid var(--line);outline:none;background:#fff}
input[type=text]:focus{border-color:#9db4ff}
.tip{background:#fff8d9;border-radius:17px;padding:13px;color:#705b12;font-size:14px;margin-bottom:20px}

.game-head{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;gap:15px;margin-bottom:16px}
.player-card{padding:16px;border-radius:20px;background:#fff;border:2px solid var(--line);display:flex;align-items:center;gap:12px}
.player-card.blue{border-color:#c5d3ff}.player-card.red{border-color:#ffc9cf;justify-content:flex-end;text-align:right}
.avatar{font-size:38px}.pname{font-weight:800}.score{font-family:Fredoka;font-size:30px}
.turn{background:#fff4c8;padding:10px 15px;border-radius:999px;font-weight:800;white-space:nowrap}
.progress{height:9px;background:#edf0f7;border-radius:20px;overflow:hidden;margin-bottom:20px}
.progress span{display:block;height:100%;background:linear-gradient(90deg,var(--blue),var(--red));width:0%;transition:.4s}
.rope-board{background:linear-gradient(#fff,#fafbff);border:2px solid var(--line);border-radius:24px;padding:18px 18px 25px;margin-bottom:20px}
.rope-track{height:92px;position:relative;max-width:880px;margin:auto}
.track-line{position:absolute;left:5%;right:5%;top:46%;height:12px;background:#b87938;border-radius:20px;box-shadow:inset 0 2px #e1a463}
.center-flag{position:absolute;left:50%;top:23%;transform:translateX(-50%);font-size:25px;background:#fff;padding:2px 7px;border-radius:10px;z-index:2}
.pull-marker{position:absolute;top:8%;left:50%;transform:translateX(-50%);font-size:50px;transition:left .55s cubic-bezier(.2,.9,.25,1);z-index:3}
.end-labels{display:flex;justify-content:space-between;font-weight:800;font-size:13px;color:var(--muted)}
.question-card{text-align:center;padding:30px}
.turn-label{font-weight:800;color:var(--blue2);letter-spacing:.4px}
.question-image{font-size:90px;line-height:1;margin:13px 0}
.question{font-family:Fredoka;font-size:30px;margin:0 auto 22px;max-width:800px}
.options{display:grid;grid-template-columns:1fr 1fr;gap:13px;max-width:800px;margin:auto}
.option{padding:17px;border-radius:17px;background:#fff;border:2px solid var(--line);font-weight:700;text-align:left;transition:.2s}
.option:hover:not(:disabled){transform:translateY(-2px);border-color:#9db4ff;background:#f7f9ff}
.option:disabled{cursor:default}.option.correct{border-color:var(--green);background:#eafbf3}.option.wrong{border-color:var(--red);background:#fff0f2}
.feedback{min-height:30px;font-weight:800;margin-top:15px}
.feedback.good{color:#159b63}.feedback.bad{color:#df3c51}
.next-wrap{margin-top:15px}

.modal{position:fixed;inset:0;background:#17213c99;display:none;place-items:center;padding:20px;z-index:20}
.modal.show{display:grid}
.modal-card{background:#fff;border-radius:28px;padding:35px;max-width:500px;width:100%;text-align:center;box-shadow:0 30px 80px #0003}
.modal-icon{font-size:65px}.modal-card h2{font-family:Fredoka;font-size:40px;margin:8px 0}
.result-score{display:flex;justify-content:center;gap:25px;margin:20px 0}.result-score div{padding:15px 25px;border-radius:18px;background:#f7f8fc}
.confetti{position:fixed;inset:0;pointer-events:none;z-index:30;overflow:hidden}
.confetti i{position:absolute;top:-20px;width:10px;height:18px;animation:fall 2.5s linear forwards}
@keyframes fall{to{transform:translateY(110vh) rotate(720deg);opacity:0}}
.shake{animation:shake .4s}.pull{animation:pull .5s}
@keyframes shake{25%{transform:translateX(-8px)}75%{transform:translateX(8px)}}
@keyframes pull{50%{scale:1.12}}
.hidden{display:none!important}
.footer{text-align:center;color:#8991a5;font-size:12px;margin-top:15px}
@media(max-width:760px){
 .app{width:96%;padding-top:10px}.card{padding:20px;border-radius:22px}
 .players-form{grid-template-columns:1fr}.game-head{grid-template-columns:1fr 1fr}.turn{grid-column:1/-1;grid-row:1;justify-self:center}
 .player-card{padding:11px}.score{font-size:25px}.avatar{font-size:30px}
 .options{grid-template-columns:1fr}.question{font-size:25px}.question-image{font-size:75px}
 .rope-track{height:75px}.pull-marker{font-size:40px}.track-line{top:46%}
}
</style>
</head>
<body>
<div class="app">
  <div class="topbar">
    <div class="brand"><div class="logo">🪢</div> Tug of Words</div>
    <button class="sound-btn" id="soundBtn" onclick="toggleSound()">🔊 Sound On</button>
  </div>

  <section id="home" class="screen active">
    <div class="card hero">
      <div class="hero-content">
        <span class="badge">ENGLISH • GRADE 4 • GAME-BASED LEARNING</span>
        <h1><span class="gradient">TUG OF WORDS</span></h1>
        <p class="subtitle"><b>What Are You Doing?</b><br>Answer the question correctly, pull the rope, and become the English champion!</p>
        <div class="rope-demo">
          <div class="kid">👦</div><div class="rope"></div><div class="kid">👧</div>
        </div>
        <div class="actions">
          <button class="btn btn-primary" onclick="showScreen('setup')">🎮 PLAY GAME</button>
          <button class="btn btn-secondary" onclick="openHow()">📖 HOW TO PLAY</button>
        </div>
      </div>
    </div>
  </section>

  <section id="setup" class="screen">
    <div class="card setup">
      <span class="badge">PLAYER SETUP</span>
      <h2 class="section-title">Ready, English Heroes?</h2>
      <p class="muted">Enter the names of the two students.</p>
      <div class="players-form">
        <div class="player-input blue">
          <div class="player-label">🔵 PLAYER 1</div>
          <input id="p1" type="text" maxlength="18" placeholder="Name Player 1">
        </div>
        <div class="player-input red">
          <div class="player-label">🔴 PLAYER 2</div>
          <input id="p2" type="text" maxlength="18" placeholder="Name Player 2">
        </div>
      </div>
      <div class="tip">💡 Tip: Take turns. Correct answer = pull the rope one step!</div>
      <div class="actions">
        <button class="btn btn-secondary" onclick="showScreen('home')">← Back</button>
        <button class="btn btn-primary" onclick="startGame()">START GAME 🚀</button>
      </div>
    </div>
  </section>

  <section id="game" class="screen">
    <div class="game-head">
      <div class="player-card blue">
        <div class="avatar">👦</div><div><div class="pname" id="name1">Player 1</div><div class="score" id="score1">0</div></div>
      </div>
      <div class="turn" id="turnText">PLAYER 1'S TURN</div>
      <div class="player-card red">
        <div><div class="pname" id="name2">Player 2</div><div class="score" id="score2">0</div></div><div class="avatar">👧</div>
      </div>
    </div>

    <div class="progress"><span id="progressBar"></span></div>

    <div class="rope-board">
      <div class="rope-track">
        <div class="track-line"></div>
        <div class="center-flag">🏁</div>
        <div class="pull-marker" id="marker">🪢</div>
      </div>
      <div class="end-labels"><span>🔵 <span id="label1">Player 1</span></span><span>🏆 GOAL</span><span><span id="label2">Player 2</span> 🔴</span></div>
    </div>

    <div class="card question-card">
      <div class="turn-label" id="questionNumber">QUESTION 1</div>
      <div class="question-image" id="qImage">📖</div>
      <h2 class="question" id="questionText">What is he doing?</h2>
      <div class="options" id="options"></div>
      <div class="feedback" id="feedback"></div>
      <div class="next-wrap hidden" id="nextWrap"><button class="btn btn-primary" onclick="nextQuestion()">NEXT QUESTION →</button></div>
    </div>
    <div class="footer">Tug of Words • What Are You Doing? • Grade 4</div>
  </section>
</div>

<div class="modal" id="howModal">
  <div class="modal-card">
    <div class="modal-icon">🎮</div>
    <h2>How to Play?</h2>
    <p><b>1.</b> Enter two player names.<br>
       <b>2.</b> Take turns answering questions.<br>
       <b>3.</b> Correct answer → 🪢 pull the rope one step.<br>
       <b>4.</b> Wrong answer → no pull, then continue.<br>
       <b>5.</b> The first player to pull the rope to their side wins!</p>
    <button class="btn btn-primary" onclick="closeHow()">LET'S PLAY!</button>
  </div>
</div>

<div class="modal" id="resultModal">
  <div class="modal-card">
    <div class="modal-icon" id="resultIcon">🏆</div>
    <h2 id="winnerTitle">PLAYER 1 WINS!</h2>
    <p id="winnerMessage">Amazing! You are an English Hero!</p>
    <div class="result-score">
      <div>🔵 <b id="final1">0</b><br><span id="finalName1">Player 1</span></div>
      <div>🔴 <b id="final2">0</b><br><span id="finalName2">Player 2</span></div>
    </div>
    <div class="actions">
      <button class="btn btn-primary" onclick="restartGame()">🔄 PLAY AGAIN</button>
      <button class="btn btn-secondary" onclick="goHome()">🏠 HOME</button>
    </div>
  </div>
</div>
<div class="confetti" id="confetti"></div>

<script>
const questions = [
  {q:"What is she doing?", img:"📖", options:["She is dancing.","She is reading.","She is writing.","She is watching."], answer:1},
  {q:"What is he doing?", img:"✏️", options:["He is reading.","He is dancing.","He is writing.","He is going."], answer:2},
  {q:"Look! She is moving to music. What is she doing?", img:"💃", options:["She is dancing.","She is reading.","She is having lunch.","She is writing."], answer:0},
  {q:"What is he doing?", img:"📺", options:["He is discussing.","He is watching.","He is dancing.","He is reading."], answer:1},
  {q:"Budi is eating his lunch. What is Budi doing?", img:"🍱", options:["He is writing.","He is going.","He is having lunch.","He is dancing."], answer:2},
  {q:"Sinta is going to school. What is she doing?", img:"🎒", options:["She is going.","She is reading.","She is watching.","She is dancing."], answer:0},
  {q:"Two students are talking about their homework. What are they doing?", img:"💬", options:["They are watching.","They are discussing.","They are dancing.","They are having lunch."], answer:1},
  {q:"Which sentence is correct?", img:"🧒", options:["She are reading.","She is reading.","She reading is.","She am reading."], answer:1},
  {q:"Which sentence means 'Dia sedang menari'?", img:"💃", options:["She is dancing.","She is writing.","She is watching.","She is going."], answer:0},
  {q:"Which sentence means 'Mereka sedang berdiskusi'?", img:"👧🧒", options:["They are reading.","They are going.","They are discussing.","They are dancing."], answer:2},
  {q:"Look! Rani has a pen and a notebook. What is she doing?", img:"📝", options:["She is writing.","She is watching.","She is dancing.","She is having lunch."], answer:0},
  {q:"Look! Andi has food in front of him. What is he doing?", img:"🍽️", options:["He is reading.","He is having lunch.","He is going.","He is discussing."], answer:1}
];

let state = {p1:"Player 1",p2:"Player 2",turn:0,scores:[0,0],position:0,index:0,order:[],sound:true,locked:false};

function showScreen(id){
  document.querySelectorAll(".screen").forEach(s=>s.classList.remove("active"));
  document.getElementById(id).classList.add("active");
}
function openHow(){document.getElementById("howModal").classList.add("show")}
function closeHow(){document.getElementById("howModal").classList.remove("show")}
function toggleSound(){
  state.sound=!state.sound;
  document.getElementById("soundBtn").textContent=state.sound?"🔊 Sound On":"🔇 Sound Off";
}
function speak(text){
  if(!state.sound || !("speechSynthesis" in window)) return;
  speechSynthesis.cancel();
  const u=new SpeechSynthesisUtterance(text);
  u.lang="en-US"; u.rate=.88;
  speechSynthesis.speak(u);
}
function shuffle(arr){
  for(let i=arr.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[arr[i],arr[j]]=[arr[j],arr[i]]}
  return arr;
}
function startGame(){
  state.p1=document.getElementById("p1").value.trim()||"Player 1";
  state.p2=document.getElementById("p2").value.trim()||"Player 2";
  state.turn=0; state.scores=[0,0]; state.position=0; state.index=0; state.locked=false;
  state.order=shuffle([...Array(questions.length).keys()]);
  document.getElementById("name1").textContent=state.p1;
  document.getElementById("name2").textContent=state.p2;
  document.getElementById("label1").textContent=state.p1;
  document.getElementById("label2").textContent=state.p2;
  showScreen("game"); renderQuestion();
}
function renderQuestion(){
  state.locked=false;
  const q=questions[state.order[state.index]];
  document.getElementById("turnText").textContent=(state.turn===0?state.p1:state.p2).toUpperCase()+"'S TURN";
  document.getElementById("questionNumber").textContent=`QUESTION ${state.index+1} / ${questions.length}`;
  document.getElementById("qImage").textContent=q.img;
  document.getElementById("questionText").textContent=q.q;
  document.getElementById("feedback").textContent="";
  document.getElementById("feedback").className="feedback";
  document.getElementById("nextWrap").classList.add("hidden");
  document.getElementById("score1").textContent=state.scores[0];
  document.getElementById("score2").textContent=state.scores[1];
  document.getElementById("progressBar").style.width=((state.index)/questions.length*100)+"%";
  const box=document.getElementById("options"); box.innerHTML="";
  q.options.forEach((opt,i)=>{
    const b=document.createElement("button");
    b.className="option"; b.textContent=String.fromCharCode(65+i)+". "+opt;
    b.onclick=()=>answer(i,b); box.appendChild(b);
  });
  speak(q.q);
}
function answer(choice,button){
  if(state.locked)return;
  state.locked=true;
  const q=questions[state.order[state.index]];
  const buttons=[...document.querySelectorAll(".option")];
  buttons.forEach(b=>b.disabled=true);
  if(choice===q.answer){
    button.classList.add("correct");
    state.scores[state.turn]++;
    state.position += state.turn===0 ? -1 : 1;
    state.position=Math.max(-5,Math.min(5,state.position));
    updateMarker();
    const f=document.getElementById("feedback");
    f.textContent="🎉 CORRECT! Pull the rope!";
    f.className="feedback good";
    speak("Correct! Pull the rope!");
    document.getElementById("marker").classList.add("pull");
    setTimeout(()=>document.getElementById("marker").classList.remove("pull"),500);
    document.getElementById("game").classList.add("shake");
    setTimeout(()=>document.getElementById("game").classList.remove("shake"),400);
    if(Math.abs(state.position)>=5){setTimeout(showWinner,650);return}
  }else{
    button.classList.add("wrong");
    buttons[q.answer].classList.add("correct");
    const f=document.getElementById("feedback");
    f.textContent="❌ Not quite! The correct answer is: "+q.options[q.answer];
    f.className="feedback bad";
    speak("Try again. The correct answer is "+q.options[q.answer]);
  }
  document.getElementById("score1").textContent=state.scores[0];
  document.getElementById("score2").textContent=state.scores[1];
  document.getElementById("nextWrap").classList.remove("hidden");
}
function updateMarker(){
  const left=50+(state.position*8.8);
  document.getElementById("marker").style.left=left+"%";
}
function nextQuestion(){
  state.index++;
  if(state.index>=questions.length){showWinner();return}
  state.turn=state.turn===0?1:0;
  renderQuestion();
}
function showWinner(){
  const winner=state.position<0?0:state.position>0?1:(state.scores[0]>=state.scores[1]?0:1);
  const winnerName=winner===0?state.p1:state.p2;
  document.getElementById("winnerTitle").textContent="🏆 "+winnerName.toUpperCase()+" WINS!";
  document.getElementById("winnerMessage").textContent="Amazing! You are an English Hero! 🌟";
  document.getElementById("final1").textContent=state.scores[0];
  document.getElementById("final2").textContent=state.scores[1];
  document.getElementById("finalName1").textContent=state.p1;
  document.getElementById("finalName2").textContent=state.p2;
  document.getElementById("resultModal").classList.add("show");
  confetti();
  speak(winnerName+" wins! Amazing!");
}
function confetti(){
  const c=document.getElementById("confetti"); c.innerHTML="";
  for(let i=0;i<80;i++){
    const x=document.createElement("i");
    x.style.left=Math.random()*100+"%";
    x.style.animationDelay=Math.random()*.8+"s";
    x.style.background=["#4f7cff","#ff6574","#ffd95a","#42c98a","#8a5cff"][Math.floor(Math.random()*5)];
    x.style.transform=`rotate(${Math.random()*360}deg)`;
    c.appendChild(x);
  }
  setTimeout(()=>c.innerHTML="",3200);
}
function restartGame(){
  document.getElementById("resultModal").classList.remove("show");
  startGame();
}
function goHome(){
  document.getElementById("resultModal").classList.remove("show");
  showScreen("home");
}
</script>
</body>
</html>
