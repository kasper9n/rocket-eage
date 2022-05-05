<script lang="ts">
  import Pong from './routes/pong.svelte'
  import Pixi from './routes/pixi.svelte'

  let loading = true
  let loadingText = 'Loading'
  setInterval(() => {
    if (loadingText === 'Loading...') {
      loading = false
    }
    loadingText += '.'
  }, 100)
</script>

{#if loading}
  <p>{loadingText}</p>
{:else if window.location.pathname === '/'}
  <Pixi />
{:else if window.location.pathname === '/pong'}
  <Pong />
{:else}
  404
{/if}

<style lang="sass">
  p
    margin: auto
    text-align: left
    width: 70px
</style>
