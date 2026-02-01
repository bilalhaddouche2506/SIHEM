# SIHEM
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>💘 Question importante</title>
  <style>
    body{
      margin:0; min-height:100vh; display:flex; justify-content:center; align-items:center;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial;
      background: radial-gradient(circle at top, #ffb6d5, #0b0b12);
      overflow:hidden; color:white;
    }
    .card{
      width:min(620px,92vw);
      background: rgba(255,255,255,.12);
      border: 1px solid rgba(255,255,255,.25);
      border-radius: 22px;
      padding: 28px;
      text-align:center;
      backdrop-filter: blur(14px);
      box-shadow: 0 20px 60px rgba(0,0,0,.4);
    }
    h1{ font-size: clamp(26px,4vw,42px); margin: 0 0 10px; }
    p{ color: rgba(255,255,255,.82); margin: 0 0 18px; }
    .chips{ display:flex; flex-wrap:wrap; justify-content:center; gap:10px; margin-bottom:20px; }
    .chip{
      padding:10px 14px; border-radius:999px;
      border:1px solid rgba(255,255,255,.25);
      background: rgba(255,255,255,.08);
      font-size:14px;
    }
    .btns{
      position:relative; height:140px;
      display:flex; justify-content:center; align-items:center; gap:15px;
    }
    button{
      border:0; padding:14px 18px; border-radius:16px;
      font-size:18px; cursor:pointer; font-weight:750;
    }
    #yes{
      background: linear-gradient(135deg,#ff2d7a,#ff77aa);
      color:white; box-shadow: 0 12px 30px rgba(255,45,122,.4);
    }
    #no{
      position:absolute; left:60%; top:55%;
      transform:translate(-50%,-50%);
      background: rgba(255,255,255,.12);
      border:1px solid rgba(255,255,255,.25);
      color:white;
    }
    .overlay{
      position:fixed; inset:0; background: rgba(0,0,0,.6);
      display:none; justify-content:center; align-items:center; padding:18px;
    }
    .overlay.show{ display:flex; }
    .modal{
      background: rgba(15,15,25,.9);
      padding:28px; border-radius:22px; text-align:center;
      width:min(520px,92vw);
      border:1px solid rgba(255,255,255,.2);
    }
    canvas{ position:fixed; inset:0; pointer-events:none; }
  </style>
</head>
<body>
  <canvas id="confetti"></canvas>

  <div class="card">
    <h1>Sihem… veux-tu être ma Valentine ? 💘</h1>
    <p>Ma Princesse, je s'occupe de tout tu s'occupe de rien 😉😌</p>

    <div class="chips">
      <div class="chip">✨ Plan : Date surprise + dessert + un petit cadeau</div>
      <div class="chip">📍 Restaurant à Paris</div>
    </div>

    <div class="btns" id="zone">
      <button id="yes">Oui 💖</button>
      <button id="no">Non 🙃</button>
    </div>
  </div>

  <div class="overlay" id="overlay">
    <div class="modal">
      <h1>YEEEES 😭💖</h1>
      <p>Ok c’est officiel Ma Princesse…</p>
      <p>📍 Restaurant sur Paris le 14 février 2026</p>
      <p>✨ Date surprise + dessert + un petit cadeau</p>
      <p>Je t'aime plus que tout❤️🫶</p>
    </div>
  </div>

  <script>
    // Non qui fuit
    const noBtn = document.getElementById("no");
    const zone = document.getElementById("zone");
    function moveNo(){
      const rect = zone.getBoundingClientRect();
      const x = Math.random() * (rect.width - noBtn.offsetWidth);
      const y = Math.random() * (rect.height - noBtn.offsetHeight);
      noBtn.style.left = x + "px";
      noBtn.style.top = y + "px";
      noBtn.style.transform = "translate(0,0)";
    }
    noBtn.addEventListener("mouseenter", moveNo);
    noBtn.addEventListener("touchstart", (e)=>{ e.preventDefault(); moveNo(); }, {passive:false});

    // Confettis + overlay
    const yesBtn = document.getElementById("yes");
    const overlay = document.getElementById("overlay");
    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");
    function resize(){ canvas.width = innerWidth; canvas.height = innerHeight; }
    addEventListener("resize", resize); resize();

    let parts = [], animId;
    function spawn(){
      parts=[];
      for(let i=0;i<180;i++){
        parts.push({ x:Math.random()*canvas.width, y:-20, vy:2+Math.random()*4, vx:-2+Math.random()*4, r:3+Math.random()*4 });
      }
    }
    function animate(){
      ctx.clearRect(0,0,canvas.width,canvas.height);
      for(const p of parts){
        p.x += p.vx; p.y += p.vy; p.vy += 0.03;
        ctx.fillStyle="white";
        ctx.fillRect(p.x,p.y,p.r*2,p.r);
      }
      animId = requestAnimationFrame(animate);
    }

    yesBtn.addEventListener("click", ()=>{
      overlay.classList.add("show");
      spawn();
      cancelAnimationFrame(animId);
      animate();
    });

    overlay.addEventListener("click", (e)=>{
      if(e.target === overlay) overlay.classList.remove("show");
    });
  </script>
</body>
</html>
