# Plano de Issues — SIG-MUSARQ

Use este arquivo como roteiro para criar as issues no GitHub.
Issues já existentes neste repositório:
- #1 `[Feature-0001] - Organização da estrutura` (MERGED)
- #2 `CRIAÇÃO DA TELA DE LOGIN` (OPEN)
- #3 `CRIAÇÃO DA TELA DE CADASTRO` (OPEN)

Observação: o repositório está em `main` e ainda não tem milestones. Se o time quiser, crie milestones por sprint ou por módulo.

---

## Como usar

- Crie as issues seguindo a ordem sugerida dentro de cada frente.
- Meso 과정을 생략하지 마시오: frontend e backend devem ser rastreáveis.
- Se uma issue depender de outra, deixe explícito em “Dependências”.
- Quam necessario, marque:
  - `enhancement` para novas funcionalidades
  - `documentation` para docs, contratos, decisões
  - `bug` se a issue for corrigir comportamento atual
  - `good first issue` se for adequada para alguém entrando agora

---

## Frente: Backend e Domínio

### B01 — Definição do modelo de dados e contratos de API
Entregável:
- Esquema inicial do sistema com entidades de usuário, máquina, suprimento, empréstimo, O.S., manutenção e log de auditoria.
- Definição clara dos campos obrigatórios, tipos e restrições.

Critério de aceite:
- Dá para ler o modelo e saber como diferenciar máquina de emprestável.
- Dá para saber como representar entrada em kg e saída em gramas.
- Dá para saber que O.S. deve conectar técnico, cliente, máquina e tempo.

Dependências:
- #1 como base organizacional
- Revisa RNF05 e RN06 antes de fechar o modelo

---

### B02 — Autenticação e perfis de acesso
Entregável:
- Fluxo de login para Admin e Técnico.
- Política de perfis: Cliente não entra no terminal de gestão.
- Controle de acesso básico nas operações de escrita.

Critério de aceite:
- Só Admin/Técnico conseguem autenticar e escrever.
- Cliente é armazenado, mas não tem acesso operational.
- As decisões de permissão são centralizadas, não espalhadas na UI.

Dependências:
- B01
- Usa RN07 e RN08 como referência principal

---

### B03 — Cadastro de máquinas de bancada
Entregável:
- Criação e listagem de máquinas com dados operacionais e horímetro/status.
- Separação clara entre máquinas fixas e itens passíveis de empréstimo.

Critério de aceite:
- Máquina cadastrada não pode ser usada como emprestável.
- Status da máquina permite identificar se está acessível para produção.

Dependências:
- B01

---

### B04 — Catálogo de equipamentos para empréstimo
Entregável:
- Cadastro de periféricos/saída com código de patrimônio e dados de circulação.
- Distinção explícita entre esse catálogo e máquinas.

Critério de aceite:
- Equipamentos emprestáveis aparecem separados das máquinas.
- Cadastro suporta o necessário para controle de empréstimo e devolução.

Dependências:
- B01
- B03

---

### B05 — Controle de suprimentos e estoque fracionado
Entregável:
- Entrada de suprimentos por kg/L.
- Saída fracionada em gramas/ml.
- Controle de saldo, tara, lote/carretel e estoque baixo.

Critério de aceite:
- O saldo só muda quando a regra do negócio manda.
- Não é possível criar saldo fantasma por operação inconsistente.
- É possível identificar itens abaixo da margem mínima definida.

Dependências:
- B01
- Revisa RN04 e RNF05

---

### B06 — Manutenções preventivas e corretivas
Entregável:
- Registro de preventiva com ciclo de 30 dias e aviso antecipado.
- Registro de corretiva com bloqueio da máquina.
- Historico consultável por máquina/período.

Critério de aceite:
- Preventiva aciona alerta antes do vencimento.
- Corretiva impede nova O.S. até resolução.
- Histórico reflete o que foi registrado.

Dependências:
- B03
- Revisa RN02 e RN03

