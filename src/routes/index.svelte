<script lang="ts">
  import { onMount } from 'svelte'

  let x = 0
  let y = 0
  let boxX = 20
  let boxY = 20
  onMount(() => {
    x = window.innerWidth / 2
    y = window.innerHeight / 2
  })
  function setPos(newX: number, newY: number) {
    x = newX
    y = newY
    limit()
  }
  function limit() {
    if (x > 1000 - boxX / 2) x = 1000 - boxX / 2
    if (x < 0 + boxX / 2) x = 0 + boxX / 2
    if (y > 500 - boxY / 2) y = 500 - boxY / 2
    if (y < 0 + boxY / 2) y = 0 + boxY / 2
  }
  function keypress(e: KeyboardEvent) {
    if (e.key === 's') setPos(x, y + 10)
    if (e.key === 'w') setPos(x, y - 10)
    if (e.key === 'd') setPos(x + 10, y)
    if (e.key === 'a') setPos(x - 10, y)
  }
  let sliderValue = 20
  function sliderChange(newValue: number) {
    boxX = newValue
    boxY = newValue
    limit()
  }
  $: sliderChange(sliderValue)
</script>

<svelte:window on:keypress={keypress} />

<input type="range" min="1" max="499" bind:value={sliderValue} />
<div class="game">
  <div class="box" style="left: {x}px; top: {y}px; width: {boxX}px; height: {boxY}px;" />
</div>

<style lang="sass">
  :global(body)
    margin: 100px 0px
    font-family: Arial, Helvetica, sans-serif
    font-size: 18px
    background-color: #000000
    color: #f2f2f2
    text-align: center
  :global(body)
    display: flex
    justify-content: center
  .game
    border: 1px solid #f2f2f2
    width: 1000px
    height: 500px
    overflow: hidden
    position: relative
    background-color: #181616
  .box
    position: absolute
    transform: translate(-50%, -50%)
    background-color: #1b0896
</style>
