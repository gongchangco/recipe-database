<script>
    let recipe;
    let ingredients;
    let instructions;
    let imageUrl;

    const API_KEY = 'Enter API KEY HERE!';
    const RANDOM_URL = `https://api.spoonacular.com/recipes/random?apiKey=${API_KEY}`;
    const INFO_URL = `https://api.spoonacular.com/recipes/{id}/information?apiKey=${API_KEY}`;
    
    async function getRandomRecipe() {
        try {
            const randomRes = await fetch(RANDOM_URL, {
                headers: { 'Content-Type': 'application/json' },
                mode: 'cors',
                cache: 'default',
            });

            const randomData = await randomRes.json();
            const id = randomData.recipes[0].id;

            const infoRes = await fetch(INFO_URL.replace('{id}', id), {
                method: 'GET',
                headers: { 'Content-Type': 'application/json' },
                mode: 'cors',
                cache: 'default',
            });

            const infoData = await infoRes.json();

            recipe = infoData;
            ingredients = infoData.extendedIngredients;
            instructions = infoData.analyzedInstructions[0].steps;
            imageUrl = infoData.image;

        } catch (error) {
            console.error(error);
        }
    }
</script>


<button><a href="/about">Go To About</a></button>
<button on:click={getRandomRecipe}>Show a random recipe</button>

{#if recipe}
    <div>
        <img src={imageUrl} alt={recipe.title} />
        <h2>{recipe.title}</h2>
        <p>{recipe.summary}</p>
        <br/>

        <h3>Ingredients</h3>
        <ul>
            {#each ingredients as ingredient}
                <li>{ingredient.name}</li>
            {/each}
        </ul>
        <br/>
        <h3>Instructions</h3>
        <ol>
            {#each instructions as instruction}
                <li>{instruction.step}</li>
            {/each}
        </ol>
    </div>
{/if}