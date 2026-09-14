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
4. Confirmir que frontend sabe o que esperar

## Decisões pendentes
- Firebase será base primária ou só parte do sistema
- Quais products do Firebase serão usados
- Se haverá backend separado para regras críticas
- Como serão gerenciados perfis
