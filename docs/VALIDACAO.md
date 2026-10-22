# Validação

## Estado atual

A documentação foi criada; a aplicação ainda não está implementada neste repositório. Os cenários abaixo são critérios futuros, não resultados de testes executados.

## Estratégia planejada

- Testes unitários para cálculos monetários, regras de datas e recorrência mensal.
- Testes de integração com PostgreSQL para migrações, persistência, transferências transacionais e geração sem duplicação.
- Testes do frontend para cadastro, confirmação e atualização dos saldos, incluindo respostas de erro.
- Verificação manual dos fluxos completos em ambiente local, com dados fictícios.

## Cenários de aceite

| Cenário | Resultado esperado |
|---|---|
| Criar conta sem informar saldo inicial | Saldo inicial zero |
| Alterar saldo inicial | Recalcular saldo da conta e geral |
| Registrar despesa prevista de R$ 30 em conta com R$ 100 | Atual R$ 100; previsto R$ 70 se incluída na projeção |
| Confirmar essa despesa | Atual R$ 70, sem duplicar o efeito na projeção |
| Desfazer confirmação | Atual volta a R$ 100; despesa volta a pendente |
| Receita futura pendente | Afetar apenas a projeção até a confirmação |
| Pendência atrasada | Continuar pendente e entrar na projeção |
| Lançamento anterior à referência | Rejeitar sem persistir |
| Transferir R$ 40 entre duas contas | Debitar uma, creditar outra e manter saldo geral |
| Transferir para a mesma conta | Rejeitar sem alterar saldo |
| Falhar uma operação de transferência | Não persistir efeito parcial |
| Excluir transferência | Reverter os efeitos nas duas contas |
| Recorrência de 31 de janeiro | Usar último dia de fevereiro e 31 de março |
| Recorrência em ano bissexto | Usar 29 de fevereiro quando aplicável |
| Série com 12 ocorrências | Criar exatamente 12, incluindo a primeira |
| Gerar novamente a mesma série | Não duplicar ocorrências |
| Reiniciar com série contínua | Completar a janela futura sem duplicação |
| Editar uma ocorrência | Preservar as demais |
| Excluir uma ocorrência e gerar novamente | Não recriar a ocorrência excluída |
| Encerrar série | Remover futuras pendentes e preservar confirmadas |
| Filtrar por período, conta, tipo e situação | Exibir somente os registros correspondentes |
| Enviar valor inválido à API | Rejeitar com erro uniforme e compreensível |

## Registro das verificações futuras

Para cada execução, registrar data, versões, ambiente, comando ou passos, resultado e limitações. Distinguir compilação, teste automatizado e verificação manual; um build bem-sucedido não comprova todos os fluxos.
