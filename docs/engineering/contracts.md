# Contratos de jogo e dados

Estes contratos orientam a implementação. Nomes de classes e arquivos podem mudar por ADR, mas invariantes e responsabilidades devem permanecer verificáveis.

## Tempo e simulação

- Um único `GameClock` possui dia, hora, estação e estado `running/paused/transitioning`.
- Tempo de jogo avança por atualização controlada; menus, pausa do Android e transição de cena não avançam tempo indevidamente.
- Ao dormir: validar ação → resolver efeitos do fim do dia em ordem estável → incrementar calendário → atualizar mundo → salvar → exibir manhã.
- Toda regra diária recebe estado e semente controlável para teste. Não usar relógio do sistema como fonte de gameplay.

## Ações e recursos

- Ação em tile: validar alcance, alvo, ferramenta, energia e estado; aplicar uma única mutação; emitir resultado e feedback.
- Ação inválida não consome energia nem duplica item. Uma interação por toque não pode ser aplicada duas vezes por engano.
- IDs de itens e conteúdo são estáveis e únicos. Quantidades nunca negativas; transferências entre inventário e baú conservam a soma.
- Definições de culturas são valores fictícios de gameplay. Não registrar parâmetros ou instruções de cultivo real.

## Economia

- Transação é atômica: validar preço e estoque → debitar/creditar moeda fictícia → mover item → emitir resultado.
- Nenhuma ação pode criar moeda ou itens por repetição de toque, tela ou carregamento.
- Preços, custos, duração e recompensas ficam em dados versionados, com simulação de balanceamento.
- Mercado e encomendas são inteiramente internos ao jogo; nunca oferecer contato, pedido ou entrega de produtos reais.

## NPCs e eventos

- Agenda define local e comportamento por faixa de tempo, com fallback para evento ou local indisponível.
- Diálogo e relação dependem de flags explícitas; presente só é consumido após aceitação válida.
- Eventos são idempotentes por ID e dia: não disparam duas vezes ao carregar, trocar de cena ou pausar.
- Personagens ligados ao tema adulto devem ser inequivocamente adultos.

## Save

- `schema_version` obrigatório. Conteúdo inclui player, mundo, fazenda, inventários, economia, NPCs, missões e opções necessárias.
- Salvar em `user://` por arquivo temporário, validar e substituir; manter recuperação do último estado íntegro.
- Migração de versão é explícita, testada com fixtures e nunca apaga silenciosamente dados desconhecidos.
- Falha de leitura mostra mensagem recuperável; não iniciar jogo novo por cima de save inválido sem escolha do usuário.

## Interface e Android

- Alvos de toque confortáveis, feedback imediato, área segura, texto legível e escalonamento em 16:9 e telas mais altas.
- Pausa e perda de foco não executam ação de jogo nem corrompem save. Retomada preserva estado e áudio coerentes.
- A tela não deve depender de hover, teclado ou conexão de rede.

## Testes de contrato

Para cada sistema, cobrir pelo menos: caminho feliz, recurso insuficiente, ação repetida, fronteira temporal, salvar/carregar e interação entre sistemas. Registrar testes sob `tests/` e roteiros manuais sob `docs/qa/`.
