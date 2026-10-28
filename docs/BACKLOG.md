# Backlog do Produto - Ordum (MVP)

Este documento organiza o backlog do MVP em épicos e histórias de usuário com critérios de aceite, pronto para ser importado para o GitHub Projects ou ferramenta de gestão ágil.

---

## Estrutura de Épicos

| ID | Épico | Objetivo |
|---|---|---|
| **EP01** | Infraestrutura e Bootstrap | Setup inicial do monorepo, Docker, backend Spring Boot e frontend Angular. |
| **EP02** | Gestão de Contas e Categorias | CRUD de contas bancárias/carteiras e categorias financeiras (base para lançamentos). |
| **EP03** | Lançamentos Financeiros e Saldos | Registro de receitas e despesas, projeções, confirmação manual e saldo consolidado. |
| **EP04** | Transferências entre Contas | Movimentação entre contas cadastradas com garantia de atomicidade e reversão. |
| **EP05** | Recorrências Mensais | Agendamento e geração automática/manual de parcelas e lançamentos recorrentes. |
| **EP06** | Dashboard e Visão Consolidada | Telas de resumo geral, filtros por período/tipo/conta e refinamento de UX. |

---

## Detalhamento das Histórias e Tarefas

### Épico 01: Infraestrutura e Bootstrap (Foco da Sprint 1)

#### `TASK-01` • Setup do Ambiente Docker e Banco de Dados
- **Descrição:** Criar `compose.yaml` com PostgreSQL (versão fixada, ex: 16-alpine) e script `.env.example`.
- **Critérios de Aceite:**
  - `docker compose up -d` sobe o banco de dados saudável.
  - Documentação no README explicando portas, credenciais padrão e variáveis.

#### `TASK-02` • Bootstrap do Backend (Java 21 + Spring Boot)
- **Descrição:** Inicializar a pasta `backend/` com Maven Wrapper, Java 21, dependências essenciais e integração com Flyway.
- **Dependências:** Spring Web, Spring Data JPA, PostgreSQL Driver, Flyway Migration, Bean Validation, Lombok (opcional/a definir).
- **Critérios de Aceite:**
  - Aplicação conecta com sucesso no PostgreSQL via Docker.
  - Endpoint de health-check ou ping (`GET /api/status` ou Actuator) respondendo `200 OK`.
  - Migração inicial Flyway (`V1__baseline.sql`) executada sem erros.

#### `TASK-03` • Bootstrap do Frontend (Angular)
- **Descrição:** Inicializar o projeto `frontend/` com Angular (versão atual estável, ex: v17+ ou v18+ com Standalone Components).
- **Critérios de Aceite:**
  - Projeto roda localmente via `npm start` ou `ng serve`.
  - Configuração de proxy reverso (`proxy.conf.json`) para apontar `/api` para a porta do backend.
  - Estrutura base de pastas (core, shared, features, layouts) definida.
  - Escolha e setup do framework de estilização/UI (Tailwind CSS, Angular Material ou Bootstrap).

#### `TASK-04` • Padronização de Git e Fluxo de Trabalho do Time
- **Descrição:** Definir estratégia de branches (GitFlow / GitHub Flow), padrões de commits (Conventional Commits) e PR Templates.
- **Critérios de Aceite:**
  - Arquivo `CONTRIBUTING.md` ou guia no README explicando o fluxo.
  - Template de Pull Request criado (`.github/pull_request_template.md`).

---

### Épico 02: Gestão de Contas e Categorias

#### `US-01` • CRUD de Contas Bancárias / Carteiras
- **Como** usuário,
- **Quero** cadastrar, editar e listar minhas contas (ex: Nubank, Carteira, Inter),
- **Para que** eu possa acompanhar onde meu dinheiro está guardado.
- **Critérios de Aceite:**
  - Saldo inicial padrão zero, permitindo customização na criação.
  - Não expor entidades JPA diretamente (usar DTOs).
  - Validação de campos obrigatórios (nome da conta não pode ser vazio).
  - Listagem com saldo atual de cada conta.

