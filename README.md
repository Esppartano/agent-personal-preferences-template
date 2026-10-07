# agent-personal-preferences-template

Template para guardar num repo Git as suas preferências do **Claude Code** e do **agy (Antigravity CLI)**, sincronizadas entre máquinas.

## Por onde começar

| Arquivo | Para quem | Quando |
|---|---|---|
| `README.md` (este) | Acabou de achar o template | Uma vez, para escolher o método **um-arquivo** ou **dois-arquivos** |
| `<método>/SETUP.md` | Escolheu o método de preferência | Em cada máquina nova |
| `GUIA.md` | Já fez o setup | No dia a dia |

1. Leia "Qual método escolher?" abaixo.
2. Clique em **Use this template** → crie o **seu** repo (pode ser privado).
3. Abra a pasta do método escolhido e siga o `SETUP.md` dela. A outra pasta pode ser apagada.

## Estrutura
```
um-arquivo/
  PREFERENCES.md   ← lido pelos dois agentes
  SETUP.md
dois-arquivos/
  CLAUDE.md        ← lido só pelo Claude Code
  GEMINI.md        ← lido só pelo agy
  SETUP.md
exemplo/
  PREFERENCES.md   ← exemplo preenchido (opcional, para se inspirar)
GUIA.md            ← dia a dia, segurança, onde fica cada coisa
```

Nos dois métodos, cada agente tem um arquivo "ponte" de **uma linha** que aponta para o arquivo do repo. Não precisa de symlink nem de permissão de administrador.

## Qual método escolher?

### `um-arquivo/`: os dois agentes leem o mesmo arquivo
Editou uma vez? Vale para os dois. Bom quando:
- A maior parte das regras vale para os dois agentes.
- As regras específicas de cada agente são poucas.
- O arquivo é curto (cada agente carrega tudo, inclusive as regras do outro).

### `dois-arquivos/`: cada agente tem o seu
A parte comum é copiada à mão entre os dois. Melhor quando:
- Os agentes têm papéis bem diferentes e as regras específicas são maiores que a parte comum.
- Uma regra de um agente não pode, de jeito nenhum, vazar para o outro (ex.: "nunca implemente, só revise").
- Você quer mudar um agente sem correr o risco de afetar o outro sem perceber.

**Na dúvida, comece pelo `um-arquivo/`.** Dá para separar depois.

**Quer ver um exemplo preenchido?** O [exemplo/PREFERENCES.md](exemplo/PREFERENCES.md) mostra um perfil fictício, com o Claude Code e o agy revisando o trabalho um do outro. Copie o que servir e apague a pasta.

**Usa só o Claude Code?** Escolha `um-arquivo/`, pule o passo do agy no setup e apague a seção "Só agy".

**Regras de vários projetos?** Não coloque todas no arquivo global. Use um arquivo na raiz de cada projeto (ver "Onde fica cada coisa" no [GUIA.md](GUIA.md)).
