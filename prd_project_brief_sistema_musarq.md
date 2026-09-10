# Product Requirements Document (PRD) & Project Brief
## Sistema de Gestão do Laboratório de Prototipagem (MUSARQ) — FAU / USP

**Equipe:** 07  
**Produto:** SIG-MUSARQ (Sistema Integrado de Gestão do Laboratório de Prototipagem)  
**Versão:** 2.0 (Consolidada com Protótipo de Alta Fidelidade)  
**Status:** Aprovado para Desenvolvimento / Sprint Planning  
**Metodologia:** Scrum / Kanban  

---

## 1. Sumário Executivo & Visão do Produto

O **SIG-MUSARQ** é uma plataforma web para gestão operacional, rastreabilidade e governança de recursos do Laboratório de Prototipagem Integrada da Faculdade de Arquitetura e Urbanismo (USP). 

O sistema soluciona três gargalos históricos de gestão em laboratórios de fabricação digital acadêmicos:
1. **Diferenciação operacional e patrimonial estrita**: Máquinas pesadas de fabricação (impressoras 3D FDM/SLA e scanners tridimensionais) são bens fixos institucionais e intransponíveis de bancada, enquanto equipamentos móveis e periféricos (mesas digitalizadoras, tablets, sensores, smartphones de teste) são passíveis de empréstimo e circulação externa regulada.
2. **Controle gravimétrico e fracionamento de insumos**: Suprimentos como filamentos termoplásticos (PLA, PETG, ABS) e resinas fotossensíveis são adquiridos institucionalmente por quilograma (kg) ou litro (L), mas consumidos fracionadamente em gramas (g) ou mililitros (ml) por ordem de serviço, exigindo baixa dinâmica em tempo real no inventário.
3. **Ciclos rigorosos de manutenção preventiva e auditoria de produção**: Aplicação mandatória de ciclos de manutenção preventiva a cada 30 dias para todas as máquinas cadastradas (independentemente de defeitos), registro ágil de corretivas com rastreamento de peças e geração de relatórios de produtividade consolidada por operador técnico.

---

## 2. Personas & Perfis de Acesso (RBAC)

| Perfil | Autenticação no Sistema | Papel e Responsabilidades | Principais Casos de Uso |
|---|---|---|---|
| **Administrador** | Sim (E-mail USP / Matrícula) | Gestão executiva e acadêmica, parametrização do laboratório, homologação de máquinas e emissão de relatórios oficiais para órgãos de fomento (FAU, FAPESP, CNPq). | Cadastro de equipamentos, auditoria de manutenções, exportação de indicadores consolidados de custos e desempenho. |
| **Técnico de Laboratório** | Sim (E-mail USP / Matrícula) | Operação direta de bancada no terminal físico, acionamento das máquinas, pesagem de carretéis, abertura de Ordens de Serviço (O.S.) e controle de empréstimos. | Registro de O.S. com débito de filamento, execução de preventivas/corretivas de máquinas, cautela e devolução de periféricos. |
| **Cliente (Discente / Docente / Pesquisador)** | **Não** (Cadastro passivo conforme RN07) | Usuários atendidos pelo laboratório (estudantes de graduação, pós-graduandos e professores da FAU). Não operam o terminal de gestão de máquinas diretamente por motivos de segurança do maquinário. | Vinculação cadastral como demandante em O.S. de corte/impressão e beneficiário de empréstimos temporários de tablets/mesas. |

---

## 3. Matriz de Requisitos Funcionais (RF)

