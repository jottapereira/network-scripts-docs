---
description: ESX Legacy (esx_notify, esx_progressbar, esx_textui). Cerca de 5 minutos.
---

# Instalação: ESX Legacy

O ESX Legacy mostra notificação, progresso e texto de ajuda chamando `exports.esx_notify`, `esx_progressbar` e
`esx_textui`. O one\_hud responde por esses exports, então `ESX.ShowNotification`, `ESX.Progressbar`,
`ESX.TextUI` e todo script que os usa aparecem no visual novo.

{% stepper %}
{% step %}
### Coloque os recursos

```cfg
ensure oxmysql
ensure es_extended

ensure one_lib
ensure one_hud

# depois: esx_*, ox_target...
```
{% endstep %}

{% step %}
### Desligue o que o one\_hud substitui (mantenha as pastas)

Tire do `server.cfg`: `esx_hud` (ou a HUD que usar), `esx_notify`, `esx_progressbar` e `esx_textui`.

{% hint style="warning" %}
**Não apague as pastas** `esx_notify`, `esx_progressbar` e `esx_textui`: o ESX confere se elas existem antes de
chamar. Paradas, quem responde é o one\_hud.
{% endhint %}
{% endstep %}
{% endstepper %}

## Observações

* **Fome, sede e estresse:** `esx_status` (evento `esx_status:onTick`).
* **Dinheiro e emprego:** atualizam na hora (`esx:setAccountMoney`, `esx:setJob`).
* **ox\_lib na base?** Se os seus scripts usam `lib.notify`/`progressBar`, siga também a "linha no ox\_lib" do
  [guia do Qbox](qbox.md).
* **Combustível:** LegacyFuel, ox\_fuel, cdn-fuel, ps-fuel ou lc\_fuel são detectados sozinhos.
