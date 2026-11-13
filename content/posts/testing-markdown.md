+++
title = 'Testing Markdown Styling'
description = "A page to test all markdown styling."
date = '2026-11-12T19:11:40-05:00'
draft = true
+++

Welcome to the **Markdown Feature Showcase**! This post exists to test how your Hugo theme renders different Markdown elements.

You can use this page to check typography, spacing, syntax highlighting, tables, lists, and more.

---

## 1. Text Formatting

This paragraph contains **bold text**, *italic text*, ***bold and italic text***, ~~strikethrough text~~, and `inline code`.

You can also combine formatting: **bold with *italic* inside**, or ~~strikethrough with `inline code`~~.

Here is a [link to GitHub](https://github.com/) and an example of an automatic URL: https://gohugo.io/.

A paragraph with a  
manual line break.

A paragraph with a normal line break that should not necessarily create a new line.

## 2. Headings

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

## 3. Blockquotes

> This is a basic blockquote.
>
> It can contain multiple paragraphs.
>
> **Formatted text** and `inline code` work inside blockquotes too.

Nested blockquotes:

> This is the outer quote.
>
> > This is a nested quote.
> >
> > > And this is nested even further.

## 4. Lists

### Unordered Lists

- First item
- Second item
  - Nested item
  - Another nested item
    - Third-level nested item
- Final item

### Ordered Lists

1. First step
2. Second step
3. Third step
   1. Nested step
   2. Another nested step
4. Final step

### Mixed Lists

1. Install Hugo.
   - Create a new project.
   - Configure the theme.
2. Write Markdown.
   - Add headings.
   - Add code blocks.
3. Build the site.

## 5. Code

Inline code: `fmt.Println("Hello, world!")`

### Plain Code Block

```
This is a plain code block.
It should use a monospace font.
No syntax highlighting is required.
```

### Bash

```bash
#!/usr/bin/env bash

set -euo pipefail

PROJECT="komidan"
BUILD_DIR="public"

echo "Building ${PROJECT}..."

hugo --minify --destination "${BUILD_DIR}"

if [[ -d "${BUILD_DIR}" ]]; then
    echo "Build completed successfully."
fi
```

### HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Example Page</title>
</head>
<body>
    <header>
        <h1>Hello, world!</h1>
    </header>

    <main>
        <p>This is an example HTML document.</p>
        <a href="/about/">About</a>
    </main>
</body>
</html>
```

### CSS

```css
:root {
    --bg: #282828;
    --fg: #ebdbb2;
    --accent: #d3869b;
}

body {
    background: var(--bg);
    color: var(--fg);
    font-family: monospace;
}

a {
    color: var(--accent);
    transition: color 200ms ease;
}

a:hover {
    text-decoration: none;
}
```

### JavaScript

```javascript
const characters = ["🐎", "馬", "猫", "ツ"];

function randomCharacter() {
    const index = Math.floor(Math.random() * characters.length);
    return characters[index];
}

document.addEventListener("DOMContentLoaded", () => {
    const title = document.querySelector("#site-title");

    if (title) {
        title.textContent += randomCharacter();
    }
});
```

### TypeScript

```typescript
interface Project {
    title: string;
    status: "active" | "paused" | "completed";
    repository?: string;
}

function describeProject(project: Project): string {
    return `${project.title} (${project.status})`;
}

const project:
