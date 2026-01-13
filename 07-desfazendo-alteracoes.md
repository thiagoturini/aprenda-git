# 7. Desfazendo Alterações

## 🎯 Cenários Comuns

Todos nós cometemos erros! O Git oferece várias formas de desfazer coisas:

1. **Modificou um arquivo** mas quer descartar as mudanças
2. **Adicionou arquivo na stage** mas quer tirar de lá
3. **Fez um commit** mas esqueceu de adicionar algo
4. **Fez um commit** com mensagem errada
5. **Fez um commit** que quer desfazer completamente

Vamos ver como resolver cada situação! 🛠️

## 🔄 Cenário 1: Descartar Mudanças Não Commitadas

Você modificou um arquivo, mas quer **voltar à versão do último commit**.

### ✅ Via Terminal

**Descartar mudanças de um arquivo:**
```bash
git restore arquivo.txt
```

**Ou (comando antigo):**
```bash
git checkout -- arquivo.txt
```

**Descartar mudanças de todos os arquivos:**
```bash
git restore .
```

**Exemplo prático:**
```bash
# Você modificou README.md
echo "Mudança ruim" >> README.md

# Vê as mudanças
git status

# Descarta as mudanças
git restore README.md

# Arquivo volta ao estado do último commit
```

### 🖱️ Via VS Code

**Método 1: Pelo Source Control**
1. Abra o **Source Control** (`Ctrl+Shift+G`)
2. Passe o mouse sobre o arquivo modificado (na seção "Changes")
3. Clique no ícone de **seta circular** (Discard Changes)
4. Confirme a ação

**Método 2: Pelo Editor**
1. Abra o arquivo modificado
2. Clique com o botão direito no editor
3. Selecione **Discard Changes**

**⚠️ Atenção:** Isso **não pode ser desfeito**! As mudanças são perdidas permanentemente.

## 📤 Cenário 2: Remover da Área de Stage (Unstage)

Você adicionou um arquivo com `git add`, mas quer tirar da stage area.

### ✅ Via Terminal

```bash
git restore --staged arquivo.txt
```

**Ou (comando antigo):**
```bash
git reset HEAD arquivo.txt
```

**Para todos os arquivos:**
```bash
git restore --staged .
```

**Exemplo:**
```bash
# Você adicionou por engano
git add arquivo-errado.txt

# Remove da stage
git restore --staged arquivo-errado.txt

# Arquivo continua modificado, mas não vai no próximo commit
```

### 🖱️ Via VS Code

1. Abra o **Source Control** (`Ctrl+Shift+G`)
2. Veja a seção **Staged Changes**
3. Passe o mouse sobre o arquivo
4. Clique no ícone **−** (minus)

Ou:
- Clique com o botão direito no arquivo
- Selecione **Unstage Changes**

## ✏️ Cenário 3: Alterar o Último Commit

Você fez um commit mas:
- Esqueceu de adicionar um arquivo
- Quer mudar a mensagem
- Quer adicionar mais mudanças

### ✅ Via Terminal

**Para mudar apenas a mensagem:**
```bash
git commit --amend -m "Nova mensagem corrigida"
```

**Para adicionar mais arquivos ao commit:**
```bash
# Adicione os arquivos esquecidos
git add arquivo-esquecido.txt

# Amend (emenda) o último commit
git commit --amend --no-edit
```

`--no-edit` mantém a mensagem original.

**Para mudar arquivos E mensagem:**
```bash
git add arquivo-esquecido.txt
git commit --amend -m "Mensagem nova e completa"
```

**Sem -m (abre editor para editar a mensagem):**
```bash
git commit --amend
```

### 🖱️ Via VS Code

**Para adicionar mais arquivos:**
1. Faça as mudanças adicionais
2. Adicione os arquivos na stage
3. No Source Control, clique nos **três pontinhos** (⋯)
4. Selecione **Commit > Commit Staged (Amend)**
5. Edite a mensagem se quiser
6. Confirme

**⚠️ Importante:** Só use `--amend` se você **ainda não deu push** do commit! Se já enviou para o remoto, não use amend (causa problemas para outras pessoas).

## ↩️ Cenário 4: Desfazer o Último Commit (Mantendo Mudanças)

Você quer **desfazer o commit**, mas **manter as mudanças** nos arquivos.

### ✅ Via Terminal

```bash
git reset --soft HEAD~1
```

**O que acontece:**
- O commit é removido do histórico
- As mudanças voltam para a stage area
- Os arquivos continuam modificados

**Exemplo:**
```bash
# Você fez um commit errado
git commit -m "Commit errado"

# Desfaz o commit
git reset --soft HEAD~1

# Agora os arquivos estão staged novamente
git status
```

`HEAD~1` significa "um commit antes do HEAD (atual)".

### 🖱️ Via VS Code

**Usando Git Graph:**
1. Abra o Git Graph
2. Clique com o botão direito no commit anterior (antes do que quer desfazer)
3. Selecione **Reset current branch to this commit**
4. Escolha **Soft**

