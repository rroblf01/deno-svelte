<script lang="ts">
  export let componentList: string[] = [];
</script>

<main>
  <ul class="list-item">
    {#each componentList as list}
      <li class="object-item"><p class="text-item">{list}</p></li>
    {/each}
  </ul>
</main>

<style>
  .list-item {
    list-style: none;
    padding: 0;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
    margin-bottom: 0.5rem;
    overflow: hidden;
    overflow-y: scroll;
    height: 50vh;
  }
  .object-item {
    padding: 0.5rem;
    margin-bottom: 0.5rem;
  }

  .text-item {
    border-bottom: 1px solid #ccc;
    text-align: center;
  }
</style>
