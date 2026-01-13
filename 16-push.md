# 16. Push: Enviando Alterações

## 🎯 O que é Push?

**Push** (empurrar) é enviar seus commits locais para o repositório remoto.

```
[Seu Computador]  ─── git push ───>  [GitHub]
     Local                              Remoto
   (commits)                          (commits)
```

É como "publicar" suas mudanças!

## 🤔 Quando Fazer Push?

Faça push quando:

- ✅ Terminou uma funcionalidade
- ✅ Quer fazer backup do seu trabalho
- ✅ Precisa compartilhar código com equipe
- ✅ Vai mudar de computador
- ✅ Fim do dia de trabalho

**Não precisa** fazer push a cada commit! Pode acumular vários commits locais e fazer push de todos de uma vez.

## 📝 Sintaxe do Push

### ✅ Via Terminal

**Forma completa:**
```bash
git push <remote> <branch>
```

**Exemplo:**
```bash
git push origin main
```

Envia a branch `main` para o remote `origin`.

**Forma curta (se configurou tracking):**
```bash
git push
```

Envia para o remote e branch configurados.

### 🖱️ Via VS Code

**Método 1: Barra Inferior (Mais Rápido)**

Na barra inferior, há um ícone de sincronização:
- **↑1** = 1 commit para push
- Clique no ícone para fazer push automaticamente

**Método 2: Source Control**

1. Abra Source Control (`Ctrl+Shift+G`)
2. Clique nos **três pontinhos** (⋯)
3. Selecione **Push**

**Método 3: Commit e Push Junto**

Ao fazer commit, você pode push ao mesmo tempo:
- Ao invés de clicar apenas "Commit"
- Clique na seta ao lado de "Commit"
- Selecione **Commit & Push**

## 🎯 Primeiro Push: Configurando Tracking

Na primeira vez que você faz push de uma branch:

### ✅ Via Terminal

```bash
git push -u origin main
```

O `-u` (ou `--set-upstream`) configura **tracking**:
- A branch local `main` agora "rastreia" `origin/main`
- Nos próximos push/pull, pode usar apenas `git push`

**Depois do primeiro push:**
```bash
git push   # Simples assim!
```

### 🖱️ Via VS Code

O VS Code configura tracking automaticamente na primeira vez!

Você só precisa:
1. Fazer commit
2. Clicar para push
3. VS Code pergunta para qual remoto/branch
4. Você escolhe
5. Pronto! Tracking configurado ✨

## 📊 Exemplo Prático Completo

### ✅ Via Terminal

```bash
# 1. Você está trabalhando em um projeto
cd meu-projeto

# 2. Faz algumas mudanças
echo "Nova funcionalidade" >> app.js

# 3. Vê o que mudou
git status

# 4. Adiciona na stage
git add app.js

# 5. Comita
git commit -m "Adiciona nova funcionalidade"

# 6. Vê que tem commit para enviar
git status
# On branch main
# Your branch is ahead of 'origin/main' by 1 commit.

# 7. Envia para o GitHub
git push

# 8. Sucesso! 🎉
# Verifica no GitHub que o commit apareceu
```

### 🖱️ Via VS Code

**Fluxo completo:**

1. **Modifique arquivos** no seu projeto

2. **Veja as mudanças:**
   - Source Control mostra arquivos modificados

3. **Stage as mudanças:**
   - Clique no **+** para stage

4. **Commit:**
   - Digite mensagem
   - Pressione `Ctrl+Enter`

5. **Push:**
   - Na barra inferior, veja **↑1** (indica 1 commit para push)
   - Clique no ícone de sincronização
   - Ou: Source Control → Menu → Push

6. **Confirme no GitHub:**
   - Atualize a página do repositório
   - Veja seu commit lá! 🎉

## 🔄 Push de Múltiplos Commits

Você pode fazer vários commits locais antes de fazer push:

### ✅ Via Terminal

```bash
# Commit 1
git add arquivo1.js
git commit -m "Adiciona arquivo1"

# Commit 2
git add arquivo2.js
git commit -m "Adiciona arquivo2"

# Commit 3
git add arquivo3.js
git commit -m "Adiciona arquivo3"

# Vê quantos commits tem para enviar
git log origin/main..HEAD --oneline
# Mostra os 3 commits

# Envia todos de uma vez
git push
# Sending 3 commits...
```

Todos os três commits são enviados juntos!

## 🌿 Push de Outras Branches

### ✅ Via Terminal

**Push de branch específica:**
```bash
git push origin nome-branch
```

**Exemplo:**
```bash
# Você está em feature-login
git push origin feature-login
```

**Primeira vez (com tracking):**
```bash
git push -u origin feature-login
```

**Depois disso:**
```bash
git push
```

### 🖱️ Via VS Code

1. Alterne para a branch que quer fazer push
2. Faça push normalmente
3. VS Code envia a branch atual automaticamente

## 🗑️ Deletando Branch Remota

Deletar uma branch no remoto:

### ✅ Via Terminal

```bash
git push origin --delete nome-branch
```

**Exemplo:**
```bash
# Deleta branch remota
git push origin --delete feature-antiga
```

**Ou:**
```bash
git push origin :nome-branch
```

### 🖱️ Via VS Code

Geralmente feito pelo GitHub:
1. Vá no repositório no GitHub
2. Vá em "Branches"
3. Clique no ícone de lixeira ao lado da branch

