---
title: 'Mermaid Plugin'
---

The Mermaid plugin turns text in a page into diagrams – flowcharts, sequence diagrams, timelines, mind maps and more. Diagrams match the site's light or dark mode, so try the light/dark switch, and they always print in light colours.

This page is also a test page: copy it into a site's `user/pages` (for example as `99.mermaid-demo/default.md`) and check it against the list at the end.

## A Flowchart

Choosing how to start with open educational resources (OER) comes down to two questions:

```mermaid
flowchart TD
    accTitle: Choosing an entry point for OER
    accDescr: A decision chart. If an open resource already exists and fits your course as it is, adopt it. If one exists but needs changes, adapt it. If nothing suitable exists, create and publish your own.

    EXISTS("`Does an open resource exist?`") -->|Yes| FITS("`Does it fit as it is?`")
    EXISTS -->|No| CREATE["`**3. Create** and publish`"]
    FITS -->|Yes| ADOPT["`**1. Adopt** as it is`"]
    FITS -->|No| ADAPT["`**2. Adapt** for your context`"]
```

The diagram is written as text, in a code block marked `mermaid`, so anyone reusing the page can revise it:

~~~markdown
```mermaid
flowchart TD
    accTitle: Choosing an entry point for OER
    accDescr: A decision chart. If an open resource already exists and fits your course as it is, adopt it. If one exists but needs changes, adapt it. If nothing suitable exists, create and publish your own.

    EXISTS("`Does an open resource exist?`") -->|Yes| FITS("`Does it fit as it is?`")
    EXISTS -->|No| CREATE["`**3. Create** and publish`"]
    FITS -->|Yes| ADOPT["`**1. Adopt** as it is`"]
    FITS -->|No| ADAPT["`**2. Adapt** for your context`"]
```
~~~

The `accTitle` and `accDescr` lines give screen readers a title and description, like an image's alt text.

## A Sequence Diagram

How a page edit travels between Grav and a Git repository with Git Sync. This one uses the older `[mermaid]...[/mermaid]` tags from the Mermaid Diagrams plugin, which still work.

[mermaid]
sequenceDiagram
    accTitle: How Git Sync keeps a site and its repository in step
    accDescr: An author saves a page in Admin, and Grav commits and pushes it to GitHub. A contributor proposes a change on GitHub; once it is merged, a webhook tells Grav, which pulls the update.
    actor Author
    participant Grav
    participant GitHub
    actor Contributor
    Author->>Grav: Save a page in Admin
    Grav->>GitHub: Commit and push
    Contributor->>GitHub: Propose a change
    GitHub->>Grav: Webhook, once merged
    Grav->>GitHub: Pull the update
[/mermaid]

## A Timeline

One way a course might move to open materials, a step at a time:

```mermaid
timeline
    Term 1 : Adopt an open textbook
    Term 2 : Adapt two chapters : Add a local lab guide
    Term 3 : Publish the adapted version : Invite contributions
```

## A Mind Map with Its Own Colours

The 5Rs of open content. This diagram sets its own colour theme (`forest`), which it keeps in both light and dark mode.

```mermaid
---
config:
  theme: forest
---
mindmap
  root((The 5Rs))
    Retain
      Keep a copy
    Reuse
      Use it as it is
    Revise
      Adapt or translate it
    Remix
      Combine it with others
    Redistribute
      Share copies
```

## Custom Colours

Boxes can have their own colours with `classDef`. Here, white text on a dark box, and bold text from Markdown strings:

```mermaid
flowchart TD
    accTitle: Where to send a course question
    accDescr: A decision chart with three outcomes. If a question is not personal, post it in the course forum. If it is personal but not sensitive, use a private forum post or email the teaching team. If it is sensitive or confidential, email the instructor.

    Q["❓ Something to ask or raise"] --> P("`Is it personal to you?`")
    P -->|No| PUB["`💬 **Course forum, public post**
Most questions go here`"]
    P -->|Yes| S("`Is it sensitive or confidential?`")
    S -->|No| TEAM["`🔒 **Private forum post**
or email the teaching team`"]
    S -->|Yes| INSTRUCTOR["`🛡️ **Email the instructor**
For confidential matters`"]

    classDef start     fill:#1F3A5F,stroke:#1F3A5F,color:#FFFFFF
    classDef decision  fill:#E8EAEC,stroke:#5E6A71,color:#20272B
    classDef public    fill:#D6E6F7,stroke:#0055B7,color:#00305F
    classDef personal  fill:#FCEBC7,stroke:#A97400,color:#553900
    classDef sensitive fill:#F6D8DC,stroke:#B0202C,color:#67121C

    class Q start
    class P,S decision
    class PUB public
    class TEAM personal
    class INSTRUCTOR sensitive
```

## Text as Typed

In plain labels, characters such as `*` and `_` show exactly as typed – Grav's Markdown never changes diagram text. For bold or italics, use a Markdown string in backticks instead.

```mermaid
flowchart LR
    A["Plain label: *draft* notes_v2.md"] --> B["`Markdown string: **bold** and _italic_`"]
```

## A Diagram with a Mistake

A diagram that Mermaid can't read shows an error box in its place, and the rest of the page still works:

```mermaid
flowchart LR
    A -->
```

## Testing Checklist

When checking this page after an update, each item should hold:

- Every diagram above draws, except the one with a mistake, which shows an error box
- No diagram code shows while the page loads – just a blank space until each diagram appears
- Switching light and dark mode redraws the diagrams to match, except the mind map, which keeps its `forest` colours
- Printing from dark mode gives light diagrams
- The dark box in Custom Colours has white text
- In Text as Typed, `*draft*` and `notes_v2.md` show as typed, while the Markdown string shows bold and italics
- The two code blocks below, and the one in A Flowchart, stay as code

A plain code block:

```
flowchart LR
    A --> B
```

A `[mermaid]` tag inside a code block:

~~~markdown
[mermaid]
flowchart LR
    A --> B
[/mermaid]
~~~
