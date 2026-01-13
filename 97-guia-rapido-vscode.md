# 🖱️ Guia Rápido: Git no VS Code

Este é um guia de referência rápida para usar Git completamente através da interface do VS Code. Perfeito para quem prefere interface gráfica!

## 🎯 Atalhos de Teclado Essenciais

```
Ctrl+Shift+G        Abrir Source Control
Ctrl+Shift+P        Command Palette (comandos Git)
Ctrl+`              Abrir/Fechar Terminal
Ctrl+Enter          Commit (quando no Source Control)
Ctrl+K Ctrl+O       Abrir pasta/repositório
Ctrl+K Ctrl+S       Salvar todos os arquivos
F1                  Command Palette (alternativa)
```

**Mac:**
- Use `Cmd` ao invés de `Ctrl`
- `Cmd+Shift+G` para Source Control
- `Cmd+Enter` para Commit

## 📍 Onde Encontrar as Funcionalidades

### Barra Lateral Esquerda

```
┌─────────────────────┐
│  📁 Explorer        │ ← Arquivos do projeto
│  🔍 Search          │ ← Buscar em arquivos
│  🌿 Source Control  │ ← Git (Ctrl+Shift+G)
│  🐛 Run and Debug   │ ← Debug
│  📦 Extensions      │ ← Extensões
└─────────────────────┘
```

**Ícone do Source Control:** Parece um "Y" ou ramificação 🌿

### Barra Inferior (Status Bar)

```
┌─────────────────────────────────────────────────┐
│ main ↓2 ↑3  ⚠ 5  ∅ 2  🔔  ≡  { }  UTF-8  LF    │
│  ↑      ↑     ↑    ↑                             │
│  │      │     │    └─ Erros                      │
│  │      │     └────── Avisos                     │
│  │      └──────────── Commits para pull/push    │
│  └─────────────────── Branch atual              │
└─────────────────────────────────────────────────┘
```

**Clique em cada elemento para ações rápidas!**

## 🎨 Cores e Símbolos nos Arquivos

### No Explorer:
```
M  arquivo.js      🟢 Verde  = Modified (modificado)
U  novo.js         🟢 Verde  = Untracked (não rastreado)
D  antigo.js       🔴 Vermelho = Deleted (deletado)
C  conflito.js     🔴 Vermelho = Conflict (conflito)
A  adicionado.js   🟢 Verde  = Added (adicionado)
R  renomeado.js    🟢 Verde  = Renamed (renomeado)
```

### No Source Control:
- **M** = Modified
- **U** = Untracked
- **A** = Added (staged)
- **D** = Deleted
- **C** = Conflict
- **R** = Renamed

## 🚀 Operações Básicas

### 1️⃣ Iniciar Repositório

**Se não tem repositório:**
1. `Ctrl+Shift+G` (Source Control)
2. Clique em **"Initialize Repository"**
3. Pronto! ✨

**Se já tem pasta aberta:**
- Source Control → **Initialize Repository**

### 2️⃣ Ver Mudanças

**Ver arquivos modificados:**
1. Abra Source Control (`Ctrl+Shift+G`)
2. Seção **"Changes"** mostra arquivos modificados

**Ver diferenças (diff):**
- Clique no arquivo no Source Control
- Abre lado a lado:
  - **Esquerda** = Versão antiga
  - **Direita** = Versão nova
  - Linhas vermelhas = removidas
  - Linhas verdes = adicionadas

**Navegar entre mudanças:**
- Setas **↑ ↓** no topo do diff

### 3️⃣ Stage (Adicionar para Commit)

**Stage um arquivo:**
- Passe mouse sobre o arquivo
- Clique no **+** (plus)

**Stage todos os arquivos:**
- Clique no **+** ao lado de "Changes"

**Unstage (remover do stage):**
- Clique no **−** (minus) ao lado do arquivo

**Stage linhas específicas:**
1. Abra o diff do arquivo
2. Selecione as linhas
3. Clique direito → **"Stage Selected Ranges"**

### 4️⃣ Commit

**Fazer commit:**
1. Stage os arquivos que quer commitar
2. Digite mensagem no campo de texto (topo)
3. `Ctrl+Enter` ou clique em **✓ Commit**

**Commit todos os arquivos:**
- Clique na **seta ▼** ao lado de Commit
- Selecione **"Commit All"**

**Commit e push junto:**
- Seta ao lado de Commit
- **"Commit & Push"**

**Amend (corrigir último commit):**
1. Source Control → **⋯** (três pontos)
2. **Commit** → **Commit Staged (Amend)**

### 5️⃣ Histórico de Commits

**Ver histórico:**
- Source Control → **⋯**
- **View History**

**Ou instale extensão:**
- **Git Graph**: Visualização gráfica linda! ⭐
- **Git History**: Histórico detalhado
- **GitLens**: Superpoderes para Git

**Ver detalhes de um commit:**
- Com Git Graph: clique no commit
- Com GitLens: aparece inline no código

### 6️⃣ Descartar Mudanças

**Descartar mudanças em arquivo:**
1. Source Control → arquivo modificado
2. Clique no ícone **↻** (circular) ou
3. Clique direito → **"Discard Changes"**

**⚠️ Não pode ser desfeito!**

**Descartar todas as mudanças:**
- Source Control → **⋯**
- **Changes** → **Discard All Changes**

## 🌿 Trabalhando com Branches

### Ver Branch Atual
**Barra inferior esquerda:** mostra nome da branch (ex: `main`)

### Criar Branch Nova

**Método 1: Clique na branch**
1. Clique em `main` (barra inferior)
2. **+ Create new branch**
3. Digite nome
4. Enter

**Método 2: Command Palette**
1. `Ctrl+Shift+P`
2. "Git: Create Branch"
3. Digite nome

**Método 3: Source Control**
- **⋯** → **Branch** → **Create Branch**

### Alternar Entre Branches

**Método mais rápido:**
1. Clique no nome da branch (barra inferior)
2. Selecione a branch desejada

**Ou:**
- `Ctrl+Shift+P` → "Git: Checkout to..."

### Deletar Branch

**Via lista:**
1. Clique no nome da branch
2. Clique direito na branch a deletar
3. **Delete Branch**

**Via menu:**
- Source Control → **⋯**
- **Branch** → **Delete Branch**

### Merge

**Fazer merge:**
1. Alterne para branch de destino (ex: `main`)
2. Source Control → **⋯**
3. **Branch** → **Merge Branch**
4. Selecione branch origem

**Com Git Graph:**
1. Clique direito na branch
2. **Merge into current branch**

## 🌐 Repositórios Remotos

### Clonar Repositório

**Método 1: Command Palette**
1. `Ctrl+Shift+P`
2. "Git: Clone"
3. Cole URL
4. Escolha pasta
5. **Open** quando terminar

**Método 2: Tela inicial**
- Se não há pasta aberta
- **Clone Git Repository**

**Método 3: Source Control**
- Se vazio, mostra opção **Clone Repository**

### Push (Enviar)

**Push rápido:**
- Clique no ícone **↑↓** (sync) na barra inferior
- Ou clique no **↑** se houver apenas commits para enviar

**Push via menu:**
1. Source Control → **⋯**
2. **Push**

**Push pela primeira vez:**
- VS Code pergunta remoto e branch
- Configure uma vez, depois é automático

**Ver quantos commits para push:**
- Barra inferior: **↑3** = 3 commits para enviar

### Pull (Receber)

**Pull rápido:**
- Clique no ícone **↑↓** (sync) na barra inferior
- Ou clique no **↓** se houver apenas commits para baixar

**Pull via menu:**
1. Source Control → **⋯**
2. **Pull**

**Ver quantos commits para pull:**
- Barra inferior: **↓2** = 2 commits para baixar

### Configurar Remote

**Adicionar remoto:**
1. Terminal integrado (`` Ctrl+` ``)
2. `git remote add origin URL`

