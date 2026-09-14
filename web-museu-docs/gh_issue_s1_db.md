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
