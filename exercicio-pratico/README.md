# 🎯 Exercício Prático: Sua Primeira Contribuição!

Bem-vindo ao exercício prático de Git! Este é um exercício **interativo** onde você vai praticar os conceitos aprendidos no curso.

## 🎓 O que você vai aprender:

✅ Clonar um repositório  
✅ Criar uma nova branch  
✅ Fazer alterações em um arquivo  
✅ Fazer commit das suas mudanças  
✅ Enviar suas mudanças para o GitHub  
✅ Criar um Pull Request  

---

## 📋 Pré-requisitos

Antes de começar, certifique-se de ter:

- [ ] Git instalado no seu computador
- [ ] Conta no GitHub criada
- [ ] VS Code instalado (opcional, mas recomendado)
- [ ] Git configurado com seu nome e email

Se ainda não configurou o Git, rode estes comandos:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@example.com"
```

---

## 🚀 Passo a Passo do Exercício

### Passo 1: Clone o Repositório

#### Pelo Terminal:

```bash
# Clone o repositório para o seu computador
git clone https://github.com/thiagoturini/aprenda-git.git

# Entre na pasta do projeto
cd aprenda-git

# Entre na pasta do exercício
cd exercicio-pratico
```

#### Pelo VS Code:

1. Pressione `Ctrl+Shift+P` (ou `Cmd+Shift+P` no Mac)
2. Digite: `Git: Clone`
3. Cole a URL: `https://github.com/thiagoturini/aprenda-git.git`
4. Escolha onde salvar
5. Clique em "Open" quando aparecer a notificação
6. No Explorer, navegue até a pasta `exercicio-pratico`

---

### Passo 2: Crie Sua Branch

**IMPORTANTE:** Nunca trabalhe diretamente na branch `main`! Sempre crie uma branch nova.

#### Pelo Terminal:

```bash
# Crie e mude para uma nova branch com seu nome
# Substitua "seu-nome" pelo seu nome (sem espaços, use hífen)
git checkout -b adiciona-nome-seu-nome

# Exemplo:
# git checkout -b adiciona-nome-joao-silva
# git checkout -b adiciona-nome-maria-santos
```

#### Pelo VS Code:

1. Clique no nome da branch na barra inferior esquerda (deve estar escrito "main")
2. Clique em "+ Create new branch..."
3. Digite: `adiciona-nome-seu-nome` (substitua "seu-nome" pelo seu nome)
4. Pressione Enter

---

### Passo 3: Adicione Seu Nome ao Arquivo

Abra o arquivo `PARTICIPANTES.md` e adicione seu nome na lista!

#### Pelo Terminal (usando nano):

```bash
# Abra o arquivo no editor nano
nano PARTICIPANTES.md

# Ou use qualquer editor de texto:
# code PARTICIPANTES.md  (VS Code)
# vim PARTICIPANTES.md   (Vim)
# notepad PARTICIPANTES.md (Windows)
```

#### Pelo VS Code:

1. No Explorer (barra lateral esquerda), clique em `PARTICIPANTES.md`
2. Role até o final da lista
3. Adicione uma nova linha seguindo o formato:
   ```
   - **Seu Nome Completo** - @seu-usuario-github - Data
   ```

**Exemplo:**

```markdown
- **João Silva** - @joaosilva - 13/01/2026
- **Maria Santos** - @mariasantos - 13/01/2026
- **Seu Nome Aqui** - @seunome - 13/01/2026
```

**Dica:** Respeite o formato e a indentação para manter o arquivo organizado!

---

### Passo 4: Veja o Status das Mudanças

Antes de fazer o commit, vamos ver o que mudou:

#### Pelo Terminal:

```bash
# Veja quais arquivos foram modificados
git status

# Veja exatamente o que mudou no arquivo
git diff PARTICIPANTES.md
```

#### Pelo VS Code:

1. Clique no ícone de **Source Control** na barra lateral esquerda (terceiro ícone, ou `Ctrl+Shift+G`)
2. Você verá o arquivo `PARTICIPANTES.md` com um "M" (Modified)
3. Clique no arquivo para ver as mudanças destacadas:
   - **Verde:** linhas adicionadas
   - **Vermelho:** linhas removidas

---

### Passo 5: Adicione o Arquivo à Área de Stage

#### Pelo Terminal:

```bash
# Adicione o arquivo modificado à área de stage
git add PARTICIPANTES.md

# Ou adicione todos os arquivos modificados
git add .

# Verifique o status novamente
git status
```

#### Pelo VS Code:

1. No painel **Source Control**, você verá `PARTICIPANTES.md` em "Changes"
2. Clique no **+** ao lado do arquivo para adicionar à área de stage
3. O arquivo agora aparece em "Staged Changes"

