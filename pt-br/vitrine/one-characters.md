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

{% embed url="https://www.youtube.com/watch?v=J-Bzgvd9RtM" %}
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

## Para o dono do servidor

* **Marca da sua cidade:** sigla, nome e subtítulo no canto da tela, e cor de destaque própria.
* **Regras de identidade:** tamanho do nome, nomes proibidos, idade mínima e máxima, lista de nacionalidades e tamanho da história.
* **Slots e apoiadores:** quantos cards aparecem, e slots extras por VIP, cargo ou qualquer regra sua.
* **Spawns:** pontos públicos, local de nascimento do personagem novo e locais exclusivos por personagem (casas, base da facção).
* **Cena própria:** mova o line-up e o criador para qualquer lugar do mapa; a câmera se ajusta às paredes sozinha.
* **Hooks abertos:** itens iniciais, mensagem de boas-vindas e o que acontece ao aparecer na cidade, sem mexer no código protegido.
* **Idiomas:** português e inglês, com todos os textos editáveis.

## Compatibilidade

| Base | Status | O que ele substitui |
|---|:-:|---|
| vRP Creative (Network, Origens, Bewitched) | ✅ | `spawn` |
| vRP Creative v4/v5 | 🧪 | `vrp_spawn` e `vrp_login` |
| vRPex | 🧪 | criação de identidade e escolha de spawn |
| ESX Legacy | 🧪 | `esx_multicharacter` |
| QBCore | 🧪 | `qb-multicharacter` e `qb-spawn` |
| Qbox | 🧪 | menu de personagens do `qbx_core` |
| Standalone | 🧪 | multipersonagem completo, sem framework |

✅ estável (validado em jogo) · 🧪 beta (validado em laboratório nas bases reais; relatos no [Discord](https://discord.gg/ntqpUuHmYV))

## O que vem na compra

* O recurso `one_characters` e o `one_lib` (biblioteca comum dos produtos Network Scripts).
* Instalação guiada para a sua base, com a documentação completa em português.
* Interface em português e inglês.
* Atualizações dentro da versão comprada e suporte por ticket no Discord.

## Perguntas frequentes

<details>
<summary>Preciso apagar os personagens que já existem?</summary>

Não. Os dados do personagem continuam nas tabelas do seu framework. O produto cria uma tabela própria só para o
que os frameworks não guardam de forma padronizada (nascimento, nacionalidade, história, horas jogadas).

</details>

<details>
<summary>As lojas de roupa e barbearias continuam funcionando?</summary>

Sim. A roupa é salva no sistema que a sua base já usa.

</details>

<details>
<summary>Posso trocar o cenário da seleção?</summary>

Sim. A cena padrão é a sala de line-up do criador do GTA Online, mas você move o line-up e o criador para qualquer
lugar do mapa.

</details>

<details>
<summary>Pesa no servidor?</summary>

Não. Depois que o jogador entra na cidade o recurso fica parado (0.00 ms).

</details>

{% content-ref url="../scripts/one-characters/" %}
[one-characters](../scripts/one-characters/)
{% endcontent-ref %}
