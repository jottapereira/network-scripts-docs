---
description: A biblioteca base de todos os produtos Network Scripts. Grátis.
cover: ../.gitbook/assets/cover-lib.svg
coverY: 0
---

# Visão geral

O `one_lib` é a camada entre os nossos produtos e o seu framework. Ele detecta a base em que está rodando
e oferece uma API única, a mesma em todos os frameworks.

{% hint style="success" %}
O `one_lib` é **grátis** e acompanha qualquer produto. Instale uma vez; todos os produtos usam a mesma cópia.
{% endhint %}

## O que ele faz

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Detecção automática</strong></td><td>Identifica vRP Creative, ESX, QBCore, Qbox ou Standalone, e o sistema de roupa em uso.</td></tr><tr><td><strong>API única</strong></td><td>Personagem, dinheiro, grupos, notificações, aparência e personagens funcionam igual em todas as bases.</td></tr><tr><td><strong>Carregamento sob demanda</strong></td><td>Cada módulo só é carregado quando um script o usa. Sem custo para o que não é usado.</td></tr><tr><td><strong>Segurança pronta</strong></td><td>Callbacks com limite de frequência, validação de dados do cliente e alertas de exploit no Discord.</td></tr><tr><td><strong>Estado compartilhado</strong></td><td>Posição do ped, veículo e jogadores online são calculados uma vez e lidos por todos os scripts.</td></tr><tr><td><strong>Banco versionado</strong></td><td>Cada produto cria e atualiza suas tabelas sozinho, sem você importar SQL.</td></tr></tbody></table>

## Normalização

O mesmo conceito tem nomes diferentes em cada framework. O `one_lib` usa sempre um só:

| Conceito no one\_lib | Creative | ESX | QBCore / Qbox | Standalone |
|---|---|---|---|---|
| `charId` | Passport | identifier | citizenid | `sa:<id>` |
| conta `cash` | item `dollar` | `money` | `cash` | |
| conta `bank` | banco | `bank` | `bank` | |
| conta `dirty` | item `dirtydollar` | `black_money` | | |
| `grade` | `0` = cargo mais baixo, crescendo com a senioridade | | | |

## Desempenho

| Situação | Cliente | Servidor |
|---|---|---|
| Ocioso | 1 loop de 100 ms (cache do jogador), compartilhado por todos os produtos | nenhum loop |
| Consultas de jogador | leitura de tabela local | leitura de tabela local |
