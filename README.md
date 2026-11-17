# Bloodrush
Крутая игра
<!DOCTYPE html>
<html lang="ru"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, viewport-fit=cover">
<title>BLOODRUSH</title>
<style>
:root{color-scheme:dark;--bg:#100404;--fg:#ffe9d6;--red:#ff2a1a}
*{box-sizing:border-box;-webkit-user-select:none;user-select:none;-webkit-touch-callout:none;-webkit-tap-highlight-color:transparent}
html,body{margin:0;height:100%;overflow:hidden;background:var(--bg);color:var(--fg);font-family:Impact,Haettenschweiler,"Arial Narrow Bold",sans-serif;touch-action:none}
canvas{position:fixed;inset:0;width:100%;height:100%;display:block}
#pad{position:fixed;inset:0;z-index:2}
.hud{position:fixed;z-index:3;pointer-events:none}
#hp{left:calc(12px + env(safe-area-inset-left,0px));top:calc(10px + env(safe-area-inset-top,0px));width:42vw;max-width:260px}
.bar{height:14px;background:#0008;border:2px solid #fff6;transform:skewX(-12deg)}
#hpf{height:100%;width:100%;background:linear-gradient(90deg,#c00,#ff4a2a)}
#dash{display:flex;gap:5px;margin-top:6px}
#dash i{flex:1;height:7px;background:#0008;border:1px solid #fff5;position:relative;transform:skewX(-12deg);overflow:hidden}
#dash b{position:absolute;inset:0;background:#3cf;width:0}
#rank{right:calc(14px + env(safe-area-inset-right,0px));top:calc(6px + env(safe-area-inset-top,0px));text-align:right}
#rl{font-size:56px;line-height:1;text-shadow:0 0 14px currentColor}
#rb{width:90px;height:6px;background:#0008;margin:2px 0 4px auto}
#rbf{height:100%;width:0;background:currentColor}
#info{font-size:15px;letter-spacing:1px;opacity:.85}
#cross{left:50%;top:50%;width:18px;height:18px;margin:-9px 0 0 -9px;border:2px solid #fff9;border-radius:50%}
#vig{inset:0;background:radial-gradient(transparent 40%,#f00 130%);opacity:0;transition:opacity .25s}
#msg{left:0;right:0;top:30%;text-align:center;font-size:34px;letter-spacing:3px;text-shadow:0 0 12px #f33;opacity:0;transition:opacity .4s}
.btn{position:fixed;z-index:4;border-radius:50%;border:3px solid #fff7;background:#ff2a1a44;color:#fff;font:inherit;display:flex;align-items:center;justify-content:center;letter-spacing:1px;touch-action:none}
.btn:active,.btn.on{background:#ff2a1acc}
#bf{width:96px;height:96px;right:calc(18px + env(safe-area-inset-right,0px));bottom:calc(26px + env(safe-area-inset-bottom,0px));font-size:22px}
#bd{width:68px;height:68px;right:calc(128px + env(safe-area-inset-right,0px));bottom:calc(30px + env(safe-area-inset-bottom,0px));font-size:16px;background:#33ccff33}
#bj{width:68px;height:68px;right:calc(34px + env(safe-area-inset-right,0px));bottom:calc(138px + env(safe-area-inset-bottom,0px));font-size:16px;background:#ffffff22}
#bw{width:60px;height:60px;right:calc(210px + env(safe-area-inset-right,0px));bottom:calc(30px + env(safe-area-inset-bottom,0px));font-size:13px;background:#ffaa0033}
#joy{position:fixed;z-index:3;width:110px;height:110px;margin:-55px 0 0 -55px;border-radius:50%;border:3px solid #fff5;display:none;pointer-events:none}
#knob{position:absolute;left:35px;top:35px;width:40px;height:40px;border-radius:50%;background:#fff8}
#ov{position:fixed;inset:0;z-index:9;background:#100404ee;display:flex;flex-direction:column;align-items:center;justify-content:safe center;text-align:center;padding:20px;overflow:auto}
.row{display:flex;gap:8px;margin:10px 0;flex-wrap:wrap;justify-content:center}
.sm,.opt{font:inherit;font-size:17px;padding:8px 16px;background:#331;color:#fff;border:2px solid #fff4;letter-spacing:2px}
.opt.on{background:var(--red)}
#coins{font-size:24px;color:#ffd24a;margin:6px 0}
#pan{width:100%;max-width:420px;font-family:system-ui,sans-serif;font-size:14px;text-align:left}
.it{display:flex;justify-content:space-between;align-items:center;gap:8px;padding:8px;border-bottom:1px solid #fff2}
.it small{opacity:.7;display:block}
.it button{font:inherit;font-size:15px;padding:6px 12px;background:var(--red);color:#fff;border:0;min-width:84px}
.it button:disabled{background:#444;opacity:.6}
#wn{right:calc(14px + env(safe-area-inset-right,0px));top:calc(112px + env(safe-area-inset-top,0px));font-size:15px;text-align:right;color:#ffd24a;text-shadow:0 0 6px #000}
#ov h1{font-size:54px;margin:0;color:var(--red);letter-spacing:4px;text-shadow:0 0 20px #f00}
#ov p{max-width:360px;font-family:system-ui,sans-serif;font-size:14px;line-height:1.5;opacity:.85}
#go{font:inherit;font-size:28px;padding:12px 40px;background:var(--red);color:#fff;border:0;transform:skewX(-12deg);letter-spacing:3px}
#bigmp{font:inherit;font-size:20px;padding:12px 28px;background:linear-gradient(135deg,#1f9d4a,#0a6b2f);color:#fff;border:0;transform:skewX(-12deg);letter-spacing:2px;margin:8px 0;box-shadow:0 0 18px #1f9d4a88}
#pvpbtn{font:inherit;font-size:20px;padding:12px 28px;background:linear-gradient(135deg,#ff8800,#aa2200);color:#fff;border:0;transform:skewX(-12deg);letter-spacing:2px;margin:8px 0;box-shadow:0 0 18px #ff880088}
#friendbtn{font:inherit;font-size:20px;padding:12px 28px;background:linear-gradient(135deg,#0066ff,#0033aa);color:#fff;border:0;transform:skewX(-12deg);letter-spacing:2px;margin:8px 0;box-shadow:0 0 18px #0066ff88}
#codebtn{font:inherit;font-size:20px;padding:12px 28px;background:linear-gradient(135deg,#ffd24a,#aa7700);color:#fff;border:0;transform:skewX(-12deg);letter-spacing:2px;margin:8px 0;box-shadow:0 0 18px #ffd24a88}
#lk{width:100%;font:inherit;font-size:12px;padding:10px;background:#0a2a14;color:#8fffb0;border:2px solid #1f9d4a;text-align:center;word-break:break-all;-webkit-user-select:text;user-select:text}
#tutprog{display:flex;justify-content:center;gap:5px;margin:8px 0}
.dot{width:9px;height:9px;border-radius:50%;background:#555;transition:background .2s}
.dot.on{background:var(--red);box-shadow:0 0 6px var(--red)}
#tutnav{display:flex;justify-content:space-between;align-items:center;gap:8px;margin-top:10px}
.stepnum{font-size:11px;opacity:.6;letter-spacing:2px}
.friend-item{display:flex;justify-content:space-between;padding:8px;border-bottom:1px solid #fff2;align-items:center}
.friend-item span{font-size:16px;color:#ffd24a}
.friend-item button{font:inherit;font-size:14px;padding:4px 8px;background:#0066ff;color:#fff;border:0}
</style></head><body>
<div id="pad"></div>
<div class="hud" id="hp"><div class="bar"><div id="hpf"></div></div><div id="dash"><i><b></b></i><i><b></b></i><i><b></b></i></div></div>
<div class="hud" id="rank"><div id="rl">D</div><div id="rb"><div id="rbf"></div></div><div id="info">ВОЛНА 1 · 0</div></div>
<div class='hud' style='left:0;right:0;top:calc(52px + env(safe-area-inset-top,0px));text-align:center;font-size:13px;letter-spacing:1px'><span style='color:#ff3b30'>■ ВРАГ</span> &nbsp; <span style='color:#3dff8a'>■ СВОЙ</span></div>
<div class="hud" id="cross"></div><div class="hud" id="vig"></div><div class="hud" id="msg"></div>
<div id="joy"><div id="knob"></div></div>
<button class="btn" id="bf">ОГОНЬ</button><button class="btn" id="bd">РЫВОК</button><button class="btn" id="bj">ПРЫЖОК</button><button class="btn" id="bw">СМЕНА</button>
<div class='hud' id='wn'></div><div class='hud' id='cap' style='left:0;right:0;top:calc(72px + env(safe-area-inset-top,0px));text-align:center;font-size:15px;letter-spacing:1px;color:#5fd7ff;text-shadow:0 0 6px #000'></div>
<div id="ov"><h1>BLOODRUSH</h1>
<p id="ovt">Убивай — и лечись кровью врагов. Двигайся без остановки, делай рывки сквозь снаряды и держи высокий ранг стиля.<br><br>Красные метки — враги, зелёные — союзники.</p>
<div id='coins'>МОНЕТЫ: <b id='cn'>0</b></div><div id='st' style='font-size:13px;opacity:.8;font-family:system-ui,sans-serif'></div>
<div class='row' id='locs'></div><div class='row' id='dif'></div>
<button id="go">ИГРАТЬ</button>
<button id="bigmp">▶ ИГРАТЬ С ДРУГОМ</button>
<button id="pvpbtn">⚔ ПВП ДУЭЛЬ (1v1)</button>
<button id="friendbtn">👥 ДРУЗЬЯ</button>
<button id="codebtn">🎁 ВВЕСТИ КОД</button>
<div class='row'><button class='sm' id='bshop'>МАГАЗИН</button><button class='sm' id='blob'>ЛОББИ</button><button class='sm' id='btut'>ОБУЧЕНИЕ</button></div>
<div id='pan' style='display:none'></div></div>
<script>onerror=function(m,s,l){var o=document.getElementById('ovt');if(o){o.textContent='Ошибка: '+m+' (строка '+l+')';document.getElementById('ov').style.display='flex'}}</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>if(!window.THREE){document.write('<script src="https://cdn.jsdelivr.net/npm/three@0.128.0/build/three.min.js"><\/script>')}</script>
<script>if(!window.THREE){document.getElementById('ovt').textContent='Не загрузилась 3D-библиотека. Проверь интернет и открой страницу заново.'}</script>
<script src="https://unpkg.com/peerjs@1.5.2/dist/peerjs.min.js"></script>
<script>
const $=id=>document.getElementById(id),V3=THREE.Vector3;
const scene=new THREE.Scene();scene.background=new THREE.Color(0x100404);scene.fog=new THREE.Fog(0x100404,8,55);
const cam=new THREE.PerspectiveCamera(80,innerWidth/innerHeight,.1,100);cam.rotation.order='YXZ';scene.add(cam);
const rd=new THREE.WebGLRenderer({antialias:false});rd.setPixelRatio(Math.min(devicePixelRatio,2));rd.setSize(innerWidth,innerHeight);document.body.prepend(rd.domElement);
addEventListener('resize',()=>{rd.setSize(innerWidth,innerHeight);cam.aspect=innerWidth/innerHeight;cam.updateProjectionMatrix()});
scene.add(new THREE.AmbientLight(0x886666,1));
const pl=new THREE.PointLight(0xff6644,1.3,45);cam.add(pl);
const floor=new THREE.Mesh(new THREE.PlaneGeometry(60,60),new THREE.MeshLambertMaterial({color:0x2a1a1a}));floor.rotation.x=-Math.PI/2;scene.add(floor);
const grid=new THREE.GridHelper(60,30,0x771111,0x441111);grid.position.y=.02;scene.add(grid);
const wm=new THREE.MeshLambertMaterial({color:0x3a1212});
[[0,-30,60,1],[0,30,60,1],[-30,0,1,60],[30,0,1,60]].forEach(([x,z,w,d])=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,10,d),wm);m.position.set(x,5,z);scene.add(m)});
const R=28,pillars=[[8,8],[-8,8],[8,-8],[-8,-8]];
pillars.forEach(([x,z])=>{const m=new THREE.Mesh(new THREE.CylinderGeometry(1.5,1.5,8,10),new THREE.MeshLambertMaterial({color:0x552222,emissive:0x220000}));m.position.set(x,4,z);scene.add(m)});

const P={pos:new V3(0,1.6,0),vel:new V3(),yaw:0,pitch:0,hp:100,gnd:true,dashes:3,dashT:0,dd:new V3()};
const RK=['D','C','B','A','S','SSS'],TH=[0,40,90,150,220,290],RC=['#aaa','#7cf','#6e6','#fd4','#f93','#f33'];
const CFG={husk:{hp:30,sp:7,c:0xcc2222,y:0,pts:30},shooter:{hp:25,sp:4,c:0xaa44ff,y:2.2,pts:45},brute:{hp:150,sp:4.5,c:0xff7700,y:0,pts:90},guard:{hp:60,sp:6,c:0x3366ff,y:0,pts:40},tank:{hp:300,sp:2,c:0x555555,y:0,pts:150},runner:{hp:15,sp:15,c:0xffaa00,y:0,pts:60},boss:{hp:3000,sp:5,c:0xff0000,y:0,pts:1000,isBoss:true}};
const WP=[
{id:0,n:'Пистолет',t:'СЛАБОЕ',p:0,dm:20,pe:1,cd:.22,sp:.02,col:0xffdd88},
{id:1,n:'Дробовик',t:'СИЛЬНОЕ',p:150,dm:9,pe:8,cd:.5,sp:.13,col:0xffcc66},
{id:2,n:'Автомат',t:'СЛАБОЕ',p:300,dm:9,pe:1,cd:.075,sp:.08,col:0x99ddff},
{id:3,n:'Рейлган',t:'МОЩНОЕ',p:600,dm:130,pe:1,cd:1.1,sp:0,pierce:1,col:0x66ffff},
{id:4,n:'Ракетница',t:'МОЩНОЕ',p:900,dm:85,pe:1,cd:1.3,sp:.02,aoe:6,col:0xff7733},
{id:5,n:'Огнемёт',t:'СИЛЬНОЕ',p:400,dm:5,pe:3,cd:.05,sp:.28,rng:10,col:0xff9933},
{id:6,n:'Шокер',t:'СИЛЬНОЕ',p:500,dm:35,pe:1,cd:.45,sp:.02,chain:4,col:0xaaccff},
{id:7,n:'Миниган',t:'СЛАБОЕ',p:750,dm:6,pe:1,cd:.04,sp:.11,col:0xffee99},
{id:8,n:'Плазмаган',t:'МОЩНОЕ',p:1100,dm:45,pe:1,cd:.35,sp:.015,aoe:3.5,col:0xcc66ff},
{id:9,n:'Снайперка',t:'МОЩНОЕ',p:1300,dm:220,pe:1,cd:1.6,sp:0,pierce:1,col:0xffff99},
{id:10,n:'Гранатомёт',t:'МОЩНОЕ',p:1500,dm:110,pe:1,cd:1.5,sp:.02,aoe:8,col:0xff5522},
{id:11,n:'Тесла-пушка',t:'СИЛЬНОЕ',p:1700,dm:40,pe:1,cd:.6,sp:.02,chain:6,col:0x66ccff},
{id:12,n:'Мясорубка',t:'СИЛЬНОЕ',p:1200,dm:60,pe:1,cd:.3,sp:.2,rng:4,col:0xff6688},
{id:13,n:'Лазер',t:'МОЩНОЕ',p:2000,dm:80,pe:1,cd:.9,sp:0,pierce:1,col:0xff44ff},
{id:14,n:'Дробовик-взрыв',t:'СИЛЬНОЕ',p:2200,dm:14,pe:6,cd:.9,sp:.18,aoe:2.5,col:0xffaa44},
{id:15,n:'Разрушитель',t:'МОЩНОЕ',p:3000,dm:35,pe:3,cd:.4,sp:.1,aoe:4,col:0xff0000},
{id:16,n:'Импульс',t:'МОЩНОЕ',p:4000,dm:150,pe:1,cd:1.8,sp:0,aoe:12,col:0x00ffff},
{id:17,n:'Копьё',t:'СИЛЬНОЕ',p:3500,dm:90,pe:1,cd:.8,sp:0,pierce:1,col:0xffaa00},
{id:18,n:'РУКА БОГА',t:'БОЖЕСТВЕННОЕ',p:20000,dm:800,pe:1,cd:.5,sp:0,pierce:1,col:0xff8800}
];
const CH=[{k:'hp',n:'Здоровье',d:'+20 макс. HP',b:100},{k:'sp',n:'Скорость',d:'+6% к скорости',b:120},{k:'bl',n:'Вампиризм',d:'+3 HP за убийство',b:150}];
const DIFF=[{n:'ЛЁГКИЙ',hp:.7,d:.6,c:.8,k:.7},{n:'СРЕДНИЙ',hp:1,d:1,c:1,k:1},{n:'ТЯЖЁЛЫЙ',hp:1.5,d:1.4,c:1.5,k:1.3}];
const LOC=[{n:'АРЕНА',bg:0x100404,fl:0x2a1a1a},{n:'АЭРОПОРТ',bg:0x0a1422,fl:0x2b3340},{n:'ЗАВОД',bg:0x1a0c04,fl:0x3a2414},{n:'ЗАМОК',bg:0x0c0806,fl:0x4a2e1c,wl:0x2a1e18},{n:'ШКОЛА',bg:0x120a06,fl:0x4a3220,wl:0x3a2416},{n:'КИБЕРПАНК',bg:0x080410,fl:0x1a1a2a,wl:0x1a1a3a},{n:'ПУСТЫНЯ',bg:0x2a1a0a,fl:0x6a4a2a,wl:0x3a2212}];

let enemies=[],shots=[],fx=[],tr=[],alive=false,started=false,cd=0,shake=0,wave=0,kills=0,style=0,wt=0,hold=false,msgT=0;
let DM=DIFF[1],run=0,SV={coins:200,own:[0],wl:{},ch:{hp:0,sp:0,bl:0},eq:0,diff:1};
let fr=0,ts=0,fc=0,wtimer=0,alarm=0,zp=0,zpos=new V3();
let LG=null,zone=null,zring=null,svt=0,room=null,rootRoom=null,lobbyCode='';
let DV=new V3(),RC2=new THREE.Raycaster(),allies=new Map(),myName='Игрок '+(100+Math.floor(Math.random()*900));
let isPvP=false, pvpHp=100, oppHp=100, pvpRespawn=0;
const joy={x:0,y:0},keys={};
const BG=new THREE.BoxGeometry(.15,.15,.15),BM=new THREE.MeshBasicMaterial({color:0xaa0000});

try{const s=JSON.parse(localStorage.getItem('br1'));if(s&&s.own)SV=Object.assign(SV,s)}catch(e){}
if(!SV.myName) SV.myName = 'Игрок ' + (100+Math.floor(Math.random()*900));
if(!SV.friends) SV.friends = [];
if(SV.codeT === undefined) SV.codeT = 0;

P.max=100;

function msg(t){const e=$('msg');e.textContent=t;e.style.opacity=1;msgT=1.6}
function lbl(txt,col,w){w=w||256;const c=document.createElement('canvas');c.width=w;c.height=64;const g=c.getContext('2d');g.font='bold 40px Impact,Arial Narrow,sans-serif';g.textAlign='center';g.lineWidth=7;g.strokeStyle='#000';g.strokeText(txt,w/2,46);g.fillStyle=col;g.fillText(txt,w/2,46);const s=new THREE.Sprite(new THREE.SpriteMaterial({map:new THREE.CanvasTexture(c),depthTest:false,transparent:true}));s.scale.set(3*w/256,.75,1);s.renderOrder=10;s.raycast=function(){};return s}
function ring(col){const r=new THREE.Mesh(new THREE.RingGeometry(1.1,1.4,24),new THREE.MeshBasicMaterial({color:col,side:THREE.DoubleSide}));r.rotation.x=-Math.PI/2;r.position.y=.05;r.raycast=function(){};return r}
const save=()=>{SV.ts=Date.now();try{localStorage.setItem('br1',JSON.stringify(SV))}catch(e){}};
const capTotal=()=>Object.values(SV.cap||{}).reduce((a,b)=>a+b,0),capMul=()=>1+.05*Math.min(20,capTotal());
function arc(a,b,c){const l=new THREE.Line(new THREE.BufferGeometry().setFromPoints([a,b]),new THREE.LineBasicMaterial({color:c,transparent:true}));scene.add(l);tr.push({l:l,t:.09})}
function blood(p,n,col){for(let i=0;i<n;i++){const m=new THREE.Mesh(BG,BM);m.position.copy(p);scene.add(m);fx.push({m,v:new V3((Math.random()-.5)*8,Math.random()*7,(Math.random()-.5)*8),t:.8})}}

function mkEnemy(t){const g=new THREE.Group(),mats=[];
const part=(geo,col,em,x,y,z)=>{const m=new THREE.Mesh(geo,new THREE.MeshLambertMaterial({color:col,emissive:em}));m.material.userData.be=em;m.position.set(x,y,z);g.add(m);mats.push(m.material);return m};
const add=(w,h,d,col,x,y,z,em,piv)=>{const geo=new THREE.BoxGeometry(w,h,d);if(piv)geo.translate(0,-h/2,0);return part(geo,col,em===undefined?0x330000:em,x,y,z)};
if(t==='husk'){add(.8,1,.45,0x8a2020,0,1.3,0);add(.42,.42,.42,0x66302a,0,2.05,0);add(.1,.08,.05,0xffee00,-.1,2.08,.22,0xffee00);add(.1,.08,.05,0xffee00,.1,2.08,.22,0xffee00);[-.55,.55].forEach(x=>{add(.22,.9,.22,0x6a1a1a,x,1.7,0,0x330000,1).rotation.x=-1.3});[-.2,.2].forEach(x=>add(.28,.85,.3,0x3a1a1a,x,.43,0))}
else if(t==='shooter'){part(new THREE.SphereGeometry(.6,12,10),0x8a3cff,0x5522aa,0,0,0);part(new THREE.SphereGeometry(.2,8,6),0xffffff,0xffffff,0,0,.55);part(new THREE.TorusGeometry(1,.07,6,20),0x6622cc,0x3311aa,0,0,0).rotation.x=Math.PI/2;part(new THREE.TorusGeometry(.85,.07,6,20),0x6622cc,0x3311aa,0,0,0);for(let i=0;i<4;i++)part(new THREE.ConeGeometry(.14,.7,5),0xcc99ff,0x442288,Math.cos(i*1.57)*.9,0,Math.sin(i*1.57)*.9)}
else if(t==='guard'){add(.9,1.1,.5,0x1d3a7a,0,1.3,0,0x0a1a40);add(.45,.45,.45,0x223355,0,2.1,0);add(.3,.1,.05,0x33ddff,0,2.12,.24,0x33ddff);add(.14,.14,.14,0xff2222,-.12,2.45,0,0xff2222);add(.14,.14,.14,0x2266ff,.12,2.45,0,0x2266ff);[-.6,.6].forEach(x=>{add(.2,.8,.2,0x14285a,x,1.7,0,0x0a1a40,1).rotation.x=-1.4});[-.22,.22].forEach(x=>add(.3,.85,.3,0x102040,x,.43,0))}
else if(t==='tank'){add(1.5,1.5,1.5,0x333333,0,1.2,0,0x111111);add(.8,.8,.8,0x555555,0,2.4,0);add(.2,.2,.2,0xff0000,-.2,2.5,.5,0xff0000);add(.2,.2,.2,0xff0000,.2,2.5,.5,0xff0000);[-.8,.8].forEach(x=>{add(.6,1,.6,0x222222,x,1.5,0,0x000000,1).rotation.x=-1.2});[-.4,.4].forEach(x=>add(.6,1.2,.6,0x1a1a1a,x,.5,0))}
else if(t==='runner'){add(.4,.8,.3,0xffaa00,0,1.1,0,0x552200);add(.25,.25,.25,0xffcc00,0,1.7,0);add(.05,.05,.05,0xffffff,-.08,1.75,.18,0xffffff);add(.05,.05,.05,0xffffff,.08,1.75,.18,0xffffff);[-.25,.25].forEach(x=>{add(.12,.6,.12,0x884400,x,1.2,0,0x220a00,1).rotation.x=-1.6});[-.15,.15].forEach(x=>add(.15,.6,.15,0x552200,x,.35,0))}
else if(t==='brute'){add(1.7,1.7,1,0xb34a00,0,2.1,0,0x331100);add(.7,.6,.6,0x552200,0,3.2,.1);add(.15,.1,.05,0xff3300,-.18,3.25,.42,0xff3300);add(.15,.1,.05,0xff3300,.18,3.25,.42,0xff3300);[-.4,.4].forEach(x=>{part(new THREE.ConeGeometry(.15,.7,5),0xeeeeee,0x444444,x,3.7,.1).rotation.z=x>0?-.4:.4});[-1.1,1.1].forEach(x=>{add(.5,1.5,.5,0x8a3a00,x,2.9,0,0x220a00,1).rotation.x=-.9});[-.4,.4].forEach(x=>add(.6,1.3,.6,0x331100,x,.65,0))}
else if(t==='boss'){add(3,3,3,0xaa0000,0,3,0,0x440000);add(1.5,1.5,1.5,0xff2222,0,5.5,0,0x880000);add(.5,.5,.5,0xffaa00,-.5,5.8,.8,0xffaa00);add(.5,.5,.5,0xffaa00,.5,5.8,.8,0xffaa00);[-2,2].forEach(x=>{part(new THREE.ConeGeometry(.3,1.5,5),0x333333,0x000000,x,6.5,0).rotation.z=x>0?-.5:.5});[-1.5,1.5].forEach(x=>{add(1,3,1,0x880000,x,4.5,0,0x220000,1).rotation.x=-.9});[-.8,.8].forEach(x=>add(1.2,2.5,1.2,0x440000,x,1.5,0))}

if(t!=='shooter'){const rg=ring(t==='boss'?0xff0000:0xff2222);if(t==='brute'||t==='boss')rg.scale.setScalar(t==='boss'?3.5:1.7);g.add(rg)}
const L=lbl(t==='boss'?'БОСС':'ВРАГ',t==='boss'?'#ffdd00':'#ff3b30',t==='boss'?512:256);L.position.y=t==='boss'?8.5:t==='brute'?4.6:t==='shooter'?1.6:2.9;g.add(L);
const B=new THREE.Sprite(new THREE.SpriteMaterial({color:0xff2222,depthTest:false}));B.scale.set(t==='boss'?4:1.8,t==='boss'?.3:.16,1);B.position.y=L.position.y-.45;B.renderOrder=10;B.raycast=function(){};g.add(B);g.userData={mats:mats,bar:B};return g}

function spawn(t){const c=CFG[t],a=Math.random()*6.283,r=20+Math.random()*6;const m=mkEnemy(t);
m.position.set(Math.cos(a)*r,c.y,Math.sin(a)*r);
const waveMulti = 1 + (wave * 0.2); 
const hpMult = DM.hp * waveMulti;
const spMult = DM.hp * (1 + wave * 0.05); 
const dmgMult = DM.d * (1 + wave * 0.1);
const e={m,t,c:c,hp:c.hp*hpMult,cd:1+Math.random()*2,fl:0,mats:m.userData.mats,bar:m.userData.bar,max:c.hp*hpMult, dmg:dmgMult, spd:c.sp*spMult};
m.traverse(o=>{o.userData.e=e});scene.add(m);enemies.push(e)}

function clearEnemies(){enemies.forEach(e=>{blood(e.m.position.clone().add(new V3(0,1.2,0)),6,0x555555);scene.remove(e.m);e.m.traverse(o=>{if(o.geometry)o.geometry.dispose();if(o.material){if(o.material.map)o.material.map.dispose();o.material.dispose()}})});enemies=[];shots.forEach(s=>scene.remove(s.m));shots=[]}

function reset(){enemies.forEach(e=>scene.remove(e.m));shots.forEach(s=>scene.remove(s.m));enemies=[];shots=[];
P.max=100+20*SV.ch.hp;DM=DIFF[SV.diff];run=0;buildLoc(SV.loc||0);alarm=0;pl.color.setHex(0xff6644);Object.assign(P,{hp:P.max,dashes:3,dashT:0,yaw:0,pitch:0});P.pos.set(0,1.6,0);P.vel.set(0,0,0);
wave=0;kills=0;style=0;wt=1;alive=true;started=true;isPvP=false;$('ov').style.display='none'}

function hurt(d){if(!alive||P.dashT>0)return;P.hp-=d;style=Math.max(0,style-35);shake=.3;
const v=$('vig');v.style.opacity=1;setTimeout(()=>v.style.opacity=0,120);
if(P.hp<=0){alive=false;hold=false;SV.best=Math.max(SV.best||0,wave);SV.tk=(SV.tk||0)+kills;save();showMenu('Ты погиб. Волна '+wave+' · убийств '+kills+' · заработано '+run+' монет')}}

function hurtPvP(d){if(!alive||P.dashT>0)return; pvpHp -= d; shake=.3;
const v=$('vig');v.style.opacity=1;setTimeout(()=>v.style.opacity=0,120);
if(pvpHp<=0){ pvpHp=0; alive=false; msg('ТЫ ПРОИГРАЛ!'); pvpRespawn=3; }
if(room && room.open){ try{room.send({type:'hp',hp:pvpHp})}catch(e){} }
}

function damage(e,d){if(e.dead)return;e.hp-=d;e.fl=.08;e.mats.forEach(x=>x.emissive.setHex(0xffffff));
if(e.hp<=0){blood(e.m.position.clone().add(new V3(0,1.2,0)),e.t==='boss'?50:16);scene.remove(e.m);e.m.traverse(o=>{if(o.geometry)o.geometry.dispose();if(o.material){if(o.material.map)o.material.map.dispose();o.material.dispose()}});e.dead=1;enemies.splice(enemies.indexOf(e),1);kills++;
P.hp=Math.min(P.max,P.hp+(e.t==='brute'?25:e.t==='boss'?150:10)+3*SV.ch.bl);
const n=Math.round(({husk:5,shooter:8,brute:20,guard:12,tank:35,runner:15,boss:500})[e.t]*DM.c*capMul());SV.coins+=n;run+=n;style=Math.min(330,style+e.c.pts)}else blood(e.m.position,2)}

function dash(){if(!alive||P.dashes<1||P.dashT>0)return;P.dashes--;P.dashT=.18;const w=wish();if(w.lengthSq()<.01)w.set(-Math.sin(P.yaw),0,-Math.cos(P.yaw));P.dd.copy(w).normalize()}
function jump(){if(P.gnd&&alive){P.vel.y=11;P.gnd=false}}
function wish(){let x=joy.x,y=joy.y;if(keys.KeyA)x-=1;if(keys.KeyD)x+=1;if(keys.KeyW)y-=1;if(keys.KeyS)y+=1;const l=Math.hypot(x,y);if(l>1){x/=l;y/=l}const s=Math.sin(P.yaw),c=Math.cos(P.yaw);return new V3(x*c+y*s,0,-x*s+y*c)}

function fire(){if(cd>0||!alive)return;const w=WP[SV.eq],lv=SV.wl[w.id]||0,dmg=w.dm*(1+.25*lv),big=w.pierce||w.aoe;cd=w.cd;fc++;shake=big?.3:.1;pl.intensity=big?8:4;
const dir=new V3();cam.getWorldDirection(dir);
const st = w.id===18 ? cam.localToWorld(new V3(0.5, -0.3, -0.8)) : cam.localToWorld(new V3(.3,-.3,-.6)); 
const rc=new THREE.Raycaster();
for(let i=0;i<w.pe;i++){const d=dir.clone().add(new V3((Math.random()-.5)*w.sp,(Math.random()-.5)*w.sp,(Math.random()-.5)*w.sp)).normalize();rc.set(cam.position,d);
const hs=rc.intersectObjects(enemies.map(e=>e.m),true).filter(x=>x.distance<(w.rng||99)),h=hs[0];let end=cam.position.clone().addScaledVector(d,h?h.distance:(w.rng||35));
if(w.pierce){end=cam.position.clone().addScaledVector(d,100);const sn=new Set();hs.forEach(x=>{const e=x.object.userData.e;if(e&&!sn.has(e)){sn.add(e);damage(e,dmg)}});if(w.id===18)pl.intensity=20;}
else if(w.aoe){const c=h?h.point.clone():d.y<-.02?cam.position.clone().addScaledVector(d,Math.min(35,-cam.position.y/d.y)):null;if(c){end=c;blood(c,14);enemies.slice().forEach(q=>{const ds=q.m.position.distanceTo(c);if(ds<w.aoe)damage(q,dmg*(1-ds/w.aoe*.6))})}}
else if(w.chain){if(h){let e=h.object.userData.e;const hit=new Set();for(let k=0;k<w.chain&&e;k++){hit.add(e);const p=e.m.position.clone();p.y+=1.2;damage(e,dmg*(1-k*.2));let nx=null,bd=10;enemies.forEach(q=>{if(!hit.has(q)){const dd=q.m.position.distanceTo(e.m.position);if(dd<bd){bd=dd;nx=q}}});if(nx){const q=nx.m.position.clone();q.y+=1.2;arc(p,q,w.col)}e=nx}}}
else if(h)damage(h.object.userData.e,w.id==1?dmg*(h.distance<8?1.2:.7):dmg);
const l=new THREE.Line(new THREE.BufferGeometry().setFromPoints([st,end]),new THREE.LineBasicMaterial({color:w.col,transparent:true,linewidth:w.id===18?3:1}));scene.add(l);tr.push({l:l,t:.09})}
if(isPvP && room && room.open){
  try{room.send({type:'shot', x:P.pos.x, y:P.pos.y, z:P.pos.z, d:dir.clone().toArray()})}catch(e){}
}}

function nextWave(){wave++;wtimer=30;if(wave>1){const b=Math.round(wave*8*DM.c);SV.coins+=b;run+=b;save()}
msg('ВОЛНА '+wave + (wave%10===0?' · БОСС!':''));
const n=Math.min(60,Math.round((3+wave*3)*DM.k));
for(let i=0;i<n;i++){
  const r=Math.random();
  let type='husk';
  if(wave%10===0 && i===0) type='boss';
  else if(wave>=5&&r<.1) type='tank';
  else if(wave>=3&&r<.3) type='runner';
  else if(wave>=3&&r<.5) type='brute';
  else if(wave>=2&&r<.8) type='shooter';
  spawn(type);
}}

function update(dt){
if(cd>0)cd-=dt;if(hold)fire();pl.intensity+=(1.3-pl.intensity)*Math.min(1,dt*15);
if(!alive){
  if(isPvP && pvpRespawn>0){
    pvpRespawn -= dt;
    if(pvpRespawn<=0){ pvpHp=100; alive=true; P.pos.set(0,1.6,0); msg('В БОЙ!'); if(room && room.open){try{room.send({type:'hp',hp:100})}catch(e){}} }
  }
  return;
}
P.dashes=Math.min(3,P.dashes+dt/1.8);
const w=wish();
if(P.dashT>0){P.dashT-=dt;P.vel.set(P.dd.x*38,0,P.dd.z*38)}
else{const k=Math.min(1,dt*(P.gnd?14:3.5));const sp=13*(1+.06*SV.ch.sp);P.vel.x+=(w.x*sp-P.vel.x)*k;P.vel.z+=(w.z*sp-P.vel.z)*k;P.vel.y-=30*dt}
P.pos.addScaledVector(P.vel,dt);
if(P.pos.y<=1.6){P.pos.y=1.6;P.vel.y=0;P.gnd=true}
P.pos.x=Math.max(-R,Math.min(R,P.pos.x));P.pos.z=Math.max(-R,Math.min(R,P.pos.z));
pillars.forEach(([x,z])=>{const dx=P.pos.x-x,dz=P.pos.z-z,d=Math.hypot(dx,dz);if(d<2.1){P.pos.x=x+dx/d*2.1;P.pos.z=z+dz/d*2.1}});
cam.position.copy(P.pos);
if(shake>0){shake-=dt;cam.position.x+=(Math.random()-.5)*shake;cam.position.y+=(Math.random()-.5)*shake}
cam.rotation.set(P.pitch,P.yaw,0);
cam.fov+=((P.dashT>0?95:80)-cam.fov)*Math.min(1,dt*12);cam.updateProjectionMatrix();
if(++fr%3==0){cam.getWorldDirection(DV);RC2.set(cam.position,DV);$('cross').style.borderColor=RC2.intersectObjects(enemies.map(e=>e.m),true)[0]?'#ff3b30':'#fff9'}
enemies.forEach(e=>{const m=e.m,dx=P.pos.x-m.position.x,dz=P.pos.z-m.position.z,d=Math.hypot(dx,dz)||1;
e.bar.scale.x=Math.max(.02,e.hp/e.max)*(e.t==='boss'?4:1.8);if(e.fl>0){e.fl-=dt;if(e.fl<=0)e.mats.forEach(x=>x.emissive.setHex(x.userData.be))}
if(e.t==='shooter'||e.t==='guard'){const mv=d>14?1:d<9?-1:0;m.position.x+=dx/d*e.c.sp*mv*dt;m.position.z+=dz/d*e.c.sp*mv*dt;
if(e.t==='shooter'){m.position.y=e.c.y+Math.sin(performance.now()/300)*.3;m.rotation.y+=dt*2}else m.rotation.y=Math.atan2(dx,dz);e.cd-=dt;
if(e.cd<=0){e.cd=e.t==='guard'?1.3:2.2;const s=new THREE.Mesh(new THREE.SphereGeometry(.35,8,6),new THREE.MeshBasicMaterial({color:0xcc66ff}));
s.position.copy(m.position);s.position.y+=e.t==='guard'?1.4:0;const v=P.pos.clone().sub(m.position).normalize().multiplyScalar(15);scene.add(s);shots.push({m:s,v,t:5,dmg:e.dmg})}}
else{m.position.x+=dx/d*e.spd*dt;m.position.z+=dz/d*e.spd*dt;m.rotation.y=Math.atan2(dx,dz);e.cd-=dt;
const rr=e.t==='brute'?2.8:e.t==='boss'?4.5:e.t==='tank'?2.5:1.7;
if(d<rr&&Math.abs(P.pos.y-1.6)<2&&e.cd<=0){e.cd=.8;hurt(e.dmg*(e.t==='brute'?22:e.t==='boss'?80:e.t==='tank'?30:10))}}});

for(let i=0;i<enemies.length;i++)for(let j=i+1;j<enemies.length;j++){const a=enemies[i].m.position,b=enemies[j].m.position,dx=a.x-b.x,dz=a.z-b.z,d=Math.hypot(dx,dz);
if(d<2.5&&d>.01){const p=(2.5-d)*.5/d;a.x+=dx*p;a.z+=dz*p;b.x-=dx*p;b.z-=dz*p}}

for(let i=shots.length-1;i>=0;i--){const s=shots[i];s.m.position.addScaledVector(s.v,dt);s.t-=dt;
if(s.m.position.distanceTo(P.pos)<1.1){hurt(s.dmg);s.t=0}if(s.t<=0){scene.remove(s.m);s.m.geometry.dispose();s.m.material.dispose();shots.splice(i,1)}}
for(let i=fx.length-1;i>=0;i--){const f=fx[i];f.v.y-=20*dt;f.m.position.addScaledVector(f.v,dt);f.t-=dt;
if(f.m.position.y<.1){f.m.position.y=.1;f.v.multiplyScalar(.3)}if(f.t<=0){scene.remove(f.m);fx.splice(i,1)}}
for(let i=tr.length-1;i>=0;i--){const t=tr[i];t.t-=dt;t.l.material.opacity=t.t/.09;if(t.t<=0){scene.remove(t.l);t.l.geometry.dispose();tr.splice(i,1)}}
if(!isPvP){
  if(enemies.length&&wtimer>0){wtimer-=dt;if(wtimer<=0){clearEnemies();msg('ВОЛНА '+wave+' ЗАВЕРШЕНА');wt=2.5}}
  if(!enemies.length){wt-=dt;if(wt<=0){nextWave();wt=2.5}}
}
let rk=0;TH.forEach((t,i)=>{if(style>=t)rk=i});style=Math.max(0,style-(4+rk*5)*dt);
if(msgT>0){msgT-=dt;if(msgT<=0)$('msg').style.opacity=0}
if(zone&&zring){const dz=Math.hypot(P.pos.x-zpos.x,P.pos.z-zpos.z),on=dz<5&&P.pos.y<4;zp=on?Math.min(100,zp+12*dt):Math.max(0,zp-3*dt);const zc=on?0xffcc33:0x33ccff;zone.material.color.setHex(zc);zring.material.color.setHex(zc);$('cap').textContent=zp>0?'ЗАХВАТ '+Math.floor(zp)+'%':'ЗОНА ЗАХВАТА · '+Math.round(dz)+' м';if(zp>=100)captured();if(alarm>0){alarm-=dt;pl.color.setHex(Math.floor(alarm*4)%2?0xff3333:0x3366ff);if(alarm<=0)pl.color.setHex(0xff6644)}}
if(isPvP){ $('hpf').style.width=Math.max(0,pvpHp)+'%'; $('info').textContent='ПВП ДУЭЛЬ · ТЫ: '+Math.ceil(pvpHp)+' · ВРАГ: '+Math.ceil(oppHp); } 
else { $('hpf').style.width=Math.max(0,P.hp/P.max*100)+'%'; $('info').textContent='ВОЛНА '+wave+' · ⏱'+Math.ceil(Math.max(0,wtimer))+' · '+kills+' · 👥'+(allies.size+1); }
document.querySelectorAll('#dash b').forEach((b,i)=>b.style.width=Math.max(0,Math.min(1,P.dashes-i))*100+'%');
const rl=$('rl');rl.textContent=RK[rk];rl.style.color=RC[rk];$('rb').style.color=RC[rk];
const nx=TH[rk+1]||330;$('rbf').style.width=Math.min(100,(style-TH[rk])/(nx-TH[rk])*100)+'%';
$('wn').textContent=WP[SV.eq].n+' · '+WP[SV.eq].t+' · '+SV.coins+' мон.'}

const pad=$('pad'),joyEl=$('joy'),knob=$('knob');let jid=null,lid=null,jo=null,lp=null;
pad.addEventListener('pointerdown',e=>{pad.setPointerCapture(e.pointerId);
if(e.clientX<innerWidth*.45&&jid===null){jid=e.pointerId;jo={x:e.clientX,y:e.clientY};joyEl.style.display='block';joyEl.style.left=jo.x+'px';joyEl.style.top=jo.y+'px'}
else if(lid===null){lid=e.pointerId;lp={x:e.clientX,y:e.clientY}}
if(e.pointerType==='mouse'&&document.pointerLockElement!==pad){pad.requestPointerLock&&pad.requestPointerLock()}else if(e.pointerType==='mouse')hold=true});
pad.addEventListener('pointermove',e=>{
if(e.pointerType==='mouse'&&document.pointerLockElement===pad){P.yaw-=e.movementX*.0025;P.pitch=Math.max(-1.4,Math.min(1.4,P.pitch-e.movementY*.0025));return}
if(e.pointerId===jid){let dx=e.clientX-jo.x,dy=e.clientY-jo.y;const l=Math.hypot(dx,dy),m=50;if(l>m){dx*=m/l;dy*=m/l}joy.x=dx/m;joy.y=dy/m;knob.style.transform='translate('+dx+'px,'+dy+'px)'}
else if(e.pointerId===lid){P.yaw-=(e.clientX-lp.x)*.006;P.pitch=Math.max(-1.4,Math.min(1.4,P.pitch-(e.clientY-lp.y)*.006));lp={x:e.clientX,y:e.clientY}}});
const up=e=>{if(e.pointerId===jid){jid=null;joy.x=joy.y=0;joyEl.style.display='none';knob.style.transform=''}if(e.pointerId===lid)lid=null;if(e.pointerType==='mouse')hold=false};
pad.addEventListener('pointerup',up);pad.addEventListener('pointercancel',up);
const bind=(id,on,off)=>{const b=$(id);b.addEventListener('pointerdown',e=>{e.preventDefault();b.classList.add('on');on()});['pointerup','pointercancel','pointerleave'].forEach(t=>b.addEventListener(t,()=>{b.classList.remove('on');off&&off()}))};
bind('bf',()=>hold=true,()=>hold=false);bind('bd',dash);bind('bj',jump);
addEventListener('keydown',e=>{keys[e.code]=1;if(e.code==='Space')jump();if(e.code==='ShiftLeft'||e.code==='ControlLeft')dash()});
addEventListener('keyup',e=>keys[e.code]=0);
const sb=$('go');let busy=0;const begin=e=>{if(e)e.preventDefault();if(busy)return;busy=1;setTimeout(()=>busy=0,500);try{reset()}catch(err){$('ovt').textContent='Ошибка: '+err.message;$('ov').style.display='flex'}};sb.addEventListener('click',begin);sb.addEventListener('pointerup',begin);
document.addEventListener('contextmenu',e=>e.preventDefault());

function nextWeapon(){const owned = SV.own.sort((a,b)=>a-b); if(owned.length < 2) { msg('Купи оружие в магазине!'); return; } let idx = owned.indexOf(SV.eq); idx = (idx + 1) % owned.length; SV.eq = owned[idx]; msg(WP[SV.eq].n + ' экипирован'); save();}
bind('bw',nextWeapon);

function moveZone(){let x=0,z=0,ok=0;for(let i=0;i<30&&!ok;i++){x=(Math.random()-.5)*36;z=(Math.random()-.5)*36;ok=pillars.every(p=>Math.hypot(p[0]-x,p[1]-z)>6)&&Math.hypot(x,z)>8}zpos.set(x,0,z);if(zone){zone.position.set(x,6,z);zring.position.set(x,.06,z)}zp=0}
function buildLoc(i){if(LG)scene.remove(LG);LG=new THREE.Group();scene.add(LG);const L=LOC[i]||LOC[0];scene.background.setHex(L.bg);scene.fog.color.setHex(L.bg);floor.material.color.setHex(L.fl);wm.color.setHex(L.wl||0x3a1212);
const B=(w,h,d,c,x,y,z,e)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),new THREE.MeshLambertMaterial({color:c,emissive:e||0}));m.position.set(x,y,z);LG.add(m);return m};
if(i==1){for(let k=-24;k<=24;k+=6)B(3,.05,.6,0xdddddd,k,.03,0);B(60,.05,.5,0xffcc00,0,.03,12);B(60,.05,.5,0xffcc00,0,.03,-12);B(70,16,12,0x56677a,0,8,-48);B(70,.5,.5,0x66ccff,0,12,-41.8,0x2288cc);B(5,30,5,0x8899aa,45,15,-45);B(8,4,8,0x66ccff,45,31,-45,0x2288cc);B(26,3.5,3.5,0xcccccc,-38,5,42);B(5,.5,24,0xbbbbbb,-36,4.5,42);B(3,6,.5,0xbbbbbb,-50,8,42)}
else if(i==2){[-40,-14,14,40].forEach((x,k)=>{const c=new THREE.Mesh(new THREE.CylinderGeometry(3,4,30+k*4,10),new THREE.MeshLambertMaterial({color:0x4a3322}));c.position.set(x,15+k*2,-45);LG.add(c);B(3.4,1.5,3.4,0xff4400,x,31+k*4,-45,0xff4400)});B(80,10,10,0x3a2a22,0,5,48);for(let k=-20;k<=20;k+=10)B(.5,.05,60,0xffaa00,k,.03,0,0x442200)}
if(i==3){B(8,.05,44,0x7a1018,0,.03,0);B(60,.5,60,0x1a0f0a,0,10.5,0);for(let k=-24;k<=24;k+=6){[-28.6,28.6].forEach(x=>{B(1.2,6,4.5,0x4a2c14,x,3,k);B(1.3,.5,4,0x8a1a1a,x,4.4,k);B(1.3,.5,4,0x1a4a6a,x,2.2,k)})}[-18,-6,6,18].forEach(x=>{B(3,6,.2,0x88aaff,x,5,-29.8,0x3355aa);B(3,6,.2,0x88aaff,x,5,29.8,0x3355aa)});[[-14,0],[14,0],[0,14],[0,-14]].forEach(([x,z])=>{B(.12,3,.12,0x222222,x,9,z);const t=new THREE.Mesh(new THREE.TorusGeometry(1.6,.12,6,16),new THREE.MeshLambertMaterial({color:0x8a6a2a,emissive:0x221100}));t.rotation.x=Math.PI/2;t.position.set(x,7.5,z);LG.add(t);for(let a=0;a<6;a++)B(.2,.5,.2,0xffe9a0,x+Math.cos(a*1.047)*1.6,7.9,z+Math.sin(a*1.047)*1.6,0xffcc66)})}
if(i==4){
B(60,.2,1,0x3a2a1a,0,.1,-28);B(60,.2,1,0x3a2a1a,0,.1,28);B(1,.2,60,0x3a2a1a,-28,.1,0);B(1,.2,60,0x3a2a1a,28,.1,0);
[-27,27].forEach(z=>B(56,4,.2,0x5a3a20,0,2,z));
B(58,.3,58,0x2a1a10,0,10,0);for(let k=-24;k<=24;k+=8)B(.6,.6,56,0x3a2414,k,9.6,0);
B(16,4,.3,0x143a1a,-10,5,-27.5,0x0a2a12);B(17,.4,.5,0x6a4a2a,-10,7.2,-27.4);
for(let r=0;r<4;r++)for(let c=0;c<4;c++){const x=-12+c*7,z=-8+r*6;B(3,.2,1.6,0x7a5a3a,x,1.8,z);B(2.6,.8,.15,0x5a3a20,x,1.2,z-.7);B(.2,.9,.2,0x3a2414,x-1.3,.9,z);B(.2,.9,.2,0x3a2414,x+1.3,.9,z)}
B(4,.2,2,0x6a4a2a,-10,1.8,-24);B(.3,1.8,.3,0x3a2414,-12,1.9,-24);B(.3,1.8,.3,0x3a2414,-8,1.9,-24);
{const gl=new THREE.Mesh(new THREE.SphereGeometry(.6,16,12),new THREE.MeshLambertMaterial({color:0x2a6a8a,emissive:0x0a2a3a}));gl.position.set(-10,2.8,-24);LG.add(gl);const st=new THREE.Mesh(new THREE.CylinderGeometry(.05,.05,.8,6),new THREE.MeshLambertMaterial({color:0x6a4a2a}));st.position.set(-10,2.3,-24);LG.add(st)}
for(let k=-20;k<=20;k+=3){B(.8,4,.15,0x1a4a6a,27,2.5,k);B(.85,.1,.18,0x88ccff,27,4.5,k,0x336699);B(.15,.15,.15,0xeeeeee,26.6,2.5,k)}
for(let k=-20;k<=20;k+=5){B(.8,8,.8,0x5a3a20,-22,4,k);B(1,1,1,0x7a5a3a,-22,8.4,k)}
B(14,.05,14,0x6a4a20,18,.05,18);B(14,.05,.3,0xeeeeee,18,.1,11);B(14,.05,.3,0xeeeeee,18,.1,25);B(.3,.05,14,0xeeeeee,11,.1,18);B(.3,.05,14,0xeeeeee,25,.1,18);
[[18,12,18,1.5],[18,24,18,-1.5]].forEach(([x,y,z,s])=>{B(.2,4,.2,0x888888,x,y-2,z-s);B(1.2,.1,1.2,0xff6622,x,y,z-s)});
for(let k=-3;k<=3;k+=2)B(6,.4,1,0x8a5a2a,18,.2,k*2+18);
[-15,0,15].forEach(x=>[-15,0,15].forEach(z=>{B(.4,.4,.4,0xffeeaa,x,9.4,z,0xffcc66)}));
B(2,2,.8,0x5a3a20,22,1,14);B(2.2,.3,1,0x7a5a3a,22,2.1,14);
}
if(i==5){for(let k=-20;k<=20;k+=5){B(2,20,2,0x111122,k,10,0,0x2222aa);B(4,4,4,0x00ffff,k,20,0,0x00aaaa)}B(60,.1,.5,0xff00ff,0,.05,15,0xaa00aa);B(60,.1,.5,0xff00ff,0,.05,-15,0xaa00aa)}
if(i==6){for(let k=-20;k<=20;k+=10){const c=new THREE.Mesh(new THREE.ConeGeometry(3,6,4),new THREE.MeshLambertMaterial({color:0x8a5a2a}));c.position.set(k,3,k);LG.add(c)}B(60,.1,60,0xc2a070,0,0,0)}

zone=new THREE.Mesh(new THREE.CylinderGeometry(5,5,12,24,1,true),new THREE.MeshBasicMaterial({color:0x33ccff,transparent:true,opacity:.18,side:THREE.DoubleSide,depthWrite:false}));zone.raycast=function(){};LG.add(zone);zring=ring(0x33ccff);zring.scale.setScalar(4.1);LG.add(zring);moveZone()}
function captured(){SV.cap=SV.cap||{};const l=SV.loc||0;SV.cap[l]=(SV.cap[l]||0)+1;const b=Math.round(80*DM.c*(1+wave*.1));SV.coins+=b;run+=b;save();moveZone();alarm=12;msg('ЗАХВАТ! +'+b+' · ПРИБЫЛА ОХРАНА');for(let i=0;i<Math.min(12,4+Math.round(wave*1.2*DM.k));i++)spawn('guard')}
function drawLoc(){const d=$('locs');d.innerHTML='';LOC.forEach((x,i)=>{const b=document.createElement('button');b.className='opt'+((SV.loc||0)===i?' on':'');b.textContent=x.n+(SV.cap&&SV.cap[i]?' ★'+SV.cap[i]:'');b.onclick=()=>{SV.loc=i;buildLoc(i);save();drawLoc()};d.appendChild(b)})}
function drawDiff(){const d=$('dif');d.innerHTML='';DIFF.forEach((x,i)=>{const b=document.createElement('button');b.className='opt'+(SV.diff===i?' on':'');b.textContent=x.n;b.onclick=()=>{SV.diff=i;save();drawDiff()};d.appendChild(b)})}
function showMenu(txt){$('ov').style.display='flex';$('cn').textContent=SV.coins;if(txt)$('ovt').textContent=txt;$('ovt').style.display='';$('pan').style.display='none';drawDiff();drawLoc();$('st').textContent='Рекорд: волна '+(SV.best||0)+' · убийств: '+(SV.tk||0)+' · захватов: '+capTotal()}

function shop(){const p=$('pan');p.style.display='block';$('ovt').style.display='none';p.innerHTML='';
const row=(t,s,txt,fn,dis)=>{const r=document.createElement('div');r.className='it';const l=document.createElement('div');l.innerHTML='<b></b><small></small>';l.firstChild.textContent=t;l.lastChild.textContent=s;const b=document.createElement('button');b.textContent=txt;b.disabled=!!dis;b.onclick=()=>{fn();save();$('cn').textContent=SV.coins;shop()};r.append(l,b);p.appendChild(r)};
WP.forEach(w=>{const own=SV.own.includes(w.id),lv=SV.wl[w.id]||0,st=w.t+' · урон '+Math.round(w.dm*(1+.25*lv))+(w.pe>1?'×'+w.pe:'')+' · ур.'+lv;
if(!own)row(w.n,st,'Купить '+w.p,()=>{SV.coins-=w.p;SV.own.push(w.id);SV.eq=w.id;save()},SV.coins<w.p);
else{const c=Math.max(60,Math.round(w.p/2))*(lv+1);if(lv>=25)row(w.n,st,'МАКС',()=>{},1);else row(w.n,st,'+ур. '+c,()=>{SV.coins-=c;SV.wl[w.id]=lv+1;save()},SV.coins<c)}});
CH.forEach(c=>{const l=SV.ch[c.k],cost=c.b*(l+1);if(l>=25)row(c.n,c.d+' · ур.'+l,'МАКС',()=>{},1);else row(c.n,c.d+' · ур.'+l,'+ур. '+cost,()=>{SV.coins-=cost;SV.ch[c.k]=l+1;save()},SV.coins<cost)});
const bk=document.createElement('button');bk.className='sm';bk.textContent='НАЗАД';bk.onclick=()=>showMenu();p.appendChild(bk)}

// --- PEERJS МУЛЬТИПЛЕЕР ---
let peer=null, conn=null, isHost=false;

function initPeer(callback) {
  if (peer) { callback(peer); return; }
  const id = 'br-' + Math.random().toString(36).substr(2, 9);
  peer = new Peer(id);
  peer.on('open', (myId) => {
    console.log('PeerJS ID:', myId);
    if (callback) callback(peer);
  });
  peer.on('error', (err) => {
    console.error('PeerJS error:', err);
    msg('Ошибка сети: ' + err.type);
  });
}

function createRoom() {
  initPeer((p) => {
    isHost = true;
    lobbyCode = p.id.replace('br-', '').toUpperCase();
    updateLobbyUI('Лобби создано! Код: ' + lobbyCode);
    p.on('connection', (c) => {
      conn = c;
      conn.on('open', () => {
        msg('Друг подключился!');
        updateLobbyUI('Друг подключен!');
        if (isPvP) { reset(); alive = true; pvpHp = 100; oppHp = 100; P.pos.set(0, 1.6, 0); msg('ПВП ДУЭЛЬ!'); }
      });
      conn.on('data', handleNetData);
      conn.on('close', () => { msg('Друг отключился'); updateLobbyUI('Друг отключился'); conn = null; });
    });
  });
}

function joinRoom(code) {
  initPeer((p) => {
    isHost = false;
    const hostId = 'br-' + code.toLowerCase();
    conn = p.connect(hostId, { reliable: true });
    conn.on('open', () => {
      msg('Подключено к лобби!');
      updateLobbyUI('Подключено к лобби ' + code);
      if (isPvP) { reset(); alive = true; pvpHp = 100; oppHp = 100; P.pos.set(0, 1.6, 0); msg('ПВП ДУЭЛЬ!'); }
    });
    conn.on('data', handleNetData);
    conn.on('error', (err) => { msg('Не удалось подключиться: ' + err); });
    conn.on('close', () => { msg('Соединение потеряно'); conn = null; });
  });
}

function handleNetData(data) {
  if (data.type === 'pos') {
    // Обновляем позицию союзника/врага
    const a = allies.get('remote') || (() => {
      const g = mkAlly(isPvP ? 'Враг' : 'Друг');
      scene.add(g);
      const obj = { g: g, f: 0 };
      allies.set('remote', obj);
      return obj;
    })();
    a.g.position.lerp(new V3(data.x, data.y - 1.6, data.z), 0.3);
    a.g.rotation.y = data.yaw + Math.PI;
    a.g.visible = data.alive;
  } else if (data.type === 'hp') {
    oppHp = data.hp;
  } else if (data.type === 'shot' && isPvP) {
    const s0 = new V3(data.x, data.y, data.z);
    const d = new V3(data.d[0], data.d[1], data.d[2]);
    const end = s0.clone().addScaledVector(d, 50);
    const l = new THREE.Line(new THREE.BufferGeometry().setFromPoints([s0, end]), new THREE.LineBasicMaterial({ color: 0xff0000, transparent: true }));
    scene.add(l); tr.push({ l: l, t: .09 });
    // Проверка попадания
    const ray = new THREE.Raycaster(s0, d);
    if (ray.ray.distanceToPoint(P.pos) < 1.2) hurtPvP(10);
  } else if (data.type === 'chat') {
    msg('Друг: ' + data.text);
  }
}

function updateLobbyUI(text) {
  const el = $('lst');
  if (el) el.textContent = text;
  const lk = $('lk');
  if (lk && lobbyCode) lk.value = location.href.split('#')[0] + '#room=' + lobbyCode;
}

const SHARE = location.href.split('#')[0];
function lobbyUI(isPvPmode){const p=$('pan');p.style.display='block';$('ovt').style.display='none';
p.innerHTML=`<div style='text-align:center'>
<div id='lst' style='margin:8px 0;font-size:15px'>${peer ? 'Готов' : 'Нажми "СОЗДАТЬ ЛОББИ"'}</div>
<input id='lk' readonly placeholder='ссылка появится после создания лобби' style='width:100%;padding:10px;background:#0a2a14;color:#8fffb0;border:2px solid #1f9d4a;text-align:center;word-break:break-all;font-family:system-ui;font-size:12px'>
<div class='row'><button class='sm' id='ls'>📋 СКОПИРОВАТЬ ССЫЛКУ</button><button class='sm' id='ln'>🔄 СОЗДАТЬ ЛОББИ</button></div>
<div style='margin:10px 0'><input id='li' maxlength='6' placeholder='КОД ДРУГА' style='width:130px;font:inherit;font-size:18px;text-align:center;padding:6px;-webkit-user-select:text;user-select:text;background:#222;color:#fff;border:2px solid #ffd24a'> <button class='sm' id='lj'>ВОЙТИ</button></div>
<button class='sm' id='lb'>НАЗАД</button></div>`;
$('ls').onclick=()=>{const u=$('lk').value;if(!u)return;$('lk').select();if(navigator.share)navigator.share({title:'BLOODRUSH',text:'Го в BLOODRUSH!',url:u}).catch(()=>{});else{try{navigator.clipboard.writeText(u)}catch(e){};msg('ССЫЛКА СКОПИРОВАНА')}};
$('ln').onclick=()=>createRoom();
$('lj').onclick=()=>{const c=$('li').value.trim().toUpperCase();if(/^[A-Z0-9]{3,6}$/.test(c))joinRoom(c);else $('lst').textContent='Код: 3–6 букв или цифр'};
$('lb').onclick=()=>showMenu();
// Автосоздание/вход по хэшу
const m = location.hash.match(/room=([A-Z0-9]{3,6})/);
if(m) joinRoom(m[1]);
}

$('bigmp').onclick=()=>{isPvP=false;lobbyUI(false)};
$('pvpbtn').onclick=()=>{isPvP=true;lobbyUI(true)};

function checkFriendInvite(){
  const hash = location.hash;
  if(hash.startsWith('#friend=')) {
    const name = decodeURIComponent(hash.replace('#friend=', ''));
    if(!SV.friends.includes(name) && name !== SV.myName) {
      setTimeout(() => {
        if(confirm(`Игрок ${name} хочет добавить тебя в друзья. Принять?`)) {
          SV.friends.push(name); save(); alert('Теперь вы друзья!'); location.hash = '';
        }
      }, 1000);
    }
  }
}

function mkAlly(n){const g=new THREE.Group(),mt=(c,e)=>new THREE.MeshLambertMaterial({color:c,emissive:e}),ad=(geo,m,x,y,z)=>{const o=new THREE.Mesh(geo,m);o.position.set(x,y,z);g.add(o);return o};
ad(new THREE.CylinderGeometry(.4,.45,1.3,8),mt(0x1f9d4a,0x0a4a20),0,1,0);ad(new THREE.SphereGeometry(.32,10,8),mt(0x3be07a,0x167a3a),0,1.9,0);ad(new THREE.BoxGeometry(.4,.12,.2),mt(0x111111,0x00ff88),0,1.92,.28);ad(new THREE.BoxGeometry(.14,.14,.8),mt(0x444444,0x112211),.4,1.2,.4);ad(new THREE.BoxGeometry(.3,.4,.3),mt(0x14702f,0x062a12),-.2,.2,0);ad(new THREE.BoxGeometry(.3,.4,.3),mt(0x14702f,0x062a12),.2,.2,0);
g.add(ring(isPvP?0xff0000:0x33ff88));const L=lbl(isPvP?'ВРАГ':'СВОЙ · '+n,isPvP?'#ff3b30':'#3dff8a',512);L.position.y=2.8;g.add(L);return g}

function net(dt) {
  if (!conn || !conn.open) return;
  if (++fr % 3 === 0) {
    try {
      conn.send({ type: 'pos', x: P.pos.x, y: P.pos.y, z: P.pos.z, yaw: P.yaw, alive: alive ? 1 : 0 });
    } catch (e) {}
  }
}

function tut(i){const p=$('pan'),c=TUT[i];p.style.display='block';$('ovt').style.display='none';
p.innerHTML=`<div style='text-align:center'>
<div class='stepnum'>ШАГ ${i+1} / ${TUT.length}</div>
<h2 style='margin:4px 0;color:#ff5a3c;font-family:Impact,sans-serif;letter-spacing:2px'>${c.t}</h2>
${c.s}<p style='margin:8px 0;font-size:13px;line-height:1.5'>${c.x}</p>
<div id='tutprog'>${TUT.map((_,k)=>`<div class='dot${k===i?' on':''}'></div>`).join('')}</div>
<div id='tutnav'><button class='sm' id='tp' ${i===0?'disabled':''}>◀</button><button class='sm' id='tn'>${i<TUT.length-1?'ДАЛЕЕ ▶':'ГОТОВО ✓'}</button></div>
</div>`;
$('tp').onclick=()=>tut(Math.max(0,i-1));$('tn').onclick=()=>{if(i<TUT.length-1)tut(i+1);else{SV.tut=1;save();showMenu()}}}

const sv=b=>`<svg viewBox='0 0 340 180' style='width:100%;max-width:360px;background:#1a0a0a;border:2px solid #fff3;border-radius:8px'>${b}</svg>`,tx=(x,y,s,c,sz)=>`<text x='${x}' y='${y}' fill='${c||'#fff'}' font-size='${sz||11}' text-anchor='middle' font-family='sans-serif'>${s}</text>`;
const TUT=[
{t:'УПРАВЛЕНИЕ',s:sv(`<circle cx='60' cy='110' r='32' fill='none' stroke='#fff6' stroke-width='3'/><circle cx='60' cy='110' r='12' fill='#fff8'/>${tx(60,160,'ДЖОЙСТИК')}<path d='M190 55l18-9v18z M260 55l-18-9v18z' fill='#fff6'/>${tx(225,90,'СВАЙП = ОБЗОР')}<circle cx='290' cy='130' r='24' fill='#ff2a1a99'/>${tx(290,168,'ОГОНЬ')}<circle cx='230' cy='140' r='14' fill='#33ccff66'/>${tx(230,168,'РЫВОК')}<circle cx='170' cy='140' r='12' fill='#ffaa0066'/>${tx(170,168,'СМЕНА')}`),x:'Левая половина экрана — джойстик, правая — обзор камеры. ОГОНЬ можно держать. РЫВОК даёт неуязвимость. ПРЫЖОК и СМЕНА — рядом.'},
{t:'ДРУЗЬЯ',s:sv(`<rect x='50' y='50' width='30' height='66' fill='#1f9d4a'/>${tx(65,38,'ТЫ','#3dff8a')}<rect x='260' y='50' width='30' height='66' fill='#3dff8a'/>${tx(275,38,'ДРУГ','#3dff8a')}<circle cx='170' cy='90' r='20' fill='none' stroke='#ffd24a' stroke-width='3'/>${tx(170,95,'+','#ffd24a',24)}`),x:'Кнопка «ДРУЗЬЯ»: добавляй друзей по имени. Скидывай им ссылку-приглашение, они подтвердят, и вы сможете приглашать друг друга в игру (ПВП или кооп).'},
{t:'ПВП ДУЭЛЬ',s:sv(`<rect x='50' y='50' width='30' height='66' fill='#1f9d4a'/>${tx(65,38,'ТЫ','#3dff8a')}<rect x='260' y='50' width='30' height='66' fill='#aa2222'/>${tx(275,38,'ВРАГ','#ff3b30')}<path d='M90 80h160' stroke='#ff0000' stroke-width='3' stroke-dasharray='6 4'/>${tx(170,68,'ЛАЗЕР','#ff0000')}`),x:'Режим ПВП: нажми «ПВП ДУЭЛЬ», создай лобби и скинь ссылку другу. Вы появитесь на арене друг против друга. Стреляй, попадай, уворачивайся! У кого кончится здоровье — тот проиграл.'},
{t:'ОРУЖИЕ И ПРОКАЧКА',s:sv(`<circle cx='80' cy='80' r='28' fill='#ffd24a'/>${tx(80,86,'МОНЕТЫ','#331')}<rect x='140' y='55' width='50' height='10' fill='#ff2a1a'/><rect x='140' y='75' width='80' height='10' fill='#ff7733'/><rect x='140' y='95' width='120' height='10' fill='#cc66ff'/><rect x='140' y='115' width='160' height='10' fill='#66ccff'/>${tx(170,145,'СЛАБОЕ · СИЛЬНОЕ · МОЩНОЕ')}`),x:'19 видов оружия, включая супер-пушку «РУКА БОГА» за 20.000 монет. В магазине можно качать оружие и персонажа до 25 уровня.'},
{t:'БОСС И ВОЛНЫ',s:sv(`<rect x='140' y='40' width='60' height='80' fill='#ff0000'/>${tx(170,30,'БОСС','#ff0000')}<rect x='150' y='130' width='40' height='8' fill='#f00'/>${tx(170,160,'КАЖДЫЕ 10 ВОЛН','#ffd24a')}`),x:'С каждой волной враги становятся сильнее и быстрее. Каждые 10 волн появляется БОСС с огромным запасом здоровья.'},
{t:'КАРТЫ',s:sv(`<rect x='30' y='30' width='280' height='120' fill='#3a2a1a'/><rect x='50' y='45' width='70' height='30' fill='#143a1a'/>${tx(85,63,'ДОСКА','#8fffb0',10)}<rect x='160' y='50' width='40' height='22' fill='#7a5a3a'/><rect x='210' y='50' width='40' height='22' fill='#7a5a3a'/><rect x='260' y='50' width='40' height='22' fill='#7a5a3a'/><circle cx='240' cy='120' r='25' fill='none' stroke='#33ccff' stroke-width='3'/>${tx(240,120,'ЗОНА','#5fd7ff',10)}`),x:'Локации: Арена, Аэропорт, Завод, Замок, Школа, Киберпанк (неон) и Пустыня (пирамиды). В каждой есть точка захвата.'}
];

$('bshop').onclick=shop;$('blob').onclick=()=>{isPvP=false;lobbyUI(false)};$('btut').onclick=()=>tut(0);
buildLoc(SV.loc||0);showMenu();if(!SV.tut)tut(0);
checkFriendInvite();
let last=performance.now();
(function loop(n){requestAnimationFrame(loop);const dt=Math.min(.05,(n-last)/1000);last=n;update(dt);net(dt);rd.render(scene,cam)})(last);

// --- КОДЫ ---
function codeUI(){
  const p=$('pan');p.style.display='block';$('ovt').style.display='none';
  p.innerHTML = `<div style='text-align:center'><h3 style='color:#ffd24a'>ВВЕДИ ПРОМОКОД</h3>
  <div style='margin:10px 0; font-size:12px; color:#aaa'>Осталось активаций кода "Тимур лучший": <b>${3 - SV.codeT}</b></div>
  <input id='cin' placeholder='ТУТ КОД' style='width:100%; padding:10px; font:inherit; font-size:20px; text-align:center; background:#222; color:#fff; border:2px solid #ffd24a; margin-bottom:10px'/>
  <div style='display:flex; gap:5px'><button class='sm' id='cok' style='flex:1; background:#1f9d4a'>АКТИВИРОВАТЬ</button><button class='sm' id='cb' style='flex:1'>НАЗАД</button></div></div>`;
  $('cb').onclick = () => showMenu();
  $('cok').onclick = () => {
    const code = $('cin').value.trim().toUpperCase();
    if(code === 'ТИМУР ЛУЧШИЙ' || code === 'ТИМУРЛУЧШИЙ') {
       if(SV.codeT < 3) {
          SV.codeT++;
          SV.coins += 25000;
          save();
          msg('+25 000 МОНЕТ!');
          showMenu();
       } else {
          alert('Этот код уже активирован 3 раза. Больше нельзя.');
       }
    } else if(code === 'BLOODRUSH') {
       SV.coins += 5000; save(); msg('+5 000 МОНЕТ!'); showMenu();
    } else if(code === 'BOSS') {
       if(!SV.own.includes(18)) { SV.own.push(18); SV.eq = 18; }
       save(); msg('РУКА БОГА ОТКРЫТА!'); showMenu();
    } else {
      alert('Неверный код');
    }
  };
}
$('codebtn').onclick = codeUI;

// --- ДРУЗЬЯ ---
function friendUI(){
  const p=$('pan');p.style.display='block';$('ovt').style.display='none';
  let html = `<div style='text-align:center'><h3 style='color:#ffd24a'>МОИ ДРУЗЬЯ</h3>
  <div id='flist' style='margin:10px 0; max-height:150px; overflow-y:auto; border:1px solid #fff2; padding:5px'>`;
  if(SV.friends.length === 0) html += `<div style='opacity:0.5'>У тебя пока нет друзей</div>`;
  SV.friends.forEach((f, i) => {
    html += `<div class="friend-item"><span>👤 ${f}</span> <button onclick="inviteFriend('${f}')" style="background:#1f9d4a">ПОЗВАТЬ</button></div>`;
  });
  html += `</div>`;
  html += `<div style='margin:10px 0; font-size:12px; color:#aaa'>Твоё имя: <b>${SV.myName}</b></div>`;
  html += `<div style='display:flex; gap:5px; margin-bottom:10px'><input id='fadd' placeholder='Имя друга' style='flex:1; padding:8px; font-family:system-ui; background:#222; color:#fff; border:1px solid #555'/><button class='sm' id='faddbtn' style='padding:4px 8px'>ДОБАВИТЬ</button></div>`;
  html += `<div style='display:flex; gap:5px'><button class='sm' id='fcopy' style='flex:1; font-size:12px'>📋 ССЫЛКА ДЛЯ ДРУГА</button><button class='sm' id='fb' style='flex:1'>НАЗАД</button></div></div>`;
  p.innerHTML = html;

  window.inviteFriend = (name) => {
     msg('Приглашение для ' + name + ' создано');
     createRoom();
     showMenu();
  };

  $('faddbtn').onclick = () => {
    const val = $('fadd').value.trim();
    if(val && val !== SV.myName && !SV.friends.includes(val)) {
       SV.friends.push(val);
       save(); friendUI();
       msg('Друг ' + val + ' добавлен в список!');
    }
  };
  $('fcopy').onclick = () => {
    const url = location.href.split('#')[0] + '#friend=' + encodeURIComponent(SV.myName);
    navigator.clipboard.writeText(url).then(()=>msg('Ссылка для друга скопирована!')).catch(()=>{});
  };
  $('fb').onclick = () => showMenu();
}
$('friendbtn').onclick = friendUI;
</script>
</body></html>
