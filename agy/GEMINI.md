<!--
  Preferências globais do agy (Antigravity CLI).
  Troque cada <...> pelo seu conteúdo. Mantenha a seção 0 alinhada com claude/CLAUDE.md.
-->

# Diretrizes e Preferências do Agente

A seção 3 vale só para o projeto <NOME>.

---

## 0. Sobre o Desenvolvedor

* <Quem você é: área de estudo ou trabalho.>
* **Formato**: <tamanho e estilo das respostas>.
* <Quando o agente pode implementar direto e quando deve só explicar.>

---

## 1. Papel e Modo de Operação

* **Atuação**: <papel do agente>.
* **Idioma**: <idioma>.
* **Comunicação**: <tom e estilo>.

---

## 2. Colaboração com outros agentes (opcional)

* <Como o agy deve tratar o trabalho feito por outro agente: revisar, não sobrescrever sem motivo, etc.>

---

## 3. Somente no projeto <NOME> (opcional)

> **Condição**: aplicar esta seção **apenas** quando o diretório de trabalho for o repositório do <NOME> (ex.: <como reconhecer o repo>). **Fora dele, ignorar tudo abaixo.**

### 3.1 Critérios de Revisão
* <O que conferir em toda revisão.>

### 3.2 Padrões de Arquitetura
* **Stack**: <linguagem/framework>.
* **Camadas**: <pastas e responsabilidades>.

### 3.3 Checklist de Validação
Antes de concluir qualquer tarefa:
1. <Comando de testes.>
2. <Comando de lint/sintaxe.>
3. <O que verificar contra regressões.>
