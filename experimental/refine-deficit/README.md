# Refino por déficit

O Master executa uma solicitação de estoque de Ingot em um tier de T1 a T6. O chamador informa `rf_tier` e `rf_goal` (estoque total desejado, em unidades inteiras), zera `rf_batches`, reserva o estado com `rf_state=1` e inicia `TPT2Refine:Master` uma única vez com a Factory aberta. Preserve tier e meta enquanto o estado for 1. O planejador de upgrades ainda precisa fornecer essa solicitação a partir da receita e das reservas do alvo.

O Master usa primeiro Dust disponível, envia uma unidade de Ore ao Crusher se precisar de Dust e só continua após a confirmação pelo estoque. O acesso concorrente aos mesmos itens/máquinas pode invalidar a confirmação. O protótipo prevê um Ingot por Dust, confirmado nesta execução em T2 e no teste anterior em T1. O caminho com Mixer e ordens de produção maiores podem ser incorporados depois da verificação dos rendimentos por tier.

Estados de `rf_state`:

| Valor | Resultado |
| --- | --- |
| 1 | Solicitação ativa |
| 2 | Meta de estoque atingida |
| 3 | Parada por F |
| 4 | Parâmetro inválido ou Factory fechada |
| 5 | Máquina ocupada/inadequada ou falta de insumo |
| 6 | Operação não confirmada no tempo limite |

## Teste no jogo

Importe e habilite os seis scripts. Na Factory, **6** define a meta igual ao estoque T2 e testa zero despachos. **5** solicita dois Ingots T2 acima do estoque atual, com três segundos de espera antes de chamar o Master. **F** interrompe o teste, o Master e seus workers. Um lote entregue à máquina pode terminar após a parada. As duas teclas numéricas são apenas pontos de entrada do pacote de teste.

No TPT2 v1.0.16 em 16/11/2026, **6** registrou 90 → 90 Ingots T2 e zero despachos. **5** registrou 90 → 92 e dois passos confirmados (Crusher e Oven), com Ore T2 4311 → 4310. **5** seguido de **F** antes do despacho registrou estado 3 e zero despachos. Não havia scripts ativos ao final de cada cenário. Os seis scripts compilaram com 6 a 36 ações e passaram pela leitura de volta no d0sboots.
