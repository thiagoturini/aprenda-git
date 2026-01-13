# 5. Entendendo a Área de Stage

## 🎯 O que é a Área de Stage?

A **área de stage** (também chamada de "staging area" ou "index") é como uma **área de preparação** antes do commit.

Pense nela como uma **mesa de trabalho** onde você coloca os arquivos que quer incluir no próximo commit.

## 📦 As Três Áreas do Git

Seu projeto tem três "áreas" principais:

```
1. Working Directory (Diretório de Trabalho)
   ↓ git add
2. Staging Area (Área de Stage)
   ↓ git commit
3. Repository (Repositório)
```

### 1. **Working Directory** (Onde você trabalha)
- Os arquivos do seu projeto no computador
- É onde você faz as modificações
- Arquivos aqui estão **modificados** mas não salvos no Git ainda

### 2. **Staging Area** (Área de preparação)
- Arquivos que você escolheu para o próximo commit
- É como separar as roupas que vai lavar
- Arquivos aqui estão **prontos** para serem commitados

### 3. **Repository** (Histórico permanente)
- Os commits já salvos
- O histórico do projeto
- Arquivos aqui estão **permanentemente salvos**

## 🤔 Por Que Existe a Área de Stage?

Imagine este cenário:

Você está trabalhando em um site e modificou 5 arquivos:
- `index.html` - Adicionou o formulário de contato ✅
- `style.css` - Estilizou o formulário ✅
- `script.js` - Adicionou validação do formulário ✅
- `about.html` - Começou a página "sobre" (não terminou ainda) ❌
- `debug.js` - Código de teste temporário ❌

Você quer commitar apenas os 3 primeiros (que estão prontos), mas não os outros 2.

**A área de stage permite isso!** Você escolhe exatamente o que vai no commit.

## 📝 Praticando com a Área de Stage

Vamos criar um exemplo prático:

### ✅ Via Terminal

**1. Crie vários arquivos:**
```bash
echo "Página principal" > index.html
echo "Página sobre" > about.html
echo "Estilos" > style.css
echo "Código temporário" > temp.js
```

**2. Veja o status:**
```bash
git status
```

Todos aparecem como **untracked** (não rastreados).

**3. Adicione apenas alguns arquivos:**
```bash
git add index.html style.css
```

**4. Veja o status novamente:**
```bash
git status
```

Agora você verá:
```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   index.html
        new file:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        about.html
        temp.js
```

**5. Faça o commit apenas dos arquivos staged:**
```bash
git commit -m "Adiciona página principal e estilos"
```

Os arquivos `about.html` e `temp.js` **não** foram incluídos no commit!

### 🖱️ Via VS Code

**1. Crie os arquivos:**
- Crie `index.html` com conteúdo "Página principal"
- Crie `about.html` com conteúdo "Página sobre"
- Crie `style.css` com conteúdo "Estilos"
- Crie `temp.js` com conteúdo "Código temporário"

**2. Abra o Source Control:**
- Pressione `Ctrl+Shift+G`
- Você verá 4 arquivos na seção "Changes"

**3. Stage apenas alguns arquivos:**
- Clique no **+** ao lado de `index.html`
- Clique no **+** ao lado de `style.css`

Agora você verá:
- **Staged Changes** (2 arquivos): index.html, style.css
- **Changes** (2 arquivos): about.html, temp.js

**4. Faça o commit:**
- Digite a mensagem: "Adiciona página principal e estilos"
- Pressione `Ctrl+Enter`

Apenas os arquivos em **Staged Changes** foram commitados!

## 🔄 Removendo da Área de Stage (Unstage)

E se você adicionar um arquivo por engano?

### ✅ Via Terminal

**Remover um arquivo específico da stage area:**
```bash
git restore --staged nome-do-arquivo
```

**Ou (comando antigo, ainda funciona):**
```bash
git reset HEAD nome-do-arquivo
```

**Exemplo:**
```bash
git add temp.js
git restore --staged temp.js
```

### 🖱️ Via VS Code

**Método 1: Clique no ícone**
- No painel Source Control
- Passe o mouse sobre o arquivo em "Staged Changes"
- Clique no ícone **−** (minus) que aparece

**Método 2: Comando**
- Clique com o botão direito no arquivo
- Selecione **Unstage Changes**

## 📊 Estados Visuais

### No VS Code:

Os arquivos aparecem com letras diferentes:

