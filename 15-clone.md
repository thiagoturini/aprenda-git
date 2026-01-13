# 15. Clone: Copiando Repositórios

## 🎯 O que é Clone?

**Clone** é copiar um repositório completo (com todo o histórico) do remoto para seu computador.

```
[GitHub]  ─── git clone ───>  [Seu Computador]
  Remoto                         Local
```

Quando você clona:
- ✅ Baixa todos os arquivos
- ✅ Baixa todo o histórico de commits
- ✅ Baixa todas as branches
- ✅ Configura automaticamente o remote "origin"
- ✅ Cria uma cópia funcional pronta para trabalhar

## 🤔 Quando Usar Clone?

- Quer contribuir com um projeto open source
- Entrando em um projeto de equipe
- Quer estudar código de outra pessoa
- Precisa trabalhar em outro computador
- Quer usar um template/starter project

## 📦 Clonando um Repositório

### ✅ Via Terminal

**Sintaxe básica:**
```bash
git clone URL
```

**Exemplo:**
```bash
git clone https://github.com/usuario/projeto.git
```

Isso cria uma pasta `projeto/` no diretório atual.

**Clone com nome diferente:**
```bash
git clone https://github.com/usuario/projeto.git minha-pasta
```

Cria a pasta `minha-pasta/` ao invés de `projeto/`.

**Clone de branch específica:**
```bash
git clone -b nome-branch https://github.com/usuario/projeto.git
```

### 🖱️ Via VS Code

**Método 1: Command Palette**

1. Pressione `Ctrl+Shift+P`
2. Digite "Git: Clone"
3. Cole a URL do repositório
4. Escolha a pasta onde salvar
5. Quando terminar, clique em "Open" ou "Open in New Window"

**Método 2: Tela de Welcome**

1. Se o VS Code estiver sem pasta aberta
2. Na tela de boas-vindas, clique em "Clone Git Repository"
3. Cole a URL
4. Escolha a pasta

**Método 3: Source Control**

1. Abra Source Control (`Ctrl+Shift+G`)
2. Se não há pasta aberta, aparece "Clone Repository"
3. Clique e cole a URL

## 🔍 Obtendo a URL para Clonar

### 🖱️ No GitHub:

1. Vá para o repositório que quer clonar
2. Clique no botão verde **Code**
3. Você vê três opções:
   - **HTTPS**: Mais comum
   - **SSH**: Se você configurou chaves SSH
   - **GitHub CLI**: Linha de comando do GitHub

4. Copie a URL (geralmente HTTPS)

**Exemplo de URLs:**

**HTTPS:**
```
https://github.com/facebook/react.git
```

**SSH:**
```
git@github.com:facebook/react.git
```

## 📝 Exemplo Prático: Clonando Projeto Real

Vamos clonar um projeto famoso como exemplo:

### ✅ Via Terminal

```bash
# 1. Entre na pasta onde quer salvar o projeto
cd ~/Projects

# 2. Clone um repositório (exemplo: um tutorial)
git clone https://github.com/github/gitignore.git

# 3. Entre na pasta criada
cd gitignore

# 4. Veja os arquivos
ls

# 5. Veja o histórico
git log --oneline -10

# 6. Veja as branches
git branch -a

# 7. Veja o remoto configurado
git remote -v
```

### 🖱️ Via VS Code

1. Pressione `Ctrl+Shift+P`
2. "Git: Clone"
3. Cole: `https://github.com/github/gitignore.git`
4. Escolha pasta (ex: Documentos/Projetos)
5. Clique "Open" quando terminar
6. Explore os arquivos no Explorer
7. Use Git Graph para ver o histórico visual

## 🎯 Diferença: Clone vs Download ZIP

### Download ZIP (❌ Não é Git!)

No GitHub, há botão "Download ZIP":
- ✅ Baixa os arquivos
- ❌ **Não** tem histórico de commits
- ❌ **Não** tem .git folder
- ❌ **Não** tem conexão com repositório remoto
- ❌ **Não** pode fazer push/pull

É apenas um snapshot dos arquivos! Não é um repositório Git.

### Git Clone (✅ Repositório Completo!)

```bash
git clone URL
```

- ✅ Baixa os arquivos
- ✅ **Tem** todo o histórico de commits
- ✅ **Tem** a pasta .git
- ✅ **Tem** conexão com remoto (origin)
- ✅ **Pode** fazer push/pull (se tiver permissão)

**Use sempre clone, não download ZIP!** 🎯

## 🔧 O que o Clone Faz Automaticamente

Quando você clona, o Git:

### 1. Cria a Pasta
```bash
git clone https://github.com/usuario/projeto.git
# Cria pasta "projeto/"
```

### 2. Inicializa o Repositório
```bash
# Equivalente a:
mkdir projeto
cd projeto
git init
```

### 3. Adiciona o Remote
```bash
# Configura origin automaticamente
git remote add origin https://github.com/usuario/projeto.git
```

### 4. Faz Fetch
```bash
# Baixa todos os dados
git fetch origin
```

### 5. Faz Checkout da Main/Master
```bash
# Cria e alterna para branch principal
git checkout main
```

**Tudo isso com UM comando!** ✨

## 📊 Clonando Projetos Grandes

Repositórios grandes (como Linux kernel) podem demorar:

