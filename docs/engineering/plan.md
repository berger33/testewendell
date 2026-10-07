# Plano de engenharia

## Visão

Simulador 2D de fazenda e comunidade para Android, voltado a adultos. O ciclo é acordar, planejar tempo e energia, cuidar da propriedade, explorar, conversar, cumprir encomendas fictícias, melhorar a fazenda e dormir. O jogo deve ter identidade original: cores vivas, formas legíveis e animações expressivas. Referências de gênero e estilo não autorizam copiar obras existentes.

## Decisões iniciais

- Motor: Godot 4 estável, GDScript, 2D, renderizador Compatibility.
- Primeiro lançamento: um jogador, offline, idioma português brasileiro, orientação paisagem.
- Meta inicial de desempenho: 60 FPS em aparelho intermediário e 30 FPS sustentados em aparelho de entrada; medir em aparelhos reais antes de prometer suporte.
- Salvamento local versionado, atômico e com recuperação. Sem conta ou telemetria na primeira versão.
- Arte, áudio e texto originais, com licença e autoria registradas.
- Cannabis é um elemento ficcional e abstrato do jogo, sem instruções reais de cultivo, compra, entrega ou consumo por menores.
- A classificação etária final depende do questionário IARC e das autoridades regionais. Revisar políticas da loja antes de publicar.

## Matriz de mecânicas e cobertura

| ID | Sistema | Escopo funcional | Fatias |
|---|---|---|---|
| M01 | Movimento | toque, colisão, câmera, transições de cena | F01, F09 |
| M02 | Dia | relógio, energia, sono, calendário | F02, F08 |
| M03 | Terreno | limpeza, preparo e ferramentas | F03 |
| M04 | Cultivos | plantio abstrato, cuidado, crescimento, colheita e qualidade | F04, F14 |
| M05 | Inventário | pilhas, ferramentas, baú, limites, descarte | F05 |
| M06 | Economia | moedas fictícias, encomendas, mercado interno, melhorias | F06, F14 |
| M07 | Persistência | salvar, carregar, migração e recuperação | F07 |
| M08 | Mundo | estações, clima, mapas, coleta e exploração | F08, F09, F12 |
| M09 | Comunidade | agendas, diálogos, amizade, presentes, eventos e festivais | F09, F10, F14 |
| M10 | Animais | abrigo, rotina, bem-estar, vínculo e produtos | F11, F14 |
| M11 | Atividades | coleta, pesca, mineração ou equivalente temático | F12 |
| M12 | Progressão | construção, receitas, coleção, conquistas e missões | F13, F14 |
| M13 | Apresentação | tutorial, mapa, diário, arte, áudio e acessibilidade | F15 |
| M14 | Android | toque, pausa, proporções, desempenho, empacotamento | F01 a F16 |

O termo “todas as mecânicas de Harvest Moon” precisa ser fechado em uma lista de títulos de referência e em fichas próprias para cada sistema. O catálogo detalhado está em `docs/gdd/mechanics-catalog.md`. A matriz acima é a cobertura inicial do gênero, não uma alegação de equivalência a todos os jogos da franquia. Para cada Mxx, criar uma ficha com regras, dados, interface, dependências, casos extremos e testes. Marcar como concluído apenas com evidência.

## Fatias e critérios de aceite

