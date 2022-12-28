<script>
    import supabase from "$lib/db";

    async function getRecipes() {
        const { data, error } = await supabase
            .from('recipes')
            .select();
        
        if (error) throw new Error(error.message);

        return data;
    }
</script>

<div>
    <h1 class="text-2xl">Recipe List Test:</h1>
    {#await getRecipes()}
        <p>Fetching recipes...</p>
    {:then data}
        {#each data as recipe}
            <li>{recipe.title}</li>
        {/each}
    {:catch error}
        <p>Something went wrong while fetching the data:</p>
        <pre>{error}</pre>
    {/await}
</div>