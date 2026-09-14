# MUSARQ Espiral — Cérebro do Projeto

> Repositório: [[MUSARQ Lab Prototipagem]]
> Método: desenvolvimento em espiral com sprints Scrum-like
> Status atual: planejamento pós-pull

---

## 1. Função do arquivo

Este arquivo é o **nó raiz do conhecimento do projeto**. Cada seção abaixo deve poder ser lida isoladamente, mas o sentido completo vem da conexão entre requisitos, módulos, testes e demais decisões.

Como é um cérebro, não é apenas uma lista de tarefas: é um lugar onde decisões, justificativas e dependências são nomeadas, conectadas e recuperáveis depois.

## 2. Visão do produto

O sistema é o **SIG-MUSARQ**, plataforma de gestão operacional do laboratório de prototipagem.

Objetivos principais:
- Diferenciar **máquinas de bancada** de **equipamentos emprestáveis**
- Controlar suprimentos comprados por kg e usados em frações de grama
- Garantir manutenção preventiva mensal e registro de corretivas
- Registrar produção por O.S. com rastreabilidade completa
- Fornecer relatórios gerenciais mensais para coordenação e fomento

Referências diretas:
- [[Visão Geral MUSARQ]]
- [[Autenticação e Perfis]]
- [[Máquinas e Manutenções]]
- [[Insumos e Estoque Fracionado]]
- [[Equipamentos para Empréstimo]]
- [[Produção e O.S.]]
- [[Relatórios Gerenciais]]

## 3. Módulos e organização de código

A recomendação é organizar o sistema por **domínios coesos**, não por tipo de arquivo.

Sugestão de módulos:
- `auth` — login, cadastro, perfis, controle de acesso
- `machines` — cadastro de máquinas, status, preventivas, corretivas
- `inventory` — suprimentos, carretéis, entradas por kg, saídas fracionadas
- `equipment-loans` — catálogo de emprestáveis, empréstimo, devolução
- `production` — O.S., rastreabilidade, consumo, técnico, cliente, máquina
- `reports` — Views analíticas, filtros por período, exportação
- `shared` — regras, validações, i18n, formatadores, UI pequena

Para cada módulo, manter:
- Tipos/schemas próximos do comportamento
- Hooks ou serviços com lógica de negócio isolada
- Componentes de UI que recebem dados prontos e evitam lógica de dominio
- Casos de uso pequenos e com nome que diz o que o sistema faz

Regra prática:
- Se um arquivo cresce e precisa de scroll constante, extraia uma responsabilidade
- Se uma tela sabe demais sobre outras telas, introduza uma camada de estado ou serviço
- Se a mesma validação aparece em mais de um lugar, centralize

## 4. Boas práticas de programação

- Nomeie por intenção, não por implementação
- Prefira tipos explícitos para os dados críticos do negócio
- Evite efeitos colaterais escondidos em componentes
- Mantenha cada função com uma única preocupação
- Trate estados inválidos o mais cedo possível
- Registre apenas o que ajuda a entender falhas ou auditoria
- Não repita condições de regra em UI e no backend

Padrão de legibilidade usado no projeto:
- Nomes em português quando a equipe e o domínio são em português
- Convenções de estrutura coerentes por módulo
- Imports organizados por camada
- Nenhum arquivo deve acumular História de outro time sem motivo

## 5. Gestão de projetos e sprints

O projeto deve andar em **espiral**: planejar, construir, verificar, revisar riscos.

### 5.1 Abordagem
- Use o PRD/Resumo do projeto como norte
- Escreva histórias de usuário com critérios de aceite claros
- Separe tarefas técnicas das histórias de valor
- Mantenha o escopo de cada sprint pequeno e verificável
- A cada final de sprint, confirme o que está pronto e o que não foi aceito

### 5.2 Critérios de prontidão
- A funcionalidade foi Exercitado
- Os critérios de aceite foram validados
- A interface está consistente com o resto do sistema
- Dados sensíveis ou logística de negócio não foram logados de forma imprudente
- Não há regras duplicadas entre camadas
- O módulo pode ser lido sem precisar abrir 5 arquivos ao mesmo tempo

## 6. Plano de sprints

O plano abaixo é um norte. Ele deve ser revisado a cada ciclo, não tratado como dogma.

### Sprint 1 — Base de acesso e ativos
Foco:
- [[Autenticação e Perfiles]]
- [[Máquinas e Manutenções]]
- [[Equipamentos para Empréstimo]]

Histórias principais:
- Login e cadastro com perfis distintos
- Perfis administrador e técnico com acesso restringido
- Cadastro de máquinas com dados operacionais
- Separar explicitamente emprestáveis de máquinas fixas
- Validações básicas e estados claros no cadastro

Qualidade necessária antes de fechar:
- Fluxo de login e recuperação de sessão verificados
- Cadastro não permite inconsistências óbvias
- Máquinas e equipamentos não se confundem no sistema

### Sprint 2 — Manutenção e rotina de máquina
Foco:
- Manutenções preventivas mensais
- Chamados corretivos
- Alertas e status das máquinas
- Relatório/visual de manutenções

