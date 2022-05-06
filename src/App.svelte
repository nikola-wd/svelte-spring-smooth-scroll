<script>
  import { spring } from 'svelte/motion';
  import Text from './lib/Text.svelte'

  let height = 0;
  let scrolled = spring(0);

  $: document.body.style.height = `${height}px`

  const handleScroll = (e) => {
    console.log(e)
    scrolled.set(window.pageYOffset || window.scrollTop || 0)
  }
</script>

<svelte:window 
  on:scroll={handleScroll} 
/>

<div class="wrap">
  <div class="inner" bind:clientHeight={height} style="transform: translateY({-$scrolled}px)">
    {height}<br />
    {$scrolled}
    <Text />
  </div>
</div>


<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  * {
	box-sizing: border-box;
}

:global(body) {
	box-shadow: 0 0 0 1px red;
}

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

 .wrap {
    position: fixed;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    overflow: hidden;
  }

  .inner {
    --scrollPos: 0;
    position: relative;
    transform: translateY(calc(var(--scrollPos, 0) * 1px));
  }

</style>
