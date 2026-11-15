# Factory, Mine e Torre — fase T6

Base de produção: `d3ea770b7af59a9ed89cad4b04d8125ea72c7ba1`. Jogo local observado no log: **v1.0.16**. Perfil de IA informado: **36,7 GB de RAM e 23,36 TFLOPS de CPU**. Medir ações, RAM e tempo de resposta no perfil antes de ativar. Manter os limites de tier, mineração e agenda parametrizáveis.

- Ler o tier das dez máquinas. Selecionar primeiro pelo menor tier instalado entre as elegíveis e depois pelo menor custo de materiais do próximo upgrade, convertido em insumos-base pelas receitas verificadas. Definir o peso de cada insumo-base e usar uma ordem fixa se o custo empatar. Tratar tier desconhecido e custo ausente explicitamente. O Belt precisa de confirmação em jogo ou valor confirmado na configuração enquanto a API não expuser o tier instalado.
- Fixar a máquina escolhida até atingir T6. A cada upgrade confirmado pelo tier instalado, recalcular o próximo da mesma máquina. Conservar o alvo e publicar o bloqueio quando faltar uma condição. Só selecionar outra quando a atual chegar ao teto.
- Calcular a árvore de receitas do alvo considerando tier, lotes, rendimento, inventário, reservas e itens em processamento. Usar minério do worker. Converter minério em dust no Crusher, subir tier por lump/Mixer quando necessário, fundir dust no Oven e fabricar os componentes necessários. Confirmar aceitação de cada lote. Verificar a substituição automática das máquinas instaladas no save de teste.
- Visitar a Mine periodicamente, escavar as grades visíveis e consumir cargas por aba acessível. Distinguir esgotamento, rodada limitada com cargas restantes, interrupção e configuração ausente. Fazer a passada por todas as abas antes de repetir.
- Quando a Factory tiver despachado todos os lotes possíveis e a Mine estiver esgotada, usar a Torre durante a janela livre. A janela é o menor tempo estimado até próximo lote útil ou próxima carga de mineração, menos a margem medida de saída e retorno. Sem leitura confiável, medir sondagens e calibrar o intervalo. Medir duração de rounds e confirmar como sair e retomar; preservar o script de skills existente.
- Um controlador coordena a troca de telas. A tecla F deve interromper os scripts da suíte e o controlador deve conferir a tela ativa antes de enviar ações. Laboratory fica para etapa posterior.

## Entregas

Gemini escreve o código e entrega a fonte com `TPT2_READY | fase | revisão | arquivos | verificações | pendências`. Codex compara as APIs com o compilador local, compila, verifica a importação local e registra confirmação `TPT2_ACK` com o resultado. Gemini confirmou que pode entregar código pelo chat. Codex publica na branch de trabalho `factory-mine-t6`. A suíte de `main` segue como base.

O pacote de revisão é experimental. A compilação é uma etapa distinta dos testes de estoque, navegação e progressão no jogo.
