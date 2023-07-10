<script>
  export let i, statuses, compute;

  const contents = {
    empty: "",
    cross: `lapp.png`,
    circle: `mudrock.png`
  };
</script>

<div 
  class="cell" 
  on:click={() => {compute(i)}} 
  style="background-image: url({contents[statuses[i]]})"
/>

<style>
  .cell {
    background-size: contain;
    background-repeat: no-repeat;
    width: 200px;
    height: 200px;
    border: 1px solid black;
    text-align: center;
    vertical-align: middle;
  }
</style>