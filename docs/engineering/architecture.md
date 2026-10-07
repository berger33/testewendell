# Arquitetura inicial

## Princípios

- Separar definições de conteúdo (`game/data`) de estado salvo.
- Manter regras de tempo, inventário, economia e crescimento em serviços testáveis sem cenas.
- Cenas apresentam dados e capturam ações; não são a única fonte das regras.
- Usar identificadores estáveis para itens, NPCs, mapas e eventos.
- Versionar formato de save desde a primeira implementação; escrever em arquivo temporário, validar e substituir com recuperação.
- Carregar apenas mapas e recursos necessários à cena atual para preservar memória no Android.

## Domínios previstos

`world`: tempo, estações, clima, mapas e transições.  
`farm`: terreno, ferramentas, cultivos e animais.  
`player`: energia, inventário, progresso e opções.  
`community`: NPCs, agendas, diálogos, vínculos e eventos.  
`economy`: moedas fictícias, encomendas, preços e melhorias.  
`persistence`: save versionado, migração, recuperação.  
`ui`: toque, HUD, menus, diário, tutorial e acessibilidade.

## Dados e contratos

Usar arquivos de conteúdo legíveis e validados na CI. Cada ação importante deve ter pré-condição, mudança de estado e resultado de interface definidos. Aleatoriedade de clima, eventos e recompensas deve aceitar uma semente nos testes. Registrar ADR para mudança de motor, formato de save, orientação, resolução base ou estratégia de renderização.

## Qualidade

Critérios obrigatórios em PR: escopo rastreado à issue, importação sem erro, testes da regra alterada, roteiro manual da fatia, evidência Android quando a fatia mexer em interação ou exportação, diff revisado e ficha da fatia atualizada.
