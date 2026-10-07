<!--
  EXEMPLO PREENCHIDO (perfil fictício) do método um-arquivo.
  Use como inspiração: copie o que servir para o seu arquivo e apague esta pasta.
-->

# Sobre mim
- Estudante de Ciência da Computação, 5º período.
- Prefiro respostas em português.
- Leio melhor em listas curtas do que em parágrafos longos.

# Formato das respostas
- Resposta direta primeiro; detalhes só se eu pedir.
- Tarefas grandes: um passo de cada vez, indicando o progresso ("passo 2 de 4").
- Código sempre com o nome do arquivo e o trecho que mudou, não o arquivo inteiro.

# Como trabalhar comigo
- Em trabalhos da faculdade: explique o conceito e dê dicas; só entregue o código se eu pedir explicitamente.
- Em scripts, configuração de ambiente e projetos pessoais: pode implementar direto.
- Antes de apagar ou sobrescrever arquivos, me mostre o que vai mudar.

# Ferramentas e colaboração entre agentes
- Uso o Claude Code (`claude -p "..."` no modo não interativo) e o agy (`agy -p "..."`). Os dois leem este mesmo arquivo.
- **Um revisa o outro.** Quando eu pedir uma segunda opinião:
  1. O agente que implementou escreve um prompt **autocontido** para o outro: objetivo, arquivos alterados, o que foi feito e o que precisa ser checado. O outro agente não tem o contexto da conversa.
  2. O revisor **só lista problemas**, por arquivo e em ordem de importância. Não edita nada.
  3. O agente que implementou avalia cada ponto ("concordo", "concordo em parte", "discordo") com o motivo, e só então aplica o que eu aprovar.
- Afirmação técnica do revisor que não dá para confirmar só lendo (ex.: "a ferramenta X aceita a sintaxe Y") deve ser **testada** antes de mudar o código.
- Não desfazer o trabalho do outro agente sem explicar o motivo.

# Só Claude Code
> Se você **não** é o Claude Code, ignore esta seção.
- Quando eu mudar de assunto na mesma sessão, me lembre de usar `/clear`.

# Só agy
> Se você **não** é o agy (Antigravity CLI), ignore esta seção.
- Seu papel padrão é de **revisor**: aponte bugs, casos não tratados e inconsistências antes de sugerir estilo.

# Projeto Calculadora de Notas
> **Condição**: aplicar esta seção **apenas** quando o diretório de trabalho for o repositório `calc-notas` (tem `calc_notas/` e `pyproject.toml` na raiz). **Fora dele, ignorar tudo abaixo.**

## Critérios de revisão
- Arredondamento de notas segue a regra da universidade (uma casa decimal, meio para cima).
- Nenhuma função lê arquivo e calcula ao mesmo tempo.

## Padrões de arquitetura
- **Stack**: Python 3.12, pytest.
- **Camadas**: `calc_notas/io.py` (leitura de planilhas), `calc_notas/regras.py` (cálculo, sem I/O), `calc_notas/cli.py` (interface).

## Checklist de validação
Antes de concluir qualquer tarefa:
1. `pytest`
2. `ruff check .`
3. Rodar `python -m calc_notas exemplo.csv` e conferir se a saída não mudou sem motivo.
