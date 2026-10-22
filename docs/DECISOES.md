# Decisões e pendências

## Decisões confirmadas pelo grupo nesta conversa

- Projeto de finanças pessoais, começando por um MVP para aprendizado.
- Java 21, Spring Boot com Maven, Angular e PostgreSQL.
- Banco no Docker; backend e frontend executados localmente.
- Repositório único próprio: `o-matheus/ordum`, separado dos materiais do grupo.
- Receitas e despesas previstas, com confirmação manual.
- Saldo geral e separado por contas; transferências incluídas no MVP.
- Saldo inicial padrão zero, com possibilidade de alteração.
- Recorrência mensal contínua ou com quantidade definida de ocorrências.
- Evolução posterior para usuários individuais, autenticação, privacidade e gestão financeira mais completa.

## Detalhes incorporados ao plano técnico aprovado

- BRL como moeda única; `BigDecimal` e `NUMERIC(19,2)` para valores.
- Flyway para migrações e DTOs na API.
- Datas financeiras sem horário.
- Projeção inclui pendências atrasadas até o horizonte escolhido.
- Recorrências contínuas com janela futura de doze meses, atualizada na inicialização e diariamente.
- Vencimentos ajustados ao último dia do mês, preservando o dia original da série.
- Edição individual de ocorrências; alterações gerais por encerramento e criação de nova série.
- Saldos negativos permitidos e transferências transacionais.

## Pendências para a implementação

- Fixar e testar versões compatíveis das ferramentas, além do Java 21 já definido.
- Definir contratos detalhados da API e estratégia de validação da alteração de referência da conta.
- Definir a estratégia de exclusão de uma ocorrência para impedir sua recriação automática.
- Definir o tratamento de datas efetivas futuras e o intervalo permitido para consultas de projeção.
- Definir limites operacionais para séries finitas e o tratamento de séries contínuas com início distante.
- Definir fuso do agendamento, concorrência da geração e precisão do horizonte de doze meses.
- Escolher a estrutura visual e bibliotecas de interface, se necessárias.
- Definir responsabilidades, disponibilidade e primeiro ciclo do grupo.

## Estado e origem

Este registro consolida as decisões e o plano da conversa de preparação do projeto. Não comprova implementação. Código experimental criado fora deste repositório não foi incorporado ao Ordum.
