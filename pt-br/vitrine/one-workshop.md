---
description: >-
  A oficina de armas da cidade: bancada física, acessórios e uma coleção de skins para todas as armas, cobrada em dinheiro, itens ou gemas.
cover: ../.gitbook/assets/cover-workshop.svg
coverY: 0
---

# one\_workshop

A arma do jogador ganha identidade. Numa **bancada de verdade** da cidade ele monta acessórios, troca a cor e escolhe entre dezenas de skins,
com prévia ao vivo e inspeção em 360°. Para o dono do servidor, é uma fonte de receita: cada categoria cobra em **dinheiro, itens, gemas** ou
deixa o jogador escolher.

{% hint style="success" %}
**Disponível** para vRP Creative (todas as gerações), vRPex, ESX, QBCore e Qbox. [Comprar no Discord](https://discord.gg/ntqpUuHmYV)
{% endhint %}

## Destaques

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Bancada física</strong></td><td>A arma e as peças reais do GTA ficam na mesa. Pegue com o mouse, leve até o encaixe e veja montada antes de soltar.</td></tr><tr><td><strong>Skins para todas as armas</strong></td><td>Cada skin troca o modelo inteiro e a arma continua a mesma: inventário, munição e acessórios intactos, e todo mundo vê.</td></tr><tr><td><strong>Galeria completa</strong></td><td>Raridades, coleções, filtros, "minhas" e prévia ao vivo na arma da mesa.</td></tr><tr><td><strong>Inspeção 360°</strong></td><td>Gire a arma com inércia, aproxime e confira cada detalhe.</td></tr><tr><td><strong>Números do jogo</strong></td><td>Barras de dano, cadência, capacidade, precisão e alcance mostram o efeito de cada peça antes de instalar.</td></tr><tr><td><strong>Coleção permanente</strong></td><td>Comprou, é do personagem: serve em qualquer arma daquele modelo e trocar é grátis.</td></tr></tbody></table>

## Na bancada

| Aba | O que o jogador faz |
|---|---|
| **Acessórios** | peças reais do jogo, cada uma com o efeito nos números da arma |
| **Cor** | troca a cor da arma |
| **Skins** | galeria com raridade e coleção, prévia na arma da mesa, compra e equipar |

Cada tipo de bancada libera só o que o dono quer. Os três tipos que vêm prontos: **pública** (cor e skins),
**armeiro** (tudo, restrito a quem trabalha na oficina ou na polícia) e **clandestina** (tudo, para qualquer um). Crie quantos tipos quiser.

## Detalhes que fazem diferença

* **Uma pessoa por bancada:** quem está usando a trava; os outros esperam.
* **Cobrança segura:** é feita no servidor e é tudo-ou-nada. Se algo falha no meio, o que já saiu volta.
* **Salva no item da arma** no one\_inventory, ox\_inventory e qb-inventory; nas outras bases, numa tabela própria que reaplica ao sacar.
* **Ocioso = 0.00 ms:** nada roda sem bancada aberta.
* **Autoteste** (`workshop_selftest`) que confere configuração, banco, pacotes, cobrança e as regras de compra e aplicação sem alterar o servidor.

## Para o dono do servidor

* **Cobrança do seu jeito:** dinheiro, itens, gemas, híbrido (o jogador escolhe) ou grátis, por categoria. Gemas da base Creative funcionam sozinhas; nas outras bases use um item ou ligue o seu sistema de moedas.
* **Monetização:** skins só por gemas, skins de VIP, facção ou permissão, pacotes exclusivos, preço por raridade, por arma, por pacote e por bancada.
* **Bancadas onde você quiser:** blip, atendente, acesso por emprego ou cargo, desconto e **comissão para o emprego dono**.
* **Pacotes de skins:** ligue vários ao mesmo tempo, os seus e os de outros criadores. O formato é aberto.
* **Controle:** logs no Discord, `/oficina_dar` e `/oficina_tirar`, e validação do config ao iniciar.
* **Idiomas:** português e inglês.

## Compatibilidade

| Base | Status | Onde a personalização fica salva |
|---|:-:|---|
| vRP Creative | 🧪 | tabela própria, reaplicada ao sacar |
| vRP Creative v4/v5 | 🧪 | tabela própria, reaplicada ao sacar |
| vRPex | 🧪 | tabela própria, reaplicada ao sacar |
| ESX | 🧪 | no item da arma (ox\_inventory) ou tabela própria |
| QBCore | 🧪 | no item da arma (qb-inventory) |
| Qbox | 🧪 | no item da arma (ox\_inventory) |

✅ estável (validado em jogo) · 🧪 beta (validado em laboratório nas bases reais; relatos no [Discord](https://discord.gg/ntqpUuHmYV))

Com o `one_inventory` instalado, a personalização fica no item da arma em qualquer base.

{% hint style="info" %}
As skins vêm em **pacotes** separados, gerados a partir do GTA V do próprio servidor. Veja [Pacotes de skins](../scripts/one-workshop/pacotes.md).
{% endhint %}

## O que vem na compra

* O recurso `one_workshop` e o `one_lib` (biblioteca comum dos produtos Network Scripts).
* Os 24 itens da oficina com imagens e arquivos de cadastro para one\_inventory, ox\_inventory, qb-inventory, ESX e Creative.
* Documentação completa em português: instalação, configuração, cobrança, skins, pacotes e administração.
* Atualizações dentro da versão comprada e suporte por ticket no Discord.

## Perguntas frequentes

<details>
<summary>As skins vêm junto com o script?</summary>

As skins vêm em pacotes separados, gerados a partir do GTA V do seu servidor. A oficina funciona com quantos
pacotes você ligar, inclusive os de outros criadores. Veja [Pacotes de skins](../scripts/one-workshop/pacotes.md).

</details>

<details>
<summary>A skin muda a arma do jogador?</summary>

Não. É um componente da arma: ela continua sendo a mesma, com a mesma munição, os mesmos acessórios e o mesmo
lugar no inventário. Os outros jogadores veem a skin sem nada extra.

</details>

<details>
<summary>Posso cobrar só em gemas?</summary>

Sim, por categoria. Na base Creative as gemas da base funcionam sozinhas; nas outras, use um item como gema ou
ligue o seu sistema de moedas com três funções.

</details>

<details>
<summary>Preciso de um inventário específico?</summary>

Não. Funciona com one\_inventory, ox\_inventory, qb-inventory ou o inventário da sua base.

</details>

{% content-ref url="../scripts/one-workshop/" %}
[one-workshop](../scripts/one-workshop/)
{% endcontent-ref %}
