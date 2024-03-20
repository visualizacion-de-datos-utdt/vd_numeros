<script>
  import {onMount} from "svelte"
  import * as d3 from "d3"

  let numbers = [10, 25, 30, 60, 70, 100]
  let pathLength
  let largo

  onMount(() => {
    // @ts-ignore
    // longitud total del path
    pathLength = document.querySelector("#path").getTotalLength()
    // longitud total del path
    let maxGap = pathLength - pathLength * numbers[0] / 100
    let minGap = 0

    // console.log("total path", pathLength)
    // console.log("maximo gap", maxGap)
    // console.log("minimo gap", maxGap)

    largo = function (n) {
      let scale = d3
        .scaleLinear()
        .domain(d3.extent(numbers)) // extent returns [min, max]
        .range([maxGap, minGap])
      return scale(n)
    }

  })
</script>

{#each numbers as n}
<svg width="100" height="100">
  <!-- Corazón gris -->
  <path
  id="path"
  d="M 10,30
  A 20,20 0,0,1 50,30
  A 20,20 0,0,1 90,30
  Q 90,60 50,90
  Q 10,60 10,30 z" 
  fill="none"
  stroke="#ccc"
  stroke-width="10"
  />
  <!-- Corazón rojo -->
  {#if pathLength}
  <path
    id="path"
    d="M 10,30
    A 20,20 0,0,1 50,30
    A 20,20 0,0,1 90,30
    Q 90,60 50,90
    Q 10,60 10,30 z" 
    fill="none"
    stroke="red"
    stroke-width="10"
    stroke-dasharray="{pathLength}"
    stroke-dashoffset="{largo(n)}"
  />
  {/if}
</svg>{/each}



