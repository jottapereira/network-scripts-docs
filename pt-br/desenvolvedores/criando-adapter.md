---
description: Como o one_lib conversa com cada framework, para quem usa uma base modificada.
---

# Criando um adapter

Se sua base é uma variação de um framework suportado (funções renomeadas, tabelas diferentes), o caminho
é um **adapter**: um arquivo que ensina o `one_lib` a falar com ela.

{% hint style="info" %}
Tem uma base diferente? Fale com a gente no [Discord](https://discord.gg/sj3T9naGG2). Adapters de bases
populares entram no `one_lib` oficial para todos os clientes.
{% endhint %}

## Onde fica

```
one_lib/bridge/framework/<nome>/server.lua   ← dinheiro, grupos, personagens
one_lib/bridge/framework/<nome>/client.lua   ← eventos de spawn
one_lib/bridge/appearance/<nome>/server.lua  ← sistema de roupa
```

Force o uso com `setr one:framework "<nome>"` ou `setr one:appearance "<nome>"`.

## Contrato do framework

O arquivo retorna uma tabela com estas partes. O que não existir é tratado como "não suportado".

```lua
local Adapter = { Lifecycle = {}, Player = {}, Money = {}, Groups = {}, Characters = {} }

-- Quem já está online:  { [source] = charId }
function Adapter.Lifecycle.Bootstrap() end
-- Avise o one_lib quando um personagem entrar ou sair
function Adapter.Lifecycle.Listen(onLoaded, onUnloaded) end

function Adapter.Player.GetName(src) end

function Adapter.Money.Get(src, account) end                     -- 'cash' | 'bank' | 'dirty'
function Adapter.Money.Add(src, account, amount, reason) end     -- boolean
function Adapter.Money.Remove(src, account, amount, reason) end  -- boolean, só com saldo

function Adapter.Groups.Has(src, name, minGrade) end
function Adapter.Groups.Get(src) end

function Adapter.Characters.List(src) end
function Adapter.Characters.Owns(src, charId) end
function Adapter.Characters.Create(src, data) end   -- cria E entra; retorna charId
function Adapter.Characters.Login(src, charId) end
function Adapter.Characters.Delete(src, charId) end

return Adapter
```

## Contrato do sistema de roupa

```lua
local Appearance = ...   -- o módulo One.Appearance (formato e utilitários)

local Adapter = { Capabilities = { skinMix = true } }

function Adapter.GetMany(charIds) end   -- { [charId] = aparência normalizada }
function Adapter.Get(charId) end
function Adapter.Save(charId, data) end -- converte do formato normalizado e grava

return Adapter
```

O formato normalizado está em [Appearance](../one-lib/modulos/appearance.md).
