---
description: Atendimento externo (na rua), autoatendimento, kit de reparo e a cobrança pelo ID do cliente.
---

# Atendimento externo, autoatendimento e cobrança

A Forja funciona em **três contextos**, com a mesma tela:

| Contexto | Onde | Quem | O que faz |
|---|---|---|---|
| **Estação de trabalho** | Carro parado na vaga da oficina (o carro é o ponto: de qualquer lado, dentro ou fora) | Equipe da oficina | Tudo, inclusive modificações (visual, performance, stance, ajuste fino) e dinamômetro |
| **Atendimento externo** | Qualquer lugar, carro **parado, desligado e vazio** | Quem tem cargo de reparo numa oficina | Inspecionar, reparar e trocar peça. **Sem modificação e sem trabalho embaixo do carro** (isso precisa do elevador) |
| **Autoatendimento** | Locais que o dono liga | Qualquer jogador, no **próprio** carro | Só o que o dono liberar, sempre com as **próprias peças**. Nunca lataria nem pintura |

## Atendimento externo

* **Abrir:** `/tablet` (comando configurável em `Config.Service.command`) perto do carro, ou mirar no carro (ALT) e escolher **Atender veículo**.
* **Condições** (o servidor confere): carro parado, motor desligado, ninguém dentro, a até `Config.Service.field.reach` metros. Se o carro é de outro jogador **online**, o dono recebe um pedido de autorização (`ownerConsent`). Carro sem dono online (abandonado, de NPC) vale sem autorização (`unownedAllowed`).
* O carro fica **parado** enquanto a tela está aberta. A câmera é orbital: arraste o fundo para girar, a roda do mouse aproxima.
* **Inspeção:** um botão, uma barra de progresso. Os marcadores no carro mostram o estado de cada parte inspecionada. Nada aparece antes da inspeção.
* **Tela:** estado geral por grupo, **itens que você tem** (kits e peças do inventário) e a **lista de problemas**. Clicar num problema mostra as ações: **Usar kit**, **Trocar agora** ou **Pôr na ordem**.
* Cada ação é **uma barra com a animação certa**, no carro: o capô e as portas abrem e a ferramenta fica na mão. A **marca no chão** aparece ao lado da peça, na distância certa para a animação: você leva o personagem até ela e aperta **E** (uma vez por ação) e o personagem se vira para a peça.

## Peças e kit de reparo

* A **peça é item**: para trocar é preciso tê-la. Na estação, vem do **estoque da oficina**; no atendimento externo e no autoatendimento, do **inventário de quem trabalha**. Sem a peça o botão diz o que falta (antes de começar a animação).
* O **kit de reparo** só conserta **motor, bateria e pneus**, até um teto (nunca substitui a oficina). **Lataria, portas, vidros, faróis e para-choques exigem mecânico** e peça (`Config.Service.mechanicOnly`).

## Autoatendimento

Desligado por padrão. Para ligar, em `Config.Service.selfService`:

```lua
selfService = {
	enabled = true,
	locations = { { shop = 1, x = 123.0, y = 456.0, z = 30.0, radius = 4.0 } },  -- /forja_selfpoint <id da oficina> imprime a linha
	fee = { flat = 50, laborPercent = 10 },   -- taxa: valor fixo + % da mão de obra; vai para o caixa da oficina do local
}
```

O jogador abre pelo ponto, só no **próprio** carro, executa com as **peças que carrega** e **paga a taxa** para concluir. Auditado (quem, qual carro, quanto).

## Cobrança pelo ID

Não há aprovação antes do serviço. O mecânico monta a ordem, executa, abre a aba **Serviço**, **digita o ID do cliente** e clica em **Cobrar cliente**. O cliente recebe o pedido de pagamento; **aceitou e tem dinheiro**, a ordem é finalizada (caixa da oficina, comissão do mecânico, garantia). Recusou ou sem saldo: a ordem continua aberta para cobrar de novo. O cliente precisa estar a até 25 m do mecânico.
