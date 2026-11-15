# Teste do seletor T6 no jogo

Abra Headquarters → Facility AI → Import, cole `selector-qa-import.txt` e aplique. Habilite os 16 scripts do pacote TPT2QA. Saia do Headquarters, abra o overlay com **F4** e pressione **9**.

O resultado esperado é `qa_done=8`, `qa_pass=8`, `qa_mask=255`. Cada linha abaixo corresponde ao valor somado à máscara se o caso passar:

| Valor | Caso |
| ---: | --- |
| 1 | Candidato único sem custo |
| 2 | Transport Belt como candidato único |
| 4 | Empate com custo zero válido |
| 8 | Empate com custo ausente |
| 16 | Manter alvo usando snapshot validado |
| 32 | Liberar o alvo ao chegar em T6 |
| 64 | Nenhuma máquina abaixo do teto |
| 128 | Snapshot inválido |

Os casos usam o motor da Facility AI com tiers e custos controlados. As ações se limitam a variáveis de teste e comandos internos de script. O pacote importável inclui `budget: -1` e `useBudget: true`, os campos usados pelo formato aceito pelo jogo.
