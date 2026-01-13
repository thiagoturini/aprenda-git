# 3. Primeiros Passos: Criando Seu Repositório

## 🎯 O que é um Repositório?

Um **repositório** (ou "repo") é uma pasta do seu computador que o Git está monitorando. Dentro dela, o Git guarda:
- Todos os seus arquivos
- Todo o histórico de mudanças
- Todas as configurações do projeto

É como transformar uma pasta normal em uma pasta "inteligente" que lembra de tudo que você fez nela.

## 📁 Por Que Preciso Iniciar um Repositório?

Uma pasta comum não tem memória. Se você modificar um arquivo, a versão antiga é perdida para sempre.

Quando você **inicializa** um repositório Git em uma pasta, você está dizendo:
> "Git, eu quero que você comece a guardar o histórico de tudo que eu fizer aqui!"

A partir desse momento, o Git pode:
- Guardar versões dos seus arquivos
- Mostrar o que mudou
- Deixar você voltar no tempo
- E muito mais!

## 🚀 Criando Seu Primeiro Repositório

Vamos criar um projeto de exemplo para praticar.

### ✅ Via Terminal

**1. Crie uma pasta para o projeto:**
```bash
mkdir meu-primeiro-projeto
```

**2. Entre na pasta:**
```bash
cd meu-primeiro-projeto
```

**3. Inicialize o repositório Git:**
```bash
git init
```

**Pronto!** 🎉 

Você verá uma mensagem como:
```
Initialized empty Git repository in /caminho/para/meu-primeiro-projeto/.git/
```

### 🖱️ Via VS Code

**Método 1: Criar pasta nova**

1. Abra o VS Code
2. Vá em: **File > New Window**
3. Vá em: **File > Open Folder**
4. Crie uma nova pasta chamada "meu-primeiro-projeto"
5. Selecione essa pasta
6. Na barra lateral, clique no ícone do **Source Control** (ícone de ramificação)
7. Clique no botão **"Initialize Repository"**

**Método 2: Se já tem uma pasta aberta**

1. Abra o VS Code
2. Abra a pasta do seu projeto (**File > Open Folder**)
3. Clique no ícone **Source Control** na barra lateral (ou pressione `Ctrl+Shift+G`)
4. Clique em **"Initialize Repository"**

**Alternativa via Terminal Integrado do VS Code:**
1. Abra o terminal no VS Code (`` Ctrl+` ``)
2. Use os comandos do terminal mostrados acima

## 🔍 O que Aconteceu?

Quando você executa `git init`, o Git cria uma pasta oculta chamada `.git` dentro do seu projeto.

**⚠️ NUNCA delete essa pasta!** É nela que fica todo o histórico do seu projeto.

### Ver a pasta .git (curiosidade)

**Linux/macOS:**
```bash
ls -la
```

**Windows (PowerShell):**
```bash
dir -Force
```

**Windows (CMD):**
```bash
dir /a
```

Você verá uma pasta `.git` - é o "cérebro" do Git!

## 📊 Estados de um Repositório

Agora seu repositório está **vazio**. Ele existe, mas não tem nenhum commit (nenhuma "foto" salva).

Um arquivo em um repositório Git pode estar em três estados:

1. **Untracked** (Não rastreado): O Git sabe que o arquivo existe, mas não está monitorando
2. **Modified** (Modificado): O arquivo mudou desde o último commit
3. **Staged** (Preparado): O arquivo está pronto para ser commitado

Não se preocupe, vamos ver isso na prática nos próximos capítulos!

## ✅ Verificando o Status

Sempre que quiser saber o que está acontecendo no seu repositório, use:

### ✅ Via Terminal

```bash
git status
```

Você verá algo como:
```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Isso significa: "Você está na branch main, não tem nenhum commit ainda, e não tem nada para commitar."

### 🖱️ Via VS Code

1. Clique no ícone **Source Control** na barra lateral
2. Você verá a lista de mudanças (por enquanto vazia)
3. No rodapé do VS Code, você vê em qual branch está (provavelmente "main")

## 📝 Criando um Arquivo de Teste

Vamos criar um arquivo para ter algo no repositório:

### ✅ Via Terminal

```bash
echo "# Meu Primeiro Projeto" > README.md
```

Este comando cria um arquivo chamado `README.md` com o texto "# Meu Primeiro Projeto".

### 🖱️ Via VS Code

1. Clique em **File > New File** (ou `Ctrl+N`)
2. Digite: `# Meu Primeiro Projeto`
3. Salve como `README.md` (pressione `Ctrl+S`)

Agora execute `git status` novamente:

### ✅ Via Terminal

```bash
git status
```

Você verá:
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

### 🖱️ Via VS Code

No painel **Source Control**, você verá:
- O arquivo `README.md` aparece com a letra **U** (Untracked)
- Um número aparece no ícone do Source Control mostrando 1 mudança

## 💡 Entendendo a Mensagem

O Git está dizendo:
- "Eu vejo que você criou um arquivo chamado README.md"
- "Mas eu ainda não estou rastreando ele"
- "Se você quiser que eu guarde o histórico dele, use `git add`"

## 🎓 Resumo

✅ Você aprendeu:
- O que é um repositório
- Por que precisamos inicializar um repositório
- Como criar um repositório via terminal e VS Code
- O que é o comando `git status`
- O que significa "untracked files"

## 🔄 Comandos Importantes

```bash
git init          # Cria um novo repositório
git status        # Mostra o estado atual do repositório
```

---

## 🎯 Próximos Passos

Agora que temos um repositório e um arquivo, vamos aprender a fazer nosso primeiro commit (salvar a primeira versão)!

➡️ **Próximo:** [Seu Primeiro Commit](04-primeiro-commit.md)
