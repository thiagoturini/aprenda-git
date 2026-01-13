# 6. Visualizando o Histórico

## 🎯 Por Que Ver o Histórico?

O histórico de commits é como um **diário do seu projeto**. Ele permite:

- Ver todas as mudanças que foram feitas
- Descobrir **quem** fez cada alteração
- Entender **por que** algo foi mudado
- Encontrar **quando** um bug foi introduzido
- Voltar para versões anteriores

## 📜 O Comando git log

O comando principal para ver o histórico é o `git log`.

### ✅ Via Terminal

**Formato padrão:**
```bash
git log
```

Você verá algo como:
```
commit a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0
Author: Seu Nome <seu.email@exemplo.com>
Date:   Mon Jan 13 10:30:00 2026 -0300

    Adiciona página principal e estilos

commit z9y8x7w6v5u4t3s2r1q0p9o8n7m6l5k4j3i2h1g0
Author: Seu Nome <seu.email@exemplo.com>
Date:   Mon Jan 13 10:00:00 2026 -0300

    Adiciona README com descrição do projeto
```

Cada commit mostra:
- **Hash (ID único)**: `a1b2c3d4...` (identifica o commit)
- **Autor**: Quem fez o commit
- **Data**: Quando foi feito
- **Mensagem**: Descrição do que foi feito

### 🖱️ Via VS Code

**Método 1: Extensão Git Graph (Recomendado)**

1. Instale a extensão **Git Graph**:
   - Pressione `Ctrl+Shift+X`
   - Busque por "Git Graph"
   - Clique em "Install"

2. Use o Git Graph:
   - Clique no ícone **Git Graph** na barra inferior (um grafo)
   - Ou: pressione `Ctrl+Shift+P` → digite "Git Graph: View Git Graph"

Você verá uma visualização gráfica linda do histórico!

**Método 2: GitLens (Alternativa poderosa)**

1. Instale a extensão **GitLens**
2. Ela adiciona muitas informações inline no código
3. Mostra quem modificou cada linha e quando

**Método 3: Terminal integrado**

