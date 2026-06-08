---
{"dg-publish":true,"permalink":"/sintaxe-do-obsidian-guia-pratico/","dg-note-properties":{}}
---


> Referência compacta para uso diário. Compatível com Obsidian e Digital Garden.

---

# Formatação Básica

|Recurso|Sintaxe|
|---|---|
|Título 1|`# Título`|
|Título 2|`## Título`|
|Título 3|`### Título`|
|Negrito|`**texto**`|
|Itálico|`*texto*`|
|Negrito + Itálico|`***texto***`|
|Riscado|`~~texto~~`|
|Destaque|`==texto==`|
|Código|`` `texto` ``|
|Subscrito|`H~2~O`|
|Sobrescrito|`X^2^`|
|Linha horizontal|`---`|

---

# Listas e Tarefas

|Recurso|Sintaxe|
|---|---|
|Item|`- Item`|
|Subitem|`- Subitem`|
|Numerada|`1. Item`|
|Tarefa|`- [ ] Fazer`|
|Concluída|`- [x] Feito`|

---

# Links

|Recurso|Sintaxe|
|---|---|
|Link externo|`[Texto](https://site.com)`|
|URL direta|`https://site.com`|
|E-mail|`<email@dominio.com>`|

---

# Tabelas

Tabela básica:

```md
| Nome | Setor |
|------|------|
| João | DAP |
| Maria | RH |
```

Alinhamento:

|Tipo|Sintaxe|
|---|---|
|Esquerda|`:---`|
|Centro|`:---:`|
|Direita|`---:`|

---

# Comentários

|Recurso|Sintaxe|
|---|---|
|Linha única|`%% comentário %%`|
|Multilinha|`%% ... %%`|

---

# Notas de Rodapé

|Recurso|Sintaxe|
|---|---|
|Referência|`Texto[^1]`|
|Definição|`[^1]: Observação`|

---

# 📌 Recursos Exclusivos do Obsidian

## Wikilinks

Criar link para uma nota:

```md
[[Projeto]]
```

Alias:

```md
[[Projeto|Meu Projeto]]
```

Link para seção:

```md
[[Projeto#Cronograma]]
```

Link para bloco:

```md
[[Projeto#^prazo]]
```

---

## Embeds (Incorporação)

Nota inteira:

```md
![[Projeto]]
```

Seção:

```md
![[Projeto#Cronograma]]
```

Bloco:

```md
![[Projeto#^prazo]]
```

---

## Referências de Bloco

Criar:

```md
Prazo final: 30/06/2026
^prazo
```

Usar:

```md
[[Projeto#^prazo]]
```

Incorporar:

```md
![[Projeto#^prazo]]
```

---

## Tags

Tag simples:

```md
#projeto
```

Hierárquica:

```md
#projeto/dap
```

Multinível:

```md
#projeto/dap/ferias
```

---

# 📦 Callouts

## Tipos disponíveis

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

### Nota

```md
> [!note]
> Conteúdo
```

### Dica

```md
> [!tip]
> Conteúdo
```

### Aviso

```md
> [!warning]
> Conteúdo
```

### Perigo

```md
> [!danger]
> Conteúdo
```

### Recolhível aberto

```md
> [!info]+ Detalhes
> Conteúdo
```

### Recolhível fechado

```md
> [!info]- Detalhes
> Conteúdo
```

---

# 🖼️ Imagens e Arquivos

Imagem:

```md
![[imagem.png]]
```

Redimensionar:

```md
![[imagem.png|300]]
```

Largura x Altura:

```md
![[imagem.png|300x200]]
```

PDF:

```md
[[arquivo.pdf]]
```

Página específica:

```md
![[arquivo.pdf#page=5]]
```

Áudio:

```md
![[audio.mp3]]
```

Vídeo:

```md
![[video.mp4]]
```

---

# 💻 Código

Inline:

```md
`const x = 10`
```

Bloco:

````md
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

# 📊 Mermaid (Diagramas)

Fluxograma:

````md
```mermaid
flowchart TD
A --> B
```
````

Sequência:

````md
```mermaid
sequenceDiagram
João->>Maria: Aprova?
Maria->>João: Sim
```
````

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

---

# 🧮 LaTeX

Inline:

```md
$E=mc^2$
```

Bloco:

```md
$
E=mc^2
$
```

Fração:

```latex
\frac{a}{b}
```

Somatório:

```latex
\sum_{i=1}^{n}
```

Integral:

```latex
\int_a^b
```

Raiz:

```latex
\sqrt{x}
```

Matriz:

```latex
\begin{bmatrix}
1 & 2\\
3 & 4
\end{bmatrix}
```

---

# ⚙️ Frontmatter

Metadados da nota:

```yaml
---
title: Projeto Férias

aliases:
  - Ferias

tags:
  - projeto
  - ferias

created: 2026-06-08

updated: 2026-06-08
---
```

---

# 🌐 HTML Útil

Recolhível:

```html
<details>
<summary>Clique aqui</summary>

Conteúdo

</details>
```

Teclas:

```html
<kbd>Ctrl</kbd> + <kbd>P</kbd>
```

Quebra de linha:

```html
<br>
```

---

# 🔍 Query Blocks

Buscar tag:

```query
tag:#projeto
```

Buscar pasta:

```query
path:"Projetos"
```

Buscar texto:

```query
ferias
```
