---
description: Instalação do one_characters em cada framework.
---

# Instalação

{% stepper %}
{% step %}
### Instale o one\_lib

O `one_characters` precisa do `one_lib` **v0.6.1 ou superior**. Veja [Instalação do one\_lib](../../one-lib/instalacao.md).
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
Vale para Creative Network, Origens, Bewitched e derivadas: a geração é identificada automaticamente.

* Remova o recurso **`spawn`** (pasta `[scripts]/spawn`), ou ele abrirá junto.
* Mantenha `barbershop` e `skinshop`: a aparência criada é salva no formato deles.
* Os slots seguem a coluna `accounts.Characters` + 2 para quem é Premium. Para outra regra, use `Hooks.GetSlots`.
{% endtab %}

{% tab title="Creative v4/v5" %}
* Remova **`vrp_spawn`** e **`vrp_login`** (seleção e criação antigas).
* Os personagens continuam em `vrp_users`. A aparência criada fica no armazenamento do `one_lib`.
* Detecção automática. Se precisar forçar: `setr one:framework "creativev5"`.
{% endtab %}

{% tab title="vRPex" %}
O vRPex tem **um personagem por conta**, então o produto funciona em modo de personagem único:

* **Conta nova**: abre direto o criador. Nome e idade são gravados em `vrp_user_identities`.
* **Conta existente**: abre a tela com o próprio personagem, só para escolher onde acordar.
* Quem fechar o jogo no meio da criação volta para o criador no próximo acesso.
* Excluir personagem não existe neste modo.

**O que remover** (tire o `ensure` do `server.cfg`): todo script que abre ao conectar para criar personagem,
registrar identidade ou escolher spawn. Os nomes mais comuns no vRPex: `vrp_creation`, `vrp_character`,
`vrp_identity` (só a tela de registro), `vrp_spawn`, `nation_creator`, `creator`, `spawnselector`.
Na dúvida: conecte com uma conta nova; se aparecer qualquer tela além da do `one_characters`, o script
dela ainda está ligado.

**O que manter**: o `vrp` e o `spawnmanager`, sem alterações. Lojas de roupa e barbearia continuam funcionando.

**Onde fica cada coisa**

| Dado | Onde | Observação |
|---|---|---|
| Nome e idade | `vrp_user_identities` | o próprio vRP |
| Modelo e roupa | datatable do vRP (`customization`) | o produto grava o resultado do criador direto no vRP. Compras em loja de roupa continuam valendo |
| Rosto (herança, traços, olhos, cabelo, barba, maquiagem) | tabela `one_appearance` | o vRP não guarda rosto; o produto reaplica a cada entrada |
| Data de nascimento, nacionalidade, biografia | tabela `one_characters` | |
| Último local | datatable do vRP (`position`) | o local escolhido na entrada é gravado na hora |

{% hint style="warning" %}
Se o seu servidor tem uma **barbearia que salva o rosto por conta própria**, o rosto do criador é reaplicado ao
entrar e pode sobrescrever o da barbearia. Fale com o suporte para integrar as duas.
{% endhint %}
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
