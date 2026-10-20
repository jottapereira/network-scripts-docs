---
description: HUD, velocímetro, notificações, progresso, formulários e pedidos num só visual, em qualquer base.
---

# one\_hud

{% hint style="warning" %}
Versão 1.0 em teste. Esta documentação acompanha a versão em teste.
{% endhint %}

Toda a tela do jogador num produto: a HUD (status, voz, dinheiro, arma, localização, velocímetro, objetivo) **e** as
telas que todo servidor usa (notificação, progresso, formulário, confirmação, pedido Y/N, texto de ajuda). Instale,
desligue os equivalentes da sua base e **os scripts que você já tem passam a usar o visual novo sem alteração**.

## Destaques

* **Um visual só.** Notificação do ESX, barra do QBCore, diálogo do ox\_lib, pedido do vRP: tudo no mesmo estilo,
  sem três tipos de notificação na tela.
* **Status que só aparecem quando importam.** Colete e estresse acima de zero, fôlego e oxigênio enquanto gastam;
  valor crítico pulsa.
* **Velocímetro de verdade.** Arco segmentado de RPM com zona vermelha e limitador, marcha com troca animada,
  combustível e motor; 60 fps na tela com o jogo mandando 15 atualizações por segundo.
* **Minimapa encaixado no design**, rua, zona, bússola, hora e clima, só dirigindo (configurável).
* **Pedidos sem tirar o controle.** "Fulano quer te dar $ 500": o jogador responde com Y/N sem parar de andar.
* **Formulários completos.** Dinheiro, seleção, chips, interruptor, slider, data, validação e "segurar para
  confirmar".
* **Chips de estado** com cronômetro: procurado, repouso, buffs, zona segura... de qualquer script.
* **Ocioso = 0.00 ms.** A pé e parado, uma leitura a cada 200 ms enviando só o que mudou; a interface só anima
  quando algo se mexe.

## Funciona na sua base

| vRP Creative | Creative v4/v5 | vRPex | ESX | QBCore | Qbox | Standalone |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 |

## Páginas

* [Instalação](instalacao.md): um guia por base
* [Configuração](configuracao.md)
* [Integração com outros scripts](integracoes.md)
* [Compatibilidade](compatibilidade.md)
* [Problemas comuns](problemas-comuns.md)
* [Changelog](changelog.md)
