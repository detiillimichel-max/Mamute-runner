# 🦣 Mamute Runner v2

Um Dino Runner clone feito em HTML5 Canvas, mas com mamute, vidas, sistema de agachar e obstáculos em emoji. Versão 2 totalmente reescrita para ser responsiva, justa e pronta para mobile.

**Demo:** abra o arquivo `mamute-runner-v2_agentic_artifact_1_b999d9a92709.html` ou a preview gerada no chat.

### ✨ O que mudou da v1 para v2

**Bugs corrigidos**
- Emoji vazio `"  "` que criava obstáculo invisível removido
- Duplicata de 🌵 removida
- Canvas com `devicePixelRatio` correto. Hitbox não desalinha mais no celular
- `AudioContext` agora faz `resume()` no primeiro gesto, funciona no iOS
- `gameSpeed` com teto máximo de 14, não fica impossível em 100 pontos
- Obstáculo removido ao colidir, evita dano duplo no mesmo cacto
- `localStorage` com `try/catch` e fallback para `NaN`

**Gameplay novo**
- Vidas visuais com ❤️, 3 vidas + 90 frames de invulnerabilidade com efeito blink
- Agachar: reduz hitbox para passar por pássaros voando
- Obstáculos terrestres e aéreos com alturas diferentes
- Partículas de poeira ao pular/aterrar e explosão ao tomar dano
- Screen shake leve no hit
- Chão com parallax em 2 camadas + nuvens
- Pausa com tecla P

### 🎮 Como jogar

Desvie de 🦛🦒🦍🐆🌵🔥⚡ e companhia. Cada obstáculo ultrapassado vale 1 ponto. A cada 6 pontos a velocidade aumenta.

**PC**
- **Pular / Reiniciar:** Espaço, Seta Cima ou W
- **Agachar:** Seta Baixo ou S (segure)
- **Pausar:** P
- **Mutar:** botão 🔊 no topo

**Mobile**
- Toque no lado direito da tela: pular
- Toque no lado esquerdo: agachar
- Botões grandes translúcidos aparecem automaticamente em telas pequenas

### 🛠️ Stack

- React + Canvas 2D API, sem libs externas
- Física com deltaTime: `dt = delta / 16.66` com cap de 32ms para consistência entre 60Hz e 144Hz
- `requestAnimationFrame` para loop principal
- Web Audio API para SFX procedurais, sem arquivos de áudio
- `localStorage` apenas para `highScore`

### 📁 Estrutura

```
/
├── index.html          # v1 original
├── mamute-runner-v2    # v2 polida em React (artifact gerado)
└── README.md           # este arquivo
```

O loop principal usa `useRef` para estado mutável e evita re-render. `useState` apenas para espelhar HUD.

```js
player = { x, y, w:58, h:58, vy, gravity:0.68, jump:-14, ducking }
obstacle = { x, y, w, h, emoji, isFlying, passed }
state = { score, high, speed, maxSpeed:14, lives, invul, over, paused }
```

### 🚀 Como rodar local

1. Baixe o HTML da v2
2. Abra direto no navegador com duplo clique, não precisa de servidor
3. Ou sirva com: `npx serve .`

### 🎨 Como customizar

- **Trocar emojis:** edite o array `EMOJIS` no topo do script
- **Dificuldade:** mude `maxSpeed`, `nextSpawn = 60 + random*70` e `gravity`
- **Tamanho do mamute:** `player.w / h` e `font` no draw

### 🗺️ Roadmap

- [ ] Power-up de coração extra ❤️‍🩹 e escudo temporário
- [ ] Ciclo dia/noite baseado no score
- [ ] Sprite sheet animado do mamute correndo em vez de emoji estático
- [ ] Leaderboard local com nome
- [ ] Modo PWA para instalar no celular

Feito com carinho para corrigir aquele obstáculo invisível que te matava do nada. Se quiser, te entrego a v3 já com sprite e sons 8-bit.
