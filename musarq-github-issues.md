# MUSARQ — Issues prontas para subir no GitHub

Rascunho de criação para o repositório:
- https://github.com/quezinhacosta/teste-aula-agil/issues

Issues já existentes (para não duplicar):
- #1 `[Feature-0001] - Organização da estrutura` → MERGED
- #2 `CRIAÇÃO DA TELA DE LOGIN` → OPEN
- #3 `CRIAÇÃO DA TELA DE CADASTRO` → OPEN

---

## Como criar

Para cada issue abaixo, use algo como:

```bash
gh issue create \
  --title "<TÍTULO>" \
  --body-file "<ARQUIVO_COM_BODY>" \
  --label "enhancement" \
  --assignee "" \
  --milestone ""
```

Ou crie diretamente pelo GitHub usando o mesmo título e corpo do markdown abaixo.

Se preferir, posso criar todas de uma vez com `gh issue create` a partir deste roteiro.

---

## Backlog organizado por frente

### 1. Base e estrutura do sistema

#### M01 — Definição do modelo de dados e contratos iniciais
Tipo: backend + documentação
Rascunho de título:
```
[M01] Modelo de dados e contratos iniciais do SIG-MUSARQ
```
Corpo plano:
```
## Objetivo
Definir o modelo inicial do sistema e os contratos usados entre frontend e backend.

## O que entregar
- Entidades principais: usuário, máquina, suprimento, empréstimo, O.S., manutenção, log.
- Campos obrigatórios e tipos básicos.
- Separação clara entre máquina de bancada e equipamento emprestável.
- Como representar entrada em kg e saída em gramas.
- Como representar O.S. com consumo zero para escaneamento.

## Critério de aceite
- [ ] Dá para identificar máquina e emprestável sem ambiguidade.
- [ ] Dá para entender como o estoque fracionado funciona no modelo.
- [ ] Dá para entender quais dados uma O.S. precisa obrigatoriamente.
- [ ] O modelo serve de referência para backend e frontend.

## Dependências
- #1 como base organizacional.

## Regras de referência
- RN01, RN04, RN05, RN06, RNF05

## Como validar
1. Ler o modelo e responder: “uma máquina pode ser emprestada?”
2. Ler o modelo e responder: “uma O.S. de escaneamento pode debitar filamento?”
3. Confirmar que os campos obrigatórios estão identificados.
```

---

#### M02 — Fronteira entre frontend e backend
Tipo: documentação + coordenação
Rascunho de título:
```
[M02] Fronteira e convenções entre frontend e backend
```
Corpo plano:
```
## Objetivo
Avisar como as duas frentes vão conversar, para não criar trabalho duplicado ou regras espalhadas.

## O que entregar
- Onde fica cada responsabilidade: validação, regras de negócio, estado, UI.
- Convenção de erro e mensagem de retorno.
- Convenção de campos compartilhados entre telas e API.

## Critério de aceite
- [ ] Frontend sabe o que não deve repetir do backend.
- [ ] Backend sabe o que deve garantir sozinho.
- [ ] Dá para adicionar uma nova tela/requisito sem reescrever a regra em dois lugares.

## Dependências
- M01
- #1

## Regras de referência
- RN06, RN07, RN08

## Como validar
1. Escolher uma regra de negócio e dizer onde está implementada.
2. Confirmar que a interface não replica a mesma regra de forma separada.
```

---

### 2. Autenticação e cadastro

#### M03 — Autenticação e perfis de acesso
Tipo: backend + parte de frontend
Rascunho de título:
```
[M03] Login e perfis de acesso Admin / Técnico / Cliente
```
Corpo plano:
```
## Objetivo
Permitir acesso ao sistema apenas para Admin e Técnico, com cliente como cadastro passivo.

## O que entregar
- Login para Admin e Técnico.
- Política de perfil: cliente não acessa o terminal de gestão.
- Controle de acesso nas operações de escrita.

## Critério de aceite
- [ ] Apenas Admin e Técnico conseguem autenticar e operar.
- [ ] Cliente é registrado, mas não tem acesso operative.
- [ ] As regras de permissão estão centralizadas.

## Dependências
- M01
- M02

## Regras de referência
- RF01, RF02, RN07, RN08

## Como validar
1. Tentar acessar com perfil inadequado e confirmar bloqueio.
2. Verificar que credenciais válidas levam ao fluxo certo.
3. Confirmar que cliente não opera gestão de máquinas.
```

