[Skyfall Royale.html](https://github.com/user-attachments/files/34636400/Skyfall.Royale.html)
<!DOCTYPE html>
<html lang="de"><head><meta charset="utf-8"><title>Skyfall Royale</title>
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, maximum-scale=1, user-scalable=no">
<link href="https://fonts.googleapis.com/css2?family=Lilita+One&family=Nunito:wght@600;800&display=swap" rel="stylesheet">
<style>
:root{--bg:#150a2e;--bg2:#2a1260;--gold:#ffc93c;--vio:#9b5cff;--ink:#fff7e0;--card:#ffffff14;color-scheme:dark}
*{box-sizing:border-box;margin:0}html,body{height:100%}
body{background:radial-gradient(circle at 50% 0,var(--bg2),var(--bg));color:var(--ink);font:800 16px Nunito,system-ui,sans-serif;overflow:hidden;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
h1,h2,.btn{font-family:'Lilita One',Impact,sans-serif;letter-spacing:.02em}
.scr{position:absolute;inset:0;display:none;flex-direction:column;align-items:center;padding:16px;overflow:auto}.scr.on{display:flex}
nav{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin:8px 0 14px}
.btn{background:var(--card);color:var(--ink);border:2px solid #ffffff30;border-radius:12px;padding:10px 18px;font-size:19px;cursor:pointer}
.btn:hover{border-color:var(--gold)}.btn.hot{background:linear-gradient(#ffd75e,#f5a300);color:#2a1260;border-color:#fff3}
.btn:disabled{opacity:.45;cursor:not-allowed}
.stat{opacity:.85;margin-bottom:6px;text-align:center}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:10px;width:min(900px,100%)}
.card{background:var(--card);border-radius:14px;padding:10px;text-align:center;border:2px solid transparent}.card.sel{border-color:var(--gold)}.card.lock{opacity:.35}
.card canvas{width:64px;height:64px}
#wheelBox{position:relative;width:min(560px,92vw,62vh)}#wheel{width:100%;display:block;filter:drop-shadow(0 0 24px #9b5cffaa)}
#ptr{position:absolute;left:50%;top:-6px;transform:translateX(-50%);width:0;height:0;border:16px solid transparent;border-top:34px solid var(--gold);filter:drop-shadow(0 0 10px var(--gold))}
#modal{position:absolute;inset:0;background:#000b;display:none;align-items:center;justify-content:center;flex-direction:column;gap:12px;z-index:9;text-align:center}
#modal.on{display:flex}#modal h1{font-size:clamp(34px,8vw,72px);color:var(--gold);text-shadow:0 0 30px var(--vio)}
#hud{position:absolute;inset:0;pointer-events:none;display:none}#hud.on{display:block}
#hud div{position:absolute;text-shadow:0 2px 4px #000}
#cross{left:50%;top:50%;width:10px;height:10px;margin:-5px;border:2px solid #fff;border-radius:50%}
#gl{position:absolute;inset:0;display:none}
.bar{height:24px;background:#000a;border-radius:8px;overflow:hidden;width:min(280px,46vw);margin:4px 0;position:relative;border:2px solid #fff4}.bar b{position:absolute;inset:0;text-align:center;font-size:14px;line-height:20px;text-shadow:0 1px 2px #000}#hp{font-size:18px}
.tb{position:absolute;border:2px solid #fff7;border-radius:50%;background:#2a126088;color:#fff;font:800 11px Nunito,system-ui,sans-serif;padding:0;display:flex;align-items:center;justify-content:center;touch-action:none;-webkit-user-select:none;user-select:none}
@media(max-width:700px){.btn{font-size:15px;padding:8px 11px}.grid{grid-template-columns:repeat(auto-fill,minmax(92px,1fr))}.card canvas{width:52px;height:52px}}
@media(pointer:coarse){#hud>div:last-child{display:none}#hud #wp{left:16px!important;right:auto!important;top:48px!important;bottom:auto!important;text-align:left!important}#mini{right:auto!important;left:16px!important;top:150px!important;width:100px;height:100px}}.bar i{display:block;height:100%}input{font:inherit;padding:10px;border-radius:10px;border:2px solid #fff3;background:#0006;color:inherit;margin:4px;width:min(260px,80vw)}
</style></head><body>

<div class='scr on' id='login'><h1 style='font-size:clamp(40px,9vw,84px);color:var(--gold);text-shadow:0 0 30px var(--vio)'>SKYFALL ROYALE</h1><p class='stat'>Melde dich an, um zu spielen</p><input id='lu' placeholder='Benutzername' autocomplete='username'><input id='lp' type='password' placeholder='Passwort' autocomplete='current-password'><div><button class='btn hot' onclick='auth(0)'>ANMELDEN</button> <button class='btn' onclick='auth(1)'>REGISTRIEREN</button></div><div id='lmsg' class='stat'></div><p class='stat' style='max-width:420px;font-size:13px'>Konten und Fortschritt werden lokal in diesem Browser gespeichert (kein Server).</p></div><div class="scr" id="menu">
<h1 style="font-size:clamp(40px,9vw,84px);color:var(--gold);text-shadow:0 0 30px var(--vio)">SKYFALL ROYALE</h1>
<div class="stat">Angemeldet als <b id="pname"></b></div><div class="stat" id="pstat"></div>
<nav><button class="btn hot" data-go="play">PLAY</button><button class="btn" data-go="wheel">SKIN WHEEL</button><button class="btn" data-go="locker">LOCKER</button><button class="btn" data-go="shop">ITEM SHOP</button><button class="btn" data-go="pass">BATTLE PASS</button><button class="btn" data-go="friends">FREUNDE</button><button class="btn" data-go="set">SETTINGS</button><button class="btn" onclick="KEY='';location.reload()">LOGOUT</button></nav>
<div id="panel" style="width:min(900px,100%);text-align:center"></div>
</div>

<div class="scr" id="wheelScr"><h2 style="font-size:36px">Daily Skin Wheel</h2>
<div id="wheelBox"><canvas id="wheel" width="800" height="800"></canvas><div id="ptr"></div></div>
<button class="btn hot" id="spin" style="margin:14px">DAILY FREE SPIN</button><div id="cd" class="stat"></div>
<button class="btn" onclick="show('menu')">Back</button></div>

<canvas id="gl"></canvas>
<div id="hud"><div id="cross"></div><canvas id="mini" width="140" height="140" style="position:absolute;right:16px;top:100px;border-radius:50%;border:3px solid #ffc93c;background:#2a8fd6"></canvas>
<div style="left:16px;bottom:16px"><div id="hp"></div><div class="bar"><i id="hpb" style="background:#4cff7a"></i><b id="hpt"></b></div><div class="bar"><i id="shb" style="background:#4cc3ff"></i><b id="sht"></b></div><div id="mats"></div></div>
<div style="right:16px;bottom:16px;text-align:right" id="wp"></div>
<div style="right:16px;top:12px;text-align:right" id="info"></div>
<div style="left:16px;top:12px;font-size:13px;opacity:.8">WASD · Shift sprint · Space jump · Maus schiessen · 1-3 Waffe · H heilen · E sammeln · Z/X/C/V Wand/Boden/Treppe/Dach · G Material · Esc Ende</div></div>

<div id="modal"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
/* ---------- Save ---------- */
let KEY='';const DEF=()=>({own:[],skin:-1,lastSpin:0,xp:0,coins:100,wins:0,kills:0,games:0,claimed:0,vol:.5,sens:1,shop:{},picks:['basic'],pick:'basic'});let S=DEF();
const save=()=>{if(!KEY)return;try{localStorage.setItem(KEY,JSON.stringify(S))}catch(e){}};
const lvl=()=>1+Math.floor(S.xp/50);
async function H(s){const b=await crypto.subtle.digest('SHA-256',new TextEncoder().encode('sky|'+s));return [...new Uint8Array(b)].map(x=>x.toString(16).padStart(2,'0')).join('')}
const ACC=()=>{try{return JSON.parse(localStorage.getItem('sky_acc')||'{}')}catch(e){return{}}};
async function auth(reg){const u=document.getElementById('lu').value.trim().toLowerCase(),p=document.getElementById('lp').value,m=document.getElementById('lmsg');if(u.length<3||p.length<4){m.textContent='Name min. 3 und Passwort min. 4 Zeichen.';return}
 const A=ACC(),h=await H(u+p);if(reg){if(A[u]){m.textContent='Name bereits vergeben.';return}A[u]=h;try{localStorage.setItem('sky_acc',JSON.stringify(A))}catch(e){}}else if(A[u]!==h){m.textContent='Name oder Passwort falsch.';return}
 KEY='sky_save_'+u;S=DEF();try{Object.assign(S,JSON.parse(localStorage.getItem(KEY)||'{}'))}catch(e){}save();document.getElementById('pname').textContent=u;show('menu');syncPresence()}

/* ---------- 25 original skins ---------- */
const SK=[["Banana Buddy","#ffe14a","#8a5a00"],["Crimson Raider","#c4262e","#222"],["Golden Touch","#ffcf3a","#fff6c8"],["Fin Crisp","#e9a15b","#5bc0e9"],["Stage Rocket","#6b3b1f","#ff7a1a"],["Kick Queen","#2f6fe0","#fff"],["Web Runner","#d6202f","#1d3a9e"],["Starlight Mage","#7a4cff","#ffd1f5"],["Iron Knight","#555b66","#cbd2de"],["Bone Trooper","#eee6d2","#222"],["Ghost Trooper","#7fffd0","#1a4d3d"],["Fox Drifter","#ff7a3c","#fff"],["Pop Idol","#ff7ac8","#fff"],["Cat Brawler","#b48a5a","#333"],["Agent Gray","#2b2b33","#e6e6e6"],["Night Prowler","#1c1c2e","#c9a0ff"],["Pop Diva","#f4c6ff","#c05cff"],["Merc Red","#b3121c","#111"],["Sea Siren","#2ec4c4","#a6ffe9"],["Wild Cat","#e8b04a","#5a3a00"],["Jester Girl","#e5233f","#2a6bff"],["Mega Heroes","#2a5cff","#ffd23a"],["Focus Monk","#f08a2c","#fff1d1"],["Wave Witch","#2a7bd6","#e1f2ff"],["Galaxy","#2a1a6e","#ff6bf2"],["Dijar","#a50044","#004d98"],["Neon Ninja","#1a1a2e","#39ff88"],["Pixel Pirate","#8a3b1c","#ffd23a"],["Lava Lord","#ff4d1a","#2a0a00"],["Frost Giant","#bfe8ff","#2a6bd6"],["Cyber Samurai","#1f1f3a","#ff2a6d"],["Jungle Ranger","#3a7a2a","#e8d9a0"],["Sunset Surfer","#ff9a5a","#2ec4c4"],["Void Walker","#120a2a","#b45cff"]].map((a,i)=>({n:a[0],c1:a[1],c2:a[2],rare:i>=25||[2,4,5,6,7,15,16,24].includes(i)}));
function icon(i,sz=64){const c=document.createElement('canvas');c.width=c.height=sz;const g=c.getContext('2d'),k=SK[i],s=sz/64;
 g.fillStyle=k.c1;g.fillRect(18*s,30*s,28*s,30*s);if(i===25){for(let x=0;x<7;x++){g.fillStyle=x%2?'#004d98':'#a50044';g.fillRect((18+x*4)*s,30*s,4*s,16*s)}g.fillStyle='#2f5fb5';g.fillRect(18*s,46*s,28*s,14*s);g.fillStyle='#fff';g.fillRect(18*s,58*s,12*s,4*s);g.fillRect(34*s,58*s,12*s,4*s)}g.fillStyle=k.c2;g.fillRect(18*s,44*s,28*s,6*s);
 g.beginPath();g.arc(32*s,20*s,13*s,0,7);g.fillStyle='#ffd9b0';g.fill();g.fillStyle=k.c2;g.fillRect(19*s,6*s,26*s,(6+i%4*2)*s);
 g.fillStyle='#222';g.fillRect(27*s,19*s,3*s,4*s);g.fillRect(35*s,19*s,3*s,4*s);return c}

/* ---------- Audio ---------- */
let AC;function snd(f,d=.08,t='square',v=.2){try{AC=AC||new AudioContext();const o=AC.createOscillator(),g=AC.createGain();o.type=t;o.frequency.value=f;g.gain.value=v*S.vol;g.gain.exponentialRampToValueAtTime(.001,AC.currentTime+d);o.connect(g);g.connect(AC.destination);o.start();o.stop(AC.currentTime+d)}catch(e){}}

/* ---------- Navigation / panels ---------- */
const $=id=>document.getElementById(id);
function show(id){document.querySelectorAll('.scr').forEach(e=>e.classList.remove('on'));$(id).classList.add('on');if(id==='menu')stats()}
function stats(){$('pstat').textContent=`Level ${lvl()} · ${S.xp%50}/50 XP · ${S.coins} Coins · ${S.wins} Siege · ${S.kills} Eliminierungen · ${S.own.length}/34 Skins · Token ${S.tokens||0}`}
document.querySelectorAll('[data-go]').forEach(b=>b.onclick=()=>{snd(500);go(b.dataset.go)});
function skinGrid(list,fn,sel){const w=document.createElement('div');w.className='grid';list.forEach(i=>{const d=document.createElement('div');const own=S.own.includes(i);d.className='card'+(sel===i?' sel':'')+(own||fn.shop?'':' lock');d.append(icon(i),document.createTextNode(SK[i].n));d.onclick=()=>fn(i);w.append(d)});return w}
function go(p){const P=$('panel');P.innerHTML='';if(p==='shop'){shopUI(P);return}if(p==='pass'){passUI(P);return}if(p==='locker'){lockerUI(P);return}if(p==='friends'){friendsUI(P);return}if(p==='play'){playUI(P);return}
 if(p==='wheel'){show('wheelScr');drawWheel();tick();return}
 if(p==='play'){const m=document.createElement('div');m.innerHTML='<h2>Modus</h2>';if(ONL){[['Online mit Freunden',PARTY()],['Öffentliche Arena','arena']].forEach(([n,r])=>{const b=document.createElement('button');b.className='btn hot';b.style.margin='8px';b.textContent='🌐 '+n;b.onclick=()=>startGame('Online',r);m.append(b)});m.insertAdjacentHTML('beforeend','<p class="stat">Online: Spieler im selben Raum sehen und treffen sich. KI-Gegner füllen die Runde auf.</p>')}['Solo','Duo','Squad'].forEach(n=>{const b=document.createElement('button');b.className='btn hot';b.style.margin='8px';b.textContent=n;b.onclick=()=>startGame(n);m.append(b)});m.insertAdjacentHTML('beforeend','<p class="stat">Duo/Squad: KI-Teammates folgen dir. Dieses Spiel läuft offline mit 24 KI-Gegnern (Prototyp, keine Online-Server).</p>');P.append(m)}
 if(p==='locker'){P.insertAdjacentHTML('beforeend','<h2>Locker – Skin wählen</h2>');P.append(skinGrid(S.own,i=>{S.skin=i;save();go('locker')},S.skin));if(!S.own.length)P.insertAdjacentHTML('beforeend','<p class="stat">Noch keine Skins. Dreh das Skin Wheel!</p>')}
 if(p==='shop'){const day=new Date().toDateString();if(S.shop.day!==day){const pool=[...Array(25).keys()].filter(i=>!S.own.includes(i)).sort(()=>Math.random()-.5);S.shop={day,items:pool.slice(0,4)};save()}
  P.insertAdjacentHTML('beforeend','<h2>Item Shop – heute (300 Coins)</h2>');const g=skinGrid(S.shop.items.filter(i=>!S.own.includes(i)),i=>{if(S.coins<300)return snd(120,.2);S.coins-=300;S.own.push(i);save();stats();go('shop')},-2);g.firstChild&&0;P.append(g)}
 if(p==='pass'){P.insertAdjacentHTML('beforeend','<h2>Battle Pass</h2><p class="stat">Jede Stufe = 100 XP. Belohnung: 150 Coins.</p>');const g=document.createElement('div');g.className='grid';for(let t=1;t<=10;t++){const d=document.createElement('div');d.className='card'+(t<lvl()?'':' lock');d.innerHTML=`Stufe ${t}<br>${t<=S.claimed?'✔ geholt':'150 Coins'}`;d.onclick=()=>{if(t===S.claimed+1&&t<lvl()){S.claimed=t;S.coins+=150;save();stats();go('pass')}};g.append(d)}P.append(g)}
 if(p==='set'){P.innerHTML=`<h2>Settings</h2><p>Lautstärke <input type=range min=0 max=1 step=.1 value=${S.vol} oninput="S.vol=+this.value;save()"></p><p>Maus-Empfindlichkeit <input type=range min=.3 max=2 step=.1 value=${S.sens} oninput="S.sens=+this.value;save()"></p><button class=btn onclick="if(confirm('Alles löschen?')){localStorage.removeItem(KEY);location.reload()}">Fortschritt zurücksetzen</button>`}}

/* ---------- Wheel ---------- */
const wc=$('wheel'),wg=wc.getContext('2d'),N=25,SEG=Math.PI*2/N;let rot=0,spinning=false;
function drawWheel(){const c=400;wg.clearRect(0,0,800,800);
 for(let i=0;i<N;i++){const a=rot+i*SEG,k=SK[i],own=S.own.includes(i);
  wg.beginPath();wg.moveTo(c,c);wg.arc(c,c,380,a,a+SEG);wg.closePath();wg.fillStyle=k.c1;wg.globalAlpha=own?.35:1;wg.fill();wg.globalAlpha=1;
  wg.strokeStyle=k.rare?'#ffc93c':'#ffffff66';wg.lineWidth=k.rare?5:2;wg.stroke();
  wg.save();wg.translate(c,c);wg.rotate(a+SEG/2);wg.drawImage(icon(i,64),235,-24,48,48);
  wg.fillStyle=k.c1.match(/^#(f|e|d|c)/i)?'#222':'#fff';wg.font='bold 17px Nunito,sans-serif';wg.textAlign='right';wg.fillText(k.n+(own?' ✔':''),352,6);wg.restore()}
 wg.beginPath();wg.arc(c,c,56,0,7);wg.fillStyle='#2a1260';wg.fill();wg.lineWidth=8;wg.strokeStyle='#ffc93c';wg.stroke();
 wg.beginPath();wg.arc(c,c,386,0,7);wg.lineWidth=12;wg.strokeStyle='#9b5cff';wg.stroke()}
function rnd(n){const a=new Uint32Array(1);let m=Math.floor(2**32/n)*n,x;do{crypto.getRandomValues(a);x=a[0]}while(x>=m);return x%n}
function left(){return Math.max(0,S.lastSpin+864e5-Date.now())}
function tick(){const l=left();$('spin').disabled=spinning||l>0;$('cd').textContent=S.own.filter(i=>i<25).length>=25?'Alle 25 Skins freigeschaltet!':l>0?'Nächster Spin in '+new Date(l).toISOString().substr(11,8):'Dein Spin ist bereit!';
 if($('wheelScr').classList.contains('on'))setTimeout(tick,500)}
$('spin').onclick=()=>{if(spinning||left()>0)return;const pool=[...Array(N).keys()].filter(i=>!S.own.includes(i));
 if(!pool.length){return}
 const win=pool[rnd(pool.length)],tok=tokenRoll();S.lastSpin=Date.now();S.own.push(win);if(S.skin<0)S.skin=win;save();spinning=true;tick();
 const base=-Math.PI/2-(win+.5)*SEG,d=(((rot-base)%(2*Math.PI))+2*Math.PI)%(2*Math.PI)+2*Math.PI*7,r0=rot,end=r0-d,t0=performance.now(),T=7000;let last=-1;
 (function f(t){const p=Math.min(1,(t-t0)/T),e=1-Math.pow(1-p,4);rot=r0+(end-r0)*e;drawWheel();
  const idx=Math.floor((((-Math.PI/2-rot)%(2*Math.PI))+2*Math.PI)%(2*Math.PI)/SEG);if(idx!==last){last=idx;snd(300+p*0,.04,'triangle',.25)}
  if(p<1)requestAnimationFrame(f);else{spinning=false;snd(880,.4,'sine');snd(1320,.6,'sine');tick();win_modal(win);if(tok)tokenWin()}})(t0)};
function win_modal(i){const all=S.own.filter(i=>i<25).length>=25,m=$('modal');m.innerHTML=`<h1>${all?'ALLE 25 SKINS!':'NEUER SKIN!'}</h1><div id="wi"></div><h2 style="font-size:34px">${SK[i].n}</h2>${all?'<p>Sammlung komplett – du bist eine Legende!</p>':''}<button class="btn hot" onclick="$('modal').classList.remove('on')">Super!</button>`;$('wi').append(icon(i,200));m.classList.add('on')}

/* ---------- 3D game ---------- */
let G=null;
function crest(x,cx,cy,r){x.save();x.translate(cx,cy);x.beginPath();x.moveTo(-r,-r);x.lineTo(r,-r);x.lineTo(r,r*.3);x.quadraticCurveTo(r,r,0,r*1.3);x.quadraticCurveTo(-r,r,-r,r*.3);x.closePath();x.fillStyle='#fff';x.fill();x.clip();x.fillStyle='#004d98';x.fillRect(-r,-r*.2,r,r*2);x.fillStyle='#a50044';x.fillRect(0,-r*.2,r,r*2);x.fillStyle='#ffd23a';x.fillRect(-r,-r,r*2,r*.35);x.restore()}
function stripe(w,h,n,cr){const c=document.createElement('canvas');c.width=w;c.height=h;const x=c.getContext('2d');for(let i=0;i<n;i++){x.fillStyle=i%2?'#004d98':'#a50044';x.fillRect(i*w/n,0,w/n+1,h)}for(let i=0;i<cr;i++)crest(x,(i+.5)*w/cr,h/2-2,h*.26);return new THREE.CanvasTexture(c)}
function dijar(g,M){const T=stripe(128,64,8,0),L=c=>new THREE.MeshLambertMaterial(c);
 const b=new THREE.Mesh(new THREE.CylinderGeometry(.45,.5,.9,16),L({map:T}));b.position.y=1.15;
 const cc=document.createElement('canvas');cc.width=cc.height=64;const y=cc.getContext('2d');crest(y,32,26,17);y.fillStyle='#fff';y.font='bold 12px sans-serif';y.textAlign='center';y.fillText('26/27',32,60);
 const pl=new THREE.Mesh(new THREE.PlaneGeometry(.4,.4),new THREE.MeshBasicMaterial({map:new THREE.CanvasTexture(cc),transparent:true}));pl.position.set(0,1.2,.53);
 [-.2,.2].forEach(px=>{const l=new THREE.Mesh(new THREE.BoxGeometry(.32,.7,.34),M('#2f5fb5'));l.position.set(px,.4,0);const s=new THREE.Mesh(new THREE.BoxGeometry(.36,.16,.52),M('#ffffff'));s.position.set(px,.08,.07);const st=new THREE.Mesh(new THREE.BoxGeometry(.37,.04,.53),M('#2a6bd6'));st.position.set(px,.12,.07);g.add(l,s,st)});
 [-.58,.58].forEach(px=>{const a=new THREE.Mesh(new THREE.BoxGeometry(.2,.5,.22),M('#ffd9b0'));a.position.set(px,1.2,0);const sl=new THREE.Mesh(new THREE.BoxGeometry(.24,.2,.26),L({map:T}));sl.position.set(px,1.45,0);g.add(a,sl)});
 const h=new THREE.Mesh(new THREE.SphereGeometry(.34,14,12),M('#ffd9b0'));h.position.y=1.85;
 const side=new THREE.Mesh(new THREE.SphereGeometry(.355,14,10,0,6.3,0,1.45),M('#4a3a2e'));side.position.y=1.86;
 const top=new THREE.Mesh(new THREE.SphereGeometry(.36,14,10,0,6.3,0,1.0),M('#241810'));top.position.y=1.9;top.scale.y=1.25;
 g.add(b,pl,h,side,top);for(let i=0;i<6;i++){const f=new THREE.Mesh(new THREE.BoxGeometry(.1,.14,.12),M('#241810'));f.position.set(-.22+i*.088,2.06-(i%2)*.03,.3);f.rotation.set(.5,0,(i%3-1)*.4);g.add(f)}return g}
function pickMesh(t){const g=new THREE.Group(),M=c=>new THREE.MeshLambertMaterial({color:c});
 g.add(new THREE.Mesh(new THREE.CylinderGeometry(.05,.05,1.3,8),M('#7a4a22')));
 const hd=new THREE.Mesh(new THREE.BoxGeometry(.9,.12,.1),M('#9aa3b0'));hd.position.y=.62;g.add(hd);
 [-1,1].forEach(s=>{const p=new THREE.Mesh(new THREE.ConeGeometry(.07,.25,6),M('#c9d2e0'));p.position.set(s*.52,.62,0);p.rotation.z=-s*Math.PI/2;g.add(p)});
 if(t==='barca'){const T=stripe(256,64,16,4);for(let i=0;i<7;i++){const r=new THREE.Mesh(new THREE.TorusGeometry(.085,.04,6,16),new THREE.MeshLambertMaterial({map:T}));r.position.y=-.3+i*.09;r.rotation.x=1.2+(i%2)*.2;g.add(r)}
  const tl=new THREE.Mesh(new THREE.BoxGeometry(.16,.55,.02),new THREE.MeshLambertMaterial({map:stripe(64,64,4,1),side:2}));tl.position.set(.1,-.6,.06);tl.rotation.z=.15;g.add(tl)}
 return g}
let LOBBY=null,USER=null,DB=null,MYID=null,PEERS=[],FR=[],ONL=false,ONLPANEL=null;
const ME=()=>document.getElementById('pname').textContent||'Spieler';
const PARTY=()=>'p'+String(MYID||'x').replace(/[^a-z0-9]/gi,'').toLowerCase().slice(0,14);
function syncPresence(){try{if(LOBBY)LOBBY.presence({name:ME(),skin:S.skin})}catch(e){}}
async function onlineInit(){try{USER=await claude.use('user');LOBBY=await claude.use('room');DB=await claude.use('db')}catch(e){}
 if(!USER||!LOBBY)return;ONL=true;try{MYID=await USER.id()}catch(e){}
 LOBBY.onPeers(c=>{PEERS=c.peers;if(ONLPANEL)ONLPANEL()});
 LOBBY.on('invite',m=>{if(G||!m.data||m.data.to!==MYID||m.isMe)return;const md=document.getElementById('modal');md.innerHTML='<h2>'+String(m.data.from||'Ein Freund').replace(/</g,'&lt;')+' lädt dich zu einem Online-Match ein!</h2><div><button class="btn hot" id="inY">Beitreten</button> <button class="btn" id="inN">Nein</button></div>';md.classList.add('on');document.getElementById('inN').onclick=()=>md.classList.remove('on');document.getElementById('inY').onclick=()=>{md.classList.remove('on');startGame('Online',String(m.data.room))}});
 syncPresence();if(DB&&MYID){try{const d=await DB.doc('data/users/'+MYID+'/social').get();if(d.exists)FR=d.data().friends||[]}catch(e){}}}
async function saveFr(){try{await DB.doc('data/users/'+MYID+'/social').set({friends:FR})}catch(e){}}
async function addFriend(id){if(!FR.includes(id)){FR.push(id);await saveFr()}renderFriends()}
async function renderFriends(){const L=document.getElementById('flist');if(!L)return;L.textContent='';if(!FR.length){L.textContent='Noch keine Freunde – such oben nach einem Namen.';return}
 let ps={};try{ps=await USER.profiles(FR)}catch(e){}
 L.textContent='';FR.forEach(id=>{const on=PEERS.find(p=>p.by===id&&!p.isMe),d=document.createElement('div');d.className='card';d.style.cssText='margin:6px auto;max-width:440px';d.append(document.createTextNode((on?'🟢 ':'⚪ ')+((ps[id]&&ps[id].name)||'Freund')+(on&&on.presence.name?' ('+on.presence.name+')':'')+' '));
  if(on){const b=document.createElement('button');b.className='btn';b.textContent='Einladen';b.onclick=()=>{LOBBY.emit('invite',{to:id,room:PARTY(),from:ME()});b.textContent='Gesendet';startGame('Online',PARTY())};d.append(b,' ')}
  const r=document.createElement('button');r.className='btn';r.textContent='✕';r.onclick=async()=>{FR=FR.filter(x=>x!==id);await saveFr();renderFriends()};d.append(r);L.append(d)})}
function friendsUI(P){P.innerHTML='<h2>Freunde</h2>';
 if(!ONL){P.insertAdjacentHTML('beforeend','<p class="stat">Online-Funktionen gibt es nur, wenn du in claude.ai angemeldet bist und diese Seite dort geöffnet hast (Mitglieder der Organisation oder eingeladene Gäste).</p>');return}
 ONLPANEL=renderFriends;P.insertAdjacentHTML('beforeend','<p class="stat">Freund suchen und hinzufügen:</p><input id="fq" placeholder="Name suchen"><div id="fres"></div><h3 style="margin-top:12px">Meine Freunde</h3><div id="flist"></div>');
 let tm;document.getElementById('fq').oninput=e=>{clearTimeout(tm);tm=setTimeout(async()=>{const q=e.target.value.trim(),r=document.getElementById('fres');r.textContent='';if(!q)return;try{(await USER.search(q)).filter(p=>p.id!==MYID).slice(0,6).forEach(p=>{const b=document.createElement('button');b.className='btn';b.textContent='+ '+(p.name||'Spieler');b.onclick=()=>addFriend(p.id);r.append(b)})}catch(e){r.textContent='Suche nicht verfügbar'}},300)};renderFriends()}
const panelEl=()=>document.getElementById('panel');
function tokenRoll(){if(rnd(100000)===0){S.tokens=(S.tokens||0)+1;save();return true}return false}
function tokenWin(){const m=document.getElementById('modal');m.insertAdjacentHTML('beforeend',"<h1 style='font-size:36px'>🎟️ TOKEN GEFUNDEN! (0,001 %)</h1><p>Du darfst dir 10 Skins frei aussuchen.</p><button class='btn hot' onclick='redeemToken()'>Token einlösen</button>");m.classList.add('on');snd(1200,.6,'sine')}
function redeemToken(){document.getElementById('modal').classList.remove('on');if(G){if(G.net)G.net.leave();G.R.dispose();G=null;document.getElementById('gl').style.display='none';document.getElementById('hud').classList.remove('on');const tc=document.getElementById('tc');if(tc)tc.remove()}show('menu');tokenUI(panelEl())}
function tokenUI(P,sel){sel=sel||[];P.innerHTML='<h2>Token: Wähle 10 Skins ('+sel.length+'/10)</h2>';const w=document.createElement('div');w.className='grid';
 for(let i=0;i<SK.length;i++){if(S.own.includes(i))continue;const d=document.createElement('div');d.className='card'+(sel.includes(i)?' sel':'');d.append(icon(i),document.createTextNode(SK[i].n));d.onclick=()=>{if(sel.includes(i))sel.splice(sel.indexOf(i),1);else if(sel.length<10)sel.push(i);tokenUI(P,sel)};w.append(d)}
 P.append(w);const b=document.createElement('button');b.className='btn hot';b.style.margin='12px';const need=Math.min(10,SK.length-S.own.length);b.textContent='Bestätigen';b.disabled=sel.length<need;b.onclick=()=>{sel.forEach(i=>S.own.push(i));S.tokens=Math.max(0,(S.tokens||1)-1);save();stats();lockerUI(P)};P.append(b)}
const TOUCH=('ontouchstart' in window)||matchMedia('(pointer:coarse)').matches;let JS={x:0,y:0,id:null,ox:0,oy:0},LK={id:null,x:0,y:0};
function healNow(){if(!G)return;const P=G.P;if(P.heal>0&&P.hp<100){P.heal--;P.hp=Math.min(100,P.hp+40);snd(700,.2,'sine')}}
function touchInit(){if(!TOUCH||document.getElementById('tc'))return;const t=document.createElement('div');t.id='tc';t.style.cssText='position:absolute;inset:0;touch-action:none;z-index:5';document.body.append(t);JS={x:0,y:0,id:null,ox:0,oy:0};LK={id:null,x:0,y:0};
 t.addEventListener('touchstart',e=>{for(const c of e.changedTouches){if(c.target!==t)continue;if(c.clientX<innerWidth/2&&JS.id==null){JS.id=c.identifier;JS.ox=c.clientX;JS.oy=c.clientY}else if(LK.id==null){LK.id=c.identifier;LK.x=c.clientX;LK.y=c.clientY}}e.preventDefault()},{passive:false});
 t.addEventListener('touchmove',e=>{for(const c of e.changedTouches){if(c.identifier===JS.id){JS.x=Math.max(-1,Math.min(1,(c.clientX-JS.ox)/50));JS.y=Math.max(-1,Math.min(1,(c.clientY-JS.oy)/50))}else if(c.identifier===LK.id&&G){G.P.yaw-=(c.clientX-LK.x)*.006*S.sens;G.P.pitch=Math.max(-.6,Math.min(1,G.P.pitch+(c.clientY-LK.y)*.006*S.sens));LK.x=c.clientX;LK.y=c.clientY}}e.preventDefault()},{passive:false});
 const end=e=>{for(const c of e.changedTouches){if(c.identifier===JS.id){JS.id=null;JS.x=JS.y=0}if(c.identifier===LK.id)LK.id=null}e.preventDefault()};t.addEventListener('touchend',end,{passive:false});t.addEventListener('touchcancel',end,{passive:false});
 const B=(txt,pos,sz,dn,up)=>{const b=document.createElement('button');b.textContent=txt;b.className='tb';b.style.cssText=pos+';width:'+sz+'px;height:'+sz+'px';const d=e=>{e.preventDefault();e.stopPropagation();dn()},u=e=>{e.preventDefault();e.stopPropagation();if(up)up()};b.addEventListener('touchstart',d,{passive:false});b.addEventListener('touchend',u,{passive:false});b.addEventListener('touchcancel',u,{passive:false});t.append(b)};
 B('FEUER','right:16px;bottom:40px;background:#e5393577',88,()=>{if(G)G.fire=1},()=>{if(G)G.fire=0});
 B('SPRUNG','right:116px;bottom:40px',64,()=>{if(G)G.keys.Space=1},()=>{if(G)G.keys.Space=0});
 B('Waffe','right:116px;bottom:114px',56,()=>{if(G){let n=G.P.w;for(let k=0;k<4;k++){n=(n+1)%4;if(WEAP[n]){G.P.w=n;break}}}});
 B('Heilen','right:190px;bottom:40px',56,healNow);
 B('Sammeln','right:190px;bottom:104px',56,()=>{if(G)harvest()});
 B('Sprint','right:190px;bottom:168px',56,()=>{if(G)G.keys.ShiftLeft=!G.keys.ShiftLeft});
 (OPT.build?[['Wand','Z'],['Boden','X'],['Treppe','C'],['Dach','V']]:[]).forEach(([n,k],i)=>B(n,'right:16px;top:'+(150+i*54)+'px',46,()=>{if(G)place(k)}));
 if(OPT.build)B('Mat.','right:16px;top:366px',46,()=>{if(G)G.P.mat={wood:'stone',stone:'metal',metal:'wood'}[G.P.mat]});
 B('Ende','left:16px;top:100px',46,()=>endGame(false))}
function human(i,g,M){const k=SK[i],sk=['#ffd9b0','#e8b58a','#c68642','#8d5524','#f1c27d'][i%5],hc=['#2a1a10','#6b3b1f','#e8c46a','#111','#a33a1c'][(i*3)%5],B=(w,h,d,c,x,y,z)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),M(c));m.position.set(x,y,z);g.add(m);return m};
 B(.72,.85,.38,k.c1,0,1.35,0);B(.74,.14,.4,k.c2,0,.93,0);
 [-.18,.18].forEach(x=>{B(.32,.8,.34,k.c2,x,.5,0);B(.34,.14,.5,'#222',x,.07,.06)});
 [-.5,.5].forEach(x=>{B(.22,.72,.24,k.c1,x,1.32,0);B(.2,.2,.22,sk,x,.88,0)});
 B(.2,.14,.2,sk,0,1.82,0);B(.5,.5,.46,sk,0,2.1,0);B(.08,.08,.02,'#111',-.11,2.12,.24);B(.08,.08,.02,'#111',.11,2.12,.24);B(.14,.03,.02,'#a0524a',0,1.97,.24);
 const st=i%4;if(st===0){B(.54,.14,.5,hc,0,2.38,-.01);B(.54,.3,.1,hc,0,2.25,-.2)}else if(st===1){B(.54,.14,.5,hc,0,2.38,0);B(.54,.6,.12,hc,0,2.1,-.22);B(.1,.5,.4,hc,-.28,2.1,-.05);B(.1,.5,.4,hc,.28,2.1,-.05)}else if(st===2){B(.56,.16,.52,k.c2,0,2.38,0);B(.5,.05,.3,k.c2,0,2.34,.34)}else{B(.56,.34,.52,k.c2,0,2.32,0)}
 return g}
function dmgPop(p,d,hs){if(!G)return;const v=new THREE.Vector3(p.x,p.y+2.5,p.z).project(G.cam);if(v.z>1)return;const e=document.createElement('div');e.textContent=hs?d+' KOPF!':d;e.style.cssText='left:'+((v.x+1)/2*innerWidth)+'px;top:'+((1-v.y)/2*innerHeight)+'px;font:'+(hs?34:26)+'px Lilita One,Impact,sans-serif;color:'+(hs?'#ff4040':'#ffd23a')+';text-shadow:0 2px 4px #000,0 0 8px #f00;transition:all .7s ease-out;opacity:1;transform:translate(-50%,0)';document.getElementById('hud').append(e);setTimeout(()=>{e.style.top=(parseFloat(e.style.top)-70)+'px';e.style.opacity='0'},20);setTimeout(()=>e.remove(),800)}
function spawnBullet(a,b,col){if(!G)return;const d=new THREE.Vector3().subVectors(b,a),L=Math.max(.1,Math.hypot(d.x,d.y,d.z)),dir=new THREE.Vector3(d.x/L,d.y/L,d.z/L),m=new THREE.Mesh(new THREE.BoxGeometry(.08,.08,2.4),new THREE.MeshBasicMaterial({color:col}));m.position.copy(a);m.lookAt(b);G.sc.add(m);(G.fx=G.fx||[]).push({m,dir,left:L})}
function fireFx(o,cd,h,fx,fz,P){const st=new THREE.Vector3(P.pos.x+fx*.9,P.pos.y+1.5,P.pos.z+fz*.9),col=WEAP[P.w].col,n=WEAP[P.w].pel||1;let dd=WEAP[P.w].t==='sniper'?200:120;if(h)dd=Math.max(4,new THREE.Vector3().subVectors(h.m.position,o).dot(cd));
 for(let i=0;i<n;i++){const e=o.clone().addScaledVector(cd,dd);if(n>1){e.x+=(Math.random()-.5)*6;e.y+=(Math.random()-.5)*4;e.z+=(Math.random()-.5)*6}spawnBullet(st,e,col)}}
const OPT={build:true};let LASTHS=false;
const RAR=[['Grün','#4cff7a',1,1],['Blau','#4cc3ff',1.15,.93],['Lila','#b45cff',1.3,.9],['Gelb','#ffd23a',1.5,.85]];
const CAT=[['Sturmgewehr','ar',24,.11,1,1.3],['Kampfgewehr','ar',30,.15,1,1.4],['Burst-Gewehr','ar',27,.13,1,1.3],['Schweres Sturmgewehr','ar',38,.2,1,1.5],['MP','smg',16,.07,1,.9],['Kompakt-MP','smg',14,.06,1,.8],['Tactical-SMG','smg',18,.08,1,.9],['Pistole','pistol',22,.3,1,.6],['Revolver','pistol',55,.7,1,.7],['Handkanone','pistol',70,.9,1,.7],['Pump-Schrotflinte','shotgun',75,.95,5,1.1],['Tac-Schrotflinte','shotgun',55,.5,5,1],['Auto-Schrotflinte','shotgun',38,.3,5,1.1],['Scharfschützengewehr','sniper',110,1.5,1,1.8],['Jagdgewehr','sniper',90,1.1,1,1.7],['Bolt-Action','sniper',130,1.8,1,1.9]];
const mkW=(b,ri)=>{const R=RAR[ri];return{n:b[0],t:b[1],d:Math.round(b[2]*R[2]),r:b[3]*R[3],col:R[1],rar:R[0],pel:b[4]>1?b[4]:0,len:b[5]}};
function lootWeapon(){const q=Math.random(),ri=q<.5?0:q<.8?1:q<.95?2:3;return mkW(CAT[Math.floor(Math.random()*CAT.length)],ri)}
function toast(t,c){const e=document.createElement('div');e.textContent=t;e.style.cssText='left:50%;top:22%;transform:translate(-50%,0);font:30px Lilita One,Impact,sans-serif;color:'+c+';text-shadow:0 2px 6px #000;transition:all 1.2s;opacity:1;white-space:nowrap';document.getElementById('hud').append(e);setTimeout(()=>{e.style.top='14%';e.style.opacity='0'},900);setTimeout(()=>e.remove(),2200)}
function giveWeapon(P,w){let s=[0,1,2].find(i=>!WEAP[i]);if(s===undefined)s=P.w<3?P.w:0;WEAP[s]=w;P.w=s;toast(w.n+' · '+w.rar,w.col)}
function addMarker(mesh,team){const m=new THREE.Mesh(new THREE.ConeGeometry(.25,.5,4),new THREE.MeshBasicMaterial({color:team==='red'?'#ff3b3b':'#3b8bff'}));m.position.y=3;m.rotation.x=Math.PI;mesh.add(m)}
function botDie(b){if(!G)return;if(b.lives>1){b.lives--;b.hp=100;const s=G.team?(b.team==='red'?-1:1)*(20+Math.random()*100):(Math.random()-.5)*200;b.m.position.set(s,0,(Math.random()-.5)*200)}else{b.dead=true;G.sc.remove(b.m)}}
function shoot2(o,dir,w,tgt){const W=WEAP[w];let hit=null,hd=W.t==='sniper'?300:120;LASTHS=false;
 for(const t of tgt){if(t.dead)continue;const c=t.pos?t.pos:t.m.position,at=y=>{const v=new THREE.Vector3(c.x-o.x,c.y+y-o.y,c.z-o.z),s=v.dot(dir);if(s<0||s>hd)return null;return{s,d:o.clone().addScaledVector(dir,s).distanceTo(new THREE.Vector3(c.x,c.y+y,c.z))}};
  const hh=at(2.1),bb=at(1);if(hh&&hh.d<.45){hit=t;hd=hh.s;LASTHS=true}else if(bb&&bb.d<(W.t==='shotgun'?1.6:1.1)){hit=t;hd=bb.s;LASTHS=false}}return hit}
function loadoutPick(){if(!G)return;G.pause=true;const m=document.getElementById('modal');m.innerHTML='<h2>Wähle deine legendäre Waffe</h2>';const w=document.createElement('div');w.className='grid';w.style.cssText='width:min(640px,94vw)';
 [0,2,4,10,13,9].forEach(i=>{const x=mkW(CAT[i],3),d=document.createElement('div');d.className='card sel';d.style.cursor='pointer';d.innerHTML='<b style=color:#ffd23a>'+x.n+'</b><br>Schaden '+x.d+'<br>Gelb · Legendär';d.onclick=()=>{giveWeapon(G.P,x);G.pause=false;m.classList.remove('on')};w.append(d)});m.append(w);m.classList.add('on')}
function playUI(P){P.innerHTML='<h2>Spielmodus</h2>';const mk2=(n,mode,room)=>{const b=document.createElement('button');b.className='btn hot';b.style.margin='6px';b.textContent=n;b.onclick=()=>startGame(mode,room);P.append(b)};
 const bt=document.createElement('button');bt.className='btn';bt.style.margin='6px';const upd=()=>bt.textContent='Bauen: '+(OPT.build?'AN':'AUS');upd();bt.onclick=()=>{OPT.build=!OPT.build;upd()};P.append(bt,document.createElement('br'));
 [['Solo','Solo'],['Duo','Duo'],['Squad','Squad'],['Reload (3 Leben)','Reload'],['Rot vs Blau','Teams']].forEach(([n,m])=>mk2(n,m));
 if(ONL){P.insertAdjacentHTML('beforeend','<h3 style=margin-top:12px>Online</h3>');[['🌐 Mit Freunden','Online',PARTY()],['🌐 Öffentliche Arena','Online','arena'],['🌐 Rot vs Blau Online','Teams','tdm']].forEach(([n,m,r])=>mk2(n,m,r))}
 P.insertAdjacentHTML('beforeend','<p class=stat>Du startest ohne Waffen – öffne Truhen (E oder Spitzhacke). Kopfschüsse machen doppelten Schaden. Rot vs Blau: leere Arena, Team zufällig, legendäre Waffe zur Auswahl.</p>')}
const PRICE={26:500,27:500,28:800,29:800,30:1200,31:500,32:800,33:1200};
function shopUI(P){P.innerHTML='<h2>Item Shop</h2><p class="stat">Du hast '+S.coins+' Coins (Eliminierungen und Siege bringen Coins).</p>';const w=document.createElement('div');w.className='grid';
 Object.keys(PRICE).forEach(k=>{k=+k;const d=document.createElement('div'),own=S.own.includes(k);d.className='card'+(own?' sel':'');d.append(icon(k),document.createTextNode(SK[k].n),document.createElement('br'),document.createTextNode(own?'✔ im Besitz':PRICE[k]+' Coins'));
  d.onclick=()=>{if(own)return;if(S.coins<PRICE[k])return snd(120,.2);S.coins-=PRICE[k];S.own.push(k);save();stats();snd(900,.3,'sine');shopUI(P)};w.append(d)});P.append(w)}
function passUI(P){P.innerHTML='<h2>Battle Pass</h2><p class="stat">Level '+lvl()+' · 50 XP pro Level · Level 25: Blaugrana-Spitzhacke · Level 50: Skin Dijar</p>';const g=document.createElement('div');g.className='grid';
 for(let t=1;t<=50;t++){const d=document.createElement('div'),rw=t===25?'⛏️ Spitzhacke':t===50?'Skin: Dijar':(t%5?'100':'250')+' Coins';d.className='card'+(t<=S.claimed?' sel':t<=lvl()?'':' lock');if(t===25||t===50)d.style.background='linear-gradient(#a5004466,#004d9866)';
  d.innerHTML='Stufe '+t+'<br>'+(t<=S.claimed?'✔ geholt':rw);
  d.onclick=()=>{if(t!==S.claimed+1||t>lvl())return;S.claimed=t;if(t===25)S.picks.push('barca');else if(t===50)S.own.push(25);else S.coins+=t%5?100:250;save();stats();snd(900,.3,'sine');passUI(P)};g.append(d)}P.append(g)}
function lockerUI(P){P.innerHTML='<h2>Locker</h2>'+((S.tokens||0)>0?'<button class="btn hot" onclick="tokenUI(panelEl())">🎟️ Token einlösen: 10 Skins wählen</button>':'')+'<h3>Skins</h3>';P.append(skinGrid(S.own,i=>{S.skin=i;save();lockerUI(P)},S.skin));if(!S.own.length)P.insertAdjacentHTML('beforeend','<p class="stat">Noch keine Skins. Dreh das Skin Wheel!</p>');
 P.insertAdjacentHTML('beforeend','<h3 style="margin-top:14px">Spitzhacken</h3>');const w=document.createElement('div');w.className='grid';
 [['basic','Standard'],['barca','Blaugrana-Spitzhacke']].forEach(([id,n])=>{const has=S.picks.includes(id),d=document.createElement('div');d.className='card'+(S.pick===id?' sel':'')+(has?'':' lock');d.innerHTML='⛏️<br>'+n+(has?'':'<br>Battle Pass Lv25');d.onclick=()=>{if(has){S.pick=id;save();lockerUI(P)}};w.append(d)});P.append(w)}
const WEAP=[{n:'Sturmgewehr',d:22,r:.11,mag:30,col:'#ffd23a'},{n:'Schrotflinte',d:75,r:.9,mag:6,col:'#ff7a3c'},{n:'Scharfschütze',d:110,r:1.5,mag:4,col:'#9b5cff'},{n:'Spitzhacke',d:0,r:.45,mag:0,col:'#9aa3b0'}];
function skinMesh(i){const k=SK[i],g=new THREE.Group(),M=c=>new THREE.MeshLambertMaterial({color:c});if(i===25)return dijar(g,M);return human(i,g,M);
 const b=new THREE.Mesh(new THREE.CylinderGeometry(.45,.5,1.1,12),M(k.c1));b.position.y=.95;
 const belt=new THREE.Mesh(new THREE.CylinderGeometry(.51,.51,.18,12),M(k.c2));belt.position.y=.75;
 const h=new THREE.Mesh(new THREE.SphereGeometry(.34,14,12),M('#ffd9b0'));h.position.y=1.8;
 const hat=[new THREE.ConeGeometry(.36,.5,10),new THREE.BoxGeometry(.7,.2,.7),new THREE.SphereGeometry(.38,10,8,0,6.3,0,1.6),new THREE.CylinderGeometry(.2,.36,.4,8)][i%4];
 const ht=new THREE.Mesh(hat,M(k.c2));ht.position.y=2.1;
 const l=new THREE.Mesh(new THREE.BoxGeometry(.7,.5,.3),M(k.c2));l.position.y=.25;g.add(b,belt,h,ht,l);return g}
function startGame(mode,room){const T=mode==='Teams';WEAP[0]=WEAP[1]=WEAP[2]=null;
 $('menu').classList.remove('on');$('hud').classList.add('on');const cv=$('gl');cv.style.display='block';
 const R=new THREE.WebGLRenderer({canvas:cv,antialias:true});R.setClearColor(0x7fd0ff);R.setSize(innerWidth,innerHeight);R.setPixelRatio(Math.min(devicePixelRatio,2));
 const sc=new THREE.Scene();sc.background=new THREE.Color('#7fd0ff');sc.fog=new THREE.Fog('#7fd0ff',80,260);
 const cam=new THREE.PerspectiveCamera(70,innerWidth/innerHeight,.1,400);
 sc.add(new THREE.HemisphereLight('#fff','#4a8a3a',.9));const sun=new THREE.DirectionalLight('#fff3c0',.7);sun.position.set(60,100,30);sc.add(sun);
 const gr=new THREE.Mesh(new THREE.PlaneGeometry(600,600),new THREE.MeshLambertMaterial({color:'#5dbb4a'}));gr.rotation.x=-Math.PI/2;sc.add(gr);if(T)[[-1,'#c94a4a'],[1,'#4a6fd6']].forEach(([s,c])=>{const p=new THREE.Mesh(new THREE.PlaneGeometry(150,300),new THREE.MeshLambertMaterial({color:c}));p.rotation.x=-Math.PI/2;p.position.set(s*75,.03,0);sc.add(p)});
 const sea=new THREE.Mesh(new THREE.RingGeometry(150,400,40),new THREE.MeshBasicMaterial({color:'#2a8fd6',side:2}));sea.rotation.x=-Math.PI/2;sea.position.y=.05;sc.add(sea);
 const boxes=[],res=[];const rr=()=>(Math.random()-.5);
 for(let i=0;i<(T?0:70);i++){const x=rr()*260,z=rr()*260;if(Math.hypot(x,z)>140)continue;const t=new THREE.Group();const tr=new THREE.Mesh(new THREE.CylinderGeometry(.3,.4,3,6),new THREE.MeshLambertMaterial({color:'#7a4a22'}));tr.position.y=1.5;const lf=new THREE.Mesh(new THREE.ConeGeometry(2,4,8),new THREE.MeshLambertMaterial({color:'#2a8a3a'}));lf.position.y=4.5;t.add(tr,lf);t.position.set(x,0,z);sc.add(t);res.push({p:t.position,m:'wood',o:t})}
 for(let i=0;i<(T?0:18);i++){const x=rr()*260,z=rr()*260;if(Math.hypot(x,z)>140)continue;const m=new THREE.Mesh(new THREE.DodecahedronGeometry(1.5),new THREE.MeshLambertMaterial({color:'#8d93a0'}));m.position.set(x,1,z);sc.add(m);res.push({p:m.position,m:'stone',o:m})}
 for(let i=0;i<(T?0:14);i++){const x=rr()*240,z=rr()*240;if(Math.hypot(x,z)>130)continue;const w=6+Math.random()*4,h=4+Math.random()*3,m=new THREE.Mesh(new THREE.BoxGeometry(w,h,w),new THREE.MeshLambertMaterial({color:['#ff9a8a','#ffd36a','#8ad0ff','#c9a0ff'][i%4]}));m.position.set(x,h/2,z);sc.add(m);const rf=new THREE.Mesh(new THREE.ConeGeometry(w*.8,3,4),new THREE.MeshLambertMaterial({color:'#c0392b'}));rf.position.set(x,h+1.5,z);rf.rotation.y=.78;sc.add(rf);boxes.push({x0:x-w/2,x1:x+w/2,z0:z-w/2,z1:z+w/2,top:h,wall:true});res.push({p:m.position,m:'metal',o:null,keep:true})}
 MT.length=0;if(T)for(let i=0;i<16;i++){const x=(i%2?1:-1)*(10+Math.random()*110),z=(Math.random()-.5)*240,w=3+Math.random()*4,h=2+Math.random()*2,m=new THREE.Mesh(new THREE.BoxGeometry(w,h,2),new THREE.MeshLambertMaterial({color:x<0?'#8a2f2f':'#2f4a8a'}));m.position.set(x,h/2,z);sc.add(m);boxes.push({x0:x-w/2,x1:x+w/2,z0:z-1,z1:z+1,top:h,wall:true})}
 for(let i=0;i<(T?0:5);i++){const a=i*1.3+.5,r=70+Math.random()*35,h=28+Math.random()*18,x=Math.cos(a)*r,z=Math.sin(a)*r;MT.push({x,z,h});const m=new THREE.Mesh(new THREE.ConeGeometry(18,h,8),new THREE.MeshLambertMaterial({color:'#8a8f99'}));m.position.set(x,h/2,z);sc.add(m);const sn=new THREE.Mesh(new THREE.ConeGeometry(5.5,h*.3,8),new THREE.MeshBasicMaterial({color:'#fff'}));sn.position.set(x,h*.85,z);sc.add(sn)}
 const bch=new THREE.Mesh(new THREE.RingGeometry(132,152,48),new THREE.MeshBasicMaterial({color:'#f2dc9a',side:2}));bch.rotation.x=-Math.PI/2;bch.position.y=.03;sc.add(bch);
 const zone=new THREE.Mesh(new THREE.CylinderGeometry(1,1,200,48,1,true),new THREE.MeshBasicMaterial({color:'#9b5cff',transparent:true,opacity:.28,side:2}));zone.position.y=90;sc.add(zone);
 const P={dm:1,bus:!T,lives:mode==='Reload'?3:T?5:1,team:T?(Math.random()<.5?'red':'blue'):'',pos:new THREE.Vector3(-150,80,rr()*100),vy:0,yaw:0,pitch:.1,hp:100,sh:0,heal:2,ammo:120,w:3,mag:[30,6,4],cd:0,mats:{wood:30,stone:0,metal:0},mat:'wood',kills:0,chute:!T,alive:true,mesh:skinMesh(S.skin>=0?S.skin:Math.floor(Math.random()*25))};sc.add(P.mesh);P.pk=pickMesh(S.pick||'basic');P.pk.position.set(.62,1.3,.35);P.pk.rotation.z=-.3;P.mesh.add(P.pk);P.gun=new THREE.Mesh(new THREE.BoxGeometry(.12,.16,.9),new THREE.MeshLambertMaterial({color:'#ffd23a'}));P.gun.position.set(.55,1.25,.6);P.mesh.add(P.gun);if(T){P.pos.set((P.team==='red'?-1:1)*(30+Math.random()*80),0,(Math.random()-.5)*160);P.yaw=P.team==='red'?-1.57:1.57;addMarker(P.mesh,P.team)}P.busM=new THREE.Mesh(new THREE.BoxGeometry(10,3,5),new THREE.MeshLambertMaterial({color:'#3a7bff'}));sc.add(P.busM);
 const bots=[];const nb=T?16:mode==='Reload'?14:24;for(let i=0;i<nb;i++){const a=Math.random()*6.28,r=20+Math.random()*100,m=skinMesh(Math.floor(Math.random()*25));m.position.set(T?(i%2?1:-1)*(15+Math.random()*100):Math.cos(a)*r,0,T?(Math.random()-.5)*200:Math.sin(a)*r);const tm=i%2?'blue':'red';if(T)addMarker(m,tm);sc.add(m);bots.push({m,hp:100,t:0,dir:Math.random()*6.28,w:Math.floor(Math.random()*3),cd:0,team:tm,lives:mode==='Reload'?3:T?4:1,ally:T?tm===P.team:(mode==='Duo'||mode==='Squad')&&i<(mode==='Duo'?1:3)})}
 G={team:T,R,sc,cam,P,bots,boxes,res,zone,t:0,zr:150,keys:{},run:true,mode,last:performance.now(),build:[]};
 for(let i=0;i<(T?0:30);i++){const m=new THREE.Mesh(new THREE.BoxGeometry(1.2,.8,.8),new THREE.MeshLambertMaterial({color:'#ffc93c',emissive:'#664400'}));m.position.set(rr()*200,.4,rr()*200);sc.add(m);G.res.push({p:m.position,m:'chest',o:m})}
 if(T)loadoutPick();touchInit();try{cv.requestPointerLock()}catch(e){}if(room&&LOBBY){LOBBY.join(room).then(r=>{if(!G){r.leave();return}G.net=r;r.onPeers(c=>{if(G)G.peersNow=c.peers});r.on('hit',m=>{if(!G||!m.data||m.data.to!==MYID||m.isMe)return;let d=m.data.d||10;const P=G.P;if(P.sh>0){const s=Math.min(P.sh,d);P.sh-=s;d-=s}P.hp-=d;snd(120,.1,'sawtooth',.3)})}).catch(()=>{})}
 loop();}
addEventListener('keydown',e=>{if(!G)return;G.keys[e.code]=1;const P=G.P;
 if(e.code==='Digit1'||e.code==='Digit2'||e.code==='Digit3'||e.code==='Digit4')if(WEAP[+e.key-1])P.w=+e.key-1;
 if(e.code==='KeyH'&&P.heal>0&&P.hp<100){P.heal--;P.hp=Math.min(100,P.hp+40);snd(700,.2,'sine')}
 if(e.code==='KeyG')P.mat={wood:'stone',stone:'metal',metal:'wood'}[P.mat];
 if(e.code==='KeyE')harvest();
 if('ZXCV'.includes(e.key.toUpperCase())&&e.code.startsWith('Key'))place(e.key.toUpperCase());
 if(e.code==='Escape')endGame(false)});
addEventListener('keyup',e=>{if(G)G.keys[e.code]=0});
addEventListener('mousemove',e=>{if(!G||(document.pointerLockElement!==$('gl')&&!G.fire))return;G.P.yaw-=e.movementX*.0025*S.sens;G.P.pitch=Math.max(-.6,Math.min(1,G.P.pitch+e.movementY*.0025*S.sens))});
addEventListener('mousedown',()=>{if(G){if(document.pointerLockElement!==$('gl'))try{$('gl').requestPointerLock()}catch(e){}G.fire=1}});
addEventListener('mouseup',()=>{if(G)G.fire=0});
function harvest(){const P=G.P;let best=null,bd=6;G.res.forEach(r=>{const d=P.pos.distanceTo(r.p);if(d<bd){bd=d;best=r}});if(!best)return;snd(200,.1,'sawtooth');
 if(best.m==='chest'){giveWeapon(P,lootWeapon());P.ammo+=40;P.heal++;P.sh=Math.min(100,P.sh+50);G.sc.remove(best.o);G.res.splice(G.res.indexOf(best),1);snd(900,.3,'sine')}else P.mats[best.m]+=S.pick==='barca'?25:15}
function place(k){if(!OPT.build)return;const P=G.P,m=P.mat,cost=10;if(P.mats[m]<cost)return snd(120,.2);P.mats[m]-=cost;
 const col={wood:'#c08a4a',stone:'#8d93a0',metal:'#4fc3f7'}[m],fx=-Math.sin(P.yaw),fz=-Math.cos(P.yaw),x=Math.round((P.pos.x+fx*4)/4)*4,z=Math.round((P.pos.z+fz*4)/4)*4,gy=Math.floor(P.pos.y/4)*4;
 let g,y,b={x0:x-2,x1:x+2,z0:z-2,z1:z+2};
 if(k==='Z'){g=new THREE.BoxGeometry(4,4,.4);y=gy+2;if(Math.abs(fx)>Math.abs(fz)){g=new THREE.BoxGeometry(.4,4,4)}b.top=gy+4;b.wall=true;b.base=gy}
 else if(k==='X'){g=new THREE.BoxGeometry(4,.4,4);y=gy+4;b.top=gy+4.2}
 else if(k==='V'){g=new THREE.BoxGeometry(4,.4,4);y=gy+8;b.top=gy+8.2}
 else{g=new THREE.BoxGeometry(4,.4,5.6);y=gy+2;b.top=gy+4;b.ramp=true;b.base=gy;b.dir=[fx,fz]}
 const mesh=new THREE.Mesh(g,new THREE.MeshLambertMaterial({color:col}));mesh.position.set(x,y,z);if(k==='C'){mesh.rotation.x=-.78;mesh.rotation.y=P.yaw}G.sc.add(mesh);G.boxes.push(b);snd(400,.06,'square')}
const MT=[];function floorY(x,z,y){let h=0;for(const q of MT){const d=Math.hypot(x-q.x,z-q.z);if(d<18)h=Math.max(h,q.h*(1-d/18))}for(const b of G.boxes){if(b.wall||x<b.x0||x>b.x1||z<b.z0||z>b.z1)continue;let t=b.top;if(b.ramp){const f=Math.abs(b.dir[0])>Math.abs(b.dir[1])?(b.dir[0]>0?(x-b.x0)/4:(b.x1-x)/4):(b.dir[1]>0?(z-b.z0)/4:(b.z1-z)/4);t=b.base+Math.max(0,Math.min(1,f))*4}if(t<=y+1.2&&t>h)h=t}return h}
function collide(p,ob){for(const b of G.boxes){if(!b.wall)continue;if(p.y>(b.top||0)-.2)continue;if(p.x>b.x0-.5&&p.x<b.x1+.5&&p.z>b.z0-.5&&p.z<b.z1+.5){const dx=Math.min(p.x-b.x0,b.x1-p.x),dz=Math.min(p.z-b.z0,b.z1-p.z);if(dx<dz)p.x=(p.x-b.x0<b.x1-p.x)?b.x0-.5:b.x1+.5;else p.z=(p.z-b.z0<b.z1-p.z)?b.z0-.5:b.z1+.5}}}
function shoot(o,dir,w,tgt){const W=WEAP[w];let hit=null,hd=W.n==='Scharfschütze'?300:120;
 for(const t of tgt){if(t.dead)continue;const c=t.pos?t.pos:t.m.position,v=new THREE.Vector3().subVectors(c,o),s=v.dot(dir);if(s<0||s>hd)continue;const p=o.clone().addScaledVector(dir,s);if(p.distanceTo(new THREE.Vector3(c.x,c.y+1,c.z))<(W.n==='Schrotflinte'?1.6:1.1)){hit=t;hd=s}}return hit}
function loop(){if(!G||!G.run)return;requestAnimationFrame(loop);const g=G,P=g.P,cam=g.cam,now=performance.now(),dt=Math.min(.05,(now-g.last)/1000);g.last=now;g.t+=dt;if(g.pause){g.R.render(g.sc,cam);return}
 // player
 const k=g.keys,sp=(k.ShiftLeft?11:7)*(P.chute?1.2:1),fx=-Math.sin(P.yaw),fz=-Math.cos(P.yaw);let mx=0,mz=0;
 if(k.KeyW){mx+=fx;mz+=fz}if(k.KeyS){mx-=fx;mz-=fz}if(k.KeyA){mx+=fz;mz-=fx}if(k.KeyD){mx-=fz;mz+=fx}if(k.ArrowLeft)P.yaw+=dt*2;if(k.ArrowRight)P.yaw-=dt*2;if(JS.id!=null){mx+=-fx*JS.y-fz*JS.x;mz+=-fz*JS.y+fx*JS.x}
 P.pos.x+=mx*sp*dt;P.pos.z+=mz*sp*dt;collide(P.pos);
 const fy=floorY(P.pos.x,P.pos.z,P.pos.y);
 if(P.bus){P.pos.x+=16*dt;P.pos.y=80;if(k.Space||P.pos.x>150)P.bus=false}else if(P.chute){P.pos.y-=(P.pos.y>45?18:7)*dt;if(P.pos.y<=fy+.01){P.chute=false;P.vy=0}}else{P.vy-=28*dt;P.pos.y+=P.vy*dt;if(P.pos.y<=fy){P.pos.y=fy;P.vy=0;if(k.Space)P.vy=10}}
 P.mesh.position.copy(P.pos);P.mesh.rotation.y=P.yaw+Math.PI;P.mesh.visible=!P.bus;P.busM.position.set(P.pos.x,P.pos.y+2,P.pos.z);P.busM.visible=P.bus;P.pk.visible=!P.bus;P.pk.position.set(P.w===3?.62:-.2,1.3,P.w===3?.35:-.4);P.pk.rotation.z=P.w===3?-.3:.9;const gw=P.w<3?WEAP[P.w]:null;P.gun.visible=!!gw&&!P.bus;if(gw){P.gun.scale.z=gw.len||1;P.gun.material.color.set(gw.col)}P.sw=Math.max(0,(P.sw||0)-dt);P.pk.rotation.x=-1.3*(P.sw/.25);P.mesh.scale.y=k.KeyC&&!P.chute?.7:1;
 const cd=new THREE.Vector3(fx*Math.cos(P.pitch),-Math.sin(P.pitch),fz*Math.cos(P.pitch));
 cam.position.copy(P.pos).addScaledVector(cd,-6).add(new THREE.Vector3(0,3.2,0));cam.lookAt(P.pos.x+cd.x*20,P.pos.y+2+cd.y*20,P.pos.z+cd.z*20);
 // shoot
 P.cd-=dt;if(g.fire&&P.w===3&&P.cd<=0&&!P.chute){P.cd=.45;P.sw=.25;harvest()}if(g.fire&&P.w<3&&P.cd<=0&&!P.chute&&P.ammo>0){const W=WEAP[P.w];P.cd=W.r;if(!g.team)P.ammo--;snd(W.t==='shotgun'?90:W.t==='sniper'?60:160,.09,'sawtooth',.3);
  const o=cam.position.clone(),h=shoot2(o,cd,P.w,g.bots.filter(b=>!b.ally).concat((g.remL||[]).filter(r=>!g.team||r.team!==P.team)));fireFx(o,cd,h,fx,fz,P);if(h){const DM=WEAP[P.w].d*P.dm*(LASTHS?2:1);if(h.remote&&g.net)g.net.emit('hit',{to:h.remote,d:DM|0});h.hp-=DM;dmgPop(h.m.position,Math.round(DM),LASTHS);P.dmgT=(P.dmgT||0)+Math.round(DM);snd(1000,.05,'sine');$('cross').style.borderColor='#f33';setTimeout(()=>$('cross').style.borderColor='#fff',120);h.m.children[0].material.emissive.set('#ff0000');setTimeout(()=>h.m.children[0]&&h.m.children[0].material.emissive.set('#000'),80);if(h.hp<=0&&!h.dead){P.kills++;S.coins+=20;snd(1400,.2,'sine');if(h.lives!==undefined)botDie(h);else{h.dead=true;g.sc.remove(h.m)}}}}
 // bots
 let alive=0;for(const b of g.bots){if(b.dead)continue;if(!b.ally)alive++;const p=b.m.position,dp=P.pos.distanceTo(p);b.t-=dt;
  if(b.t<=0){b.t=1+Math.random()*2;b.dir=g.team?Math.atan2((b.team==='red'?1:-1)*30-p.x,(Math.random()-.5)*120-p.z):b.ally?Math.atan2(P.pos.x-p.x,P.pos.z-p.z):Math.random()*6.28}
  if(Math.hypot(p.x,p.z)>g.zr){b.dir=Math.atan2(-p.x,-p.z)}
  if(!b.ally&&dp<45&&dp>6)b.dir=Math.atan2(P.pos.x-p.x,P.pos.z-p.z);
  const old=p.clone();p.x+=Math.sin(b.dir)*4.5*dt;p.z+=Math.cos(b.dir)*4.5*dt;collide(p);p.y=floorY(p.x,p.z,p.y+1);b.m.rotation.y=b.dir;
  b.cd-=dt;if(!b.ally&&dp<50&&b.cd<=0&&P.alive&&!P.chute){b.cd=.5+Math.random();spawnBullet(new THREE.Vector3(p.x,p.y+1.5,p.z),new THREE.Vector3(P.pos.x+(Math.random()-.5)*2,P.pos.y+1.2,P.pos.z+(Math.random()-.5)*2),'#ff5533');if(Math.random()<.28){let d=7;if(P.sh>0){const s=Math.min(P.sh,d);P.sh-=s;d-=s}P.hp-=d;snd(120,.1,'sawtooth',.25)}}
  if(Math.hypot(p.x,p.z)>g.zr&&Math.random()<dt)b.hp-=3;if(b.hp<=0&&!b.dead){b.dead=true;g.sc.remove(b.m)}}
 // zone
 if(g.team){for(const a of g.bots){if(a.dead)continue;a.tc=(a.tc||0)-dt;if(a.tc>0)continue;let best=null,bd=45;for(const e of g.bots){if(e.dead||e.ally===a.ally)continue;const d=a.m.position.distanceTo(e.m.position);if(d<bd){bd=d;best=e}}if(!best)continue;a.tc=.7+Math.random();const ap=a.m.position,bp=best.m.position;spawnBullet(new THREE.Vector3(ap.x,ap.y+1.5,ap.z),new THREE.Vector3(bp.x,bp.y+1.3,bp.z),a.ally?'#ffd23a':'#ff5533');if(Math.random()<.35){best.hp-=18;if(best.hp<=0)botDie(best)}}}
 g.zr=g.team||g.mode==='Reload'?150:Math.max(14,150-g.t*.9);g.zone.scale.set(g.zr,1,g.zr);if(Math.hypot(P.pos.x,P.pos.z)>g.zr&&!P.chute)P.hp-=4*dt;
 if(P.hp<=0){if(P.lives>1){P.lives--;P.hp=100;P.sh=0;if(g.team){P.pos.set((P.team==='red'?-1:1)*(30+Math.random()*80),0,(Math.random()-.5)*160);P.vy=0;loadoutPick()}else{P.pos.set((Math.random()-.5)*160,40,(Math.random()-.5)*160);P.chute=true}toast('Respawn! Leben: '+P.lives,'#4cff7a')}else return endGame(false)}if(g.team&&P.kills>=20&&!g.over)return endGame(true);if(alive===0&&!(g.remL||[]).some(r=>!r.dead&&r.hp>0)&&!g.over)return endGame(true);
 // HUD
 $('hp').textContent=`Leben ${Math.max(0,P.hp|0)} · Schild ${P.sh|0} · Heilung ×${P.heal}`;$('hpb').style.width=Math.max(0,P.hp)+'%';$('hpt').textContent='❤ '+Math.max(0,P.hp|0)+' / 100';$('sht').textContent='🛡 '+(P.sh|0)+' / 100';$('shb').style.width=P.sh+'%';
 $('mats').textContent=`Holz ${P.mats.wood} · Stein ${P.mats.stone} · Metall ${P.mats.metal} (Bau: ${P.mat})`;
 $('wp').innerHTML=`<b style="color:${WEAP[P.w].col}">${WEAP[P.w].n}</b><br>${P.w<3?'Munition '+P.ammo+' · Schaden '+Math.round(WEAP[P.w].d*P.dm):'Klicken = Hacken'}`;
 $('info').innerHTML=`Übrig: ${alive+1}<br>Elims: ${P.kills}<br>Schaden: ${P.dmgT|0}${g.team?'<br>Team: '+(P.team==='red'?'ROT':'BLAU')+' · Ziel 20 Elims':''}${g.team||g.mode==='Reload'?'<br>Leben: '+P.lives:''}<br>Zone: ${g.zr|0} m${P.bus?'<br><b>SPACE: Bus verlassen</b>':P.chute?'<br>Fallschirm aktiv':''}`;
 if(g.fx){for(let i=g.fx.length-1;i>=0;i--){const f=g.fx[i],s=240*dt;f.m.position.addScaledVector(f.dir,s);f.left-=s;if(f.left<=0){g.sc.remove(f.m);g.fx.splice(i,1)}}}
if(g.net){g.rem=g.rem||{};const L=[],seen={};for(const p of (g.peersNow||[])){const q=p.presence;if(p.isMe||q.x==null)continue;seen[p.peer]=1;let r=g.rem[p.peer];if(!r){r={m:skinMesh(q.skin|0),hp:100,remote:p.by};g.rem[p.peer]=r;r.m.position.set(q.x,q.y,q.z);g.sc.add(r.m)}const m=r.m.position;m.x+=(q.x-m.x)*.3;m.y+=(q.y-m.y)*.3;m.z+=(q.z-m.z)*.3;r.m.rotation.y=q.yaw+Math.PI;r.m.visible=q.hp>0&&!r.dead;if(!r.dead)r.hp=q.hp;r.team=q.team;L.push(r)}for(const id in g.rem)if(!seen[id]){g.sc.remove(g.rem[id].m);delete g.rem[id]}g.remL=L;if(now-(g.lp||0)>100){g.lp=now;g.net.presence({x:+P.pos.x.toFixed(1),y:+P.pos.y.toFixed(1),z:+P.pos.z.toFixed(1),yaw:+P.yaw.toFixed(2),skin:S.skin>=0?S.skin:0,team:P.team||'',hp:Math.max(0,P.hp|0)}).catch(()=>{})}}const mc=$('mini').getContext('2d');mc.clearRect(0,0,140,140);mc.fillStyle='#5dbb4a';mc.beginPath();mc.arc(70,70,64,0,7);mc.fill();mc.strokeStyle='#9b5cff';mc.lineWidth=3;mc.beginPath();mc.arc(70,70,Math.min(64,g.zr*.42),0,7);mc.stroke();mc.fillStyle='#f33';g.bots.forEach(b=>{if(!b.dead&&!b.ally)mc.fillRect(70+b.m.position.x*.42-1.5,70+b.m.position.z*.42-1.5,3,3)});mc.fillStyle='#fff';mc.fillRect(70+P.pos.x*.42-3,70+P.pos.z*.42-3,6,6);
 g.R.render(g.sc,cam)}
function endGame(win){if(!G||G.over)return;G.over=true;G.run=false;const P=G.P;if(document.pointerLockElement)document.exitPointerLock();
 const xp=20+P.kills*25+(win?200:0)+Math.floor(G.t/5);S.xp+=xp;S.kills+=P.kills;S.games++;const tk=tokenRoll();if(win)S.wins++;save();snd(win?1000:200,.6,'sine');
 const m=$('modal');m.innerHTML=`<h1>${win?'VICTORY ROYALE!':'Eliminiert'}</h1><p>${P.kills} Eliminierungen · +${xp} XP</p><button class="btn hot" id="bk">Zurück zur Lobby</button>`;m.classList.add('on');if(tk)tokenWin();
 $('bk').onclick=()=>{m.classList.remove('on');if(G.net)G.net.leave();const tc=document.getElementById('tc');if(tc)tc.remove();G.R.dispose();G=null;$('gl').style.display='none';$('hud').classList.remove('on');show('menu');$('panel').innerHTML=''}}
addEventListener('resize',()=>{if(G){G.R.setSize(innerWidth,innerHeight);G.cam.aspect=innerWidth/innerHeight;G.cam.updateProjectionMatrix()}});
let CB='';addEventListener('keydown',e=>{if(G||!KEY||!e.key||e.key.length!==1)return;CB=(CB+e.key.toLowerCase()).slice(-14);if(CB==='dijarismydaddy'){CB='';for(let i=0;i<34;i++)if(!S.own.includes(i))S.own.push(i);S.picks=['basic','barca'];S.claimed=50;S.xp=Math.max(S.xp,49*50);if(!S.cheat){S.cheat=1;S.coins+=6000}if(S.skin<0)S.skin=25;save();stats();snd(1000,.4,'sine');const m=document.getElementById('modal');m.innerHTML='<h1>CHEAT AKTIVIERT</h1><p>Alle Skins und der komplette Battle Pass sind freigeschaltet!</p><button class="btn hot" onclick="document.getElementById(\'modal\').classList.remove(\'on\')">OK</button>';m.classList.add('on')}});
addEventListener('error',e=>{try{if(G)G.run=false;const m=document.getElementById('modal');m.innerHTML='<h2>Fehler im Spiel</h2><p style="max-width:80vw">'+String(e.message).replace(/</g,'&lt;')+'</p><button class="btn hot" onclick="location.reload()">Neu laden</button>';m.classList.add('on')}catch(_){}});
onlineInit();stats();
</script></body></html>
