# 9. O que são Branches

## 🎯 Conceito de Branch

**Branch** (ramificação) é uma **linha paralela de desenvolvimento** no seu projeto.

Imagine um livro com várias versões alternativas da história - cada branch é uma dessas versões!

## 📚 Analogia: Escrevendo um Livro

Você está escrevendo um livro:

```
Capítulo 1 → Capítulo 2 → Capítulo 3  [Branch principal: main]
                    ↓
            Versão alternativa
            com final diferente       [Branch: final-alternativo]
```

Com branches você pode:
- Trabalhar no livro principal (branch `main`)
- Criar uma versão alternativa (branch `final-alternativo`)
- Depois decidir qual usar
- Ou até combinar as duas versões!

## 🌳 Visualização de Branches

```
        A --- B --- C  [main]
                 \
                  D --- E  [nova-funcionalidade]
```

- **main**: Branch principal (linha do tempo original)
- **nova-funcionalidade**: Branch nova (linha alternativa)
- Os commits A, B, C estão na main
- Os commits D, E estão na branch nova-funcionalidade

## 🤔 Por Que Usar Branches?

### 1. **Experimentar Sem Quebrar**
Teste ideias novas sem afetar o código que funciona.

### 2. **Trabalhar em Paralelo**
Várias pessoas (ou você mesmo) trabalhando em funcionalidades diferentes ao mesmo tempo.

### 3. **Organização**
Cada funcionalidade/correção em sua própria branch.

### 4. **Segurança**
O código principal fica protegido enquanto você desenvolve.

### 5. **Revisão de Código**
Outras pessoas podem revisar sua branch antes de juntar ao código principal.

## 📊 Cenários Práticos

### Cenário 1: Desenvolvendo Funcionalidade Nova

```
main:         A --- B --- C --- D
                       \
nova-feature:           E --- F --- G
```

Você cria uma branch `nova-feature`:
- A branch `main` continua com o código estável
- Você trabalha em `nova-feature` com segurança
- Quando terminar, pode juntar (merge) em `main`

### Cenário 2: Correção de Bug Urgente

```
main:     A --- B --- C ------------ F
                   \                 /
hotfix:             D --- E ---------
```

Enquanto trabalha em uma funcionalidade:
- Surge um bug urgente na produção
- Você cria uma branch `hotfix` a partir da `main`
- Corrige o bug rapidamente
- Faz merge de volta para `main`
- Volta a trabalhar na funcionalidade original

### Cenário 3: Trabalho em Equipe

```
main:         A --- B ----------- G
                   / \           /
feature-1:        C   E         /
                   \   \       /
feature-2:          D   F ----
```

- Pessoa 1 trabalha em `feature-1`
- Pessoa 2 trabalha em `feature-2`
- Cada um no seu ritmo
- Depois fazem merge na `main`

## 🏷️ Branch Padrão: main (ou master)

Quando você cria um repositório, ele vem com uma branch padrão:

- **Antigamente**: `master`
- **Hoje em dia**: `main` (mais comum)

Essa é a branch principal - o "tronco" da árvore.

## 🎯 Boas Práticas de Nomenclatura

### ✅ Bons nomes de branches:

**Por tipo:**
```
feature/login
feature/cadastro-usuario
bugfix/corrige-validacao
hotfix/erro-pagamento
```

**Por descrição:**
```
adiciona-dark-mode
corrige-bug-formulario
atualiza-documentacao
```

**Por ticket/issue:**
```
ISSUE-123-login
JIRA-456-pagamento
```

### ❌ Evite:

```
branch1
teste
aaa
final
final-final
versao-2
```

## 🔍 Fluxos Comuns de Branch

### Git Flow (Complexo, para empresas grandes)

```
main: Produção
  ↓
develop: Desenvolvimento
  ↓
feature/*: Funcionalidades
hotfix/*: Correções urgentes
release/*: Preparação de lançamento
```

### GitHub Flow (Simples, mais usado hoje)

```
main: Produção (sempre estável)
  ↓
feature/*: Uma branch para cada coisa nova
```

1. Crie branch da main
2. Desenvolva
3. Abra Pull Request
4. Revisão
5. Merge na main

**Mais simples e eficiente!**

## 💡 Conceitos Importantes

### HEAD

`HEAD` é um "ponteiro" que indica **onde você está agora**.

```
A --- B --- C  [main] ← HEAD
         \
          D  [feature]
```

Aqui, o `HEAD` aponta para a branch `main`, no commit `C`.

Se você trocar para a branch `feature`:

```
A --- B --- C  [main]
         \
          D  [feature] ← HEAD
```

Agora o `HEAD` está na branch `feature`.

### Detached HEAD

Se o HEAD apontar diretamente para um commit (não para uma branch):

```
A --- B --- C  [main]
      ↑
     HEAD (detached)
```

Isso é **Detached HEAD** - você não está em nenhuma branch.

## 🎨 Visualizando Branches

### ✅ Via Terminal

**Ver branches:**
```bash
git branch
```

Resultado:
```
* main
  feature-login
  bugfix-form
```

O `*` indica em qual branch você está.

**Ver com mais informações:**
```bash
git branch -v
```

Resultado:
```
* main          a1b2c3d Último commit da main
  feature-login z9y8x7w Adiciona página de login
```

### 🖱️ Via VS Code

**Na barra inferior:**
- No canto inferior esquerdo, você vê o nome da branch atual
- Exemplo: `main` ou `feature-login`

**No Source Control:**
- O painel Source Control mostra a branch atual no topo

**Com Git Graph:**
- Abra o Git Graph
- Você vê visualmente todas as branches e seus commits

## 📖 Exemplo do Mundo Real

Imagine que você está desenvolvendo um site:

### Semana 1:
```
main: A (Site básico)
```

### Semana 2: Você adiciona um formulário
```
main:         A --- B
                   \
formulario:         C --- D
```

Você cria branch `formulario` e desenvolve.

### Semana 3: Bug urgente na main!
```
main:         A --- B ----------- F
                   \   \         /
formulario:         \   E ------
                     \
                      C --- D
```

Você cria branch para corrigir bug (commit E), faz merge na main (commit F).

### Semana 4: Termina o formulário e faz merge
```
main:         A --- B --- F ------------ G
                   \       \            /
formulario:         C --- D ------------
```

Formulário pronto! Faz merge na main.

**Resultado:** Main tem site básico + correção de bug + formulário. ✨

## 🎓 Benefícios das Branches

✅ **Isolamento**: Mudanças não afetam outras partes
✅ **Experimentação**: Teste à vontade
✅ **Colaboração**: Várias pessoas trabalhando juntas
✅ **Organização**: Histórico limpo e claro
✅ **Segurança**: Main sempre estável

## 🎯 Quando Criar uma Branch?

Crie uma branch quando for:

- ✅ Desenvolver uma nova funcionalidade
- ✅ Corrigir um bug
- ✅ Experimentar algo novo
- ✅ Fazer uma grande refatoração
- ✅ Trabalhar em algo que levará vários commits

**Regra de ouro:** Se algo demora mais de 1 commit, use uma branch!

## 🎓 Resumo

✅ Você aprendeu:
- O que são branches (ramificações)
- Por que usar branches
- Cenários práticos de uso
- Fluxos de trabalho com branches
- Nomenclatura de branches
- O conceito de HEAD
- Como visualizar branches

## 🎯 Próximos Passos

Agora que você entende o conceito de branches, vamos aprender a **criar e alternar entre branches** na prática!

➡️ **Próximo:** [Criando e Alternando Entre Branches](10-criando-branches.md)
