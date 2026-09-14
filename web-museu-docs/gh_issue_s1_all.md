# Sprint 1 — Issues de equipe

Use este arquivo para criar as issues de Sprint 1 com divisão por frente.

---

## Frontend

Título:
```
[Sprint 1] [F01] Front: estrutura de pastas, base reutilizável e protótipos iniciais
```

Body pronto:
```
## Objetivo
Estruturar a frente frontend e entregar a base que o time pode usar nos próximos passos.

## Responsável
Frontend / frontend duo

## O que entregar
- Estrutura de pastas do frontend
- Componentes/base pequenos e reutilizáveis
- Protótipo de tela de login
- Protótipo de tela de cadastro
- Definição de como estado e rotas vão ser organizados

## Critério de aceite
- Dá para adicionar uma nova tela sem dificuldade desnecessária
- Componentes são reutilizáveis quando faz sentido
- Telas do protótipo ajudam a validar ideia, não só “estar lá”
- Front não assume backend pronto sem definir como vai lidar com isso

## Dependências
- Projeto e documentação: definição de convenções
- Backend: maneira de comunicação preparada ou pelo menos definida

## Regras e requisitos de referência
- RNF01
- RN07
- RN08

## Como validar
1. Criar uma nova tela nova no esquema definido
2. Verificar que componentes são reutilizáveis
3. Verificar que protótipos funcionam para validação
4. Confirmar que frontend sabe como lidar com backend não pronto

## Decisões pendentes
- Tecnologia/framework exata do frontend
- Forma de comunicação com backend
- Estado global versus local
```

---

## Backend

Título:
```
[Sprint 1] [M01] Back: definição inicial de backend e contratos com frontend
```

Body pronto:
```
## Objetivo
Definir a base da frente backend e alinhar como ela vai conversar com frontend.

## Responsável
Backend / backend duo

## O que entregar
- Decisão inicial sobre backend
- Definição de como as operações principais são acionadas
- Rascunho de contratos entre frontend e backend
- Base para Firebase ou outra solução, se for essa a escolha

## Critério de aceite
- Dá para saber como backend vai ser acionado
- Dá para saber o que backend deve garantir sozinho
- Backend não depende de adivinhação da equipe
- Fica claro o que será feito no cliente e o que não pode ser

## Dependências
- Projeto e documentação: convenções e decisões
- Banco de dados: modelo suficiente para conversar contratos

## Regras e requisitos de referência
- RN06
- RN07
- RN08
- RNF02

## Como validar
1. Escolher uma operação e explicar como backend a trata
2. Escrever um contrato preliminar para essa operação
3. Confirmar que regras críticas não ficam apenas no cliente
4. Confirmar que frontend sabe o que esperar

## Decisões pendentes
- Firebase será base primária ou só parte do sistema
- Quais products do Firebase serão usados
- Se haverá backend separado para regras críticas
- Como serão gerenciados perfis
```

---

## Banco de dados

Título:
```
[Sprint 1] [M02] Data: modelo inicial das entidades principais
```

Body pronto:
```
## Objetivo
Modelar as entidades principais e deixar claro como o dado será organizado.

## Responsável
Banco de dados / data duo

## O que entregar
- Modelo inicial das entidades principais
- Definição de campos obrigatórios
- Separação entre máquina, equipamento, suprimento, manutenção, O.S., empréstimo e auditoria
- Pequena nota sobre consistência de saldo e operações críticas

## Critério de aceite
- Dá para ler o modelo e entender o sistema
- Dá para identificar como cada entidade se relaciona
- Dá para entender onde pode vir saldo inconsistente
- Modelo suporta conversa com backend e frontend

## Dependências
- Projeto e documentação: convenções e tipo de backend
- Backend: formato aceitável para contratos

## Regras e requisitos de referência
- RN01
- RN04
- RN05
- RN06
- RNF05
- RNF06

## Como validar
1. Ler o modelo e responder: “uma máquina pode ser emprestada?”
2. Ler o modelo e responder: “uma O.S. de escaneamento pode debitar insumo?”
3. Ler o modelo e responder: “é possível gerar saldo inconsistente?”
4. Conferir que informações de auditoria básica estão previstas

## Decisões pendentes
- Banco escolhido
- Se modelo inicial será normalizado ou com ajustes para relatórios
- Se auditoria vira entidade própria ou decorrente
- Nomes das tabelas ou coleções adotados
```

