---
theme: apple-basic
background: false
title: come with vim in the rabbit-hole :q
highlighter: shiki
drawings:
  persist: false
transition: slide-left

---
---
src: ../shared/start.md
title: why no microfrontend
subtitle: Let's dispel the myth that Vim is only for "elite" programmers.
---
imported slide

---
src: ../shared/me.md
---
imported slide

---

<h1>what is this talk about</h1>
<div grid="~ cols-2 gap-2 justify-items-center items-center" class="h-100">
<div>
<br>
it's ugly and scary <img src = "/assets/images/scary.svg" alt="scary" class="inline w-6"/>

today we are <strong>not</strong> gonna speak about this

but about what makes vim <strong>efficient</strong> and <strong>natural</strong>

**modal editing** and his **natural language**
</div>

<div class="relative">
<img
  src="/assets/images/vim.png"
  alt="lt"
  border="rounded"
/>
<img src = "/assets/images/scary.svg" alt="scary" class="w-10 absolute bottom-0 right-0 mr-2 mb-2"/>
</div>
</div>


<!--
we are not gonna speak about the "program" but about the editor mordal
-->

---

<h1>what is this talk about</h1>

<div class="flex flex-col gap-2 items-center justify-center text-align-center">
<img
  src="/assets/images/apps.webp"
  class="w-120"
  alt="lt"
  border="rounded"
/>

<h3>are you aware that these programs can have vim enabled?</h3>
</div>

--- 

<h1>the keyboard is our brush</h1>

<div grid="~ cols-2 gap-2 justify-items-center items-center" m="t-2">
<div class="leading-8 opacity-80">
developers are like <strong>artists</strong>

artists don't press <strong>constantly</strong> the brush to the canvas

they <strong>think</strong>, they <strong>look</strong>, they <strong>move</strong>, and sometimes they draw a line

why use the keyboards only to write <strong>code</strong>

when most of our time is passed navigating the <strong>code</strong>

<i text=!2xl>the keyboard is our <strong>brush</strong></i>

</div>

<img src="https://www.sspaeti.com/blog/why-using-neovim-data-engineer-and-writer-2023/weel-too-busy.png" class="rounded-full w-80"/>
</div>

---
layout: center
---

<h1 text="!6xl">quiz time</h1>

<!-- claper todo -->
---

<h1>vim grammar - verbs (operators)</h1>

<div>
Just as spoken language grammar has <strong>verbs</strong>, <strong>adjectives</strong> and <strong>subjects</strong>, so does the vim grammar.

The grammar has different <strong>verbs</strong> to begin with:

<ul>
<li>Copying (or <strong>y</strong>anking) in Vim with <strong>y</strong></li>
<li><strong>d</strong>eleting with <strong>d</strong></li>
<li><strong>p</strong>asting with <strong>p</strong></li>
<li><strong>c</strong>hanging with <strong>c</strong></li>
<li><strong>f</strong>finding with <strong>f</strong></li>
<li>..more</li>
</ul>

<strong>Verbs</strong> can do nothing alone, they need a followup, a <strong>subject</strong>.
</div>

---

<h1>vim grammar - subjects (motions)</h1>

<div>
Next, we can add motions. Each <strong>verb</strong> takes a <strong>subject</strong> for their action. 

<ul>
<li>numbers</li>
<li><strong>w</strong>ords</li>
<li><strong>b</strong>back - beginning of previous word</li>
<li>..more</li>
</ul>
</div>

--- 

<h1>vim grammar - adjectives and count</h1>

<div>
The count allows you to multiply the effect of your <strong>verb</strong> a count number of times.

the adjectives is inner and around tbd
</div>

---

<h1>vim grammar - composability</h1>

{verb}{count}{adjective}{subject} => {operator}{count}{adjective}{motion}
{count}{verb}{adjective}{subject} => {count}{operator}kadjective}{motion}

---

Most commands come in two, three or four parts. One version of the three-part structure goes like this: operator — text object — motion.

**Operators** are always one of ***d**elete*, ***c**hange*, ***v**isual select* and ***r**eplace*.

**Text objects** are always one of **i**nside* or ***a**round*.

There’s a ton of different motions but we’ll get into that in a second, for now we can think of the motion as a kind of target for the command. To take an example I could press dib, meaning delete inside block.

The operator is delete, the text object is inside and the motion is block. This deletes everything inside a block of (parentheses).

<!-- mention the abscence of "shortcuts" -->

--- 

<h1>modal editing</h1>

what is modal editor

**Normal** mode is for reading code and navigating quickly.
**Insert** mode is for when you want to add some code or text.
**Visual** mode is unique, the same as highlighting text with the mouse, but with the above Vim motions.

---
layout: center
---

<h1 text="!6xl">modal editing demo time</h1>


---

<h1>text-objects</h1>

````md magic-move
```ts
const text = "some words";
```
```ts
const text = "some words";
```
```ts 
const text = ""; 
```
````

<div v-click="1">di"</div>
di’ —delete inside the ‘single quotes’.

---

<h1>text-objects</h1>

````md magic-move {at:2, lines: true}
```html {*|1,3}
<div>
    <p>some text</p>
</div>
```

cstsection
```html {*}{lines: false}
<section>
    <p>some text</p>
</section>
```
```html {*|2}
<section>
    <p>some text</p>
</section>
```

dst
```html
<section>
    some text
</section>
```

citvim
```html
<section>
    vim
</section>
```
````

<div v-click="2">cstsection</div>
<div v-click="5">dst</div>
<div v-click="7">citvim</div>

---

<h1>it gamifies coding</h1>

sometime the job is boring

---

<h1 text="!6xl">macro demo time</h1>

<!-- show live action of a macro, using registers, for a repetive action -->
---

<h1>extra mile</h1>

show pics of 

dap
lsp
ai
preview
taks runner etc

---

<h1>References</h1>

[why-vim-is-better-than-vscode-d09e2355eb37](https://sean-warman.medium.com/why-vim-is-better-than-vscode-d09e2355eb37)
[vim-language-and-motions-explained](https://www.freecodecamp.org/news/vim-language-and-motions-explained/)
[editing-like-magic-with-vim-operators](https://www.barbarianmeetscoding.com/boost-your-coding-fu-with-vscode-and-vim/editing-like-magic-with-vim-operators)

[GitHub](https://github.com/lucax88x/slides)
