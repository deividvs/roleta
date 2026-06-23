# Roleta de Prêmios — T.R.I. 2.0

App de "spin the wheel" (roleta de prêmios) em **HTML, CSS e JavaScript puro**, sem framework, sem build. Gira uma roda dividida em fatias, sorteia um prêmio por probabilidade configurável, limita as tentativas por navegador e captura o e-mail antes de revelar o código de desconto.

> Brand: Victor Darido / T.R.I. 2.0 — "Precision Agriculture": verde-floresta como primária, âmbar como acento de "dinheiro", neutros terrosos sobre fundo escuro.

---

## Prompt para o Claude Code

Cole o texto abaixo no Claude Code para gerar o projeto do zero:

```
Crie um app de roleta de prêmios ("spin the wheel") em HTML, CSS e JavaScript puro
(um único arquivo index.html, sem framework e sem build), com:

- Roda circular com 8 fatias usando conic-gradient, cores alternadas verde-floresta
  (#064C34 / #0E9F6E / #03261A) e âmbar (#D4A017 / #E8B931) para prêmios raros.
- Rótulos de prêmio posicionados radialmente no centro de cada fatia (transform rotate).
- Ponteiro âmbar fixo no topo apontando o resultado.
- Hub central circular configurável com o texto "T.R.I. 2.0" (espaço para logo).
- Botão "Girar" que anima a rotação com transform: rotate + transition
  cubic-bezier(0.16,1,0.3,1) de ~4.2s (desaceleração suave) parando na fatia sorteada.
- Array de configuração PRIZES com label, code, weight (peso/probabilidade),
  color, textColor e message por prêmio.
- Sorteio por peso, com opção FORCE_INDEX para forçar um resultado específico.
- Limite de 3 tentativas (MAX_SPINS) persistido em localStorage: ao recarregar
  ou voltar, o contador continua de onde parou; ao zerar, exibe aviso
  "Suas tentativas acabaram" e desativa o botão.
- Modal de resultado com a mensagem do prêmio e, antes de revelar o código,
  um campo de e-mail validado (REQUIRE_EMAIL).
- Layout responsivo para mobile e desktop usando clamp() e min(86vw,440px) na roda.
- Tipografia: Bricolage Grotesque (títulos), Source Sans 3 (corpo), DM Mono (números),
  via Google Fonts.
- Código comentado em português para personalizar prêmios, cores, textos e pesos.
```

---

## Funcionalidades

- **Roda configurável** — 6 a 8 fatias, cada uma com rótulo, código, peso, cor e mensagem.
- **Probabilidade por peso** — `weight` define a chance relativa de cada prêmio.
- **Resultado forçado** — `FORCE_INDEX` força sempre uma fatia (útil para demos/QA).
- **Tentativas limitadas e persistentes** — `MAX_SPINS` giros gravados em `localStorage`; o navegador reconhece quem já jogou.
- **Captura de e-mail** — quando `REQUIRE_EMAIL = true`, o código só é revelado após e-mail válido.
- **Responsivo** — funciona em qualquer celular ou desktop.

---

## Configuração (no topo da classe `Component`)

| Campo | O que faz |
|---|---|
| `PRIZES[]` | Lista de prêmios. Cada item: `label`, `code`, `weight`, `color`, `textColor`, `message`. |
| `CENTER_LABEL` | Texto/logo no centro da roda (atual: `T.R.I. 2.0`). |
| `MAX_SPINS` | Número de tentativas permitidas (atual: `3`). |
| `REQUIRE_EMAIL` | `true` exige e-mail antes de revelar o código. |
| `FORCE_INDEX` | `null` = sorteio por peso. Um índice (0-based) força aquele prêmio. |
| `STORAGE_KEY` | Chave do `localStorage` que guarda os giros usados (`tri-roleta-spins`). |

### Exemplo de prêmio

```js
{ label: '30% OFF', code: 'TRI30', weight: 8, color: '#064C34', textColor: '#fff',
  message: 'Desconto cheio. Não deixe dinheiro na mesa.' }
```

`weight` é relativo: um prêmio com `weight: 30` é 30× mais provável que um com `weight: 1`. A soma não precisa dar 100.

---

## Paleta da marca

| Token | Hex | Uso |
|---|---|---|
| forest-950 | `#021A0E` | Fundo escuro / texto sobre âmbar |
| forest-800 | `#064C34` | Fatias |
| forest-600 | `#0E9F6E` | Ação / fatias |
| forest-400 | `#3DDBA0` | Acento sobre escuro |
| amber-400 | `#E8B931` | Ponteiro, hub, CTA, prêmio raro |
| amber-500 | `#D4A017` | Acento "dinheiro" |
| cream | `#FAF8F3` | Fundo do modal de resultado |

**Fontes:** Bricolage Grotesque (display), Source Sans 3 (corpo), DM Mono (números).

---

## Como rodar

É um único arquivo estático. Basta abrir no navegador:

```bash
# qualquer servidor estático serve
python3 -m http.server 8000
# depois acesse http://localhost:8000
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
