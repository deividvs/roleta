# Roleta de Prêmios — T.R.I. 2.0

App de "spin the wheel" (roleta de prêmios) em **HTML, CSS e JavaScript puro**, sem framework e sem build. Roda dividida em 6 fatias, sorteio por probabilidade configurável, limite de tentativas persistido no navegador e captura de e-mail antes de revelar o código de desconto.

> Estilo visual: roleta "carnaval/cassino" — fundo escuro roxo→vinho, fatias em laranja/roxo/coral alternados, aro escuro com lâmpadas brilhantes piscando, ponteiro em gota, centro branco "GIRAR" e CTA com gradiente.

---

## Aparência atual da tela

- **Eyebrow:** `Promoção T.R.I. 2.0 · Gire e ganhe`
- **Título:** GIRE A ROLETA **AGORA** (gradiente laranja→coral→roxo)
- **Subtítulo:** *"Sua chance de levar desconto de verdade. Gire a roleta para ver qual será o seu prêmio."*
- **Contador:** pílula gradiente `Tentativas restantes` + número
- **Centro da roda:** botão branco `GIRAR` com borda tracejada
- **CTA:** `Girar a roleta` (pílula gradiente com glow)
- **Ícones decorativos flutuantes:** 🎁 ⭐ 🎟️ 🏅 🎬

---

## Código-fonte completo (`index.html`)

