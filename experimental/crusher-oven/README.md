# Crusher → Oven

Teste de um lote T1 no TPT2 v1.0.16. Importe o pacote na Facility AI e habilite os dois scripts TPT2Smelt. Abra a Factory e pressione **7**. O script espera quatro segundos, verifica se as máquinas estão ociosas e despacha 1 Ore T1. Só envia Dust ao Oven após confirmar o consumo de 1 Ore e a entrada de 2 Dust T1. Confirma Ingot comparando o estoque final com a leitura inicial. Pressione **F** para interromper o script. Uma operação já entregue à máquina pode terminar.

Resultado observado em 16/11/2026:

| Estoque T1 | Inicial | Após Crusher | Final |
| --- | ---: | ---: | ---: |
| Ore | 56622 | 56621 | 56621 |
| Dust | 2 | 4 | 2 |
| Ingot | 120 | — | 122 |

O overlay mostrou `sm_state=6` com a lista de scripts ativos vazia. Na repetição, F antes do despacho mudou o estado para 5, encerrou o script e preservou o estoque. Run compilou com 35 ações e Stop com 3. O teste usa T1 fixo, pressupõe acesso exclusivo ao Crusher e Oven e termina após um lote. A integração ao Master, seleção de tier pelo planejador e fabricação de peças ainda precisam ser feitas.
