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
