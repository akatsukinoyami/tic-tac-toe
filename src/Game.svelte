<script lang="ts">
    import Cell from "./Cell.svelte";
    let statuses: string[], winner: boolean | string;
    clear();
  
    const combinations = [
      [0, 4, 8],
      [2, 4, 6],
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8]
    ];
  
    function check() {
      combinations.forEach(combination => {
        if (combination.every(i => statuses[i] === "cross")) winner = "User";
        if (combination.every(i => statuses[i] === "circle")) winner = "Computer";
      });
  
      if (!winner && !statuses.find(i => i === "empty")) winner = "Draw";
    }
  
    function setCell(i: number) {
      if (statuses[i] === "empty") {
        statuses[i] = "circle";
        return true;
      }
      return false;
    }
  
    function setRandomly() {
      return [...Array(9)].some(() => setCell(Math.floor(Math.random() * 8)));
    }
  
    function setFirst() {
      return [...Array(9)].some(i => setCell(i));
    }
  
    function compute(cell) {
      if (!winner && statuses[cell] === "empty") {
        statuses[cell] = "cross";
        check();
  
        !winner && !setRandomly() && setFirst();
        check();
      }
    }
  
    function clear() {
      winner = false;
      statuses = [...Array(9)].fill("empty");
    }
  
    $: props = { statuses, compute };
  </script>
  
  <div class="field">
    {#each [[0,1,2], [3,4,5], [6,7,8]] as row}
      <div class="row">
        {#each row as i}
          <Cell i={i} {...props}/>
        {/each}
      </div>
    {/each}
  
    <div class="row footer">
      <div class="footer_cell">{#if winner} Winner: {/if}</div>
      <div class="footer_cell">{#if winner} {winner} {/if}</div>
      <div class="footer_cell"><button on:click={clear}>Clear</button></div>
    </div>
  </div>
  
  <style>
    .field {
      margin: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
  
    .row {
      display: flex;
      justify-content: space-between;
    }
  
    .footer {
      margin-top: 10px;
      height: 30px;
    }
  
    .footer_cell {
      width: 200px;
    }
  </style>