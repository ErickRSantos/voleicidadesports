# Guia de Instalação — Cidade Sports

Siga este passo a passo para colocar o sistema no ar gratuitamente.
Tempo estimado: **20 a 30 minutos**.

---

## Parte 1 — Criar o banco de dados no Firebase

### 1.1 Criar conta e projeto

1. Acesse [firebase.google.com](https://firebase.google.com) e clique em **"Começar"**
2. Entre com sua conta Google
3. Clique em **"Adicionar projeto"**
4. Nome do projeto: `cidade-sports` → clique em **Continuar**
5. Desative o Google Analytics (não é necessário) → clique em **Criar projeto**
6. Aguarde e clique em **Continuar**

### 1.2 Criar o banco de dados (Firestore)

1. No menu lateral, clique em **"Firestore Database"**
2. Clique em **"Criar banco de dados"**
3. Selecione **"Iniciar no modo de teste"** → clique em **Próximo**
4. Selecione a região **`southamerica-east1 (São Paulo)`** → clique em **Ativar**
5. Aguarde o banco ser criado

### 1.3 Ajustar as regras de segurança

1. Dentro do Firestore, clique na aba **"Regras"**
2. Substitua o conteúdo por:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

3. Clique em **"Publicar"**

> ℹ️ Esta regra permite acesso público — suficiente para uso interno do ministério.
> No futuro, se quiser mais segurança, posso ajudar a adicionar autenticação.

### 1.4 Pegar as credenciais do projeto

1. No menu lateral, clique no ícone de engrenagem (⚙) → **"Configurações do projeto"**
2. Role a página para baixo até **"Seus aplicativos"**
3. Clique no ícone **`</>`** (Web)
4. Nome do app: `cidade-sports-web` → clique em **"Registrar app"**
5. Vai aparecer um bloco de código assim:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "cidade-sports.firebaseapp.com",
  projectId: "cidade-sports",
  storageBucket: "cidade-sports.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123:web:abc123"
};
```

6. **Copie esses valores** — você vai precisar no próximo passo

---

## Parte 2 — Configurar o arquivo do site

1. Abra o arquivo `index.html` em qualquer editor de texto
   (pode ser o Bloco de Notas, mas recomendo o [VS Code](https://code.visualstudio.com/) — gratuito)

2. Encontre esta seção no arquivo (por volta da linha 180):

```javascript
const firebaseConfig = {
  apiKey:            "COLE_AQUI_SUA_apiKey",
  authDomain:        "COLE_AQUI_SEU_authDomain",
  projectId:         "COLE_AQUI_SEU_projectId",
  storageBucket:     "COLE_AQUI_SEU_storageBucket",
  messagingSenderId: "COLE_AQUI_SEU_messagingSenderId",
  appId:             "COLE_AQUI_SEU_appId"
};
```

3. Substitua cada `"COLE_AQUI_..."` pelo valor correspondente que você copiou do Firebase

4. Para mudar o PIN de acesso da área do líder, encontre a linha:
```javascript
const ADMIN_PIN = "1234";
```
E troque `1234` pelo PIN que desejar (apenas números)

5. Salve o arquivo

---

## Parte 3 — Colocar o site no ar com GitHub Pages

### 3.1 Criar conta no GitHub

1. Acesse [github.com](https://github.com) e clique em **"Sign up"**
2. Crie uma conta gratuita (se já tiver, pule este passo)

### 3.2 Criar o repositório

1. Clique no **"+"** no canto superior direito → **"New repository"**
2. Nome do repositório: `cidade-sports`
3. Deixe como **Public**
4. Marque **"Add a README file"**
5. Clique em **"Create repository"**

### 3.3 Subir o arquivo

1. Dentro do repositório recém-criado, clique em **"Add file"** → **"Upload files"**
2. Arraste o arquivo `index.html` para a área indicada
3. No campo **"Commit changes"**, escreva: `Adiciona site Cidade Sports`
4. Clique em **"Commit changes"**

### 3.4 Ativar o GitHub Pages

1. Clique em **"Settings"** (aba no menu do repositório)
2. No menu lateral, clique em **"Pages"**
3. Em **"Source"**, selecione **"Deploy from a branch"**
4. Em **"Branch"**, selecione `main` e a pasta `/ (root)`
5. Clique em **"Save"**
6. Aguarde 2 a 3 minutos
7. Atualize a página — aparecerá o link do seu site, tipo:
   `https://seu-usuario.github.io/cidade-sports`

---

## Parte 4 — Gerar o QR Code

1. Acesse [qr-code-generator.com](https://www.qr-code-generator.com/)
2. Cole o link do seu site
3. Baixe o QR Code em PNG ou SVG
4. Imprima e cole na entrada da quadra!

---

## Resumo final

| O que | Serviço | Custo |
|---|---|---|
| Banco de dados | Firebase (Google) | Gratuito |
| Hospedagem do site | GitHub Pages | Gratuito |
| QR Code | qr-code-generator.com | Gratuito |

---

## Dúvidas frequentes

**Quantos registros o Firebase suporta no plano gratuito?**
50.000 leituras e 20.000 escritas por dia — muito mais do que um ministério vai usar.

**Os dados ficam salvos para sempre?**
Sim, ficam no servidor do Google até você apagar manualmente.

**Posso acessar o painel de qualquer celular?**
Sim! O site funciona em qualquer dispositivo com internet.

**Como atualizo o elenco?**
Pelo próprio painel, na aba "Elenco" da área do líder.