- **U** (Untracked): Arquivo novo que o Git nunca viu
- **M** (Modified): Arquivo que foi modificado
- **A** (Added): Arquivo adicionado à stage area
- **D** (Deleted): Arquivo deletado
- **R** (Renamed): Arquivo renomeado

### No Terminal:

Cores diferentes:
- **Vermelho**: Arquivos não staged
- **Verde**: Arquivos staged (prontos para commit)

## 🎯 Estratégias de Stage

### Estratégia 1: Stage Seletivo (Recomendado)

Adicione apenas o que está pronto:
```bash
git add arquivo1.js
git add arquivo2.css
git commit -m "Adiciona funcionalidade X"
```

### Estratégia 2: Stage Tudo

Para projetos pequenos ou quando tudo está pronto:
```bash
git add .
git commit -m "Implementa funcionalidade completa"
```

### Estratégia 3: Stage Interativo (Avançado)

Permite escolher parte de um arquivo:
```bash
git add -p arquivo.js
```

O Git mostrará cada mudança e você escolhe o que adicionar (y/n).

## 🖱️ Stage no VS Code: Recursos Avançados

### Ver o Diff Antes de Stage

1. No Source Control, clique no arquivo
2. Você verá o diff (comparação do antes e depois)
3. Linhas em vermelho = removidas
4. Linhas em verde = adicionadas

### Stage Linhas Específicas

1. Abra o diff do arquivo
2. Selecione as linhas que quer stage
3. Clique com o botão direito
4. Selecione **Stage Selected Ranges**

Incrível! Você pode commitar apenas parte de um arquivo! 🎉

## 💡 Quando Usar Stage Seletivo?

**Use quando:**
- Fez várias mudanças não relacionadas
- Quer commits pequenos e focados
- Tem arquivos de teste ou debug
- Quer revisar o que está commitando

**Pode pular quando:**
- Todas as mudanças são relacionadas
- Projeto pequeno
- Trabalhando sozinho em algo simples

## 🔍 Comandos para Inspecionar a Stage Area

### ✅ Via Terminal

**Ver o que está staged:**
```bash
git status
```

**Ver diferenças dos arquivos staged:**
```bash
git diff --staged
```

Ou:
```bash
git diff --cached
```

**Ver diferenças dos arquivos NÃO staged:**
```bash
git diff
```

### 🖱️ Via VS Code

- Clique no arquivo no Source Control
- Você verá o diff automaticamente
- Arquivos em "Staged Changes" = vão no commit
- Arquivos em "Changes" = não vão no commit

## 🎓 Fluxo Completo

```bash
# 1. Modificar arquivos
echo "conteúdo" > arquivo.txt

# 2. Ver o que mudou
git status

# 3. Adicionar na stage area
git add arquivo.txt

# 4. Ver o que será commitado
git diff --staged

# 5. Fazer o commit
git commit -m "Mensagem"
```

## ⚠️ Cuidados

### ⚠️ Não comite arquivos temporários

Evite adicionar:
- Arquivos de backup (`*~`, `*.bak`)
- Logs (`*.log`)
- Dependências (`node_modules/`, `venv/`)
- Arquivos de configuração local (`.env`)

Veremos como ignorar esses arquivos no capítulo sobre `.gitignore`!

### ⚠️ Revise antes de commitar

Sempre use `git status` e `git diff --staged` para revisar o que vai no commit.

## 🎓 Resumo

✅ Você aprendeu:
- O que é a área de stage
- As três áreas do Git (Working, Stage, Repository)
- Por que a área de stage existe
- Como adicionar e remover da stage
- Stage seletivo vs stage completo
- Como visualizar mudanças

## 🔄 Comandos Importantes

```bash
git add arquivo.txt          # Adiciona arquivo específico
git add .                    # Adiciona todos os arquivos
git add *.js                 # Adiciona todos arquivos .js
git restore --staged arquivo # Remove da stage area
git diff                     # Mostra mudanças não staged
git diff --staged            # Mostra mudanças staged
git status                   # Mostra estado atual
```

## 🎯 Exercício

1. Crie 3 arquivos: `a.txt`, `b.txt`, `c.txt`
2. Adicione apenas `a.txt` e `b.txt` na stage area
3. Faça um commit com esses dois arquivos
4. Depois adicione `c.txt` e faça outro commit
5. Use `git log --oneline` para ver os dois commits separados

---

## 🎯 Próximos Passos

Agora que você entende a área de stage, vamos aprender a visualizar o histórico de commits de forma mais detalhada!

➡️ **Próximo:** [Visualizando o Histórico](06-historico-log.md)
