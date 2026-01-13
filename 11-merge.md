# 11. Mesclando Branches (Merge)

## 🎯 O que é Merge?

**Merge** (mesclar) é o ato de **juntar** duas branches. É quando você pega as mudanças de uma branch e incorpora em outra.

```
Antes do merge:
        A --- B --- C  [main]
               \
                D --- E  [feature]

Depois do merge:
        A --- B --- C --- F  [main]
               \         /
                D --- E   [feature]
```

O commit `F` é um **merge commit** que junta as duas linhas.

## 🤔 Quando Fazer Merge?

Você faz merge quando:

- ✅ Terminou de desenvolver uma funcionalidade
- ✅ A funcionalidade foi testada e está funcionando
- ✅ Quer incorporar as mudanças na branch principal
- ✅ Precisa trazer atualizações da main para sua branch

## 📝 Como Fazer Merge

### ✅ Via Terminal

**Passos:**

1. **Vá para a branch que vai RECEBER as mudanças**
2. **Execute o merge da outra branch**

**Exemplo:**
```bash
# 1. Vai para a branch de destino (main)
git switch main

# 2. Faz merge da branch feature-login
git merge feature-login
```

**O que acontece:**
- O Git junta as mudanças de `feature-login` em `main`
- Um novo commit de merge é criado (geralmente)
- `main` agora tem todas as mudanças

### 🖱️ Via VS Code

**Método 1: Via Source Control**

1. Alterne para a branch de destino (ex: `main`)
   - Clique em `feature-login` na barra inferior
   - Selecione `main`

2. Abra o Source Control (`Ctrl+Shift+G`)

3. Clique nos **três pontinhos** (⋯)

4. Selecione **Branch > Merge Branch**

5. Escolha a branch que quer mesclar (ex: `feature-login`)

**Método 2: Via Git Graph**

1. Abra o Git Graph

2. Clique com o botão direito na branch que quer mesclar

3. Selecione **Merge into current branch**

**Método 3: Terminal integrado**
- Use o terminal do VS Code com os comandos acima

## 🎨 Tipos de Merge

### 1. Fast-Forward Merge (Mais Simples)

Quando não há commits novos na branch de destino:

```
Antes:
        A --- B  [main]
               \
                C --- D  [feature]

Depois (fast-forward):
        A --- B --- C --- D  [main]
                         [feature]
```

O Git simplesmente **move** o ponteiro da `main` para frente. Não cria commit de merge.

**Como acontece:**
```bash
git switch main
git merge feature
# Fast-forward!
```

### 2. Three-Way Merge (Merge Verdadeiro)

Quando há commits em ambas as branches:

```
Antes:
        A --- B --- C  [main]
               \
                D --- E  [feature]

Depois (three-way merge):
        A --- B --- C --- F  [main]
               \         /
                D --- E   [feature]
```

O Git cria um **commit de merge** (F) que tem dois "pais": C e E.

**Como acontece:**
```bash
git switch main
git merge feature
# Three-way merge!
# Editor abre para você escrever mensagem do merge
```

## 📝 Exemplo Prático Completo

Vamos simular um cenário real:

### ✅ Via Terminal

```bash
# 1. Você está na main
git switch main
git log --oneline
# a1b2c3d Commit inicial

# 2. Cria branch para nova funcionalidade
git switch -c feature-contato

# 3. Trabalha na funcionalidade
echo "Página de contato" > contato.html
git add contato.html
git commit -m "Adiciona página de contato"

echo "Email: contato@exemplo.com" >> contato.html
git add contato.html
git commit -m "Adiciona email de contato"

# 4. Vê o histórico
git log --oneline
# z9y8x7w Adiciona email de contato
# y8x7w6v Adiciona página de contato
# a1b2c3d Commit inicial

# 5. Volta para main
git switch main

# 6. Vê que contato.html não existe aqui
ls
# (contato.html não está listado)

# 7. Faz merge da feature-contato
git merge feature-contato

# 8. Agora contato.html existe!
ls
# contato.html  (agora aparece!)

# 9. Vê o histórico com gráfico
git log --oneline --graph
# * z9y8x7w (HEAD -> main, feature-contato) Adiciona email
# * y8x7w6v Adiciona página de contato
# * a1b2c3d Commit inicial
```

### 🖱️ Via VS Code

**1. Criar e trabalhar na branch:**
- Clique em `main` na barra inferior
- Crie nova branch: `feature-contato`
- Crie arquivo `contato.html`
- Faça commit: "Adiciona página de contato"
- Modifique o arquivo
- Faça commit: "Adiciona email de contato"