---

#### M04 — Tela de login
Tipo: frontend
Rascunho de título:
```
[F04] Tela de login do SIG-MUSARQ
```
Corpo plano:
```
## Objetivo
Entregar a tela de login com perfil, validação e feedback claro.

## O que entregar
- Seleção de perfil quando aplicável.
- Validação mínima e mensagens compreensíveis.
- Caminho claro para cadastro quando relevante.

## Critério de aceite
- [ ] Admin e Técnico encontram o acesso rapidamente.
- [ ] Erros são legíveis.
- [ ] A tela é coerente com o restante do sistema.

## Dependências
- M03
- #2

## Regras de referência
- RNF01, RN08

## Como validar
1. Tentar login com dados inválidos e ler a mensagem.
2. Acessar com perfil correto e verificar redirecionamento/estado.
```

---

#### M05 — Tela de cadastro
Tipo: frontend
Rascunho de título:
```
[F05] Tela de cadastro de usuários
```
Corpo plano:
```
## Objetivo
Criar cadastro com distinção de perfis e campos adequados.

## O que entregar
- Diferença de campos conforme perfil.
- Layout coerente com login.
- Cliente cadastrado sem acesso operacional.

## Critério de aceite
- [ ] Admin/Técnico recebem credenciais.
- [ ] Cliente é registrado com os dados necessários.
- [ ] O cadastro não abre acesso indevido.

## Dependências
- M03
- #3

## Regras de referência
- RF02, RN07

## Como validar
1. Cadastrar cada perfil e verificar o que foi criado.
2. Confirmar que cliente não recebe acesso ao terminal de gestão.
```

---

### 3. Ativos e equipamentos

#### M06 — Cadastro de máquinas de bancada
Tipo: backend + frontend
Rascunho de título:
```
[M06] Cadastro e status de máquinas de bancada
```
Corpo plano:
```
## Objetivo
Cadastrar impressoras e scanners como máquinas fixas do laboratório.

## O que entregar
- Cadastro com dados operacionais e status/horímetro quando aplicável.
- Diferença clara entre máquina e emprestável.
- Máquina bloqueada não deve ser usada para produção.

## Critério de aceite
- [ ] Máquina não pode ser marcada como emprestável.
- [ ] Status da máquina ajuda na operação.
- [ ] O cadastro não permite confusão óbvia com equipamento de saída.

## Dependências
- M01

## Regras de referência
- RF03, RN01, RN03

## Como validar
1. Criar máquina e confirmar que ela não aparece como emprestável.
2. Alterar status e verificar impacto na operação.
```

---

#### M07 — Catálogo de equipamentos para empréstimo
Tipo: backend + frontend
Rascunho de título:
```
[M07] Catálogo de equipamentos emprestáveis
```
Corpo plano:
```
## Objetivo
Cadastrar periféricos que podem circular fora do laboratório.

## O que entregar
- Código de patrimônio e dados úteis para empréstimo/devolução.
- Catálogo separado das máquinas.
- Visual que identifica rapidamente o que pode sair.

## Critério de aceite
- [ ] Equipamentos emprestáveis aparecem separados das máquinas.
- [ ] Cadastro suporta o necessário para controle de empréstimo.
- [ ] A ambiguidade entre máquina e periférico é baixa.

## Dependências
- M01
- M06

## Regras de referência
- RF07, RN01

## Como validar
1. Listar máquinas e equipamentos e confirmar separação.
2. Criar um emprestável e verificar que ele entra no catálogo certo.
```

---

### 4. Estoque e produção

#### M08 — Suprimentos e estoque fracionado
Tipo: backend + frontend
Rascunho de título:
```
[M08] Controle de suprimentos e estoque fracionado
```
Corpo plano:
```
## Objetivo
Controlar insumos comprados por kg/L e usados em frações.

## O que entregar
- Entrada por kg/L.
- Saída em gramas/ml.
- Controle de saldo, tara, lote/carretel.
- Alerta para estoque baixo.

## Critério de aceite
- [ ] O saldo só muda quando a regra manda.
- [ ] Não é possível gerar saldo fantasma por operação inconsistente.
- [ ] Itens abaixo da margem mínima são identificados.

## Dependências
- M01

## Regras de referência
- RF04, RN04, RNF05

## Como validar
1. Registrar entrada e saída e conferir saldo final.
2. Tentar operação inconsistente e confirmar bloqueio/alerta.
```

