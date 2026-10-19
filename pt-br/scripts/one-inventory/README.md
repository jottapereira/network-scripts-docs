---
description: Inventário, baús, lojas, bancadas, porta-malas, chão e armas em um só sistema, em qualquer base.
---

# one\_inventory

{% hint style="warning" %}
Versão 1.0 em teste. Esta documentação acompanha a versão em teste.
{% endhint %}

Um único sistema para tudo que envolve itens: bolsos, mochila, equipamento, chão, porta-malas, porta-luvas,
baús, lojas, bancadas e revista. Ele vira a **fonte da verdade dos itens** do servidor, e os scripts que você já
tem continuam funcionando.

## Destaques

* **Servidor como única autoridade.** Toda movimentação é validada e aplicada de uma vez no servidor; a interface
  responde na hora e desfaz se o servidor recusar. Sem duplicação de itens.
* **O seu personagem na tela.** A pé, o inventário abre com a câmera no seu personagem (gire arrastando); em baús,
  lojas e veículos, ele aparece como parte da interface.
* **Itens com vida.** Metadados por item (número de série, durabilidade por tempo, munição na arma, dados da base).
* **Containers de verdade.** Mochila equipada vira um inventário próprio; maletas e bolsas guardam itens e o
  **peso do conteúdo conta** para quem carrega.
* **Mundo físico.** Item solto vira objeto no chão; o porta-malas abre a tampa e o personagem faz a animação.
* **Interação 3D.** Lojas, bancadas e baús mostram uma marca ao chegar perto e o cartão de opções no alcance; o
  porta-malas abre mirando no carro.
* **Lojas e bancadas** na mesma tela: estoque gravado, moeda em dinheiro ou item, fila de fabricação que continua
  com o jogador offline.
* **Peso que pesa** e **rastro de digitais** para a polícia.
* **Interface de jogo.** Arrastar com Shift (metade) e Ctrl (um), hotbar 1–5, menu de contexto, busca e filtros.
* **Ocioso = 0.00 ms.** Fechado, nada roda em loop. A interface recebe só as diferenças.

## Funciona na sua base

| vRP Creative | Creative v4/v5 | vRPex | ESX | QBCore | Qbox | Standalone |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| ✅ | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 | 🧪 |

Scripts feitos para `ox_inventory` e `qb-inventory` funcionam sem alteração. Veja
[Compatibilidade e migração](compatibilidade.md).

## Páginas

* [Instalação](instalacao.md): um guia por base
* [Configuração](configuracao.md)
* [Integração com outros scripts](integracoes.md)
* [Compatibilidade e migração](compatibilidade.md)
* [Extensão Creative](extensao-creative.md)
* [Problemas comuns](problemas-comuns.md)
* [Changelog](changelog.md)
