---
description: Soluções rápidas para o que mais aparece no suporte.
---

# Problemas comuns

**Avisos de configuração no console.** Ao iniciar, a oficina confere o `config.lua` (bancadas repetidas, tipo que não existe, item sem definição, forma de cobrança inválida) e avisa o que está errado, com o caminho exato.

**A aba Skins não aparece.** O pacote não está ligado ou não tem skins para a arma da mão. Rode `workshop_skins` no
console: ele diz quantas skins a oficina encontrou. Confira `ensure one_skins_v1` antes de `ensure one_workshop` e o
`Config.Skins.packs`.

**A skin aparece na lista mas não muda a arma.** A definição da arma no servidor não lista a skin. Rode o mesclador
de novo depois de instalar ou atualizar armas, reinicie o servidor e **reconecte**.

**"Essa arma não está no seu inventário" ao aplicar.** A arma da mão não veio do inventário (foi dada por comando de
admin, por exemplo). Pegue a arma pelo inventário.

**A opção de gemas não aparece.** A base não tem gemas que a oficina reconheça. Use `Config.Gems.provider = 'item'`
ou `'custom'` (veja [Cobrança](cobranca.md)).

**"Alguém já está usando esta bancada."** A bancada atende uma pessoa por vez. Ela libera quando a pessoa sai, cai do
servidor ou depois de 30 minutos.

**Os itens aparecem sem imagem.** Copie `one_workshop/images/*.png` para a pasta de imagens do seu inventário (veja
[Instalação](instalacao.md)). No one\_inventory isso é automático.

**"Você não pode usar esta bancada."** O tipo da bancada exige emprego ou facção (`groups` no tipo ou na bancada).

**Logs não chegam no Discord.** Confira a convar `one_workshop:webhook` no `server.cfg` e se o evento está ligado em
`Config.Logs`.

**A câmera da bancada não pega a manta inteira.** Ajuste `Config.Mat.center` (centro da manta em relação ao tampo) e
`Config.Camera.height`. O scroll do mouse também aproxima e afasta.

**Acessório não aparece na arma.** A arma precisa aceitar aquele componente (o jogo decide). Para armas addon, liste
os componentes em `Config.ExtraComponents`.
