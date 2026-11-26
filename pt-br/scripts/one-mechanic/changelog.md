---
description: Histórico de versões da Forja (one_mechanic).
---

# Changelog

## 1.0.0

Primeira versão estável da Forja: mecânica, tuning e customização de veículos para Creative, vRPex, ESX, QBCore e Qbox. Modo express (sem andar de ponto em ponto): estação de trabalho com elevador, atendimento externo na rua e autoatendimento configurável; inspeção em uma barra; lataria lida peça por peça (ossos reais, amassado por região, lanternas por osso) com conserto seletivo; cobrança pelo ID do cliente; gestão com estoque, fornecedor, fabricação, equipe e garantia.

* **Lataria peça por peça:** a ordem de faróis, vidros, portas, para-choques e lataria lê o dano real do carro e o mecânico visita só as peças que precisam, com a marca em cima da peça (osso real do modelo).
* **Leitura do carro:** portas, vidros (índices reais do jogo: 4 e 5 são vidros centrais, 6 é o para-brisa e 7 o vidro traseiro), faróis, lanternas e setas (osso quebrado), amassado por região com gravidade (leve, média, forte).
* **Conserto seletivo:** trocar farol, porta ou para-choque preserva o resto do amassado e as luzes que a ordem não cobre; só "Lataria" apaga o amassado.
* **Inspeção:** lista o nome de cada peça danificada, e uma peça quebrada já aparece como problema.
* **Ajuste fino:** altera o handling real do carro (força, freio, aderência, suspensão); o dinamômetro mostra a curva.
* **Ferramenta de diagnóstico:** `/forja_scan` (com `set one_mechanic:debug true`) escreve cada peça danificada no lugar dela no carro.

## 0.1.0 (em testes)

Primeira versão completa, ainda sem a rodada de teste em jogo.

* **v2 (express):** atendimento externo na rua (`/tablet` ou mira), autoatendimento configurável, kit de reparo só motor/bateria/pneus, cobrança pelo ID do cliente sem aprovação prévia, inspeção em uma barra, execução uma ação por serviço e app de gestão com navegação lateral.
* **Garantia e disputa:** `/garantia`, aba Garantia na gestão (refazer grátis, reembolsar, recusar). Serviços clandestinos na estação de trabalho, `/ranking` e `/pericias`.
* **Oficinas e ordens de serviço:** oficinas de jogador ou emprego, equipe, cargos como dado, pontos com criador a laser, preço no servidor, aprovação do cliente, comissão, garantia e avaliação.
* **Desgaste e diagnóstico:** telemetria do motorista, sintomas, superaquecimento, fumaça, luzes de aviso, inspeção por zona, scanner OBD, alinhador, relatório com validade, reparo de rua e guincho.
* **Peças e ajuste:** 15 peças com origem e qualidade, pipeline de handling, ajuste fino de 16 campos, chip de ajuste, dinamômetro com certificado.
* **Visual:** catálogo do Mod Kit com prévia, pintura com nota e verniz que desgasta, rodas, stance, neon, película, adesivos e pacotes.
* **Economia e gente:** estoque, fornecedor com preço por demanda, desmanche, reciclagem, fabricação, perícias, licenças, mentoria e frotas.
* **Lei e corrida:** oito regras, vistoria, perícia, classes de corrida e exports; sabotagem opcional.
* **Drivetrain** opcional e experimental: nitro, câmbio manual e controle de tração.
* Painel da cidade com simulador. Exige `one_lib` 0.8.0.