---

## Projeto e documentação

Título:
```
[Sprint 1] [P01] Projeto: README, legenda de issues e roteiro de equipe
```

Body pronto:
```
## Objetivo
Organizar o projeto, a documentação e o padrão de trabalho da equipe.

## Responsável
Projeto / documentação duo

## O que entregar
- README atualizado com visão rápida do projeto
- Legenda de nomenclatura de issues
- Roteiro de issues atualizado
- Pequena nota de decisões pendentes

## Critério de aceite
- Dá para saber onde está a documentação do projeto
- Dá para entender como criar e ler novas issues
- Dá para saber o que ainda não foi decidido
- A equipe tem um ponto claro de referência

## Dependências
- Todas as frentes, para saber o que está acontecendo

## Regras e requisitos de referência
- N/A para esta frente, mas relacionado a toda a organização do projeto

## Como validar
1. Abrir o repositório e achar a documentação principal
2. Criar uma issue novo usando o padrão definido
3. Ler o roteiro e entender onde cada frente deve atuar
4. Confirmar que as coisas não decididas estão explícitas

## Decisões pendentes
- Onde fica o projeto no GitHub
- Quais convenções serão obrigatórias
- Como o time vai registrar decisões pequenas
```

---

## Prototipagem e validação

Título:
```
[Sprint 1] [T01] Proto: protótipos de fluxos principais para validação rápida
```

Body pronto:
```
## Objetivo
Criar protótipos que ajudem a validar fluxos principais sem construir tudo.

## Responsável
Prototipagem / validação duo

## O que entregar
- Protótipos de fluxos principais
- Vista de telas como login, cadastro e catálogo inicial
- Registro do que foi testado e o que ainda não foi

## Critério de aceite
- Protótipos ajudam a tomar decisões, não só ocupar lugar
- Dá para ver fluxos principais antes de implementação completa
- Protótipos não se tornam fonte da verdade sobre regras

## Dependências
- Frontend: estrutura e componentes suficientes para prototipar
- Backend: se necessário, contrato ou plano de contrato
- Projeto e documentação: para saber o que deve ser válido

## Regras e requisitos de referência
- RNF01
- RN01

## Como validar
1. Escolher um fluxo e prototipar a jornada principal
2. Conferir que o fluxo ajuda a decidir mais do que atrapalha
3. Registrar o que ficou claro e o que ficou ambíguo
4. Deixar claro que protótipo não define regra

## Decisões pendentes
- Qual a diferença entre protótipo e implementação real
- O que deve ser feito só para validar ideia
- O que pode ser ignorado nessa sprint
```

---

## Coordenação da sprint

Título:
```
[Sprint 1] [S01] Sprint 1: divisão de frentes, checkpoint e entrega mínima
```

Body pronto:
```
## Objetivo
Definir como a Sprint 1 será organizada entre as frentes e o que cada uma entrega.

## Responsável
Equipe como um todo, com coordenação definida

## O que entregar
- Divisão das frentes: projeto, frontend, backend, banco, prototipagem
- Checkpoint de início e de fim de sprint
- Lista do que cada frente entrega e do que ainda está pendente

## Critério de aceite
- Dá para saber quem é responsável por cada frente
- Dá para saber o que cada frente deve entregar
- Dá para saber como saber se a sprint acabou

## Dependências
- Todas as demais issues da Sprint 1

## Regras e requisitos de referência
- N/A para esta frente, mas ela sustenta o resto

## Como validar
1. Reunir os responsáveis das frentes
2. Definir checkpoint de início e fim
3. Registrar o que cada frente vai entregar
4. Confirmar que ninguém está trabalhando sem alinhamento

## Decisões pendentes
- Quem coordena a sprint
- Como será o acompanhamento diário ou pontual
- O que acontece se uma frente atrasar
```
