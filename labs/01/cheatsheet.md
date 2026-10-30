# Markdown Cheat Sheet

My reference for Markdown. **CommonMark** = works in the [CommonMark dingus](https://spec.commonmark.org/dingus/) and on GitHub. **GitHub** = works on GitHub only.

## Contents

- [Text](#text)
- [Lists](#lists)
- [Links and images](#links-and-images)
- [Code](#code)
- [Quotes](#quotes)
- [Tables](#tables)
- [Layout](#layout)
- [Pitfalls](#pitfalls)

## Text

### Headings · CommonMark

One to six `#` create headings of level 1 to 6.

```markdown
#### Heading level 4
```

#### Heading level 4

### Paragraphs and line breaks · CommonMark

An empty line starts a new paragraph. A backslash (or two spaces) at the end of a line forces a line break.

```markdown
First paragraph.

Second paragraph,\
same paragraph, new line.
```

First paragraph.

Second paragraph,\
same paragraph, new line.

### Italic, bold and both · CommonMark

One, two or three asterisks around a word.

```markdown
*italic*, **bold**, ***both***
```

*italic*, **bold**, ***both***

### Strikethrough · GitHub

Two tildes cross out text.

```markdown
~~deleted~~
```

~~deleted~~

### Inline code · CommonMark

Backticks mark code inside a sentence.

```markdown
Run `python script.py` in the terminal.
```

Run `python script.py` in the terminal.

### Escaping a character · CommonMark

A backslash shows a special character as it is.

```markdown
\*not italic\*
```

\*not italic\*

## Lists

### Unordered, ordered and nested lists · CommonMark

`-` for bullets, `1.` for numbers, indentation for nesting.

```markdown
- Fruit
  - Apple
  - Pear
1. First
2. Second
   1. Second, part one
```

- Fruit
  - Apple
  - Pear
1. First
2. Second
   1. Second, part one

### Task lists · GitHub

Checkboxes in a list.

```markdown
- [x] Profile README
- [ ] Cheat sheet
```

- [x] Profile README
- [ ] Cheat sheet

## Links and images

### Inline and reference-style links · CommonMark

The URL directly in brackets, or defined once elsewhere in the file.

```markdown
[GitHub](https://github.com) and [the course][course]

[course]: https://github.com/breuert/data-integration
```

[GitHub](https://github.com) and [the course][course]

[course]: https://github.com/breuert/data-integration

### Relative link to another file · CommonMark

A path instead of a URL. The syntax is standard; the target only exists in my repository.

```markdown
[My licence](../../LICENSE)
```

[My licence](../../LICENSE)

### Link to a section · GitHub

`#` plus the heading in lowercase, spaces become hyphens. GitHub creates these anchors; the dingus does not.

```markdown
[Back to contents](#contents)
```

[Back to contents](#contents)

### Image with alt text · CommonMark

Like a link with `!` in front. The alt text describes the image.

```markdown
![My GitHub avatar](https://github.com/trinhthomas.png?size=80)
```

![My GitHub avatar](https://github.com/trinhthomas.png?size=80)

### Image that is a link · CommonMark

An image inside the brackets of a link.

```markdown
[![My GitHub avatar](https://github.com/trinhthomas.png?size=80)](https://github.com/trinhthomas)
```

[![My GitHub avatar](https://github.com/trinhthomas.png?size=80)](https://github.com/trinhthomas)

## Code

### Fenced code blocks with syntax highlighting · CommonMark / GitHub

Three backticks plus the language. The block is CommonMark; the colours appear only on GitHub.

````markdown
```python
print("Hello")
```

```bash
ls -la
```

```json
{"name": "Thomas"}
```
````

```python
print("Hello")
```

```bash
ls -la
```

```json
{"name": "Thomas"}
```

## Quotes

### Blockquotes, nested and with formatting · CommonMark

`>` quotes, `>>` nests, formatting works inside.

```markdown
> A quote with **bold** text.
>> A nested quote.
```

> A quote with **bold** text.
>> A nested quote.

### Alerts · GitHub

A blockquote with a type in the first line.

```markdown
> [!NOTE]
> Useful information.

> [!WARNING]
> Be careful.
```

> [!NOTE]
> Useful information.

> [!WARNING]
> Be careful.

## Tables

### Table with aligned columns · GitHub

Colons in the second row align left, centre or right.

```markdown
| Left | Centre | Right |
| :--- | :---: | ---: |
| a | b | 1 |
| aa | bb | 22 |
```

| Left | Centre | Right |
| :--- | :---: | ---: |
| a | b | 1 |
| aa | bb | 22 |

### Cell with a link or a pipe · GitHub

Links work inside cells; `\|` shows a pipe.

```markdown
| Tool | Note |
| --- | --- |
| [GitHub](https://github.com) | a \| b |
```

| Tool | Note |
| --- | --- |
| [GitHub](https://github.com) | a \| b |

## Layout

### Horizontal rule · CommonMark

Three hyphens on their own line, with an empty line above.

```markdown
Above

---

Below
```

Above

---

Below

### Collapsed section · CommonMark

HTML `<details>` hides content until clicked. Leave an empty line after `<summary>`.

```markdown
<details>
<summary>Click to open</summary>

Hidden **content**.

</details>
```

<details>
<summary>Click to open</summary>

Hidden **content**.

</details>

### Comment that does not render · CommonMark

An HTML comment is invisible in the result.

```markdown
Visible <!-- invisible -->
```

Visible <!-- invisible -->

## Pitfalls

1. …
2. …
3. …
