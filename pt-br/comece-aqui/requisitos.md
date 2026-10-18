---
description: O que seu servidor precisa ter antes de instalar.
---

# Requisitos

| Requisito | Versão | Observação |
|---|---|---|
| Artifacts do FiveM (FXServer) | recentes | Lua 5.4 e OneSync |
| OneSync | ligado | `set onesync on` no `server.cfg` |
| [oxmysql](https://github.com/overextended/oxmysql) | 2.x | já incluso no ESX, QBCore, Qbox e na maioria das bases Creative |
| Banco de dados | MariaDB ou MySQL | o mesmo que sua base já usa |
| **one\_lib** | mais recente | grátis, entregue junto com qualquer produto |

{% hint style="info" %}
Nenhum produto exige `ox_lib`, `ox_target` ou qualquer outra biblioteca de terceiros. Se você já usa `ox_lib`,
as notificações dos nossos scripts aparecem nele automaticamente.
{% endhint %}

## Requisitos por framework

{% tabs %}
{% tab title="vRP Creative" %}
* Creative Network (versão atual) com `oxmysql`.
* Para a aparência funcionar com as lojas legadas: `barbershop` e `skinshop` presentes.
{% endtab %}

{% tab title="ESX" %}
* ESX Legacy com `Config.Multichar` ativo (a pasta `esx_multicharacter` precisa existir no servidor).
* Sistema de roupa: `illenium-appearance`, `fivem-appearance` ou `skinchanger`.
{% endtab %}

{% tab title="QBCore" %}
* QBCore atual.
* Sistema de roupa: `illenium-appearance` (recomendado).
{% endtab %}

{% tab title="Qbox" %}
* `qbx_core` atual com `illenium-appearance`.
{% endtab %}

{% tab title="Standalone" %}
* Apenas `oxmysql`. O `one_lib` cria e gerencia os personagens sozinho.
{% endtab %}
{% endtabs %}