---

### B07 — Registro de Ordens de Serviço
Entregável:
- Abertura de O.S. com técnico, cliente, máquina, descrição e consumo.
- Suporte a O.S. de escaneamento com consumo zero.
- Rastreabilidade obrigatória mínima.

Critério de aceite:
- O.S. não é finalizada sem os nós obrigatórios.
- Escaneamento não debita insumo.
- O.S. registra máquina e tempo de produção.

Dependências:
- B03
- B05
- Revisa RN05 e RN06

---

### B08 — Fluxo de empréstimo e devolução
Entregável:
- Empréstimo com responsável, prazo e status.
- Devolução com inspeção/checklist e liberação.
- Indicação clara de atraso.

Critère de aceite:
- Máquinas não aparecem no fluxo de empréstimo.
- O status de empréstimo é legível: no prazo, atrasado, devolvido.
- Devolução só libera quando o protocolo está completo.

Dependências:
- B04
- Revisa RN10

---

### B09 — Relatórios gerenciais
Entregável:
- Relatório mensal de produção por técnico.
- Relatório de consumo de estoque.
- Relatório de empréstimos por mês.
- Recorte por período parametrizável.

Critério de aceite:
- Os relatórios respondem perguntas reais do laboratório.
- O período é ajustável.
- Resultado é consistente com os dados consolidados.

Dependências:
- B06
- B07
- B08
- Revisa RN09

---

### B10 — Auditoria e logs de operação
Entregável:
- Registro de eventos relevantes com timestamp, responsável e origem.
- Base para rastreabilidade de manutenção, pesagem e empréstimo.

Critério de aceite:
- É possível saber quem fez o que e quando.
- O log não depende apenas de correções manuais posteriores.

Dependências:
- B01
- Revisa RNF06

---

## Frente: Frontend

### F01 — Arquitetura e convenções da interface
Entregável:
- Organização de pastas/componentes por módulo.
- Convenções de rotas, formulários e estado.
- Pequena base reutilizável para telas administrativas.

Critério de aceite:
- Dá para adicionar uma nova tela sem “decorar” a estrutura todo tempo.
- Componentes têm responsabilidade clara.

Dependências:
- #1

---

### F02 — Tela de login
Entregável:
- Login com seleção de perfil e validação mínima.
- Feedback claro de erro e caminho para cadastro quando aplicável.

Critério de aceite:
- Admin/Técnico encontram o caminho de acesso rapidamente.
- Erros são compreensíveis.

Dependências:
- B02
- #2

---

### F03 — Tela de cadastro
Entregável:
- Cadastro com distinção de perfis e campos adequados.
- Layout coerente com o login.

Critério de aceite:
- Admin/Técnico recebem credenciais.
- Cliente é registrado com os dados necessários, sem acesso operacional.

Dependências:
- B02
- #3

---

### F04 — Dashboard de operação
Entregável:
- Visão rápida com alertas de manutenção, acessos rápidos e status laboratorial.
- Navegação para as ações de bancada.

Critério de aceite:
- Técnico identifica o que precisa de atenção sem dar volta.
- Atalhos levam às telas certas.

Dependências:
- B02
- B03
- B06

---

### F05 — Cadastro e listagem de máquinas
Entregável:
- Formulário e listagem para máquinas.
- Status e filtros suficientes para uso operacional.

Critério de aceite:
- Máquina cadastrada fica visível e consistente.
- A lista ajuda a identificar máquinas críticas.

Dependências:
- B03
- F01

---

### F06 — Catálogo de equipamentos emprestáveis
Entregável:
- Listagem de periféricos autorizados.
- Visual que deixa claro que são emprestáveis, não máquinas.

Critério de aceite:
- A diferença entre máquina e equipamento é visual e sem ambiguidade.

Dependências:
- B04
- F01

---

### F07 — Controle de suprimentos em estoque
Entregável:
- Entrada de insumos e monitoramento de saldo.
- Alerta visual para itens baixos.

