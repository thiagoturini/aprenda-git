# 14. Conectando com GitHub

## 🎯 Objetivo

Vamos conectar seu repositório local com o GitHub e enviar seu código para lá!

## 📋 Pré-requisitos

Antes de começar, certifique-se de ter:

- ✅ Conta no GitHub criada
- ✅ Git instalado e configurado
- ✅ Repositório local com alguns commits

Se não tem, volte para os capítulos anteriores!

## 🆕 Dois Caminhos Possíveis

### Caminho 1: Projeto Novo no GitHub

Você cria o repositório no GitHub primeiro e clona para seu computador.

### Caminho 2: Projeto Já Existe Localmente

Você já tem um projeto local e quer enviá-lo para o GitHub.

Vamos ver os dois! 🚀

## 📦 Caminho 1: Criando Repo no GitHub e Clonando

### 🖱️ Criar Repositório no GitHub

**1. Faça login no GitHub**

**2. Crie novo repositório:**
- Clique no ícone **+** (canto superior direito)
- Selecione **New repository**

**3. Preencha as informações:**
- **Repository name**: `meu-primeiro-repo` (sem espaços!)
- **Description**: (opcional) "Meu primeiro repositório Git"
- **Public** ou **Private**: 
  - Public: Qualquer um pode ver
  - Private: Só você (e quem você convidar)
- **NÃO** marque nenhuma das opções:
  - ❌ Add a README file
  - ❌ Add .gitignore
  - ❌ Choose a license
  
  (Criaremos esses arquivos localmente)

**4. Clique em "Create repository"**

**5. GitHub mostra instruções:** Guarde essa página, vamos usar!

### ✅ Clonar Repositório

**Via Terminal:**

```bash
# Clone o repositório (copie a URL do GitHub)
git clone https://github.com/seu-usuario/meu-primeiro-repo.git

# Entre na pasta
cd meu-primeiro-repo

# Crie um arquivo
echo "# Meu Primeiro Repositório" > README.md

# Adicione e comite
git add README.md
git commit -m "Adiciona README"

# Envie para o GitHub
git push origin main
```

**🖱️ Via VS Code:**

**1. Clone pelo VS Code:**
- Pressione `Ctrl+Shift+P`
- Digite "Git: Clone"
- Cole a URL: `https://github.com/seu-usuario/meu-primeiro-repo.git`
- Escolha pasta onde salvar
- Clique em "Open" quando perguntar

**2. Crie arquivo:**
- Crie `README.md`
- Adicione conteúdo: `# Meu Primeiro Repositório`

**3. Commit:**
- Source Control (`Ctrl+Shift+G`)
- Stage o arquivo (`+`)
- Digite mensagem: "Adiciona README"
- Commit (`Ctrl+Enter`)

**4. Push:**
- Clique nos **três pontinhos** (⋯)
- Selecione **Push**
- Ou clique no ícone de "sync" na barra inferior

**5. Autentique:**
- Se for a primeira vez, o VS Code pede credenciais
- Use seu email do GitHub
- Use o **token** como senha (não a senha da conta!)

**6. Verifique no GitHub:**
- Atualize a página do repositório
- Você verá seu arquivo lá! 🎉

## 📤 Caminho 2: Enviando Projeto Local para GitHub

Você já tem um projeto local e quer colocá-lo no GitHub.

### 🖱️ Criar Repositório Vazio no GitHub

**1. No GitHub:**
- Clique no **+** → **New repository**
- Nome: `meu-projeto-existente`
- **NÃO marque** nenhuma opção (README, .gitignore, license)
- **Create repository**

**2. GitHub mostra duas opções:**

```
…or create a new repository on the command line
…or push an existing repository from the command line  ← Esta!
```

Copie os comandos da segunda opção!

### ✅ Conectar e Enviar (Via Terminal)

```bash
# 1. Entre no seu projeto local
cd /caminho/para/seu-projeto

# 2. Adicione o remoto (copie a URL do GitHub)
git remote add origin https://github.com/seu-usuario/meu-projeto-existente.git

# 3. Verifique que foi adicionado
git remote -v

# Resultado:
# origin  https://github.com/seu-usuario/meu-projeto-existente.git (fetch)
# origin  https://github.com/seu-usuario/meu-projeto-existente.git (push)

# 4. Envie o código
git push -u origin main
```

**Se der erro "branch main não existe":**

Seu branch pode chamar `master`. Veja com:
```bash
git branch
```

Se for `master`, use:
```bash
git push -u origin master
```

Ou renomeie para `main`:
```bash
git branch -M main
git push -u origin main
```

### 🖱️ Conectar e Enviar (Via VS Code)

**1. Abra seu projeto no VS Code**

