---
description: O comando onedebug mostra como os scripts enxergam o seu personagem.
---

# Diagnóstico (onedebug)

Com o personagem carregado, abra o console do **F8** e digite:

```
onedebug
```

Exemplo de resultado:

```
[one_lib] cliente
  charId: 2
  cache: ped=9474 vehicle=false seat=false weapon=false
  foco NUI: nil
[one_lib] servidor v0.3.0 · framework: creative
  charId: 2 · nome: Lamar Davies
  dinheiro: cash=0 bank=5000 dirty=0
  grupo: Admin (group) grade=2 Administrador duty=true
```

## Como ler

| Linha | O que conferir |
|---|---|
| `framework` | é o seu framework? Se não, force com `setr one:framework` |
| `charId` | aparece nos dois lados (cliente e servidor)? Se estiver `nil`, o personagem não foi registrado |
| `dinheiro` | bate com o que o jogador tem? |
| `grupo` | os cargos aparecem com a grade certa (`0` = mais baixo)? |
| `foco NUI` | nome de um recurso aqui com nenhuma tela aberta indica foco preso |

{% hint style="info" %}
Cada jogador só vê os próprios dados. É seguro pedir o print para qualquer jogador.
{% endhint %}
