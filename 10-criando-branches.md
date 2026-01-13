# 10. Criando e Alternando Entre Branches

## 🎯 Comandos Principais

Para trabalhar com branches, você precisa saber três coisas:

1. **Criar** uma nova branch
2. **Alternar** entre branches
3. **Ver** quais branches existem

Vamos aprender cada uma! 🚀

## 📝 Criando uma Nova Branch

### ✅ Via Terminal

**Comando básico:**
```bash
git branch nome-da-branch
```

**Exemplo:**
```bash
git branch feature-login
```

Isso **cria** a branch, mas você **ainda está na branch atual**.

**Verificar:**
```bash
git branch
```

Resultado:
```
  feature-login
* main
```

O `*` mostra que você ainda está na `main`.

### 🖱️ Via VS Code

**Método 1: Barra inferior**
1. Clique no nome da branch na barra inferior (ex: `main`)
2. Selecione **+ Create new branch**
3. Digite o nome da nova branch
4. Pressione Enter

**Método 2: Command Palette**
1. Pressione `Ctrl+Shift+P`
2. Digite "Git: Create Branch"
3. Digite o nome da branch
4. Pressione Enter

**Método 3: Source Control**
1. Abra Source Control (`Ctrl+Shift+G`)
2. Clique nos **três pontinhos** (⋯)
3. Selecione **Branch > Create Branch**
4. Digite o nome

## 🔄 Alternando Entre Branches (Checkout/Switch)

Depois de criar uma branch, você precisa "ir para ela".

### ✅ Via Terminal

**Comando moderno (recomendado):**
```bash
git switch nome-da-branch
```

**Exemplo:**
```bash
git switch feature-login
```

**Comando tradicional (ainda funciona):**
```bash
git checkout nome-da-branch
```

**Verificar onde você está:**
```bash
git branch
```

Resultado:
```
* feature-login
  main
```

Agora você está em `feature-login`! ✨

### 🖱️ Via VS Code

**Método 1: Barra inferior (mais rápido)**
1. Clique no nome da branch na barra inferior
2. Selecione a branch para onde quer ir
3. Pronto!

**Método 2: Command Palette**
1. Pressione `Ctrl+Shift+P`
2. Digite "Git: Checkout to"
3. Selecione a branch

## ⚡ Criar E Alternar de Uma Vez

É muito comum querer criar uma branch e ir para ela imediatamente.

### ✅ Via Terminal

**Comando moderno:**
```bash
git switch -c nome-da-branch
```

**Comando tradicional:**
```bash
git checkout -b nome-da-branch
```

O `-c` (ou `-b`) significa "create" (criar).

**Exemplo completo:**
```bash
git switch -c feature-cadastro
```

Isso:
1. ✅ Cria a branch `feature-cadastro`
2. ✅ Alterna para ela automaticamente

### 🖱️ Via VS Code

Quando você cria uma branch pelos métodos do VS Code, ele já alterna automaticamente para a nova branch!

## 📝 Exemplo Prático Completo

Vamos criar um cenário real:

### ✅ Via Terminal

```bash
# 1. Ver onde estou
git branch
# * main

# 2. Criar e ir para nova branch
git switch -c feature-menu

# 3. Confirmar que mudei
git branch
# * feature-menu
#   main

# 4. Fazer alterações
echo "Menu do site" > menu.html
git add menu.html
git commit -m "Adiciona página de menu"

# 5. Voltar para main
git switch main

# 6. Ver que menu.html não está aqui
ls
# (menu.html não aparece!)

# 7. Voltar para feature-menu
git switch feature-menu

# 8. Ver que menu.html está aqui
ls
# (menu.html aparece!)
```

### 🖱️ Via VS Code

**1. Criar nova branch:**
- Clique em `main` na barra inferior
- Selecione **+ Create new branch**
- Digite `feature-menu`
- A branch é criada e você já está nela

**2. Fazer alterações:**
- Crie arquivo `menu.html`
- Adicione conteúdo: "Menu do site"
- Salve o arquivo

**3. Fazer commit:**
- Abra Source Control (`Ctrl+Shift+G`)
- Stage o arquivo (`+`)
- Digite mensagem: "Adiciona página de menu"
- Commit (`Ctrl+Enter`)

**4. Voltar para main:**
- Clique em `feature-menu` na barra inferior
- Selecione `main`
- **Observe:** `menu.html` desaparece do explorador!

**5. Voltar para feature-menu:**
- Clique em `main` na barra inferior
- Selecione `feature-menu`
- **Observe:** `menu.html` reaparece!

## 🔍 Listando Branches

### ✅ Via Terminal

**Branches locais:**
```bash
git branch
```

**Branches locais com último commit:**
```bash
git branch -v
```

Resultado:
```
* feature-menu  a1b2c3d Adiciona página de menu
  main          z9y8x7w Commit anterior
```

**Todas as branches (incluindo remotas):**
```bash
git branch -a
```

**Apenas branches remotas:**
```bash
git branch -r
```

### 🖱️ Via VS Code

