# 17. Pull: Recebendo Alterações

## 🎯 O que é Pull?

**Pull** (puxar) é baixar commits do repositório remoto e mesclar com sua branch local.

```
[GitHub]  ─── git pull ───>  [Seu Computador]
 Remoto                          Local
(commits novos)              (atualizado!)
```

É como "sincronizar" para ter as últimas mudanças!

## 🤔 Quando Fazer Pull?

Faça pull quando:

- ✅ Antes de começar a trabalhar (início do dia)
- ✅ Antes de criar uma nova branch
- ✅ Antes de fazer merge
- ✅ Quando alguém da equipe fez push
- ✅ Antes de fazer push (para evitar conflitos)
- ✅ Mudou de computador

**Regra de ouro:** Pull frequentemente!

## 📝 Sintaxe do Pull

### ✅ Via Terminal

**Forma completa:**
```bash
git pull <remote> <branch>
```

**Exemplo:**
```bash
git pull origin main
```

**Forma curta (se configurou tracking):**
```bash
git pull
```

Puxa da branch remota configurada.

### 🖱️ Via VS Code

**Método 1: Barra Inferior**

Na barra inferior:
- **↓2** = 2 commits para baixar
- Clique no ícone de sincronização

**Método 2: Source Control**

1. Abra Source Control (`Ctrl+Shift+G`)
2. Clique nos **três pontinhos** (⋯)
3. Selecione **Pull**

**Método 3: Command Palette**

1. Pressione `Ctrl+Shift+P`
2. Digite "Git: Pull"
3. Enter

## 🔍 O que o Pull Faz?

Pull é na verdade **dois comandos em um**:

```bash
git pull = git fetch + git merge
```

### 1. **Fetch**: Baixa dados
```bash
git fetch origin
```
- Baixa commits do remoto
- Atualiza `origin/main`
- **Não** mexe no seu código local

### 2. **Merge**: Mescla com local
```bash
git merge origin/main
```
- Junta os commits baixados com sua branch
- Atualiza seus arquivos

## 📊 Exemplo Prático

### ✅ Via Terminal

**Cenário:** Você trabalha em equipe. Um colega fez push.

```bash
# 1. Ver status atual
git status
# On branch main
# Your branch is up to date with 'origin/main'.

# 2. Seu colega fez push de novos commits

# 3. Baixar as mudanças
git pull

# Resultado:
# remote: Counting objects: 5, done.
# remote: Compressing objects: 100% (3/3), done.
# remote: Total 5 (delta 2), reused 0 (delta 0)
# Unpacking objects: 100% (5/5), done.
# From https://github.com/usuario/projeto
#    a1b2c3d..z9y8x7w  main       -> origin/main
# Updating a1b2c3d..z9y8x7w
# Fast-forward
#  arquivo.js | 10 ++++++++++
#  1 file changed, 10 insertions(+)

# 4. Verificar que foi atualizado
git log --oneline -3

# 5. Ver o que mudou
git show HEAD
```

### 🖱️ Via VS Code

**Cenário visual:**

1. **Verificar atualizações:**
   - Barra inferior mostra **↓3** (3 commits para baixar)

2. **Fazer pull:**
   - Clique no ícone de sincronização
   - Ou: Source Control → Menu → Pull

3. **VS Code baixa e mescla automaticamente**

4. **Ver mudanças:**
   - Arquivos modificados aparecem
   - Git Graph mostra novos commits
   - Explorer mostra arquivos atualizados

## ⚠️ Pull com Mudanças Locais Não Commitadas

E se você tiver mudanças não commitadas quando faz pull?

### Cenário A: Não Há Conflito

O Git mescla automaticamente. Suas mudanças são preservadas.

```bash
# Você modificou arquivo.js mas não commitou
git pull
# Funcionou! Suas mudanças ainda estão lá
```

### Cenário B: Há Conflito

```bash
git pull

error: Your local changes to the following files would be overwritten by merge:
        arquivo.js
Please commit your changes or stash them before you merge.
```

**Solução 1: Commitar antes**
```bash
git add .
git commit -m "Trabalho em progresso"
git pull
```

**Solução 2: Usar Stash**
```bash
# Guarda mudanças temporariamente
git stash

# Puxa atualizações
git pull

# Restaura suas mudanças
git stash pop
```

Veremos stash em detalhes depois!

## 🔄 Pull vs Fetch

### Fetch (Baixar Sem Mesclar)

```bash
git fetch origin
```

- Baixa commits do remoto
- Atualiza referências remotas
- **Não** muda seus arquivos
- Seguro - você decide quando mesclar

**Ver o que foi baixado:**
```bash
git log origin/main..main  # O que você tem a mais
git log main..origin/main  # O que o remoto tem a mais
```

**Mesclar manualmente depois:**
```bash
git merge origin/main
```

### Pull (Baixar E Mesclar)

```bash
git pull origin main
```

- Baixa commits
- Mescla automaticamente
- Atualiza arquivos
- Mais rápido, mas menos controle

**Quando usar cada um:**

**Use fetch quando:**
- Quer ver o que mudou antes de mesclar
- Quer ter mais controle
- Está trabalhando em algo delicado

**Use pull quando:**
- Confia no código remoto
- Quer sincronizar rapidamente
- Situação simples

## 🌿 Pull de Branches Específicas

### ✅ Via Terminal

**Pull de branch específica:**
```bash
git pull origin nome-branch
```

**Exemplo - você está em feature-login:**
```bash
# Puxa atualizações da main
git pull origin main

# Isso mescla main em feature-login
# Mantém sua branch atualizada!
```

### 🖱️ Via VS Code

