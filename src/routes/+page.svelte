<script>
  import autoAnimate from "@formkit/auto-animate"


const groups = [
    {
        year: 2024,
        photos: [{id: 1}, {id: 2}, {id: 3}, {id: 4}, {id: 5}, {id: 6}, {id: 7}, {id: 8}]
    },
    {
        year: 2023,
        photos: [
            {id: 9}, {id: 12}, {id: 15}, {id: 18}
        ],
    },
    {
        year: 2022,
        photos: [
            {id: 20}, {id: 25}, {id: 30}, {id: 35}, {id: 40}, {id: 45}
        ]
    }
]
let mod = 1
const toggleMod = () => mod = (mod + 1) % 5

$: groupsVisible = groups
    .map((group) => ({
        ...group,
        photos: group.photos.filter((photo) => photo.id % mod === 0),
    }))
    .filter((group) => group.photos.length)
</script>


<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<h1>Gallery <button on:click={toggleMod}>{mod}</button></h1>
<div class="photo-grid" use:autoAnimate>
{#each groupsVisible as group}
    <h2 class="group-caption">{ group.year }</h2>
    {#each group.photos as photo (photo.id)}
    <div class="item">
        <div class="title-image">{photo.id}</div>
    </div>
    {/each}
{/each}
</div>

<style lang="scss">
.photo-grid {
    --gap: 1rem;
    text-align: center;
    background-color: lightblue;

    max-width: 120ch;
    margin: 0 auto;

    .group-caption {
        width: 100%;
        text-align: center;
    }
}

.photo-grid .item {
    display: inline-block;
    background-color: ivory;
    padding: 0.2rem 0.2rem 1rem;
    margin: calc(var(--gap) / 2);

    .title-image {
        width: 12rem;
        height: 9rem;

        display: grid;
        place-content: center;
        font-family: Helvetica;
        font-size: 6rem;

        background-color: dodgerblue;
        color: wheat;
    }
    
}
</style>