---

### Passo 6: Faça o Commit

Agora vamos salvar suas mudanças com uma mensagem descritiva!

#### Pelo Terminal:

```bash
# Faça o commit com uma mensagem clara
git commit -m "docs(participantes): adiciona [Seu Nome] à lista"

# Exemplo:
# git commit -m "docs(participantes): adiciona João Silva à lista"
```

#### Pelo VS Code:

1. No painel **Source Control**, digite a mensagem de commit na caixa de texto:
   ```
   docs(participantes): adiciona [Seu Nome] à lista
   ```
2. Pressione `Ctrl+Enter` (ou clique no ✓ Commit)

---

### Passo 7: Envie Sua Branch para o GitHub

#### Pelo Terminal:

```bash
# Envie sua branch para o GitHub
git push origin adiciona-nome-seu-nome

# Substitua "adiciona-nome-seu-nome" pelo nome da sua branch
```

**Nota:** Se for a primeira vez, o Git pode pedir suas credenciais do GitHub.

#### Pelo VS Code:

1. Clique no ícone de **Source Control**
2. Clique nos três pontos `...` no topo
3. Selecione **Push**
4. Se aparecer uma mensagem perguntando sobre publicar a branch, clique em "OK"

---

### Passo 8: Crie um Pull Request (PR)

Agora vamos pedir para o instrutor revisar e aceitar sua contribuição!

1. **Acesse o GitHub** no navegador:
   ```
   https://github.com/thiagoturini/aprenda-git
   ```

2. Você verá um banner amarelo com sua branch e um botão **"Compare & pull request"**
   - Clique nele!

3. **Preencha o Pull Request:**
   - **Título:** `docs(participantes): adiciona [Seu Nome] à lista`
   - **Descrição:** 
     ```
     ## 📝 Descrição
     Adicionando meu nome à lista de participantes do curso de Git.
     
     ## ✅ Checklist
     - [x] Nome adicionado no formato correto
     - [x] Commit com mensagem clara
     - [x] Respeitei a estrutura do arquivo
     ```

4. **Clique em "Create pull request"**

5. **Aguarde a aprovação!** O instrutor vai revisar e fazer o merge da sua contribuição. 🎉

---

## 🎉 Parabéns!

Você acabou de fazer sua primeira contribuição para um projeto no GitHub! 

Você aprendeu:

✅ Como clonar um repositório  
✅ Como criar uma branch  
✅ Como fazer alterações e commits  
✅ Como enviar suas mudanças  
✅ Como criar um Pull Request  

Esses são os conceitos fundamentais que você usará em qualquer projeto colaborativo!

---

## 🔄 Quer Praticar Mais?

Depois que seu PR for aceito, você pode:

1. **Atualizar sua branch local:**
   ```bash
   git checkout main
   git pull origin main
   ```

2. **Ver seu nome na lista!**
   ```bash
   cat PARTICIPANTES.md
   ```

3. **Deletar sua branch antiga (opcional):**
   ```bash
   git branch -d adiciona-nome-seu-nome
   ```

---

## ❓ Problemas Comuns

### "Já existe uma branch com esse nome"

```bash
# Delete a branch antiga e crie novamente
git checkout main
git branch -D adiciona-nome-seu-nome
git checkout -b adiciona-nome-seu-nome
```

### "Conflito ao fazer push"

```bash
# Atualize sua branch com as mudanças mais recentes
git pull origin main
# Resolva os conflitos se houver
git add .
git commit -m "resolve conflitos"
git push origin sua-branch
```

### "Não consigo fazer push"

Verifique se:
- Você está logado no GitHub
- Você tem permissão para contribuir no repositório
- O nome da branch está correto

---

## 📚 Recursos Adicionais

Precisa revisar algum conceito? Volte aos arquivos do curso:

- [03 - Primeiro Repositório](../03-primeiro-repositorio.md)
- [04 - Primeiro Commit](../04-primeiro-commit.md)
- [10 - Criando Branches](../10-criando-branches.md)
- [16 - Push](../16-push.md)
- [97 - Guia Rápido VS Code](../97-guia-rapido-vscode.md)
- [99 - Guia Rápido Terminal](../99-guia-rapido.md)

---

## 💬 Dúvidas?

Se tiver alguma dúvida:

1. Revise o passo a passo acima
2. Consulte os materiais do curso
3. Pergunte ao instrutor
4. Peça ajuda aos colegas!

**Lembre-se:** Errar faz parte do aprendizado! Não tenha medo de experimentar. 🚀

---

**Boa sorte e bons commits!** 💻✨
