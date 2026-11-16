# Refiner T5 → T6

O pacote experimental faz uma única receita com o inventário atual. Habilite Run e Stop. Na Factory, **J** inicia a passada e **F** solicita parada. Um lote já despachado pode terminar. No teste com J e F praticamente simultâneos, o despacho ainda ocorreu. A parada no mesmo frame precisa de correção antes da integração.

O teste de 16/11/2026 leu cinco máquinas T5: Assembly, Refiner, Cutter, Shaper e Boiler. Oven, Crusher, Presser e Mixer estavam em T6. Belt T6 foi confirmado na interface. O Refiner era o único candidato cujo déficit podia ser coberto sem minério novo. Estoque inicial relevante: 4 Dense Plate T6, 16 Motor T6, 5 Pump T6, 2 Ring T6, 31 Rod T6 e 15 Advanced Chip.

1. J despachou 1 Rod T6 no Shaper T5 e confirmou Ring T6 2 → 3, com Rod 31 → 30.
2. O operador moveu o Refiner T5 ao inventário e pressionou J novamente.
3. A IA fabricou o Refiner T6. O jogo entregou a máquina no inventário, com o slot vazio.
4. O operador instalou o Refiner na interface. O painel mostrou T6, e J confirmou `ref6_state=2` sem outro despacho.

O pacote compilou com 35 e 3 ações. A peça T5 já disponível no inventário permite seguir da produção para a bancada na mesma passada. O operador pode usar o pacote com a grade de crafting exibindo uma receita. O teste preservou o arranjo da grade que já estava visível.

| Estado | Significado |
| --- | --- |
| 1 | Passada em execução |
| 2 | Refiner T6 confirmado no slot |
| 3 | Parada solicitada |
| 4 | Factory fechou durante a passada |
| 5 | Pré-condição ausente ou produção/fabricação sem confirmação |
| 7 | Colocar Refiner T5 no inventário |
| 8 | Instalar Refiner T6 do inventário |

Próximo candidato no estoque após o teste: Shaper T6, com déficit de 4 Plate T6. A decisão foi feita a partir da leitura do estoque. A seleção automática de candidatos pelo Master, a movimentação de máquinas e a integração Mine/Factory/Torre seguem pendentes.
