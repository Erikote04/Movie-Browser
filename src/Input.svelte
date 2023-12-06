<script>
    let value = "";
    let response = [];

    const handleInput = (e) => value = e.target.value;

    $: if (value.length > 2){
        fetch(`https://www.omdbapi.com/?s=${value}&apikey=422350ff`)
        .then(res => res.json())
        .then((apiResponse) => response = apiResponse.Search || []);
    }
</script>

<input 
    placeholder="Search movies..." 
    value 
    on:input={handleInput}
>

{#if response.length > 0}
    <p>We have {response.length} movies for your search</p>
{:else}
    <p>No results found</p>
{/if}
