---
description: Scripts premium para FiveM. A imersão de GTA VI na plataforma do GTA V.
cover: .gitbook/assets/cover-home.svg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
---

# Network Scripts

Sistemas para FiveM feitos com o padrão de um jogo AAA: interface refinada, imersão no mundo do jogo e desempenho de **0.00 ms** quando ociosos.
Instalam em minutos na sua base, seja ela **vRP Creative, vRPex, ESX, QBCore, Qbox** ou **Standalone**.

{% hint style="success" %}
**Compra e suporte acontecem no nosso Discord.** [Entrar no Discord](https://discord.gg/ntqpUuHmYV)
{% endhint %}

## Veja funcionando

{% tabs %}
{% tab title="one_hud" %}
{% embed url="https://www.youtube.com/watch?v=XRstOl4t62M" %}
{% endembed %}
{% endtab %}

{% tab title="one_inventory" %}
{% embed url="https://www.youtube.com/watch?v=JvsmuEtCk-I" %}
{% endembed %}
{% endtab %}

{% tab title="one_characters" %}
{% embed url="https://www.youtube.com/watch?v=J-Bzgvd9RtM" %}
{% endembed %}
{% endtab %}
{% endtabs %}

## Produtos

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>one_characters</strong></td><td>Seleção, criação e spawn de personagem com line-up no mundo, prévia aérea do spawn e entrada estilo GTA.</td><td><a href="vitrine/one-characters.md">one-characters.md</a></td><td><a href=".gitbook/assets/cover-characters.svg">cover-characters.svg</a></td></tr><tr><td><strong>one_inventory</strong></td><td>Bolsos, mochila, baús, lojas, bancadas e porta-malas num sistema só. Seus scripts continuam funcionando.</td><td><a href="vitrine/one-inventory.md">one-inventory.md</a></td><td><a href=".gitbook/assets/cover-inventory.svg">cover-inventory.svg</a></td></tr><tr><td><strong>one_hud</strong></td><td>HUD, velocímetro, notificações, progresso e formulários no mesmo visual.</td><td><a href="vitrine/one-hud.md">one-hud.md</a></td><td><a href=".gitbook/assets/cover-hud.svg">cover-hud.svg</a></td></tr><tr><td><strong>one_workshop</strong></td><td>A oficina de armas: bancada física, acessórios e skins para todas as armas, cobradas em dinheiro, itens ou gemas.</td><td><a href="vitrine/one-workshop.md">one-workshop.md</a></td><td><a href=".gitbook/assets/cover-workshop.svg">cover-workshop.svg</a></td></tr><tr><td><strong>Base Network One</strong></td><td>A base completa que roda todos os nossos sistemas, pronta para abrir sua cidade.</td><td><a href="vitrine/base-network-one.md">base-network-one.md</a></td><td><a href=".gitbook/assets/cover-base.svg">cover-base.svg</a></td></tr></tbody></table>

## Funciona na sua base

| | vRP Creative | Creative v4/v5 | vRPex | ESX | QBCore | Qbox | Standalone |
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **one_characters** | ✅ | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 |
| **one_inventory** | ✅ | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 |
| **one_hud** | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 |
| **one_workshop** | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | – |

✅ estável (validado em jogo) · 🧪 beta (validado em laboratório nas bases reais; relatos no [Discord](https://discord.gg/ntqpUuHmYV))

O [one\_lib](one-lib/) detecta o seu framework sozinho: o mesmo download funciona em todas as bases. Detalhes em [Frameworks suportados](comece-aqui/frameworks-suportados.md).

## Por que Network Scripts

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Imersão primeiro</strong></td><td>O que pode acontecer no mundo do jogo acontece no mundo: câmeras cinematográficas, personagens reais em cena, sons dos próprios menus do GTA.</td></tr><tr><td><strong>0.00 ms ocioso</strong></td><td>Nenhum sistema roda nada quando não está em uso. Uma única biblioteca compartilhada evita trabalho duplicado entre scripts.</td></tr><tr><td><strong>Instala em qualquer base</strong></td><td>Creative, vRPex, ESX, QBCore, Qbox e Standalone. Os scripts que você já tem continuam funcionando.</td></tr><tr><td><strong>Seguro por padrão</strong></td><td>O servidor valida tudo. O cliente só escolhe entre opções que o servidor ofereceu, e toda ação tem limite de frequência.</td></tr><tr><td><strong>Tudo editável</strong></td><td>Config, textos e pontos de integração ficam abertos para você editar, mesmo com o código protegido.</td></tr><tr><td><strong>Português e inglês</strong></td><td>Todos os textos, inclusive os da interface, vêm de arquivos de idioma que você pode traduzir ou ajustar.</td></tr></tbody></table>

## Como funciona

1. **Instale o one\_lib.** É a biblioteca que todos os produtos compartilham. [Instalação rápida](comece-aqui/instalacao-rapida.md).
2. **Instale o produto** na pasta de recursos e inicie depois do one\_lib. Cada produto tem um guia por base.
3. **Ajuste o config.lua** (preços, cores, textos). O resto o produto resolve sozinho.

{% content-ref url="comece-aqui/instalacao-rapida.md" %}
[instalacao-rapida.md](comece-aqui/instalacao-rapida.md)
{% endcontent-ref %}

{% content-ref url="comece-aqui/frameworks-suportados.md" %}
[frameworks-suportados.md](comece-aqui/frameworks-suportados.md)
{% endcontent-ref %}

## Perguntas frequentes

<details>

<summary>Preciso trocar minha base?</summary>

Não. Os produtos se adaptam à sua base e continuam funcionando com os scripts que você já tem (por exemplo, o one\_inventory atende scripts feitos para ox\_inventory e qb-inventory).

</details>

<details>

<summary>Como funciona a compra e o suporte?</summary>

Tudo pelo [Discord](https://discord.gg/ntqpUuHmYV): compra, entrega, licença e suporte por ticket. Veja [Compra, entrega e licença](comece-aqui/compra-e-licenca.md).

</details>

<details>

<summary>Posso editar textos, cores e regras?</summary>

Sim. Config, textos (português e inglês) e os pontos de integração ficam abertos. A cor de destaque de todos os produtos muda com uma linha ([Cor das telas](comece-aqui/cor-das-telas.md)).

</details>

<details>

<summary>Posso fazer um script meu usar o one_lib?</summary>

Pode. A biblioteca é documentada e aberta para desenvolvedores: [Usando o one\_lib no seu script](desenvolvedores/usando-one-lib.md).

</details>

## Fale com a gente

Dúvidas, sugestões e o que vem a seguir são decididos no [Discord](https://discord.gg/ntqpUuHmYV).