#### `US-02` • CRUD de Categorias
- **Como** usuário,
- **Quero** cadastrar categorias (ex: Alimentação, Transporte, Salário) com tipo (Receita ou Despesa),
- **Para que** eu possa organizar e filtrar meus gastos e ganhos.
- **Critérios de Aceite:**
  - Cadastro com nome e tipo (Receita/Despesa).
  - Listagem e edição simples no frontend.

---

### Épico 03: Lançamentos Financeiros e Saldos

#### `US-03` • Cadastro e Edição de Lançamentos (Receita / Despesa)
- **Como** usuário,
- **Quero** lançar receitas e despesas com descrição, valor, data prevista, conta e categoria,
- **Para que** eu tenha histórico e previsão financeira.
- **Critérios de Aceite:**
  - Valores monetários usando `BigDecimal` / `NUMERIC(19,2)`.
  - Datas sem componente de hora.
  - Status inicial: Pendente ou Confirmado.

#### `US-04` • Confirmação Manual de Lançamento e Reversão
- **Como** usuário,
- **Quero** marcar um lançamento como pago/recebido (ou desfazer a marcação),
- **Para que** meu saldo real reflita apenas o que já se concretizou.
- **Critérios de Aceite:**
  - Lançamento pendente não altera o saldo real/atual da conta.
  - Ao confirmar, o saldo atual da conta é recalculado.
  - Permitir desfazer a confirmação restaurando o saldo anterior.

#### `US-05` • Consulta de Saldo Atual e Previsto
- **Como** usuário,
- **Quero** visualizar o saldo atual consolidado e a projeção futura (saldo previsto),
- **Para que** eu saiba quanto tenho agora e quanto terei após as contas pendentes vencerem.
- **Critérios de Aceite:**
  - Saldo Atual: soma dos saldos iniciais + lançamentos confirmados.
  - Saldo Previsto: saldo atual + pendências até o horizonte de data selecionado (incluindo pendências atrasadas).

---

### Épico 04: Transferências entre Contas

#### `US-06` • Transferência de Valores entre Contas
- **Como** usuário,
- **Quero** transferir um valor de uma conta de origem para uma conta de destino,
- **Para que** eu mova meu saldo sem distorcer o total geral ou criar receitas/despesas falsas.
- **Critérios de Aceite:**
  - Operação atômica (`@Transactional`): debita na origem e credita no destino.
  - Saldo geral da aplicação permanece inalterado.
  - Exclusão da transferência reverte os saldos das duas contas.

---

### Épico 05: Recorrências Mensais

#### `US-07` • Criação de Séries Recorrentes
- **Como** usuário,
- **Quero** cadastrar despesas e receitas que se repetem mensalmente (fixas ou parceladas com N ocorrências),
- **Para que** eu não precise cadastrar manualmente todo mês.
- **Critérios de Aceite:**
  - Janela de geração de 12 meses para séries contínuas.
  - Ajuste inteligente para meses com menos dias (ex: dia 31 caindo em 28 de fevereiro).
  - Edição de uma ocorrência sem quebrar as ocorrências futuras.

---

### Épico 06: Dashboard, Filtros e Polimento

#### `US-08` • Filtros Avançados de Lançamentos
- **Como** usuário,
- **Quero** filtrar meus lançamentos por período (mês/ano), conta, categoria, tipo e situação (pago/pendente),
- **Para que** eu encontre rapidamente movimentações específicas.

#### `US-09` • Resumo Financeiro / Dashboard
- **Como** usuário,
- **Quero** uma tela inicial com cards de Saldo Atual, Saldo Previsto, Total a Pagar e Total a Receber no mês,
- **Para que** eu tenha uma visão imediata da minha saúde financeira.
