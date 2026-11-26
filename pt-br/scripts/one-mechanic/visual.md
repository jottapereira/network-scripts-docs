---
description: Catálogo do Mod Kit, pintura com nota, rodas, neon e adesivos.
---

# Visual e pintura

## Catálogo

O terminal lista só os tipos de modificação que o **modelo do carro** tem (Mod Kit do GTA), com o nome do jogo e o atual marcado. Passar o mouse numa opção
mostra a **prévia local**: nada é gravado nem cobrado, e fechar o terminal volta ao original. "Pôr na ordem" cria a linha com o preço do servidor;
a mudança só vale quando o mecânico marca a linha como feita.

Os tipos de **desempenho** do Mod Kit (motor, freio, câmbio, suspensão, blindagem) ficam escondidos por padrão: o desempenho é das peças
(`Config.Visual.performanceMods` mostra de novo).

## Pintura com nota

O GTA não pinta por painel, então a Forja não promete isso. A pintura é um **processo com nota**:

1. **Mistura**: cor primária, secundária, acabamento (sólida, metálica, perolada, acetinada, fosca, cromada, camaleão) e pérola.
2. **Minijogo**: preparo, mistura, aplicação e polimento (barra com cursor; `Config.Visual.paintGame = 'off'` usa nota fixa).
3. A **nota S, A, B ou C** limita-se pela perícia de pintura e define o **preço** e a **durabilidade do verniz**.
4. O verniz **gasta com os km**: desbota e oxida (o carro vai ficando sujo). O serviço **Polimento e cera** devolve vida.

Pintura só na cabine (ou box). Cromada e camaleão custam mais e duram menos.

## Rodas, stance, neon, película e adesivos

Rodas (tipo e modelo), cambagem, altura e offset, neon (lados e cor), xenônio, película (0 a 6), estilo da placa e adesivos. Altura e cambagem dependem
de natives que variam por build do jogo: se alguma não existir na sua build, o resto continua funcionando.

**Adesivos de pacotes de terceiros:** recursos externos dão nome aos índices de livery dos próprios carros (veja *Conteúdo*). O editor de vinil livre por
textura não existe enquanto o GTA não permitir textura por entidade.
