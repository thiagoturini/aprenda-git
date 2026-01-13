# 12. Resolvendo Conflitos

## 🎯 O que é um Conflito?

Um **conflito** acontece quando o Git não consegue fazer merge automaticamente porque duas branches modificaram a **mesma parte** do mesmo arquivo de formas diferentes.

```
Branch main:        Linha 5: "Olá Mundo"
Branch feature:     Linha 5: "Hello World"

Git: "🤔 Qual versão usar? Você decide!"
```

**Não entre em pânico!** Conflitos são normais e fáceis de resolver. 💪

## 🤔 Quando Acontecem Conflitos?

### Cenário de Conflito:

```
main:     A --- B --- C
               \
feature:        D --- E
```

**No commit B:**
```python
# arquivo.py
nome = "João"
```

**No commit C (main):**
```python
# arquivo.py
nome = "Maria"
```

**No commit E (feature):**
```python
# arquivo.py
nome = "Pedro"
```

Quando você tenta fazer merge de `feature` em `main`:
```bash
git switch main
git merge feature
# CONFLITO! 💥
```

Git não sabe qual nome usar: Maria ou Pedro?

## 📝 Como Identificar um Conflito

### ✅ Via Terminal

Quando você tenta fazer merge:

```bash
git merge feature-login

Auto-merging login.py
CONFLICT (content): Merge conflict in login.py
Automatic merge failed; fix conflicts and then commit the result.
```

**Mensagens importantes:**
- `CONFLICT (content)`: Há conflito de conteúdo
- `Merge conflict in login.py`: O arquivo com conflito
- `Automatic merge failed`: Precisa resolver manualmente

**Verificar status:**
```bash
git status
```

Resultado:
```
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   login.py
```

### 🖱️ Via VS Code

Quando há conflito:

1. **Notificação**: VS Code mostra notificação de conflito
2. **Source Control**: Arquivos aparecem com **C** (conflict)
3. **Barra lateral**: Cor diferente nos arquivos conflitantes
4. **Editor**: Arquivo abre com marcações especiais

## 🔍 Anatomia de um Conflito

Quando você abre o arquivo conflitante, vê algo assim:

```python
def login(usuario):
<<<<<<< HEAD
    return f"Bem-vindo, {usuario}!"
=======
    return f"Hello, {usuario}!"
>>>>>>> feature-login
```

**Entendendo as marcações:**

```
<<<<<<< HEAD
    Versão da branch atual (main)
=======
    Versão da branch que você está mesclando (feature)
>>>>>>> nome-da-branch
```

- `<<<<<<< HEAD`: Início do conflito (versão atual)
- `=======`: Separador entre as versões
- `>>>>>>> branch`: Fim do conflito (versão da outra branch)

## 🛠️ Resolvendo Conflitos

Você tem três opções:

1. **Manter versão atual** (HEAD)
2. **Manter versão da outra branch**
3. **Manter ambas** ou criar uma versão mesclada

### ✅ Via Terminal (Manualmente)

**1. Abra o arquivo conflitante:**
```bash
nano login.py
```
(ou use seu editor preferido: vim, code, etc.)

**2. Veja o conflito:**
```python
<<<<<<< HEAD
    return f"Bem-vindo, {usuario}!"
=======
    return f"Hello, {usuario}!"
>>>>>>> feature-login
```

**3. Escolha o que manter:**

**Opção A - Manter versão atual:**
```python
    return f"Bem-vindo, {usuario}!"
```

**Opção B - Manter versão da feature:**
```python
    return f"Hello, {usuario}!"
```

**Opção C - Mesclar ambas:**
```python
    # Suporta dois idiomas
    if idioma == "pt":
        return f"Bem-vindo, {usuario}!"
    else:
        return f"Hello, {usuario}!"
```

**4. Delete as marcações do Git:**
Remove completamente:
- `<<<<<<< HEAD`
- `=======`
- `>>>>>>> feature-login`

**5. Salve o arquivo**

**6. Marque como resolvido:**
```bash
git add login.py
```

**7. Complete o merge:**
```bash
git commit
```

