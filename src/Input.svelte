<script>
    import Movie from "./Movie.svelte";

    let value = "";
    let loading = false;
    let response = [];

    const handleInput = (e) => value = e.target.value;

    $: if (value.length > 2) {
        loading = true;
        fetch(`https://www.omdbapi.com/?s=${value}&apikey=422350ff`)
        .then(res => res.json())
        .then(apiResponse => {
            response = apiResponse.Search || [];
            loading = false;
        });
    }
</script>

<input 
    placeholder="Search movies..." 
    value 
    on:input={handleInput}
>

{#if loading}
    <p>Loading...</p>
{:else}
    {#each response as {
        Title: movieTitle, 
        Year: movieYear, 
        Poster: moviePoster
    }}
        <Movie 
            title={movieTitle}
            year={movieYear}
            poster={moviePoster}
        />
    {:else}
        <p>No results found</p>
    {/each}
{/if}