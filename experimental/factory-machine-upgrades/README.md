# Factory upgrades T1–T10

Protótipo para o editor d0sboots. Há um arquivo `.tpt2` por máquina e tier. O T1 é a fabricação inicial. Para T2–T10, cada arquivo contém a receita direta, inclusive a máquina do tier anterior. A lógica de produção fica em `core/`.

## Importação e execução

1. No editor d0sboots, importe o JSON de **uma máquina** em `workspaces/` como fonte. Cada workspace individual tem 19 scripts e inclui T1–T10. Ao trocar de máquina, exporte o workspace desejado e substitua o pacote anterior `TPT2Upgrade` no jogo.
2. Exporte o workspace compilado e importe o código na IA do jogo. Habilite o pacote `TPT2Upgrade`. Desative outros scripts que controlam a Factory para manter estáveis as leituras de estoque. Os JSON desta pasta são para o editor, e precisam passar pela exportação do editor antes da importação no jogo.
3. Abra a Factory e use **J** para iniciar. **F** interrompe os próximos despachos. Um lote aceito pela máquina pode terminar depois da parada.
4. Acompanhe `uf_note` no overlay. Quando aparecer `Move machine...`, mova a máquina antiga para o inventário. Quando aparecer `Install machine...`, instale a nova. Pare com F antes de devolver a anterior ao slot. O Master prossegue quando confirma o tier instalado.
5. O arquivo `Config` limita a automação a **T6**. Após desbloquear tiers superiores, ajuste `uf_cap` no editor e exporte novamente.

`workspaces/all-t2-t10-source.json` contém 99 scripts e cobre os upgrades de todas as dez máquinas que já têm T1 instalado. O Master escolhe pelo menor tier instalado, compara candidatos desse tier pelo total de unidades de Ore e Rubber ainda necessárias para produzir as peças faltantes e mantém a máquina escolhida até o limite configurado. O workspace de uma máquina precisa de 19 slots e também permite a fabricação inicial T1 quando as outras máquinas já conseguem fazer as peças.

O planejador desconta o estoque e reserva insumos compartilhados entre peças. Usa Dust disponível, depois Ore do mesmo tier, e finalmente Lumps do tier anterior pelo Mixer. O Crusher, Shaper e Refiner têm rotas que produzem múltiplas unidades por insumo. Nelas, o arredondamento usa o menor número de lotes inteiros que cobre o déficit. A operação aguarda a confirmação de inventário antes do lote seguinte.

## Verificação

- As 50 receitas de T2–T6 coincidem com as receitas diretas já registradas nesta branch. T1 e T7–T10 vêm da mesma [referência d0sboots](https://github.com/d0sboots/PerfectTower/blob/main/factory/recipes.tpt2).
- A simulação executou os arquivos TPT2 com funções mockadas, incluindo a movimentação pela interface. Passaram 18 cenários, incluindo as dez cadeias T5–T10 desde Ore e Rubber, estoque suficiente, déficit exato, falta de material e parada antes de despachar.
- A compilação no editor, a leitura do slot Belt pela IA e o teste em jogo deste pacote estão pendentes. A troca da máquina é manual. Este pacote cobre a Factory, e a integração com Mine e Torre ainda está pendente.
