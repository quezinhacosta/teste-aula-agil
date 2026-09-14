# MUSARQ Sprints — Planejamento de Desenvolvimento

> Repositório: [[MUSARQ Lab Prototipagem]]
> Artefato pai: [[MUSARQ Espiral — Cérebro do Projeto]]

Este arquivo reúne o plano de sprints, a organização modular do projeto e os critérios de qualidade e usabilidade. Ele deve ser revisado a cada ciclo. Não é um cronograma fechado; é um instrumento de decisão.

---

## 0. Princípios de desenvolvimento

- Entregue valor primeiro, complexidade depois.
- Separe o sistema por domínio, não por tipo de arquivo.
- Mantenha regras de negócio isoladas e reutilizáveis.
- Evite que o UI repita lógica que já existe no serviço ou no schema.
- Documente a intenção, não só o mecanismo.
- Antecipe estado inválido, não só o estado feliz.

Convenções recomendadas:
- Módulos por área de negócio
- Tipos próximos ao uso
- Componentes de UI focados em apresentação
- Serviços/hooks focados em comportamento
- Histórias com critérios de aceite claros

## 1. Visão rápida do produto

O sistema deve gerenciar:
- Usuários
- Máquinas de bancada
- Suprimentos fracionados
- Manutenções preventivas e corretivas
- Empréstimos de equipamentos
- Produção por O.S.
- Relatórios gerenciais

Importante:
- Máquinas não são emprestáveis.
- Suprimentos entram por kg e saem em frações.
- Escaneamento isenta consumo de insumo.
- Manutenção preventiva é obrigatória a cada 30 dias.

## 2. Módulos do sistema

### Auth
Responsável por:
- Login
- cadastro
- Perfis e papéis
- Controle de acesso e restrições

Conceitos-chave:
- Admin e técnico podem autenticar e escrever
- Cliente é cadastro passivo
- A autorização deve ser clara e centralizada

### Machines
Responsável por:
- Cadastro de máquinas
- Status operacional
- Preventivas
- Corretivas
- Bloqueios e alertas

Conceitos-chave:
- Cada máquina tem ciclo preventivo mensal
- Corretiva bloqueia produção até resolução
- Histórico deve ser consultável

### Inventory
Responsável por:
- Suprimentos comprados por kg ou L
- Controle de carretéis
- Saldo fracionado
- Estoque mínimo

Conceitos-chave:
- Entrada em kg
- Saída em gramas
- Consistência transacional
- Aviso de estoque baixo

### EquipmentLoans
Responsável por:
- Catálogo de emprestáveis
- Cautela
- Prazo
- Atraso
- Devolução com checklist

Conceitos-chave:
- Apenas periféricos podem ser emprestados
- Deve haver estado claro: no prazo, atrasado, devolvido
- Devolução libera o ativo

### Production
Responsável por:
- O.S.
- Peça ou projeto
- Técnico
- Cliente
- Máquina
- Consumo
- Tempo de produção

Conceitos-chave:
- Rastreabilidade obrigatória
- Escaneamento com consumo zero
- Produção não é só “o que foi feito”, mas “com quem, com que máquina e em quanto tempo”

### Reports
Responsável por:
- Filtros por período
- Consolidação mensal
- Exportação
- Rastreabilidade para auditoria

Conceitos-chave:
- Produção por técnico
- Consumo de estoque
- Empréstimos por mês
- Saída útil para prestação de contas

### Shared
Responsável por:
- Formatadores
- Validações menores
- Constantes
- Pequenas utilities de domínio
- UI leve reutilizável

## 3. Método de trabalho

Recomendação: ciclo em espiral com ritmo Scrum-like.

Ciclo sugerido:
1. Ler o que já existe
2. Definir histórias com aceite
3. Separar tarefas técnicas
4. Implementar em ordem de risco e dependência
5. Verificar qualidade e usabilidade
6. Revisar riscos e ajustar o plano

Regra prática:
- Sprint pequena > sprint ambiciosa e instável
- Se precisa de risco, faça cedo
- Se uma decisão é importante, anote a razão
- Se o módulo está confuso, o problema costuma ser o domínio, não a velocidade

## 4. Sprint 1 — Acesso e ativos

Objetivo:
- Permitir login e cadastro
- Separar máquinas de emprestáveis
- Criar base para todos os outros módulos

Histórias:
- Login de usuário
- Cadastro de usuário
- Cadastro de máquinas
- Cadastro de equipamentos para empréstimo

Critérios de aceite:
- Admin e técnico conseguem acessar o sistema
- Cliente não opera a gestão de máquinas
- Máquina e equipamento são distintos no modelo
- O cadastro não aceita dados inconsistentes óbvios

Entregáveis sugeridos:
- Módulo de auth funcional
- Módulo de máquinas com modelo definido
- Módulo de equipamentos com separação explícita

## 5. Sprint 2 — Manutenção

