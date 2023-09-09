<script lang="ts">
  import Sqaure from "./Sqaure.svelte";

  export let grid: string[];

  let a: number = -1;
  let b: number = -1;
  let reset_timeout: number;

</script>
<div class="grid">
    {#each grid as emoji, index}
        <Sqaure {emoji} on:click={() => {
            clearTimeout(reset_timeout)
            if(a === -1 && b === -1) {
                a = index;
            } else if (b === -1) {
                b = index;
                if(grid[a] === grid[b]) {
                    // correct

                } else {
                    // incorrect
                    reset_timeout = setTimeout(() => {
                        a = b = -1;
                    }, 1000)
                }
            } else {
                b = -1;
                a = index;
            }
        }}
        selected={a === index || b === index}
        />
    {/each}
</div>

<style>
    .grid {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-template-rows: repeat(4, 1fr);
        grid-gap: 0.5em;
        height: 100%;
    }
</style>