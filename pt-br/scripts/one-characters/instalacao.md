---
description: Instalação do one_characters em cada framework.
---

# Instalação

{% stepper %}
{% step %}
### Instale o one\_lib

O `one_characters` precisa do `one_lib` **v0.3 ou superior**. Veja [Instalação do one\_lib](../../one-lib/instalacao.md).
{% endstep %}

{% step %}
### Coloque o recurso

Extraia `one_characters` dentro de `resources`.
{% endstep %}

{% step %}
### Desative a seleção de personagem atual

Siga a aba do seu framework abaixo.
{% endstep %}

{% step %}
### Adicione ao server.cfg

```cfg
ensure one_lib
ensure one_characters
```

As tabelas são criadas sozinhas no primeiro start.
{% endstep %}

{% step %}
### Ajuste a configuração

Abra `config.lua` e defina pelo menos a marca (`Config.Branding`) e os pontos de spawn
(`Config.Spawns`). Veja [Configuração](configuracao.md).
{% endstep %}
{% endstepper %}

## Por framework

{% tabs %}
{% tab title="vRP Creative" %}
* Remova o recurso **`spawn`** (pasta `[scripts]/spawn`), ou ele abrirá junto.
* Mantenha `barbershop` e `skinshop`: a aparência criada é salva no formato deles.
* Os slots seguem a coluna `accounts.Characters` + 2 para quem é Premium. Para outra regra, use `Hooks.GetSlots`.
{% endtab %}

{% tab title="ESX" %}
* **Remova o `ensure esx_multicharacter`, mas mantenha a pasta no servidor.**
  O ESX só liga o modo multipersonagem (`Config.Multichar`) quando a pasta existe.
* Se usa `esx_identity` apenas para o registro, remova o `ensure` dele: o registro agora é feito pelo criador.
* Slots: lidos da tabela `multicharacter_slots`, quando existir.
* Personagens usam o formato padrão `char1:<license>`. Para outro prefixo: `set one:esx:prefix "char"`.
{% endtab %}

{% tab title="QBCore" %}
* Remova **`qb-multicharacter`** e **`qb-spawn`** (a escolha de spawn é feita pelo produto).
* Se usa `qb-apartments` para o spawn inicial, adicione os apartamentos como spawn em [`Hooks.GetSpawns`](personalizacao.md#spawns-extras).
* Os itens iniciais de `QBCore.Shared.StarterItems` são entregues como no `qb-multicharacter`, com identidade e CNH preenchidas.
{% endtab %}

{% tab title="Qbox" %}
* Em `qbx_core/config/client.lua`, ligue `characters.useExternalCharacters = true`.
* Remova `qbx_spawn`, se usar.
* Os itens iniciais de `qbx_core/config/shared.lua` (`starterItems`) são entregues via `ox_inventory`.
{% endtab %}

{% tab title="Standalone" %}
* Nada a desativar. Com o `one_characters` instalado, o `one_lib` passa a ter multipersonagem próprio
  (tabela `one_standalone_characters`), com última localização salva ao desconectar.
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Teste rápido: conecte, crie um personagem, entre na cidade e rode `onedebug` no F8. O `charId` deve aparecer.
{% endhint %}
