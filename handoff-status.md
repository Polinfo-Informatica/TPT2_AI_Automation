# Entregas TPT2

Última revisão avaliada: **REV-20261115-07**.

## Seletor corrigido

O Codex preparou um candidato para a revisão 06 a partir da entrega 05. O pacote experimental em `experimental/selector` inclui:

- `Check_Lock` (34 ações), `Find_Min_Tier` (29), `Resolve_Unique` (36), `Run_Selector` (9), `Tie_Break_A` (31) e `Tie_Break_B` (32).
- A compilação e a leitura de volta dos seis scripts passaram. Oito cenários passaram em simulação local, incluindo candidato único sem custo, empate com custo zero válido, ausência de custo em empate, lock com snapshot divergente da leitura ao vivo e liberação ao chegar em T6.
- `Run_Selector` recebe um snapshot válido e, quando houver empate, os custos válidos da mesma rodada. O chamador deve serializar a execução e fornecer os dados antes da seleção. O pacote não emite comandos de craft/produce.

O candidato foi compartilhado com o Gemini para revisão. `Auto_Mine` e `Read_Machines` continuam publicados como candidatos experimentais. Permanecem pendentes a ligação ao Master, a confirmação do tier do Belt, o planejador de custos por receita, a execução no jogo v1.0.16 e a cronometragem da Torre.

## Execução do seletor no jogo

Em 15/11/2026, o pacote isolado `TPT2QA` foi importado e executado no TPT2 v1.0.16. Resultado no overlay: `qa_done=8`, `qa_pass=8`, `qa_mask=255`. As entradas de tiers e custos foram controladas pelos casos. Integração com a Factory, atuação do Master e consumo de materiais seguem pendentes. O [pacote de teste](experimental/selector-qa/selector-qa-import.txt) pode ser executado pela tecla **9** com os 16 scripts habilitados.

## REV-20261115-07 — Phase 3a

**Resultado:** revisão estática concluída com bloqueios. O Google Doc contém as cinco fontes (`Toggle_F`, `Plan_Costs`, `Factory_Batch_A`, `Factory_Batch_B`, `Master`) e o `TPT2_ACK` foi confirmado por leitura. Os workers de Mine, leitura de máquinas e seleção são dependências da branch.

- `Read_Machines` publica `read_done` e nove tiers. `Master` não define `snap_valid` nem fornece um tier confirmado para o Belt. `Check_Lock` exige ambos antes de selecionar.
- `Plan_Costs` marca custos fixos da planilha como válidos. Calcular o próximo upgrade a partir das 50 receitas da branch, com rendimento, tier, estoque, reservas, itens em processamento e pesos de insumos-base. O mapa de chips muda conforme a receita. Assembly T3 usa Basic Chip e T6 usa Advanced Chip.
- `Factory_Batch_A/B` usam metas genéricas de estoque e rotas incompatíveis para Rubber no Oven e no Cutter segundo a referência da branch. Faltam caminhos para componentes exigidos como Dense Plate, Pipe e Rubber Plate. `Factory_Batch_B` tenta o upgrade sem confirmar os insumos e seta `batch_state = 2` sem verificar aceitação ou tier instalado.
- `Master` ignora `mine_state = 4` (configuração ausente) e ainda não calcula a janela da Torre. O primeiro passo é isolar e confirmar um lote Ore → Dust no Crusher com leitura de estoque e parada por F.

**Testes pendentes:** compilação e leitura de volta no compilador d0sboots no PC do projeto, despacho e confirmação de lote, troca da máquina e progressão com lock até T6, Belt, esgotamento da Mine, parada por F e tempo da janela da Torre. O PC e o chat local do Gemini estiveram indisponíveis nesta checagem.

## 16/11/2026 — primeiro lote real

As cinco fontes da revisão 07 compilam (18, 20, 26, 44 e 23 ações, na ordem do Docs) e passaram pela leitura de volta no d0sboots. Os bloqueios de integração da revisão 07 continuam.

O [pacote isolado do Crusher](experimental/crusher-batch) compilou, foi importado e executado no TPT2 v1.0.16. No Crusher T6, 1 Ore T1 virou 2 Dust T1. A parada por F antes do despacho seguinte encerrou o script sem consumir minério. Interromper um worker executado por `executesync` deixou o chamador preso no primeiro teste; a versão aprovada executa o lote diretamente.

Próxima etapa: ligar Crusher → Oven, confirmar Ingot via inventário e integrar ao Master com parada limpa. O teste do Crusher não instala máquinas.
