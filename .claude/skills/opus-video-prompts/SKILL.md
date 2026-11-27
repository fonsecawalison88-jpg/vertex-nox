---
name: opus-video-prompts
description: Galeria de 703 prompts reais que geraram vídeos feitos por código com Claude (motion graphics, explainers, cenas 3D, jogos e interativos), com autor, categoria e tecnologia (Canvas, SVG, GSAP, three.js, Remotion...). Use quando a pessoa quiser ideias ou referências para um vídeo animado, pedir "exemplos de prompt", "inspiração", "o que dá pra fazer", ou quando um pedido de vídeo estiver vago e um exemplo real ajudar a definir estilo e escopo.
---

# Galeria de prompts de vídeo (awesome-opus5-5-videos)

`SKILL_DIR` é a pasta deste arquivo. Os dados estão em `SKILL_DIR/videos.json`: uma lista de 703 itens com
`slug`, `author`, `author_url`, `post_url`, `category`, `tech_tags`, `prompt` (texto completo, às vezes em chinês, japonês etc.).

Categorias: `motion-graphics` (~370), `3d` (~117), `explainer` (~116), `games` / interativos (~100).

## Como usar

1. Não leia o arquivo inteiro (800 KB). Filtre com Python:

```bash
python3 -I - "$SKILL_DIR/videos.json" <<'EOF'
import json, sys
d = json.load(open(sys.argv[1]))
termo, cat = "logo", None          # ajuste
for v in d:
    if cat and v["category"] != cat: continue
    if termo.lower() in v["prompt"].lower():
        print(f'[{v["category"]}] {",".join(v["tech_tags"])} @{v["author"]}\n  {v["prompt"][:300]}\n  {v["post_url"]}\n')
EOF
```

Use `print(sorted({v["category"] for v in d}))` e `sorted({t for v in d for t in v["tech_tags"]})` para ver os valores existentes.

2. Mostre 3 a 5 exemplos curtos e relevantes (traduza para o idioma da pessoa), com o link do post original como crédito.
3. Use o prompt escolhido como ponto de partida e adapte ao pedido. Para executar, combine com a skill de produção certa:
   `remotion-motion-graphics` / `remotion-best-practices` (Remotion), `teardown` (máquina em 3D), ou HTML + Canvas/GSAP.

Os prompts são de autores terceiros (posts públicos no X), reunidos em github.com/yihui-dev/awesome-opus5-5-videos (MIT). Cite o autor ao reaproveitar.