Crie um arquivo `index.html` no Claude Code e cole **exatamente** o código abaixo — é a conversão fiel do que projetamos (HTML, CSS e JavaScript puro, sem framework e sem build). Abre direto no navegador e gera um modelo **idêntico**. Toda a personalização fica no bloco `CONFIGURAÇÃO` no topo do `<script>`.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Roleta de Prêmios — T.R.I. 2.0</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,400;12..96,600;12..96,700;12..96,800&family=Source+Sans+3:wght@400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  *{box-sizing:border-box;margin:0;padding:0}
  @keyframes vd-pop{0%{transform:scale(.85);opacity:0}60%{transform:scale(1.03)}100%{transform:scale(1);opacity:1}}
  @keyframes vd-rise{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
  @keyframes vd-float{0%,100%{transform:translateY(0) rotate(var(--r,0deg))}50%{transform:translateY(-10px) rotate(var(--r,0deg))}}
  @keyframes vd-twinkle{0%,100%{opacity:1}50%{opacity:.4}}
</style>
</head>
<body>
<div style="min-height:100vh;width:100%;font-family:'Source Sans 3',system-ui,sans-serif;background:radial-gradient(85% 55% at 50% -6%, rgba(224,74,86,.40), transparent 60%), radial-gradient(130% 100% at 50% 8%, #3C1531 0%, #271036 44%, #150A22 100%);color:rgba(255,255,255,.94);display:flex;flex-direction:column;align-items:center;padding:clamp(24px,6vw,48px) clamp(16px,5vw,24px) clamp(40px,9vw,64px);position:relative;overflow:hidden">

  <!-- dot grid -->
  <div style="position:absolute;inset:0;background-image:radial-gradient(rgba(255,255,255,.04) 1px,transparent 1px);background-size:30px 30px;pointer-events:none"></div>

  <!-- ícones decorativos flutuantes -->
  <div style="position:absolute;top:clamp(70px,15vw,120px);left:3%;font-size:clamp(34px,9vw,58px);filter:drop-shadow(0 10px 16px rgba(0,0,0,.55));--r:-14deg;animation:vd-float 5s ease-in-out infinite;pointer-events:none;z-index:1">🎁</div>
  <div style="position:absolute;top:clamp(96px,18vw,150px);right:5%;font-size:clamp(26px,6.5vw,44px);filter:drop-shadow(0 8px 14px rgba(0,0,0,.5));--r:12deg;animation:vd-float 6s ease-in-out infinite .6s;pointer-events:none;z-index:1">⭐</div>
  <div style="position:absolute;top:clamp(220px,46vw,340px);right:1%;font-size:clamp(30px,7.5vw,50px);filter:drop-shadow(0 8px 14px rgba(0,0,0,.5));--r:-10deg;animation:vd-float 5.5s ease-in-out infinite .3s;pointer-events:none;z-index:1">🎟️</div>
  <div style="position:absolute;top:46%;left:0.5%;font-size:clamp(30px,7.5vw,50px);filter:drop-shadow(0 8px 14px rgba(0,0,0,.5));--r:8deg;animation:vd-float 6.2s ease-in-out infinite .9s;pointer-events:none;z-index:1">🏅</div>
  <div style="position:absolute;bottom:clamp(48px,12vw,90px);right:6%;font-size:clamp(32px,8vw,52px);filter:drop-shadow(0 10px 16px rgba(0,0,0,.55));--r:-8deg;animation:vd-float 5.8s ease-in-out infinite .4s;pointer-events:none;z-index:1">🎬</div>

  <!-- header -->
  <div style="position:relative;z-index:2;text-align:center;max-width:560px;margin-bottom:24px">
    <div style="font-size:11px;letter-spacing:.16em;text-transform:uppercase;color:#F4A93C;font-weight:700;margin-bottom:12px">Promoção T.R.I. 2.0 · Gire e ganhe</div>
    <h1 style="font-family:'Bricolage Grotesque',sans-serif;font-weight:800;letter-spacing:-.02em;line-height:1;font-size:clamp(34px,9vw,58px);text-transform:uppercase;color:#fff;text-shadow:0 3px 18px rgba(0,0,0,.45)">Gire a roleta<br><span style="background:linear-gradient(90deg,#F4842A,#F0506E 55%,#A855F7);-webkit-background-clip:text;background-clip:text;color:transparent">agora</span></h1>
    <p style="margin-top:14px;font-size:clamp(14px,3.6vw,17px);line-height:1.55;color:rgba(255,255,255,.78)">Sua chance de levar desconto de verdade. Gire a roleta para ver qual será o seu prêmio.</p>
  </div>

  <!-- contador -->
  <div style="position:relative;z-index:2;display:inline-flex;align-items:center;gap:10px;background:linear-gradient(90deg,#F4842A,#F0506E,#9333EA);border-radius:999px;padding:9px 22px;margin-bottom:30px;box-shadow:0 8px 22px rgba(240,80,110,.4)">
    <span style="font-size:13px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:rgba(255,255,255,.92)">Tentativas restantes</span>
    <span id="counter" style="font-family:'DM Mono',monospace;font-weight:500;font-size:18px;color:#fff">3</span>
  </div>

  <!-- RODA -->
  <div style="position:relative;z-index:2;width:min(88vw,440px);aspect-ratio:1/1;margin-bottom:34px">

    <!-- ponteiro em gota -->
    <div style="position:absolute;top:-4px;left:50%;transform:translateX(-50%) rotate(45deg);z-index:6;width:clamp(24px,6vw,32px);height:clamp(24px,6vw,32px);background:linear-gradient(135deg,#F0506E,#9333EA);border-radius:50% 50% 50% 0;box-shadow:0 4px 10px rgba(0,0,0,.5),inset 0 2px 4px rgba(255,255,255,.4)"></div>

    <!-- aro escuro -->
    <div style="position:absolute;inset:0;border-radius:50%;padding:clamp(12px,3.6vw,20px);background:radial-gradient(circle at 50% 35%, #2A1640, #140A22 75%);box-shadow:0 22px 50px rgba(0,0,0,.6),0 0 0 2px rgba(255,255,255,.05),inset 0 2px 6px rgba(255,255,255,.08)">
      <!-- disco giratório (preenchido via JS) -->
      <div id="disc" style="position:relative;width:100%;height:100%;border-radius:50%;overflow:hidden;box-shadow:inset 0 0 0 3px rgba(0,0,0,.25);transition:none;transform:rotate(0deg);will-change:transform"></div>
    </div>

    <!-- lâmpadas do aro (geradas via JS) -->
    <div id="bulbs" style="position:absolute;inset:0;z-index:3;pointer-events:none"></div>

    <!-- centro GIRAR (também é botão / slot pro logo) -->
    <button id="hub" style="position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);z-index:5;width:27%;height:27%;border-radius:50%;border:none;padding:0;cursor:pointer;background:radial-gradient(circle at 42% 32%,#fff,#F6E9F2 60%,#E9CEDE);box-shadow:0 6px 16px rgba(0,0,0,.45),inset 0 2px 4px rgba(255,255,255,.9)">
      <span style="display:flex;align-items:center;justify-content:center;width:100%;height:100%;border-radius:50%;border:2px dashed rgba(147,51,234,.5);font-family:'Bricolage Grotesque',sans-serif;font-weight:800;font-size:clamp(12px,3vw,17px);letter-spacing:.02em;color:#6D28D9;text-transform:uppercase">GIRAR</span>
    </button>
  </div>

  <!-- CTA -->
  <button id="cta" style="position:relative;z-index:2;font-family:'Bricolage Grotesque',sans-serif;font-weight:800;font-size:clamp(16px,4.4vw,20px);letter-spacing:.04em;text-transform:uppercase;padding:18px 52px;border:none;border-radius:999px;color:#fff;background:linear-gradient(90deg,#F4842A,#F0506E 55%,#9333EA);box-shadow:0 0 0 4px rgba(255,255,255,.06),0 12px 34px rgba(240,80,110,.55);cursor:pointer;transition:transform .15s,box-shadow .2s">Girar a roleta</button>

  <!-- aviso de esgotado -->
  <div id="exhausted" style="display:none;position:relative;z-index:2;margin-top:20px;max-width:420px;text-align:center;background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.12);backdrop-filter:blur(12px);border-radius:16px;padding:20px 24px;animation:vd-rise .5s cubic-bezier(.16,1,.3,1) both">
    <div style="font-family:'Bricolage Grotesque',sans-serif;font-weight:800;letter-spacing:-.01em;font-size:19px;color:#F4A93C;margin-bottom:6px">Suas tentativas acabaram</div>
    <p style="font-size:14px;line-height:1.55;color:rgba(255,255,255,.72)">Você já usou seus 3 giros neste dispositivo. Use o código que ganhou — ele não expira por aqui.</p>
  </div>

  <!-- MODAL DE RESULTADO -->
  <div id="modal" style="display:none;position:fixed;inset:0;z-index:50;background:rgba(20,10,32,.82);backdrop-filter:blur(6px);align-items:center;justify-content:center;padding:20px">
    <div style="position:relative;width:100%;max-width:420px;background:#FFFDFB;border-radius:24px;padding:36px 30px 32px;text-align:center;box-shadow:0 30px 60px rgba(0,0,0,.55);animation:vd-pop .45s cubic-bezier(.16,1,.3,1) both">
      <button id="modalClose" style="position:absolute;top:16px;right:18px;background:none;border:none;font-size:22px;line-height:1;color:#A8A29E;cursor:pointer">×</button>
      <div style="font-size:11px;letter-spacing:.16em;text-transform:uppercase;color:#9333EA;font-weight:800;margin-bottom:10px">Você ganhou</div>
      <div id="wonLabel" style="font-family:'Bricolage Grotesque',sans-serif;font-weight:800;letter-spacing:-.02em;font-size:clamp(34px,9vw,52px);line-height:1;text-transform:uppercase;background:linear-gradient(90deg,#F4842A,#F0506E 55%,#9333EA);-webkit-background-clip:text;background-clip:text;color:transparent;margin-bottom:8px"></div>
      <p id="wonMessage" style="font-size:15px;line-height:1.55;color:#57534E;margin-bottom:24px"></p>

      <!-- captura de e-mail -->
      <div id="emailStep" style="display:none;text-align:left">
        <label style="display:block;font-size:13px;font-weight:600;color:#292524;margin-bottom:7px">Informe seu e-mail pra liberar o código</label>
        <input id="emailInput" type="email" placeholder="seu@email.com.br" style="width:100%;padding:13px 15px;font-size:15px;font-family:inherit;border:1px solid #D6D3D1;border-radius:10px;background:#fff;color:#292524;outline:none;margin-bottom:6px"/>
        <div id="emailError" style="min-height:18px;font-size:12px;color:#B91C1C;margin-bottom:12px"></div>
        <button id="revealBtn" style="width:100%;padding:15px;font-family:'Source Sans 3',sans-serif;font-weight:700;font-size:15px;letter-spacing:.04em;text-transform:uppercase;color:#fff;background:linear-gradient(135deg,#F0506E,#9333EA);border:none;border-radius:10px;cursor:pointer;box-shadow:0 6px 16px rgba(147,51,234,.35)">Liberar meu código</button>
      </div>

      <!-- código revelado -->
      <div id="codeStep" style="display:none">
        <div style="font-size:13px;color:#57534E;margin-bottom:8px">Use este código no checkout:</div>
        <div id="wonCode" style="font-family:'DM Mono',monospace;font-weight:500;font-size:24px;letter-spacing:.06em;color:#3B0A52;background:#F6ECFE;border:2px dashed #9333EA;border-radius:12px;padding:14px;margin-bottom:8px"></div>
        <div style="font-size:12px;color:#78716C">Código enviado também para seu e-mail.</div>
      </div>
    </div>
  </div>
</div>

<script>
/* ───────────────────────────────────────────────────────────
   CONFIGURAÇÃO — personalize prêmios, cores, textos e pesos
   ───────────────────────────────────────────────────────────
   Cada prêmio: top (valor grande) · sub (descrição) · label (resultado)
   code · weight (peso/probabilidade) · color · textColor · message
   PALETA: laranja #F4842A · roxo #7C3AED (destaque) · coral #F0506E
*/
var PRIZES = [
  { top:'10%',  sub:'DESCONTO',         label:'10% DESCONTO',          code:'SGF10',      weight:30, color:'#F4842A', textColor:'#fff', message:'Um bom começo pra entrar na gestão.' },
  { top:'30%',  sub:'DESCONTO',         label:'30% DESCONTO',          code:'TRI30',      weight:8,  color:'#7C3AED', textColor:'#fff', message:'Desconto cheio. Não deixe dinheiro na mesa.' },
  { top:'15%',  sub:'DESCONTO',         label:'15% DESCONTO',          code:'TRI15',      weight:22, color:'#F0506E', textColor:'#fff', message:'Desconto firme. Aproveite.' },
  { top:'20%',  sub:'DESCONTO',         label:'20% DESCONTO',          code:'TRI20',      weight:18, color:'#F4842A', textColor:'#fff', message:'Conta que fecha melhor pra você.' },
  { top:'DZG',  sub:'POR R$ 1,00',      label:'DZG por 1,00',          code:'DZG1',       weight:1,  color:'#7C3AED', textColor:'#fff', message:'Acesso ao DZG por apenas R$ 1,00. Fale com nosso time.' },
  { top:'GUIA', sub:'DE SUPLEMENTAÇÃO', label:'Guia de Suplementação', code:'GUIASUPLEM', weight:5,  color:'#F0506E', textColor:'#fff', message:'Guia de Suplementação liberado pra você.' },
];
var CENTER_LABEL  = 'GIRAR';   // texto/logo do centro
var MAX_SPINS     = 3;         // tentativas permitidas
var REQUIRE_EMAIL = true;      // exigir e-mail antes de revelar o código?
var FORCE_INDEX   = null;      // índice (0-based) p/ forçar resultado; null = por peso
var STORAGE_KEY   = 'tri-roleta-spins';

var SLICE = 360 / PRIZES.length;
var rotation = 0, spinning = false, spinsLeft = readSpinsLeft(), timer = null;

/* ── persistência das tentativas no navegador ── */
function readSpinsLeft(){
  try{ var v = localStorage.getItem(STORAGE_KEY);
    if(v == null) return MAX_SPINS;
    var used = parseInt(v,10);
    return isNaN(used) ? MAX_SPINS : Math.max(0, MAX_SPINS - used);
  }catch(e){ return MAX_SPINS; }
}
function saveSpinsUsed(){
  try{ localStorage.setItem(STORAGE_KEY, String(MAX_SPINS - spinsLeft)); }catch(e){}
}

/* ── sorteio por peso (ou forçado) ── */
function pickIndex(){
  if(FORCE_INDEX != null) return FORCE_INDEX;
  var total = PRIZES.reduce(function(s,p){ return s + p.weight; }, 0);
  var r = Math.random() * total;
  for(var i=0;i<PRIZES.length;i++){ r -= PRIZES[i].weight; if(r <= 0) return i; }
  return PRIZES.length - 1;
}

/* ── monta as fatias (conic-gradient) e os rótulos ── */
var disc = document.getElementById('disc');
function buildWheel(){
  var stops = PRIZES.map(function(p,i){ return p.color+' '+(i*SLICE)+'deg '+((i+1)*SLICE)+'deg'; }).join(', ');
  disc.style.background = 'conic-gradient(from 0deg, '+stops+')';
  PRIZES.forEach(function(p,i){
    var angle = i*SLICE + SLICE/2;                 // centro da fatia, a partir do topo
    var outer = document.createElement('div');
    outer.style.cssText = 'position:absolute;left:50%;top:50%;width:min(27vw,132px);pointer-events:none;'+
      'transform:translate(-50%,-50%) rotate('+angle+'deg) translateY(calc(clamp(86px,33vw,158px) * -1)) rotate('+(-angle)+'deg)';
    var inner = document.createElement('div');     // contra-rotor: mantém o texto na horizontal
    inner.className = 'label-counter';
    inner.style.cssText = 'display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;gap:2px;transform:rotate(0deg);transition:none;will-change:transform';
    inner.innerHTML =
      '<span style="font-family:\'Bricolage Grotesque\',sans-serif;font-weight:800;font-size:clamp(18px,5.4vw,28px);line-height:1;letter-spacing:-.02em;color:'+p.textColor+';text-shadow:0 1px 5px rgba(0,0,0,.5)">'+p.top+'</span>'+
      '<span style="font-family:\'Bricolage Grotesque\',sans-serif;font-weight:700;font-size:clamp(9px,2.5vw,13px);line-height:1.08;text-transform:uppercase;letter-spacing:.03em;color:'+p.textColor+';text-shadow:0 1px 3px rgba(0,0,0,.5)">'+p.sub+'</span>';
    outer.appendChild(inner);
    disc.appendChild(outer);
  });
}

/* ── lâmpadas brilhantes no aro ── */
function buildBulbs(){
  var box = document.getElementById('bulbs');
  for(var i=0;i<12;i++){
    var a = i*30 * Math.PI/180;                    // 12 luzes, a cada 30°
    var left = 50 + 47*Math.sin(a);
    var top  = 50 - 47*Math.cos(a);
    var b = document.createElement('div');
    b.style.cssText = 'position:absolute;left:'+left.toFixed(1)+'%;top:'+top.toFixed(1)+'%;'+
      'width:clamp(7px,2vw,11px);height:clamp(7px,2vw,11px);border-radius:50%;'+
      'background:radial-gradient(circle at 35% 30%,#fff,#FFE7A0 42%,#F0A93C);'+
      'box-shadow:0 0 9px 2px rgba(255,205,110,.85);transform:translate(-50%,-50%);'+
      'animation:vd-twinkle 1.8s ease-in-out infinite '+(i*0.15)+'s';
    box.appendChild(b);
  }
}

/* ── girar ── */
function spin(){
  if(spinning || spinsLeft <= 0) return;
  var idx = pickIndex();
  var center = idx*SLICE + SLICE/2;
  var baseTurns = Math.ceil(rotation/360) + 5;      // pelo menos 5 voltas
  var target = baseTurns*360 + (360 - center);      // para com a fatia no topo
  rotation = target;
  spinning = true;

  var trans = 'transform 4.2s cubic-bezier(0.16, 1, 0.3, 1)';
  disc.style.transition = trans;
  disc.style.transform = 'rotate('+target+'deg)';
  // contra-giro sincronizado: o texto permanece na horizontal durante todo o giro
  document.querySelectorAll('.label-counter').forEach(function(el){
    el.style.transition = trans;
    el.style.transform = 'rotate('+(-target)+'deg)';
  });

  clearTimeout(timer);
  timer = setTimeout(function(){
    spinning = false;
    spinsLeft -= 1;
    saveSpinsUsed();
    updateCounter();
    showResult(PRIZES[idx]);
  }, 4200);
}

/* ── contador / botões ── */
function updateCounter(){
  document.getElementById('counter').textContent = spinsLeft;
  var noSpins = spinsLeft <= 0;
  var cta = document.getElementById('cta');
  cta.textContent = noSpins ? 'Sem tentativas' : 'Girar a roleta';
  cta.style.background = noSpins ? '#5B4A6E' : 'linear-gradient(90deg,#F4842A,#F0506E 55%,#9333EA)';
  cta.style.boxShadow  = noSpins ? 'none' : '0 0 0 4px rgba(255,255,255,.06),0 12px 34px rgba(240,80,110,.55)';
  cta.style.cursor     = noSpins ? 'not-allowed' : 'pointer';
  cta.style.opacity    = noSpins ? .65 : 1;
  document.getElementById('hub').style.cursor = noSpins ? 'not-allowed' : 'pointer';
  document.getElementById('exhausted').style.display = noSpins ? 'block' : 'none';
}

/* ── modal de resultado + captura de e-mail ── */
function showResult(prize){
  document.getElementById('wonLabel').textContent = prize.label;
  document.getElementById('wonMessage').textContent = prize.message;
  var hasCode = !!prize.code;
  var needEmail = REQUIRE_EMAIL && hasCode;
  document.getElementById('emailStep').style.display = needEmail ? 'block' : 'none';
  document.getElementById('codeStep').style.display  = (hasCode && !REQUIRE_EMAIL) ? 'block' : 'none';
  document.getElementById('emailInput').value = '';
  document.getElementById('emailError').textContent = '';
  document.getElementById('wonCode').textContent = prize.code || '';
  document.getElementById('modal')._code = prize.code || '';
  document.getElementById('modal').style.display = 'flex';
}
function revealCode(){
  var email = document.getElementById('emailInput').value.trim();
  if(!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)){
    document.getElementById('emailError').textContent = 'Digite um e-mail válido.'; return;
  }
  // aqui você pode enviar o e-mail para sua lista (API/CRM) antes de revelar
  document.getElementById('emailStep').style.display = 'none';
  document.getElementById('wonCode').textContent = document.getElementById('modal')._code;
  document.getElementById('codeStep').style.display = 'block';
}

