---
description: Histórico de versões do one_inventory.
---

# Changelog

## 1.0.0 (em teste)

* vRPex com inventário em recurso separado (lotus e derivados): itens lidos da base, uso dos itens importado com
  `oneinv_import`, peso pela regra da base, itens antigos migrados na primeira entrada, aviso de item da base.
* vRPex: o import descobre sozinho quem tira o item ao usar (o próprio item ou o inventário antes de usar) e
  devolve o item quando o uso falha; inventário com slots (forks) reconhecido; imagens do inventário antigo
  encontradas automaticamente (mesmo quando ficam num site).
* vRPex: arquivos extras do cliente podem ser passados no comando (`oneinv_import client/pasta/arquivo.lua`).
* Inventário completo: bolsos, equipamento, mochila, containers com peso do conteúdo, chão, porta-malas com
  tampa e animação, porta-luvas, baús, revista, hotbar, armas, munição e acessórios de arma.
* Lojas (compra/venda, estoque gravado, moeda em dinheiro ou item) e bancadas (fila que corre offline).
* Peso que pesa, rastro de digitais, acessórios de roupa como itens.
* Interação 3D pelo one\_lib: marca ao chegar perto de lojas, bancadas e baús; porta-malas mirando no carro.
* Bases: vRP Creative (com importação do gameplay da base), Creative v4/v5, vRPex, ESX, QBCore, Qbox e Standalone.
* Compatibilidade com scripts de `ox_inventory` e `qb-inventory`; migradores `oneinv_migrate ox|qb`.
* Dois layouts (`Config.Layout`): `open` (padrão, compacto e com o jogo visível) e `classic`.
* Mochila nas costas: no Creative, a mochila equipada aparece no personagem como no inventário antigo (pelo
  `skinshop` da base, então lojas de roupa não a tiram). Em outras bases, via `Config.EquipmentVisuals`.
* Item recebido com os bolsos cheios vai para a mochila equipada antes de cair no chão; scripts que conferem
  espaço (`CheckWeight`, `CanCarry`) contam a mochila.
* Reiniciar o one\_inventory com jogadores online: sem erro do oxmysql no console e sem perder plantas
  aprendidas, munições e acessórios do gameplay do Creative.
* Sem o aviso `could not find file web/images/*.png` no start (a pasta vem com um README explicando o uso).
