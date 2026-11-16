# Shaper T5 → T6

Este pacote executa uma passada do Shaper T6 usando o inventário real. Ele depende do pacote [TPT2Refine](../refine-deficit), incluindo Master, Oven, Crusher e Stop habilitados. Na Factory, **L** inicia a passada e **F** solicita parada. Um lote já despachado pode terminar.

A passada reserva 3 Screw, 3 Block, 2 Motor e 2 Insulated Cable do tier T6. Calcula quantas unidades faltam para 4 Plate T6, usa os lingotes disponíveis e solicita ao Master apenas a meta necessária. Aguarda confirmação do refino, produz o déficit de placas no Presser e confere a receita novamente antes de fabricar. Quando o Shaper T5 ainda está instalado, a passada termina em estado 7. Coloque a máquina T5 no inventário e pressione L para retomar. O estado 8 sinaliza Shaper T6 no inventário. Instale-o na Factory e pressione L para confirmar o tier pelo jogo.

| Estado | Significado |
| --- | --- |
| 1 | Passada em execução |
| 2 | Shaper T6 confirmado no slot |
| 3 | Parada por F |
| 4 | Factory fechada durante a passada |
| 5 | Pré-condição ausente ou lote não confirmado |
| 7 | Colocar Shaper T5 no inventário |
| 8 | Instalar Shaper T6 do inventário |

## Resultado no TPT2 v1.0.16

- L seguido de F encerrou a tentativa anterior ao primeiro despacho, com estado 3 e 5 Ore T6 preservados.
- Na execução normal, 2 Ore T6 (5 → 3) produziram 4 Dust T6 e 4 Ingots T6 (0 → 4) em quatro operações confirmadas pelo Master. O Presser produziu 4 Plate T6. Com o Shaper T5 previamente movido ao inventário, a IA fabricou o Shaper T6 e retornou estado 8.
- A instalação foi feita pela interface do jogo. O painel mostrou Shaper T6 e a repetição de L confirmou o estado 2, sem script ativo ao final.
- Os scripts passaram pela compilação e leitura de volta, com 36, 26 e 4 ações.

A integração ao seletor e o caminho de recuperação por Mixer seguem pendentes.