| ID | Módulo | Requisito Funcional | Descrição Detalhada | Critérios de Aceite |
|---|---|---|---|---|
| **RF01** | Autenticação | Login de Usuário | Permitir login seguro dos perfis Administrador e Técnico via matrícula USP ou e-mail institucional e senha. | Bloqueio de clientes; retenção opcional de sessão em terminal de bancada. |
| **RF02** | Autenticação | Cadastro de Usuário | Cadastro de administradores, técnicos e clientes (alunos/pesquisadores vinculados à unidade acadêmica). | Perfis Técnico/Admin recebem credenciais; Cliente armazena matrícula/curso/vínculo. |
| **RF03** | Máquinas | Cadastro de Máquinas | Registro de impressoras 3D (FDM, SLA) e scanners tridimensionais com especificações técnicas e horímetro. | Impede marcação de empréstimo para máquinas cadastradas (RN01). |
| **RF04** | Estoque | Cadastro de Suprimentos 3D | Cadastro de insumos comprados em kg/litro, com controle de carretéis ativos e saldo fracionado em gramas. | Rastreabilidade de lote, peso da tara e saldo remanescente em tempo real. |
| **RF05** | Manutenção | Gestão de Manutenções | Registro e controle de manutenções preventivas mensais (ciclo 30 dias) e chamados corretivos imediatos. | Checklist obrigatório de lubrificação, alinhamento e peças trocadas. |
| **RF06** | Manutenção | Relatórios & Gráficos de Manutenção | Visualização gráfica de histórico de intervenções preventivas vs corretivas por período e equipamento. | Filtros por data, máquina e tipo; cálculo de MTBF e taxa de disponibilidade. |
| **RF07** | Empréstimos | Cadastro de Equipamentos de Saída | Cadastro de periféricos autorizados para circulação externa (tablets, mesas digitalizadoras, celulares de depuração). | Código de patrimônio (TAG PAT), estojo de transporte e acessórios inclusos. |
| **RF08** | Empréstimos | Gestão de Empréstimos e Devoluções | Controle de cautela e devolução com identificação do solicitante, técnico responsável, data de retirada e prazo. | Indicação em tempo real de status: No Prazo, Atrasado, Devolvido (RN10). |
| **RF09** | Produção | Registro de O.S. e Produção | Emissão de ordem de serviço vinculando peça/projeto, técnico, cliente, máquina, insumo fracionado e tempo de máquina. | Suporte a consumo zero (0 g) para trabalhos de escaneamento 3D (RN05). |
| **RF10** | Relatórios | Relatório Mensal por Técnico | Consolidação mensal da quantidade de peças produzidas, horas em operação e taxa de produtividade por técnico. | Gráfico comparativo e detalhamento nominal para dimensionamento de escala de trabalho. |
| **RF11** | Relatórios | Relatório de Consumo de Estoque | Balanço mensal de material consumido (kg/g e ml) por tipologia (PLA, PETG, ABS, Resina) e peças descartadas. | Alerta visual para insumos com estoque abaixo da margem de segurança (<150g). |
| **RF12** | Relatórios | Relatório Mensal de Empréstimos | Histórico e estatísticas de utilização de periféricos por mês, taxas de rotatividade e registros de atraso. | Exportação formatada para auditoria acadêmica e prestação de contas. |

---

## 4. Regras de Negócio Invioláveis (RN)

* **RN01 — Não Emprestabilidade de Máquinas:** Máquinas de prototipagem (impressoras 3D, scanners de bancada, cortadoras a laser) são bens permanentes fixos do laboratório. É terminantemente proibido cadastrar ou emitir empréstimos desses itens para fora da bancada operacional. Apenas periféricos cadastrados no módulo de empréstimo (RF07) podem sair do laboratório.
* **RN02 — Periodicidade Preventiva Mensal Mandatória:** Toda máquina cadastrada possui ciclo preventivo obrigatório com periodicidade máxima de 30 dias corridos, independentemente de apresentar ou não falhas. O sistema aciona alerta crítico amarelo/vermelho 3 dias antes do vencimento da preventiva.
* **RN03 — Manutenção Corretiva Imediata:** Manutenções corretivas podem ser deflagradas a qualquer momento mediante registro de anomalia, bloqueando imediatamente a máquina para novas Ordens de Produção até a finalização do reparo.
* **RN04 — Entrada em Quilo e Saída Fracionada (Gravimétrica):** Suprimentos de impressão 3D são adquiridos formalmente por quilograma (kg), porém debitados das bobinas em gramas (g) ou miligramas de acordo com a fatiação do arquivo `.GCODE`/`.3MF`.
* **RN05 — Isenção de Consumo em Escaneamento Tridimensional:** Para Ordens de Serviço cujo processo seja de digitalização/escaneamento tridimensional, o campo de consumo de filamento é registrado compulsoriamente como **0 g / Isento**, sem debitar carretéis de insumos.
* **RN06 — Rastreabilidade Quádrupla Obrigatória em O.S.:** Nenhuma produção é iniciada ou concluída sem associação estrita a 4 nós de dados: (1) Técnico Operador, (2) Cliente/Demandante, (3) Máquina Alocada e (4) Tempo de Produção.
* **RN07 — Isolamento de Acesso do Cliente:** Discentes e docentes na categoria *Cliente* não possuem acesso com senha ao terminal de gestão. Seu cadastro existe para identificação unívoca de autoria do projeto e garantia de custódia em empréstimos.
* **RN08 — Restrição de Autenticação RBAC:** Apenas credenciais com papéis *Técnico* e *Administrador* têm permissão para autenticar-se e realizar operações de escrita no sistema.
* **RN09 — Parametrização Temporal de Relatórios:** Todos os relatórios gerenciais e de auditoria devem permitir recorte parametrizado por Mês/Ano de referência com consolidação automática de métricas.
* **RN10 — Protocolo e Devolução Obrigatória:** O encerramento de um empréstimo exige inspeção de integridade física dos conectores e telas, registro de devolução no sistema e liberação imediata do ativo para a fila de espera.

