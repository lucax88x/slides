---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---
---
<div class="pt-12">
  <span class="text-5xl font-bold">Microfrontends</span>
  <p class="text-2xl mt-4 opacity-75">The Good, The Bad, and The Federation</p>
</div>

<div class="abs-br m-6 flex gap-2">
  <span>[Your Name]</span>
  <span>[Your Company/Community]</span>
  <span class="opacity-50">[Date]</span>
</div>

---
layout: default
---

# Agenda

<div class="grid grid-cols-2 gap-4">
<div>

1.  **The Problem**: The Crisis of the Frontend Monolith
2.  **The Promise**: What is a Microfrontend?
3.  **The Harsh Reality**: Why You (Often) Shouldn't Use Them
</div>
<div>

4.  **The Modern Solution**: Module Federation
5.  **Case Study**: Our Journey at [Project Name]
6.  **The Future**: A Glimpse at Rolldown
</div>
</div>

<br>
<br>

<p class="opacity-75">Spoiler: there's no simple answer.</p>

---
layout: two-cols
---

# 1. The Crisis of the Frontend Monolith

### The "Big Ball of Mud"

A single, huge Single Page Application (SPA) that contains everything.

<br>

<div v-click>

#### The Pain Points:
-   🐢 **Slow builds**: Minutes to start the dev environment or for a production build.
-   🔗 **Tight coupling**: A change in one place can break something seemingly unrelated.
-   🤝 **Difficulty scaling teams**: Merge-hell, confusing code ownership, difficult onboarding.
-   🔒 **Locked-in tech stack**: Upgrading a major dependency (e.g., from React 16 to 18) is a monumental task.

</div>

::right::

<img src="https://i.imgur.com/gKddm29.jpeg" alt="Tangled Yarn" class="rounded-lg shadow-lg" />

---
layout: default
---

# 2. The Promise: Microfrontends

> An architectural style where front-end applications are composed of **smaller, independent, and autonomously deployable pieces**.

<br>

### The Microservices Analogy

<div class="grid grid-cols-2 gap-8 mt-4">

<div class="text-center">
  <p>Backend Monolith</p>
  <svg class="w-40 h-40 mx-auto" viewBox="0 0 24 24"><path fill="currentColor" d="M4 4h16v16H4z"/></svg>
  <p class="text-4xl opacity-50">→</p>
  <p>Microservices</p>
  <div>
    <svg class="w-12 h-12 inline-block" viewBox="0 0 24 24"><path fill="currentColor" d="M4 4h6v6H4z"/></svg>
    <svg class="w-12 h-12 inline-block" viewBox="0 0 24 24"><path fill="currentColor" d="M14 4h6v6h-6z"/></svg>
    <svg class="w-12 h-12 inline-block" viewBox="0 0 24 24"><path fill="currentColor" d="M4 14h6v6H4z"/></svg>
  </div>
</div>

<div class="text-center">
  <p>Frontend Monolith</p>
  <svg class="w-40 h-40 mx-auto" viewBox="0 0 24 24"><path fill="currentColor" d="M4 4h16v16H4z"/></svg>
  <p class="text-4xl opacity-50">→</p>
  <p>Microfrontends</p>
  <div>
    <svg class="w-12 h-12 inline-block" viewBox="0 0 24 24"><path fill="currentColor" d="M4 4h6v6H4z"/></svg>
    <svg class="w-12 h-12 inline-block" viewBox="0 0 24 24"><path fill="currentColor" d="M14 4h6v6h-6z"/></svg>
    <svg class="w-12 h-12 inline-block" viewBox="0 0 24 24"><path fill="currentColor" d="M4 14h6v6H4z"/></svg>
  </div>
</div>

</div>

---
layout: default
---

# 3. The Harsh Reality: The Complications

Microfrontends don't *reduce* complexity. They **shift** and **organize** it.

<div class="grid grid-cols-2 gap-8 mt-8">

<div v-click>
  <h3 class="text-xl font-bold">🤯 Operational Complexity (DevOps)</h3>
  <ul class="mt-2 list-disc pl-5">
    <li>Managing <b>N</b> repositories and <b>N</b> CI/CD pipelines.</li>
    <li>Complex routing between the different "apps".</li>
    <li>Setting up the local development environment.</li>
  </ul>
</div>

<div v-click>
  <h3 class="text-xl font-bold">📦 The Dependency Drama</h3>
  <ul class="mt-2 list-disc pl-5">
    <li><b>Duplication</b>: each MFE downloads its own version of React, lodash, etc. Huge bundle sizes!</li>
    <li><b>Inconsistency</b>: App A uses React 17, App B uses React 18. Crash!</li>
    <li><b>Mono-repo?</b> It helps, but it doesn't magically solve these problems.</li>
  </ul>
</div>

<div v-click>
  <h3 class="text-xl font-bold">🎭 UX Inconsistency</h3>
  <ul class="mt-2 list-disc pl-5">
    <li>Different styles and behaviors across various parts.</li>
    <li>Requires strong governance (Design System).</li>
    <li>Layout Shifting during the loading process.</li>
  </ul>
</div>
</div>

---
layout: default
---

# 4. A Modern Solution: Module Federation

A feature introduced in Webpack 5 that changes the game.

<br>

**In simple terms:** it allows a JavaScript application to **dynamically load code from another application**... at **RUNTIME**.

<br>

<div class="grid grid-cols-2 gap-4">

<div>
  <h3 class="font-bold">Classic Approach (NPM Package)</h3>
  <ul class="list-disc pl-5 opacity-80">
    <li>Integration at <b>Build-time</b>.</li>
    <li>If the shared library changes, all consumers must be updated, rebuilt, and redeployed.</li>
    <li>Slow and cumbersome.</li>
  </ul>
</div>

<div>
  <h3 class="font-bold">Module Federation</h3>
  <ul class="list-disc pl-5 opacity-80">
    <li>Integration at <b>Run-time</b>.</li>
    <li>If the "remote" microfrontend changes, you only deploy that one. The "host" app will load it on the next refresh.</li>
    <li>Agile and flexible.</li>
  </ul>
</div>

</div>

---
layout: two-cols
---

## Hands-on: The Key Code

Let's see how a **Host** app loads a component from a **Remote** app.

::left::

### "Remote" App (localhost:3001)
Exposes its `Button` component.

```js {all|3-8|10-13}
// webpack.config.js
new ModuleFederationPlugin({
  name: 'remoteApp',
  filename: 'remoteEntry.js',
  exposes: {
    // We expose the Button component
    './Button': './src/Button',
  },
  shared: { react, 'react-dom' },
}),