## ⚠️ Quando Push Falha

### Erro: "Updates were rejected"

```
! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/usuario/projeto.git'
hint: Updates were rejected because the remote contains work that you do not have locally.
```

**Problema:** O remoto tem commits que você não tem.

**Causa comum:**
- Outra pessoa fez push
- Você fez push de outro computador
- Você alterou histórico localmente

**Solução 1: Pull primeiro**

```bash
# Baixe as mudanças
git pull

# Depois faça push
git push
```

**Solução 2: Pull com rebase**

```bash
# Baixe e reaplique seus commits
git pull --rebase

# Depois faça push
git push
```

### 🖱️ Via VS Code

Se push falhar:
1. VS Code mostra erro
2. Clique em "Pull" quando sugerido
3. Resolva conflitos se houver
4. Faça push novamente

## 🚨 Force Push (Cuidado!)

### ✅ Via Terminal

```bash
git push --force
```

ou

```bash
git push -f
```

**⚠️ MUITO PERIGOSO!** Isso:
- Sobrescreve o histórico remoto
- Pode apagar trabalho de outras pessoas
- Causa problemas para toda equipe

**Quando usar (raramente):**
- Você é a única pessoa trabalhando na branch
- Fez rebase e precisa atualizar
- Corrigiu commit incorreto

**Alternativa mais segura:**
```bash
git push --force-with-lease
```

Só faz força se ninguém mais fez push nesse meio tempo.

### 🖱️ Via VS Code

Force push geralmente precisa ser feito pelo terminal integrado.

Por segurança, VS Code não tem botão de force push na interface principal.

## 📊 Verificando Status Antes do Push

### ✅ Via Terminal

**Ver quantos commits para push:**
```bash
git status
```

Resultado:
```
Your branch is ahead of 'origin/main' by 3 commits.
```

**Ver quais commits:**
```bash
git log origin/main..HEAD --oneline
```

**Ver diferenças:**
```bash
git diff origin/main
```

### 🖱️ Via VS Code

- **Barra inferior**: Mostra **↑3** (3 commits para push)
- **Source Control**: Lista os commits
- **Git Graph**: Visualização gráfica

## 🎯 Boas Práticas de Push

### ✅ Faça:

**1. Pull antes de Push:**
```bash
git pull
git push
```

Garante que você tem as últimas mudanças.

**2. Verifique o que está enviando:**
```bash
git log origin/main..HEAD
```

**3. Push frequente:**
- Pelo menos uma vez por dia
- Sempre no fim do dia
- Depois de terminar funcionalidades

**4. Mensagens de commit claras:**
Boas mensagens ajudam a equipe a entender o que mudou.

**5. Teste antes de push:**
Certifique-se de que o código funciona!

### ❌ Evite:

- Push de código quebrado
- Push de credenciais/senhas
- Force push em branches compartilhadas
- Push sem pull (em equipe)
- Push de arquivos grandes desnecessários

## 🔄 Push vs Publish

### No VS Code:

Você pode ver dois botões diferentes:

**Push:** Branch já existe no remoto
- Envia novos commits

**Publish Branch:** Branch ainda não existe no remoto
- Cria a branch no remoto
- Envia todos os commits

É automático - o VS Code escolhe o correto!

## 💡 Workflows Comuns

### Workflow 1: Trabalho Solo

```bash
# Trabalhe
git add .
git commit -m "Mudanças"

# Fim do dia
git push
```

### Workflow 2: Trabalho em Equipe

```bash
# Início do dia
git pull

# Trabalhe
git add .
git commit -m "Feature X"

# Antes de push
git pull
git push
```

### Workflow 3: Feature Branch

```bash
# Cria branch
git switch -c feature-nova

# Trabalha
git commit -m "Progresso"

# Push da branch
git push -u origin feature-nova

# No GitHub: cria Pull Request
# Equipe revisa
# Merge na main
```

## 🔄 Comandos Resumidos

```bash
# Push básico
git push

# Push completo (primeira vez)
git push -u origin main

# Push de branch específica
git push origin nome-branch

# Ver status
git status
git log origin/main..HEAD

# Deletar branch remota
git push origin --delete nome-branch

# Force push (cuidado!)
git push --force-with-lease
```

## 🎓 Resumo

✅ Você aprendeu:
- O que é push e quando usar
- Como fazer push via terminal e VS Code
- Configurar tracking com -u
- Push de múltiplos commits
- Push de diferentes branches
- Como resolver erros de push
- Boas práticas de push
- Diferença entre push e publish

## 🎯 Exercício Prático

**Exercício 1: Push básico**
1. Modifique um arquivo no seu projeto
2. Comite a mudança
3. Faça push
4. Verifique no GitHub

**Exercício 2: Múltiplos commits**
1. Faça 3 commits diferentes
2. Use `git status` para ver quantos commits tem
3. Faça push de todos de uma vez
4. Verifique no GitHub que os 3 commits estão lá

**Exercício 3: Nova branch**
1. Crie uma branch `feature-teste`
2. Faça um commit
3. Push da branch
4. Veja a branch aparecer no GitHub

---

## 🎯 Próximos Passos

Você sabe fazer push! Agora vamos aprender o contrário: **pull** - baixar mudanças do remoto.

➡️ **Próximo:** [Pull: Recebendo Alterações](17-pull.md)
