---
description: Documentação técnica do one_inventory.
---

# one\_inventory

Inventário, baús, lojas, bancadas, porta-malas, chão e armas em um só sistema. Para a apresentação do produto, veja a
[vitrine](../../vitrine/one-inventory.md).

{% embed url="https://www.youtube.com/watch?v=JvsmuEtCk-I" %}
Showcase do one\_inventory.
{% endembed %}

## Como funciona

```
Jogador abre (TAB) · mira no carro (ALT) · chega perto de uma loja, bancada ou baú
  └─ cliente pede ao servidor ──► servidor valida (distância, grupo, peso, espaço)
                                      └─ aplica a movimentação de uma vez
                                           └─ envia só as diferenças para a interface
                                                └─ se o servidor recusar, a interface desfaz

Outros scripts (ox_inventory, qb-inventory, vRP, ESX...)
  └─ camada de compatibilidade responde com as mesmas funções, e o one_inventory é a fonte da verdade
```

## Arquivos

| Arquivo | Editável | Para quê |
|---|---|---|
| `config.lua` | ✅ | todas as opções ([Configuração](configuracao.md)) |
| `items.lua` | ✅ | cria ou sobrescreve itens |
| `server/open.lua` · `client/open.lua` | ✅ | regras do seu servidor (não são alterados nas atualizações) |
| `locales/pt-BR.lua` · `locales/en.lua` | ✅ | todos os textos, inclusive os da interface |
| `web/images` | ✅ | imagens dos itens |
| `sql/*.sql` | ✅ | tabelas criadas e atualizadas automaticamente |
| demais arquivos | protegido | |

## Banco de dados

| Tabela | Conteúdo |
|---|---|
| `one_inventory` | inventários (bolsos, baús, porta-malas, porta-luvas) |
| `one_inventory_shops` | estoque das lojas |
| `one_inventory_crafting` | filas de fabricação das bancadas |

## Páginas

* [Instalação](instalacao/README.md): um guia por base
* [Configuração](configuracao.md)
* [Integração com outros scripts](integracoes.md)
* [Compatibilidade e migração](compatibilidade.md)
* [Extensão Creative](extensao-creative.md)
* [Problemas comuns](problemas-comuns.md)
* [Changelog](changelog.md)
