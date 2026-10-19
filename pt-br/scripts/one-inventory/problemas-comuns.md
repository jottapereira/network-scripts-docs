---
description: Sintoma, causa e solução dos problemas mais frequentes na instalação.
---

# Problemas comuns

{% hint style="info" %}
Antes de abrir ticket, rode `onedebug` no console do servidor e mande o resultado junto: ele mostra framework,
versões e o que foi detectado.
{% endhint %}

## Instalação

<details>

<summary>"one_lib precisa iniciar antes deste recurso"</summary>

O `one_inventory` subiu antes do `one_lib`. No `server.cfg`, `ensure one_lib` vem **antes** de
`ensure one_inventory`. Se você usa `start [pasta]`, coloque o `one_lib` numa pasta iniciada antes.

</details>

<details>

<summary>O inventário abre vazio / "0 itens registrados"</summary>

O importador não achou a lista de itens da sua base:

* **ESX / Qbox:** a pasta `ox_inventory` foi apagada. Coloque-a de volta (só não dê `ensure`).
* **ESX sem ox:** a tabela `items` do banco está vazia ou com outro nome.
* **Creative v4/v5:** a base não tem `vrp/modules/inventory.lua` com `itemlist`. Declare os itens em `items.lua`.
* **Standalone:** cadastre em `items.lua`.

O console mostra `[one_inventory] N itens registrados (<framework>)` ao iniciar.

</details>

<details>

<summary>Scripts dão item e ele não aparece</summary>

O item foi para o inventário antigo, não para o one\_inventory:

* **vRP / Creative / vRPex:** falta a linha `'@one_inventory/bridge/vrp.lua'` no `fxmanifest.lua` do `vrp`
  (console deve mostrar `ponte vRP ativa`).
* **ESX:** o ESX não está no "modo ox". Deixe a pasta `ox_inventory` no servidor ou use
  `Config.OxInventory = true` no `es_extended`.
* **QBCore:** qb-core antigo (anterior a 2023). Atualize o qb-core.
* **Inventário antigo ainda iniciado:** com o original ligado, a camada de compatibilidade fica desligada.

</details>

<details>

<summary>Itens sem imagem</summary>

Copie os PNG da pasta do inventário antigo para `one_inventory/web/images/` (caminho certo no guia da sua base),
rode `refresh` e reinicie. `oneinv_images` no console lista quais itens ainda estão sem imagem.

</details>

<details>

<summary>Usar um item não faz nada</summary>

* **Creative / Creative v4/v5:** o gameplay da base não foi importado. Rode `oneinv_import` e reinicie.
* **ESX / QBCore / Qbox:** o script que registra o item (`RegisterUsableItem`, `CreateUseableItem`) não iniciou.
* **vRPex:** o item não tem escolha de uso no vRP (só dar/jogar fora).
* **Item seu:** registre com `exports.one_inventory:RegisterUsable` ou `consume` em `items.lua`.

</details>

## Em jogo

<details>

<summary>TAB não abre</summary>

O jogador está algemado, morto, mirando ou com outra tela aberta, ou trocou a tecla em **Configurações > Atalhos >
FiveM**. No Creative, estados `Handcuff`, `Buttons` e `Commands` também bloqueiam (como no inventário antigo).

</details>

<details>

<summary>Não aparece a marca da loja/bancada</summary>

* O jogador não tem acesso (grupo ou serviço): quem não pode usar não vê o ponto.
* Há uma parede ou porta entre a câmera e o ponto (a marca respeita a linha de visão).
* A loja não tem `locations` (só abre por script).

</details>

<details>

<summary>ALT não mostra o porta-malas</summary>

* **Com ox\_target ou qb-target:** a opção aparece dentro do target da base.
* **Creative com o `target` antigo ligado:** a mira é dele; o porta-malas abre com TAB atrás do carro até você
  trocar pelo one\_lib (ver [Instalação Creative](instalacao/creative.md)).
* O veículo está trancado ou a classe não tem porta-malas (`Config.Vehicles.Classes`).

</details>

<details>

<summary>Peso errado / personagem lento</summary>

O peso máximo vem de `Config.Player.Weight` (ou do hook `GetPlayerWeight`). Lento ao andar é o "peso que pesa":
ajuste ou desligue em `Config.Burden`.

</details>
