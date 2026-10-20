---
description: >-
  Seleção, criação e spawn de personagem num fluxo único e cinematográfico.
  A primeira impressão da sua cidade, no nível de um jogo AAA.
cover: ../.gitbook/assets/cover-characters.svg
coverY: 0
---

# one\_characters

A tela de personagens é a primeira coisa que todo jogador vê no seu servidor. O `one_characters` transforma
esse momento numa experiência de jogo: seus personagens aparecem **no mundo**, a câmera é cinematográfica,
e a entrada na cidade usa a mesma transição do GTA.

{% embed url="https://www.youtube.com/watch?v=S4YHOlFGhF8" %}
Showcase do one\_characters: seleção, criação e entrada na cidade.
{% endembed %}

{% hint style="success" %}
**Disponível** para vRP Creative (todas as gerações), vRPex, ESX, QBCore, Qbox e Standalone. [Comprar no Discord](https://discord.gg/ntqpUuHmYV)
{% endhint %}

## Destaques

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Line-up no mundo</strong></td><td>Todos os personagens da conta lado a lado numa cena real, cada um com a própria roupa e postura. A câmera desliza até o escolhido.</td></tr><tr><td><strong>Prévia do spawn</strong></td><td>Antes de entrar, a câmera sobrevoa ao vivo o local escolhido, com o nome da rua. Volte com Esc quando quiser.</td></tr><tr><td><strong>Entrada estilo GTA</strong></td><td>A transição "Switch" nativa do GTA: a câmera sobe ao céu e mergulha no seu personagem.</td></tr><tr><td><strong>Retratos reais</strong></td><td>O rosto de cada personagem aparece na interface, gerado do próprio jogo.</td></tr><tr><td><strong>Criador em 6 etapas</strong></td><td>Identidade, herança, rosto, cabelo, roupas e revisão, tudo aplicado ao vivo no personagem.</td></tr><tr><td><strong>Documento de identidade</strong></td><td>A revisão mostra o documento do personagem com foto, nome e nacionalidade.</td></tr></tbody></table>

## Seleção

* Troque de personagem com `A`/`D`, gire com o mouse, aproxime com o scroll.
* Painel com nascimento, telefone, carteira, banco, emprego, horas jogadas e último acesso.
* **Onde acordar**: última localização, propriedades do personagem e pontos públicos configuráveis.
* **Segure para entrar** e **segure para excluir**: nada acontece por um clique acidental.
* Slots bloqueados viram vitrine para apoiadores do seu servidor.

## Criação

| Etapa | O que o jogador define |
|---|---|
| **Identidade** | nome, sobrenome, data de nascimento (com idade calculada), sexo, nacionalidade e história |
| **Herança** | pai e mãe entre os 46 rostos do GTA Online, semelhança e tom de pele |
| **Rosto** | 20 ajustes de estrutura facial, cada um com as pontas escritas (Fino ↔ Largo) |
| **Cabelo** | corte, cor e reflexo com a paleta real do jogo, barba, sobrancelhas e olhos |
| **Roupas** | peça por peça, só com modelos e texturas que existem no seu servidor |
| **Revisão** | documento de identidade com foto e confirmação das regras |

Câmera com rosto, tronco e corpo, giro por arrastar, zoom e **sortear aparência**.

## Detalhes que fazem diferença

* **Sons dos menus do GTA** em cada hover e clique, respeitando o volume de efeitos do jogo.
* **Navegação completa por teclado**, com os atalhos sempre visíveis na tela.
* **Validação no servidor** de nome, idade, nacionalidade, aparência, slot e local de spawn. O cliente nunca envia coordenadas.
* **Roupa salva no seu sistema atual**: barbearias e lojas continuam funcionando com o personagem criado.
* **0.00 ms** depois que o jogador entra na cidade. O recurso fica totalmente parado.

## Compatibilidade

| Framework | Substitui |
|---|---|
| vRP Creative (Network, Origens, Bewitched) | `spawn` |
| vRP Creative v4/v5 | `vrp_spawn` e `vrp_login` |
| vRPex | criação de identidade e escolha de spawn |
| ESX Legacy | `esx_multicharacter` |
| QBCore | `qb-multicharacter` e `qb-spawn` |
| Qbox | menu de personagens do `qbx_core` |
| Standalone | multipersonagem completo, sem framework |

{% content-ref url="../scripts/one-characters/" %}
[one-characters](../scripts/one-characters/)
{% endcontent-ref %}