**Ver remotos:**
- Source Control → **⋯**
- **Remote** → mostra lista

## 🚨 Resolvendo Conflitos

### Quando Há Conflito:

**VS Code mostra:**
1. Notificação de conflito
2. Arquivo com **C** (conflict) no Source Control
3. Arquivo abre automaticamente com opções

### Interface de Conflito:

```javascript
<<<<<<< Accept Current Change | Accept Incoming Change | Accept Both Changes | Compare Changes

function hello() {
<<<<<<< HEAD (Current Change)
  return "Olá!";
=======
  return "Hello!"; (Incoming Change)
>>>>>>> feature-branch
}
```

**Botões:**
- **Accept Current Change** - Mantém só a versão atual
- **Accept Incoming Change** - Mantém só a versão nova
- **Accept Both Changes** - Mantém as duas
- **Compare Changes** - Abre visualização lado a lado

### Resolver:

1. Clique no botão desejado, **ou**
2. Edite manualmente o código
3. Delete as marcações (`<<<<`, `====`, `>>>>`)
4. Salve o arquivo (`Ctrl+S`)
5. Stage o arquivo (clique no **+**)
6. Commit para finalizar

### Merge Editor (Novo!)

**Para conflitos complexos:**
1. `Ctrl+Shift+P`
2. "Git: Open Merge Editor"
3. Você vê três painéis:
   - **Incoming** (mudanças deles)
   - **Current** (suas mudanças)
   - **Result** (resultado final)
