---
theme: apple-basic
background: false
title: why no microfrontends
highlighter: shiki
drawings:
  persist: false
transition: slide-left
---
---
src: ../shared/start.md
title: why no microfrontends
subtitle: todo subtitle
---
imported slide

---
src: ../shared/me.md
---
imported slide

---
class: text-center
---

# What is the microfrontends architecture?
<br>

<div class="text-xl" v-click.hide="2">
    
## ❝ An architectural style where <br>  independently deliverable <span v-mark.circle.white="1">frontend applications</span><br> are composed into a greater whole. ❞ <br>
### ~ Martin Fowler
</div>

<div class="text-xl" v-click.show="2">
    
❝ An architectural style where <br>  independently deliverable <span v-mark.circle.white="0">services</span> <br> are composed into a greater whole. ❞ <br>
</div>

---
class: text-center
---

### Basically it's
## Microservices, but for Frontend

---
title: Microservices vs Microfrontends
layout: two-cols
---

# Microservices

<br>
<v-click>

- One purpose service
</v-click>
<v-click at="3">

- Own database
</v-click>
<v-click at="5">

- Own deployment pipeline
</v-click>
<v-click at="7">

 - Own server / container
 </v-click>
<v-click at="9">

 - API contracts (OpenAPI) 
</v-click>
<v-click at="11">

 - Runtime invocation
 </v-click>

::right::

# Microfrontends

<br>
<v-click at="2">

 - One application/feature/component
</v-click>
<v-click at="4">

 - Own bundle
</v-click>
<v-click at="6">

 - Own deployment pipeline
</v-click>
<v-click at="8">

 - Own server / container
</v-click>
<v-click at="10">

 - Component contracts (TypeScript) 
</v-click>
<v-click at="12">

 - Runtime import
</v-click>

---
class: text-center
---

<div class="text-xl">
<div>

## Remember the microservices hype?
</div>

<div v-click class="mt-8">

### And then the "microservices are bad" backlash?
</div>

<div v-click class="mt-12 text-2xl">

# The same applies to microfrontends
</div>

<div v-click class="mt-8 text-green-400">

## You need the **right tool** for the **right context**
</div>
</div>

---
class: text-center
---

# When should you consider microfrontends?

<!-- Okay so, also based on the lessons we learned at Post, let's see when I can recommend it or when instead I would probably push you off of the idea to implement it -->

---
class: text-center
---

# Key factors to take in consideration

<div class="flex flex-row gap-8 mt-16">
<div v-click class="flex-1">

  ## Teams
  #### independent teams
</div>
<div v-click class="flex-1">

  ## Modules
  #### clear domain boundaries
</div>
<div v-click class="flex-1">

  ## Releases
  #### independent deployments
</div>
<div v-click class="flex-1">

  ## Reusability
  #### shared components
</div>
<div v-click class="flex-1">

  ## Technology
  #### flexibility
</div>
</div>


<!-- 
[click] Teams: how many teams will work on the frontend and how they are scoped 
[click] Modules: how many modules (applications, features or components) 
[click] Releases: how will the modules be released
[click] Reusability: how will the modules be reused across applications
 -->


---
hideInToc: true
class: text-center
---

# How many teams will be working on the frontend?

<div class="flex flex-row gap-8 mt-16">

<div class="flex-1">
  <div v-click>

  # One team
  </div>
  <div v-click class="text-red-400">
  Probably not worth
  </div>
</div>


<div class="flex-1">
  <div v-click>

  # More than one team
  </div>
  <div v-click class="text-amber-400">

  Well, it depends™️
  </div>
</div>

</div>


---
hideInToc: true
class: text-center
---

# How do you expect teams working on the modules?

<div class="flex flex-row gap-6 mt-16">


<div class="flex-1">
  <div v-click>

  # One team <br> per module
  </div>
  <div v-click class="text-green-400">
  Probably worth
  </div>
</div>

<div class="flex-1">
  <div v-click>

  # One team <br> on many modules
  </div>
  <div v-click class="text-red-400">
  Probably not worth
  </div>
</div>

</div>


---
hideInToc: true
class: text-center
---

# How do you expect to release your modules?

<div class="flex flex-row gap-8 mt-16">

<div class="flex-1">
  <div v-click>

  # All together
  </div>
  <div v-click class="text-red-400">
  Not worth
  </div>
</div>


<div class="flex-1">
  <div v-click>

  # Independently
  </div>
  <div v-click class="text-green-400">

  Probably worth
  </div>
</div>

</div>


---
class: text-center
---

# Do you need your modules to be shared across applications?

<div class="flex flex-row gap-8 mt-16">

<div class="flex-1">
  <div v-click>

  # No
  </div>
  <div v-click class="text-red-400">

  Probably not worth
  </div>
</div>

<div class="flex-1">
  <div v-click>

  # Yes
  </div>
  <div v-click class="text-amber-400">

  Well, it depends™️
  </div>
</div>

</div>

---
class: text-center
---

# The hidden costs of microfrontends

<div class="flex flex-row gap-6 mt-16">

<div class="flex-1">
  <div v-click>

  ## Performance
  #### duplicate dependencies
  </div>
</div>

<div class="flex-1">
  <div v-click>

  ## Complexity
  #### distributed debugging
  </div>
</div>

<div class="flex-1">
  <div v-click>

  ## Governance
  #### inconsistent UX
  </div>
</div>

<div class="flex-1">
  <div v-click>

  ## Overhead
  #### coordination burden
  </div>
</div>
    
<div class="flex-1">
  <div v-click>

  #### .. and more
  ### *the books don't tell you*
  </div>
</div>

</div>

<!-- mention that performance is main goal of module federation -->
<!-- mention that debugging is still one of our biggest problems -->

---
class: text-center
---

# Problem 1: how do we ensure type safety?

<div class="flex flex-col gap-4 text-left">

<div v-click>
        
### Problem
Runtime imports = No compile-time type checking
</div>

<div v-click>

### Solution
**Dual-mode approach:**
- **Runtime**: Load ESM bundles from remote server (Module Federation)
- **Compile-time**: Install npm package with **only `.d.ts` files**
</div>

<div v-click class="text-green-400">

## Benefits
✓ Type checking during development
✓ IDE autocomplete and IntelliSense
✓ Independent runtime deployments
</div>

</div>

<!-- if we have runtime imports, it means we dont have typescript at compile time -->

---
class: text-center
---

# how do we effectively do microfrontends

<div class="flex flex-col gap-4 mt-12 text-left text-lg">
    
<ul>
<li v-click="1"><span v-mark.strike.white="6"><strong>iframes</strong> - Isolated contexts</span></li>
<li v-click="2"><span v-mark.strike.white="7"><strong>web components</strong> - Custom elements</span></li>
<li v-click="3"><span v-mark.strike.white="8"><strong>SPAs</strong> - Runtime loading</span></li>
<li v-click="4"><span v-mark.circle.white="9"><strong>Module Federation / Import maps</strong> - Dynamic imports</span></li>
</ul>
</div>

<div v-click="5" class="mt-4 text-xl text-green-400">

**Key:** Runtime invocation ensures independent deployability
</div>

