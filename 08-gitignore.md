# 8. O Arquivo .gitignore

## 🎯 O que é o .gitignore?

O `.gitignore` é um arquivo especial que diz ao Git **quais arquivos ele deve ignorar**.

Esses arquivos continuam existindo no seu computador, mas o Git:
- ❌ Não os rastreia
- ❌ Não os adiciona nos commits
- ❌ Não os envia para o repositório remoto

## 🤔 Por Que Ignorar Arquivos?

Existem arquivos que **não devem** estar no repositório:

### 1. **Arquivos Temporários**
- Backups: `*~`, `*.bak`
- Cache: `.cache/`
- Logs: `*.log`

### 2. **Dependências** (podem ser reinstaladas)
- Node.js: `node_modules/`
- Python: `venv/`, `__pycache__/`
- Ruby: `vendor/bundle/`

### 3. **Arquivos de Configuração Local**
- `.env` (senhas e chaves secretas!)
- `.vscode/settings.json` (configurações pessoais)
- `.idea/` (configurações do IDE)

### 4. **Arquivos Gerados** (compilados)
- `*.o`, `*.class`
- `dist/`, `build/`
- `*.exe`

### 5. **Arquivos do Sistema Operacional**
- macOS: `.DS_Store`
- Windows: `Thumbs.db`, `desktop.ini`
- Linux: `.directory`

## 📝 Criando o Arquivo .gitignore

O `.gitignore` deve estar na **raiz do seu repositório** (pasta principal do projeto).

### ✅ Via Terminal

**Criar o arquivo:**
```bash
touch .gitignore
```

**Adicionar conteúdo:**
```bash
echo "node_modules/" >> .gitignore
echo "*.log" >> .gitignore
echo ".env" >> .gitignore
```

**Ou editar com editor:**
```bash
nano .gitignore
```

### 🖱️ Via VS Code

**Método 1: Criar novo arquivo**
1. Clique com o botão direito na pasta raiz do projeto
2. Selecione **New File**
3. Digite `.gitignore` como nome
4. Adicione os padrões de arquivos a ignorar

**Método 2: Mais rápido**
1. Pressione `Ctrl+N` (novo arquivo)
2. Salve como `.gitignore` (`Ctrl+S`)
3. Adicione o conteúdo

## 📋 Sintaxe do .gitignore

### Ignorar Arquivo Específico

```gitignore
secrets.txt
```

Ignora o arquivo `secrets.txt`.

### Ignorar Todos Arquivos de um Tipo

```gitignore
*.log
```

Ignora todos arquivos `.log` (debug.log, error.log, etc).

### Ignorar Pasta

```gitignore
node_modules/
```

Ignora toda a pasta `node_modules/` e seu conteúdo.

### Ignorar Arquivos em Qualquer Lugar

```gitignore
**/temp
```

Ignora pasta ou arquivo `temp` em qualquer lugar do projeto.

### Exceções (Não Ignorar)

```gitignore
# Ignora todos .log
*.log

# MAS não ignora important.log
!important.log
```

O `!` significa "exceção" - esse arquivo NÃO será ignorado.

### Comentários

```gitignore
# Isto é um comentário
# Use para documentar seu .gitignore
```

## 🎯 Exemplos Práticos

### Projeto Node.js

```gitignore
# Dependências
node_modules/
npm-debug.log
yarn-error.log

# Arquivos de ambiente
.env
.env.local
.env.production

# Arquivos de build
dist/
build/

# Cache
.cache/
.parcel-cache/

# Logs
logs/
*.log

# Sistema Operacional
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/
*.swp
*.swo
```

### Projeto Python

```gitignore
# Ambientes virtuais
venv/
env/
ENV/
.venv

# Cache do Python
__pycache__/
*.py[cod]
*$py.class

# Arquivos compilados
*.so
*.egg
*.egg-info/
dist/
build/

# Jupyter Notebooks
.ipynb_checkpoints/

# Ambiente
.env

# Sistema Operacional
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
*.swp
```

### Projeto Java

```gitignore
# Arquivos compilados
*.class
*.jar
*.war
*.ear

# Logs
*.log

# Diretórios de build
target/
build/
out/

# IDE
.idea/
.eclipse/
.vscode/
*.iml

# Sistema Operacional
.DS_Store
Thumbs.db
```

### Projeto React

```gitignore
# Dependências
node_modules/

# Build
/build
/dist

# Produção
.env.production
.env.local

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Cache
.cache/

# Sistema Operacional
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/
```

## 🌐 Templates Prontos

Você pode usar templates prontos do GitHub!

