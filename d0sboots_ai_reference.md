# Referência do compilador d0sboots para Factory e Mine

Editor 2.07, com alvo de jogo v1.0.12 no workspace original. As listas abaixo correspondem aos validadores de literais `craft`, `produce` e `machine` do editor.

## Assinaturas

```text
craft(string item, int tier, double amount)
produce(string item, int tier, double amount, string machine)
```

O compilador aceita `tier` literal de **1 a 10**. O tier efetivo, os desbloqueios, a compatibilidade da máquina e os insumos são avaliados pelo jogo. Use os IDs com a grafia exata, incluindo o `F` maiúsculo em `producer.constructionFirm`.

## `craft` — IDs de item (49)

| Família | IDs válidos |
| --- | --- |
| Chips | `chip.basic`, `chip.advanced`, `chip.hitech`, `chip.nano`, `chip.quantum`, `chip` |
| Componentes e itens especiais | `hammer`, `sapling.rubber`, `sapling.void`, `dust.rainbow`, `cable.insulated`, `plate`, `motor`, `pump`, `block`, `plate.stack`, `lump` |
| Produtores | `producer.town`, `producer.statueofcubos`, `producer.workshop`, `producer.shipyard`, `producer.laboratory`, `producer.constructionFirm`, `producer.mine`, `producer.powerplant`, `producer.arcade`, `producer.headquarters`, `producer.tradingpost`, `producer.museum`, `producer.factory`, `producer.exoticgems`, `producer.gems`, `pumpkin.producer` |
| Boosters | `booster.acceleration`, `booster.machines`, `booster.production.regular`, `booster.resource.drops`, `booster.trees` |
| Halloween | `pumpkin.stack` |
| Máquinas | `machine.oven`, `machine.assembler`, `machine.refinery`, `machine.crusher`, `machine.cutter`, `machine.presser`, `machine.mixer`, `machine.transportbelt`, `machine.shaper`, `machine.boiler` |

## `produce` — IDs de entrada (14)

`rubber`, `dust.rainbow`, `ingot.rainbow`, `cable`, `ore`, `dust`, `ingot`, `plate`, `block`, `plate.stack`, `rod`, `lump`, `pumpkin`, `pumpkin.stack`.

O primeiro argumento é o **item que entra** na máquina. Os nove IDs aceitos no quarto argumento são `oven`, `assembler`, `refinery`, `crusher`, `cutter`, `presser`, `mixer`, `shaper`, `boiler`. O Belt é usado no refino e seu ID de fabricação é `machine.transportbelt`.

### Combinações de produção documentadas

| Máquina | Entrada → saída |
| --- | --- |
| `crusher` | `ore` → `dust` |
| `oven` | `dust` → `ingot`, `dust.rainbow` → `ingot.rainbow` |
| `mixer` | `lump` → `dust` do tier seguinte |
| `presser` | `ingot` → `plate`, `ingot.rainbow` → `plate.rainbow`, `plate.stack` → `plate.dense`, `rubber` → `plate.rubber`, `pumpkin.stack` → `pumpkin.plate` |
| `boiler` | `block` → `block.dense`, `pumpkin` → `pumpkin.anti` |
| `shaper` | `ingot` → `rod`, `plate` → `pipe`, `rod` → `ring` |
| `refinery` | `ingot` → `cable`, `plate` → `plate.circuit`, `cable` → `wire` |
| `cutter` | `rod` → `screw`, `pumpkin` → `pumpkin.carved` |
| `assembler` | `cable` → `circuit` |

Em `produce("rubber", tier, amount, "presser")`, o jogo ignora o tier de `rubber`. Para subir dust de tier, a automação de referência usa `craft("lump", tier, amount)` e envia o lote de lumps ao Mixer.

## Restrições de execução e UI

| Operação | Condições |
| --- | --- |
| Abrir e fechar prédio | `show("factory", true)` ou `show("mine", true)` abre a janela sem animação de transição. Use `false` para fechar e `isopen("factory")` ou `isopen("mine")` para conferir se a janela está ativa e visível. |
| Fabricar na Factory | `craft` exige a Factory visível. Usa o inventário e a grade de fabricação. A chamada fica sem efeito quando o lote pedido não pode ser fabricado. |
| Alimentar uma máquina | `produce` precisa do lote de entrada disponível e de uma máquina compatível. Uma máquina ocupada com outro tipo de item impede a operação. Na suíte, essas chamadas são executadas durante a janela da Factory. |
| Comprar na Shop | A Shop é um painel da Factory com estoque limitado e compras em cubos vermelhos. A lista de funções Factory do editor não expõe compra na Shop. Uma automação por clique precisa abrir o painel certo e localizar os controles na escala de UI usada. |
| Minerar e abrir camada | `dig(x, y)` e `newlayer()` exigem a Mine ativa. O compilador valida coordenadas de `0` a `3` por eixo, com origem no canto superior esquerdo. `newlayer()` opera na aba ativa e depende de uma carga. |
| Escolher recurso da Mine | `tab(pos)` seleciona uma aba de `1` a `12`, de Orange a Black. `hasLayers()` consulta a disponibilidade de camada na aba ativa. |

## Fontes

- [Validadores do compilador](https://github.com/d0sboots/perfect-tower/blob/main/scripts/lexer-functions.lua)
- [API de scripting do jogo](https://wiki.perfecttower2.com/AI)
- [Receitas da Factory Automation](https://github.com/d0sboots/PerfectTower/blob/main/factory/recipes.tpt2) e [tratamento de ore, dust e lump](https://github.com/d0sboots/PerfectTower/blob/main/factory/craft.tpt2)
- [Factory](https://wiki.perfecttower2.com/Factory) e [Mine](https://wiki.perfecttower2.com/Mine)
