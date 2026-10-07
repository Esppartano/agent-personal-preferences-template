# Guia: uso no dia a dia

**Para quem:** já fez o setup (`um-arquivo/SETUP.md` ou `dois-arquivos/SETUP.md`).
**Quando:** sempre que for mudar suas preferências, ou para consultar onde fica cada coisa.

`<REPO>` = pasta onde você clonou o seu repo.

---

## Dia a dia

- **Antes de mexer:** `git -C <REPO> pull`
- Edite o arquivo **dentro do repo**, nunca o arquivo ponte.
- **Um arquivo:** o arquivo vale para os **dois** agentes. Regra de um só vai na seção "Só Claude Code" ou "Só agy".
- **Dois arquivos:** mudou a parte comum? Copie a mudança para o outro arquivo.
- **Depois de mexer:**
  ```
  git -C <REPO> add .
  git -C <REPO> commit -m "atualiza prefs"
  git -C <REPO> push
  ```
- Na outra máquina: `pull`. Pronto.
- As mudanças só valem em **sessões novas** dos agentes.

---

## Onde fica cada coisa

| | Claude Code | agy |
|---|---|---|
| Arquivo ponte (global) | `~/.claude/CLAUDE.md` | `~/.gemini/GEMINI.md` |
| Sintaxe da ponte | `@caminho` (aceita `~`) | `@[nome](caminho)` (aceita `~`; `@caminho` **não** funciona) |
| Regras só de um projeto | `CLAUDE.local.md` na raiz do projeto | `GEMINI.md` / `AGENTS.md` na raiz do projeto |

**Regras pessoais num projeto de equipe:** para não mexer no `.gitignore` do time, adicione o nome do arquivo em `.git/info/exclude` (vale só naquela máquina).

---

## Alternativa: symlink

Em vez da ponte de uma linha, dá para fazer o `~/.gemini/GEMINI.md` **ser** o arquivo do repo, via link. Só vale a pena se você tiver um motivo específico; a ponte de uma linha é mais simples.
- **Windows:** precisa do Modo de Desenvolvedor (Configurações → Sistema → Para desenvolvedores). Use caminho absoluto, porque o `cmd` não entende `~`:
  ```
  cmd /c mklink "%USERPROFILE%\.gemini\GEMINI.md" "%USERPROFILE%\agent-prefs\um-arquivo\PREFERENCES.md"
  ```
  ⚠️ Sem Modo de Desenvolvedor, só o hardlink (`cmd /c mklink /H ...`) funciona, e ele **quebra** quando um `git pull` altera o arquivo.
- **macOS/Linux:**
  ```
  ln -sf ~/agent-prefs/um-arquivo/PREFERENCES.md ~/.gemini/GEMINI.md
  ```

(No método de dois arquivos, troque o destino por `dois-arquivos/GEMINI.md`.)

---

## ⚠️ Nunca commitar aqui
- `~/.claude/.credentials.json`
- `~/.gemini/oauth_creds.json`
- Tokens, chaves de API, `mcp_config.json` com segredos
- `~/.gemini/config/config.json` (tem o hostname da máquina)

Recomendado: deixe o seu repo **privado**, já que ele descreve como você trabalha.
