<!DOCTYPE html>
<html lang="es"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>CONTROL DE ENTRADAS LOST</title>
<style>
:root{--bg:#b9e3ff;--bg2:#eaf7ff;--card:#fff;--tx:#0f2a3f;--mut:#4f6f88;--pri:#e8452c;--pri2:#ff9d1c;--ok:#12a150;--bad:#d92d3a;--warn:#e59b00;--bd:#c3e4f8;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media(prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0b2540;--bg2:#12385c;--card:#16324f;--tx:#eaf6ff;--mut:#9cc0dc;--bd:#25506f;--pri:#ff6a3d;--pri2:#ffb238}}
:root[data-theme="dark"]{--bg:#0b2540;--bg2:#12385c;--card:#16324f;--tx:#eaf6ff;--mut:#9cc0dc;--bd:#25506f;--pri:#ff6a3d;--pri2:#ffb238}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;min-height:100vh;background:var(--bg);background:linear-gradient(180deg,var(--bg) 0%,var(--bg2) 100%) fixed;color:var(--tx);font:16px/1.4 system-ui,-apple-system,Segoe UI,Roboto,sans-serif}
main{max-width:720px;margin:0 auto;padding:16px}
h1{font-size:22px;margin:4px 0 12px}
.ht{background:linear-gradient(90deg,var(--pri),var(--pri2));-webkit-background-clip:text;background-clip:text;color:transparent}
.stat b{color:var(--pri)}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px}
.stat{background:var(--card);border:1px solid var(--bd);border-radius:12px;padding:10px;text-align:center}
.stat b{display:block;font-size:24px}.stat span{font-size:12px;color:var(--mut)}
.tabs{display:flex;gap:6px;margin-bottom:12px}
.tabs button{flex:1;padding:10px;border:1px solid var(--bd);background:var(--card);color:var(--tx);border-radius:10px;font-weight:600}
.tabs button.on{background:linear-gradient(135deg,var(--pri),var(--pri2));color:#fff;border-color:var(--pri)}
.card{background:var(--card);border:1px solid var(--bd);border-radius:12px;padding:12px;margin-bottom:10px}
input,textarea{width:100%;padding:10px;border:1px solid var(--bd);border-radius:8px;background:var(--bg2);color:var(--tx);font:inherit}
button{font:inherit;cursor:pointer}
.btn{padding:10px 14px;border:0;border-radius:8px;background:linear-gradient(135deg,var(--pri),var(--pri2));color:#fff;font-weight:700;box-shadow:0 2px 6px #e8452c44}
.btn.sec{background:transparent;color:var(--pri);border:1px solid var(--pri)}
.btn.sm{padding:6px 10px;font-size:14px}
.row{display:flex;gap:8px;align-items:center}.row>*{flex:1}.row>.btn{flex:none}
.g{display:flex;justify-content:space-between;align-items:center;gap:8px;padding:10px 0;border-bottom:1px solid var(--bd)}
.g:last-child{border:0}.g small{color:var(--mut);display:block}
.tag{font-size:12px;padding:3px 8px;border-radius:99px;font-weight:700;white-space:nowrap}
.tag.in{background:#12a15022;color:var(--ok)}.tag.out{background:#8884;color:var(--mut)}.tag.bad{background:#d92d3a22;color:var(--bad)}
.acts{display:flex;gap:6px;flex-wrap:wrap;justify-content:flex-end}
#reader{width:100%;border-radius:12px;overflow:hidden;background:#000;min-height:120px}
#res{margin-top:10px;padding:18px;border-radius:12px;text-align:center;font-weight:700;font-size:20px;display:none}
#res small{display:block;font-weight:400;font-size:15px;margin-top:4px}
#res.ok{background:var(--ok);color:#fff}#res.bad{background:var(--bad);color:#fff}#res.warn{background:var(--warn);color:#fff}
#qr{display:flex;justify-content:center;margin:12px 0}#qr img{width:256px;max-width:100%;height:auto;image-rendering:pixelated}
.mut{color:var(--mut);font-size:14px}
.code{font-family:ui-monospace,Menlo,monospace;font-weight:800;letter-spacing:2px;background:linear-gradient(135deg,var(--pri),var(--pri2));color:#fff;padding:2px 8px;border-radius:6px;font-size:14px}
</style></head><body><main>
<h1>🌅 <span class="ht">CONTROL DE ENTRADAS LOST</span></h1>
<div class="stats"><div class="stat"><b id="sT">0</b><span>En lista</span></div><div class="stat"><b id="sI" style="color:var(--ok)">0</b><span>Ya entraron</span></div><div class="stat"><b id="sP">0</b><span>Faltan</span></div></div>
<div class="tabs"><button data-t="l" class="on">Invitados</button><button data-t="p">Preventa</button><button data-t="s">Entrada</button><button data-t="r">Registro</button></div>

<section id="l"><h2 id="lh" style="font-size:18px;margin:0 0 10px"></h2>
<div class="card"><div class="row"><input id="nm" placeholder="Nombre"><button class="btn" id="add">Agregar</button></div>
<details style="margin-top:10px"><summary class="mut">Agregar varios (uno por línea)</summary><textarea id="bulk" rows="4" style="margin-top:8px"></textarea><button class="btn sec sm" id="addB" style="margin-top:8px">Agregar lista</button></details></div>
<input id="q" placeholder="Buscar invitado…" style="margin-bottom:10px">
<div class="card" id="list"></div>
<p class="mut">Datos guardados en este dispositivo. Usa el mismo dispositivo para la lista y para escanear.</p>
</section>

<section id="s" style="display:none"><div class="card"><b>Validar entrada</b><p class="mut" style="margin:4px 0 10px">Escribe el código del invitado (2 letras y 2 números).</p><div class="row"><input id="cd" placeholder="AB12" maxlength="4" autocapitalize="characters" autocomplete="off" style="font-size:26px;text-align:center;letter-spacing:4px;text-transform:uppercase"><button class="btn" id="cdb">Validar</button></div></div><div id="res"></div></section>

<section id="r" style="display:none"><div class="card" id="log"></div>
<button class="btn sec sm" id="rst">Reiniciar evento (borrar todo)</button></section>
</main>

<script>
const K='fiesta_v1';let S={guests:[],rejects:[]};
try{const r=localStorage.getItem(K);if(r)S=JSON.parse(r)}catch(e){}
const $=id=>document.getElementById(id);
const save=()=>{try{localStorage.setItem(K,JSON.stringify(S))}catch(e){}};
const hora=t=>new Date(t).toLocaleString('es',{hour:'2-digit',minute:'2-digit',second:'2-digit',day:'2-digit',month:'short'});
const esc=s=>s.replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const AZ='ABCDEFGHJKLMNPQRSTUVWXYZ';const tok=()=>{let c;do{c=AZ[Math.random()*24|0]+AZ[Math.random()*24|0]+String(Math.random()*100|0).padStart(2,'0')}while(S.guests.some(g=>g.id===c));return c};
S.guests.forEach(g=>{if(!/^[A-Z]{2}[0-9]{2}$/.test(g.id))g.id=tok()});
let lt='inv',tab='l',pd=null,pdT=0;const TL=t=>t==='pre'?'Preventa':'Invitado';
function add(n){n=n.trim();if(n)S.guests.push({id:tok(),name:n,type:lt,inAt:null,how:null})}
function render(){
 const inTab=tab==='l'||tab==='p';const g=inTab?S.guests.filter(x=>(x.type||'inv')===lt):S.guests,i=g.filter(x=>x.inAt).length;
 $('lh').textContent=lt==='pre'?'Lista de Preventa (compraron entrada)':'Lista de Invitados';
 $('sT').textContent=g.length;$('sI').textContent=i;$('sP').textContent=g.length-i;
 const f=$('q').value.toLowerCase();
 const rows=S.guests.filter(x=>(x.type||'inv')===lt).filter(x=>x.name.toLowerCase().includes(f));
 $('list').innerHTML=rows.length?rows.map(x=>`<div class="g"><div><b>${esc(x.name)}</b> <span class="code">${x.id}</span><small>${x.inAt?'Entró '+hora(x.inAt)+(x.how==='manual'?' (manual)':''):'Sin entrar'}</small></div><div class="acts"><span class="tag ${x.inAt?'in':'out'}">${x.inAt?'✔ Asistió':'Pendiente'}</span>${x.inAt?'':`<button class="btn sm sec" data-man="${x.id}">Marcar</button>`}<button class="btn sm sec" data-del="${x.id}" style="${pd===x.id?'background:var(--bad);color:#fff;border-color:var(--bad)':''}">${pd===x.id?'¿Seguro?':'🗑 Eliminar'}</button></div></div>`).join(''):'<span class="mut">Sin personas en esta lista aún.</span>';
 const L=[...S.guests.filter(x=>x.inAt).map(x=>({t:x.inAt,h:`<span class="tag in">Entró</span> ${esc(x.name)} <small>· ${TL(x.type||'inv')}</small>`})),...S.rejects.map(x=>({t:x.t,h:`<span class="tag bad">${x.why}</span> ${esc(x.who||'')}`}))].sort((a,b)=>b.t-a.t);
 $('log').innerHTML=L.length?L.map(x=>`<div class="g"><span>${x.h}</span><small>${hora(x.t)}</small></div>`).join(''):'<span class="mut">Sin movimientos.</span>';
 save();
}
$('add').onclick=()=>{add($('nm').value);$('nm').value='';render()};
$('addB').onclick=()=>{$('bulk').value.split('\n').forEach(add);$('bulk').value='';render()};
$('q').oninput=render;
$('list').onclick=e=>{const b=e.target.closest('button');if(!b)return;const d=b.dataset;
 if(d.man){const x=S.guests.find(y=>y.id===d.man);x.inAt=Date.now();x.how='manual';render()}
 if(d.del){if(pd===d.del){clearTimeout(pdT);pd=null;S.guests=S.guests.filter(y=>y.id!==d.del)}else{pd=d.del;clearTimeout(pdT);pdT=setTimeout(()=>{pd=null;render()},3000)}render()}};
let rt=0;$('rst').onclick=()=>{const b=$('rst');if(rt){clearTimeout(rt);rt=0;S={guests:[],rejects:[]};b.textContent='Reiniciar evento (borrar todo)';b.style.cssText='';render()}else{b.textContent='¿Seguro? Toca otra vez para borrar TODO';b.style.cssText='background:var(--bad);color:#fff;border-color:var(--bad)';rt=setTimeout(()=>{rt=0;b.textContent='Reiniciar evento (borrar todo)';b.style.cssText=''},4000)}};
document.querySelectorAll('.tabs button').forEach(b=>b.onclick=()=>{
 tab=b.dataset.t;if(tab==='l')lt='inv';if(tab==='p')lt='pre';
 document.querySelectorAll('.tabs button').forEach(x=>x.classList.toggle('on',x===b));
 const sec=tab==='p'?'l':tab;['l','s','r'].forEach(t=>$(t).style.display=t===sec?'':'none');render()});

function show(c,h,s){const r=$('res');r.className=c;r.style.display='block';r.innerHTML=h+(s?`<small>${s}</small>`:'')}
function beep(ok){try{const a=new (window.AudioContext||window.webkitAudioContext)(),o=a.createOscillator();o.frequency.value=ok?880:220;o.connect(a.destination);o.start();setTimeout(()=>{o.stop();a.close()},ok?150:400)}catch(e){}if(navigator.vibrate)navigator.vibrate(ok?80:[150,80,150])}
function validar(){
 const id=$('cd').value.trim().toUpperCase();if(!id)return;$('cd').value='';$('cd').focus();
 const n=Date.now(),x=S.guests.find(y=>y.id===id);
 if(!x){S.rejects.push({t:n,why:'No está en lista',who:'Código '+id});beep(0);show('bad','✖ NO ESTÁ EN LISTA','Código '+esc(id)+' no existe')}
 else if(x.inAt){S.rejects.push({t:n,why:'Código ya usado',who:x.name});beep(0);show('warn','⚠ CÓDIGO YA USADO',`${esc(x.name)} (${TL(x.type||'inv')}) ya entró a las ${hora(x.inAt)}`)}
 else{x.inAt=n;x.how='codigo';beep(1);show('ok','✔ BIENVENIDO/A',`${esc(x.name)} · ${TL(x.type||'inv')} · ${hora(n)}`)}
 render();
}
$('cdb').onclick=validar;$('cd').onkeydown=e=>{if(e.key==='Enter')validar()};
render();
</script></body></html>
