---
description: Tudo o que dá para ajustar no config.lua da one_workshop.
---

# Configuração

## Bancadas

| Opção | O que faz |
|---|---|
| `Config.Benches` | Bancadas da cidade. Cada uma: `id`, `type`, `coords` (chão em frente, `w` = direção), `label`, `prop` (modelo criado ali; sem ele, use uma bancada do mapa e informe `top`), `ped` (atendente), `blip`, `groups`/`grade` (sobrescreve o tipo), `society` (comissão) e `prices` (fator de preço). |
| `Config.BenchTypes` | O que cada tipo faz: `parts` (acessórios), `paint` (cores), `skins` (skins e acabamentos) e `groups`/`grade` (quem usa). Crie quantos tipos quiser. |
| `Config.BenchProp` | Modelo padrão da bancada. |
| `Config.Mat` | Centro e tamanho da manta (as peças não saem dela). |
| `Config.Camera` / `Config.Inspect` | Altura da câmera e inspeção 360°. |
| `Config.Scene` | Luz da bancada (cor, brilho, altura). |

```lua
Config.Benches = {
	{
		id = 'ammunation', type = 'public', coords = vec4(21.6, -1106.6, 28.8, 160.0), prop = 'prop_tool_bench02',
		label = 'Oficina Ammu-Nation', blip = { sprite = 110, color = 5 },
		ped = { model = 's_m_y_ammucity_01', coords = vec4(22.5, -1105.2, 29.8, 160.0) },
		society = { name = 'ammunation', percent = 30 }, prices = { skins = 0.9 }
	},
}
```

## Acessórios e cor

| Opção | O que faz |
|---|---|
| `Config.Items` | Item que cada tipo de acessório pede quando a cobrança aceita itens. A chave é o tipo exato (`'muzzle.supp'`) ou a família (`'muzzle'`). `false` = livre. |
| `Config.PaintItem` | Item gasto a cada troca de cor (quando a cobrança da cor aceita itens). |
| `Config.ItemDefs` | Nome, peso e descrição dos itens (usados no cadastro e no one\_inventory). |
| `Config.Weapons` | Armas da oficina (nome interno → nome mostrado). Armas addon entram aqui. |
| `Config.ExtraComponents` | Acessórios ou acabamentos extras por arma (addons). |

## Cobrança e skins

| Opção | O que faz |
|---|---|
| `Config.Pricing` | Forma de cobrar de cada categoria (`item`, `money`, `gems`, `hybrid`, `free`) e as contas de dinheiro. |
| `Config.Prices` | Preços dos acessórios (por tipo, família e padrão) e da cor. |
| `Config.Gems` | De onde vêm as gemas (`auto`, `item`, `custom`, `none`). |
| `Config.Society` | Função que paga a comissão das bancadas ao emprego. |
| `Config.Skins` | Pacotes (`packs`, `packOptions`), skins iniciais, raridade por estilo, preço por raridade, fator por arma, preço específico e acesso. |

Detalhes em [Cobrança](cobranca.md) e [Skins](skins.md).

## Logs e administração

| Opção | O que faz |
|---|---|
| `Config.Logs` | Quais eventos vão para o Discord (`apply`, `buy`, `admin`). O webhook fica na convar `one_workshop:webhook`. |
| `Config.AdminGroups` | Grupos com acesso de admin, além do ACE `oneworkshop.admin`. |
| `Config.Accent` | Cor de destaque das telas (ou a geral do servidor em `setr one:accent`). |
| `Config.Debug` / `Config.DebugFree` | `/oficina` e `/skinlab` (só com a convar `one_workshop:debug`) e bancada de teste sem custo. Em produção ficam desligados. |
