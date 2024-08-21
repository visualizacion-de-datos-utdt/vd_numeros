<script>
  import * as d3 from "d3"
  import Waffles from "./lib/Waffles.svelte"
  import IrregularPath from "./lib/IrregularPath.svelte"
  import CoffeColumns from "./lib/CoffeColumns.svelte"
  import Donas from "./lib/Donas.svelte"

  let numbers = [5, 18, 29, 75, 100]
  let numbersDivided5 = numbers.map(n => Math.floor(n / 5))

  function altura(n) {
    let scale = d3
      .scaleLinear()
      .domain(d3.extent(numbers)) // extent returns [min, max]
      .range([15, 225])
    return scale(n)
  }
</script>

<main class="container">
  <!-- ISOTYPE - Canal: altura -->
  <h3 class="headline">Magnitudes. Canal: longitud</h3>
  <div class="iso__container">
    <img style="height: 75px" src="./images/person-iso.svg" alt="person" />
    <img style="height: 150px" src="./images/person-iso.svg" alt="person" />
  </div>
  <hr />

  <!-- Cafés -->
  <CoffeColumns numbers={numbers} title="Canal: altura. Tipo: columnas" />
  <hr />

  <!-- Canal: altura -->
  <h3 class="headline">Magnitudes. Canal: longitud</h3>
  <div class="iso__container-big">
    {#each numbers as n}
      <img
        style="height: {altura(n)}px; padding: 10px"
        src="./images/person.png"
        alt="person"
      />
    {/each}
  </div>
  <hr />

  <IrregularPath title="Canal: longitud (path irregular)" numbers={numbers} />
  <hr />

  <!-- Canal: longitud. Type: Isotype Chart  -->
  <h3 class="headline">Magnitudes. Canal: longitud. Tipo: gráfico Isotype</h3>

  <div class="iso__container-iso">
    {#each numbersDivided5 as n, index}
      <div class="row">
        {#each Array(n) as m}
          <img
            style="height: 50px; padding: 2px"
            src="./images/person.png"
            alt="person"
          />
        {/each}
        <p>{numbers[index]}</p>
      </div>
    {/each}
  </div>
  <hr />

  <!-- Waffles -->
  <Waffles
    numbers={numbers}
    title="Magnitudes. Canal: área. Tipo: gráfico waffle"
  />
  <hr />

  <!-- Donas -->
  <Donas numbers={numbers} title="Magnitudes. Canal: ángulo. Tipo: gráfico donas" />
  <hr />

</main>

<style>
  .container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;
  }

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
  .headline {
    text-align: left;
    margin-top: 50px;
    /* border: 1px solid red; */
  }
</style>
