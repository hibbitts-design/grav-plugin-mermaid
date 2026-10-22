---
title: 'Mermaid Tests'
---

Edge cases for the Mermaid plugin, each with what to expect. Copy this page into a site's `user/pages` (for example as `99.mermaid-test/default.md`), and check it in light and dark mode, and printed from dark mode. For the main features, see `mermaid-demo.md`.

## Fenced Block with Markdown Characters

Expect: the labels read exactly as typed, including `*your*` and `content_here` – Grav's Markdown doesn't change diagram text.

```mermaid
flowchart LR
    A[Read a guide] --> B{Want to reuse it?}
    B -->|Yes| C[Copy to your site]
    B -->|No| D[Keep reading]
    C --> E[Edit with *your* content_here]
```

## Older [mermaid] Tags

Expect: a sequence diagram. The mention of [mermaid] in this heading and sentence is left alone – only a tag at the start of a line counts.

[mermaid]
sequenceDiagram
    Author->>Grav: Save page
    Grav-->>Reader: Show diagram
[/mermaid]

## Special Characters

Expect: `<`, `>`, `&` and quotes show as typed.

```mermaid
flowchart LR
    A["x < y & y > z"] --> B["Say #quot;hello#quot;"]
```

## Several Diagrams in a Row

Expect: both draw, one after the other.

```mermaid
pie title Example: content formats
    "Markdown" : 60
    "HTML" : 25
    "PDF" : 15
```

```mermaid
flowchart LR
    Markdown --> HTML --> Print
```

## Multi-line Description and Custom Colours

Expect: a screen reader announces the title and the full description; the dark box has white text, in light and dark mode.

```mermaid
flowchart LR
    accTitle: A two-step check
    accDescr {
      A draft goes to review.
      Once reviewed, it is published.
    }
    DRAFT[Draft] --> REVIEW[Review] --> PUBLISH[Publish]
    classDef dark fill:#1F3A5F,stroke:#1F3A5F,color:#FFFFFF
    class DRAFT dark
```

## Own Colour Theme

Expect: green (`forest`) in both light and dark mode.

```mermaid
---
config:
  theme: forest
---
flowchart LR
    A[Read] --> B[Reuse]
```

## A Link in a Diagram

Expect: clicking Special Characters jumps to that section of this page.

```mermaid
flowchart LR
    A[Go to] --> B[Special Characters]
    click B "#special-characters"
```

## A Wide Diagram

Expect: with Diagram Width set to Fit to Page, it shrinks to fit; with Natural Size, it scrolls sideways without the page scrolling.

```mermaid
flowchart LR
    A[Find] --> B[Read] --> C[Adopt] --> D[Adapt] --> E[Remix] --> F[Publish] --> G[Share] --> H[Invite contributions] --> I[Review changes] --> J[Release a new edition]
```

## In a Closed Details Box

Expect: open the box to find a correctly drawn diagram, with labels that fit their boxes. (Written as HTML, as Markdown inside HTML needs Markdown Extra.)

<details>
<summary>Show the diagram</summary>
<pre><code class="language-mermaid">flowchart LR
    A[Hidden at first] --&gt; B[Still drawn correctly]
</code></pre>
</details>

## A Diagram with a Mistake

Expect: an error box, while the diagrams after it still draw.

```mermaid
flowchart LR
    A -->
```

```mermaid
flowchart LR
    A[Still drawn] --> B[After the error]
```

## Not Drawn

Expect: all three stay as code.

A plain code block:

```
flowchart LR
    A --> B
```

A `[mermaid]` tag inside a code block:

```text
[mermaid]
flowchart LR
    A --> B
[/mermaid]
```

A Mermaid example shown as source, wrapped in `~~~` rather than four backticks, which Grav's Markdown ends at the first inner fence:

~~~markdown
```mermaid
flowchart LR
    A --> B
```
~~~
