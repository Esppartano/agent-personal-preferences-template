# Setup: método de um arquivo

**Para quem:** escolheu o método de um arquivo no README.
**Quando:** uma vez em cada máquina nova.

Os dois agentes leem o mesmo `PREFERENCES.md`. Cada um tem um arquivo "ponte" com o nome que ele espera:

```
~/.claude/CLAUDE.md  ──@caminho──────┐
                                     ├──► <REPO>/um-arquivo/PREFERENCES.md
~/.gemini/GEMINI.md  ──@[prefs](...)──┘
```

Nos comandos abaixo, **troque antes de rodar**:
- `<REPO>` = pasta onde você clonou (ex.: `~/agent-prefs`)
- `<URL>` = endereço do **seu** repo (ex.: `https://github.com/<usuario>/agent-prefs.git`)

---

### 0. Criar o seu repo (só na primeira vez)
- No GitHub, abra o template → **Use this template** → crie o seu repo.

### 1. Clonar
```
git clone <URL> <REPO>
```

### 2. Preparar o repo (só na primeira vez)
- Apague a pasta `dois-arquivos/`.
- Edite `um-arquivo/PREFERENCES.md`: troque tudo entre `<...>` e apague o opcional que não usar.
- Quer um ponto de partida? Veja o [exemplo](../exemplo/PREFERENCES.md). Depois de copiar o que servir, apague a pasta `exemplo/`.
- Faça commit e push:
  ```
  git -C <REPO> add .
  git -C <REPO> commit -m "minhas preferências"
  git -C <REPO> push
  ```

### 3. Criar as pastas dos agentes (se não existirem)
Numa máquina nova, elas só aparecem depois que você abre o agente pela primeira vez.
- **Windows (PowerShell):**
  ```
  New-Item -ItemType Directory -Force "$HOME\.claude", "$HOME\.gemini"
  ```
- **macOS/Linux:**
  ```
  mkdir -p ~/.claude ~/.gemini
  ```

### 4. Claude Code
- Se já existir `~/.claude/CLAUDE.md`, faça backup (`CLAUDE.md.bak`) e passe o que valer a pena para `um-arquivo/PREFERENCES.md`.
- Crie `~/.claude/CLAUDE.md` com **uma única linha**:
  ```
  @<REPO>/um-arquivo/PREFERENCES.md
  ```
  (ex.: `@~/agent-prefs/um-arquivo/PREFERENCES.md`)

### 5. agy (pule se não usar)
O agy aceita inclusão de arquivo, mas com **outra sintaxe**: `@[nome](caminho)`. O `@caminho` do Claude **não** funciona no agy.
- Se já existir `~/.gemini/GEMINI.md`, faça backup (`GEMINI.md.bak`) e passe o que valer a pena para `um-arquivo/PREFERENCES.md`.
- Crie `~/.gemini/GEMINI.md` com **uma única linha**:
  ```
  @[prefs](<REPO>/um-arquivo/PREFERENCES.md)
  ```
  (ex.: `@[prefs](~/agent-prefs/um-arquivo/PREFERENCES.md)`)

Funciona igual no Windows, macOS e Linux. Prefere symlink? Veja "Alternativa: symlink" no [GUIA.md](../GUIA.md).

### 6. Testar
- Abra uma sessão **nova** de cada agente e pergunte: "quais são as minhas preferências?"

Pronto. Para o uso no dia a dia, veja o [GUIA.md](../GUIA.md).

---

## Prompt pronto (para colar no Claude de uma máquina nova)

⚠️ Troque `<URL>` e `<REPO>` antes de colar.

> Faça `git clone <URL> <REPO>` (ou `git pull`, se já existir) e siga o `um-arquivo/SETUP.md`. Antes de mexer em qualquer arquivo ponte:
> 1. Veja se já existem `~/.claude/CLAUDE.md` e `~/.gemini/GEMINI.md`. Se existirem, compare com o `um-arquivo/PREFERENCES.md` e me mostre o que vale aproveitar antes de alterar.
> 2. Depois de eu aprovar, faça os passos 3, 4 e 5.
> 3. Se mudou algo no repo, faça commit e push.
