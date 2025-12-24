<div class="flex flex-col gap-2 h-full">
<div class="flex flex-col gap-2 items-center justify-center h-full">
<h1 text="!5xl">{{ $frontmatter.title }}</h1>

<div class="text-sm opacity-50">{{ $frontmatter.subtitle }}</div>
<div text="!2xl">lucatrazzi</div>
</div>

<div class="text-align-right">
<div><strong>voxxed</strong> days <strong>@lugano</strong></div>
<div class="text-sm opacity-50">{{ new Date().toLocaleDateString('en-GB') }}</div>
</div>
</div>