4. Clique nas checkboxes para escolher o que manter

## 🔍 GitLens (Extensão Recomendada)

### Instalar:
1. `Ctrl+Shift+X` (Extensions)
2. Busque "GitLens"
3. Install

### Recursos:

**Anotações inline:**
- Mostra quem mudou cada linha
- Quando foi mudado
- Mensagem do commit

**File History:**
- Clique direito no arquivo
- **"Open File History"**

**Line History:**
- Clique direito em uma linha
- **"Open Line History"**

**Compare:**
- Compare branches
- Compare commits
- Compare com working tree

**Visualizações:**
- **Repositories** - Visão de repositórios
- **File History** - Histórico de arquivos
- **Line History** - Histórico de linhas
- **Branches** - Gerenciar branches
- **Remotes** - Gerenciar remotos
- **Stashes** - Gerenciar stashes
- **Tags** - Gerenciar tags

## 📦 Git Graph (Extensão Essencial)

### Instalar:
1. `Ctrl+Shift+X`
2. Busque "Git Graph"
3. Install

### Usar:

**Abrir:**
- Clique no ícone **Git Graph** na barra inferior
- Ou: Source Control → **⋯** → **View Git Graph**

**Interface:**
```
● ─── ● ─── ● ─── ●  main
    \           /
     ● ─── ●       feature
```

**Ações no Graph:**
- **Clique no commit** → Ver detalhes
- **Clique direito no commit** → Menu de ações
- **Clique direito na branch** → Merge, rebase, etc
- **Arraste para selecionar múltiplos commits**

**Menu de ações:**
- Checkout
- Merge
- Rebase
- Cherry-pick
- Reset
- Create branch
- Create tag

## ⚙️ Configurações Úteis

### Abrir Settings:
- `Ctrl+,` (Ctrl + vírgula)
- Ou: **File** → **Preferences** → **Settings**

### Configurações Git:

**Auto Fetch:**
```json
"git.autofetch": true
```
Busca atualizações automaticamente.

**Confirm Sync:**
```json
"git.confirmSync": false
```
Não pede confirmação para sync.

**Enable Smart Commit:**
```json
"git.enableSmartCommit": true
```
Commit todos se não há staged.

**Post Commit Command:**
```json
"git.postCommitCommand": "push"
```
Push automático após commit.

**Mostrar inline diff:**
```json
"diffEditor.renderSideBySide": false
```
Diff inline (não lado a lado).