(O Git já prepara uma mensagem padrão de merge)

Ou com mensagem personalizada:
```bash
git commit -m "Merge feature-login: resolve conflito de mensagem"
```

### 🖱️ Via VS Code (Muito mais fácil!)

Quando você abre um arquivo com conflito no VS Code:

#### **Interface Visual de Conflito**

O VS Code mostra botões acima do conflito:

```python
Accept Current Change | Accept Incoming Change | Accept Both Changes | Compare Changes

def login(usuario):
<<<<<<< HEAD (Current Change)
    return f"Bem-vindo, {usuario}!"
=======
    return f"Hello, {usuario}!"  (Incoming Change)
>>>>>>> feature-login
```

**Opções:**

1. **Accept Current Change**: Mantém apenas a versão atual (HEAD)
2. **Accept Incoming Change**: Mantém apenas a versão da outra branch
3. **Accept Both Changes**: Mantém as duas versões
4. **Compare Changes**: Abre diff visual lado a lado

**Basta clicar no botão desejado!** ✨

#### **Passos completos:**

1. VS Code detecta conflito automaticamente
2. Arquivo abre com os botões de resolução
3. Clique no botão apropriado
4. O VS Code remove as marcações automaticamente
5. Salve o arquivo (`Ctrl+S`)
6. No Source Control, stage o arquivo (botão `+`)
7. Commit as mudanças (`Ctrl+Enter`)

**Pronto! Conflito resolvido!** 🎉

## 📊 Exemplo Prático Completo

Vamos criar um conflito de propósito e resolver:

### ✅ Via Terminal

```bash
# 1. Crie repositório de teste
mkdir teste-conflito
cd teste-conflito
git init

# 2. Crie arquivo inicial
echo "Linha 1" > arquivo.txt
git add arquivo.txt
git commit -m "Commit inicial"

# 3. Modifique na main
echo "Linha 2 - versão main" >> arquivo.txt
git add arquivo.txt
git commit -m "Adiciona linha 2 na main"

# 4. Volta e cria branch
git switch -c feature
git reset --hard HEAD~1  # Volta um commit

# 5. Modifica diferente na feature
echo "Linha 2 - versão feature" >> arquivo.txt
git add arquivo.txt
git commit -m "Adiciona linha 2 na feature"

# 6. Tenta fazer merge
git switch main
git merge feature

# CONFLITO! 💥
# Auto-merging arquivo.txt
# CONFLICT (content): Merge conflict in arquivo.txt

# 7. Vê o conflito
cat arquivo.txt
# Linha 1
# <<<<<<< HEAD
# Linha 2 - versão main
# =======
# Linha 2 - versão feature
# >>>>>>> feature

# 8. Edita e resolve (escolhe manter ambas)
echo "Linha 1" > arquivo.txt
echo "Linha 2 - versão main" >> arquivo.txt
echo "Linha 2 - versão feature" >> arquivo.txt

# 9. Marca como resolvido
git add arquivo.txt

# 10. Completa o merge
git commit -m "Merge feature: mantém ambas as linhas"

# 11. Sucesso! 🎉
git log --oneline --graph
```

### 🖱️ Via VS Code

**1. Crie o cenário de conflito:**
(Use os comandos acima no terminal integrado)

**2. Quando o conflito acontecer:**
- VS Code mostra notificação
- Arquivo `arquivo.txt` aparece com **C** no Source Control

**3. Abra o arquivo:**
- VS Code mostra os botões de resolução
- Clique em **Compare Changes** para ver lado a lado

**4. Resolva:**
- Clique em **Accept Both Changes** (ou outra opção)
- Ou edite manualmente para uma solução personalizada

**5. Finalize:**
- Salve o arquivo
- Stage no Source Control (`+`)
- Commit com mensagem descritiva

## 🔧 Ferramentas de Merge

### VS Code Merge Editor

VS Code tem um editor de merge visual integrado!

**Ativar:**
1. `Ctrl+Shift+P`
2. Digite "Git: Open Merge Editor"

Você vê:
- **Incoming**: Mudanças da branch que está mesclando
- **Current**: Mudanças da branch atual
- **Result**: O resultado final que você está criando

