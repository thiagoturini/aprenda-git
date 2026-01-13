# 2. Instalação e Configuração Inicial

## 📥 Instalando o Git

### Windows

**Opção 1: Download direto**
1. Acesse [git-scm.com](https://git-scm.com/)
2. Clique em "Download for Windows"
3. Execute o instalador
4. Use as opções padrão (apenas clique "Next")

**Opção 2: Via Chocolatey (se você usa)**
```bash
choco install git
```

### macOS

**Opção 1: Via Homebrew (recomendado)**
```bash
brew install git
```

**Opção 2: Via Xcode Command Line Tools**
```bash
xcode-select --install
```

### Linux

**Ubuntu/Debian:**
```bash
sudo apt update
sudo apt install git
```

**Fedora:**
```bash
sudo dnf install git
```

**Arch Linux:**
```bash
sudo pacman -S git
```

## ✅ Verificando a Instalação

Abra o terminal e digite:

```bash
git --version
```

Você deve ver algo como: `git version 2.40.0`

Se aparecer a versão, o Git está instalado corretamente! 🎉

## ⚙️ Configuração Inicial

Antes de usar o Git, você precisa configurar seu nome e email. Essas informações aparecerão em todos os commits que você fizer.

### ✅ Via Terminal

**1. Configure seu nome:**
```bash
git config --global user.name "Seu Nome"
```

**2. Configure seu email:**
```bash
git config --global user.email "seu.email@exemplo.com"
```

**Exemplo:**
```bash
git config --global user.name "Maria Silva"
git config --global user.email "maria.silva@gmail.com"
```

### 🖱️ Via VS Code

1. Abra o VS Code
2. Pressione `Cmd+Shift+P` (Mac) ou `Ctrl+Shift+P` (Windows/Linux)
3. Digite "Git: Set User Name" e pressione Enter
4. Digite seu nome e pressione Enter
5. Repita para "Git: Set User Email"

**Ou use o terminal integrado do VS Code:**
- Pressione `` Ctrl+` `` (abre o terminal no VS Code)
- Digite os mesmos comandos acima

## 🔍 Verificando suas Configurações

### ✅ Via Terminal

**Ver todas as configurações:**
```bash
git config --list
```

**Ver apenas nome:**
```bash
git config user.name
```

**Ver apenas email:**
```bash
git config user.email
```

### 🖱️ Via VS Code

1. Abra o terminal integrado (`` Ctrl+` ``)
2. Use os comandos acima

## 🎨 Configurações Opcionais (mas Úteis)

### Editor Padrão

Por padrão, o Git usa o Vim como editor. Se você prefere usar o VS Code:

```bash
git config --global core.editor "code --wait"
```

### Cores no Terminal

Deixa a saída do Git colorida (mais fácil de ler):

```bash
git config --global color.ui auto
```

### Nome da Branch Padrão

Configura "main" como nome padrão da branch principal (ao invés de "master"):

```bash
git config --global init.defaultBranch main
```

### Configuração Completa Recomendada

Copie e cole tudo de uma vez (substitua nome e email):

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"
git config --global core.editor "code --wait"
git config --global color.ui auto
git config --global init.defaultBranch main
```

## 📍 Onde Ficam as Configurações?

As configurações ficam salvas em um arquivo chamado `.gitconfig` na sua pasta home.

**Ver o arquivo:**

### Linux/macOS:
```bash
cat ~/.gitconfig
```

### Windows:
```bash
type %USERPROFILE%\.gitconfig
```

## 🔧 Níveis de Configuração

O Git tem três níveis de configuração:

1. **--system**: Para todos os usuários do computador
2. **--global**: Para o seu usuário (o que usamos)
3. **--local**: Apenas para um repositório específico

A prioridade é: local > global > system

## 💡 Dicas

- Use seu **nome real** e **email real** nas configurações
- Se você vai usar GitHub, use o **mesmo email** que você usará lá
- Essas configurações são feitas **uma vez só**
- Você pode mudar essas configurações a qualquer momento

## ⚠️ Troubleshooting

### Problema: "git: command not found"

**Solução:**
- Reinicie o terminal após instalar
- No Windows, pode precisar reiniciar o computador
- Verifique se o Git foi instalado corretamente

### Problema: Não sei meu email do GitHub

**Solução:**
- Acesse [github.com](https://github.com)
- Faça login
- Vá em Settings > Emails
- Use o email que aparece lá (ou pode usar o email privado que o GitHub fornece)

---

## 🎯 Próximos Passos

Agora que o Git está instalado e configurado, vamos criar nosso primeiro repositório!

➡️ **Próximo:** [Primeiros Passos: Criando Seu Repositório](03-primeiro-repositorio.md)
