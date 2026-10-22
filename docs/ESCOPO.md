# Escopo do MVP

## Objetivo e público

Permitir que uma pessoa acompanhe receitas, despesas e saldos, incluindo movimentações futuras, enquanto o grupo aprende Java, Angular, PostgreSQL e Docker.

A primeira versão terá um único contexto financeiro, sem autenticação. O desenvolvimento e as demonstrações usarão dados de exemplo.

## Funcionalidades previstas

- Cadastrar e editar contas, com saldo inicial padrão zero e possibilidade de alteração.
- Consultar saldo geral e saldo separado por conta.
- Cadastrar e editar categorias.
- Cadastrar, editar e excluir receitas e despesas com data prevista.
- Confirmar manualmente pagamentos e recebimentos e desfazer a confirmação.
- Consultar saldo atual e saldo previsto, incluindo pendências atrasadas na projeção.
- Criar recorrências mensais contínuas ou com quantidade definida de ocorrências.
- Editar uma ocorrência sem alterar as demais e encerrar uma série.
- Transferir valores entre contas sem alterar o saldo geral.
- Filtrar lançamentos por período, conta, tipo e situação.

## Evolução posterior

1. Contas de usuários, autenticação e isolamento dos dados de cada pessoa.
2. Gestão mais completa: cartões, parcelamentos, metas e planejamento financeiro, conforme prioridades futuras do grupo.

Importação bancária, publicação pública e moedas diferentes do real não fazem parte do MVP planejado.

## Condição de conclusão

Os fluxos principais devem funcionar de ponta a ponta entre Angular, API e PostgreSQL, com critérios de [validação](VALIDACAO.md) atendidos e instruções de execução reproduzíveis.