**Usando terminal integrado:**
- Use o comando acima no terminal do VS Code

## 🗑️ Cenário 5: Desfazer o Último Commit (Perdendo Mudanças)

Você quer **desfazer o commit** e **descartar todas as mudanças**.

### ✅ Via Terminal

```bash
git reset --hard HEAD~1
```

**⚠️ CUIDADO:** Isso **apaga permanentemente** as mudanças!

**O que acontece:**
- O commit é removido
- Todas as mudanças são descartadas
- Não há como recuperar

Use apenas se tiver certeza!

### 🖱️ Via VS Code

**Usando Git Graph:**
1. Abra o Git Graph
2. Clique com o botão direito no commit anterior
3. Selecione **Reset current branch to this commit**
4. Escolha **Hard**
5. Confirme (cuidado!)

## 🔢 Tipos de Reset

O `git reset` tem três modos:

### --soft
```bash
git reset --soft HEAD~1
```
- Remove o commit
- ✅ Mantém mudanças staged
- ✅ Mantém arquivos modificados

### --mixed (padrão)
```bash
git reset HEAD~1
```
ou
```bash
git reset --mixed HEAD~1
```
- Remove o commit
- ❌ Remove da stage area
- ✅ Mantém arquivos modificados

### --hard
```bash
git reset --hard HEAD~1
```
- Remove o commit
- ❌ Remove da stage area
- ❌ **Apaga as mudanças dos arquivos**

## 📝 Voltando Vários Commits

**Voltar 3 commits atrás:**
```bash
git reset --soft HEAD~3
```

**Voltar para um commit específico:**
```bash
git reset --soft a1b2c3d
```

(Use o hash do commit que quer voltar)

## 🔍 Verificando o que Vai Acontecer

Antes de fazer reset, veja onde está:

```bash
# Ver histórico
git log --oneline

# Resultado:
# a1b2c3d (HEAD) Commit mais recente
# z9y8x7w Commit anterior
# x8w7v6u Mais antigo
```

Se você fizer `git reset --soft HEAD~1`, voltará para `z9y8x7w`.

## 🎯 Fluxograma de Decisão

```
Você cometeu um erro?
│
├─ Arquivo modificado mas não adicionado?
│  └─ git restore arquivo.txt
│
├─ Arquivo adicionado (staged) mas não commitado?
│  └─ git restore --staged arquivo.txt
│
├─ Já commitou mas quer adicionar mais coisas?
│  └─ git add ... → git commit --amend
│
├─ Quer desfazer commit mas manter mudanças?
│  └─ git reset --soft HEAD~1
│
└─ Quer desfazer commit E descartar mudanças?
   └─ git reset --hard HEAD~1 (CUIDADO!)
```

## 💡 Dicas Importantes

### ✅ Use git status Sempre

Antes e depois de desfazer algo, use:
```bash
git status
```

Para ver o estado atual.

### ✅ Veja o Histórico

```bash
git log --oneline
```

Para saber onde você está.

### ⚠️ Cuidado com --hard

`git reset --hard` **apaga mudanças permanentemente**. Use apenas se tiver certeza!

### ✅ Teste em um Projeto de Exemplo

Antes de usar esses comandos em projetos reais, pratique em um repositório de teste.

### ⚠️ Não Amend Commits Já Enviados

Se você já deu `git push`, **não use** `git commit --amend`. Isso reescreve o histórico e causa problemas.

## 🔄 Comandos Resumidos

```bash
# Descartar mudanças em arquivo
git restore arquivo.txt

# Remover da stage area
git restore --staged arquivo.txt

# Alterar último commit (mensagem)
git commit --amend -m "Nova mensagem"

# Adicionar ao último commit
git add arquivo.txt
git commit --amend --no-edit

# Desfazer commit (manter mudanças)
git reset --soft HEAD~1

# Desfazer commit (descartar mudanças)
git reset --hard HEAD~1  # CUIDADO!

# Voltar vários commits
git reset --soft HEAD~3

# Voltar para commit específico
git reset --soft a1b2c3d
```

## 🎓 Resumo

✅ Você aprendeu:
- Como descartar mudanças não commitadas
- Como remover arquivos da stage area
- Como alterar o último commit (amend)
- Como desfazer commits com reset
- A diferença entre --soft, --mixed e --hard
- Quando usar cada comando

## 🎯 Exercício Prático

Pratique cada cenário:

1. Modifique um arquivo e descarte as mudanças
2. Adicione um arquivo e remova da stage
3. Faça um commit e use amend para mudar a mensagem
4. Faça um commit e desfaça com --soft
5. Veja o histórico para confirmar

---

## 🎯 Próximos Passos

Agora você sabe desfazer erros! Vamos aprender sobre o `.gitignore`, que evita commitar arquivos indesejados.

➡️ **Próximo:** [O Arquivo .gitignore](08-gitignore.md)
