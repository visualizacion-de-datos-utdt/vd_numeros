<script>
  import * as d3 from "d3"
  import Waffle from "./Waffle.svelte"

  // import person from "/images/person.png"

  let numbers = [5, 18, 29, 37, 75]
  let numbersDivided5 = numbers.map(n => Math.floor(n / 5))

  function altura(n) {
    let scale = d3.scaleLinear().domain(d3.extent(numbers)).range([15, 225])
    return scale(n)
  }

  function sides(n) {
    let s = d3.scaleLinear().domain(d3.extent(numbers)).range([3, 12])
    return s(n)
  }

  /* Polígonos */

  function drawPolygon(numSides) {
    // Define the radius of the polygon
    const radius = 50
    // Define the center of the polygon
    const centerX = 100
    const centerY = 100

    // Calculate the points of the polygon
    const points = d3.range(numSides).map(function (i) {
      const angle = (i / numSides) * 2 * Math.PI
      const x = centerX + radius * Math.cos(angle)
      const y = centerY + radius * Math.sin(angle)
      return [x, y]
    })

    return points.join(" ")
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
  <!-- ISOTYPE - Canal: altura -->
  <h3 class="headline">Dos magnitudes. Canal: longitud</h3>
  <div class="iso__container">
    <img style="height: 75px" src="/images/person-iso.svg" alt="person" />
    <img style="height: 150px" src="/images/person-iso.svg" alt="person" />
  </div>

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
  <!-- Poligonos - Canal: lados -->
  <h3 class="headline">Set magnitudes. Canal: lados polígonos.</h3>
  {#each numbers as n}
    <svg height="200" width="200">
      <polygon
        points={drawPolygon(sides(n))}
        style="fill:#ddd;stroke:red;stroke-width:1"
      />
    </svg>
  {/each}

  <!-- Draw svg arc -->
  <h3 class="headline">Set magnitudes. Canal: longitud. Tipo: gráfco arco</h3>
  <svg width="300" height="300" viewBox="-100 -100 200 200">
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
    />
  </svg>
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
