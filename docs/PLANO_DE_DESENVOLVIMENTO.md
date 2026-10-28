# Plano de desenvolvimento

Todas as etapas abaixo estão planejadas. Não há entrega de software validada neste repositório.

## 1. Preparar o ambiente

Criar backend, frontend e Compose. Fixar versões compatíveis, configurar Maven Wrapper, migração inicial e modelo de variáveis. Documentar os comandos de execução.

**Aceite:** outra pessoa do grupo consegue iniciar o banco, o backend e o frontend seguindo as instruções.

## 2. Contas e categorias

Implementar persistência, API e formulários. Permitir saldo inicial padrão zero e edição, respeitando a data de referência.

**Aceite:** cadastrar e editar pela interface, com dados persistidos após reiniciar a aplicação.

## 3. Lançamentos e saldos

Implementar receitas e despesas, filtros, confirmação manual, desfazer confirmação, edição e exclusão. Integrar resumo atual e previsto.

**Aceite:** pendências afetam apenas a projeção; confirmações e reversões atualizam corretamente os saldos.

## 4. Transferências e recorrências

Implementar transferências atômicas e exclusão com reversão. Adicionar séries mensais finitas e contínuas, geração sem duplicação, edição individual e encerramento.

**Aceite:** transferências preservam o saldo geral; recorrências respeitam os dias de vencimento e não recriam ocorrências excluídas.

## 5. Integração e revisão

Revisar telas, mensagens, filtros, documentação de execução e testes. Executar os cenários de [validação](VALIDACAO.md) e registrar evidências e limitações.

**Aceite:** fluxos completos funcionam entre frontend, API e PostgreSQL.

## Organização e Capacidade do Time

- **Tamanho da equipe:** ~7 a 8 pessoas (todos atuando como full stack).
- **Papel de Product Owner (PO):** Matheus.
- **Disponibilidade semanal informada:**
  - Matheus: 6h/semana
  - Marcelo: 6h/semana
  - Bianca: 6h/semana
  - Fabio: 4h/semana
  - Joniel: 4h/semana
  - Lucas Yago e Nicole Ferraz: a confirmar na reunião (estimativa base: ~4h/semana cada).
  - **Capacidade semanal estimada:** ~26h a 34h/semana total do time (ou ~38h se houver mais um integrante).
- **Cadência recomendada:** Sprints de 2 semanas (para acomodar dedicação parcial, pair programming e ciclo completo de PRs e code review).
