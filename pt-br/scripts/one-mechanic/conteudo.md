---
description: "Peças, regras, acabamentos, receitas e perícias são dados: como criar e mudar."
---

# Conteúdo

A Forja não tem regra escondida no código. O que o jogo faz com cada peça, regra e receita vem de arquivos em `content/` (abertos, fora do escrow).
**Registrar um id que já existe mescla** com o padrão: só o que você escrever muda.

| Tipo | Registro | O que define |
|---|---|---|
| Componentes | `Forja.Component` | Vida em km, zona, item da peça, sintomas por estado, o que acelera o desgaste, como se diagnostica |
| Peças | `Forja.Part` | Slot, item, preço, mão de obra, modificadores de handling, requisitos, estresse, legalidade |
| Origens | `Forja.Origin` | Nova, original, recondicionada, usada, artesanal, pirata: faixas de qualidade e vida |
| Campos de ajuste | `Forja.TuneField` | Os 16 campos do ajuste fino, o slot que libera cada um e a faixa |
| Regras | `Forja.Rule` | Infrações da legalidade: gravidade, multa, consequência |
| Acabamentos / tipos do Mod Kit | `Forja.Finish`, `Forja.VMod` | Pintura e modificações visuais com preço |
| Receitas, perícias, serviços, itens | `Forja.Recipe`, `Forja.Skill`, `Forja.Service`, `Forja.Item` | Fabricação, XP, serviços da ordem, itens de rua e materiais |
| Luzes, cargos, tipos de oficina | `Forja.Light`, `Forja.Role`, `Forja.ShopType` | Painel do carro, permissões da equipe, o que cada oficina oferece |

## Exemplo

Copie `examples/custom_content.lua` para `content/zz_custom.lua` (o prefixo `zz` carrega por último):

```lua
-- Uma peça nova
Forja.Part('turbo_hybrid', {
  label = 'Turbo híbrido', slot = 'turbo', item = 'turbo_hybrid', price = 12500, labor = 100, tier = 2, life = 90000,
  mods = { { field = 'fInitialDriveForce', op = 'mul', value = 1.2 } },
  stress = { oil = 1.15, radiator = 1.1 }
})

-- Mudar regras e componentes existentes: só o que você escreve muda
Forja.Rule('neon', { fine = 0 })
Forja.Component('oil', { life = 5000 })
Forja.Light('oil', { from = 1 })
```

O console valida tudo ao subir (`forja_status`) e o painel da cidade lista problemas do conteúdo (campo faltando, componente que não existe,
faixa inválida). Um erro de conteúdo nunca derruba o servidor: o item inválido é apontado e ignorado.

## Pacotes de adesivos

Um recurso de terceiros dá nome aos índices de adesivo dos carros dele:

```lua
exports.one_mechanic:RegisterLiveryPack({
  name = 'meu_pack', label = 'Meu pacote',
  liveries = { { model = 'sultan', index = 1, label = 'Rally azul' } }
})
```

Há um exemplo pronto em `examples/forja_pack_exemplo/`.
