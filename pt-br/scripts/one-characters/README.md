---
description: Documentação técnica do one_characters.
---

# one\_characters

Seleção, criação e spawn de personagem. Para a apresentação do produto, veja a
[vitrine](../../vitrine/one-characters.md).

{% embed url="https://www.youtube.com/watch?v=J-Bzgvd9RtM" %}
Showcase do one\_characters.
{% endembed %}

## Fluxo

```
Jogador conecta
  └─ entra num "bucket" privado (ninguém vê ninguém na seleção)
       ├─ tem personagens ──► Seleção ──► escolhe onde acordar ──► segura para entrar
       └─ não tem          ──► Criação (6 etapas) ──► segura para criar
                                                          │
                     transição "Switch" do GTA ◄──────────┘
                                │
                     personagem na cidade · recurso parado (0.00 ms)
```

## Arquivos

| Arquivo | Editável | Para quê |
|---|---|---|
| `config.lua` | ✅ | todas as opções ([Configuração](configuracao.md)) |
| `shared/data.lua` | ✅ | pais do criador, cores de olho, direção dos sliders de rosto |
| `locales/pt-BR.lua` · `locales/en.lua` | ✅ | todos os textos, inclusive os da interface |
| `server/open.lua` | ✅ | slots, spawns extras, itens iniciais ([Personalização](personalizacao.md)) |
| `client/open.lua` | ✅ | o que acontece ao aparecer na cidade |
| `sql/*.sql` | ✅ | tabela `one_characters` (criada e atualizada automaticamente) |
| demais arquivos | protegido | |

## Banco de dados

O produto guarda numa tabela própria só o que os frameworks não guardam de forma padronizada. Os dados do
personagem continuam nas tabelas do seu framework.

| Coluna | Conteúdo |
|---|---|
| `charId` | identificador do personagem no framework |
| `dob` | data de nascimento |
| `nationality` | nacionalidade |
| `bio` | história |
| `playtime` | segundos jogados |
| `last_login` | último acesso (unix) |
| `pending` | vRPex: criação começada e não concluída (volta ao criador no próximo acesso) |
