<script>
  let numbers = [10, 25, 33, 62, 75, 100]
  // binding
  let color = 'red'
  let num = 60


</script>
<div class="col-container">


  {#each numbers as number}
  <div class="col-wrapper">
    <div class="column" style="height: {number}px;"></div>
    <img class="mask" src="./images/coffe-cup-mask.svg" alt="">
  </div>
  {/each}


</div>


<style>
  .col-container {
    display: flex;
    flex-direction: row;
    align-items: flex-end;
  }
  .col-wrapper {
    position: relative;
    /* border: 1px solid black; */
    width: 75px;
    height: 100px;
    margin: 5px;
  }

  .column {
    position: absolute;
    bottom: 0;
    left: 5px;
    right: 0;
    background-color: red;
  }
  .mask {
    position: absolute;
    width: 77px;
    bottom: -2px;
    z-index: 1;
  }



</style>