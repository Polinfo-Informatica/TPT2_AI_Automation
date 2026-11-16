# Teste de um lote no Crusher

Pacote experimental TPT2Batch. Habilite Run e Stop após importar. Na Factory, **8** solicita um lote de 1 Ore com atraso de 4 segundos e **F** interrompe o script. F encerra a automação, e um lote já enviado à máquina continua sendo processado.

O teste escolhe o menor tier de Ore disponível até T6 e até o tier instalado do Crusher. Despacha somente quando o Crusher está ocioso e confirma a redução de 1 Ore e aumento do Dust do mesmo tier. O teste deixa a bancada e as outras máquinas fora do fluxo.

No TPT2 v1.0.16 em 16/11/2026, o Crusher T6 converteu 1 Ore T1 em 2 Dust T1. Ore: 56623 → 56622. Dust: 0 → 2. Na tentativa seguinte, F antes do despacho encerrou o script e manteve Ore em 56622 e Dust em 2. Run compilou com 31 ações e Stop com 5. O jogo deixou os scripts importados desabilitados de início.

Na primeira tentativa do protótipo, interromper um worker chamado por `executesync` deixou o chamador preso. Use um worker direto ou garanta o encerramento explícito do chamador na integração. O Stop também encerra o chamador do pacote experimental anterior, se presente; deixe o pacote anterior desabilitado.

Código e pacote de teste para uso isolado. A integração ao Master, o processamento até Ingot e o upgrade automático ficam para as próximas etapas.
