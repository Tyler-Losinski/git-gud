<script>
  import '../app.css'
  import '../prism.css'
  import MoonIcon from 'heroicons-svelte/solid/MoonIcon.svelte'
  import SunIcon from 'heroicons-svelte/solid/SunIcon.svelte'
  import { browser } from '$app/environment'
  import { inject } from '@vercel/analytics'

  inject();//analytics for vercel

  let isDarkMode = browser ? Boolean(document.documentElement.classList.contains('dark')) : true

  function disableTransitionsTemporarily() {
    document.documentElement.classList.add('[&_*]:!transition-none')
    window.setTimeout(() => {
      document.documentElement.classList.remove('[&_*]:!transition-none')
    }, 0)
  }
</script>

<link
  href="https://fonts.googleapis.com/css?family=Open+Sans:300,400,500,600,700&amp;amp;subset=cyrillic"
  rel="stylesheet"
/>

<div class="body">
  <header class="flex items-center justify-between w-full max-w-2xl py-4 mx-auto lg:pb-8">
    <button
      type="button"
      role="switch"
      aria-label="Toggle Dark Mode"
      aria-checked={isDarkMode}
      class="w-5 h-5 sm:h-8 sm:w-8 sm:p-1"
      on:click={() => {
        isDarkMode = !isDarkMode
        localStorage.setItem('isDarkMode', isDarkMode.toString())

        disableTransitionsTemporarily()

        if (isDarkMode) {
          document.querySelector('html').classList.add('dark')
        } else {
          document.querySelector('html').classList.remove('dark')
        }
      }}
    >
      <MoonIcon class="hidden text-zinc-500 dark:block" />
      <SunIcon class="block text-zinc-400 dark:hidden" />
    </button>
    <a id="question" href="/blog">help</a>
  </header>
  <a id="answer" class="text-zinc-900 dark:text-white" href="#" target="_blank" title="NO"
    >Git Gud</a
  >
</div>

<style type="text/css">
  html,
  .body {
    height: 100%;
    width: 100%;
  }
  .body {
    text-align: center;
  }

  a#answer {
    display: inline-block;
    margin-top: 200px;
    font-weight: bold;
    font-size: 120pt;
    font-family: Arial, sans-serif;
    text-decoration: none;
    cursor: default;
  }
</style>
