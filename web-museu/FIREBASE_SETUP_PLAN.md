# Firebase Setup Plan — SIG-MUSARQ

Este documento existe para alinhar o time antes de criar qualquer arquivo de código real ou modificar o repositório.
Ele registra a estrutura pretendida, o que será necessário do Firebase e o que ainda precisa ser decidido.

## 1. O que Firebase vai resolver aqui

Para o SIG-MUSARQ, o Firebase pode ser usado como base para:
- autenticação simples deadministradores e técnicos
- armazenamento de dados operacionais do laboratório
- possibilidade de sincronização mobile ou em múltiplos clients, se necessário

Isso não é decidido como “backend definitivo”. É uma opção de partida prática para um projeto pequeno que quer começar rápido.

## 2. Decisões que precisam ficar claras antes de codar

- Qual Firebase product vai guardar cada coisa:
  - Authentication
  - Firestore ou Realtime Database
  - Storage, se for usar
- Se o banco escolhido será Firestore ou outro produto
- Seuais sensíveis vão ser controlados no Firebase ou num backend próprio
- Se vai haver backend separado só para regras não confiáveis no cliente

Até essas decisões estarem prontas, o projeto deve ser estruturado para aceitar Firebase, mas não assumir toda a arquitetura nele.

## 3. Estrutura pretendida no repositório

O ideal é deixar claro onde entra Firebase e onde fica o resto.

Sugestão de estrutura inicial:

```
web-museu/
  index.html
  main.js
  style.css
  firebase/
    auth.js
    init.js
    rules-notes.md
  app/
    ui/
    state/
    routes/
    modules/
  docs/
    firebase-setup-checklist.md
```

Ou, se o projeto for mais Node/React/Vite do que site estático simples, a estrutura será ajustada para:

```
src/
  firebase/
    init.ts
    auth.ts
  app/
    modules/
    ui/
  ...
```

A ideia é separar claramente:
- inicialização do Firebase
- uso de auth
- uso de banco
- código de UI
- código do domínio

## 4. O que essa estrutura deve evitar

- Colocar credenciais no código
- Misturar regras de negócio no mesmo arquivo de UI
- Assumir que tudo vai ficar no cliente sem planejar validação
- Criar pastas genéricas que não representam nada real

## 5. O que vai no Firebase

Provavelmente:
- Auth para login simples
- Firestore para dados principais, se a equipe aceitar
- Storage apenas se houver necessidade real de arquivos

Não é para:
- código crítico que não pode confiar no cliente
- regras secretas expostas no frontend

## 6. O que precisamos ter antes de usar

- projeto Firebase criado
- products habilitados conforme a decisão
- regras de segurança escritas com consciência do domínio
-Chaves de API organizadas e nunca versionadas
- um modo claro de testar o comportamento tanto no dev quanto no eventual staging

## 7. Próximos passos

Se o time concorda, o próximo passo é:
1. confirmar se Firebase será a base primária ou só parte do sistema
2. escolher products exatos
3. criar estrutura mínima de inicialização
4. adicionar uma issue para “configuração inicial do Firebase” com checklist

Esse arquivo pode virar a base da issue de Firebase e do roteiro de setup.
