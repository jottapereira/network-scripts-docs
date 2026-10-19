---
description: Em quais bases nossos sistemas funcionam e com quais sistemas de roupa.
---

# Frameworks suportados

O `one_lib` identifica o framework sozinho na inicialização. Você não precisa configurar nada.

| Framework | Status | Personagem identificado por | Sistema de roupa |
|---|---|---|---|
| **vRP Creative** (Network) | ✅ Estável | Passport | `barbershop` + `skinshop` |
| **vRP Creative** (Origens, Bewitched e derivadas) | 🧪 Beta | Passport | `barbershop` + `skinshop` |
| **vRP Creative v4/v5** | 🧪 Beta | user\_id (`vrp_users`) | armazenamento próprio |
| **vRPex / vRP 1** | 🧪 Beta | user\_id (um personagem por conta) | armazenamento próprio |
| **ESX Legacy** | 🧪 Beta | identifier (`char1:...`) | illenium-appearance, fivem-appearance ou skinchanger |
| **QBCore** | 🧪 Beta | citizenid | illenium-appearance |
| **Qbox** | 🧪 Beta | citizenid | illenium-appearance |
| **Standalone** | 🧪 Beta | personagem próprio do one\_lib | armazenamento próprio |

{% hint style="info" %}
**Bases Creative:** o `one_lib` lê o código do seu `vrp` e descobre sozinho qual geração ele é, mesmo em bases
modificadas que mantêm a estrutura original.
{% endhint %}

{% hint style="info" %}
**Beta** significa que a integração segue o código oficial do framework, mas ainda está em validação em
servidores reais. Se encontrar qualquer problema, abra um ticket no Discord com o resultado do
[`onedebug`](../one-lib/diagnostico.md) que resolvemos com prioridade.
{% endhint %}

## Produtos por base

| | Creative | Creative v4/v5 | vRPex | ESX | QBCore | Qbox | Standalone |
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| [one\_characters](../scripts/one-characters/README.md) | ✅ | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 |
| [one\_inventory](../scripts/one-inventory/README.md) | ✅ | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 |
| [Interação 3D](../one-lib/modulos/interact.md) | ✅ substitui `target`/`hoverfy` | ✅ | ✅ | ✅ convive com `ox_target` | ✅ convive com `qb-target` | ✅ convive com `ox_target` | ✅ |

Cada produto tem um guia de instalação **por base**, com o que desligar, o que migrar e como conferir.

## Sistemas de roupa

Quando um produto cria ou altera a aparência de um personagem, ela é salva **no sistema de roupa que seu
servidor já usa**. Assim lojas de roupa, barbearias e outfits continuam enxergando tudo.

| Sistema | Onde fica salvo |
|---|---|
| Creative (`barbershop` + `skinshop`) | `playerdata` e `characters.Skin` |
| illenium-appearance / fivem-appearance | QBCore e Qbox: `playerskins` · ESX: `users.skin` |
| skinchanger | `users.skin` |
| Nenhum dos anteriores | tabela própria `one_appearance` |

{% hint style="warning" %}
`qb-clothing` ainda não é suportado: a aparência é guardada no armazenamento próprio do `one_lib`.
Recomendamos `illenium-appearance`, que é o padrão atual do QBCore e do Qbox.
{% endhint %}
