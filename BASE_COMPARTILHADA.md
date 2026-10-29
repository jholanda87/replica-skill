# Base compartilhada da equipe: como ligar (10 minutos)

Com a base compartilhada, todos os vendedores veem e editam os mesmos clientes,
em tempo real, no computador e no celular. Cada um entra com a própria conta
Google, e só os e-mails que o administrador liberar têm acesso.

A base fica no **Firebase**, serviço do Google. O plano gratuito (Spark) basta
para este uso: 50 mil leituras e 20 mil gravações por dia, sem cartão de crédito.

Você faz os passos 1 a 6 uma única vez, no console do Firebase. Os nomes dos
menus podem aparecer em português ou em inglês; os dois estão indicados.

---

## 1. Criar o projeto

1. Acesse <https://console.firebase.google.com> com a conta Google da empresa.
2. Clique em **Criar um projeto** (*Create a project*).
3. Nome: `mapa-clientes` (ou outro). Aceite os termos e continue.
4. **Google Analytics:** desative. Não é necessário.
5. Clique em **Criar projeto** e espere terminar.

## 2. Criar o banco de dados (Firestore)

1. No menu da esquerda: **Criação** (*Build*) > **Firestore Database**.
2. Clique em **Criar banco de dados** (*Create database*).
3. Se perguntar a edição, escolha **Standard**.
4. Local: **southamerica-east1 (São Paulo)**. Não dá para mudar depois.
5. Escolha **Iniciar no modo de produção** (*Start in production mode*) e crie.

## 3. Colar as regras de segurança

Ainda no Firestore, abra a aba **Regras** (*Rules*), apague tudo o que estiver
lá, cole o texto abaixo e clique em **Publicar** (*Publish*).

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    function logado() {
      return request.auth != null && request.auth.token.email_verified == true;
    }
    function membro() {
      return logado()
        && exists(/databases/$(database)/documents/equipe/acesso)
        && request.auth.token.email in get(/databases/$(database)/documents/equipe/acesso).data.emails;
    }
    // Lista de quem tem acesso. Quem cria vira o administrador.
    match /equipe/acesso {
      allow read: if logado();
      allow create: if logado()
        && request.resource.data.dono == request.auth.token.email
        && request.auth.token.email in request.resource.data.emails;
      allow update: if logado()
        && resource.data.dono == request.auth.token.email
        && request.resource.data.dono == resource.data.dono;
      allow delete: if false;
    }
    match /clientes/{id} {
      allow read, write: if membro();
    }
    match /config/{doc} {
      allow read, write: if membro();
    }
  }
}
```

O que essas regras garantem:

- Ninguém lê nem altera clientes sem entrar com uma conta Google **liberada**.
- Só o administrador da equipe libera ou remove e-mails.
- O administrador é quem cria a equipe no mapa, no passo 7. **Faça o passo 7
  logo depois de terminar este guia**, para ninguém criar antes de você.

## 4. Ativar o login com Google

1. Menu da esquerda: **Criação** (*Build*) > **Authentication**.
2. Clique em **Vamos começar** (*Get started*).
3. Na aba **Método de login** (*Sign-in method*), clique em **Google**.
4. Ative a chave, escolha o **e-mail de suporte** e clique em **Salvar**.

## 5. Autorizar o endereço do mapa

1. Em **Authentication**, abra a aba **Configurações** (*Settings*).
2. Clique em **Domínios autorizados** (*Authorized domains*) > **Adicionar domínio**.
3. Digite `jholanda87.github.io` e adicione.

Sem isso, o botão "Entrar com Google" mostra um erro de domínio não autorizado.

## 6. Pegar a configuração do app

1. Clique na engrenagem ao lado de **Visão geral do projeto** > **Configurações do projeto**.
2. Em **Seus apps** (*Your apps*), clique no ícone **Web** (`</>`).
3. Apelido: `mapa`. **Não** marque o Firebase Hosting. Clique em **Registrar app**.
4. Aparece um bloco de código com `const firebaseConfig = { apiKey: ..., ... };`.
   **Copie o bloco inteiro** (pode copiar o código todo da tela; o mapa acha a parte certa).

Esses dados identificam o projeto, mas não dão acesso aos clientes: quem protege a
base são as regras do passo 3 e o login.

## 7. Ligar no mapa (você, como administrador)

1. Abra <https://jholanda87.github.io/replica-skill/>.
2. Aba **Dados** > **Base compartilhada da equipe**: cole o bloco e clique em **Conectar à base**.
3. Clique em **Entrar com Google** e escolha a sua conta.
4. Clique em **Criar equipe (sou o administrador)**.
5. Se este aparelho já tinha clientes cadastrados, aparece **Enviar para a base**:
   clique para levá-los para a equipe.

O selo ao lado do título passa a mostrar **Equipe · sincronizado**.

## 8. Convidar os vendedores

1. Na mesma seção, digite o e-mail Google do vendedor e clique em **Liberar**.
2. Clique em **Enviar por WhatsApp** (ou **Copiar link**) e mande o link para ele.
3. O vendedor abre o link no celular, clica em **Entrar com Google** e pronto.

Para tirar o acesso de alguém, clique em **remover** ao lado do e-mail.

---

## Como funciona no dia a dia

- Tudo o que um vendedor cadastra ou altera aparece para os outros em segundos.
- **Sem internet:** o mapa continua funcionando com os dados já carregados, e as
  alterações são enviadas quando a conexão voltar.
- Cada alteração registra **quem** fez, e o histórico de contatos mostra o autor.
- **Sair** apaga os dados da equipe daquele aparelho (útil quando um vendedor sai
  da empresa ou troca de celular).
- Se duas pessoas editarem o **mesmo cliente** ao mesmo tempo, fica valendo a
  última gravação.
- Importar um backup JSON com a base ligada **só adiciona ou atualiza** clientes;
  nunca apaga o que os outros cadastraram.
- Apagar a base inteira só é permitido ao administrador.
- Continue exportando o backup JSON de vez em quando, por segurança.

## Problemas comuns

| Mensagem | O que fazer |
|---|---|
| "O e-mail ... ainda não foi liberado na equipe" | O administrador precisa liberar esse e-mail (passo 8). |
| "Este endereço ainda não foi autorizado no Firebase" | Refaça o passo 5. |
| "O login com Google ainda não foi ativado" | Refaça o passo 4. |
| "Não reconheci a configuração" | Copie de novo o bloco inteiro do passo 6. |
| A janela do Google não abre no celular | Permita pop-ups para o site; se não abrir, o mapa tenta pelo redirecionamento. |
