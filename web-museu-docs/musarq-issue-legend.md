# Legenda da Nomenclatura de Issues — SIG-MUSARQ

Este repositório adota nomenclatura padronizada para facilitar leitura e triagem.

## Prefixo de frente

- `F` → **Frontend**
  - Telas, componentes, rotas, estado de interface e interação do usuário.
  - Exemplos: `F01`, `F04`, `F05`.

- `M` → **Modelo e Backend**
  - Regras de negócio, domínio, persistência, API, integração e comportamento do sistema.
  - Exemplos: `M01`, `M02`, `M03`, `M06` a `M13`.

- `I` → **Infraestrutura e Garantia**
  - Ambiente, segurança, consistência, performance, observabilidade e disponibilidade.
  - Exemplos: `I01`, `I02`, `I03`, `I04`.

Números são sequenciais dentro de cada frente e não precisam estar em ordem absoluta no repositório; o importante é que cada código identifique um trabalho coerente e único.

## Nome completo

O padrão usado nas issues é:

```
[Sprint N] [Prefixo] Título da entrega
```

Exemplos:

- `[Sprint 1] [F01] Prototipagem: estrutura de pastas e telas base do frontend`
- `[Sprint 3] [M01] Modelo de dados e contratos iniciais do SIG-MUSARQ`
- `[Sprint 10] [I03] Performance e prontidão do dashboard`

## O que cada frente entrega

### Frontend
- Interface usável e coerente.
- Navegação clara para o técnico e para o admin.
- Feedback legível em erros, estados e avisos.
- Componentes reutilizáveis quando faz sentido.

### Modelo e Backend
- Entidades e regras alinhadas ao PRD.
- Distinção correta entre máquinas, equipamentos, estoque e O.S.
- Validação forte em pontos críticos.
- Rastreabilidade e logs onde o negócio exige.

### Infraestrutura e Garantia
- Ambientes distinguíveis e credenciais protegidas.
- Operações críticas mais resistentes a falhas.
- Dashboards e listagens aceitáveis conforme os dados crescem.
- Capacidade de identificar problemas rapidamente.

## Separação das Sprints

### Sprint 1 — Prototipagem e estrutura
- Foco: definir como o repositório e o projeto vão ficar organizados.
- Entregável principal: estrutura de pastas, base de telas e README claro.
- Issues de exemplo:
  - `[Sprint 1] [I01] Prototipagem: organização inicial do repositório e README`
  - `[Sprint 1] [F01] Prototipagem: estrutura de pastas e telas base do frontend`
  - `[Sprint 1] [F02] Prototipagem: tela de cadastro com separação de perfis`

### Sprint 2 — Ativos visíveis
- Foco: máquinas e equipamentos como entidades distintas.
- Entregáveis principais: cadastro de máquinas e catálogo de emprestáveis.
- Issues de exemplo:
  - `[Sprint 2] [M06] Cadastro e status de máquinas de bancada`
  - `[Sprint 2] [M07] Catálogo de equipamentos para empréstimo`

### Sprint 3 — Base técnica para desenvolvimento
- Foco: modelo e contratos antes de codar módulos pesados.
- Entregáveis principais: modelo inicial e fronteira entre frentes.
- Issues de exemplo:
  - `[Sprint 3] [M01] Modelo de dados e contratos iniciais do SIG-MUSARQ`
  - `[Sprint 3] [M02] Fronteira e convenções entre frontend e backend`

### Sprint 4 — Acesso e cadastro
- Foco: login, perfis e cadastro operacional.
- Entregáveis principais: autenticação/back e telas de login e cadastro.
- Issues de exemplo:
  - `[Sprint 4] [M03] Login e perfis de acesso Admin / Técnico / Cliente`
  - `[Sprint 4] [F04] Tela de login do SIG-MUSARQ`
  - `[Sprint 4] [F05] Tela de cadastro de usuários`

A partir daqui, as sprints avançam por módulo/funcionalidade, não apenas por frente. A separação não é rígida: uma issue de backend pode estar em uma sprint que também tem tela correspondente.

### Sprints seguintes — desenvolvimento por domínio
- Sprints 5 a 9 concentram-se em módulos principais: máquinas/emprestáveis mais elaborados, suprimentos, O.S., manutenção, empréstimo, relatórios e auditoria.
- Sprint 10 concentra issues transversais de infra/garantia: ambiente seguro, consistência, performance e disponibilidade.

## Como usar a legenda
- Ao criar uma issue, escolha a frente pelo conteúdo real da entrega, não pela tinta da pessoa que vai fazer.
- Se uma issue toca mais de uma frente, use o prefixo da frente que tem a maior responsabilidade na entrega.
- Se uma issue é puramente organizacional ou documental do projeto, pode ser `I` quando for infra/garantia, ou `M` quando for modelo/contrato/documentação técnica do domínio.

## Leitura cruzada recomendada
- `musarq-cerebro.md` para o nó raiz do conhecimento do projeto.
- `musarq-sprints.md` para a visão por sprints e critérios de qualidade/usabilidade.
- `prd_project_brief_sistema_musarq.md` para os requisitos funcionais, regras de negócio e requisitos não funcionais.
- `musarq-github-issues.md` para o roteiro completo usado para criar as issues.
