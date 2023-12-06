<script>
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
    {#if response.length > 0}
        <div>
            <p>We have {response.length} movies for your search</p>
            {#each response as movie}
                <article>
                    <img src={movie.Poster} alt={movie.Title}>
                    <h3>{movie.Title}</h3>
                    <span>{movie.Year}</span>
                </article>
            {/each}
        </div>
    {:else}
        <p>No results found</p>
    {/if}
{/if}