---

#### M09 — Registro de Ordens de Serviço
Tipo: backend + frontend
Rascunho de título:
```
[M09] Registro de O.S. e produção
```
Corpo plano:
```
## Objetivo
Permitir registrar produção com rastreabilidade completa.

## O que entregar
- O.S. com técnico, cliente, máquina, descrição e consumo.
- Suporte a O.S. de escaneamento com consumo zero.
- Validações de campos obrigatórios.

## Critério de aceite
- [ ] O.S. não é finalizada sem nós obrigatórios.
- [ ] Escaneamento fica com consumo zero por regra.
- [ ] O.S. registra máquina e tempo de produção.

## Dependências
- M01
- M06
- M08

## Regras de referência
- RF09, RN05, RN06

## Como validar
1. Criar O.S. de impressão e conferir débito.
2. Criar O.S. de escaneamento e confirmar consumo zero.
3. Tentar salvar O.S. incompleta e verificar validação.
```

---

### 5. Manutenção

#### M10 — Manutenções preventivas e corretivas
Tipo: backend + frontend
Rascunho de título:
```
[M10] Ciclo de manutenção preventiva e corretivas
```
Corpo plano:
```
## Objetivo
Gerenciar manutenção obrigatória mensal e chamados corretivos.

## O que entregar
- Preventiva com ciclo de 30 dias e alerta antecipado.
- Corretiva com bloqueio da máquina.
- Histórico por máquina/período.

## Critério de aceite
- [ ] Preventiva aciona alerta antes do vencimento.
- [ ] Corretiva impede nova O.S. até resolução.
- [ ] Histórico reflete o registrado.

## Dependências
- M01
- M06

## Regras de referência
- RF05, RF06, RN02, RN03

## Como validar
1. Marcar preventiva e conferir alerta próximo ao vencimento.
2. Abrir corretiva e verificar bloqueio da máquina.
3. Consultar histórico e confirmar legibilidade.
```

---

### 6. Empréstimos

#### M11 — Empréstimo e devolução de equipamentos
Tipo: backend + frontend
Rascunho de título:
```
[M11] Fluxo de empréstimo e devolução
```
Corpo plano:
```
## Objetivo
Controlar circulação de equipamentos com prazo, atraso e protocolo de devolução.

## O que entregar
- Empréstimo com responsável, prazo e status.
- Devolução com checklist/inspeção e liberação.
- Sinalização de atraso.

## Critério de aceite
- [ ] Máquinas não aparecem no fluxo de empréstimo.
- [ ] Status é legível: no prazo, atrasado, devolvido.
- [ ] Devolução só libera quando o protocolo está completo.

## Dependências
- M07

## Regras de referência
- RF08, RN10

## Como validar
1. Criar empréstimo e conferir status inicial.
2. Atrasar o prazo e verificar sinalização.
3. Finalizar devolução e confirmar liberação.
```

---

### 7. Relatórios e auditoria

#### M12 — Relatórios gerenciais
Tipo: backend + frontend
Rascunho de título:
```
[M12] Relatórios gerenciais mensais
```
Corpo plano:
```
## Objetivo
Fornecer visão consolidada para coordenação e prestação de contas.

## O que entregar
- Produção por técnico.
- Consumo de estoque.
- Empréstimos por mês.
- Filtro por período parametrizável.
- Exportação útil para auditoria.

## Critério de aceite
- [ ] Os relatórios respondem perguntas reais do laboratório.
- [ ] O período é ajustável.
- [ ] Resultado é consistente com os dados.

## Dependências
- M10
- M09
- M11

## Regras de referência
- RF10, RF11, RF12, RN09

## Como validar
1. Abrir relatório por período e conferir consistência.
2. Exportar e verificar se o resultado é interpretável fora do sistema.
```

---