/* ── eventos ── */
document.getElementById('cta').addEventListener('click', spin);
document.getElementById('hub').addEventListener('click', spin);
document.getElementById('revealBtn').addEventListener('click', revealCode);
document.getElementById('modalClose').addEventListener('click', function(){
  document.getElementById('modal').style.display = 'none';
});

/* ── init ── */
buildWheel();
buildBulbs();
updateCounter();
</script>
</body>
</html>
```

---

## Como o texto fica na horizontal durante o giro

Cada rótulo tem duas camadas:

1. **Posicionador** (externo) — leva o rótulo até o centro da fatia:
   `translate(-50%,-50%) rotate(ÂNGULO) translateY(-RAIO) rotate(-ÂNGULO)`
2. **Contra-rotor** (interno, com os textos) — cancela o giro da roda:
   `rotate(-ROTAÇÃO_ATUAL)` usando a **mesma** `transition` da roda.

Como a roda gira `+R(t)` e o contra-rotor `-R(t)` com a mesma curva/duração, a orientação final do texto é sempre `0°` → permanece na horizontal em todos os quadros.

---

## Configuração (no topo da classe `Component`)

| Campo | Valor atual | O que faz |
|---|---|---|
| `PRIZES[]` | 6 itens | Lista de prêmios. Cada item: `top`, `sub`, `label`, `code`, `weight`, `color`, `textColor`, `message`. |
| `CENTER_LABEL` | `GIRAR` | Texto/logo no centro da roda. |
| `MAX_SPINS` | `3` | Número de tentativas permitidas. |
| `REQUIRE_EMAIL` | `true` | Exige e-mail antes de revelar o código. |
| `FORCE_INDEX` | `null` | `null` = sorteio por peso. Um índice (0-based) força aquele prêmio. |
| `STORAGE_KEY` | `tri-roleta-spins` | Chave do `localStorage` que guarda os giros usados. |

### Tabela de prêmios atual

| # | Valor (top) | Descrição (sub) | Código | Peso | Cor |
|---|---|---|---|---|---|
| 0 | 10% | DESCONTO | `SGF10` | 30 | laranja `#F4842A` |
| 1 | 30% | DESCONTO | `TRI30` | 8 | **roxo `#7C3AED`** |
| 2 | 15% | DESCONTO | `TRI15` | 22 | coral `#F0506E` |
| 3 | 20% | DESCONTO | `TRI20` | 18 | laranja `#F4842A` |
| 4 | DZG | POR R$ 1,00 | `DZG1` | 1 | **roxo `#7C3AED`** |
| 5 | GUIA | DE SUPLEMENTAÇÃO | `GUIASUPLEM` | 5 | coral `#F0506E` |

