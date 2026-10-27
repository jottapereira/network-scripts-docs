---
description: Documentação técnica do one_workshop.
---

# one\_workshop

A oficina de armas: bancadas físicas, acessórios, cor e skins, cobrados em dinheiro, itens ou gemas. Para a
apresentação do produto, veja a [vitrine](../../vitrine/one-workshop.md).

## Como funciona

```
Jogador chega na bancada ──► servidor trava a bancada (uma pessoa por vez) e confere acesso
  └─ escolhe acessórios · cor · skins (a arma da mesa mostra tudo ao vivo)
       └─ confirma ──► servidor calcula o preço, cobra (tudo ou nada) e grava
                           └─ a arma volta para a mão com a personalização aplicada

Skins ──► pacotes (recursos separados com skins.json) ──► a oficina junta todos numa galeria só
```

## Arquivos

| Arquivo | Editável | Para quê |
|---|---|---|
| `config.lua` | ✅ | todas as opções ([Configuração](configuracao.md)) |
| `locales/pt-BR.lua` · `locales/en.lua` | ✅ | todos os textos, inclusive os da interface |
| `install/*` · `images/*` | ✅ | cadastro e imagens dos 24 itens para cada inventário |
| `sql/*.sql` | ✅ | tabelas criadas e atualizadas automaticamente |
| demais arquivos | protegido | |

## Banco de dados

| Tabela | Conteúdo |
|---|---|
| `one_workshop_weapons` | personalização por personagem e arma (só nas bases cujo inventário não guarda dados no item) |
| `one_workshop_skins` | skins que cada personagem possui (coleção permanente) |

## Páginas

* [Instalação](instalacao.md)
* [Configuração](configuracao.md)
* [Skins](skins.md)
* [Pacotes de skins](pacotes.md)
* [Cobrança: dinheiro, itens e gemas](cobranca.md)
* [Administração e logs](administracao.md)
* [Problemas comuns](problemas-comuns.md)
* [Changelog](changelog.md)