**2. Fazer merge:**
- Clique em `feature-contato` na barra inferior
- Selecione `main` (volta para main)
- Abra Source Control (`Ctrl+Shift+G`)
- Clique nos **três pontinhos** (⋯)
- **Branch > Merge Branch**
- Selecione `feature-contato`
- Pronto! As mudanças estão em `main`

## 📊 Verificando o Merge

### ✅ Via Terminal

**Ver o histórico com gráfico:**
```bash
git log --oneline --graph --all
```

**Ver branches mescladas:**
```bash
git branch --merged
```

Mostra quais branches já foram mescladas na branch atual.

**Ver branches NÃO mescladas:**
```bash
git branch --no-merged
```

### 🖱️ Via VS Code

**Com Git Graph:**
- Você vê visualmente as linhas de merge
- Os commits aparecem conectados

## 🗑️ Limpeza Após Merge

Depois do merge bem-sucedido, você pode deletar a branch:

### ✅ Via Terminal

```bash
# Deleta a branch (seguro - só funciona se já foi merged)
git branch -d feature-contato
```

Resultado:
```
Deleted branch feature-contato (was z9y8x7w).
```

**Por quê deletar?**
- As mudanças já estão na main
- Mantém o repositório organizado
- Evita confusão com branches antigas

### 🖱️ Via VS Code

- Clique com botão direito na branch
- Selecione **Delete Branch**

## 🔄 Merge vs Rebase

**Merge** cria um commit de merge:
```
A --- B --- C --- M  [main]
         \       /
          D --- E    [feature]
```

**Rebase** reescreve o histórico (mais avançado):
```
A --- B --- C --- D' --- E'  [main, feature]
```

**Quando usar:**
- **Merge**: Padrão, mais seguro, preserva histórico
- **Rebase**: História linear limpa, mas reescreve histórico

Por enquanto, use **merge**! É mais seguro para iniciantes.

## ⚠️ Conflitos (Preview)

Às vezes, o merge não funciona automaticamente:

```
Auto-merging arquivo.txt
CONFLICT (content): Merge conflict in arquivo.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Isso é um **conflito de merge**. Veremos como resolver no próximo capítulo!

## 💡 Estratégias de Merge

### Estratégia 1: Feature Branch (Recomendado)

```bash
# Cria branch para cada funcionalidade
git switch -c feature-X
# ... desenvolve ...
git switch main
git merge feature-X
git branch -d feature-X
```

### Estratégia 2: Keep Main Updated

```bash
# Na sua feature branch
git switch feature-login

# Traz mudanças da main para sua branch
git merge main

# Continua desenvolvendo com código atualizado
```

### Estratégia 3: Multiple Features

```bash
# Várias features independentes
git switch -c feature-A
# ... trabalha ...

git switch main
git switch -c feature-B
# ... trabalha ...

# Depois merge cada uma
git switch main
git merge feature-A
git merge feature-B
```

## 🎯 Boas Práticas

### ✅ Faça:

- Teste antes do merge
- Faça merge de branches pequenas e frequentes
- Delete branches após merge
- Use mensagens descritivas no merge
- Faça merge da main para sua branch periodicamente

### ❌ Evite:

- Fazer merge de código não testado
- Deixar branches muito tempo sem merge
- Fazer merge direto na main sem revisão (em equipe)
- Acumular muitas mudanças antes do merge

## 🔄 Comandos Resumidos

```bash
# Fazer merge
git switch branch-destino
git merge branch-origem

# Ver branches mescladas
git branch --merged

# Ver branches não mescladas
git branch --no-merged

# Deletar branch após merge
git branch -d nome-branch

# Ver histórico com merge
git log --oneline --graph --all

# Abortar merge (se algo der errado)
git merge --abort
```

## 📋 Checklist de Merge

Antes de fazer merge na main:

- [ ] O código está funcionando?
- [ ] Os testes passam?
- [ ] Fez commit de todas as mudanças?
- [ ] Está na branch correta?
- [ ] Revisou as mudanças?

## 🎓 Resumo

✅ Você aprendeu:
- O que é merge e quando usar
- Como fazer merge via terminal e VS Code
- Fast-forward vs three-way merge
- Como verificar o histórico após merge
- Como limpar branches após merge
- Boas práticas de merge

## 🎯 Exercício Prático

Pratique o fluxo completo:

1. Crie uma branch `feature-sobre`
2. Adicione arquivo `sobre.html` com algum conteúdo
3. Faça 2 commits
4. Volte para `main`
5. Faça merge de `feature-sobre`
6. Use `git log --oneline --graph` para ver o resultado
7. Delete a branch `feature-sobre`
8. Verifique com `git branch` que ela foi deletada

---

## 🎯 Próximos Passos

Agora você sabe fazer merge! Mas e quando o merge dá conflito? Vamos aprender a resolver!

➡️ **Próximo:** [Resolvendo Conflitos](12-conflitos.md)
