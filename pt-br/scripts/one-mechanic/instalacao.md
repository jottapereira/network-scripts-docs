---
description: Como instalar a Forja (one_mechanic) em qualquer base.
---

# Instalação

## Requisitos

* `one_lib` **0.8.0 ou mais novo** (traz a camada de carros `One.Vehicle` e as regras de preço `One.Pricing`)
* `oxmysql`
* Recomendado: `one_hud` (luzes de aviso, confirmações, progresso) e `one_inventory` (itens cadastrados sozinhos)

## Passos

1. Coloque a pasta `one_mechanic` em `resources/[one]/`.
2. No `server.cfg`, depois do `one_lib` e do `oxmysql`: `ensure one_mechanic`.
3. Reinicie. As tabelas (`mec_*`) são criadas sozinhas na primeira subida; o console mostra `Forja 1.0.0 pronta`.
4. Confira com `forja_status` (módulos, base detectada, conflitos) e rode `forja_selftest` no console do servidor: o resultado esperado é **0 falha(s)**.

{% hint style="info" %}
A Forja descobre sozinha a tabela de carros da sua base (vRP, ESX, QBCore, Qbox, Creative) pela estrutura do banco. Se a sua base for muito
diferente, o console diz o que não achou e você ajusta com as convars `one:vehicle:*` (veja a página de compatibilidade do one\_lib).
{% endhint %}

## Scripts da base que disputam o mesmo domínio

Com `Config.Vehicle.takeover = 'exclusive'` (padrão) a Forja assume dano, handling e oficina. O console avisa quais scripts da base
(lojas de tuning, scripts de dano, `lscustoms`, `engine`...) desligar. Use `'coexist'` para conviver ou `'observe'` para só observar.

## Itens

Com `one_inventory` os itens (peças, materiais, kits) são cadastrados sozinhos. Em `ox_inventory` e `qb-inventory`, rode `forja_items` no console:
ele lista os nomes para você cadastrar. Peças têm variantes por origem: `turbo_street`, `turbo_street_used`, `turbo_street_pirate`...

## Primeira oficina

```
/forja_shop create player char <id do jogador> Oficina do Zé
/forja_shop panel <id da oficina>
```

No painel, crie um ponto de **Escritório** e outro de **Elevador** com o laser (E salva, setas giram, roda do mouse muda o raio).
Depois o dono contrata a equipe pelo painel e abre o terminal do carro pelo ponto de elevador.