Critério de aceite:
- Entrada e saída se entendem rapidamente.
- Estoque baixo chama atenção sem gerar ruído excessivo.

Dependências:
- B05
- F01

---

### F08 — Registro de O.S. e produção
Entregável:
- Formulário de O.S. para impressão e escaneamento.
- Seleção de técnico, cliente, máquina e consumo.
- Feedback quando campos obrigatórios estão faltando.

Critério de aceite:
- A O.S. pode ser aberta sem que o técnico precise decorar o sistema.
- Escaneamento é registrado com consumo zero de forma deliberada.

Dependências:
- B07
- B03
- B05

---

### F09 — Fluxo de empréstimo e devolução
Entregável:
- Retirada com prazo e responsável.
- Devolução com checklist e liberação.
- Sinalização de atraso.

Critério de aceite:
- Técnico sabe qual equipamento está circulando.
- Devolução é clara e protocolo visível.

Dependências:
- B08
- B04

---

### F10 — Relatórios gerenciais na interface
Entregável:
- Telas de relatório por técnico, consumo e empréstimos.
- Filtros por período e exportação útil.

Critério de aceite:
- Relatório não é “bonito por bonito”.
- Exportação ajuda prestação de contas.

Dependências:
- B09
- Revisa RN09

---

## Frente: Infraestrutura e Integração

### I01 — Base de ambiente e acesso seguro
Entregável:
- Separação clara entre dev e produção para variáveis sensíveis.
- Senhas com armazenamento/verificação segura.
- Tráfego protegido com HTTPS em ambientes adequados.

Critério de aceite:
- Credenciais não ficam expostas no código.
- Medições de segurança básicas estão em vigor.

Dependências:
- B02
- Revisa RNF02

---

### I02 — Consistência e resiliência das operações críticas
Entregável:
- Operações de consumo, manutenção e empréstimo tratadas com cuidado transacional/robustez.
- Logs e retentativas adequados para pontos sensíveis.

Critério de aceite:
- Estoque e rastreabilidade não ficam inconsistentes por falha interrompida.
- O sistema não oculta falhas críticas necessárias.

Dependências:
- B05
- B06
- B07
- B08
- Revisa RNF05 e RNF06

---

### I03 — Performance e prontidão do dashboard
Entregável:
- Listas e relatórios com tempo de resposta aceitável à medida que os dados crescem.
- Estratégia para consultas e agregações menores.

Critério de aceite:
- O sistema não vira lento só porque acumula histórico.
- Gráficos e listagens não travam a rotina de bancada.

Dependências:
- B09
- Revisa RNF03

---

### I04 — Disponibilidade e contingência
Entregável:
- Responsividade do serviço durante horário útil.
- Forma básica de manter o sistema disponível e observável.

Critério de aceite:
- A operação não trava por motivos triviais em horário de uso.
- Dá para perceber problemas rapidamente.

Dependências:
- B10
- Revisa RNF04

---

## Sugestão de ordem de trabalho

Ordem mínima sugerida para começar a entregar valor:
1. #1 / F01 / B01 — base e estrutura
2. B02 / F02 / F03 — acesso e cadastro
3. B03 / B04 / F05 / F06 — máquinas e emprestáveis
4. B05 / F07 — suprimentos
5. B06 / F04 — manutenções e visão geral
6. B07 / F08 — O.S. e produção
7. B08 / F09 — empréstimos
8. B09 / F10 — relatórios
9. B10 / I02 / I04 — auditoria e resiliência
10. I01 / I03 — segurança e performance (pode ir andando junto)

---

## O que não é issue agora

- Decoração visual avançada sem impacto no uso.
- Etiquetas de CSS que não mudam comportamento.
- Artefatos de relatório que não respondem a pergunta real do laboratório.

---

Esse plano deve ser ajustado a cada ciclo. Se a equipe quiser, eu posso transformar cada item aqui em issues reais ou gerar um plano de milestone por sprint.
