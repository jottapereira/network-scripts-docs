---
description: Como os sistemas da Network Scripts se encaixam na sua base.
---

# Como funciona

Todo produto da Network Scripts é formado por duas peças:

| Peça | O que é | Preço |
|---|---|---|
| **one\_lib** | Biblioteca base. Detecta seu framework e oferece aos scripts uma forma única de falar com ele. | Grátis |
| **one\_\<produto\>** | O sistema em si (ex.: `one_characters`). | Pago |

```
Seu servidor
├── framework (Creative, ESX, QBCore, Qbox... ou nenhum)
├── one_lib            ← instalada uma vez, serve a todos os produtos
├── one_characters     ← produto
└── one_<próximo>      ← produto
```

## Por que uma biblioteca separada

Cada framework faz as coisas do seu jeito: o Creative chama o personagem de *Passport*, o ESX de
*identifier*, o QBCore de *citizenid*. O `one_lib` traduz tudo isso para uma linguagem única.

Para você, isso significa:

* **Um único download por produto**, que funciona em qualquer base suportada.
* **Atualizações de compatibilidade num lugar só.** Se um framework muda, atualizamos o `one_lib` e todos os seus produtos voltam a funcionar.
* **Desempenho.** Coisas que todo script precisa (posição do jogador, veículo atual, quem está online) são calculadas uma vez e compartilhadas.

## O que você pode editar

Os produtos são entregues com o código principal protegido (escrow do FiveM), mas tudo que muda de
servidor para servidor fica aberto:

| Arquivo | Para quê |
|---|---|
| `config.lua` | todas as opções do produto |
| `locales/*.lua` | todos os textos, inclusive os da interface |
| `server/open.lua` · `client/open.lua` | pontos de integração com outros scripts do seu servidor |
| `sql/*` | estrutura do banco (criada automaticamente) |
