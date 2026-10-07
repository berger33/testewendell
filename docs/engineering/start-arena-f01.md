# Prompt de partida no Arena — F01

Depois de revisar e mesclar o PR da F00, abra **uma nova sessão no Arena Agent Mode**, conecte GitHub, selecione `berger33/testewendell` e cole o texto abaixo. Se o PR #1 ainda estiver aberto, o agente deve parar antes de implementar F01 e informar a dependência.

```text
Trabalhe no repositório GitHub berger33/testewendell, em Agent Mode. Execute apenas a issue #2: F01 — Personagem e mapa jogável. Esta sessão deve gerar uma branch e um único PR.

Primeiro, confirme que o PR #1 (F00) está mesclado em main. Leia README.md, AGENTS.md, docs/engineering/execution.md, docs/engineering/plan.md, docs/gdd/mechanics-catalog.md, docs/engineering/architecture.md, docs/engineering/contracts.md, docs/qa/test-plan.md e docs/slices/F01.md. Confira o estado real do repositório e dos Checks. Se F00 não estiver mesclada, não comece código dependente: informe o bloqueio.

Implemente um primeiro fluxo jogável pequeno: personagem original andando por toque em uma fazenda pequena, colisões, câmera e interface legível em tela Android. Preserve a cena inicial e adapte-a ao jogo. Não implemente cultivo, inventário, economia ou NPCs nesta sessão. Use arte provisória original, sem copiar ativos de Harvest Moon ou Mario.

Valide importação headless e os critérios de F01. Se houver SDK e aparelho Android acessíveis, exporte APK de desenvolvimento, instale, jogue e registre modelo, versão Android, FPS observado e evidência. Se não houver aparelho, marque exatamente essa validação como pendente; não a simule nem declare aprovação. Revise o diff, remova arquivos gerados e atualize docs/slices/F01.md com resultado, comandos e pendências. Siga docs/engineering/execution.md para commit, push e PR.

No relatório final entregue URL do PR, fluxo demonstrado, testes executados, limites e esta linha exata: Próximo passo: F02 — Tempo, energia e dia.
```
