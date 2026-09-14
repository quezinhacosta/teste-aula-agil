## Objetivo
Estruturar o banco de dados do SIG-MUSARQ de forma que ele sirva de base para backend, frontend e auditoria, sem acoplamento desnecessário.

## Contexto
O sistema precisa:
- diferenciar máquinas de bancada de equipamentos emprestáveis;
- controlar suprimentos que entram por kg/L e saem em frações;
- registrar manutenção preventiva mensal e corretiva com bloqueio;
- rastrear O.S. com técnico, cliente, máquina e tempo;
- registrar empréstimos com prazo, atraso e devolução;
- gerar relatórios gerenciais e logs de auditoria.

## O que entregar
- Modelo físico ou lógico aceito pela equipe, com entidades e relacionamentos.
- Definição de campos obrigatórios e tipos principais.
- Separação clara entre:
  - usuários e perfis
  - máquinas de bancada
  - equipamentos para empréstimo
  - suprimentos e saldo fracionado
  - manutenções
  - O.S./produção
  - empréstimos e devoluções
  - logs ou registros de auditoria relevantes
- Critérios para evitar saldo fantasma em operações de consumo.
- Decisão sobre chaves, timestamps e quem registra cada operação.

## Critério de aceite
- [ ] Dá para ler o modelo e identificar cada entidade principal.
- [ ] Dá para entender como o saldo de suprimentos é representado e como muda.
- [ ] Dá para entender como máquina e emprestável são diferentes no modelo.
- [ ] Dá para identificar os dados obrigatórios de uma O.S.
- [ ] Dá para saber como será registrada a auditoria das operações críticas.
- [ ] O modelo pode ser usado para iniciar implementação de backend.

## Fronteira
- Back: principal
- Front: receptivo
- Infra: decisão de tecnologia e conexão

## Dependências
- `[Sprint 3] [M01] Modelo de dados e contratos iniciais do SIG-MUSARQ`
- `[Sprint 3] [M02] Fronteira e convenções entre frontend e backend`
- `[Sprint 4] [M03] Login e perfis de acesso Admin / Técnico / Cliente`

## Regras e requisitos de referência
- RN01, RN04, RN05, RN06
- RN09
- RNF05, RNF06

## Como validar
1. Ler o modelo e responder: "uma máquina pode ser emprestada?"
2. Ler o modelo e responder: "uma O.S. de escaneamento pode debitar insumo?"
3. Ler o modelo e responder: "é possível gerar saldo inconsistente por cancelamento ou falha?"
4. Conferir que informações de auditoria básica estão previstas.
5. Confirmar que os campos de cada entidade cobrem os requisitos do PRD.

## Decisões pendentes
- Tecnologia de banco escolhida
- Se o modelo inicial será normalizado ou com desnormalizações controladas para relatórios
- Se logs de auditoria serão tabela própria ou parte de cada entidade
- Nomes das tabelas e convenção de nomenclatura adotada pela equipe
