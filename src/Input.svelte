<script>
    import Movie from "./Movie.svelte";

    let value = "";
    let response = [];

    const handleInput = (e) => value = e.target.value;

    $: if (value.length > 2) {
        response = fetch(`https://www.omdbapi.com/?s=${value}&apikey=422350ff`)
        .then(res => res.json())
        .then(apiResponse => apiResponse.Search || []);
    }
</script>

<input 
    placeholder="Search movies..." 
    value 
    on:input={handleInput}
>

{#await response}
    <p>Loading...</p>
{:then movies}
    {#each movies as {
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
{/await}