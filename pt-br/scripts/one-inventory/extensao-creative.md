---
description: Mantém roubos, drogas, desmanche e os usos de itens da sua cidade Creative.
---

# Extensão Creative

O inventário do Creative faz muito mais que guardar itens: roubos, drogas, desmanche, lavagem de dinheiro,
mergulho, reboque, caça, roubo de NPC e o uso de centenas de itens. A extensão Creative mantém **tudo isso
funcionando**, usando o código **da sua própria base**, com as alterações que a sua cidade já fez.

## Como funciona

1. `oneinv_import` copia os arquivos de gameplay do recurso `inventory` antigo para
   `one_inventory/extensions/creative/legacy/`.
2. Esses arquivos rodam isolados dentro do one\_inventory. Os usos de item (`itens.lua`) passam a responder pelo
   novo inventário; armas, chão e interface ficam com o one\_inventory.
3. Os scripts que chamavam o inventário antigo continuam funcionando: `exports["inventory"]:Drops`, `Buffs`,
   `Blueprint`, `CleanWeapons` e eventos como `inventory:Close`.
4. A revista (`inspect:Player`, usada pela polícia e pelo menu) abre o inventário novo, com as mesmas regras:
   polícia em serviço, pessoa nocauteada ou pedido aceito.

## Lojas e bancadas da base

As lojas do recurso `shops` e as receitas do `crafting` da sua base são importadas automaticamente, com os mesmos
pontos, permissões e moedas (dinheiro ou dinheiro sujo). Os pontos de lojas, bancadas e baús de facção aparecem
pela [interação do one_lib](../../one-lib/modulos/interact.md), e cada jogador só vê os do serviço em que está.
As máquinas de café e donuts e as bancadas que os jogadores colocam no chão continuam abrindo, agora no inventário novo. O Creative
fabrica na hora; aqui cada fabricação leva alguns segundos (ajuste em `extensions/creative/legacy.lua`), e itens com
planta (`Blueprint`) exigem a planta aprendida, como antes. Depois de instalar, `shops` e `crafting` não devem
mais iniciar (tire do `server.cfg`), mas **mantenha as pastas**: as listas são lidas delas.

## Importar

```
oneinv_import
```

Rode no console do servidor (não no F8). Depois **remova `inventory` do `server.cfg`** e reinicie.
Se você alterou o inventário antigo depois, importe de novo.

## Arquivos a mais ou a menos

A lista fica em `extensions/creative/legacy.lua` (código aberto). Ficam de fora a interface, as armas, o chão e a
ferramenta de foto de itens, que o one\_inventory substitui.

## Baús de outros scripts (casas, armazéns)

Scripts que abriam **baús próprios** na interface antiga (`TriggerEvent("inventory:Open", { Type = "Chest", ... })`)
passam a abrir pelo servidor, depois de validar o acesso do jeito deles:

```lua
-- no SERVIDOR do script, depois das validações (dono, chave, senha...)
exports.one_inventory:OpenLegacyChest(source, 'Vault:' .. Name, {
    label = 'Baú',
    weight = 50,                    -- kg
    fridge = false,                 -- true: só itens de geladeira · false: nenhum · nil: sem regra
    upgrade = function(amount)      -- guardar "diagram" aumenta a capacidade (10 kg cada)
        vRP.Query('propertys/Vault', { Name = Name, Weight = 10 * amount })
    end
})
```

O cliente nunca escolhe qual baú abre; enquanto aberto, o jogador precisa ficar perto e na mesma instância.
No Creative, os scripts que costumam precisar dessa troca são `propertys` (cofre e geladeira) e `warehouse`:
no servidor, uma função nova que valida e chama `OpenLegacyChest`; no cliente, o `TriggerEvent("inventory:Open", ...)`
vira a chamada dessa função. Um aviso aparece no F8 quando algum script ainda tenta usar a interface antiga.
