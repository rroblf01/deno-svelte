<script lang="ts">
    export let componentList: string[] = [];
</script>

<main>
    <ul class="list-item">
        {#each componentList as list}
            <li class="object-item">{list}</li>
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
    }
    .object-item {
        padding: 0.5rem;
        margin-bottom: 0.5rem;
    }
</style>