---

## 5. Requisitos Não-Funcionais & Arquitetura Técnica (RNF)

* **RNF01 (Usabilidade & Ergonomia de Bancada):** Interface limpa, com tipografia legível a distância de bancada, botões de toque generosos e navegação simplificada sem ruído visual.
* **RNF02 (Segurança & Criptografia):** Senhas com hash criptográfico PBKDF2 / Argon2, proteção contra injeção de parâmetros e tráfego criptografado com protocolo TLS 1.3.
* **RNF03 (Performance & Throughput):** Renderização de listagens e gráficos em menos de 1,2s, mesmo com histórico acumulado de milhares de O.S. e logs de manutenção.
* **RNF04 (Disponibilidade & Contingência):** Disponibilidade mínima de 99,5% no período útil de funcionamento da unidade acadêmica (08h00 às 20h00).
* **RNF05 (Consistência Gravimétrica Transacional):** Operações de baixa de filamento e cancelamento de O.S. devem possuir consistência transacional ACID para evitar saldos fantasmas de insumos.
* **RNF06 (Auditabilidade & Rastreabilidade — RNF08):** Todo registro de manutenção, pesagem de carretel e cautela gera log indelével contendo timestamp, IP de bancada e matrícula do técnico operador.

---

## 6. Mapeamento das Telas do Sistema (Protótipo Implementado)

| Código da Tela | Título da Tela | Objetivo e Funcionalidades Principais |
|---|---|---|
| **SCREEN_2** | *Login e Cadastro Simplificado* | Acesso minimalista e intuitivo com seleção de perfil (Técnico / Administrador), validação de matrícula USP, alternador de aba para novo cadastro e suporte a alunos. |
| **SCREEN_13** | *Dashboard & Visão Geral da Operação* | Centro de comando com horímetro de bancada, indicadores de trabalhos ativos (FDM/SLA/Scanners), atalhos rápidos para nova O.S., cautela e alertas de manutenção RN02. |
| **SCREEN_9** | *Máquinas & Manutenções* | Catálogo visual de impressoras e scanners, status operacional em tempo real, disparador de preventivas mensais e comparativo histórico entre preventivas e corretivas. |
| **SCREEN_11** | *Produção & Insumos Fracionados* | Calculadora de abatimento gravimétrico de carretéis, monitoramento de bobinas em bancada, alerta de estoque mínimo (<150g) e tabela de O.S. com isenção para escaneamentos. |
| **SCREEN_7** | *Empréstimos de Equipamentos* | Painel segregado de periféricos autorizados (sem máquinas de corte), controle de prazos e atrasos, checklist de integridade de devolução e assinatura de protocolo. |
| **SCREEN_5** | *Relatórios Gerenciais* | Consolidação mensal por técnico operador, taxa de impressões sem falhas (96.4%), balanço de consumo de filamentos e exportação com autenticação digital para auditoria acadêmica. |

---

## 7. Roadmap de Implementação (Sprints Sugeridas)

1. **Sprint 1 — Core Auth & Gestão de Ativos (RF01, RF02, RF03, RF07, RN01, RN08):**
   * Estruturação do banco de dados relacional (PostgreSQL).
   * Implementação do fluxo de login e cadastro com RBAC estrito.
   * Módulos de cadastro de máquinas de bancada e equipamentos portáteis de empréstimo.
2. **Sprint 2 — Manutenções & Rotinas Periódicas (RF05, RF06, RN02, RN03):**
   * Motor de regras para ciclo de manutenção preventiva de 30 dias com alertas no Dashboard.
   * Registro de chamados corretivos e formulário de checklist com histórico.
3. **Sprint 3 — Produção & Estoque Fracionado (RF04, RF09, RN04, RN05, RN06):**
   * Controle de carretéis e balança de precisão integrada (ou entrada manual de tara e peso líquido).
   * Emissão de O.S. de impressão 3D (com débito em gramas) e escaneamento (consumo 0 g).
4. **Sprint 4 — Empréstimos & Circulação de Periféricos (RF08, RN10):**
   * Fluxo completo de empréstimo, cálculo de prazos com sinalização de atrasos e protocolo de devolução.
5. **Sprint 5 — Relatórios & Auditoria Executiva (RF10, RF11, RF12, RN09, RNF08):**
   * Dashboards analíticos mensais, exportação em CSV/PDF e log completo de auditoria para fomento acadêmico.
