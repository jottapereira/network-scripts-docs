---
description: Documentação técnica do one_hud.
---

# one\_hud

HUD, velocímetro, notificações, progresso, formulários e pedidos num só visual. Para a apresentação do produto, veja a
[vitrine](../../vitrine/one-hud.md).

{% embed url="https://www.youtube.com/watch?v=XRstOl4t62M" %}
Showcase do one\_hud.
{% endembed %}

## Como funciona

```
Jogo e framework (vida, fome, voz, dinheiro, combustível...)
  └─ client/sources.lua lê cada dado da fonte certa da sua base (a cada 200 ms)
       └─ só o que mudou vai para a interface
            └─ HUD · velocímetro · notificação · progresso · formulário · pedido Y/N · texto de ajuda

Seus scripts (esx_notify, progressbar, qb-input, ox_lib, vRP...)
  └─ compat/ responde no lugar dos originais e usa as telas do one_hud
```

## Arquivos

| Arquivo | Editável | Para quê |
|---|---|---|
| `config.lua` | ✅ | todas as opções ([Configuração](configuracao.md)) |
| `client/sources.lua` | ✅ | de onde vem cada dado (status, voz, combustível, cinto, dinheiro) em cada base |
| `shared/weapons.lua` | ✅ | nome e modo das armas quando o inventário não informa |
| `compat/client.lua` | ✅ | respostas no lugar de `esx_notify`, `esx_progressbar`, `esx_textui`, `progressbar`, `qb-input` e `Notify` |
| `bridge/*.lua` | ✅ | pontes de uma linha (qb-core, ox\_lib, vrp) |
| `locales/pt-BR.lua` · `locales/en.lua` | ✅ | todos os textos, inclusive os da interface |
| demais arquivos | protegido | |

O one\_hud não usa banco de dados.

## Páginas

* [Instalação](instalacao/README.md): um guia por base
* [Configuração](configuracao.md)
* [Integração com outros scripts](integracoes.md)
* [Compatibilidade](compatibilidade.md)
* [Problemas comuns](problemas-comuns.md)
* [Changelog](changelog.md)
