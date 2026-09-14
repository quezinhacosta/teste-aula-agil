# Plano de Consolidação de Issues

Este plano serve para reduzir redundâncias e deixar a fila de issues minimamente objetiva antes de começar o desenvolvimento.

## Princípios

- Uma issue = um trabalho objetivo e não repetido
- Sprint tem que estar clara
- Frente tem que estar clara: front, back, data/banco, proto, projeto/doc, coordenação, infra
- Tempo de sprint não pode ser usado como desculpa para acumular pendências obscuras
- Firebase foi trocado por Supabase como backend pretendido

## O que consolidar

### Sprint 1

Grupo que está sobrecarregado:
- #2, #3, #26, #30, #25, #29, #31, #4

Ação:
- Manter um conjunto menor por frente
- Unificar estrutura de front num problema só
- Unificar prototipagem num problema só
- Manter projeto/doc num problema só
- Manter coordenação/sprint num problema só
- Ajustar #25 para Supabase e deixá-lo como decisão/backplane

Sugestão de estado após consolidação:
- Front: um ou dois problemas
- Back/supabase: um ou dois problemas
- Data: um ou dois problemas
- Projeto/doc: um problema
- Proto: um problema
- Coordenação: um problema

### Sprint 2

Grupo com possível duplicata:
- #5 e #12
- #6 e #13

Ação:
- Verificar se são mesmo escopo
- Se forem, consolidar por sprint ou manter um só com escopo mais amplo, não dois iguais

### Sprint 3

Grupo com possível duplicata:
- #7, #8, #24, #28

Ação:
- Separar claramente:
  - modelo/contratos
  - banco/supabase
  - fronteira/convensoes
- Evitar que quatro issues fiquem dizendo a mesma coisa com nomes diferentes

### Sprint 4 a Sprint 9

Ações:
- Manter esse bloco, mas revisar apenas sobreposições óbvias
- Não abrir novos problemas enquanto não definir schema/back/auth

### Sprint 10

Ações:
- Manter bloco infra, mas reavaliar se cada um ainda faz sentido depois de definição de Supabase
- Não criar problema de infra antes da base estar clara

## Regra prática de parada

Se duas issues responderem à mesma pergunta principal, uma delas deve ser removida ou fundida.
Se uma issue não puder ser entregue sem outra, a dependência precisa ficar clara e não virar duplicata.
Se uma issue for “organizar o projeto”, ela deve ter escopo pequeno e útil, não ser repositório de tudo que a equipe ainda não decidiu.

## Próximos passos após consolidação

1. Aprovar grupo final de issues
2. Reabrir ou fundir apenas o necessário
3. Ajustar #25 para Supabase
4. Criar issues mínimas para Supabase: schema, auth/perfis, RLS/perms
5. Parar de criar issues genéricas
6. Começar desenvolvimento quando o grupo estiver enxuto e as principais decisões forem óbvias
