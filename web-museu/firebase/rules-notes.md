# Firebase Security Rules Notes — SIG-MUSARQ

Use este arquivo como memória de decisão e checklist para as regras do Firebase.

## O que as regras precisam proteger

- Authentication: acesso de admin e técnico, sem concessão indevida.
- Dados de máquinas, suprimentos, manutenções, O.S., empréstimos e auditoria.
- Operações que não podem ser feitas apenas porque o cliente fez requisição.

## Princípios

- Regras não podem ser substituto completo para validação de negócio.
- Regras podem ser a primeira barreira, mas a regra principal deve ser aplicada onde ela faz sentido.
- Se uma operação for crítica, ela deve ter controle centralizado e não depender só do cliente.
- Logs e rastreabilidade devem ser compatíveis com as regras do sistema.

## Checklist de revisão

- [ ] Quem pode ler cada coleção/caminho
- [ ] Quem pode escrever em cada coleção/caminho
- [ ] O que precisa de controle por perfil
- [ ] O que não pode ser escrito direto pelo cliente
- [ ] O que precisa de validação extra no backend ou em regras mais rígidas
- [ ] Como serão feitos testes de regras

## Padrão desejado

Regras claras, leves e com justificativa.
Nenhuma regra deve deixar passar operação que o domínio proíbe.

## Pendências

- Definir products exatos que serão usados
- Definir quem é admin/tecnico no Firebase ou num sistema 연계ado
- Decidir se regras de negócio ficam no cliente, no Firebase ou num backend separado
