# 📚 Guia Rápido de Referência Git

Este é um guia de consulta rápida com os comandos mais usados. Use como cola! 📋

## ⚙️ Configuração Inicial

```bash
# Configurar nome
git config --global user.name "Seu Nome"

# Configurar email
git config --global user.email "seu@email.com"

# Ver configurações
git config --list

# Editor padrão (VS Code)
git config --global core.editor "code --wait"

# Branch padrão
git config --global init.defaultBranch main
```

## 🆕 Criar Repositório

```bash
# Criar novo repositório
git init

# Clonar repositório existente
git clone URL

# Clonar branch específica
git clone -b nome-branch URL
```

## 📝 Alterações Básicas

```bash
# Ver status
git status

# Ver mudanças
git diff

# Adicionar arquivo
git add arquivo.txt

# Adicionar todos os arquivos
git add .

# Commitar
git commit -m "Mensagem"

# Add + commit junto
git commit -am "Mensagem"
```

## 📜 Histórico

```bash
# Ver histórico
git log

# Histórico resumido
git log --oneline

# Histórico com gráfico
git log --oneline --graph --all

# Últimos 5 commits
git log -5

# Histórico de um arquivo
git log arquivo.txt

# Detalhes de um commit
git show a1b2c3d
```

## 🔄 Desfazer Mudanças

```bash
# Descartar mudanças (arquivo)
git restore arquivo.txt

# Descartar todas mudanças
git restore .

# Remover da stage
git restore --staged arquivo.txt

# Alterar último commit
git commit --amend -m "Nova mensagem"

# Desfazer commit (manter mudanças)
git reset --soft HEAD~1

# Desfazer commit (descartar mudanças)
git reset --hard HEAD~1
```

## 🌿 Branches

```bash
# Listar branches
git branch

# Criar branch
git branch nome-branch

# Alternar para branch
git switch nome-branch
git checkout nome-branch  # (antigo)

# Criar e alternar
git switch -c nome-branch
git checkout -b nome-branch  # (antigo)

# Deletar branch
git branch -d nome-branch

# Deletar forçado
git branch -D nome-branch

# Ver branches remotas
git branch -a
```

## 🔀 Merge

```bash
# Fazer merge
git switch main
git merge nome-branch

# Abortar merge
git merge --abort

# Ver branches mescladas
git branch --merged

# Ver branches não mescladas
git branch --no-merged
```

## 🌐 Repositório Remoto

```bash
# Ver remotos
git remote -v

# Adicionar remoto
git remote add origin URL

# Remover remoto
git remote remove origin

# Ver informações do remoto
git remote show origin
```

## ⬆️ Push (Enviar)

```bash
# Push básico
git push

# Push primeira vez (com tracking)
git push -u origin main

# Push de branch específica
git push origin nome-branch

# Push todas as branches
git push --all

# Deletar branch remota
git push origin --delete nome-branch

# Force push (cuidado!)
git push --force-with-lease
```

## ⬇️ Pull (Receber)

```bash
# Pull básico
git pull

# Pull de remoto/branch específico
git pull origin main

# Pull com rebase
git pull --rebase

# Fetch (só baixar, sem merge)
git fetch

# Fetch de todos os remotos
git fetch --all
```

## 💾 Stash (Guardar Temporário)

```bash
# Guardar mudanças
git stash

# Guardar com mensagem
git stash save "Mensagem"

# Listar stashes
git stash list

# Aplicar último stash
git stash pop

# Aplicar stash específico
git stash apply stash@{0}

# Ver mudanças no stash
git stash show

# Deletar stash
git stash drop stash@{0}

# Limpar todos os stashes
git stash clear
```

## 🏷️ Tags

```bash
# Listar tags
git tag

# Criar tag
git tag v1.0.0

# Criar tag anotada
git tag -a v1.0.0 -m "Versão 1.0.0"

# Push de tags
git push origin v1.0.0

# Push todas as tags
git push --tags

# Deletar tag local
git tag -d v1.0.0

# Deletar tag remota
git push origin --delete v1.0.0
```

## 🔍 Busca e Inspeção

```bash
# Buscar em commits
git log --grep="palavra"

# Buscar por autor
git log --author="Nome"

# Buscar por data
git log --since="2 weeks ago"

# Ver quem mudou cada linha
git blame arquivo.txt

# Comparar branches
git diff main..feature

# Ver arquivos modificados
git diff --name-only
```