Objetivo:
- Implementar ciclo preventivo
- Registrar corretivas
- Mostar estado das máquinas e alertas

Histórias:
- Preventiva mensal com alerta
- Corretiva com bloqueio
- Histórico de manutenção por máquina/período

Critérios de aceite:
- Preventiva dispara no tempo certo
- Corretiva bloqueia a máquina
- O histórico é legível e coerente

Entregáveis sugeridos:
- Motor para ciclo preventivo
- Registro de corretiva
- View ou dashboard de manutenção

## 6. Sprint 3 — Produção e insumo

Objetivo:
- Permitir que técnico registre produção
- Controlar saldo fracionado
- Isentar consumo em escaneamento

Histórias:
- Carretéis e saldo
- O.S. de impressão com débito
- O.S. de escaneamento com consumo zero
- Rastreabilidade na produção

Critérios de aceite:
- Entrada por kg, saída por fração
- Escaneamento não debita insumo
- O.S. liga técnico, cliente, máquina e tempo

Entregáveis sugeridos:
- Módulo de estoque fracionado
- Módulo de O.S.
- Validação de isenção e saldo

## 7. Sprint 4 — Empréstimo

Objetivo:
- Controlar circulação de equipamentos
- Gerenciar prazo e atraso
- Executar devolução com protocolo

Histórias:
- Catálogo de emprestáveis
- Empréstimo com prazo
- Atraso visível
- Devolução com checklist e liberação

Critérios de aceite:
- Máquinas não aparecem para empréstimo
- Prazo e atraso são claros
- Devolução só libera quando o protocolo está completo

Entregáveis sugeridos:
- Fluxo de empréstimo e devolução
- Estado de rotatividade e atraso

## 8. Sprint 5 — Relatórios e auditoria

Objetivo:
- Fornecer visão gerencial
- Permitir recorte por período
- Exportar resultado útil

Histórias:
- Produção por técnico
- Consumo de estoque
- Empréstimos por mês
- Exportação e logs de auditoria

Critérios de aceite:
- Os relatórios respondem perguntas reais
- O período é parametrizável
- A exportação é útil para prestação de contas

Entregáveis sugeridos:
- Relatórios por módulo
- Exportação e visão consolidada
- Logs de auditoria

## 9. Testes de qualidade

### O que testar
- Regras de negócio isoladas
- Cálculo de consumo e saldo
- Lógica de ciclo preventivo
- Bloqueio por corretiva
- Estado de empréstimo
- Obrigatoriedade e consistência de O.S.
- RBAC e restrições de acesso

### Como organizar
- Comece pelas regras mais críticas
- Teste cálculos operacionais, não decoração
- Teste combinações inválidas, não apenas o caminho feliz
- Mantenha os testes legíveis; se não explicam o comportamento, são fracos

### Indicador de qualidade
- É fácil entender o que está sendo protegido
- É difícil criar um saldo fantasma ou uma O.S. incompleta sem aviso
- As regras não vivem só no frontend

## 10. Testes de usabilidade

### O que testar com pessoas
- Login e cadastro são diretos
- Técnico sabe onde registrar O.S.
- Máquina e emprestável são distinguidos de forma rápida
- Alerta de manutenção é entendido antes da operação
- Devolução é clara e o checklist é usado
- Relatório ajuda a decisão, não apenas informa

### Como conduzir
- Escolha tarefas curtas e reais
- Observe mais do que pergunte
- Registre onde a pessoa hesita
- Meça tempo e erros nos fluxos importantes
- Não confunda “bonito” com “usável”

### Sinais de que precisa melhorar
- O usuário não encontra a ação
- O aviso parece genérico demais
- O erro não diz como recuperar
- O relatório é visualmente rico, mas pouco analítico
- O técnico precisa voltar porque o fluxo não foi claro

## 11. Boas práticas para manutenção

- Dê nome ao módulo pelo que ele faz
- Dê nome ao tipo pelo que ele representa
- Dê nome ao estado pelo que ele significa
- Evite arquivos gigantes
- Evite componentes que decidem coisa de negócio
- Evite repetir validação em mais de um lugar
- Sempre que uma regra for importante, deixe o teste falando por ela

## 12. Checklist de revisão antes de fechar algo

- O módulo responde a um propósito claro?
- Os tipos coerem com a realidade do laboratório?
- A UI mostra o que importa, sem ruído?
- As regras de negócio estão longe do espaguete?
- O fluxo funciona para o técnico na bancada?
- O relatório/estado/alerta é interpretável?
- O código custodia algo sensível de forma cuidadosa?
- A mudança foi Exercitado onde era necessário?

## 13. Decisões pendentes

Use esta seção para registrar o que ainda não está definido.

Exemplos típicos:
- Onde o sistema vai rodar
- Se vai haver integração institucional
- Como serão gerados os relatórios exportáveis no MVP
- Como será o fluxo de restauro de dados e backup
- Quais recursos serão feitos primeiro fora do plano ideal

---
^LerMUSARQSprints
