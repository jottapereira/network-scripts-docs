---
description: Como o one_lib se integra a cada framework, em detalhe.
---

# Compatibilidade

## Detecção

Na inicialização, nesta ordem:

| Encontrado | Framework |
|---|---|
| `qbx_core` | Qbox |
| `qb-core` | QBCore |
| `es_extended` | ESX |
| `vrp` com função `Passport` | vRP Creative |
| `vrp` sem ela | vRPex |
| nenhum | Standalone |

## Entrada e saída de personagem

O `one_lib` escuta os eventos de cada framework e dispara sempre os mesmos eventos normalizados
(`one:server:playerLoaded` / `one:server:playerUnloaded`).

| Framework | Personagem entrou | Personagem saiu |
|---|---|---|
| vRP Creative | `ChosenCharacter` | `Disconnect` |
| vRPex | `vRP:playerSpawn` (primeiro spawn) | `vRP:playerLeave` |
| ESX | `esx:playerLoaded` | `esx:playerLogout` · `esx:playerDropped` |
| QBCore / Qbox | `QBCore:Server:PlayerLoaded` | `QBCore:Server:OnPlayerUnload` |
| Standalone | login do personagem (ou entrada no servidor, sem `one_characters`) | saída do servidor |

Reiniciar o `one_lib` com o servidor cheio não perde ninguém: ele reconstrói a lista de quem está online.

## Dinheiro

| Conta | Creative | vRPex | ESX | QBCore / Qbox |
|---|---|---|---|---|
| `cash` | item `dollar` | `getMoney` | `money` | `cash` |
| `bank` | banco do personagem | `getBankMoney` | `bank` | `bank` |
| `dirty` | item `dirtydollar` | item `dinheirosujo` | `black_money` | não existe |

## Grupos

| Framework | Origem | Grade |
|---|---|---|
| vRP Creative | `Groups.lua` | convertida: `#Hierarchy - nível` (o nível 1 do Creative é o mais alto) |
| vRPex | `hasGroup` / `hasPermission` | sempre `0` |
| ESX | `job` | `job.grade` |
| QBCore | `job` + `gang` | `grade.level` |
| Qbox | `jobs` + `gangs` (múltiplos) | `grade` |
| Standalone | ACE: `add_ace group.police one.group.police allow` | |

## Limitações conhecidas

* **vRP Creative**: cobrar em espécie usa o `TakeItem` do Creative, que remove de **um** slot. Dinheiro dividido em duas pilhas pode não ser cobrado mesmo com saldo total suficiente.
* **vRPex**: não tem grade de cargo; pedir `minGrade` maior que `0` sempre retorna falso.
* **QBCore / Qbox**: não há conta de dinheiro sujo (o QBCore usa o item `markedbills`).
