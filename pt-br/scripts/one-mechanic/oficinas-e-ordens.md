---
description: Oficinas de jogador ou de emprego, equipe, pontos de trabalho e ordens de serviço.
---

# Oficinas e ordens de serviço

## Oficinas

Uma oficina tem **dono** (um personagem ou um emprego), **tipo** (o que ela oferece), **equipe**, **pontos de trabalho**, **caixa** e **reputação**
(média das avaliações dos clientes).

| Tipo | Para quê |
|---|---|
| `official` | Oficina oficial: vistoria, dinamômetro, garantia maior |
| `player` | Oficina de jogador comum |
| `tuner` | Preparadora: dinamômetro e corridas |
| `bodyshop` | Funilaria e pintura |
| `clandestine` | Sem registro: aceita peça pirata e serviços fora da lei, sem garantia |
| `police` | Garagem da polícia: serviços de graça |
| `selfservice` | Autoatendimento |
| `scrapyard` | Ferro-velho e desmanche |

Crie tipos novos com `Forja.ShopType`. Cada tipo escolhe módulos, regras de preço, serviços ilegais aceitos e garantia.

## Cargos

Aprendiz, mecânico, chefe e dono (padrão); crie os seus com `Forja.Role`. Em oficina de **emprego** o cargo vem do grau do jogador no emprego
(`Config.Shops.gradeRoles`). Cada cargo tem permissões (`repair`, `tune`, `custom`, `diagnose`, `orders`, `discount`, `stock`, `staff`, `finance`, `points`)
e um limite de desconto. Ninguém dá um cargo acima do próprio.

## Duas estações

* **Estação de trabalho:** a vaga do elevador. O carro parado na vaga é o ponto de interação (de qualquer lado, dentro ou fora). A câmera enquadra o carro com os passos Veículo, Tuning, Visual e Serviço. Cada serviço é **uma ação**: a marca aparece no chão ao lado da peça, você leva o personagem e aperta E; então barra de progresso e animação no carro, com o elevador na altura da zona.
* **Estação de gestão:** o app do dono, com navegação lateral: visão geral (caixa, avaliação, equipe, reclamações), equipe, estoque, fornecedor, fabricação, frotas, garantia e estações. Clientes compram peças aqui.

O dono cria as estações pelo painel com o **laser da câmera**:
E salva, as setas giram, a roda do mouse muda o raio, Backspace cancela. O servidor recusa pontos a mais de 60 m do jogador.

## Ordem de serviço

1. O mecânico abre o terminal do carro e monta a ordem (troca de peça, serviço, item avulso, peça de desempenho, visual).
2. O **servidor calcula o preço**: peça mais margem da oficina, mão de obra, ajustados pelo preset.
3. Quem tem a permissão aplica **desconto** até o limite do cargo.
4. O mecânico **executa** cada item (ou **Executar tudo**). A peça sai do estoque da oficina; sem estoque, o botão avisa antes da animação.
5. Com tudo executado, o mecânico **digita o ID do cliente e cobra**. O cliente recebe o pedido de pagamento e, se aceitar e tiver dinheiro, a ordem é finalizada.
6. A **comissão** do mecânico é paga na hora se ele estiver online; se não, o valor fica no caixa.
7. A ordem concluída gera **garantia** (dias e km do tipo da oficina), entra na caderneta do carro e o cliente **avalia** a oficina.

Nada de customização fica no carro antes da cobrança: executar só mostra, cancelar a ordem devolve o carro como entrou.

## Garantia e disputa

Ordens concluídas têm garantia (dias e km do tipo da oficina). Dentro dela, o cliente, perto do carro, usa `/garantia <o que aconteceu>` e a reclamação chega à aba **Garantia** da estação de gestão. O dono escolhe:

* **Refazer grátis:** abre uma ordem nova do carro com 100% de desconto (feche antes qualquer ordem aberta do mesmo carro).
* **Reembolsar:** devolve ao cliente a fração `Config.Shops.claimRefund` (50% por padrão) do total da ordem, paga pelo caixa da oficina.
* **Recusar:** encerra a reclamação.

O cliente é avisado em todos os casos e a auditoria registra a decisão. Outros comandos de jogador: `/ranking [classe]` (melhores passadas do dinamômetro) e `/pericias` (suas perícias e licenças).

## Comandos de administração

```
/forja_shop list
/forja_shop create <tipo> <char|job> <dono> <nome>
/forja_shop panel <id>
/forja_shop delete <id>
/forja_license grant|revoke <id do jogador> <licença> [dias]
```
