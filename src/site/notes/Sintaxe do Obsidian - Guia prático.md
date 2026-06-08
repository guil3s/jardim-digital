---
{"dg-publish":true,"permalink":"/sintaxe-do-obsidian-guia-pratico/","dg-note-properties":{}}
---


|Categoria|Recurso|Sintaxe|
|---|---|---|
|Texto|Negrito|`**texto**`|
|Texto|Itálico|`*texto*`|
|Texto|Negrito + Itálico|`***texto***`|
|Texto|Riscado|`~~texto~~`|
|Texto|Destacado|`==texto==`|
|Texto|Código inline|`` `texto` ``|
|Texto|Subscrito|`H~2~O`|
|Texto|Sobrescrito|`X^2^`|
|Estrutura|Título 1|`# Título`|
|Estrutura|Título 2|`## Título`|
|Estrutura|Título 3|`### Título`|
|Estrutura|Título 4|`#### Título`|
|Estrutura|Título 5|`##### Título`|
|Estrutura|Título 6|`###### Título`|
|Estrutura|Linha horizontal|`---`|
|Estrutura|Quebra de linha|`Linha 1\`|
|Lista|Item|`- Item`|
|Lista|Subitem|`- Subitem`|
|Lista|Numerada|`1. Item`|
|Lista|Tarefa pendente|`- [ ] Fazer`|
|Lista|Tarefa concluída|`- [x] Feito`|
|Link|Externo|`[Google](https://google.com)`|
|Link|URL direta|`https://obsidian.md`|
|Link|E-mail|`<email@dominio.com>`|
|Obsidian|Nota|`[[Projeto]]`|
|Obsidian|Alias|`[[Projeto\|Meu Projeto]]`|
|Obsidian|Cabeçalho|`[[Projeto#Cronograma]]`|
|Obsidian|Cabeçalho + Alias|`[[Projeto#Cronograma\|Cronograma]]`|
|Obsidian|Bloco|`[[Projeto#^prazo]]`|
|Obsidian|Nota incorporada|`![[Projeto]]`|
|Obsidian|Seção incorporada|`![[Projeto#Cronograma]]`|
|Obsidian|Bloco incorporado|`![[Projeto#^prazo]]`|
|Obsidian|Criar bloco|`Texto importante` + `^bloco`|
|Tags|Simples|`#projeto`|
|Tags|Hierárquica|`#projeto/dap`|
|Tags|Multinível|`#projeto/dap/ferias`|
|Citação|Simples|`> Texto`|
|Citação|Nível 2|`>> Texto`|
|Citação|Nível 3|`>>> Texto`|
|Callout|Nota|`> [!note]`|
|Callout|Abstract|`> [!abstract]`|
|Callout|Info|`> [!info]`|
|Callout|Todo|`> [!todo]`|
|Callout|Tip|`> [!tip]`|
|Callout|Success|`> [!success]`|
|Callout|Question|`> [!question]`|
|Callout|Warning|`> [!warning]`|
|Callout|Failure|`> [!failure]`|
|Callout|Danger|`> [!danger]`|
|Callout|Bug|`> [!bug]`|
|Callout|Example|`> [!example]`|
|Callout|Quote|`> [!quote]`|
|Callout|Expansível aberto|`> [!info]+ Título`|
|Callout|Expansível fechado|`> [!info]- Título`|
|Tabela|Estrutura básica|`\| Nome \| Cargo \|`|
|Tabela|Separador|`\|------\|------\|`|
|Tabela|Alinhar esquerda|`:---`|
|Tabela|Alinhar centro|`:---:`|
|Tabela|Alinhar direita|`---:`|
|Rodapé|Referência|`Texto[^1]`|
|Rodapé|Definição|`[^1]: Observação`|
|Comentário|Linha única|`%% comentário %%`|
|Comentário|Multilinha|`%% ... %%`|
|Imagem|Inserir|`![[imagem.png]]`|
|Imagem|Redimensionar|`![[imagem.png\|300]]`|
|Imagem|Largura x Altura|`![[imagem.png\|300x200]]`|
|PDF|Inserir|`[[arquivo.pdf]]`|
|PDF|Página específica|`![[arquivo.pdf#page=5]]`|
|Áudio|Inserir|`![[audio.mp3]]`|
|Vídeo|Inserir|`![[video.mp4]]`|
|Código|Bloco genérico|` ``` ``` `|
|Código|JavaScript|` ```javascript ``` `|
|Código|SQL|` ```sql ``` `|
|Código|JSON|` ```json ``` `|
|Código|YAML|` ```yaml ``` `|
|Código|Python|` ```python ``` `|
|Matemática|Fórmula inline|`$E=mc^2$`|
|Matemática|Fórmula bloco|`$$ fórmula $$`|
|Matemática|Fração|`\frac{a}{b}`|
|Matemática|Somatório|`\sum_{i=1}^{n}`|
|Matemática|Integral|`\int_a^b`|
|Matemática|Raiz|`\sqrt{x}`|
|Matemática|Potência|`x^2`|
|Matemática|Matriz|`\begin{bmatrix}...\end{bmatrix}`|
|Mermaid|Fluxograma|`flowchart TD`|
|Mermaid|Sequência|`sequenceDiagram`|
|Mermaid|Classe|`classDiagram`|
|Mermaid|Gantt|`gantt`|
|Mermaid|ERD|`erDiagram`|
|Mermaid|Timeline|`timeline`|
|Mermaid|Jornada|`journey`|
|Mermaid|Estado|`stateDiagram-v2`|
|Mermaid|Pizza|`pie`|
|HTML|Recolhível|`<details>`|
|HTML|Título recolhível|`<summary>`|
|HTML|Quebra linha|`<br>`|
|HTML|Destacar|`<mark>`|
|HTML|Tecla|`<kbd>Ctrl</kbd>`|
|HTML|Div|`<div>`|
|HTML|Span|`<span>`|
|Escape|Asterisco literal|`\*texto\*`|
|Escape|Tag literal|`\#tag`|
|Escape|Wikilink literal|`\[\[Nota\]\]`|
|Escape|Pipe literal|`\|`|
|Query|Buscar tag|`tag:#projeto`|
|Query|Buscar pasta|`path:"Projetos"`|
|Query|Buscar texto|`ferias`|
|Frontmatter|Início/Fim|`---`|
|Frontmatter|Título|`title: Minha Nota`|
|Frontmatter|Alias|`aliases:`|
|Frontmatter|Tags|`tags:`|
|Frontmatter|Data|`created: 2026-06-08`|
|Frontmatter|Classe CSS|`cssclasses:`|

---

## Tipos de Callout

|Tipo|
|---|
|`note`|
|`abstract`|
|`info`|
|`todo`|
|`tip`|
|`success`|
|`question`|
|`warning`|
|`failure`|
|`danger`|
|`bug`|
|`example`|
|`quote`|

---

## Tipos de Mermaid

|Tipo|Sintaxe|
|---|---|
|Fluxograma|`flowchart TD`|
|Sequência|`sequenceDiagram`|
|Classe|`classDiagram`|
|ERD|`erDiagram`|
|Estado|`stateDiagram-v2`|
|Jornada|`journey`|
|Timeline|`timeline`|
|Pizza|`pie`|
|Gantt|`gantt`|

---

## Frontmatter Completo

```yaml
---
title: Minha Nota

aliases:
  - Alias 1
  - Alias 2

tags:
  - projeto
  - obsidian

created: 2026-06-08

updated: 2026-06-08

cssclasses:
  - dashboard
---
```