### Configurar via Settings UI:

1. `Ctrl+,`
2. Busque "git"
3. Configure visualmente

## 🎯 Command Palette - Comandos Git

Pressione `Ctrl+Shift+P` e digite:

```
Git: Clone                          Clonar repositório
Git: Initialize Repository          Criar repositório
Git: Commit                         Fazer commit
Git: Commit All                     Commit todos
Git: Push                           Enviar commits
Git: Pull                           Baixar commits
Git: Sync                           Sincronizar (pull + push)
Git: Create Branch                  Criar branch
Git: Checkout to...                 Trocar branch
Git: Merge Branch                   Fazer merge
Git: Delete Branch                  Deletar branch
Git: Fetch                          Buscar atualizações
Git: Stage All Changes              Stage tudo
Git: Unstage All                    Unstage tudo
Git: Discard All Changes            Descartar mudanças
Git: Show Git Output                Ver log do Git
Git: View History                   Ver histórico
Git: Stash                          Guardar mudanças
Git: Apply Stash                    Aplicar stash
```

## 📱 Timeline (Linha do Tempo)

**Ver histórico de um arquivo:**

1. Abra o arquivo
2. Na parte inferior do Explorer
3. Seção **TIMELINE** mostra todos os commits

**Ações:**
- Clique no commit para ver mudanças
- Clique direito → **Open Changes**
- Compara com versão daquele commit

## 🔄 Source Control: Estrutura Completa

```
SOURCE CONTROL: GIT
┌──────────────────────────────────┐
│ Message (Ctrl+Enter to commit)   │ ← Campo de mensagem
├──────────────────────────────────┤
│ ✓ Commit  ▼                      │ ← Botão commit
├──────────────────────────────────┤
│ STAGED CHANGES (2)               │ ← Arquivos staged
│   M  arquivo1.js         -       │
│   A  arquivo2.js         -       │
├──────────────────────────────────┤
│ CHANGES (3)                      │ ← Arquivos modificados
│   M  arquivo3.js         +       │
│   U  novo.js             +       │
│   D  antigo.js           +       │
├──────────────────────────────────┤
│ ⋯ More Actions                   │ ← Menu com todas ações
└──────────────────────────────────┘
```

**Ícones:**
- **+** = Stage este arquivo
- **−** = Unstage este arquivo
- **↻** = Discard changes
- **⋯** = More actions

## 🎨 Personalizações Visuais

### Temas Git-Friendly:

**Instalar tema:**
1. `Ctrl+K Ctrl+T` (atalho de tema)
2. Escolha tema com bom suporte Git

**Recomendados:**
- **GitLens Theme** (vem com GitLens)
- **Material Theme**
- **One Dark Pro**

### Ícones do Git:

```json
"workbench.iconTheme": "material-icon-theme"
```

Ícones diferentes para status Git.

### Cores personalizadas:

```json
"workbench.colorCustomizations": {
  "gitDecoration.modifiedResourceForeground": "#ffa500",
  "gitDecoration.deletedResourceForeground": "#ff0000",
  "gitDecoration.untrackedResourceForeground": "#00ff00"
}
```

## 🚀 Fluxo de Trabalho Completo no VS Code

### 1. Início do Dia:

```
1. Abra VS Code
2. Ctrl+Shift+G (Source Control)
3. Clique em ↓ (pull) na barra inferior
4. Confirme que está atualizado
```

### 2. Desenvolvimento:

```
1. Modifique arquivos
2. Ctrl+S para salvar
3. Veja mudanças no Source Control
4. Clique no arquivo para ver diff
```

### 3. Commit:

```
1. Ctrl+Shift+G
2. Stage arquivos (clique em +)
3. Digite mensagem
4. Ctrl+Enter (commit)
```

### 4. Push:

```
1. Veja ↑1 na barra inferior
2. Clique no ícone sync
3. Aguarde confirmação
```

### 5. Nova Feature:

