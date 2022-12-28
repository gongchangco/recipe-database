<script>
    import supabase from "$lib/db";
    import { onMount } from 'svelte';

    let recipes = []

    onMount(async() => {
        let { data, error } = await supabase.from("recipes").from('recipes').select('*');

        recipes = data;

        console.log(data, error);
    });

</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>