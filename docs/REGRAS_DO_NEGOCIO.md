# Regras de negócio

Estas regras descrevem o comportamento planejado para o MVP.

## Contas e saldo inicial

Cada conta terá nome, saldo inicial e data de referência. O saldo inicial será zero por padrão, mas poderá ser informado e alterado. Alterá-lo recalculará os saldos derivados, sem criar uma receita ou despesa artificial.

Não serão aceitos lançamentos anteriores à referência da conta. A alteração dessa referência não poderá tornar registros existentes incompatíveis; os detalhes de validação serão definidos antes da implementação.

## Receitas e despesas

Cada lançamento terá descrição, valor positivo, tipo (receita ou despesa), categoria, conta e data prevista. Começará pendente. A passagem da data prevista não o confirmará automaticamente.

A confirmação manual registrará a data efetiva de pagamento ou recebimento. Desfazer a confirmação removerá seu efeito sobre o saldo atual e devolverá o lançamento às pendências. Editar ou excluir um lançamento confirmado deverá atualizar os saldos correspondentes.

Valores serão representados em reais, com duas casas decimais. O backend usará `BigDecimal` e o banco, `NUMERIC(19,2)`.

## Saldo atual e projeção

O saldo atual de uma conta será o saldo inicial somado às receitas confirmadas, menos as despesas confirmadas, com os efeitos das transferências realizadas. O saldo geral será a soma dos saldos de todas as contas.

O saldo previsto acrescentará ao saldo atual as receitas pendentes e subtrairá as despesas pendentes até a data escolhida. Pendências atrasadas também entrarão nessa projeção. Um lançamento confirmado não poderá ser contado novamente como pendente.

Exemplo: saldo inicial de R$ 100 e despesa pendente de R$ 30 resultam em saldo atual de R$ 100 e previsto de R$ 70, se a despesa estiver no horizonte escolhido. Após confirmá-la, ambos passam a R$ 70.

## Recorrência mensal

O usuário poderá escolher repetição mensal contínua ou uma quantidade total de ocorrências, incluindo a primeira. Doze ocorrências representam doze lançamentos mensais; não representam um único lançamento anual.

Séries finitas gerarão todas as ocorrências na criação. Séries contínuas manterão uma janela de doze meses futuros, atualizada na inicialização e diariamente. A geração deverá ser idempotente: executar novamente não poderá duplicar ocorrências. O banco terá uma restrição única por série e ocorrência.

Para vencimentos em dias inexistentes, usar o último dia do mês, mantendo o dia original como referência. Uma série iniciada em 31 de janeiro terá vencimento no último dia de fevereiro e em 31 de março.

Editar uma ocorrência afetará apenas ela. Excluir uma ocorrência não poderá fazer com que ela reapareça na geração seguinte; a estratégia técnica para garantir isso será definida antes da implementação.

Encerrar uma série removerá ocorrências futuras pendentes e preservará o histórico confirmado. Para alterações gerais, o MVP exigirá encerrar a série e criar outra.

## Transferências

Informar conta de origem, conta de destino, valor positivo e data efetiva. As contas devem ser diferentes. Débito e crédito deverão ocorrer em uma única transação: ou ambos os efeitos serão aplicados, ou nenhum.

Transferências não serão classificadas como receitas ou despesas e não alterarão o saldo geral. Excluir uma transferência reverterá os efeitos nas duas contas. Saldos negativos serão permitidos.
