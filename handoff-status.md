# Entregas TPT2

Última revisão avaliada: **REV-20261115-05**.

| Módulo | Validação local | Estado |
| --- | --- | --- |
| `Auto_Mine.tpt2` | 37 ações, leitura do pacote no editor | Candidato experimental publicado; exige intervalo de abas confirmado |
| `Read_Machines.tpt2` | 11 ações, leitura do pacote no editor | Candidato experimental publicado; lê nove máquinas |
| `Check_Lock.tpt2` | 34 ações, leitura do pacote no editor | Pendente: reutilizar o tier do snapshot validado |
| `Find_Min_Tier.tpt2` | 29 ações, leitura do pacote no editor | Pendente: identificar e selecionar candidato único sem consultar custos |
| `Tie_Break_A.tpt2` | 31 ações, leitura do pacote no editor | Comparação de custos deve rodar apenas quando houver empate |
| `Tie_Break_B.tpt2` | 32 ações, leitura do pacote no editor | Comparação de custos deve rodar apenas quando houver empate |

A simulação do seletor confirmou que custo ausente de tier superior não bloqueia, que zero válido desempata e que custo ausente em empate bloqueia. Também reproduziu seleção bloqueada com candidato único sem custo e destino T1 quando a leitura ao vivo diverge do snapshot.

O código da revisão 05 permanece em revisão local. A execução no jogo v1.0.16, o tier do Belt, o planejador de receitas/custos, a ligação ao Master e a duração da janela da Torre estão pendentes.

A confirmação `TPT2_ACK` foi preparada para o documento TPT2_Master_Sync.
