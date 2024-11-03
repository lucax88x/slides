---
theme: apple-basic
background: false
title: microfrontend
highlighter: shiki
drawings:
  persist: false
transition: slide-left

---

<div class="flex flex-col gap-2 h-full">
<div class="flex flex-col gap-2 items-center justify-center h-full">
<h1 text="!5xl">microfrontend</h1>

<div class="text-sm opacity-50">why and when it can be useful, a real usecase</div>
<div text="!2xl">lucatrazzi</div>
</div>

<div class="text-align-right">
<div><strong>adesso</strong> <strong>@lugano</strong></div>
<div class="text-sm opacity-50">06/08/2024</div>
</div>
</div>

---

<h1>micro-frontend</h1>

<div class="flex flex-col items-center gap-2">
<img src="/assets/images/architecture.webp" alt="arch" class="w-120"></img>

<i class="text-center">
enhanced flexibility and scalability, empowering developers to construct, test, and deploy each micro frontend independently.
</i>
</div>

<!--
enhanced flexibility and scalability, empowering developers to construct, test, and deploy each micro frontend independently.
-->

---

<h1>what is good</h1>

<div>

<ul>
<li>isolation</li>
<li>separate ci/cd with separate deployment times</li>
<li>team/stream autonomy</li>
<li>technology flexibility</li>
<li>better scalability</li>
<li>isolated failures</li>
</ul>

</div>

<!--

4. Reusability:
[Micro FrontEnd]: It will make the Test suite also reusable. We just need to test once.

[Monolithic FrontEnd]: We might have to run the test suite redundantly. If we are working with different teams, then test cases
would be redundant.

5. Continuous Integration/Deployment:
[Micro FrontEnd]: Each micro frontend can be developed and deployed
independently, it’s possible to set up a CI/CD pipeline for each micro frontend, allowing for faster development cycles and less downtime when deploying new features.

[Monolithic FrontEnd]: If something wrong will go in production and we want to roll back the commit. As CI/CD time would be more so total
downtime of the application would also be more, which might
lead to heavy revenue loss.
-->

---

<h1>it's not all sunshines and roses</h1>

<div>

<ul>
<li>increased complexity in setup and coordination</li>
<li>overhead in build/deployment</li>
<li>potential performance issues</li>
<li>consistency challenges (ui/ux)</li>
<li>complexity in testing and debugging</li>
</ul>

</div>

---

<div class="flex flex-col h-full gap-2 justify-center">
<center v-click>
<strong text="!3xl">TLDR</strong>
</center>

<center v-click>
<strong text="!3xl">CONs largely outweight PROs for 90% use cases</strong>
</center>

<center v-click>
<strong text="!3xl">however</strong>
</center>

<center v-click>
<strong text="!3xl">there's still a 10% when it's worth</strong>
</center>
</div>

---

<h1>federation</h1>

TBD

---

<h1>real example</h1>

<ul>
<li>ui components</li>
<li>shells
<ul>
<li>shell 1..n</li>
</ul>
</li>

<li>modules
<ul>
<li>react 1</li>
<li>angular 2</li>
</ul>
</li>

<li>shared
<ul>
<li>react 1</li>
<li>angular 2</li>
</ul>
</li>

</ul>

---

<h1>References</h1>

[The Testing Dilemma in Micro Frontend Architecture: Pros and Cons Discussed
](https://blog.bitsrc.io/the-testing-dilemma-in-micro-frontend-architecture-pros-and-cons-discussed-8cf9a6a90c3d)

[GitHub](https://github.com/lucax88x/slides)
