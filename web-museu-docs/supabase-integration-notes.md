# Como usar Supabase no SIG-MUSARQ

Este arquivo serve como memória de decisão e roteiro prático para adotar Supabase no lugar de Firebase.

## Por que Supabase pode ser útil aqui

Supabase é uma opção que traz:
- banco relacional baseado em PostgreSQL
- um dos produtos mais próximos de “backend pronto” para projetos pequenos
- autenticação com suporte a role/regras
- API generada a partir do banco
- possibilidade de escalar para SQL puro quando o projeto precisar

Isso combina bem com um sistema cujo negócio já tem estrutura relacional clara: usuários, máquinas, suprimentos, manutenções, O.S., empréstimos, auditoria.

## O que pode ficar no Supabase

- Usuários, perfis e autenticação básica
- Tabelas principais do sistema
- Relacionamentos entre entidades
- Regras e constraints no banco
- Storage, se houver necessidade de arquivos
- Funções/security para validações mais fortes, quando necessário

## O que não deve ser só Supabase

- Regras de negócio críticas que não podem depender apenas do cliente
- Validações importantes que precisam de controle centralizado
- Politicas de auditoria que precisam de garantia maior que UI ou cliente

Em outras palavras: Supabase pode ser backbone, mas não pode ser excusa para negligenciar controle de acesso e consistência.

## Fluxo sugerido de uso

1. Definir schema inicial
2. Habilitar auth e configurar provedor/estratégia
3. Criar tabelas principais com relacionamentos claros
4. Montar RLS/perms básicas por perfil
5. Conectar frontend ao Supabase client
6. Codificar validação extra no backend ou nas regras do sistema
7. Testar rotas críticas antes de codar UI completa

## Pontos de atenção

- Que entries de auth representam admin/tecnico/cliente
- Como será a separação entre operador logado e sistema
- O que vai na tabela de usuário e o que vai em tabela de perfis
- Como será salvo apenas quem fez cada operação crítica
- Como evitar saldo fantasma em suprimentos
- Como representar O.S. com consumo zero sem ambiguidade
- Como lidar com máquinas bloqueadas em corretiva

## Vantagens para este projeto

- Relacional: facilita modelar máquina vs equipamento, suprimento vs carretel, O.S. vs produção
- Possibilita migrations e schema claro
- Facilita auditoria com timestamps e quem registrou
- Permite evoluir para SQL puro se necessário
- Ajuda na consistência de saldos e relações

## Riscos a controlar

- Regras ficarem espalhadas
- Cliente fazer escrita que não deveria
- Saldo inconsistente por falta de transação/controle
- Auditoria incompleta se quem registra não for registrado corretamente
- Desempenho em relatórios se for tudo feito no cliente sem cuidado

## Sugestão de próximos passos

1. Escolher Supabase como backend primário
2. Definir schema mínimo inicial em documento
3. Criar issue específica para “schema e banco no Supabase”
4. Criar issue para “auth e perfis no Supabase”
5. Criar issue para “RLS/permissoes no Supabase”
6. Grid a implementação de backend/frente depois que schema e auth estiverem claros

---

Se quiser, eu posso transformar isso em:
- issue de setup do Supabase
- issue de schema inicial
- issue de auth e perfis
- roteiro de RLS/permissoes
