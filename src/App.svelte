<script lang="ts">
  import Pong from './routes/pong.svelte'
  import Pixi from './routes/pixi.svelte'
</script>

{#if window.location.pathname === '/'}
  <Pong />
{:else if window.location.pathname === '/pong'}
  <Pixi />
{:else}
  404
{/if}

<style lang="sass">
  :global(body)
    margin: 0px
    font-family: Arial, Helvetica, sans-serif
    font-size: 18px
    background-color: #000000
    color: #f2f2f2
    text-align: center
    min-height: 100%
</style>
