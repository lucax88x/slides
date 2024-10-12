---
theme: seriph
background: false
title: come with vim in the rabbit-hole :q
info: todo
class: text-center
highlighter: shiki
drawings:
  persist: false
transition: slide-left

---

# whoami

@lucatrazzi

- works at @adesso schweiz ag in Lugano
- lives in italy
- husband and proud father of 2 kids
- loves to code

<div grid="~ cols-2 gap-2" m="t-2">
    <img
      src="/assets/images/photo.jpg"
      alt="lt"
      border="rounded"
    />
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# what - is this talk about


<img
  src="/assets/images/vim.png"
  alt="lt"
  border="rounded"
/>

it's a text editor

and it's ugly and scary :scary-face:

today we are not gonna speak about this

but about what makes vim efficient and natural

**modal editing**

<!--
we are not gonna speak about the "program" but about the editor mordal
-->

---

# what - is this talk about

(pic of intellij, vscode, chrome, zathura, obsidian)

are you aware that these programs can have vim enabled?

--- 

# the keyboard is our brush

developers are like artists.

artists don't press constantly the brush to the canvas.

they think, they look, they move, and sometimes they draw a line, or a hue.

the keyboard is our **brush**.

it's a waste to use the keyboards only to draw lines, 

when most of our time is passed navigating the code.

---

# video time

<div class="flex justify-center">
  <video width="640" height="360" controls>
    <source src="/assets/videos/quiz.mp4" type="video/mp4">
  </video>
</div>

---
layout: center
---

# quiz time

---

# modal editing

what is modal editor

normal
visual

https://www.freecodecamp.org/news/vim-language-and-motions-explained/

Vim Grammar
Just as spoken language grammar has verbs, subjects, and objects, so does the Vim language. The grammar has different verbs to begin with. Copying (or yanking) in Vim with y, deleting with d, pasting with p, changing with c, and so on.

---

# it gamifies coding

sometime the job is boring

---

# gamification

Most commands come in two, three or four parts. One version of the three-part structure goes like this: operator — text object — motion.

**Operators** are always one of ***d**elete*, ***c**hange*, ***v**isual select* and ***r**eplace*.

**Text objects** are always one of **i**nside* or ***a**round*.

There’s a ton of different motions but we’ll get into that in a second, for now we can think of the motion as a kind of target for the command. To take an example I could press dib, meaning delete inside block.

The operator is delete, the text object is inside and the motion is block. This deletes everything inside a block of (parentheses).

--- 

# text-objects

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

# text-objects

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

# extra mile

dap
lsp
ai
preview
taks runner etc

---

# References

[sean warman](https://sean-warman.medium.com/why-vim-is-better-than-vscode-d09e2355eb37)

[GitHub](https://github.com/lucax88x/slides)
