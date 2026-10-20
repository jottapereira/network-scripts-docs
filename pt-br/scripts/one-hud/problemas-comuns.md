---
description: Sintoma, causa e solução.
---

# Problemas comuns

<details>

<summary>Aparecem duas notificações (a antiga e a nova)</summary>

O recurso antigo ainda está iniciado (`notify`, `esx_notify`...) ou falta a linha no core (QBCore: qb-core;
Qbox/ox\_lib: ox\_lib). Veja o guia da sua base.

</details>

<details>

<summary>A HUD não aparece</summary>

* Ela só aparece depois que o personagem carrega (e some no menu de pausa e em cutscenes).
* `/hud` pode ter sido usado para esconder.
* Outro produto com tela aberta (inventário, personagens) esconde a HUD enquanto está aberto.

</details>

<details>

<summary>Fome/sede paradas (Creative)</summary>

O gameplay do HUD da base não foi importado: rode `onehud_import`, tire `hud` do `server.cfg`, `refresh` e
reinicie. O console deve mostrar `gameplay do HUD da base carregado`.

</details>

<details>

<summary>O minimapa não encaixa na moldura</summary>

O radar do jogo é posicionado pela moldura da interface, descontando a "zona segura" do jogador (Configurações >
Tela > Zona segura). Avise o suporte com um print e a resolução do jogador.

</details>

<details>

<summary>Formulário do ESX/QBCore não abre no one\_hud</summary>

`esx_menu_dialog` (ESX.UI.Menu) e `qb-menu` não são substituídos nesta versão. `qb-input` sim: confirme que ele
está fora do `server.cfg`.

</details>

<details>

<summary>Dois cintos (tecla dupla)</summary>

O one\_hud liga o próprio cinto só quando não encontra outro. Se a sua base usa um recurso de cinto diferente,
force `Config.Seatbelt = 'statebag'` (ou `'none'`).

</details>
