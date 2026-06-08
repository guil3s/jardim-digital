---
{"dg-publish":true,"permalink":"/sintaxe-do-obsidian-guia-pratico/","dg-note-properties":{}}
---


> Referência rápida para Markdown, Obsidian, Mermaid, LaTeX e recursos avançados.

---

# ⚡ Consulta Rápida

|Categoria|Recurso|Sintaxe|
|---|---|---|
|Texto|Negrito|`**texto**`|
|Texto|Itálico|`*texto*`|
|Texto|Negrito + Itálico|`***texto***`|
|Texto|Riscado|`~~texto~~`|
|Texto|Destaque|`==texto==`|
|Texto|Código|`` `texto` ``|
|Texto|Subscrito|`H~2~O`|
|Texto|Sobrescrito|`X^2^`|
|Estrutura|Título 1|`# Título`|
|Estrutura|Título 2|`## Título`|
|Estrutura|Título 3|`### Título`|
|Estrutura|Linha horizontal|`---`|
|Lista|Item|`- Item`|
|Lista|Subitem|`- Subitem`|
|Lista|Numerada|`1. Item`|
|Lista|Tarefa|`- [ ] Fazer`|
|Lista|Concluída|`- [x] Feito`|
|Link|Externo|`[Texto](https://site.com)`|
|Link|URL|`https://site.com`|
|Link|E-mail|`<email@dominio.com>`|
|Tabela|Coluna|`|
|Tabela|Alinhar esquerda|`:---`|
|Tabela|Alinhar centro|`:---:`|
|Tabela|Alinhar direita|`---:`|
|Rodapé|Referência|`Texto[^1]`|
|Rodapé|Definição|`[^1]: Nota`|
|Comentário|Linha única|`%% comentário %%`|
|Comentário|Multilinha|`%% ... %%`|

---

# 🔗 Wikilinks

```text
\[\[Projeto\]\]

\[\[Projeto\|Meu Projeto\]\]

\[\[Projeto#Cronograma\]\]

\[\[Projeto#^bloco\]\]
```

---

# 📥 Embeds

```text
!\[\[Projeto\]\]

!\[\[Projeto#Cronograma\]\]

!\[\[Projeto#^bloco\]\]
```

---

# 🏷️ Tags

```text
\#projeto

\#projeto/dap

\#projeto/dap/ferias
```

---

# 🧩 Referências de Bloco

Criar:

```text
Texto importante

^bloco
```

Usar:

```text
\[\[Nota#^bloco\]\]

!\[\[Nota#^bloco\]\]
```

---

# 📦 Callouts

Tipos:

```text
note
abstract
info
todo
tip
success
question
warning
failure
danger
bug
example
quote
```

Exemplos:

```text
\> [!note]
\> Conteúdo
```

```text
\> [!warning]
\> Atenção
```

```text
\> [!danger]
\> Crítico
```

Expansível aberto:

```text
\> [!info]+ Detalhes
\> Conteúdo
```

Expansível fechado:

```text
\> [!info]- Detalhes
\> Conteúdo
```

---

# 🖼️ Imagens e Arquivos

```text
!\[\[imagem.png\]\]

!\[\[imagem.png\|300\]\]

!\[\[imagem.png\|300x200\]\]

!\[\[arquivo.pdf\]\]

!\[\[arquivo.pdf#page=5\]\]

!\[\[audio.mp3\]\]

!\[\[video.mp4\]\]
```

---

# 💻 Código

Inline:

```text
`const x = 10`
```

Bloco:

````text
```javascript
const x = 10;
```
````

Linguagens comuns:

```text
javascript
typescript
python
sql
json
yaml
bash
powershell
html
css
```

---

# ⚙️ Frontmatter

```text
\---
title: Minha Nota

aliases:
  - Alias

tags:
  - projeto

created: 2026-06-08
\---
```

---

# 🧮 LaTeX

```text
\$E=mc^2\$

\$\$
E=mc^2
\$\$

\\frac{a}{b}

\\sum_{i=1}^{n}

\\int_a^b

\\sqrt{x}

\\begin{bmatrix}
1 & 2\\
3 & 4
\\end{bmatrix}
```

---

# 📊 Mermaid

Tipos:

```text
flowchart
sequenceDiagram
classDiagram
erDiagram
stateDiagram-v2
journey
timeline
pie
gantt
```

Fluxograma:

```text
\```mermaid
flowchart TD
A --> B
\```
```

Sequência:

```text
\```mermaid
sequenceDiagram
João->>Maria: Aprova?
Maria->>João: Sim
\```
```

---

# 🌐 HTML Útil

```text
<details>

<summary>

<br>

<mark>

<kbd>
```

Exemplo:

```text
<details>
<summary>Clique aqui</summary>

Conteúdo

</details>
```

---

# 🔍 Query Blocks

```text
tag:#projeto

path:"Projetos"

ferias
```

---

# 🔐 Escapes Úteis

|Quero mostrar|Digite|
|---|---|
|`[[Nota]]`|`\[\[Nota\]\]`|
|`![[Nota]]`|`!\[\[Nota\]\]`|
|`#tag`|`\#tag`|
|`> texto`|`\> texto`|
|`$formula$`|`\$formula\$`|
|`$$formula$$`|`\$\$ formula \$\$`|
|`|`|
|`*texto*`|`\*texto\*`|
