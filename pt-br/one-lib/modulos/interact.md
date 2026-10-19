---
description: Interação no mundo — marca ao chegar perto, mira com ALT, um cartão de opções para todos os scripts.
---

# Interact

Um único sistema para tudo que o jogador "usa" no mundo: baús, lojas, bancadas, NPCs, caixas eletrônicos,
veículos, jogadores e objetos. A tela é desenhada pelo one\_lib, então dois scripts nunca disputam tecla ou espaço.

**Dois jeitos de interagir, uma aparência só**

* **Chegar perto**: pontos fixos mostram uma marca a até 14 m, o nome e a distância a até 7 m e, no alcance, o
  cartão com as opções. `E` confirma; a rodinha do mouse troca a opção.
* **Mirar (segurar ALT)**: veículos, jogadores, modelos e pontos marcados como "só mira". O alvo ganha contorno
  e o cartão abre preso a ele. Rodinha troca, `E` ou clique esquerdo confirmam, clique direito solta o cursor
  para clicar direto na opção.

As teclas ficam em **Configurações > Atalhos > FiveM** e o jogador pode trocá-las.

## Pontos

```lua
local id = One.Interact.AddPoint({
    coords = vec3(452.0, -980.0, 30.7),
    label = 'Armário', icon = 'storage', range = 1.5,
    options = {
        { label = 'Abrir', onSelect = function(ctx) abrirArmario() end },
        { key = 'G', label = 'Arrombar', hold = 3000,
          canInteract = function(ctx)
              if not temPeDeCabra() then return false, 'Sem pé de cabra' end
              return true
          end,
          onSelect = function(ctx) arrombar() end }
    }
})

One.Interact.Remove(id)
```

| Campo | Descrição |
|---|---|
| `coords` | posição (ou `entity` + `offset` para prender numa entidade) |
| `label`, `icon` | nome no cartão e ícone (`storage`, `shop`, `craft`, `car`, `person`, `pin`...) |
| `range` | alcance para o cartão abrir (padrão 1,5 m) |
| `radius` | o mesmo que `range`, para zonas esféricas |
| `proximity = false` | sem marca passiva: só aparece mirando com ALT |
| `vehicle = true` | também funciona de dentro do veículo (drive-thru, por exemplo) |
| `canInteract(ctx)` | regra do alvo inteiro (`false` esconde tudo) |
| `options` | lista de opções (abaixo) |

`One.Interact.AddBox({ coords, size = vec3(2, 1, 2), heading, ... })` cria uma zona em caixa.

## Entidades, modelos e globais (só com ALT)

```lua
One.Interact.AddEntity(entity, { label = 'Caixa', options = { ... } })
One.Interact.AddEntity({ netId = netId }, { ... })
One.Interact.AddModel({ `prop_atm_01`, `prop_atm_02` }, { label = 'Caixa eletrônico', options = { ... } })
One.Interact.AddGlobalVehicle({ options = { ... } })
One.Interact.AddGlobalPlayer({ options = { ... } })
One.Interact.AddGlobalPed({ options = { ... } })
One.Interact.AddGlobalObject({ options = { ... } })
```

Vários recursos podem registrar opções no mesmo alvo: elas aparecem juntas no mesmo cartão.

## Opções

| Campo | Descrição |
|---|---|
| `label` | texto (já traduzido pelo seu recurso) |
| `key` | atalho próprio: `G`, `H`, `X`, `Z`, `Y`, `K`, `B`, `Q`, `R`. Sem `key`, a opção selecionada usa a tecla de confirmar |
| `hold` | milissegundos segurando para confirmar (anel de progresso) |
| `distance` | alcance só desta opção |
| `canInteract(ctx)` | `true` mostra; `false` esconde; `false, 'motivo'` mostra bloqueada com o motivo |
| `onSelect(ctx)` | executa (roda numa thread do seu recurso, pode usar `Await`) |
| `event` / `serverEvent` / `command` | alternativas a `onSelect` (`args` vai junto) |

`ctx` traz `entity`, `netId`, `player` (server id de outro jogador), `coords`, `distance`, `type`, `id` e `name`.

`canInteract` é chamado só quando o alvo está em foco, algumas vezes por segundo. Mantenha leve.

## Outras funções

| Função | Descrição |
|---|---|
| `One.Interact.Update(id, patch)` | troca `label`, `icon`, `options`, `range`, `coords`, `canInteract` |
| `One.Interact.Disable(state)` | trava a interação enquanto o seu recurso quiser (algemado, minigame) |
| `One.Interact.IsAiming()` | `true` com ALT segurado |

Os alvos pertencem ao recurso que os criou e somem sozinhos quando ele para.

## Desempenho

Sem nada por perto: uma checagem a cada 500 ms. O loop por frame só existe com uma marca visível ou com ALT
segurado; a tela recebe apenas o que se moveu, e o raio da mira só é lançado enquanto se mira. Com qualquer tela
aberta (inventário, menu de pausa), a interação some.

## Bases com ox\_target ou qb-target

Para não existirem dois sistemas na mesma tecla, quando a base tem `ox_target` ou `qb-target`:

* a mira (ALT) continua sendo do target da base;
* alvos **de mira** criados pelos produtos (`AddGlobalVehicle`, `AddGlobalPlayer`, `AddModel`, `AddEntity` e pontos
  com `proximity = false`) são registrados **dentro** dele, com o mesmo texto, `canInteract` e ação;
* marcas por proximidade (`AddPoint`, `AddBox`) continuam no One.Interact.

Opções bloqueadas com motivo não existem nesses targets: lá elas ficam escondidas. Forçar um lado:
`setr one:interact_aim "one"` (sempre a mira do one\_lib) ou `"external"`.

## vRP Creative: substitui `target` e `hoverfy`

No Creative, o one\_lib assume os dois recursos de interação da base:

* **`exports["target"]`** (`AddBoxZone`, `AddCircleZone`, `AddTargetModel`, `RemCircleZone`, `LabelText`,
  `LabelOptions`) continua funcionando em todos os scripts, com os mesmos eventos e `tunnel`. As zonas aparecem
  mirando com ALT, como antes; as que o jogador precisa encontrar (salário, pátio, empregos, banco, armazém,
  interior das propriedades) mostram a marca ao chegar perto. A lista fica em
  `one_lib/bridge/interact/creative/legacy.lua`.
* **Os pontos do `hoverfy`** ("Pressione E para abrir": lojas de roupa, barbearia, tatuagem, propriedades) viram
  marcas com cartão. A tecla continua sendo lida pelo próprio script.
* **Os menus prontos do target** (veículo: abastecer, placa, chave, desvirar, rebocar, apreender, desmanche...;
  jogador: revistar, reanimar, cobrança, tratamento...) aparecem mirando com ALT, com as mesmas regras.

Instalação no Creative:

1. No console do servidor: `onelib_import_target` (copia o `target` da sua base para dentro do one\_lib; ele roda
   isolado: cadeiras, macas, ligações para serviços e as zonas dele continuam iguais).
2. Tire `target` e `hoverfy` do `server.cfg` (ou mova as pastas para fora de `[scripts]`).
3. `refresh` e reinicie o servidor.

{% hint style="info" %}
Enquanto o recurso `target` antigo estiver ligado, ele continua no comando e a mira com ALT do one\_lib fica
desligada (para não disputarem a tecla). Os pontos por proximidade funcionam normalmente.
{% endhint %}