Histórias principais:
- Ciclo preventivo de 30 dias com aviso prévio
- Registro de corretivas com rastreabilidade
- Bloqueio operacional em máquinas em corretiva
- Visão de histórico por máquina e por período

Qualidade necessária antes de fechar:
- O ciclo preventivo dispara nos tempos esperados
- Máquina em corretiva não pode ser usada como produtiva
- O relatório de manutenção reflete o histórico real

### Sprint 3 — Produção e estoque fracionado
Foco:
- Carretéis e gramatura
- Entrada por kg e saída fracionada
- Registro de O.S.
- Isenção de consumo em escaneamento

Histórias principais:
- Cadastro de suprimentos com tara e saldo
- O.S. com débito de insumo em gramas
- O.S. de escaneamento sem débito
- Rastreabilidade obrigatória em produção

Qualidade necessária antes de fechar:
- O saldo muda apenas quando a regra do negócio manda
- O consumo de escaneamento é zero por regra, não por acidente
- O.S. deve carregar técnico, cliente, máquina e tempo

### Sprint 4 — Empréstimo e circulação de equipamentos
Foco:
- Catálogo portátil
- Empréstimo, prazo, atraso, devolução
- Checklist de integridade na devolução

Histórias principais:
- Listagem de emprestáveis
- Fluir retirada com prazo
- Sinalizar atraso
- Protocolo de devolução e liberação

Qualidade necessária antes de fechar:
- Máquinas não aparecem como emprestáveis
- O prazo e o retorno geram estado claro
- A devolução só libera quando o protocolo está completo

### Sprint 5 — Relatórios gerenciais e auditoria
Foco:
- Produção por técnico
- Consumo de estoque
- Empréstimos
- Exportação e logs de auditoria

Histórias principais:
- Recorte mensal por técnico
- Balanço de consumo por tipo de insumo
- Estatísticas de empréstimo por mês
- Exportação e rastreabilidade para prestação de contas

Qualidade necessária antes de fechar:
- Os relatórios refletem os dados consolidados
- O período é parametrizável
- Exportação é útil para auditoria e não apenas cosmética

## 7. Testes de qualidade

Este projeto deve tratar qualidade como **verificação de comportamento**, não como depois de tudo pronto.

### 7.1 Tipos de teste recomendados
- Teste de regras de negócio isoladas
- Teste de transformação de dados e cálculos de saldo/consumo
- Teste de fluxo de manutenção: preventivas, corretivas, bloqueios
- Teste de estado de empréstimo: prazo, atraso, devolução
- Teste de integridade de O.S.: obrigatoriedades e combinações inválidas
- Teste de acesso: perfis errados não conseguem ações proibidas

### 7.2 O que não merece teste complexo
- Renderização decorativa pura
- Detalles de CSS que não mudam o significado da tela
- Estados que só existem para efeito visual sem regra

### 7.3 Quais são os bons alvos do projeto
- Cálculos de consumo fracionado
- Verificação de isenção de escaneamento
- Lógica de ciclo preventivo
- Lógica de estoque mínimo
- Construção de relatórios por período
- Regras de RBAC

## 8. Testes de usabilidade

Usabilidade aqui não é só “ficar bonito”. É o sistema funcionar na bancada, com pressa, sem erro fácil.

### 8.1 O que testar com pessoas
- Login e cadastro são compreensíveis em poucos passos
- Técnico consegue abrir O.S. sem precisar decorar o sistema
- Identificação de máquina e de emprestável é imediata
- Aviso de manutenção é lido antes da operação
- Devolução é clara e o checklist é usado de verdade
- Relatórios entendidos por quem vai tomar decisão

### 8.2 Como testar
- Sessões curtas com personas reais ou próximas delas
- Tarefas com objetivo: “cadastre a máquina”, “registre uma O.S. de impressão”, “devolva um equipamento”
- Observe dúvidas, não só sucesso
- Meça tempo e erros em fluxos críticos
- Valide se os CTAs e avisos têm nível de urgência coerente

### 8.3 Sinais de problemas
- A pessoa não sabe onde registrar a ação
- O sistema permite clique, mas a ação não é a desejada
- O mensagem de erro não diz como recuperar
- O relatório parece bonito mas não responde a pergunta real
- O técnico precisa voltar atrás porque o fluxo foi ambíguo

## 9. Artefatos conectados

- [[PRD e Brief MUSARQ]]
- [[Visão Geral MUSARQ]]
- [[North Star MUSARQ]]
- [[Estrutura de Módulos]]
- [[Plano de Sprints]]
- [[Plano de Testes]]
- [[Checklist de Versão]]

## 10. Como ler este cérebro

- Se você quer entender o produto, comece por [[Visão Geral MUSARQ]] e [[PRD e Brief MUSARQ]]
- Se você vai codar, vá para [[Estrutura de Módulos]] e depois para o módulo específico
- Se vai planejar, use [[Plano de Sprints]]
- Se vai garantir qualidade, use [[Plano de Testes]] e a seção de usabilidade
- Se está revisando uma entrega, use [[Checklist de Versão]]

---
^LerMUSARQCerebro