### Clone Superficial (Shallow Clone)

Clone apenas o commit mais recente (sem histórico):

```bash
git clone --depth 1 https://github.com/usuario/projeto-gigante.git
```

**Vantagens:**
- ✅ Muito mais rápido
- ✅ Ocupa menos espaço

**Desvantagens:**
- ❌ Sem histórico completo
- ❌ Limitações para alguns comandos

**Quando usar:**
- Deploy de produção
- CI/CD
- Apenas quer ver o código atual

## 🔄 Depois de Clonar

Depois de clonar um repositório, você pode:

### Trabalhar Normalmente

```bash
# Criar branch
git switch -c minha-feature

# Modificar arquivos
echo "mudança" >> arquivo.txt

# Commitar
git add .
git commit -m "Minha mudança"

# Fazer push (se tiver permissão)
git push origin minha-feature
```

### Manter Atualizado

```bash
# Baixar atualizações
git pull

# Ou
git fetch
git merge origin/main
```

### Contribuir (Open Source)

Se for projeto de outra pessoa:
1. Fork no GitHub
2. Clone o seu fork
3. Faça mudanças
4. Push para seu fork
5. Abra Pull Request

(Veremos isso em detalhes depois!)

## 🌐 Clonando Repositórios Privados

Para clonar repositórios privados, você precisa ter:

### Via HTTPS:
- Acesso ao repositório (permissão)
- Credenciais (token de acesso)

```bash
git clone https://github.com/usuario/repo-privado.git
# Pede username e token
```

### Via SSH:
- Chave SSH configurada no GitHub
- Acesso ao repositório

```bash
git clone git@github.com:usuario/repo-privado.git
```

## 💡 Casos de Uso Práticos

### 1. Estudando um Framework

```bash
# Clone React para estudar
git clone https://github.com/facebook/react.git
cd react
code .
```

### 2. Começando Projeto em Novo Computador

```bash
# No computador novo
git clone https://github.com/seu-usuario/seu-projeto.git
cd seu-projeto
npm install  # ou pip install -r requirements.txt
```

### 3. Revisando Pull Request

```bash
# Clone o fork da pessoa
git clone https://github.com/colaborador/projeto.git
cd projeto
git switch branch-do-pr
# Revise o código
```

### 4. Usando Template

```bash
# Clone um template
git clone https://github.com/usuario/template-react.git meu-app
cd meu-app
rm -rf .git  # Remove o Git do template
git init     # Inicia seu próprio Git
```

## 🖱️ GitHub Desktop

Se você usa GitHub Desktop:

1. Abra GitHub Desktop
2. **File > Clone Repository**
3. Escolha da lista ou cole URL
4. Escolha pasta local
5. Click "Clone"

## ⚠️ Troubleshooting

### Erro: "Could not resolve host"

**Problema:** Sem internet ou URL errada.

**Solução:**
- Verifique sua conexão
- Verifique se a URL está correta

### Erro: "Repository not found"

**Problema:** Repositório não existe ou é privado e você não tem acesso.

**Solução:**
- Verifique se a URL está correta
- Se for privado, verifique se tem permissão
- Verifique credenciais

### Erro: "Permission denied"

**Problema:** Sem permissão ou credenciais erradas.

**Solução:**
- Para repositório privado, forneça credenciais corretas
- Use token de acesso, não senha
- Configure autenticação (cache de credenciais)

### Clone Muito Lento

**Problema:** Repositório muito grande ou internet lenta.

**Solução:**
- Use shallow clone: `git clone --depth 1 URL`
- Clone apenas uma branch: `git clone -b main --single-branch URL`
- Aguarde... ☕

## 🔄 Comandos Resumidos

```bash
# Clone básico
git clone URL

# Clone com nome diferente
git clone URL nome-pasta

# Clone de branch específica
git clone -b branch-name URL

# Clone raso (sem histórico)
git clone --depth 1 URL

# Clone apenas uma branch
git clone -b main --single-branch URL

# Ver remoto após clone
git remote -v

# Ver branches após clone
git branch -a
```

## 🎓 Resumo

✅ Você aprendeu:
- O que é clone e por que usar
- Como clonar repositórios via terminal e VS Code
- Diferença entre clone e download ZIP
- O que acontece automaticamente ao clonar
- Como clonar repositórios grandes (shallow clone)
- Como trabalhar após clonar
- Casos de uso práticos
- Solução de problemas comuns

## 🎯 Exercício Prático

Pratique clonando repositórios:

**Exercício 1: Clone projeto famoso**
```bash
git clone https://github.com/github/gitignore.git
cd gitignore
git log --oneline -5
git branch -a
```

**Exercício 2: Clone seu próprio projeto**
1. Crie um repositório no GitHub (se ainda não tem)
2. Clone para outra pasta no seu computador
3. Faça mudanças
4. Comite
5. Push
6. Veja as mudanças no GitHub

**Exercício 3: Clone e explore**
- Clone: `https://github.com/airbnb/javascript.git`
- É um guia de estilo JavaScript
- Explore os arquivos
- Veja o histórico

---

## 🎯 Próximos Passos

Agora você sabe clonar repositórios! Vamos aprender a enviar mudanças de volta com **push**.

➡️ **Próximo:** [Push: Enviando Alterações](16-push.md)
