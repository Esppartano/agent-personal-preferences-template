# Tutorial: preferências dos agentes sincronizadas

Este repo guarda as preferências do **Claude Code** e do **agy (Antigravity)**.
Os agentes não leem daqui direto: cada um tem um arquivo "ponte" que aponta para o arquivo do repo.

```
<REPO>/
├── claude/CLAUDE.md   ← preferências do Claude Code
└── agy/GEMINI.md      ← preferências do agy
```

Nos comandos abaixo:
- `<REPO>` = pasta onde você clonou (ex.: `~/agent-prefs`)
- `<URL>` = endereço do **seu** repo (ex.: `https://github.com/<usuario>/agent-prefs.git`)

---

## Máquina nova (setup único)

### 0. Criar o seu repo (só na primeira vez)
- [ ] No GitHub, abra este template → **Use this template** → crie o seu repo.
- [ ] Edite `claude/CLAUDE.md` e `agy/GEMINI.md`: troque tudo entre `<...>` e apague o opcional que não usar.

### 1. Clonar
```
git clone <URL> <REPO>
```

### 2. Claude Code
- [ ] Se já existir `~/.claude/CLAUDE.md`, faça backup (`CLAUDE.md.bak`) e passe o que valer a pena para `claude/CLAUDE.md`.
- [ ] Crie `~/.claude/CLAUDE.md` com **uma única linha**:
  ```
  @<REPO>/claude/CLAUDE.md
  ```
  (`~` funciona aqui, ex.: `@~/agent-prefs/claude/CLAUDE.md`)
- [ ] **(Só se usar a seção 3 do GEMINI.md com o Claude)** libere a leitura em `~/.claude/settings.json` (faça depois do passo 3):
  ```json
  "permissions": { "allow": [
    "Read(~/.gemini/GEMINI.md)",
    "Read(<REPO>/agy/GEMINI.md)"
  ] }
  ```
  As duas linhas são necessárias: o Claude checa o caminho real do link.

### 3. agy (pule se não usar)
O agy lê `~/.gemini/GEMINI.md`, mas **não expande `@import`**. Por isso a ponte é um **link de arquivo**.
- [ ] Se já existir `~/.gemini/GEMINI.md`, faça backup (`GEMINI.md.bak`) e passe o que valer a pena para `agy/GEMINI.md`.
- [ ] **Windows:**
  1. Ative o Modo de Desenvolvedor (Configurações → Sistema → Para desenvolvedores).
  2. Apague o `~/.gemini/GEMINI.md` original e crie o symlink:
     ```
     cmd /c mklink "%USERPROFILE%\.gemini\GEMINI.md" "<REPO>\agy\GEMINI.md"
     ```
     ⚠️ Use `mklink`: o `New-Item -ItemType SymbolicLink` do PowerShell 5.1 pede admin mesmo com o Modo de Desenvolvedor.
  3. Sem Modo de Desenvolvedor: `mklink /H` (hardlink). ⚠️ Ele **quebra** quando um `git pull` altera o `agy/GEMINI.md`; aí é preciso apagar e recriar.
- [ ] **macOS/Linux:**
  ```
  ln -sf <REPO>/agy/GEMINI.md ~/.gemini/GEMINI.md
  ```

### 4. Testar
- [ ] Abra uma sessão **nova** de cada agente e pergunte: "quais são as minhas preferências?"

---

## Dia a dia

- [ ] **Antes de mexer:** `git -C <REPO> pull`
- [ ] Edite o arquivo **dentro do repo**, nunca o arquivo ponte.
- [ ] **Depois de mexer:**
  ```
  git -C <REPO> add .
  git -C <REPO> commit -m "atualiza prefs"
  git -C <REPO> push
  ```
- [ ] Na outra máquina: `pull`. Pronto.
- [ ] As mudanças só valem em **sessões novas** dos agentes.

---

## Prompt pronto (para colar no Claude de uma máquina nova)

> Faça `git clone <URL> <REPO>` (ou `git pull`, se já existir) e siga o `TUTORIAL.md`. Antes de mexer em qualquer arquivo ponte:
> 1. Veja se já existem `~/.claude/CLAUDE.md` e `~/.gemini/GEMINI.md`. Se existirem, compare com os do repo e me mostre o que vale aproveitar antes de alterar.
> 2. Depois de eu aprovar, faça os passos 2 e 3.
> 3. Se mudou algo no repo, faça commit e push.

---

## Onde fica cada coisa

| | Claude Code | agy |
|---|---|---|
| Arquivo ponte (global) | `~/.claude/CLAUDE.md` | `~/.gemini/GEMINI.md` |
| Tipo de ponte | `@import` (aceita `~`) | symlink/hardlink (`@import` não funciona) |
| Regras só de um projeto | `CLAUDE.local.md` na raiz do projeto | `GEMINI.md` / `AGENTS.md` na raiz do projeto |

**Regras pessoais num projeto de equipe:** para não mexer no `.gitignore` do time, adicione o nome do arquivo em `.git/info/exclude` (vale só naquela máquina).

---

## ⚠️ Nunca commitar aqui
- `~/.claude/.credentials.json`
- `~/.gemini/oauth_creds.json`
- Tokens, chaves de API, `mcp_config.json` com segredos
- `~/.gemini/config/config.json` (tem o hostname da máquina)

Recomendado: deixe o seu repo **privado**, já que ele descreve como você trabalha.