```
1. Clique na branch atual (barra inferior)
2. + Create new branch
3. Digite "feature-nome"
4. Trabalhe normalmente
5. Commit, push
```

### 6. Merge:

```
1. Alterne para main (clique na branch)
2. Pull (↓) para atualizar
3. ⋯ → Branch → Merge Branch
4. Selecione feature-nome
5. Resolva conflitos se houver
6. Push
```

## 💡 Dicas Pro

### Atalhos Personalizados:

**File** → **Preferences** → **Keyboard Shortcuts**

Ou crie em `keybindings.json`:

```json
[
  {
    "key": "ctrl+shift+c",
    "command": "git.commit"
  },
  {
    "key": "ctrl+shift+p",
    "command": "git.push"
  }
]
```

### Multi-cursor em Conflitos:

1. `Alt+Click` para criar múltiplos cursores
2. Selecione todas as marcações de conflito
3. Delete de uma vez

### Diff Editor Inline:

- `Alt+F5` - Próxima mudança
- `Shift+Alt+F5` - Mudança anterior

### Terminal Integrado:

- `` Ctrl+` `` - Toggle terminal
- Comandos Git direto quando precisar
- Combina melhor dos dois mundos!

## 📋 Checklist Diário

```
[ ] Abrir projeto no VS Code
[ ] Pull (↓) para atualizar
[ ] Criar branch se necessário
[ ] Trabalhar e salvar (Ctrl+S)
[ ] Ver mudanças (Ctrl+Shift+G)
[ ] Stage arquivos (+)
[ ] Commit (Ctrl+Enter)
[ ] Push (↑)
[ ] Verificar no GitHub
```

## 🆘 Problemas Comuns

### "Git not found"

**Solução:**
1. Instale Git (veja capítulo 02)
2. Reinicie VS Code
3. `Ctrl+Shift+P` → "Git: Show Git Output" para ver logs

### Não mostra mudanças

**Solução:**
1. Verifique se abriu a pasta correta
2. **File** → **Open Folder**
3. Selecione pasta com `.git`

### Conflitos de merge

**Solução:**
1. Abra arquivo conflitante
2. Use botões do VS Code
3. Ou edite manualmente
4. Stage e commit

### Push falha

**Solução:**
1. Pull primeiro (↓)
2. Resolva conflitos
3. Tente push novamente

### Autenticação falha

**Solução:**
1. Use token, não senha
2. `Ctrl+Shift+P` → "Git: Clone"
3. VS Code gerencia autenticação

## 🎯 Resumo Visual

### Tela do VS Code com Git:

```
┌────────────────────────────────────────────────────┐
│  File  Edit  View  Terminal  Help            ⚙️   │
├─────┬──────────────────────────────────────────────┤
│  📁 │  arquivo.js ●                           M    │
│  🔍 │  function hello() {                          │
│  🌿 │    return "Hello World";    ← GitLens: João  │
│  🐛 │  }                            2 hours ago    │
│  📦 │                                               │
│     │  TIMELINE ▼                                  │
│     │  ● 2 hours ago - João                        │
│     │  ● yesterday - Maria                         │
├─────┴──────────────────────────────────────────────┤
│  main ↓2 ↑3  ⚠ 0  ∅ 0  🔔  Ln 3, Col 5  UTF-8     │
└────────────────────────────────────────────────────┘
```

---

## ✨ Conclusão

O VS Code torna Git **visual, intuitivo e poderoso**! 

**Principais vantagens:**
- ✅ Interface visual clara
- ✅ Resolve conflitos facilmente
- ✅ Diff lado a lado
- ✅ Extensões poderosas
- ✅ Integração perfeita
- ✅ Não precisa memorizar comandos

**Melhor estratégia:**
- Use VS Code para 90% das tarefas
- Terminal para casos específicos
- Combine os dois para máximo poder!

---

**Pratique e ficará natural! 🚀**

**Atalho mais importante:** `Ctrl+Shift+G` (Source Control)

Use-o constantemente e explore a interface!
