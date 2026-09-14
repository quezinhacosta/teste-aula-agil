# Sprint 1 — Divisão de Responsabilidades

Objetivo da Sprint 1:
- Delimitar o projeto
- Criar estrutura inicial do repositório
- Montar prototipagem e base frontal
- Definir risca de backend e banco

A ideia não é que cada um codifique tudo, mas que cada um responsabilize uma frente e deixe claro o que entrega.

---

## 1. Fronteira do time

Sugestão de divisão por frente:

- Front
  - estrutura de pastas do frontend
  - componentes/base reutilizável
  - protótipos de telas principais
- Backend
  - definição inicial do backend
  - contratos iniciais
  - integração com Firebase, se for essa a escolha
- Banco de dados
  - modelo inicial
  - esquema de entidades principais
  - regras de consistência básica
- Projeto
  - README
  - legenda de issues
  - roteiro de issues
  - regras de projeto e nomenclatura
- Prototipagem
  - telas de apoio ao entendimento e ao planejamento
  - funcionalidade limitada, focada na validação rápida

---

## 2. Frente: Projeto e Documentação

Responsável: pessoa ou par

Entregáveis sugeridos:
- README atualizado com visão rápida do projeto
- Legenda de nomenclatura de issues
- Roteiro de issues atualizado
- Pequena nota de decisões pendentes

Critério de aceite:
- Dá para saber onde está a documentação do projeto
- Dá para entender como criar e ler novas issues
- Dá para saber o que ainda não foi decidido

Questões para responder:
- Onde fica o projeto no GitHub
- Queixa de documentação é obrigatória
- Qual a convenção de commits e branches, se houver

---

## 3. Frente: Frontend

Responsável: pessoa ou par

Entregáveis sugeridos:
- Estrutura de pastas do frontend
- Componentes/base pequenos e reutilizáveis
- Protótipo de tela de login
- Protótipo de tela de cadastro
- Definição de como telas e estado vão ser organizados

Critério de aceite:
- Dá para adicionar uma nova tela sem dificuldade desnecessária
- Componentes são reutilizáveis quando faz sentido
- Telas do protótipo ajudam a validar ideia, não só “estar lá”

Questões para responder:
- Front vai ser HTML/JS simples, React, Vite ou outra coisa
- Estado vai ser local, global, ou atrelado ao backend
- Como será a comunicação com backend antes dele pronto

---

## 4. Frente: Backend

Responsável: pessoa ou par

Entregáveis sugeridos:
- Decisão inicial sobre backend
- Definição de como vende as operações principais
- Rascunho de contratos entre frontend e backend
- Base para Firebase ou outra solução, se for esse o caminho

Critério de aceite:
- Dá para saber como backend vai ser acionado
- Dá para saber o que backend deve garantir sozinho
- Backend não depende de adivinhação da equipe

Questões para responder:
- Firebase será base ou será só parte
- Se Firebase, quais products serão usados
- Se haverá backend separado para regras críticas
- Como será a autenticação e quem gerencia perfis

---

## 5. Frente: Banco de Dados

Responsável: pessoa ou par

Entregáveis sugeridos:
- Modelo inicial das entidades principais
- Definição de campos obrigatórios
- Separação entre máquina, equipamento, suprimento, manutenção, O.S., empréstimo e auditoria
- PequenaNota sobre consistência de saldo e de operações críticas

Critério de aceite:
- Dá para ler o modelo e entender o sistema
- Dá para identificar como cada entidade se relaciona
- Dá para entender onde pode vir saldo inconsistente

Questões para responder:
- Qual banco será usado
- Se modelo inicial será normalizado ou com ajustes para relatórios
- Se auditoria vai ser entidade própria ou decorrente
- Quais dados são obrigatórios para não comprometer rastreabilidade

---

## 6. Frente: Prototipagem e Validação

Responsável: pessoa ou par

Entregáveis sugeridos:
- Protótipos que ajudem a provar fluxos principais
- Vista de telas como login, cadastro e catálogo inicial
- Registro de o que foi testado e o que ainda não foi

Critério de aceite:
- Protótipos ajudam a tomar decisões, não só ocupar lugar
- Dá para ver fluxos principais antes de implementação completa
- Protótipos não se tornam fonte da verdade sobre regras

Questões para responder:
- Qual a diferença entre protótipo e implementação real
- O que deve ser feito só para validar ideia
- O que pode ser ignorado nessa sprint

---

## 7. Como dividir sem bagunçar

Regra prática:
- Cada frente tem um dono ou duo
- Cada frente entrega algo pequeno, mas válido
- Cada frente deixa claro o que depende de outra frente
- Documentação acompanha o que foi decidido, não apenas o que foi feito

Cronograma sugerido dentro da sprint:
1. Projeto e documentação definem o “como vamos trabalhar”
2. Front define estrutura e protótipos
3. Backend define contrato e escolha de Firebase
4. Banco modela entidades principais
5. Prototipagem ajuda a confirmar que os demais estão alinhados

---

## 8. O que não é responsabilidade desta sprint

- Implementação completa de todos os módulos
- Backend final com todas as regras
- Banco final com todas as entidades
- Front final com todos os detalhes
- Decisões finais sobre infraestrutura de produção

---

## 9. Checkpoint de fim de sprint

Ao final, a equipe deve conseguir responder:
- Qual front foi escolhido
- Qual backend foi escolhido
- Qual banco foi escolhido
- Qual a estrutura inicial do repositório
- Qual o que cada frente entregou
- Qual o que ainda está pendente

Se alguma frente não consegue responder, a Sprint 1 não está pronta.

---

Este arquivo pode ser usado como base para montar issues de equipe e ainda é uma referência para quem entra depois.