- Abra o terminal (`` Ctrl+` ``)
- Use os comandos `git log` normalmente

## 🎨 Formatos do git log

### Formato Compacto (Uma Linha)

```bash
git log --oneline
```

Resultado:
```
a1b2c3d Adiciona página principal e estilos
z9y8x7w Adiciona README com descrição do projeto
```

Muito mais fácil de ler! ✨

### Com Gráfico de Branches

```bash
git log --oneline --graph
```

Resultado:
```
* a1b2c3d Adiciona página principal e estilos
* z9y8x7w Adiciona README com descrição do projeto
```

(Fica mais interessante quando você tem branches - veremos depois!)

### Com Decorações

```bash
git log --oneline --decorate
```

Mostra em qual branch cada commit está.

### Formato Personalizado

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Resultado:
```
a1b2c3d - Seu Nome, 2 hours ago : Adiciona página principal e estilos
z9y8x7w - Seu Nome, 3 hours ago : Adiciona README com descrição do projeto
```

**Placeholders úteis:**
- `%h` = Hash abreviado
- `%an` = Nome do autor
- `%ar` = Data relativa (2 hours ago)
- `%s` = Mensagem do commit
- `%ad` = Data do autor

## 🔍 Filtrando o Histórico

### Por Quantidade

**Últimos 3 commits:**
```bash
git log -3
```

**Últimos 5 commits em uma linha:**
```bash
git log --oneline -5
```

### Por Autor

```bash
git log --author="Maria Silva"
```

### Por Data

**Commits desde uma data:**
```bash
git log --since="2026-01-01"
git log --since="2 weeks ago"
git log --since="yesterday"
```

**Commits até uma data:**
```bash
git log --until="2026-01-13"
git log --until="3 days ago"
```

**Entre datas:**
```bash
git log --since="2026-01-01" --until="2026-01-13"
```

### Por Mensagem

**Commits que contém palavra específica:**
```bash
git log --grep="README"
```

### Por Arquivo

**Ver histórico de um arquivo específico:**
```bash
git log README.md
```

**Com as mudanças:**
```bash
git log -p README.md
```

## 📊 Visualizando Mudanças

### Ver Mudanças de um Commit

```bash
git show a1b2c3d
```

Mostra:
- Informações do commit
- Quais arquivos mudaram
- O que mudou em cada arquivo (diff)

### Ver Apenas os Arquivos que Mudaram

```bash
git log --name-only
```

### Ver Estatísticas

```bash
git log --stat
```

Resultado:
```
commit a1b2c3d Adiciona página principal e estilos
 index.html | 1 +
 style.css  | 1 +
 2 files changed, 2 insertions(+)
```

## 🎨 Alias: Atalhos Personalizados

Você pode criar atalhos para comandos longos!

### ✅ Via Terminal

```bash
git config --global alias.lg "log --oneline --graph --decorate"
```

Agora você pode usar:
```bash
git lg
```

Ao invés de:
```bash
git log --oneline --graph --decorate
```

### Aliases Úteis

```bash
# Log bonito
git config --global alias.lg "log --oneline --graph --decorate --all"

# Status curto
git config --global alias.st "status -s"

# Log das últimas 10
git config --global alias.last "log -10 --oneline"

# Histórico completo com gráfico
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"
```

## 🖱️ Visualização no VS Code com Git Graph

Quando você abre o Git Graph:

**Você pode:**
- Ver o histórico visual com linhas conectando commits
- Clicar em um commit para ver detalhes
- Ver quais arquivos mudaram em cada commit
- Ver o diff de cada arquivo
- Criar branches
- Fazer merge
- E muito mais!

**Ícones no Git Graph:**
- 🔵 Commit normal
- 🟢 HEAD (onde você está agora)
- 🏷️ Tags
- 📁 Branches

## 📋 Comparando Commits

### Diferença Entre Dois Commits

```bash
git diff a1b2c3d z9y8x7w
```

### Diferença Entre um Commit e Agora

```bash
git diff a1b2c3d
```

### Ver Arquivos que Mudaram Entre Commits

```bash
git diff --name-only a1b2c3d z9y8x7w
```

## 🔍 Encontrando Quem Mudou Cada Linha

### git blame (Quem é o "Culpado")

```bash
git blame README.md
```

Resultado:
```
a1b2c3d (Seu Nome 2026-01-13 10:00:00 -0300 1) # Meu Primeiro Projeto
z9y8x7w (Seu Nome 2026-01-13 11:00:00 -0300 2) 
z9y8x7w (Seu Nome 2026-01-13 11:00:00 -0300 3) Este é um projeto para aprender Git.
```

Mostra para cada linha:
- Qual commit a criou
- Quem criou
- Quando foi criado

### 🖱️ Via VS Code com GitLens

Com a extensão GitLens instalada:

1. Abra um arquivo
2. Você verá anotações inline mostrando quem modificou cada linha
3. Passe o mouse sobre uma linha para ver detalhes completos

## 🎯 Comandos de Navegação

### Ver Último Commit

```bash
git log -1
```

### Ver Commit Específico

```bash
git show a1b2c3d
```

### Ver Arquivos de um Commit

```bash
git show --name-only a1b2c3d
```

## 💡 Dicas Práticas

### 1. Sempre use --oneline para Visão Rápida

```bash
git log --oneline
```

É a forma mais rápida de ver o histórico.

### 2. Use Alias para Comandos Frequentes

Configure os aliases mostrados anteriormente para economizar tempo.

### 3. Instale Git Graph

É a melhor forma visual de entender o histórico no VS Code.

### 4. Combine Filtros

```bash
git log --oneline --author="Maria" --since="1 week ago"
```

## 🔄 Comandos Resumidos

```bash
# Ver histórico
git log                          # Histórico completo
git log --oneline               # Histórico resumido
git log --graph                 # Com gráfico
git log -5                      # Últimos 5 commits
git log --author="Nome"         # Por autor
git log --since="1 week ago"    # Por data
git log --grep="palavra"        # Por palavra na mensagem
git log arquivo.txt             # De um arquivo específico

# Ver mudanças
git show a1b2c3d                # Detalhes de um commit
git diff a1b2c3d z9y8x7w       # Diferença entre commits
git blame arquivo.txt           # Quem mudou cada linha

# Alias
git config --global alias.lg "log --oneline --graph"
```

## 🎓 Resumo

✅ Você aprendeu:
- Como visualizar o histórico de commits
- Diferentes formatos do `git log`
- Como filtrar commits por autor, data, mensagem
- Como ver mudanças de commits específicos
- Como criar aliases para economizar tempo
- Como usar extensões do VS Code para visualização

## 🎯 Exercício

1. Crie 3 commits no seu repositório
2. Use `git log --oneline` para ver o histórico
3. Use `git show` para ver detalhes do primeiro commit
4. Crie um alias `git lg` para log com gráfico
5. Instale a extensão Git Graph e explore visualmente

---

## 🎯 Próximos Passos

Agora que você sabe ver o histórico, vamos aprender a desfazer alterações quando algo dá errado!

➡️ **Próximo:** [Desfazendo Alterações](07-desfazendo-alteracoes.md)
