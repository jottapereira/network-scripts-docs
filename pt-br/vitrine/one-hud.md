---
description: >-
  A tela inteira do jogador num visual só: HUD, velocímetro e as telas que todo servidor usa.
cover: ../.gitbook/assets/cover-hud.svg
coverY: 0
---

# one\_hud

A HUD (status, voz, dinheiro, arma, localização, velocímetro, objetivo) **e** as telas que todo servidor usa: notificação, progresso, formulário,
confirmação, pedido Y/N e texto de ajuda. Instale, desligue os equivalentes da sua base e **os scripts que você já tem passam a usar o visual novo**.

{% embed url="https://www.youtube.com/watch?v=XRstOl4t62M" %}
Showcase do one\_hud.
{% endembed %}

{% hint style="success" %}
**Disponível** para vRP Creative (todas as gerações), vRPex, ESX, QBCore, Qbox e Standalone. [Comprar no Discord](https://discord.gg/ntqpUuHmYV)
{% endhint %}

## Destaques

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Um visual só</strong></td><td>Notificação do ESX, barra do QBCore, diálogo do ox_lib, pedido do vRP: tudo no mesmo estilo, sem três tipos de notificação na tela.</td></tr><tr><td><strong>Status que só aparecem quando importam</strong></td><td>Colete e estresse acima de zero, fôlego e oxigênio enquanto gastam; valor crítico pulsa.</td></tr><tr><td><strong>Velocímetro de verdade</strong></td><td>Arco segmentado de RPM com zona vermelha e limitador, marcha com troca animada, combustível e motor.</td></tr><tr><td><strong>Pedidos sem tirar o controle</strong></td><td>"Fulano quer te dar $ 500": o jogador responde com Y/N sem parar de andar.</td></tr><tr><td><strong>Formulários completos</strong></td><td>Dinheiro, seleção, chips, interruptor, slider, data, validação e "segurar para confirmar".</td></tr><tr><td><strong>Chips de estado</strong></td><td>Procurado, repouso, buffs, zona segura, com cronômetro, de qualquer script.</td></tr></tbody></table>

## A HUD

| Elemento | O que mostra |
|---|---|
| **Status** | vida, colete, fome, sede, estresse, fôlego e oxigênio; só aparecem quando importam, e o valor crítico pulsa |
| **Voz** | quem está falando e o alcance (pma-voice, SaltyChat e variantes do Creative) |
| **Dinheiro e emprego** | carteira, banco e emprego, atualizados pelos eventos do seu framework |
| **Arma** | nome, modo e munição |
| **Localização** | rua, zona, bússola, hora e clima |
| **Velocímetro** | RPM em arco segmentado com zona vermelha e limitador, marcha, combustível, motor, cinto e limitador de velocidade |
| **Objetivo** | título, tempo restante e passos de uma missão, de qualquer script |

O **minimapa** é encaixado no design (redondo, como o do vRP Creative, ou retangular) e pode aparecer só dirigindo.

## As telas do servidor

| Tela | Para quê |
|---|---|
| **Notificação** | seis tipos (info, sucesso, erro, aviso, dinheiro e polícia) com duração configurável |
| **Progresso** | barra com animação, bloqueio de controles e cancelamento |
| **Formulário** | texto, número, senha, seleção, chips, interruptor, slider, dinheiro e data, com validação |
| **Confirmação** | com modo perigo e "segurar para confirmar" |
| **Pedido Y/N** | o jogador aceita ou recusa andando |
| **Texto de ajuda** | tecla e ação perto do alvo |
| **Legenda e chips** | frases de cena e estados com cronômetro |

## Detalhes que fazem diferença

* **60 fps** na tela com o jogo mandando 15 atualizações por segundo.
* **0.00 ms** parado: uma leitura a cada 200 ms enviando só o que mudou.
* **Cinto próprio** só liga quando a base não tem um; o do Creative, do qb-smallresources e do qbx\_seatbelt são respeitados.
* **Detecção automática** de voz, combustível e cinto: nada para configurar na maioria dos servidores.
* **Compatível com os scripts que você já tem**: respostas no lugar de `esx_notify`, `esx_progressbar`, `esx_textui`, `progressbar`, `qb-input` e do `ox_lib`, sem editar nenhum deles.

## Para o dono do servidor

* **Sua marca:** sigla ou logo no canto, e cor de destaque própria.
* **Unidades e moeda:** km/h ou mph, símbolo do dinheiro e chip de ID (servidor ou personagem).
* **Minimapa:** sempre, só dirigindo ou nunca; redondo ou retangular.
* **Teclas:** aceitar, recusar, cancelar progresso, cinto e limitador de velocidade.
* **Fontes de dados abertas:** de onde vem cada status, voz, combustível e cinto fica num arquivo editável.
* **Jogador no controle:** comando `/hud` para esconder e mostrar.
* **Idiomas:** português e inglês.

## Compatibilidade

| Base | Status | O que ele substitui |
|---|:-:|---|
| vRP Creative | 🧪 | `hud`, `notify`, `Progress`, `keyboard`, `request` e `notifyitem` |
| vRP Creative v4/v5 | 🧪 | HUD e notificações da base (ponte no `vrp`) |
| vRPex | 🧪 | HUD e notificações da base (ponte no `vrp`) |
| ESX | 🧪 | `esx_hud`, `esx_notify`, `esx_progressbar` e `esx_textui` |
| QBCore | 🧪 | `qb-hud`, `progressbar`, `qb-input` e `DrawText` (ponte no `qb-core`) |
| Qbox | 🧪 | `qbx_hud` e as telas do `ox_lib` (ponte) |
| Standalone | 🧪 | HUD completa, sem framework |

✅ estável (validado em jogo) · 🧪 beta (validado em laboratório nas bases reais; relatos no [Discord](https://discord.gg/ntqpUuHmYV))

Menus de contexto, skill check e chamados da polícia continuam com as telas da base.

## O que vem na compra

* O recurso `one_hud` e o `one_lib` (biblioteca comum dos produtos Network Scripts).
* Um guia de instalação para cada base, com a documentação completa em português.
* Exports de cliente e servidor para usar as telas nos seus scripts.
* Atualizações dentro da versão comprada e suporte por ticket no Discord.

## Perguntas frequentes

<details>
<summary>Preciso reescrever os scripts que já uso?</summary>

Não. Desligue o recurso original (mantendo a pasta) e os pedidos de notificação, progresso, formulário e texto de ajuda
dos seus scripts passam a usar o visual do `one_hud`. Em algumas bases a troca é uma linha no `fxmanifest.lua`.

</details>

<details>
<summary>Funciona com o meu sistema de voz e de combustível?</summary>

Detecta pma-voice, SaltyChat, ox\_fuel, LegacyFuel, cdn-fuel, ps-fuel e lc\_fuel automaticamente. Para outro sistema,
o arquivo de fontes de dados é aberto.

</details>

<details>
<summary>Posso usar nos scripts novos que eu escrever?</summary>

Sim. O `one_hud` tem exports de cliente e servidor, e o `one_lib` usa o `one_hud` quando ele está instalado.

</details>

<details>
<summary>Pesa no cliente?</summary>

Não. Parado, ele faz uma leitura a cada 200 ms e envia só o que mudou.

</details>

{% content-ref url="../scripts/one-hud/" %}
[one-hud](../scripts/one-hud/)
{% endcontent-ref %}
