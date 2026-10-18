---
description: Empregos, gangues e grupos normalizados.
---

# Groups

A **grade** é sempre um inteiro: `0` é o cargo mais baixo e cresce com a senioridade, em todos os frameworks.

| Função | Retorno |
|---|---|
| `One.Groups.Has(src, name, minGrade?)` | `boolean`. `name` pode ser uma lista (basta ter um) |
| `One.Groups.Get(src)` | lista de grupos |
| `One.Groups.GetJob(src)` | primeiro grupo do tipo `job` ou `nil` |

Cada grupo:

```lua
{ name = 'police', label = 'Polícia', grade = 3, gradeLabel = 'Sargento', type = 'job', duty = true }
```

`type` é `job`, `gang` ou `group`. `duty` é `nil` quando o framework não tem serviço.

```lua
if One.Groups.Has(src, { 'police', 'sheriff' }, 2) then
    -- policial ou xerife com grade 2 ou mais
end
```