| Fatia | Entrega testável | Próximo passo |
|---|---|---|
| F00 Fundação | plano, matriz, projeto abre, CI básico | F01 — Personagem e mapa jogável |
| F01 Personagem e mapa jogável | movimento por toque, colisão, câmera; APK em Android | F02 — Tempo, energia e dia |
| F02 Tempo, energia e dia | relógio, energia, sono, virada de dia | F03 — Terreno e ferramentas |
| F03 Terreno e ferramentas | grade interativa, limpeza, preparo e feedback | F04 — Primeiro ciclo de cultivo |
| F04 Primeiro ciclo de cultivo | plantar, cuidar, avançar dias e colher | F05 — Inventário e armazenamento |
| F05 Inventário e armazenamento | itens, pilhas, baú, sem perda ou duplicação | F06 — Economia e melhorias |
| F06 Economia e melhorias | encomendas fictícias, moeda e melhoria | F07 — Salvamento e recuperação |
| F07 Salvamento e recuperação | fechar e retomar, arquivo interrompido recuperado | F08 — Estações, clima e calendário |
| F08 Estações, clima e calendário | estação e clima alteram regras e aparência | F09 — Vila e NPCs |
| F09 Vila e NPCs | transição fazenda-vila, agenda e diálogo | F10 — Relações e eventos |
| F10 Relações e eventos | amizade, presentes, festival, evento condicional | F11 — Animais |
| F11 Animais | abrigo, cuidado, vínculo e produto | F12 — Exploração e coleta |
| F12 Exploração e coleta | mapa explorável, coleta e atividade extra | F13 — Construção e coleção |
| F13 Construção e coleção | melhoria, receita, registro de descobertas | F14 — Conteúdo e balanceamento |
| F14 Conteúdo e balanceamento | ampliar conteúdo e auditar progressão | F15 — Arte, áudio e acessibilidade |
| F15 Arte, áudio e acessibilidade | identidade original, legibilidade e opções | F16 — QA Android e publicação |
| F16 QA Android e publicação | matriz de aparelhos, estabilidade, classificação, pacote | Ciclo de atualizações pós-lançamento |

Se uma fatia exceder uma sessão ou PR revisável, dividir em Fxxa/Fxxb antes de implementar. Não avançar para conteúdo em escala enquanto o ciclo inicial não estiver jogável em Android.

## GitHub e Arena Agent Mode

1. Criar issue com objetivo, arquivos previstos, critérios de aceite, testes e próximo passo.
2. Iniciar uma sessão nova do Arena Agent Mode com GitHub ativado e este repositório selecionado.
3. Trabalhar em branch própria, abrir exatamente um PR e revisar diff e Checks.
4. Mesclar somente após evidência. Uma sessão do Arena suporta um PR; após fechar ou mesclar o PR, iniciar outra sessão para a próxima fatia.
5. Como o limite de contexto por sessão não é um orçamento numérico garantido, manter cada fatia pequena. Usar os arquivos do repositório como passagem de contexto entre sessões.

## Estratégia de teste

- **Por regra:** testes determinísticos de relógio, energia, inventário, economia, crescimento e migração de save.
- **Por cena:** importação headless, erros do Godot, navegação e estados de interface.
- **Por fatia:** roteiro manual reproduzível com capturas, vídeo curto ou logs quando útil.
- **Por build Android:** instalar APK, executar o ciclo da fatia, pausar e retomar, testar diferentes proporções, toque, memória, FPS e falhas.
- **Por lançamento:** regressão completa, acessibilidade, classificação etária, privacidade, assinatura e revisão das políticas da loja.

Prévia do Arena e CI não substituem teste em aparelho. Um resultado só é “aprovado” quando há comando ou roteiro, ambiente, resultado observado e ligação no PR.

## Riscos e decisões pendentes

- Escopo: fechar títulos de referência e priorizar variantes de mecânicas antes da produção extensa.
- Distribuição: a presença de cannabis exige revisão de políticas e classificação; aprovação na Google Play não é garantida.
- Direção visual: fazer protótipo visual original e comparar legibilidade em tela pequena, sem copiar ativos Nintendo.
- Android: escolher aparelhos de entrada e intermediários para a matriz antes de fixar requisitos mínimos.
- Economia: testar se o ciclo é divertido e equilibrado no protótipo, não apenas numericamente consistente.

## Fontes oficiais consultadas em 2026-10-07

- Arena Agent Mode e GitHub: https://help.arena.ai/articles/1655691990-how-to-use-coding-in-agent-mode
- Arena, PR e workspace: https://help.arena.ai/articles/5432423882-how-to-use-agent-mode
- Arena, limite de sessão: https://help.arena.ai/articles/3975292349-arena-troubleshooting-session-token-limits
- Godot Android: https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_android.html
- Godot renderizadores: https://docs.godotengine.org/en/stable/tutorials/rendering/renderers.html
- Google Play conteúdo: https://support.google.com/googleplay/android-developer/answer/9878810?hl=en
- Google Play classificação: https://support.google.com/googleplay/android-developer/answer/9898843?hl=en
