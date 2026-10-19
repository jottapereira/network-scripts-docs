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
| `vrp` com função `Passport` | vRP Creative (a geração é lida do código do `vrp`) |
| `vrp` com `baseModule:idLoaded` | vRP Creative v4/v5 |
| `vrp` sem nenhum dos dois | vRPex / vRP 1 |
| nenhum | Standalone |

## Entrada e saída de personagem

O `one_lib` escuta os eventos de cada framework e dispara sempre os mesmos eventos normalizados
(`one:server:playerLoaded` / `one:server:playerUnloaded`).

| Framework | Personagem entrou | Personagem saiu |
|---|---|---|
| vRP Creative | `ChosenCharacter` ou `CharacterChosen` | `Disconnect` |
| vRP Creative v4/v5 | `vRP:playerSpawn` (disparado por `baseModule:idLoaded`) | `vRP:playerLeave` |
| vRPex | `vRP:playerSpawn` | `vRP:playerLeave` |
| ESX | `esx:playerLoaded` | `esx:playerLogout` · `esx:playerDropped` |
| QBCore / Qbox | `QBCore:Server:PlayerLoaded` | `QBCore:Server:OnPlayerUnload` |
| Standalone | login do personagem (ou entrada no servidor, sem `one_characters`) | saída do servidor |

Reiniciar o `one_lib` com o servidor cheio não perde ninguém: ele reconstrói a lista de quem está online.

## Dinheiro

| Conta | Creative | Creative v4/v5 | vRPex | ESX | QBCore / Qbox |
|---|---|---|---|---|---|
| `cash` | item `dollar` | item `dollars` | `getMoney` | `money` | `cash` |
| `bank` | banco do personagem | coluna `bank` | `getBankMoney` | `bank` | `bank` |
| `dirty` | item `dirtydollar` | item `dollars2` | item `dinheirosujo` | `black_money` | não existe |

## Grupos

| Framework | Origem | Grade |
|---|---|---|
| vRP Creative | `Groups.lua` | convertida: `#Hierarchy - nível` (o nível 1 do Creative é o mais alto) |
| vRP Creative v4/v5 | `hasPermission` (sem hierarquia) | sempre `0` |
| vRPex | `hasGroup` / `hasPermission` | sempre `0` |
| ESX | `job` | `job.grade` |
| QBCore | `job` + `gang` | `grade.level` |
| Qbox | `jobs` + `gangs` (múltiplos) | `grade` |
| Standalone | ACE: `add_ace group.police one.group.police allow` | |

## Interação (One.Interact)

Marcas por proximidade são sempre do one\_lib. A mira (ALT) depende do que a base já tem:

| Base | Mira (ALT) | Regras de bloqueio |
|---|---|---|
| vRP Creative | one\_lib (substitui `target` e `hoverfy` da base) | `Handcuff`, `Carry`, `Cancel`, `Buttons`, `Commands`, `Camera`, `Freecam`, `Active` |
| ESX | `ox_target` se houver; senão one\_lib | morto, algemado (`esx_policejob`) |
| QBCore | `qb-target` / `ox_target` se houver; senão one\_lib | `isdead`, `inlaststand`, `ishandcuffed` |
| Qbox | `ox_target` se houver; senão one\_lib | `isdead`, `inlaststand`, `ishandcuffed` |
| demais | one\_lib | morto |

Com ox\_target ou qb-target, as opções de mira dos produtos (porta-malas, por exemplo) são registradas **dentro**
deles, para não existirem dois sistemas na mesma tecla. Forçar: `setr one:interact_aim "one" | "external"`.

## Limitações conhecidas

* **vRP Creative**: sem o one\_inventory, cobrar em espécie usa o `TakeItem` do Creative, que remove de **um** slot. Dinheiro dividido em duas pilhas pode não ser cobrado mesmo com saldo total suficiente.
* **vRPex**: não tem grade de cargo; pedir `minGrade` maior que `0` sempre retorna falso.
* **QBCore / Qbox**: não há conta de dinheiro sujo (o QBCore usa o item `markedbills`).