**2. Adicione o remoto via terminal integrado:**
- Pressione `` Ctrl+` `` (abre terminal)
- Execute:
```bash
git remote add origin https://github.com/seu-usuario/meu-projeto-existente.git
```

**3. Push via interface:**
- Source Control (`Ctrl+Shift+G`)
- Clique nos **três pontinhos** (⋯)
- Selecione **Push to...**
- Selecione `origin`
- Selecione a branch (`main`)

**4. Autentique:**
- Forneça credenciais quando solicitado
- Use token como senha

**5. Sucesso!** 🎉
- Verifique no GitHub
- Seu código está lá!

## 🔍 Verificando a Conexão

### ✅ Via Terminal

**Ver remotos configurados:**
```bash
git remote -v
```

Resultado:
```
origin  https://github.com/usuario/repo.git (fetch)
origin  https://github.com/usuario/repo.git (push)
```

**Ver informações detalhadas:**
```bash
git remote show origin
```

Mostra:
- URL do remoto
- Branches remotas
- Configuração de push/pull

### 🖱️ Via VS Code

**Na barra inferior:**
- Você vê um ícone de sincronização
- Número de commits para push/pull

**No Source Control:**
- Três pontinhos → **Remote** → mostra remotos

## 🔐 Autenticação: HTTPS com Token

Quando você faz push pela primeira vez:

### ✅ Via Terminal

**1. Git pede credenciais:**
```
Username for 'https://github.com': seu-usuario
Password for 'https://seu-usuario@github.com': [cole seu token]
```

**2. Use:**
- **Username**: seu nome de usuário do GitHub
- **Password**: **não use sua senha!** Use o **token de acesso**

**3. Para não pedir sempre, configure cache:**

**Linux/Mac:**
```bash
git config --global credential.helper cache
```

**Mac (Keychain):**
```bash
git config --global credential.helper osxkeychain
```

**Windows:**
```bash
git config --global credential.helper wincred
```

### 🖱️ Via VS Code

O VS Code gerencia autenticação automaticamente:

1. Quando faz push pela primeira vez
2. Abre janela do navegador
3. Você autoriza o VS Code no GitHub
4. Pronto! Não precisa mais fazer login

**Muito mais fácil!** ✨

## 📊 Entendendo git push -u

```bash
git push -u origin main
```

**O que significa `-u`?**

- `-u` = `--set-upstream`
- Configura **tracking** (rastreamento)
- A branch local `main` "rastreia" a branch remota `origin/main`

**Depois disso, você pode usar apenas:**
```bash
git push    # Ao invés de: git push origin main
git pull    # Ao invés de: git pull origin main
```

**Você só precisa usar `-u` uma vez!**

## 🔄 Fluxo Completo de Trabalho

### Daily Workflow:

```bash
# 1. Atualiza seu repositório local
git pull

# 2. Cria branch para nova funcionalidade
git switch -c feature-nova

# 3. Trabalha e comita
git add .
git commit -m "Implementa funcionalidade"

# 4. Volta para main
git switch main

# 5. Faz merge
git merge feature-nova

# 6. Envia para GitHub
git push

# 7. Deleta branch local
git branch -d feature-nova
```

### 🖱️ Via VS Code:

Todo esse fluxo pode ser feito visualmente:
- Pull: Ícone de sync na barra inferior
- Branches: Clique no nome da branch
- Commit: Source Control
- Merge: Source Control → Menu
- Push: Automático ou ícone de sync

## ⚠️ Troubleshooting

### Erro: "remote origin already exists"

**Problema:** Você já tem um remoto chamado `origin`.

**Solução:**

```bash
# Ver o remoto existente
git remote -v

# Remover
git remote remove origin

# Adicionar o novo
git remote add origin NOVA_URL
```

### Erro: "failed to push some refs"

**Problema:** O remoto tem commits que você não tem localmente.

**Solução:**

```bash
# Primeiro puxe as mudanças
git pull origin main

# Depois faça push
git push origin main
```

### Erro: "authentication failed"

**Problema:** Credenciais incorretas.

**Solução:**
- Certifique-se de usar o **token**, não a senha
- Gere um novo token se necessário
- Verifique se o token tem permissões de `repo`

### Erro: "Permission denied (publickey)"

**Problema:** Tentou usar SSH mas não tem chave configurada.

**Solução:**
- Use HTTPS ao invés de SSH
- Ou configure chave SSH (veremos depois)

## 🎓 Resumo

✅ Você aprendeu:
- Criar repositório no GitHub
- Clonar repositório para seu computador
- Conectar repositório local existente com GitHub
- Fazer push do código
- Autenticar com token
- Verificar conexão com remoto
- Solucionar problemas comuns

## 🎯 Exercício Prático

**Opção 1 (Iniciante):**
1. Crie novo repositório no GitHub
2. Clone para seu computador
3. Adicione um arquivo README.md
4. Comite e faça push

**Opção 2 (Prático):**
1. Use um projeto local existente
2. Crie repositório vazio no GitHub
3. Conecte os dois
4. Faça push do código
5. Verifique no GitHub que está lá

---

## 🎯 Próximos Passos

Agora que seu código está no GitHub, vamos aprender a clonar repositórios de outras pessoas!

➡️ **Próximo:** [Clone: Copiando Repositórios](15-clone.md)
