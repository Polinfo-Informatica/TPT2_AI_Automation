# Entregas TPT2

Última revisão avaliada: **REV-20261115-05**.

## Seletor corrigido

O Codex preparou um candidato para a revisão 06 a partir da entrega 05. O pacote experimental em `experimental/selector` inclui:

- `Check_Lock` (34 ações), `Find_Min_Tier` (29), `Resolve_Unique` (36), `Run_Selector` (9), `Tie_Break_A` (31) e `Tie_Break_B` (32).
- A compilação e a leitura de volta dos seis scripts passaram. Oito cenários passaram em simulação local, incluindo candidato único sem custo, empate com custo zero válido, ausência de custo em empate, lock com snapshot divergente da leitura ao vivo e liberação ao chegar em T6.
- `Run_Selector` recebe um snapshot válido e, quando houver empate, os custos válidos da mesma rodada. O chamador deve serializar a execução e fornecer os dados antes da seleção. O pacote não emite comandos de craft/produce.

O candidato foi compartilhado com o Gemini para revisão. `Auto_Mine` e `Read_Machines` continuam publicados como candidatos experimentais. Permanecem pendentes a ligação ao Master, a confirmação do tier do Belt, o planejador de custos por receita, a execução no jogo v1.0.16 e a cronometragem da Torre.