## 🚨 Resolução de Conflitos

```bash
# Ver arquivos com conflito
git diff --name-only --diff-filter=U

# Aceitar versão deles (theirs)
git checkout --theirs arquivo.txt

# Aceitar versão nossa (ours)
git checkout --ours arquivo.txt

# Depois de resolver
git add arquivo.txt
git commit
```

## 📋 .gitignore

Exemplos de padrões:

```gitignore
# Arquivo específico
secrets.txt

# Tipo de arquivo
*.log

# Pasta
node_modules/

# Exceção (não ignorar)
!important.log
```

## 🔧 Configurações Úteis

```bash
# Alias úteis
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.ci "commit"
git config --global alias.lg "log --oneline --graph --decorate"

# Colorir saída
git config --global color.ui auto

# Cache de credenciais (15 min)
git config --global credential.helper cache

# Cache de credenciais (permanente)
git config --global credential.helper store
```

## 🆘 Situações de Emergência

### Commitei no branch errado

```bash
# Salva o commit
git log  # copia o hash do commit

# Volta o branch
git reset --hard HEAD~1

# Vai para branch correto
git switch branch-correto

# Aplica o commit
git cherry-pick HASH-DO-COMMIT
```

### Fiz push de algo errado

```bash
# Volte localmente
git reset --hard HEAD~1

# Force push (SE estiver sozinho)
git push --force-with-lease
```

### Perdi commits

```bash
# Ver histórico de tudo
git reflog

# Recuperar commit perdido
git checkout HASH-DO-COMMIT
git switch -c branch-recuperada
```

### Commitei senha/arquivo sensível

```bash
# Remover do último commit
git rm --cached arquivo-sensivel
git commit --amend --no-edit

# Se já fez push
# Use BFG Repo-Cleaner ou git filter-branch
# E mude a senha imediatamente!
```

## 📱 VS Code: Atalhos

- `Ctrl+Shift+G` - Abrir Source Control
- `Ctrl+Enter` - Commit
- `Ctrl+Shift+P` → "Git: ..." - Comandos Git
- Clique na branch (barra inferior) - Trocar branch
- Ícone sync (barra inferior) - Pull/Push

## 🔗 Fluxo de Trabalho Típico

### Começar o dia

```bash
git switch main
git pull
git switch -c feature-nova
```

### Durante o trabalho

```bash
# Modificar arquivos
git add .
git commit -m "Descrição clara"
# Repetir...
```

### Finalizar feature

```bash
git switch main
git pull
git merge feature-nova
git push
git branch -d feature-nova
```

## 🎯 Comandos por Frequência

### Usa TODO DIA:

```bash
git status
git add .
git commit -m "..."
git push
git pull
git switch branch-name
```

### Usa FREQUENTEMENTE:

```bash
git branch
git log --oneline
git diff
git merge
git restore
```

### Usa OCASIONALMENTE:

```bash
git clone
git remote add
git stash
git reset
git rebase
git tag
```

## 🆘 Quando Algo Dá Errado

**1. Não entre em pânico! 🧘**

**2. Veja o status:**
```bash
git status
```

**3. Leia a mensagem de erro** - Git é bem informativo

**4. Comandos seguros:**
```bash
git merge --abort    # Cancela merge
git rebase --abort   # Cancela rebase
git stash            # Guarda mudanças
```

**5. Última opção:**
```bash
git reflog           # Ver histórico completo
# Você pode recuperar praticamente tudo!
```

## 📚 Recursos Adicionais

- **Documentação oficial**: [git-scm.com/doc](https://git-scm.com/doc)
- **GitHub Guides**: [guides.github.com](https://guides.github.com)
- **Git Cheat Sheet**: [education.github.com/git-cheat-sheet-education.pdf](https://education.github.com/git-cheat-sheet-education.pdf)
- **Visualizador**: [git-school.github.io/visualizing-git](https://git-school.github.io/visualizing-git)

---

## 💡 Dica Final

Imprima este guia ou salve nos favoritos. Com o tempo, esses comandos ficam automáticos! 🚀

**Lembre-se:**
- Commit frequentemente
- Pull antes de push
- Mensagens claras
- Branches para cada feature
- Teste antes de commitar

**Boa sorte com Git!** 🎉
