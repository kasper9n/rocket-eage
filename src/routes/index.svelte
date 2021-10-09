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
  $: maxX = 1000 - boxX / 2
  $: minX = 0 + boxX / 2
  $: maxY = 500 - boxY / 2
  function limit() {
    if (x > maxX) x = 1000 - boxX / 2
    if (x < minX) x = 0 + boxX / 2
    if (y > maxY) y = maxY
    if (y < 0 + boxY / 2) y = 0 + boxY / 2
  }
  function keypress(e: KeyboardEvent) {
    if (e.key === 's') setPos(x, y + 10)
    if (e.key === 'w') setPos(x, y - 10)
    if (e.key === 'd') setPos(x + 10, y)
    if (e.key === 'a') setPos(x - 10, y)
  }
  let movePerMillisecond = 0.5
  let last = Date.now()
  let movingRight = true
  onMount(() => {
    function step() {
      let now = Date.now()
      let difference = now - last
      if (movingRight === true) {
        x += movePerMillisecond * difference
        if (x > maxX) {
          movingRight = false
          x = maxX - (x - maxX)
        }
      } else {
        x -= movePerMillisecond * difference
        if (x < minX) {
          movingRight = true
          x = minX + (minX - x)
        }
      }
      window.requestAnimationFrame(step)
      last = now
    }
    window.requestAnimationFrame(step)
  })
  let sliderValue = 20
  function sliderChange(newValue: number) {
    boxX = newValue
    boxY = newValue
    limit()
  }
  $: sliderChange(sliderValue)
</script>

<svelte:window on:keypress={keypress} />

<input type="range" min="1" max="400" bind:value={sliderValue} />
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
