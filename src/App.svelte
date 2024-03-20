<script>

  import * as d3 from "d3"
  import Waffle from "./lib/Waffle.svelte"
  import IrregularPath from "./lib/IrregularPath.svelte"
  import CoffeColumns from "./lib/CoffeColumns.svelte"

  let numbers = [5, 18, 29, 37, 75]
  let numbersDivided5 = numbers.map(n => Math.floor(n / 5))


  function altura(n) {
    let scale = d3
      .scaleLinear()
      .domain(d3.extent(numbers)) // extent returns [min, max]
      .range([15, 225])
    return scale(n)
  }

  function arcGenerator({startAngle, endAngle, innerRadius, outerRadius}) {
    return d3.arc()({
      startAngle,
      endAngle,
      innerRadius,
      outerRadius,
    })
  }


</script>

<main>
  
  <!-- 1. Canal: altura. Tipo: col con divs -->
  <h3 class="headline">Canal: altura. Tipo: columnas</h3>
  <CoffeColumns />

  <!-- 1. Canal: altura. Tipo: col con divs -->
  <h3 class="headline">Canal: longitud (path irregular)</h3>
  <IrregularPath />
  <hr>


  <!-- Canal: altura -->
  <h3 class="headline">Set magnitudes. Canal: longitud</h3>
  <div class="iso__container-big">
    {#each numbers as n}
      <img
        style="height: {altura(n)}px; padding: 10px"
        src="/images/person.png"
        alt="person"
      />
    {/each}
  </div>

  <!-- Canal: longitud. Type: Isotype Chart  -->
  <h3 class="headline">
    Set magnitudes. Canal: longitud. Tipo: gráfco Isotype
  </h3>

  <div class="iso__container-iso">
    {#each numbersDivided5 as n, index}
      <div class="row">
        {#each Array(n) as m}
          <img
            style="height: 50px; padding: 2px"
            src="/images/person.png"
            alt="person"
          />
        {/each}
        <p>{numbers[index]}</p>
      </div>
    {/each}

    <!-- Waffle - Canal: área -->
    <h3 class="headline">Set magnitudes. Canal: área. Tipo: gráfco waffle</h3>
    <div class="waffle__container">
      {#each numbers as n}
        <Waffle n={n} />
      {/each}
    </div>
  </div>

  <!-- Draw svg arc -->
  <h3 class="headline">Set magnitudes. Canal: longitud. Tipo: gráfco arco</h3>
  <svg width="300" height="300">
    <path
      d={arcGenerator({
        startAngle: 0,
        endAngle: Math.PI / 2,
        innerRadius: 0,
        outerRadius: 100,
      })}
      fill="black"
      stroke="black"
      stroke-width="3"
      transform="translate(150, 150)"
    />
  </svg>

    <!-- ISOTYPE - Canal: altura -->
    <h3 class="headline">Dos magnitudes. Canal: longitud</h3>
    <div class="iso__container">
      <img style="height: 75px" src="/images/person-iso.svg" alt="person" />
      <img style="height: 150px" src="/images/person-iso.svg" alt="person" />
    </div>
  
</main>

<style>
  .iso__container {
    display: flex;
    width: 300px;
    align-items: end;
    justify-content: space-around;
  }
  .iso__container-big {
    display: flex;
    flex-direction: row-reverse;
    width: 600px;
    align-items: end;
    justify-content: space-around;
  }
  .iso__container-iso {
    display: flex;
    flex-direction: column;
    max-width: 1000px;
    align-items: start;
    justify-content: space-around;
  }
  .waffle__container {
    display: flex;
    /* flex-direction: column; */
    align-items: center;
    justify-content: center;
  }
  .headline {
    text-align: left;
    margin-top: 50px;
    /* border: 1px solid red; */
  }
</style>
