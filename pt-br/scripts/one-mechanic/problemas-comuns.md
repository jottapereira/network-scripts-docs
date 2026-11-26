---
description: Soluções para os problemas mais comuns da Forja.
---

# Problemas comuns

## O terminal não abre
Confira se o jogador está dentro do raio de um ponto de trabalho da oficina (elevador, box, cabine...), se tem cargo na oficina e se há um carro perto
(até `Config.Shops.reach` metros). Sem carro perto o aviso é "Nenhum carro perto do ponto".

## O carro não desgasta
Só carros que têm dono na base desgastam (`Config.Wear.trackUnowned = true` inclui os demais). Confirme com `forja_status` que a tabela de carros foi
encontrada e que o módulo `wear` está ligado.

## Aviso de conflito com scripts da base
Lojas de tuning, scripts de dano e oficina da base disputam o mesmo domínio. Desligue o que o console indicar, ou use `Config.Vehicle.takeover = 'coexist'`.

## Os itens não existem no inventário
Em `one_inventory` são cadastrados sozinhos. Em `ox_inventory` e `qb-inventory`, rode `forja_items` no console e cadastre os nomes.

## As luzes do painel não aparecem
Elas usam o `one_hud`. Sem ele, ou com `Config.Diagnosis.lights = 'off'`, não aparecem.

## A pintura recusa
Pintura só em ponto de cabine (ou box). Se a nota ficou baixa, a perícia do mecânico limita o teto (`Config.Skills`).

## Altura e cambagem não mudam
Natives de stance variam por build do jogo. Se alguma não existir na sua build, as rodas e as demais modificações continuam funcionando.

## `forja_selftest` falha
Rode no console do servidor e leia a linha marcada `FALHOU`. Se vier de conteúdo próprio, o painel da cidade (`/forja`) lista os problemas do conteúdo.
