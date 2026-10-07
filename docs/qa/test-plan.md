# Plano de testes e evidências

## Níveis

1. **Importação e lint:** Godot headless sem erro; validar referências de cenas e dados. Rodar em todo PR.
2. **Regras:** testes determinísticos de tempo, energia, ação em tile, inventário, transação, NPC, evento e save; incluir sucesso, falha e fronteira.
3. **Integração:** jogar o caminho da fatia do início ao fim; repetir após salvar/carregar e trocar de cena.
4. **Android:** instalar build no aparelho, testar toque, pausa/retomada, proporção, FPS e memória; registrar aparelho e Android.
5. **Regressão:** repetir ciclos anteriores depois de alterar contratos compartilhados.

## Modelo de evidência por fatia

```text
Fatia/commit/PR:
Ambiente: Godot, sistema operacional, aparelho Android, versão Android
Comandos executados e saída resumida:
Roteiro manual: passos numerados
Esperado / observado:
Captura, vídeo ou log:
Defeitos e severidade:
Resultado: aprovado / pendente / reprovado
```

Guardar registros em `docs/qa/runs/Fxx-AAAA-MM-DD.md`. Anexar mídia pequena ao PR ou a release de teste; não colocar vídeos grandes no histórico Git. Resultados do Arena são apoio, nunca substituto da execução em aparelho.

## Matriz Android mínima

Definir aparelhos reais antes da F01. Cobrir ao menos um aparelho de entrada e um intermediário, duas proporções de tela, uma versão Android mais antiga dentro do alvo e uma atual. Para cada um: instalação, primeira execução, toque, rotação se permitida, bloqueio/desbloqueio, alternância de aplicativo, salvar, reabrir, desempenho por 15 minutos e saída limpa. Registar números medidos; não usar “roda bem” como evidência.

## Critério de defeitos

- **Bloqueador:** crash, perda/corrupção de save, progressão impossível, ação essencial sem resposta.
- **Alto:** duplicação de itens/moeda, NPC/evento inacessível, toque impreciso que impede jogar, FPS abaixo do alvo sustentado.
- **Médio:** texto cortado, animação incorreta, feedback ambíguo, desequilíbrio localizado.
- **Baixo:** polimento visual ou sonoro sem impacto funcional.

Bloqueadores e defeitos altos impedem mesclar uma fatia que os introduziu. Falhas pré-existentes devem ser ligadas a uma issue e não escondidas no relatório.
