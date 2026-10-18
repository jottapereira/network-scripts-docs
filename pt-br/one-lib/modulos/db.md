---
description: Banco de dados via oxmysql e migrações versionadas.
---

# DB

| Função | Retorno |
|---|---|
| `One.DB.Query(sql, params)` | linhas |
| `One.DB.Single(sql, params)` | primeira linha |
| `One.DB.Scalar(sql, params)` | primeiro valor |
| `One.DB.Insert(sql, params)` | id inserido |
| `One.DB.Update(sql, params)` | linhas afetadas |
| `One.DB.Prepare(sql, params)` | statement preparado |
| `One.DB.Transaction(queries, params)` | `boolean` |
| `One.DB.Migrate(files)` | aplica migrações pendentes |

## Migrações

Cada recurso declara seus arquivos SQL em ordem. Só os ainda não aplicados rodam, e o registro fica na
tabela `one_migrations`.

```lua
CreateThread(function()
    One.DB.Migrate({
        'sql/001_init.sql',
        'sql/002_add_column.sql'
    })
end)
```

{% hint style="warning" %}
Nunca edite nem reordene um arquivo já publicado. Toda mudança é um arquivo novo. Instruções separadas por
`;`, sem `;` dentro de strings.
{% endhint %}
