---
description: Comandos de admin, logs no Discord e integrações.
---

# Administração e logs

## Comandos

| Comando | Quem | O que faz |
|---|---|---|
| `/oficina_dar <id> <estilo\|componente> [arma\|todas]` | Admin, console | Entrega skins sem cobrar. `estilo` vale para todas as armas (ou só para a arma informada). |
| `/oficina_tirar <id> <estilo\|componente> [arma\|todas]` | Admin, console | Retira skins da coleção do jogador. |
| `workshop_skins` | Console | Recarrega o `skins.json` e mostra quantas skins, armas e estilos a oficina encontrou. |
| `workshop_export` | Console | Gera de novo os arquivos de cadastro dos itens em `install/`. |
| `workshop_selftest` | Console | Autoteste: configuração, banco, catálogo, pacotes, cobrança (dinheiro, itens, gemas), compra de skin e aplicar acessórios, com um jogador de mentira. Não altera nada do servidor. |
| `/oficina`, `/skinlab` | Com `setr one_workshop:debug true` | Bancada de teste na sua frente e vitrine de skins (escolha arma e skin, veja na inspeção 360°, sem gravar nem cobrar). |

Admin = ACE `oneworkshop.admin` (`add_ace group.admin oneworkshop.admin allow`) ou um grupo de `Config.AdminGroups`.

Exemplos:

```
/oficina_dar 12 dragao                 -- Dragão em todas as armas
/oficina_dar 12 galaxia pistol         -- Galáxia só na pistola
/oficina_tirar 12 dragao todas
```

## Logs no Discord

`set one_workshop:webhook "..."` no `server.cfg`. Eventos (cada um liga e desliga em `Config.Logs`):

* **apply:** personalização aplicada (quem, peças, cor, forma de pagamento, bancada).
* **buy:** skin comprada (quem, arma, skin, forma de pagamento, bancada).
* **admin:** skins entregues ou retiradas.

## Integrações

* Evento de servidor `one_workshop:server:sale`: `{ src, bench, society, amount, share, kind, label }` a cada venda em
  dinheiro.
* Evento de cliente `one_workshop:client:applied`: `{ weapon, components, tint, camoColor }` depois de aplicar.