As fatias **roxas** são os prêmios em destaque (30% e DZG). `weight` é relativo — um prêmio com `weight: 30` é 30× mais provável que um com `weight: 1`; a soma não precisa dar 100.

### Exemplo de prêmio

```js
{ top: '30%', sub: 'DESCONTO', label: '30% DESCONTO', code: 'TRI30',
  weight: 8, color: '#7C3AED', textColor: '#fff',
  message: 'Desconto cheio. Não deixe dinheiro na mesa.' }
```

---

## Paleta

| Cor | Hex | Uso |
|---|---|---|
| Laranja | `#F4842A` | Fatias |
| Roxo (destaque) | `#7C3AED` | Fatias de destaque (30%, DZG) |
| Coral | `#F0506E` | Fatias |
| Fundo | `#3C1531 → #271036 → #150A22` | Gradiente da página |
| Aro | `#2A1640 → #140A22` | Aro escuro da roda |
| Lâmpadas | `#FFE7A0 / #F0A93C` | Luzes do aro |

**Fontes:** Bricolage Grotesque (display/fatias), Source Sans 3 (corpo), DM Mono (números).

---

## Como rodar

Arquivo estático único. Abra no navegador:

```bash
python3 -m http.server 8000   # depois acesse http://localhost:8000
```

### Reiniciar as tentativas (teste)

No console do navegador:

```js
localStorage.removeItem('tri-roleta-spins');
```

---

## Estrutura

```
index.html      # app completo: markup + estilos inline + lógica JS
README.md       # este arquivo
```

> Neste projeto o app vive em `Roleta de Prêmios.dc.html` (formato Design Component). Ao recriar no Claude Code como HTML puro, peça um `index.html` único — toda a lógica da classe `Component` vira um `<script>` com as mesmas constantes de configuração.
