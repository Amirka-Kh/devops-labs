<script lang="ts">
    const fetchQuote = (async () => {
        const response = await fetch('https://api.kanye.rest')
        return await response.json()
    })()

    const fetchCat = (async () => {
        const response = await fetch('https://api.thecatapi.com/v1/images/search?')
        return await response.json()
    })()
</script>

<main>
    {#await fetchQuote}
        <p>...waiting</p>
    {:then quote}
    <div class="quote-section">
        <div id="quotes">
            <h2>{quote.quote}</h2>
        </div>
    </div>
    {:catch error}
        <p>An error occurred!</p>
    {/await}
    {#await fetchCat}
        <p>...waiting</p>
    {:then cat}
    <div class="cat-section">
        <div id="cat-pic">
            {#each cat as catty}
                <img src={catty.url} alt="kitty"/>
            {/each}
        </div>
    </div>
    {:catch error}
        <p>An error occurred!</p>
    {/await}
</main>

<style>
    main {
        background: black;
        color: white;
    }

    div.quote-section {
        margin: 100px;
    }

    #quotes {
        text-align: center;
        font-weight: bold;
        color: white;
        font-size: 60px;
    }

    img {
        border-radius: 30px;
        display: block;
        margin-left: auto;
        margin-right: auto;
        width: 80%;
    }
</style>