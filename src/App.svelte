<script lang="ts">
  import Pong from './pong.svelte'
  import Phaser from './phaser/phaser.svelte'

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
  <Phaser />
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
