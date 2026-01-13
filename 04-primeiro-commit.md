# 4. Seu Primeiro Commit

## 🎯 O que é um Commit?

Um **commit** é como tirar uma **foto** do seu projeto em um momento específico. É um ponto de salvamento no histórico.

Cada commit guarda:
- **Quais arquivos** mudaram
- **O que** mudou em cada arquivo
- **Quem** fez a mudança
- **Quando** foi feita
- **Por que** foi feita (através da mensagem do commit)

Pense no commit como um checkpoint em um jogo - você pode voltar para ele a qualquer momento!

## 🔄 O Fluxo do Commit

Para fazer um commit, seguimos 2 passos:

1. **ADD**: Adicionar arquivos na "área de stage" (preparação)
2. **COMMIT**: Tirar a "foto" dos arquivos que estão na área de stage

```
Arquivo modificado → git add → Área de Stage → git commit → Histórico
```

Por que dois passos? Porque às vezes você modifica vários arquivos, mas quer commitar apenas alguns. O `git add` deixa você escolher o que vai no commit.

## 🎬 Fazendo Seu Primeiro Commit

Vamos commitar o arquivo `README.md` que criamos no capítulo anterior.

### ✅ Via Terminal

**1. Adicione o arquivo na área de stage:**
```bash
git add README.md
```

**2. Verifique o status:**
```bash
git status
```

Você verá:
```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```

Agora o arquivo está **staged** (preparado)! A cor mudou para verde.

**3. Faça o commit:**
```bash
git commit -m "Adiciona README com descrição do projeto"
```

A flag `-m` significa "mensagem". Sempre coloque uma mensagem descrevendo o que você fez.

**Pronto! 🎉** Você verá algo como:
```
[main (root-commit) a1b2c3d] Adiciona README com descrição do projeto
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

### 🖱️ Via VS Code

**1. Vá no Source Control:**
- Clique no ícone do **Source Control** (ou pressione `Ctrl+Shift+G`)

**2. Adicione o arquivo na área de stage:**
- Passe o mouse sobre o arquivo `README.md`
- Clique no ícone **+** (plus) que aparece ao lado do arquivo

Ou:
- Clique no ícone **+** ao lado de "Changes" para adicionar TODOS os arquivos de uma vez

**3. Escreva a mensagem do commit:**
- No campo de texto no topo (onde está escrito "Message"), digite:
  ```
  Adiciona README com descrição do projeto
  ```

**4. Faça o commit:**
- Pressione `Ctrl+Enter` ou
- Clique no botão **✓ Commit** (no topo do painel)

**Pronto! 🎉** Você fez seu primeiro commit pelo VS Code!

## 🔍 Verificando o Que Foi Feito

### ✅ Via Terminal

**Ver o histórico de commits:**
```bash
git log
```

Você verá:
```
commit a1b2c3d4e5f6g7h8i9j0 (HEAD -> main)
Author: Seu Nome <seu.email@exemplo.com>
Date:   Mon Jan 13 10:30:00 2026 -0300

    Adiciona README com descrição do projeto
```

**Versão mais compacta:**
```bash
git log --oneline
```

Resultado:
```
a1b2c3d Adiciona README com descrição do projeto
```

### 🖱️ Via VS Code

**Método 1: Pelo Source Control**
1. No painel Source Control, clique nos **três pontinhos** (⋯)
2. Selecione **View History** (pode precisar de extensão)

**Método 2: Usando extensão (recomendado)**
1. Instale a extensão **Git Graph** ou **GitLens**
2. Clique no ícone que aparece na barra inferior
3. Você verá uma visualização gráfica dos commits

**Método 3: Terminal integrado**
1. Abra o terminal (`` Ctrl+` ``)
2. Use `git log` ou `git log --oneline`

## 📝 Praticando: Mais Commits

Vamos fazer mais algumas mudanças para praticar!

### ✅ Via Terminal

**1. Crie um novo arquivo:**
```bash
echo "print('Olá, Git!')" > hello.py
```

**2. Modifique o README:**
```bash
echo "" >> README.md
echo "Este é um projeto para aprender Git." >> README.md
```

**3. Veja o status:**
```bash
git status
```

