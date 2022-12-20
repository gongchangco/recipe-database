<script>
    let count = 0;

    function increment() {
        count += 1;
    }
</script>

<h1>Welcome to About</h1>
<h3>Counting: {count}</h3>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<button on:click={increment}>Click to Count</button>