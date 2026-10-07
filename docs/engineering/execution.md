# Manual de execução para Arena Agent Mode

## Fonte da verdade e ordem de leitura

`README.md` → `AGENTS.md` → este manual → `plan.md` → `architecture.md` → `contracts.md` → ficha `docs/slices/Fxx.md` → código existente. Se houver conflito, a issue e a ficha da fatia aprovada prevalecem para o escopo daquela execução; registrar qualquer mudança de arquitetura em ADR antes de espalhá-la pelo projeto.

O GitHub contém o estado durável. Não depender da memória de conversas do Arena. Uma sessão do Agent Mode deve trabalhar em uma fatia, branch e PR. Não iniciar outra fatia no mesmo PR. Não mesclar o PR pela automação sem revisão humana.

## Entrada de uma sessão

1. Conectar a conta GitHub ao Arena, habilitar GitHub no Agent Mode e selecionar `berger33/testewendell`.
2. Verificar branch principal, último PR mesclado, issues abertas, estado do CI e `git status`.
3. Ler ficha da fatia. Se a predecessora não estiver mesclada, interromper implementação dependente e relatar a dependência.
4. Confirmar o menor fluxo completo demonstrável, arquivos a tocar, critérios de aceite e testes.
5. Criar branch `feat/fxx-nome-curto` a partir de `main` atualizado. Se o Arena criar branch automaticamente, registrar seu nome na ficha.

## Ciclo dentro da sessão

1. Reproduzir o estado inicial: importar Godot headless, abrir a cena, registrar falhas pré-existentes.
2. Implementar primeiro o caminho vertical mínimo: ação do jogador → regra → mudança de estado → feedback → persistência quando já existir.
3. Adicionar teste de regra para comportamento não trivial; testar entrada inválida e fronteira. Evitar testes que apenas copiem a implementação.
4. Executar importação headless e roteiro manual da ficha. Se houver Android disponível, instalar e testar o APK; se não houver, registrar pendência explícita.
5. Inspecionar diff, remover arquivos gerados, verificar licenças de recursos e atualizar a ficha com resultado real.
6. Commit, push e um PR com descrição da função, comandos executados, evidência, limites e próximo passo.

## Limite de sessão

Não há orçamento de tokens fixo assumido. Planejar uma tarefa que caiba em uma única revisão de PR. Se o contexto estiver perto do limite: parar novas funções, preservar um estado compilável, rodar testes disponíveis, escrever `HANDOFF.md` ou atualizar a ficha com arquivos alterados, comandos, resultados, lacunas e próximo passo; enviar a branch e abrir o PR. Uma nova sessão começa lendo esses arquivos. Não afirmar que um teste foi executado quando apenas foi planejado.

## Definição de pronto por fatia

- Critérios da ficha demonstrados ou marcados como pendentes com motivo.
- Projeto importa sem erro novo; CI verde.
- Testes da regra alterada passam; roteiro manual descrito com resultado observado.
- Android real validado quando a fatia exigir interação, toque, desempenho ou exportação; caso contrário, a fatia fica pendente de validação Android.
- Sem recurso protegido de terceiros, segredos, build ou cache no Git.
- Ficha atualizada e PR aberto para revisão; nome exato da próxima fatia incluído no fim.

## Formato obrigatório do PR

```text
Fatia: Fxx — nome
Issue: #n
Fluxo implementado: ação → estado → feedback
Arquivos principais:
Testes: comando, ambiente, resultado
Android: aparelho/versão/resultado ou pendente
Riscos e pendências:
Evidências: captura, vídeo, log ou link do CI
Próximo passo: Fyy — nome
```

## Falhas e escalonamento

- Erro pré-existente: registrar evidência; corrigir somente se bloquear a fatia e manter correção mínima.
- Falta de SDK, aparelho ou credencial: concluir o que for verificável e deixar portão Android aberto; não inventar resultado.
- Escopo excessivo: dividir em `Fxxa`, `Fxxb` na issue e na ficha; um PR por subdivisão.
- Mudança de conteúdo ou política de loja: registrar decisão, atualizar classificação prevista e revisar o plano antes da publicação.
- Dependência de decisão do proprietário: apresentar opção recomendada e impacto; continuar tarefas independentes.