Você verá:
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.py
```

**4. Adicione os dois arquivos:**
```bash
git add README.md hello.py
```

Ou adicione todos de uma vez:
```bash
git add .
```

O ponto `.` significa "adicionar todos os arquivos modificados/novos".

**5. Faça o commit:**
```bash
git commit -m "Adiciona arquivo Python e atualiza README"
```

### 🖱️ Via VS Code

**1. Crie um novo arquivo:**
- Clique em **File > New File**
- Cole: `print('Olá, Git!')`
- Salve como `hello.py`

**2. Modifique o README:**
- Abra o arquivo `README.md`
- Adicione uma nova linha:
  ```markdown
  # Meu Primeiro Projeto
  
  Este é um projeto para aprender Git.
  ```
- Salve (`Ctrl+S`)

**3. Veja as mudanças no Source Control:**
- Você verá 2 arquivos na seção "Changes"
- `hello.py` com **U** (untracked)
- `README.md` com **M** (modified)

**4. Stage os arquivos:**
- Clique no **+** ao lado de "Changes" para adicionar todos
- Ou clique no **+** de cada arquivo individualmente

**5. Escreva a mensagem e comite:**
- Digite: `Adiciona arquivo Python e atualiza README`
- Pressione `Ctrl+Enter`

## 📊 Visualizando o Histórico

### ✅ Via Terminal

```bash
git log --oneline
```

Resultado:
```
b2c3d4e Adiciona arquivo Python e atualiza README
a1b2c3d Adiciona README com descrição do projeto
```

Agora você tem **2 commits** no seu histórico! 🎉

## 💡 Boas Práticas para Commits

### ✅ Faça

- **Commits pequenos e frequentes**: Um commit por funcionalidade/correção
- **Mensagens claras**: "Adiciona validação de email" ao invés de "mudanças"
- **Commits completos**: Não comite código quebrado
- **Use verbos no imperativo**: "Adiciona" ao invés de "Adicionado" ou "Adicionando"

### ❌ Evite

- Commits gigantes com muitas mudanças não relacionadas
- Mensagens vagas: "fix", "update", "changes"
- Commitar código que não funciona
- Deixar arquivos temporários no commit

### 📝 Exemplos de Boas Mensagens

```bash
git commit -m "Adiciona formulário de login"
git commit -m "Corrige bug no cálculo de desconto"
git commit -m "Remove código não utilizado"
git commit -m "Atualiza documentação da API"
git commit -m "Refatora função de validação"
```

## 🔄 Comandos Resumidos

```bash
# Adicionar arquivos
git add nome-arquivo.txt      # Adiciona um arquivo específico
git add .                     # Adiciona todos os arquivos modificados
git add *.js                  # Adiciona todos os arquivos .js

# Fazer commit
git commit -m "Mensagem"      # Commit com mensagem

# Ver histórico
git log                       # Histórico completo
git log --oneline            # Histórico resumido
git log --graph              # Histórico com gráfico

# Ver status
git status                    # Estado atual do repositório
```

## ⚠️ Troubleshooting

### Erro: "Please tell me who you are"

Você esqueceu de configurar nome e email. Volte para o [capítulo 2](02-instalacao-configuracao.md).

### Esqueci a mensagem do commit

Se você executou `git commit` sem o `-m`, o Git abriu um editor (provavelmente Vim).

**Para sair do Vim:**
1. Pressione `ESC`
2. Digite `:q!`
3. Pressione `Enter`

Depois execute novamente com `-m`:
```bash
git commit -m "Sua mensagem"
```

### Como desfazer um commit?

Veremos isso em capítulos futuros! Por enquanto, não se preocupe.

## 🎓 Resumo

✅ Você aprendeu:
- O que é um commit
- O fluxo: modificar → add → commit
- Como fazer commits via terminal e VS Code
- Como ver o histórico
- Boas práticas para mensagens de commit

## 🎯 Exercício Prático

Pratique fazendo mais alguns commits:

1. Crie um arquivo `style.css`
2. Adicione nele: `body { margin: 0; }`
3. Faça o commit: "Adiciona arquivo de estilos"
4. Modifique o CSS adicionando: `padding: 0;`
5. Faça outro commit: "Adiciona padding zero ao body"
6. Use `git log --oneline` para ver o histórico

---

## 🎯 Próximos Passos

Agora que você sabe fazer commits, vamos entender melhor o conceito de **área de stage** (staging area).

➡️ **Próximo:** [Entendendo a Área de Stage](05-area-de-stage.md)
