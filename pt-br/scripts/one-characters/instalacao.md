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
Vale para as variantes "Three" (`vrp_users`) e "Summerz / South Network" (`summerz_characters`): o one\_lib
identifica qual é e usa as consultas e funções da própria base.

* Remova a seleção e criação antigas: **`vrp_spawn`** e **`vrp_login`** (Three) ou **`spawn`** (Summerz).
* Os personagens continuam na tabela da sua base; personagem novo é criado pelas mesmas consultas dela (com
  telefone, serial, tipo sanguíneo e conta no banco).
* Detecção automática. Se precisar forçar: `setr one:framework "creativev5"`.
{% endtab %}

{% tab title="vRPex" %}
No vRPex cada personagem é um `user_id`, e é o próprio `vrp` que escolhe qual carregar quando o jogador conecta.

**Sem mexer no vrp: um personagem por conta** (o padrão do vRPex). Conta nova abre o criador; nome, idade e
nascimento vão para as colunas da sua base. Depois disso, a tela é só para escolher onde acordar.

**Vários personagens: um bloco no `vrp`.** O `vrp` pergunta ao one\_lib qual personagem carregar. Cole no
`playerConnecting` do `vrp` (geralmente `vrp/base.lua`), logo **depois** da linha que pega o `user_id`
(`local user_id = vRP.getUserIdByIdentifiers(ids)` e o `if not user_id then ... end` que vem em seguida):

```lua
-- [one_characters] VÁRIOS PERSONAGENS
if GetResourceState("one_lib") == "started" then
	local ok, chosen = pcall(function() return exports.one_lib:VrpexCharacter(ids, user_id) end)
	if ok and chosen == "new" then
		local rows = exports["oxmysql"]:executeSync("INSERT INTO vrp_users(whitelist) SELECT whitelist FROM vrp_users WHERE id = ?", { user_id })
		if rows and rows.insertId then
			vRP.execute("vRP/init_users_infos",{ user_id = rows.insertId })   -- só se a sua base tiver essa consulta
			TriggerEvent("vRP/new_user_created", rows.insertId)
			exports.one_lib:VrpexAdopt(ids, rows.insertId)
			user_id = rows.insertId
		end
	elseif ok and tonumber(chosen) then
		user_id = tonumber(chosen)
	end
end
```

E no **fim** do mesmo arquivo:

```lua
SetConvar("one:vrpex:multichar", "true")
```

{% hint style="info" %}
O nome da variável dos identificadores (`ids`) e da criação de conta podem mudar de base para base. Se a sua base
for diferente, o suporte adapta o bloco na instalação.
{% endhint %}

Com o bloco:

* A seleção mostra todos os personagens da conta (até `Config.Slots`). Entrar com **outro**, ou criar um **novo**,
  reconecta o jogador (alguns segundos) e o `vrp` carrega o escolhido.
* **Excluir** personagem tira ele da seleção (os dados ficam no banco). O personagem em uso não pode ser excluído.
* Personagem novo herda a **whitelist** da conta.
* O próximo acesso entra no último personagem usado.
* O one\_lib não mexe em `vrp_user_ids` nem nos identificadores: quem decide é o `vrp`, com a resposta do one\_lib.

O console confirma ao iniciar: `vários personagens: sim (patch no vrp ativo)`.

**Confira o relatório no console** ao iniciar o servidor. O one\_lib mostra o que encontrou na sua base:

```
[one_lib] compatibilidade com a base (vrpex): tudo encontrado
[one_lib]   funções: getCore
[one_lib]   identidade: vrp_user_identities (nome=nome, sobrenome=sobrenome, idade=idade, nascimento=data_nascimento)
[one_lib]   personagem criado: vrp_users_infos.controller
```

Linhas em amarelo (`faltando ...`) dizem o que não foi encontrado e o que deixa de funcionar. Mande esse trecho ao
suporte se algo não estiver certo.

**O que remover** (tire o `ensure` do `server.cfg`): todo script que abre ao conectar para criar personagem,
registrar identidade ou escolher spawn. Os nomes mais comuns no vRPex: `vrp_creation`, `vrp_character`,
`vrp_identity` (só a tela de registro), `vrp_spawn`, `nation_creator`, `creator`, `spawnselector`.
Na dúvida: conecte com uma conta nova; se aparecer qualquer tela além da do `one_characters`, o script
dela ainda está ligado.

**O que manter**: o `vrp` (só com o bloco acima, se quiser vários personagens) e o `spawnmanager`. Lojas de
roupa e barbearia continuam funcionando.

**Diagnóstico**: `onelib_vrpex <id do jogador>` no console do servidor mostra os personagens da conta e qual a
próxima conexão carrega.

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