1. Alterne para a branch desejada
2. Pull normalmente
3. Ou especifique branch via Command Palette

## 🔄 Pull com Rebase

Em vez de merge, você pode usar rebase:

### ✅ Via Terminal

```bash
git pull --rebase
```

**Diferença:**

**Pull normal (merge):**
```
A --- B --- C [main]
         \   \
          D   M [sua branch]
              (merge commit)
```

**Pull com rebase:**
```
A --- B --- C [main]
             \
              D' [sua branch]
              (commit reaplicado)
```

**Vantagens do rebase:**
- Histórico linear e limpo
- Sem commits de merge

**Desvantagens:**
- Reescreve histórico
- Pode dar mais conflitos

**Configurar rebase como padrão:**
```bash
git config --global pull.rebase true
```

### 🖱️ Via VS Code

Pull com rebase geralmente via terminal integrado:
```bash
git pull --rebase
```

## ⚠️ Resolvendo Conflitos no Pull

Se houver conflitos ao fazer pull:

### ✅ Via Terminal

```bash
git pull

# CONFLICT (content): Merge conflict in arquivo.js
# Automatic merge failed; fix conflicts and then commit the result.

# 1. Abra o arquivo
code arquivo.js

# 2. Resolva os conflitos
# (remova as marcações <<<< ==== >>>>)

# 3. Marque como resolvido
git add arquivo.js

# 4. Complete o merge
git commit
```

### 🖱️ Via VS Code

1. VS Code detecta conflito automaticamente
2. Arquivo abre com botões de resolução
3. Clique no botão apropriado (Accept Current/Incoming/Both)
4. Salve o arquivo
5. Stage e commit

(Mesmo processo que vimos no capítulo de conflitos!)

## 💡 Boas Práticas

### ✅ Faça:

**1. Pull frequentemente:**
```bash
# Todo dia antes de trabalhar
git pull

# Antes de criar nova branch
git pull
git switch -c nova-feature

# Antes de fazer push
git pull
git push
```

**2. Commit antes de pull:**
```bash
# Salve seu trabalho primeiro
git add .
git commit -m "Progresso atual"

# Depois puxa
git pull
```

**3. Verifique o que mudou:**
```bash
git pull
git log --oneline -5  # Ver últimos commits
git diff HEAD~1       # Ver mudanças
```

**4. Mantenha main atualizada:**
```bash
# Periodicamente, atualize main
git switch main
git pull

# Volte para sua branch
git switch feature-minha
```

### ❌ Evite:

- Nunca fazer pull (fica desatualizado)
- Pull sem verificar mudanças
- Pull com mudanças críticas não commitadas
- Ignorar conflitos

## 📊 Verificando Status

### ✅ Via Terminal

**Ver se precisa pull:**
```bash
git fetch
git status
```

Resultado possíveis:
```
# Está atualizado
Your branch is up to date with 'origin/main'.

# Tem commits no remoto
Your branch is behind 'origin/main' by 3 commits.

# Tem commits em ambos (você E remoto)
Your branch and 'origin/main' have diverged.
```

**Ver diferenças com remoto:**
```bash
# O que o remoto tem que você não tem
git log main..origin/main --oneline

# O que você tem que o remoto não tem
git log origin/main..main --oneline
```

### 🖱️ Via VS Code

- **Barra inferior**: **↓3** = 3 commits para baixar
- **Fetch**: VS Code faz fetch automático periodicamente
- **Source Control**: Mostra status da branch

## 🔄 Comandos Resumidos

```bash
# Pull básico
git pull

# Pull completo
git pull origin main

# Fetch (baixar sem mesclar)
git fetch origin

# Ver o que fetch trouxe
git log main..origin/main

# Pull com rebase
git pull --rebase

# Ver status
git status

# Ver diferenças
git diff origin/main
```

## 🎯 Workflows Comuns

### Workflow 1: Início do Dia

```bash
# Atualiza main
git switch main
git pull

# Cria/volta para feature
git switch feature-minha
# ou
git switch -c feature-nova
```

### Workflow 2: Manter Feature Atualizada

```bash
# Você está em feature-login
git switch feature-login

# Atualiza com mudanças da main
git pull origin main

# Resolve conflitos se houver
# Continua trabalhando atualizado!
```

### Workflow 3: Antes de Push

```bash
# Terminou trabalho
git add .
git commit -m "Feature completa"

# Puxa últimas mudanças
git pull

# Resolve conflitos se houver

# Envia
git push
```

## 🎓 Resumo

✅ Você aprendeu:
- O que é pull e quando usar
- Como fazer pull via terminal e VS Code
- Diferença entre pull e fetch
- Pull = fetch + merge
- Como lidar com mudanças não commitadas
- Pull com rebase
- Resolver conflitos no pull
- Boas práticas de pull
- Verificar status antes/depois do pull

## 🎯 Exercício Prático

**Exercício 1: Pull básico**
1. Clone um repositório
2. Modifique algo no GitHub (pelo site)
3. Faça pull no seu computador
4. Veja que a mudança apareceu

**Exercício 2: Trabalho simulado em equipe**
1. Clone seu repositório em duas pastas diferentes
2. Na pasta A: faça commit e push
3. Na pasta B: faça pull
4. Verifique que recebeu as mudanças

**Exercício 3: Fetch primeiro**
1. Use `git fetch`
2. Use `git log origin/main..main`
3. Veja o que mudou
4. Decida fazer merge: `git merge origin/main`

---

## 🎯 Próximos Passos

Agora você domina push e pull! Vamos aprender sobre **Fork e Pull Request** - essenciais para contribuir com projetos open source.

➡️ **Próximo:** [Fork e Pull Request](18-fork-pull-request.md)
