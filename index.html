<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>XO Ultimate — تحدّي الذكاء</title>
<style>
:root{--bg:#080e1b;--panel:#111b2e;--tile:#192740;--line:#2c4263;--text:#f0f6ff;--muted:#a2b4d0;--cyan:#5bf0d6;--pink:#ff7da8;--gold:#ffd166}
*{box-sizing:border-box}body{margin:0;min-height:100vh;padding:20px;display:grid;place-items:center;background:radial-gradient(ellipse at top,#203b60 0%,var(--bg) 58%);color:var(--text);font-family:system-ui,Arial,sans-serif}
main{width:min(720px,100%)}header{text-align:center;margin-bottom:18px}h1{margin:0;font-size:clamp(30px,7vw,52px);letter-spacing:1px}header p{color:var(--muted);margin:4px 0}
.panel{background:#111b2eee;border:1px solid #2a3e5c;border-radius:24px;padding:clamp(13px,3vw,24px);box-shadow:0 25px 80px #0005}
.toolbar{display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap;margin-bottom:16px}
.controls{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
select,button{font:inherit;color:var(--text);background:#1a2a45;border:1px solid #354d70;border-radius:12px;padding:10px 13px}
button{font-weight:700;cursor:pointer;transition:.12s}button:hover{filter:brightness(1.15)}button:active{transform:scale(.97)}
.status{font-weight:800;color:var(--cyan);min-height:28px}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin:0 0 14px}
.stat{background:#0c1525;border:1px solid #263a57;border-radius:13px;padding:10px}.stat b{display:block;font-size:23px}.stat span{font-size:12px;color:var(--muted)}
.board{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;width:min(460px,100%);margin:0 auto 16px}
.cell{aspect-ratio:1;border-radius:18px;background:linear-gradient(145deg,#1d304e,#14223a);border:1px solid #304969;display:grid;place-items:center;font-size:clamp(48px,14vw,88px);font-weight:900;line-height:1;position:relative}
.cell:disabled{opacity:1;cursor:default}.cell.x{color:var(--cyan);text-shadow:0 0 25px #5bf0d655}.cell.o{color:var(--pink);text-shadow:0 0 25px #ff7da855}.cell.win{background:#28534f;border-color:var(--gold);box-shadow:0 0 0 2px #ffd16655}
.cell.hint{outline:3px dashed var(--gold);outline-offset:-6px}
.actions{display:flex;justify-content:center;gap:9px;flex-wrap:wrap}.primary{background:var(--cyan);color:#06151c;border-color:var(--cyan)}.gold{background:#3a2e20;border-color:#826533;color:var(--gold)}
.note{text-align:center;color:var(--muted);font-size:13px;margin:14px 0 0}
</style>
</head>
<body><main>
<header><h1>XO <span style="color:#5bf0d6">ULTIMATE</span></h1><p>النسخة المطوّرة — مستويات، نقاط، وتحدّيات</p></header>
<section class="panel">
<div class="toolbar">
<div id="status" class="status" aria-live="polite">اختار المستوى ورمزك وابدأ!</div>
<div class="controls">
<label for="level">المستوى</label>
<select id="level"><option value="easy">سهل</option><option value="medium">متوسط</option><option value="hard" selected>صعب</option><option value="perfect">مستحيل (لا يخسر)</option></select>
<label for="symbol">رمزك</label><select id="symbol"><option value="X">X</option><option value="O">O</option></select>
</div></div>
<div class="stats">
<div class="stat"><b id="wins">0</b><span>انتصاراتك</span></div><div class="stat"><b id="draws">0</b><span>تعادلات</span></div><div class="stat"><b id="losses">0</b><span>انتصارات AI</span></div>
</div>
<div id="board" class="board" aria-label="لوحة XO"></div>
<div class="actions"><button id="restart" class="primary">جولة جديدة ↻</button><button id="undo">تراجع حركة</button><button id="hint" class="gold">اقتراح حركة ✦</button><button id="reset">تصفير النقاط</button></div>
<p class="note">مستوى «مستحيل» يستخدم بحثًا كاملًا؛ إذا لعبت بأفضل طريقة، أقصى ما تقدر تحققه هو التعادل.</p>
</section></main>
<script>
const $=id=>document.getElementById(id);
const boardEl=$('board'),statusEl=$('status'),levelEl=$('level'),symbolEl=$('symbol');
const lines=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
let b=[],human='X',ai='O',ended=false,thinking=false,history=[],hintIndex=null;
let stats={wins:0,draws:0,losses:0};
function empty(a){return a.map((v,i)=>v===''?i:null).filter(i=>i!==null)}
function won(a){for(const line of lines){let [x,y,z]=line;if(a[x]&&a[x]===a[y]&&a[x]===a[z])return {who:a[x],line}}return null}
function terminal(a){let w=won(a);if(w)return w.who==='O'?10:-10;if(empty(a).length===0)return 0;return null}
function orderMoves(a){return empty(a).sort((x,y)=>rank(y)-rank(x))}
function rank(i){return i===4?5:[0,2,6,8].includes(i)?3:1}
function minimax(a,turn,depth,alpha,beta){
 let t=terminal(a);if(t!==null)return t===10?10-depth:t===-10?depth-10:0;
 let moves=orderMoves(a);
 if(turn===ai){let best=-Infinity;for(let i of moves){a[i]=ai;best=Math.max(best,minimax(a,human,depth+1,alpha,beta));a[i]='';alpha=Math.max(alpha,best);if(beta<=alpha)break}return best}
 let best=Infinity;for(let i of moves){a[i]=human;best=Math.min(best,minimax(a,ai,depth+1,alpha,beta));a[i]='';beta=Math.min(beta,best);if(beta<=alpha)break}return best
}
function perfectMove(a,turn=ai){
 let best=-Infinity,choice=null;
 for(let i of orderMoves(a)){a[i]=turn;let val=minimax(a,turn===ai?human:ai,0,-Infinity,Infinity);a[i]='';if(val>best){best=val;choice=i}}
 return choice
}
function heuristic(a,turn){
 // Evaluate line threats, center/corners, and immediate tactical moves.
 let opp=turn===ai?human:ai,score=0;
 for(const line of lines){
  let mine=0,theirs=0;
  for(let i of line){if(a[i]===turn)mine++;else if(a[i]===opp)theirs++}
  if(!theirs)score+=mine===2?90:mine===1?8:0;
  if(!mine)score-=theirs===2?100:theirs===1?7:0;
 }
 if(a[4]===turn)score+=4;else if(a[4]===opp)score-=4;
 return score
}
function mediumMove(){
 let moves=orderMoves(b);
 // Win now, then block, then tactical positional preference.
 for(let i of moves){b[i]=ai;let w=won(b);b[i]='';if(w)return i}
 for(let i of moves){b[i]=human;let w=won(b);b[i]='';if(w)return i}
 return moves[Math.floor(Math.random()*Math.min(3,moves.length))]
}
function easyMove(){let m=empty(b);return m[Math.floor(Math.random()*m.length)]}
function chooseAI(){
 let level=levelEl.value;
 if(level==='perfect')return perfectMove(b);
 if(level==='hard'){
  // Strong but not mathematically perfect: sometimes selects a near-best move.
  let moves=orderMoves(b),scores=[];
  for(let i of moves){b[i]=ai;let v=minimax(b,human,0,-Infinity,Infinity);b[i]='';scores.push({i,v})}
  scores.sort((x,y)=>y.v-x.v);
  if(scores.length>1&&Math.random()<0.16)return scores[1].i;
  return scores[0].i
 }
 if(level==='medium')return mediumMove();
 return easyMove()
}
function render(winLine=[]){
 boardEl.innerHTML='';
 b.forEach((v,i)=>{
  let btn=document.createElement('button');btn.className='cell'+(v?' '+v.toLowerCase():'')+(winLine.includes(i)?' win':'')+(hintIndex===i?' hint':'');
  btn.textContent=v;btn.disabled=!!v||ended||thinking;btn.setAttribute('aria-label',`مربع ${i+1} ${v||'فارغ'}`);
  btn.addEventListener('click',()=>playHuman(i));boardEl.appendChild(btn)
 })
 $('wins').textContent=stats.wins;$('draws').textContent=stats.draws;$('losses').textContent=stats.losses
}
function finish(){
 let w=won(b);
 if(w){ended=true;if(w.who===human){stats.wins++;statusEl.textContent='فزت على الذكاء الاصطناعي! 🔥'}else{stats.losses++;statusEl.textContent='الذكاء الاصطناعي فاز هذه الجولة! 🤖'}render(w.line);return true}
 if(empty(b).length===0){ended=true;stats.draws++;statusEl.textContent='تعادل! الجولة القادمة؟ 🤝';render();return true}
 return false
}
function playHuman(i){
 if(ended||thinking||b[i])return;
 history.push(b.slice());b[i]=human;hintIndex=null;if(finish())return;
 thinking=true;statusEl.textContent='الذكاء الاصطناعي يحسب…';render();
 setTimeout(()=>{let m=chooseAI();if(m!==null)b[m]=ai;thinking=false;if(!finish()){statusEl.textContent='دورك!';render()}},240)
}
function newGame(){
 human=symbolEl.value;ai=human==='X'?'O':'X';b=Array(9).fill('');ended=false;thinking=false;history=[];hintIndex=null;
 if(human==='O'){b[4]=ai;statusEl.textContent='AI بدأ في الوسط — دورك!'}else statusEl.textContent='دورك! أنت X';
 render()
}
$('restart').addEventListener('click',newGame);
levelEl.addEventListener('change',()=>{newGame();statusEl.textContent='تم تغيير المستوى. ابدأ جولة جديدة!'});
symbolEl.addEventListener('change',newGame);
$('undo').addEventListener('click',()=>{
 if(thinking||history.length===0||ended)return;
 b=history.pop();hintIndex=null;statusEl.textContent='تراجعت عن آخر حركة.';render()
});
$('hint').addEventListener('click',()=>{
 if(ended||thinking)return;
 hintIndex=perfectMove(b,human);statusEl.textContent=hintIndex===null?'ما بقاتش حركة!':'اقتراح: المربع المضيء';render()
});
$('reset').addEventListener('click',()=>{stats={wins:0,draws:0,losses:0};newGame()});
newGame();
</script></body></html>
