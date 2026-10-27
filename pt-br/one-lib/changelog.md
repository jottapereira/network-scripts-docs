---
description: Histórico de versões do one_lib.
---

# Changelog

## 0.7.0

* **`One.Gems`**: moeda premium configurável por recurso: gemas da base Creative e Creative v4/v5 sozinhas, item do inventário ou funções próprias ([Gems](modulos/gems.md)).
* **`One.Inventory.GetWeaponMods` / `SetWeaponMods` / `HasWeaponMods`**: acessórios, cor e cor da camuflagem da arma, no formato de cada inventário (one\_inventory, ox\_inventory, qb-inventory). Acessórios de outros scripts são preservados.
* Adapters ganham a seção opcional `Gems` ([contrato](../desenvolvedores/criando-adapter.md)).

## 0.6.2

* `setr one:accent`: a cor de destaque de todos os produtos ([Cor das telas](../comece-aqui/cor-das-telas.md)).
* Nomes das funções do vRP achados automaticamente em bases misturadas (vRPex com funções do Creative e vice-versa).
* Bases que não deixam ler as pastas do `vrp`: os arquivos são achados pelo nome e nada é dado como "faltando" à toa.
* Banco fora do ar não trava mais o start.
* Funciona nos artefatos novos do FiveM (a detecção não depende mais do GlobalState).
* vRPex com vários personagens: personagem novo aparece em `vrp_users` e a troca não reconecta no personagem errado.
* Código importado das bases (itens, HUD) roda isolado sem travar as chamadas entre servidor e cliente.

## 0.6.0

* `One.Progress`, `One.Input`, `One.Confirm`, `One.Request` e `One.TextUI`: telas com o one\_hud, ox\_lib ou
  versão simples ([página](modulos/tela.md)).
* `One.Notify` usa o one\_hud quando instalado.
* Interação: ox\_target e qb-target recebem as opções de mira dos produtos; regras de bloqueio por base.

## 0.5.0

* `One.Interact`: interação no mundo (marca ao chegar perto, mira com ALT, cartão de opções com atalhos,
  opções de segurar e bloqueadas com motivo). Interface própria do one\_lib.

## 0.4.0

* `One.Inventory`: dar e consumir itens em qualquer inventário (one\_inventory, ox, qb ou o nativo do framework).
* `One.Status.Get`: valores atuais de fome, sede e estresse.

## 0.3.0

* Personagens para ESX Legacy, QBCore, Qbox e Standalone (multipersonagem próprio).
* Aparência: suporte a illenium-appearance, fivem-appearance e skinchanger.
* `One.Sound`: sons de interface nativos do GTA.

## 0.2.0

* `One.Appearance` e `One.Characters` (vRP Creative).
* Detecção do sistema de roupa.
* Comando `onedebug`.

## 0.1.0

* Lançamento: detecção de framework, ciclo de vida normalizado e os módulos Player, Money, Groups, Callback,
  Notify, Locale, DB, Log, RateLimit, Cache, Focus e Utils.
