---
description: Em quais bases nossos sistemas funcionam e com quais sistemas de roupa.
---

# Frameworks suportados

O `one_lib` identifica o framework sozinho na inicialização. Você não precisa configurar nada.

| Framework | Status | Personagem identificado por | Sistema de roupa |
|---|---|---|---|
| **vRP Creative** (Network) | ✅ Estável | Passport | `barbershop` + `skinshop` |
| **ESX Legacy** | 🧪 Beta | identifier (`char1:...`) | illenium-appearance, fivem-appearance ou skinchanger |
| **QBCore** | 🧪 Beta | citizenid | illenium-appearance |
| **Qbox** | 🧪 Beta | citizenid | illenium-appearance |
| **Standalone** | 🧪 Beta | personagem próprio do one\_lib | armazenamento próprio |
| **vRP Creative v5** | 🔜 Em breve | | |
| **vRPex** | 🔜 Em breve | | |

{% hint style="info" %}
**Beta** significa que a integração segue o código oficial do framework, mas ainda está em validação em
servidores reais. Se encontrar qualquer problema, abra um ticket no Discord com o resultado do
[`onedebug`](../one-lib/diagnostico.md) que resolvemos com prioridade.
{% endhint %}

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
