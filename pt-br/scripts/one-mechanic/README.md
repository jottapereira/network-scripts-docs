---
description: Documentação técnica da Forja (one_mechanic), o sistema de mecânica de veículos.
---

# one\_mechanic (Forja)

Mecânica, tuning e customização de veículos com desgaste real, diagnóstico, oficinas de jogador, economia de peças e perícia. Tudo é **dado**
(componentes, peças, regras, receitas, perícias), então o dono da cidade muda o que quiser sem mexer em código.

{% hint style="warning" %}
**Em testes.** O laboratório automático passa nas 7 bases (664 verificações), mas o sistema inteiro ainda não passou pela rodada de teste em jogo.
Use o roteiro de testes em jogo que acompanha o pacote (`docs/testing/one_mechanic.md`) antes de abrir em produção.
{% endhint %}

## Como funciona

```
Carro rodando ──► o motorista mede (1 vez por segundo) e envia a cada 30 s ──► o servidor valida e converte em desgaste
  └─ peças ganham/perdem vida · sintomas aparecem (potência, freio, ignição, calor) · luzes acendem no painel

Cliente leva o carro à oficina ──► terminal no ponto de trabalho
  ├─ inspeção (olho, scanner OBD, alinhador, dinamômetro) ──► relatório com validade
  ├─ ordem de serviço (peças + mão de obra, preço do servidor) ──► o cliente aprova ──► o mecânico executa ──► cobrança, comissão e garantia
  └─ peças de desempenho, ajuste fino, visual e pintura com nota: tudo vira linha da ordem
```

## Módulos

Cada módulo liga e desliga em `Config.Modules`; um módulo desligado não registra evento nem roda laço.

| Módulo | O que faz |
|---|---|
| `shops`, `orders` | Oficinas de jogador ou de emprego, equipe e cargos, pontos de trabalho, ordens de serviço, aprovação, comissão, garantia, avaliação |
| `wear`, `diagnosis` | Desgaste por componente, sintomas, superaquecimento, luzes de aviso, inspeção por zona, scanner OBD, relatório |
| `roadside` | Reparo de rua limitado, troca de pneu, partida de emergência, guincho |
| `parts`, `tuning`, `dyno` | Peças com origem e qualidade, ajuste fino, chips de ajuste, dinamômetro com curva e certificado |
| `visual` | Catálogo do Mod Kit com prévia, pintura com nota S–C, verniz, rodas e stance, neon, película, adesivos |
| `economy`, `skills` | Estoque, fornecedor, venda, desmanche, reciclagem, fabricação; perícias, licenças, mentoria |
| `legality`, `racing`, `sabotage` | Regras, vistoria, perícia (hodômetro, VIN, clone), classes de corrida, sabotagem opcional |
| `drivetrain` | Opcional: câmbio manual, controle de tração e nitro (experimental) |

## Páginas

* [Instalação](instalacao.md) · [Configuração](configuracao.md) · [Conteúdo (peças, regras, receitas)](conteudo.md)
* [Oficinas e ordens de serviço](oficinas-e-ordens.md) · [Desgaste e diagnóstico](desgaste-e-diagnostico.md) · [Peças e ajuste](pecas-e-ajuste.md)
* [Visual e pintura](visual.md) · [Economia e perícias](economia-e-pericias.md) · [Lei, perícia e corrida](lei-e-corrida.md)
* [Integração com outros scripts](integracoes.md) · [Problemas comuns](problemas-comuns.md) · [Changelog](changelog.md)