**Acesse:**
- [github.com/github/gitignore](https://github.com/github/gitignore)

Tem templates para praticamente todas as linguagens e frameworks!

### ✅ Via Terminal

**Baixar template do Node.js:**
```bash
curl https://raw.githubusercontent.com/github/gitignore/main/Node.gitignore -o .gitignore
```

**Baixar template do Python:**
```bash
curl https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore -o .gitignore
```

### 🖱️ Via VS Code

**Com extensão:**
1. Instale a extensão **gitignore** (do CodeZombie)
2. Pressione `Ctrl+Shift+P`
3. Digite "Add gitignore"
4. Escolha a linguagem/framework

Ou:
1. Acesse o link do GitHub
2. Copie o conteúdo
3. Cole no seu `.gitignore`

## 🔧 Arquivo Já Está Sendo Rastreado?

Se você já commitou um arquivo **antes** de adicionar ao `.gitignore`, ele continuará sendo rastreado!

### Como Remover do Git (mas manter no computador)

### ✅ Via Terminal

**Remover um arquivo:**
```bash
git rm --cached arquivo.txt
```

**Remover uma pasta:**
```bash
git rm --cached -r pasta/
```

**Exemplo completo:**
```bash
# 1. Adicione ao .gitignore
echo ".env" >> .gitignore

# 2. Remova do Git (mas mantém no computador)
git rm --cached .env

# 3. Comite a remoção
git add .gitignore
git commit -m "Remove .env do repositório e adiciona ao gitignore"
```

### 🖱️ Via VS Code

1. Adicione o arquivo ao `.gitignore`
2. Abra o terminal integrado (`` Ctrl+` ``)
3. Execute os comandos acima

## 🔍 Verificando o que Será Ignorado

### ✅ Via Terminal

**Ver arquivos ignorados:**
```bash
git status --ignored
```

**Testar se um arquivo será ignorado:**
```bash
git check-ignore -v arquivo.txt
```

Resultado mostra qual regra do `.gitignore` está fazendo o arquivo ser ignorado.

## 💡 Padrões Globais (Ignorar em Todos os Projetos)

Você pode criar um `.gitignore` global para o seu usuário!

### ✅ Via Terminal

**1. Crie o arquivo global:**
```bash
touch ~/.gitignore_global
```

**2. Configure o Git:**
```bash
git config --global core.excludesfile ~/.gitignore_global
```

**3. Adicione padrões:**
```bash
echo ".DS_Store" >> ~/.gitignore_global
echo "Thumbs.db" >> ~/.gitignore_global
echo ".vscode/" >> ~/.gitignore_global
```

Agora esses arquivos serão ignorados em **todos** os seus projetos Git!

## ⚠️ Cuidados Importantes

### ❌ Nunca comite:
- **Senhas e chaves**: `.env`, `secrets.txt`
- **Tokens de API**: `config/keys.js`
- **Credenciais**: `credentials.json`
- **Certificados privados**: `*.pem`, `*.key`

### ✅ Sempre ignore:
- **Dependências**: `node_modules/`, `venv/`
- **Arquivos gerados**: `dist/`, `build/`
- **Logs**: `*.log`
- **Arquivos do SO**: `.DS_Store`, `Thumbs.db`

## 📚 Estrutura de Exemplo

```
meu-projeto/
├── .gitignore          ← Arquivo de ignore
├── .env                ← Ignorado
├── node_modules/       ← Ignorado
├── dist/               ← Ignorado
├── src/
│   ├── index.js        ← Commitado
│   └── app.js          ← Commitado
├── package.json        ← Commitado
└── README.md           ← Commitado
```

## 🎓 Exemplo Completo

### ✅ Via Terminal

```bash
# 1. Crie o projeto
mkdir meu-projeto
cd meu-projeto
git init

# 2. Crie o .gitignore
cat > .gitignore << EOF
# Dependências
node_modules/

# Ambiente
.env

# Logs
*.log

# Sistema Operacional
.DS_Store
Thumbs.db

# Editor
.vscode/
EOF

# 3. Crie arquivos
echo "console.log('App');" > app.js
echo "NODE_ENV=production" > .env
mkdir node_modules
echo "dependency" > node_modules/dep.txt

# 4. Veja o status
git status

# Apenas app.js e .gitignore aparecem!
# .env e node_modules/ são ignorados

# 5. Comite
git add .
git commit -m "Configuração inicial com .gitignore"
```

## 🔄 Comandos Resumidos

```bash
# Criar .gitignore
touch .gitignore

# Remover arquivo do Git (manter no computador)
git rm --cached arquivo.txt

# Ver arquivos ignorados
git status --ignored

# Testar se arquivo será ignorado
git check-ignore -v arquivo.txt

# Configurar .gitignore global
git config --global core.excludesfile ~/.gitignore_global
```

## 🎓 Resumo

✅ Você aprendeu:
- O que é o `.gitignore` e por que usar
- Que tipos de arquivos devem ser ignorados
- Como criar e configurar o `.gitignore`
- Sintaxe e padrões do `.gitignore`
- Como remover arquivos já rastreados
- Templates prontos para diferentes linguagens

## 🎯 Exercício

1. Crie um projeto novo
2. Crie um arquivo `.gitignore`
3. Adicione padrões para ignorar:
   - Arquivos `.log`
   - Pasta `temp/`
   - Arquivo `.env`
4. Crie esses arquivos e pasta
5. Use `git status` - eles não devem aparecer!
6. Crie um arquivo normal como `README.md`
7. Comite apenas o README e o .gitignore

---

## 🎯 Próximos Passos

Agora você sabe ignorar arquivos indesejados! Vamos aprender sobre **branches**, um dos recursos mais poderosos do Git.

➡️ **Próximo:** [O que são Branches](09-branches-conceito.md)
