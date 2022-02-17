<script >
  import { fly } from 'svelte/transition';
  import { fade } from 'svelte/transition';
  import Hamburger from '$lib/assets/hamburger.svelte';
  import MediaQuery from "svelte-media-query";
  import OutClick from 'svelte-outclick'

  export let open = false
  export let onClick = () => {
    open = !open
  }
</script>

{#if open}
<div class="overlay z-10" transition:fade={{duration: 400}}></div>
{/if}

<header class="text-gray-600 body-font z-20">
  <div class="container mx-auto flex flex-wrap p-5 flex-row items-center justify-between"> 

    <!-- LOGO -->
    <a class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0 z-20">
      <span class="ml-3 text-6xl">L.</span>
    </a>

    <!-- LINKS NAVBAR -->
    <MediaQuery query="(min-width: 768px)" let:matches>
      {#if matches}
        <nav class="md:ml-auto flex flex-wrap items-center text-base justify-center">
          <a class="mr-5 hover:text-gray-900">Sobre Mi</a>
          <a class="mr-5 hover:text-gray-900">Proyectos</a>
          <a class="mr-5 hover:text-gray-900">In</a>
        </nav>
      {/if}
    </MediaQuery>

    <!-- BURGUER ICON -->
    <!-- LINKS MENU BURGER -->
    <MediaQuery query="(max-width: 768px)" let:matches>
    {#if matches}
    {#if open}
      <nav class="flex flex-wrap flex-col items-center text-base justify-center absolute inset-0 text-5xl uppercase z-20" >
          <a class="hover:text-gray-900 py-16 menuLinks" transition:fly={{ y: -500, duration: 600 }}>Sobre Mi</a>
          <a class="hover:text-gray-900 py-16 menuLinks2" transition:fly={{ y: -450, duration: 550 }}>Proyectos</a>
          <a class="hover:text-gray-900 py-16 menuLinks3" transition:fly={{ y: -400, duration: 500 }}>In</a>
      </nav>
    {/if}

    <OutClick on:outclick={() => open = false} excludeByQuerySelector={['.menuLinks', '.menuLinks2', '.menuLinks3']} useWrapper={true}>
      <Hamburger {open} {onClick} />
    </OutClick>

    {/if}
    </MediaQuery>

  </div>
</header>

<style lang="scss">
  .overlay{
    position: absolute;
    width: 100vw;
    height: 100vh;
    background: linear-gradient(180deg, #FFC8C8 0%, #F9FFB9 18.23%, #BEFFB9 34.9%, #C6FFFC 55.73%, #E3C0FF 76.56%, #FFD2ED 94.79%);
    overflow: hidden;
  }
</style>