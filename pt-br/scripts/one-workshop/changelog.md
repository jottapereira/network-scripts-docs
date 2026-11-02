---
description: Histórico de versões da one_workshop.
---

# Changelog

## 1.1.0

* **Cobrança por regras:** forma de pagar (item, dinheiro, gemas) e escopo (**só nesta arma** ou **vitalício**) por categoria e por tipo de bancada. Vêm prontos os tipos Ammu-Nation, polícia (acessório de graça), clandestina (pede item) e pública; crie os seus.
* **Acessórios vitalícios:** o personagem desbloqueia a peça e encaixa de graça em qualquer arma que a aceite. Skins cobram ao aplicar, sem tela de compra separada.
* **Aba Meus itens:** acessórios com item no inventário, vitalícios, gravados na arma e as suas skins; a mesa sempre abre só com a arma.
* **Bancada de armas do GTA Online** no lugar da mesa de ferramentas (com a antiga como reserva) e mesa presente no mundo antes de abrir. O comando `/bancada` mostra a mesa na sua frente e gera a linha de `Config.Benches`.
* **Encaixe de verdade:** só no ponto certo, lugar ocupado pede para retirar a peça, o menu encaixa (e troca) e retira, o ponto do carregador fica onde ele entra, e o enquadramento acompanha o tamanho da arma.
* **Pintura numa escolha só:** Original, cores, acabamentos e skins, com fotos reais da arma no jogo.
* **Corrigido:** a personalização (skins, acabamentos e peças pagas com dinheiro ou gemas) sumia ao guardar e sacar a arma. Exige o `one_lib` mais recente.
* **Gemas** por conta do framework (`account`) além de item, `custom` e a automática da Creative.
* Interface refeita: abas com ícone, cabeçalho com saldo, painel de desempenho e barra de ações.

## 1.0.0

* **Bancadas** em locais do config: blip, atendente, acesso por emprego ou cargo, uma pessoa por vez, desconto por bancada e comissão para o emprego dono.
* **Bancada física:** arma e acessórios reais do GTA na manta, pegar e soltar com o mouse, prévia montada antes de soltar, inspeção 360°, números do jogo.
* **Acessórios, cores e pinturas**, salvos no item da arma (one\_inventory, ox\_inventory, qb-inventory) ou numa tabela própria nas outras bases.
* **Skins por pacotes:** vários ao mesmo tempo, galeria com raridades, coleções e filtros, prévia ao vivo, compra, posse permanente por personagem, acesso por grupo, cargo ou permissão.
* **Cobrança** em dinheiro, itens, gemas, híbrida ou grátis, por categoria; cobrança atômica; gemas da base Creative sozinhas.
* **Ferramentas:** `/skinlab` (vitrine), `workshop_selftest` (autoteste), validação do config ao iniciar, `workshop_export` e logs no Discord.
