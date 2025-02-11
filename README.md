# README

## Integrantes da Equipe
- ** Antonio Irandilson

## Projeto
O projeto trabalhado foi  o **"Memos"**, um sistema para gerenciamento de notas e informações.

## Code Smells Refatorados

Durante esta atividade, foi realizado a refatoração de um **code smell específico** no projeto. O code smell identificado e corrigido foi:

- **Code Smell Refatorado: Hardcoded Values**  
  **Local:** Linha 17 do arquivo `CreateIdentityProviderDialog.tsx`.

### Descrição da Refatoração

O problema identificado na linha 17 foi a definição do `templateList` diretamente dentro do componente. Isso gerava um código difícil de manter, reutilizar e testar, além de um excesso de informações dentro do próprio componente.

**Refatoração Realizada:**  
A lista `templateList` foi movida para um arquivo de configuração separado, centralizando os dados em um único lugar e tornando o código mais modular e reutilizável.

**Antes da Refatoração:**

```tsx
const templateList = [
  {
    name: "",
    title: "GitHub",
    type: IdentityProvider_Type.OAUTH2,
    config: {
      oauth2Config: {
        clientId: "",
        clientSecret: "",
        authUrl: "https://github.com/login/oauth/authorize",
        tokenUrl: "https://github.com/login/oauth/access_token",
      },
    },
  },
  // outros templates...
];

### Após a Refatoração:

**Arquivo identityProviderTemplates.ts (novo arquivo de configuração):

export const identityProviderTemplates: IdentityProvider[] = [
  {
    name: "",
    title: "GitHub",
    type: IdentityProvider_Type.OAUTH2,
    config: {
      oauth2Config: {
        clientId: "",
        clientSecret: "",
        authUrl: "https://github.com/login/oauth/authorize",
        tokenUrl: "https://github.com/login/oauth/access_token",
        userInfoUrl: "https://api.github.com/user",
      },
    },
  },
  // outros templates...
];


**E no componente CreateIdentityProviderDialog.tsx, o código ficou:

import { identityProviderTemplates } from "@/config/identityProviderTemplates";

// Dentro do componente:
const identityProviderTypes = [...new Set(identityProviderTemplates.map((t) => t.type))];