### Extensões Úteis

**GitLens:**
- Mostra quem modificou cada linha
- Ajuda a entender o contexto do conflito

**Git History:**
- Visualiza histórico detalhado
- Vê exatamente o que mudou em cada branch

## ⚠️ Abortando um Merge

Se você quer cancelar o merge e voltar ao estado anterior:

### ✅ Via Terminal

```bash
git merge --abort
```

Tudo volta ao estado anterior ao merge!

### 🖱️ Via VS Code

1. Source Control > Três pontinhos (⋯)
2. **Merge > Abort Merge**

Ou use o terminal integrado.

## 💡 Prevenindo Conflitos

### ✅ Boas Práticas:

**1. Commits pequenos e frequentes:**
```bash
# Ao invés de um commit gigante
git commit -m "Funcionalidade completa com 50 mudanças"

# Faça vários commits menores
git commit -m "Adiciona estrutura HTML"
git commit -m "Adiciona estilos CSS"
git commit -m "Adiciona lógica JavaScript"
```

**2. Atualize sua branch frequentemente:**
```bash
# Regularmente, traga mudanças da main
git switch feature-minha
git merge main
```

**3. Comunique-se com a equipe:**
- "Estou trabalhando no arquivo X"
- Evite que duas pessoas modifiquem o mesmo arquivo simultaneamente

**4. Use branches pequenas:**
- Uma funcionalidade = uma branch
- Faça merge rápido

**5. Pull antes de começar:**
```bash
# Sempre atualize antes de trabalhar
git switch main
git pull
git switch -c nova-feature
```

## 🎯 Tipos de Conflito

### 1. Conflito de Conteúdo (Mais Comum)

Duas branches modificaram as mesmas linhas.

**Solução:** Escolher qual versão manter ou mesclar.

### 2. Conflito de Delete/Modify

Uma branch deletou o arquivo, outra modificou.

```
CONFLICT (modify/delete): arquivo.txt deleted in feature
and modified in HEAD.
```

**Solução:** Decidir se mantém ou deleta o arquivo.

### 3. Conflito de Rename

Duas branches renomearam o mesmo arquivo para nomes diferentes.

**Solução:** Escolher qual nome usar.

## 🔍 Verificando Conflitos

### ✅ Via Terminal

**Ver arquivos com conflito:**
```bash
git diff --name-only --diff-filter=U
```

**Ver detalhes dos conflitos:**
```bash
git diff
```

### 🖱️ Via VS Code

- Source Control mostra seção **Merge Changes**
- Arquivos conflitantes têm ícone **C**

## 🔄 Comandos Resumidos

```bash
# Durante conflito
git status                  # Ver arquivos conflitantes
git diff                    # Ver detalhes do conflito

# Resolver
# (edite os arquivos manualmente)
git add arquivo.txt         # Marca como resolvido
git commit                  # Completa o merge

# Abortar merge
git merge --abort           # Cancela tudo

# Verificar conflitos
git diff --name-only --diff-filter=U
```

## 🎓 Resumo

✅ Você aprendeu:
- O que são conflitos e por que acontecem
- Como identificar conflitos
- Anatomia de um conflito (marcações)
- Como resolver via terminal
- Como resolver via VS Code (muito mais fácil!)
- Como abortar um merge
- Como prevenir conflitos
- Tipos de conflitos

## 🎯 Exercício Prático

Crie um conflito e resolva:

1. Crie um repositório
2. Crie arquivo `teste.txt` com "Linha 1"
3. Commit
4. Modifique para "Linha 1\nLinha 2 - main"
5. Commit
6. Volte um commit e crie branch
7. Modifique para "Linha 1\nLinha 2 - feature"
8. Commit
9. Tente fazer merge
10. Resolva o conflito
11. Complete o merge

---

## 🎯 Próximos Passos

Agora você sabe trabalhar com branches e resolver conflitos! Vamos aprender sobre **repositórios remotos** e trabalhar com GitHub.

➡️ **Próximo:** [O que é um Repositório Remoto](13-repositorios-remotos.md)
