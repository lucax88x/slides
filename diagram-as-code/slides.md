---
theme: seriph
background: false
title: diagram-as-code
info: who loves draw.io?
class: text-center
highlighter: shiki
drawings:
  persist: false
transition: slide-left
mdc: true
---

# diagram-as-code

who loves draw.io?

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/lucax88x/slides" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# but.. seriously, who likes draw.io

<div grid="~ cols-2 gap-2" m="t-2">
    <img
      src="/assets/images/drawio.png"
      alt="drawio"
      border="rounded"
    />
</div>

## please raise an hand!

---
---
# paintpoints as developers

---
---

* maintenance of diagrams, in form of UML or draw.io or others
* consistency and scaling
* version control (collaboration)
* the customer has an intranet
* reinventing the wheel
* thinking in arrows and not in "domain entities"
---
---
# so, what is c4model
<b>Context</b>
Context abstraction represents my first need that i presented under the name subsystem, this represent a single block that can contain an isolated complexity inside and locally, a rich or moderate process.
<b>Container</b>
Containers helps to look at the isolated complexity inside a Software Context and see how that complexity looks like, here we need to just understand what happens or can happen inside a local zone.
<b>Component</b>
Components explore the internal composition and detailed blocks of a container, a container can have many components like a database, api, event bus.
<b>Code</b>
This level represents the composition of each component code details like Class , Sequence and Entity relationship.
---
---
# so, what is structurizr

---
layout: center
class: text-center
---

# Learn More

[youtube](https://sli.dev) · [GitHub](https://github.com/lucax88x/slides)
