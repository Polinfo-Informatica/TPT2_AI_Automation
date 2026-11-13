# Status do projeto

**13/11/2026.** A [suíte de produção](tpt2_production_suite.txt) registra os dez scripts exportados do editor d0sboots 2.07, com alvo de jogo v1.0.12. A compilação e a leitura de volta pelo importador do editor passaram para os dez scripts. A execução em um save do jogo e a progressão completa ainda precisam de validação.

## Coordenação

`Toggle_F` usa a tecla **F** e a variável global `active`. Ao ligar, inicia `Master`. Ao desligar, para `Master` e os oito scripts de trabalho. `Master` fecha a Factory, abre a Mine e dá até 1,5 s a `Auto_Mine`. Depois fecha a Mine, abre a Factory, inicia os sete scripts da Factory com `execute` e aguarda 45 s. No próximo ciclo, para esses scripts antes de voltar à Mine. O controlador usa tempos fixos e não aguarda confirmação de camada, estoque ou conclusão de receita.

| Script | Ações compiladas | Comportamento no código exportado |
| --- | ---: | --- |
| `Toggle_F` | 14 | Liga e desliga a suíte com F. No editor, a aba se chama `Starter_F`. |
| `Master` | 23 | Alterna Mine e Factory e inicia os scripts de cada fase. |
| `Auto_Mine` | 8 | Tenta abrir uma camada e escava a grade 4 × 4 da aba selecionada. No editor, a aba se chama `Auto_MIne`. |
| `Auto_Shop` | 11 | Faz uma rodada de chamadas `craft` T1 em lotes de 50 a 200. |
| `Auto_Base` | 15 | Repete tentativas de produção de insumos de T1 a T5, incluindo ore no Crusher. |
| `Auto_Parts` | 13 | Tenta alimentar Mixer, Oven e Cutter e fabricar componentes de T1 a T5. |
| `Auto_Up1` | 9 | Tenta fabricar Oven, Presser, Assembler, Refinery e Crusher de T2 a T5. |
| `Auto_Up2` | 9 | Tenta fabricar Cutter, Mixer, Shaper, Boiler e Transport Belt de T2 a T5. |
| `Auto_Prod1` | 12 | Tenta fabricar oito tipos de produtores regulares de T1 a T5, em lotes de cinco. |
| `Auto_Prod2` | 11 | Tenta fabricar cinco tipos de produtores regulares, mais Gem e Exotic Gem, com o mesmo laço T1–T5 e lotes de cinco. |

## Pendências observadas no código

- **Cadeia depois do Crusher.** `Auto_Base` envia `ore` ao Oven e `dust` ao Mixer. A [referência de receitas](d0sboots_ai_reference.md) usa `dust` no Oven e `lump` no Mixer. O script fabrica lumps, mas os encaminha à Refinery. `Auto_Parts` também tenta usar `rubber` no Oven e no Cutter, enquanto a receita de `plate.rubber` usa o Presser.
- **Estoque e concorrência.** Lotes fixos podem falhar quando só existe estoque para um lote menor. Os sete scripts da Factory iniciam na mesma fase e podem disputar insumos sem checar `count` ou `active` para coordenar cada tentativa.
- **Shop e refino.** `Auto_Shop` usa fabricação e não aciona compras na interface. A suíte não inicia o refino de shards em minério. `Auto_Mine` opera na aba selecionada e não percorre as outras abas.
- **Progressão.** `Auto_Up1` e `Auto_Up2` começam em T2 e terminam em T5. Faltam a fabricação inicial de máquinas T1 e a progressão T6–T10. A suíte pressupõe os slots de máquinas já instalados para a substituição automática pelo jogo.
- **Produtores especiais.** Gem e Exotic Gem têm receita T1 no [catálogo de Factory Automation](https://github.com/d0sboots/PerfectTower/blob/main/factory/factory_constants.tpt2). `Auto_Prod2` tenta esses dois IDs também em T2–T5. A suíte exportada não inclui Pumpkin Producer.