#### M13 — Auditoria e logs de operação
Tipo: backend
Rascunho de título:
```
[M13] Auditoria e logs de operação
```
Corpo plano:
```
## Objetivo
Rastrear quem fez o quê, quando e de onde em operações críticas.

## O que entregar
- Log de eventos relevantes com timestamp, responsável e origem.
- Base para manutenção, pesagem e empréstimo.

## Critério de aceite
- [ ] É possível saber quem fez a operação e quando.
- [ ] O registro não depende apenas de correções manuais posteriores.

## Dependências
- M01

## Regras de referência
- RNF06

## Como validar
1. Realizar uma operação crítica e conferir o registro.
2. Confirmar que os dados de auditoria estão presentes.
```

---

### 8. Infraestrutura e qualidade

#### M14 — Segurança básica e ambientes
Tipo: infra + backend
Rascunho de título:
```
[I01] Base de ambiente e acesso seguro
```
Corpo plano:
```
## Objetivo
Manter credenciais e tráfego em condições adequadas.

## O que entregar
- Separação entre dev e produção para variáveis sensíveis.
- Senhas com armazenamento/verificação segura.
- HTTPS em ambientes adequados.

## Critério de aceite
- [ ] Credenciais não ficam expostas no código.
- [ ] Medidas básicas de segurança estão em vigor.

## Dependências
- M03

## Regras de referência
- RNF02

## Como validar
1. Verificar que variáveis sensíveis não estão versionadas.
2. Confirmar proteção básica no fluxo de autenticação.
```

---

#### M15 — Consistência nas operações críticas
Tipo: backend + infra
Rascunho de título:
```
[I02] Consistência e resiliência nas operações críticas
```
Corpo plano:
```
## Objetivo
Evitar inconsistência em consumo, manutenção e empréstimo.

## O que entregar
- Tratamento robusto para operações sensíveis.
- Logs e comportamento adequados em caso de erro.

## Critério de aceite
- [ ] Estoque e rastreabilidade não ficam inconsistentes por falha.
- [ ] O sistema não esconde falhas críticas.

## Dependências
- M08
- M10
- M09
- M11

## Regras de referência
- RNF05, RNF06

## Como validar
1. Simular falha durante operação crítica.
2. Confirmar estado final consistente ou com aviso claro.
```

---

#### M16 — Performance e prontidão do dashboard
Tipo: backend + frontend
Rascunho de título:
```
[I03] Performance e prontidão do dashboard
```
Corpo plano:
```
## Objetivo
Manter listas e relatórios responsivos conforme os dados crescem.

## O que entregar
- Estratégia para consultas e agregações.
- Dashboards e listagens aceitáveis em uso real.

## Critério de aceite
- [ ] O sistema não fica lento só por acumular histórico.
- [ ] Gráficos e listagens não travam a rotina de bancada.

## Dependências
- M12

## Regras de referência
- RNF01, RNF03

## Como validar
1. Medir tempo de resposta em operações frequentes.
2. Confirmar que dashboard e listas continuam utilizáveis.
```

---

#### M17 — Disponibilidade no horário útil
Tipo: infra
Rascunho de título:
```
[I04] Disponibilidade e contingência no horário de uso
```
Corpo plano:
```
## Objetivo
Manter o sistema responsivo durante o horário útil do laboratório.

## O que entregar
- Forma básica de observabilidade e contingência.
- Prática para perceber problemas rapidamente.

## Critério de aceite
- [ ] A operação não trava por motivos triviais em horário de uso.
- [ ] Dá para identificar problemas rapidamente.

## Dependências
- M13

## Regras de referência
- RNF04

## Como validar
1. Verificar monitoramento/observabilidade básica.
2. Confirmar que falhas têm caminho claro de diagnóstico.
```

---

## Ordem sugerida para o time

Ordem prática para começar a entregar valor:
1. M01 + M02 + M04 + M05
2. M03 + M06 + M07
3. M08 + M09
4. M10
5. M11
6. M12 + M13
7. I01 + I02 + I03 + I04

Essa ordem pode ser ajustada pela equipe, mas não inverter dependências óbvias.

---

## O que não precisa virar issue agora

- Polir aparência sem impacto no uso.
- Detales de CSS que não mudam o comportamento.
- Relatórios bonitos que não respondem pergunta real do laboratório.

---

Se quiser, eu posso:
- criar as issues diretamente no GitHub com `gh`;
- gerar milestones por sprint;
- agrupar em project no GitHub, se o time usar.
