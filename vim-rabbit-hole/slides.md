---
theme: apple-basic
background: false
title: come with vim in the rabbit-hole :q
info: todo
highlighter: shiki
drawings:
  persist: false
transition: slide-left
layout: intro

---

<h1 text="!4xl">come with vim in the rabbit hole! :q</h1>

<div>Curious about Vim's reputation as a powerful editor? <br>
Join me for a hands-on exploration of modal editing. <br>
We'll break down the intuitive concepts, test your knowledge with a quiz, and witness the magic of Vim in action.<br>
<strong>Let's dispel the myth that Vim is only for "elite" programmers.</strong>
</div>

---

<h1 text="!5xl">luca trazzi</h1>

<div grid="~ cols-2 gap-2 justify-items-center items-center" m="t-2">
<div class="leading-8 opacity-80">
works at @adesso schweiz at in lugano<br>
husband and proud father of 2 kids<br>
loves to dance with the code<br>
</div>

<img src="/assets/images/photo.jpg" class="rounded-full w-40"/>
</div>

---

<h1>what - is this talk about</h1>
<div grid="~ cols-2 gap-2 justify-items-center items-center" m="t-2">
<div>
it's a text editor

and it's ugly and scary :scary-face:

today we are not gonna speak about this

but about what makes vim efficient and natural

**modal editing** and his **natural language**
</div>

<img
  src="/assets/images/vim.png"
  alt="lt"
  border="rounded"
/>
</div>


<!--
we are not gonna speak about the "program" but about the editor mordal
-->

---

<h1>what - is this talk about</h1>

(pic of intellij, vscode, chrome, zathura, obsidian)

are you aware that these programs can have vim enabled?

--- 

<h1>the keyboard is our brush</h1>

developers are like artists.

artists don't press constantly the brush to the canvas.

they think, they look, they move, and sometimes they draw a line, or a hue.

the keyboard is our **brush**.

it's a waste to use the keyboards only to draw lines, 

when most of our time is passed navigating the code.

<img src="https://www.sspaeti.com/blog/why-using-neovim-data-engineer-and-writer-2023/weel-too-busy.png" class="w-40"/>


---

<h1>video time</h1>

<div class="flex justify-center">
  <video width="640" height="360" controls>
    <source src="/assets/videos/quiz.mp4" type="video/mp4">
  </video>
</div>

---
layout: center
---

<h1>quiz time</h1>

---


<h1>vim grammar</h1>

Just as spoken language grammar has **verbs**, **subjects**, and **objects**, so does the Vim grammar.

https://www.freecodecamp.org/news/vim-language-and-motions-explained/

Most commands come in two, three or four parts. One version of the three-part structure goes like this: operator — text object — motion.

**Operators** are always one of ***d**elete*, ***c**hange*, ***v**isual select* and ***r**eplace*.

**Text objects** are always one of **i**nside* or ***a**round*.

There’s a ton of different motions but we’ll get into that in a second, for now we can think of the motion as a kind of target for the command. To take an example I could press dib, meaning delete inside block.

The operator is delete, the text object is inside and the motion is block. This deletes everything inside a block of (parentheses).

--- 

<h1>modal editing</h1>

what is modal editor

**Normal** mode is for reading code and navigating quickly.
**Insert** mode is for when you want to add some code or text.
**Visual** mode is unique, the same as highlighting text with the mouse, but with the above Vim motions.

---

<h1>it gamifies coding</h1>

sometime the job is boring

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

<h1>the macro demo</h1>

show live action of a macro, using registers, for a repetive action

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

[GitHub](https://github.com/lucax88x/slides)
