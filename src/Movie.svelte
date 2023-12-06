<script>
    export let title, year, poster;
</script>

<article>
    <img src={poster} alt={title}>
    <h3>{title}</h3>
    <span>{year}</span>
    {#if 2023 - year < 5}
        <icon>🆕</icon>
    {/if}
</article>

<style>
    article {
        border: 1px solid black;
        border-radius: 4px;
        padding: 16px;
        margin-bottom: 8px
    }

    h3 {
        font-size: 24px;
        margin-bottom: 4px;
    }
</style>