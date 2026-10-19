---
description: vRP Creative (Network, Origens, Bewitched e derivadas). Cerca de 10 minutos.
---

# Instalação: vRP Creative

Vale para as bases Creative da "família Passport": Creative Network, Origens, Bewitched, Bahamas, Reescrita e
derivadas. Para Creative v4/v5 (`vrp_creative`, `vrp_inventory`), use o [guia do Creative v4/v5](creative-v5.md).

{% hint style="info" %}
No Creative o one\_inventory **reaproveita a sua base**: itens, imagens, lojas, receitas, baús de facção e todo o
gameplay do inventário antigo (roubos, drogas, desmanche, lavagem, usos de itens) continuam iguais, inclusive as
suas modificações. Nada do Creative é enviado por nós: o código vem da **sua** pasta.
{% endhint %}

{% stepper %}
{% step %}
### Coloque os recursos

Extraia `one_lib` e `one_inventory` em `resources` (por exemplo em `resources/[one]`). No `server.cfg`, depois do
`vrp` e antes dos scripts da base:

```cfg
ensure oxmysql
start vrp

ensure one_lib
ensure one_inventory

start [scripts]
```
{% endstep %}

{% step %}
### Ligue a ponte no vRP

Abra `resources/vrp/fxmanifest.lua` e adicione **uma linha no fim** de `server_scripts`:

```lua
server_scripts {
    -- ... o que já estava aqui ...
    '@one_inventory/bridge/vrp.lua'
}
```

Assim `vRP.GiveItem`, `TakeItem`, `ItemAmount`, `InventoryWeight` e as demais funções de item de **todos** os
scripts passam a usar o inventário novo. Para desfazer, apague a linha.
{% endstep %}

{% step %}
### Importe o gameplay da sua base

Com o servidor ligado (e o inventário antigo ainda na pasta), rode no **console do servidor**:

```
oneinv_import
```

Isso copia os arquivos de gameplay do seu `inventory` para dentro do one\_inventory. Detalhes em
[Extensão Creative](../extensao-creative.md).
{% endstep %}

{% step %}
### Desligue os recursos antigos

Tire do `server.cfg` (ou mova para uma pasta que não inicia, como `[disabled]`), **sem apagar as pastas**:

| Recurso | Substituído por |
|---|---|
| `inventory` | inventário, chão, armas, usos de itens |
| `chest` | baús de facção, pessoais, bandejas, lixeiras |
| `shops` | lojas (importadas com os mesmos pontos e preços) |
| `trunkchest` | porta-malas e porta-luvas |
| `inspect` | revista |
| `crafting` | bancadas (receitas importadas) |
{% endstep %}

{% step %}
### Interação: target e hoverfy

O one\_lib substitui o `target` (ALT) e o `hoverfy` ("Pressione E") da base. Rode também:

```
onelib_import_target
```

e tire `target` e `hoverfy` do `server.cfg`. Detalhes em [Interact](../../../one-lib/modulos/interact.md).
Enquanto o `target` antigo estiver ligado, ele continua funcionando; a troca é opcional, mas é ela que traz as
marcas de interação e o porta-malas mirando no carro.
{% endstep %}

{% step %}
### Reinicie

Rode `refresh` e reinicie o **servidor inteiro** (arquivos novos foram copiados para os recursos).
{% endstep %}
{% endstepper %}

## Como saber que deu certo

No console, ao iniciar:

```
[one_inventory] 1234 itens registrados (creative)
[one_inventory] extensão carregada: creative
[one_inventory] ponte vRP ativa
```

Em jogo: TAB abre o inventário com os seus itens; perto de uma loja aparece a marca; mirando com ALT num carro
aparece "Abrir porta-malas".

## Dados antigos

Não há comando: cada inventário é trazido **sozinho** na primeira vez que é usado (bolsos na primeira entrada do
personagem; baús, casas, armazéns e porta-malas na primeira abertura). O conteúdo sai do armazenamento antigo ao
entrar no novo, então não há como duplicar.

## Imagens

Usadas direto de `vrp/config/inventory/<item>.png`, como no inventário antigo. Nada a copiar.

## Scripts que abrem baús próprios

Scripts que abriam baús pela interface antiga (`TriggerEvent("inventory:Open", { Type = "Chest" ... })`) precisam
chamar o one\_inventory. Os da base (`propertys`, `warehouse`) já são atendidos. Para outros, veja
[Integração com outros scripts](../integracoes.md) (`OpenLegacyChest`).
