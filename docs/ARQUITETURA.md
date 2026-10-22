# Arquitetura e ambiente

## Estrutura planejada

Um repositório único, independente do repositório de materiais do grupo:

```text
ordum/
├── docs/
├── backend/
├── frontend/
├── compose.yaml
└── .env.example
```

Atualmente, apenas a documentação está presente. As demais pastas e configurações são planejadas.

## Backend

Java 21, Spring Boot e Maven, com Spring Web, Spring Data JPA, Bean Validation e Flyway. Organizar o código por funcionalidade, separando controllers, serviços, repositórios e DTOs. Não expor entidades JPA diretamente na API.

Entidades planejadas: Conta, Categoria, Lançamento, Recorrência e Transferência. Datas financeiras serão representadas sem horário. Operações financeiras que alterem múltiplos registros deverão ser transacionais.

As migrações Flyway definirão e evoluirão o esquema. O banco deverá aplicar chaves estrangeiras, precisão monetária e unicidade das ocorrências recorrentes.

## Frontend

Angular com componentes standalone e formulários reativos. Telas de resumo, contas, categorias e lançamentos, com acesso aos fluxos de transferências e recorrências. Exibir erros de validação de forma compreensível e atualizar saldos após as operações.

## API REST planejada

Prefixo `/api`. Os contratos detalhados de campos, respostas e códigos HTTP ainda serão definidos na implementação.

| Recurso | Operações previstas |
|---|---|
| `/contas` | Listar, cadastrar e editar contas |
| `/categorias` | Listar, cadastrar e editar categorias |
| `/lancamentos` | Listar com filtros, cadastrar, editar, excluir, confirmar e desfazer confirmação |
| `/recorrencias` | Listar, criar e encerrar séries |
| `/transferencias` | Listar, criar e excluir com reversão dos efeitos |
| `/resumo` | Consultar saldo geral e por conta, atual e previsto |

Usar erros uniformes para validação e regras de negócio. O frontend não será a única camada de validação.

## Ambiente e versões

PostgreSQL via Docker Compose; Java e Angular executados localmente. Incluir Maven Wrapper, imagem do banco com versão fixada, dependências fixadas, modelo de configuração e instruções de execução.

Java 21 está confirmado. Versões exatas de Spring Boot, Maven Wrapper, Angular, Node.js e PostgreSQL deverão ser verificadas em conjunto e fixadas antes do bootstrap. Nenhuma combinação foi testada neste repositório ainda.

Credenciais locais ficarão fora do Git. O `.env.example` documentará as variáveis necessárias sem conter segredos reais. A integração entre frontend e API deverá ter configuração local documentada.

## Uso inicial

Sem autenticação, o MVP terá um único contexto financeiro e será executado localmente com dados fictícios. Autenticação e isolamento por usuário precederão o uso compartilhado com dados reais.
