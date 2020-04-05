<script>
  import { tweened } from "svelte/motion"
  import { elasticOut } from "svelte/easing"
  export let height = 70,
    width = 250,
    amount = 10,
    duration = 500,
    gluten = false,
    barlow = false,
    mutator = false
  let bulge = false,
    w = width * 2,
    h = height * 2,
    minWeight,
    maxWeight,
    minWidth,
    maxWidth,
    show = false

  const top = tweened(0, { duration, easing: elasticOut })
  const left = tweened(0, { duration, easing: elasticOut })
  const bottom = tweened(h, { duration, easing: elasticOut })
  const right = tweened(w, { duration, easing: elasticOut })
  const fontWidth = tweened(minWidth, { duration, easing: elasticOut })
  const fontWeight = tweened(minWeight, { duration, easing: elasticOut })

  $: if (gluten) {
    minWidth = 100
    maxWidth = 100
    minWeight = 150
    maxWeight = 450
  }
  $: if (barlow) {
    minWidth = 50
    maxWidth = 450
    minWeight = 50
    maxWeight = 450
  }
  $: if (mutator) {
    minWidth = 20
    maxWidth = 500
    minWeight = 250
    maxWeight = 20
  }

  $: bulge
    ? (top.set(0 - amount),
      left.set(0 - amount),
      bottom.set(h + amount),
      right.set(w + amount),
      fontWidth.set(maxWidth),
      fontWeight.set(maxWeight))
    : (top.set(0),
      left.set(0),
      bottom.set(h),
      right.set(w),
      fontWidth.set(minWidth),
      fontWeight.set(minWeight))
</script>

<button
  on:click
  on:touchstart={() => (bulge = true)}
  on:touchend={() => (bulge = false)}
  on:mousedown={() => (bulge = true)}
  on:mouseup={() => (bulge = false)}
  on:keydown={e => (e.code == 'Space'? bulge = true : '')}
  on:keyup={e => (e.code == 'Space'? bulge = false : '')}
  on:mouseleave={() => (bulge = false)}>

  <span class:gluten class:barlow class:mutator style="font-variation-settings: 'wght' {$fontWeight}, 'wdth' {$fontWidth};"><slot></slot></span>
  <svg aria-hidden="true" viewbox="0 0 {w} {h}">
    <path
      d=" M 0 0 Q {width}
      {$top}
      {w} 0 Q {$right}
      {height}
      {w}
      {h} Q {width}
      {$bottom} 0 {h} Q {$left}
      {height} 0 0 Z" />
  </svg>
</button>
{#if show}
  <span class="focus-visible"><svg></svg></span>
{/if}
<style>
  button {
    position: relative;
    background: transparent;
    border: none;
    height: 70px;
    width: 250px;
    cursor: pointer;
    background-color: transparent;
    color: var(--color);
    font-weight: bold;
    font-size: 2rem;
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -webkit-tap-highlight-color: transparent;
  }
  button:hover {
    background-color: transparent;
    color: var(--color-hover);
  }
  button svg {
    fill: var(--bg-color);
    stroke: var(--border-color);
    stroke-width: var(--border-width);
  }
  button:hover svg {
    fill: var(--bg-color-hover);
    stroke: var(--border-color-hover);
  }
  button:active svg {
    fill: var(--bg-color-active);
    stroke: var(--border-color-active);
  }
  button:active {
    background-color: transparent;
    color: var(--color-hover);
  }
  span {
    display: block;
    position: relative;
    z-index: 1
  }
  span.gluten {
    font-family: "Gluten";
    letter-spacing: 2px;
  }
  span.mutator {
    font-family: "Mutator";
  }
  span.barlow {
    font-family: "Barlow";
    letter-spacing: 3px;
  }

  svg {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 0;
    width: 100%;
    height: auto;
    overflow: visible;
    transition: all 0.3s ease-out;
  }

  .focus-visible svg {
    box-shadow: 0 0 0px 4px rgb(111, 173, 240) !important;
    stroke: white;
    stroke-width: 3px;
  }
</style>