**Ver lista de branches:**
- Clique no nome da branch na barra inferior
- Você verá a lista de todas as branches

**Com Git Graph:**
- Abra o Git Graph
- Você vê visualmente todas as branches e onde cada uma está

## 🗑️ Deletando Branches

Depois de terminar o trabalho em uma branch e fazer merge, você pode deletá-la.

### ✅ Via Terminal

**Deletar branch (seguro):**
```bash
git branch -d nome-da-branch
```

O `-d` só deleta se a branch já foi merged.

**Forçar deleção:**
```bash
git branch -D nome-da-branch
```

O `-D` deleta mesmo se não foi merged (cuidado!).

**Exemplo:**
```bash
# Você está na main
git switch main

# Deleta a branch feature-menu
git branch -d feature-menu
```

**⚠️ Não pode deletar a branch em que você está!**

### 🖱️ Via VS Code

**Método 1:**
1. Clique com o botão direito no nome da branch (na lista)
2. Selecione **Delete Branch**

**Método 2: Via Source Control**
1. Abra Source Control
2. Clique nos **três pontinhos** (⋯)
3. **Branch > Delete Branch**
4. Selecione a branch a deletar

## 📊 Situações Práticas

### Situação 1: Trabalho em Andamento

```bash
# Você está desenvolvendo
git switch -c feature-nova
# ... trabalha ...
git add .
git commit -m "Progresso parcial"

# Precisa voltar para main urgentemente
git switch main
# Seu trabalho está salvo na branch feature-nova!
```

### Situação 2: Múltiplas Funcionalidades

```bash
# Trabalha no login
git switch -c feature-login
# ... desenvolve login ...
git commit -m "Adiciona login"

# Precisa fazer o cadastro também
git switch main  # Volta para base limpa
git switch -c feature-cadastro
# ... desenvolve cadastro ...
git commit -m "Adiciona cadastro"

# Agora tem duas branches independentes!
```

### Situação 3: Experiência Rápida

```bash
# Quer testar uma ideia
git switch -c experimento
# ... testa ...

# Não deu certo, volta e deleta
git switch main
git branch -D experimento  # Força deleção
```

## ⚠️ Mudanças Não Commitadas

**E se você tiver mudanças não commitadas e tentar trocar de branch?**

### Cenário A: Mudanças não conflitam

O Git leva as mudanças junto para a outra branch.

### Cenário B: Mudanças conflitam

O Git **não deixa** você trocar de branch:

```
error: Your local changes to the following files would be overwritten by checkout:
        arquivo.txt
Please commit your changes or stash them before you switch branches.
```

**Soluções:**

**1. Commitar as mudanças:**
```bash
git add .
git commit -m "Salva progresso"
git switch outra-branch
```

**2. Usar stash (guardar temporariamente):**
```bash
git stash
git switch outra-branch
# Quando voltar:
git switch branch-original
git stash pop
```

Veremos stash em detalhes mais tarde!

## 🎯 Boas Práticas

### ✅ Faça:

- Crie branches com nomes descritivos
- Use uma branch por funcionalidade
- Faça commits frequentes na sua branch
- Delete branches após o merge
- Mantenha a main sempre funcional

### ❌ Evite:

- Branches com nomes genéricos (`test`, `branch1`)
- Deixar branches antigas e não utilizadas
- Trabalhar direto na main
- Múltiplas funcionalidades na mesma branch

## 🔄 Comandos Resumidos

```bash
# Criar branch
git branch nome-da-branch

# Alternar para branch
git switch nome-da-branch
git checkout nome-da-branch  # (comando antigo)

# Criar e alternar de uma vez
git switch -c nome-da-branch
git checkout -b nome-da-branch  # (comando antigo)

# Listar branches
git branch              # Locais
git branch -v           # Com último commit
git branch -a           # Todas (locais + remotas)

# Deletar branch
git branch -d nome-da-branch   # Seguro
git branch -D nome-da-branch   # Forçado

# Ver branch atual
git branch
git status
```

## 💡 Dica Pro

**Configure cores para branches no terminal:**
```bash
git config --global color.branch auto
```

**Veja a branch atual no prompt:**
Muitos terminais mostram automaticamente. Se não, procure por "git prompt" para sua shell.

## 🎓 Resumo

✅ Você aprendeu:
- Como criar branches
- Como alternar entre branches
- Como criar e alternar de uma vez
- Como listar e visualizar branches
- Como deletar branches
- Situações práticas do dia a dia
- O que fazer com mudanças não commitadas

## 🎯 Exercício Prático

Pratique criando branches:

1. Crie uma branch `feature-header`
2. Alterne para ela
3. Crie um arquivo `header.html`
4. Faça um commit
5. Volte para `main`
6. Crie outra branch `feature-footer`
7. Alterne para ela
8. Crie um arquivo `footer.html`
9. Faça um commit
10. Use `git log --oneline --graph --all` para ver o histórico

---

## 🎯 Próximos Passos

Agora que você sabe criar e alternar branches, vamos aprender a **juntar branches** (merge)!

➡️ **Próximo:** [Mesclando Branches (Merge)](11-merge.md)
