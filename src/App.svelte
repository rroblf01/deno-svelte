<script lang="ts">
  import WsChat from "./components/WsChat.svelte";

  let isLogged = false;
  let name = "Stranger";

  const logging = () => {
    isLogged = true;
  };
</script>

<main>
  {#if isLogged}
    <WsChat {name} bind:isLogged />
  {:else}
    <div class="logged-item">
      <h1>Not logged</h1>
      <p>Your Name will be {name}</p>
      <input
        type="text"
        bind:value={name}
        on:keydown={(event) => event.key === "Enter" && logging()}
      />
    </div>
  {/if}
</main>

<style>
  .logged-item {
    max-width: 36em;
    margin: 0 auto;
    text-align: center;
    font-size: 1.4em;
    width: 60vh;
    resize: none;
  }
</style>
