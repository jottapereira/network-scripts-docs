---
description: Os padrões que seguimos em todos os nossos sistemas.
---

# Boas práticas

Estes são os padrões dos sistemas da Network Scripts. Seguir os mesmos no seu servidor deixa tudo mais
rápido e seguro.

## Desempenho

* **Nenhum loop por frame fora de uso.** Um loop com `Wait(0)` só existe enquanto algo está na tela ou perto do jogador.
* **Proximidade em camadas.** Um loop lento (500 a 1500 ms) decide *se* o jogador está perto; só então um loop rápido começa.
* **Eventos em vez de consulta.** Reaja a mudanças ([`One.Cache.OnChange`](../one-lib/modulos/cache.md)) em vez de perguntar a cada X ms.
* **Meta:** 0.00 a 0.01 ms no `resmon` com o recurso ocioso.

## Segurança

* O cliente **nunca** define preço, quantidade recebida, item, dano ou permissão.
* Todo evento de servidor confere: jogador carregado, permissão, distância (pelas coordenadas do servidor), posse e intervalo entre usos.
* Todo evento exposto ao cliente tem limite de frequência.
* Ação suspeita vai para [`One.Log.Exploit`](../one-lib/modulos/log.md). Registre antes de punir.

## Interface (NUI)

* **Não use `backdrop-filter` nem `filter: blur()`**: o navegador do FiveM desenha como um bloco preto. Para desfocar algo da própria interface, use filtro SVG (`<feGaussianBlur>`).
* Feche com **Esc** sempre, e nunca deixe o foco preso: use [`One.Focus`](../one-lib/modulos/focus.md).
* Interface fechada não deve receber mensagens nem rodar timers.
* Textos sempre em arquivos de idioma, nunca escritos direto no código.
