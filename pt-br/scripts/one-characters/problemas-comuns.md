---
description: Soluções para os problemas mais comuns do one_characters.
---

# Problemas comuns

<details>

<summary>Duas telas de personagem abrem ao mesmo tempo</summary>

A seleção antiga do framework continua ativa. Veja "O que desativar" na [Instalação](instalacao.md#por-framework).

</details>

<details>

<summary>A tela não abre e o jogador fica numa tela preta</summary>

1. Confira no console do servidor se aparece `[one_lib] ... framework: <nome>` com o framework certo.
   Se estiver errado, force com `setr one:framework "<nome>"`.
2. Procure por `one_characters` no console do servidor: o motivo aparece lá
   (ex.: `o framework "x" ainda não tem adapter de personagens`).
3. ESX: confirme que a pasta `esx_multicharacter` **existe** no servidor (mesmo sem `ensure`).

</details>

<details>

<summary>Só aparece 1 slot liberado (vRP Creative)</summary>

O Creative usa a coluna `accounts.Characters`, que vem com `1` por padrão. Aumente no banco ou defina sua
regra em [`Hooks.GetSlots`](personalizacao.md#slots).

</details>

<details>

<summary>A câmera ficou dentro de uma parede ou longe do personagem</summary>

Se você mudou a cena, confira se o `z` de `Config.Scene.Lineup` e `Config.Scene.Creator` é a altura do
**chão**. A câmera recua sozinha quando há parede entre ela e o personagem.

</details>

<details>

<summary>Algum slider de rosto funciona ao contrário</summary>

Em `shared/data.lua`, adicione ou remova o índice da feature em `Data.FaceInvert`. A lista de índices está
comentada no próprio arquivo.

</details>

<details>

<summary>A roupa criada não aparece na loja de roupas</summary>

Confira qual sistema de roupa foi detectado: a mensagem de start do `one_lib` mostra `aparência: <nome>`.
Se aparecer `one`, seu sistema não foi reconhecido; force com `setr one:appearance "illenium"` (ou
`skinchanger`, `creative`).

</details>

<details>

<summary>"Calma! Aguarde um instante."</summary>

É o limite de frequência protegendo o servidor contra spam. Aparece só quando o jogador repete a mesma
ação muitas vezes em poucos segundos.

</details>
