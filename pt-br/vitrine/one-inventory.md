---
description: >-
  Bolsos, mochila, baús, lojas, bancadas e porta-malas num sistema só. Os scripts que você já tem continuam funcionando.
cover: ../.gitbook/assets/cover-inventory.svg
coverY: 0
---

# one\_inventory

Tudo que envolve itens num lugar só: bolsos, mochila, equipamento, chão, porta-malas, porta-luvas, baús, lojas, bancadas e revista.
O servidor é a única autoridade: nada de item duplicado, e a interface responde na hora.

{% embed url="https://www.youtube.com/watch?v=JvsmuEtCk-I" %}
Showcase do one\_inventory.
{% endembed %}

{% hint style="success" %}
**Disponível** para vRP Creative (todas as gerações), vRPex, ESX, QBCore, Qbox e Standalone. [Comprar no Discord](https://discord.gg/ntqpUuHmYV)
{% endhint %}

## Destaques

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Seu personagem na tela</strong></td><td>A pé, a câmera abre no personagem (gire arrastando). Em baús, lojas e veículos ele aparece como parte da interface.</td></tr><tr><td><strong>Itens com vida</strong></td><td>Número de série, durabilidade por tempo, munição na arma e dados da base, tudo como metadado do item.</td></tr><tr><td><strong>Mochilas e maletas de verdade</strong></td><td>Equipada, a mochila vira um inventário próprio, e o peso do que está dentro conta para quem carrega.</td></tr><tr><td><strong>Mundo físico</strong></td><td>Item solto vira objeto no chão, e o porta-malas abre a tampa com a animação do personagem.</td></tr><tr><td><strong>Lojas e bancadas</strong></td><td>Estoque gravado, moeda em dinheiro ou item e fila de fabricação que continua com o jogador offline.</td></tr><tr><td><strong>Compatível com o mercado</strong></td><td>Scripts feitos para ox_inventory e qb-inventory funcionam sem alteração. No Creative, mantém roubos, drogas e usos de item da sua base.</td></tr></tbody></table>

## Tudo que envolve itens

| Onde | O que o jogador faz |
|---|---|
| **Bolsos e equipamento** | guarda itens, veste chapéu, óculos, máscara, colete, luvas e mochila; peças de roupa viram itens e voltam ao personagem |
| **Mochilas e maletas** | equipa e ganha um inventário extra embaixo dos bolsos; no Creative, a mochila aparece nas costas |
| **Chão** | itens soltos viram objetos no mundo, agrupados e com tempo de vida |
| **Veículos** | porta-malas (mirando no carro, segure `ALT`) e porta-luvas, com capacidade por classe ou modelo |
| **Baús** | fixos (cofres de facção, armários) ou pessoais, com grupo e cargo mínimo |
| **Lojas** | compra e venda, estoque gravado, moeda em dinheiro, banco, sujo ou qualquer item |
| **Bancadas** | receitas com ingredientes, tempo, nível e planta; a fila continua correndo com o jogador offline |
| **Revista** | olhar e pegar itens de outro jogador, quando a regra do seu servidor permitir |

## Interface de jogo

* Arrastar com **Shift** (metade) e **Ctrl** (um), hotbar 1–5, menu de contexto, busca e filtros.
* **Peso que pesa**: carga demais e o personagem não corre, depois anda devagar.
* **Rastro de digitais** para a polícia analisar.
* **Interação 3D**: lojas, bancadas e baús mostram uma marca ao chegar perto e o cartão de opções no alcance.
* **0.00 ms** com o inventário fechado: a interface recebe só as diferenças.

## Detalhes que fazem diferença

* **Sem duplicação:** toda movimentação é validada e aplicada de uma vez no servidor; a interface desfaz se o servidor recusar.
* **Gravação em lote** no banco, em intervalo configurável.
* **Migração dos dados** de `ox_inventory` e `qb-inventory` por comando. No Creative, cada inventário vem sozinho na primeira vez que é usado.
* **Imagens dos itens** reaproveitadas do inventário antigo.
* **Comandos de admin** (`/giveitem`, `/removeitem`, `/clearinventory`) e permissões por ACE ou grupo.
* **Integra com a Oficina:** as skins e acessórios das armas ficam salvas no próprio item.

## Para o dono do servidor

* **Capacidades:** slots e peso dos bolsos, mochilas, porta-malas por classe de veículo, porta-luvas e baús.
* **Lojas, baús e bancadas** definidos em tabelas simples, ou registrados por script com exports.
* **Catálogo de itens:** importa o da sua base (no Creative, o `Item.lua`) e deixa você sobrescrever só o que quiser.
* **Regras abertas:** peso máximo por VIP, quem pode revistar, nível de fabricação, porta-malas personalizado.
* **Hooks que cancelam** movimentação, uso, entrega e soltar, para as regras do seu servidor.
* **Exports de servidor e cliente** para usar de qualquer script.
* **Idiomas:** português e inglês.

## Compatibilidade

| Base | Status | Como os outros scripts chegam ao inventário |
|---|:-:|---|
| vRP Creative | ✅ | ponte no `vrp`; gameplay da base importado |
| vRP Creative v4/v5 | 🧪 | ponte no `vrp`; `vrp_inventory` da base importado |
| vRPex | 🧪 | ponte no `vrp` e escolhas do menu do vRP |
| ESX | 🧪 | camada `ox_inventory` |
| QBCore | 🧪 | camada `qb-inventory` |
| Qbox | 🧪 | camada `ox_inventory` |
| Standalone | 🧪 | `exports.one_inventory` |

✅ estável (validado em jogo) · 🧪 beta (validado em laboratório nas bases reais; relatos no [Discord](https://discord.gg/ntqpUuHmYV))

## O que vem na compra

* O recurso `one_inventory` e o `one_lib` (biblioteca comum dos produtos Network Scripts).
* Um guia de instalação para cada base e o guia de migração do inventário antigo.
* Documentação completa de configuração, exports e hooks, em português.
* Atualizações dentro da versão comprada e suporte por ticket no Discord.

## Perguntas frequentes

<details>
<summary>Os meus scripts de ox_inventory e qb-inventory vão funcionar?</summary>

Sim, sem alteração. O `one_inventory` responde aos exports desses inventários. Desligue o inventário antigo
(mantendo a pasta, porque os itens são lidos dela).

</details>

<details>
<summary>Perco os itens dos jogadores ao trocar de inventário?</summary>

Não. `oneinv_migrate ox` e `oneinv_migrate qb` copiam jogadores, baús, porta-malas e porta-luvas sem apagar a
origem. No Creative, cada inventário é trazido sozinho no primeiro uso.

</details>

<details>
<summary>Dá para duplicar item?</summary>

O servidor valida e aplica cada movimentação de uma vez. Se algo falha, o cliente volta ao estado real.

</details>

<details>
<summary>Pesa no servidor?</summary>

Com o inventário fechado, nada roda em loop (0.00 ms). A gravação no banco é em lote.

</details>

{% content-ref url="../scripts/one-inventory/" %}
[one-inventory](../scripts/one-inventory/)
{% endcontent-ref %}
