---
description: Textos traduzíveis, com variáveis.
---

# Locale

Os textos ficam em `locales/<idioma>.lua` no **seu** recurso:

```lua
-- locales/pt-BR.lua
return {
    ['welcome'] = 'Bem-vindo, {name}!'
}
```

```lua
One.Locale('welcome', { name = 'Lamar' })   -- 'Bem-vindo, Lamar!'
```

| Função | Descrição |
|---|---|
| `One.Locale(key, vars?)` / `One.Locale.T(key, vars?)` | texto traduzido |
| `One.Locale.All()` | tabela completa (para enviar à NUI) |
| `One.Locale.Language()` | idioma ativo |

**Idioma usado:** `Config.Locale` do recurso → convar `one:locale` → `pt-BR`.
**Chave ausente:** usa o texto em `en`; se também não existir, mostra a própria chave.

{% hint style="warning" %}
Para o cliente ler os arquivos, inclua `'locales/*.lua'` em `files` no `fxmanifest.lua`.
{% endhint %}
