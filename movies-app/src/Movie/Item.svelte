<script>
    import { createEventDispatcher } from 'svelte';
    
    const dispatch = createEventDispatcher();
    export let id;
    export let title;
    export let overview;
    export let cover;
    export let like;
	$: coverURL = `https://image.tmdb.org/t/p/original${cover}`;
    function toggleLike(){
        dispatch('onToggleLike', {id, title, overview, cover});
    }
</script>

<div class="card">
    <img src={coverURL} class="card-img-top" alt={title} />
    <div class="card-body">
        <h5 class="card-title">{title}</h5>
        <p class="card-text">
            {overview}
        </p>
        <div class="text-center">
            <button class={like ? 'btn btn-secondary': 'btn btn-primary'} on:click={toggleLike}>{like ? 'Unlike!': 'Like!'}</button>
        </div>
    </div>
</div>