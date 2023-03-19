<script>
  
    import { fly } from 'svelte/transition';
    import MovieItem from "./Movie/Item.svelte";
    const APIKEY = "7288a68afbe7d9d75f554e6e650b49e2";
    const BASEURL = `https://api.themoviedb.org/3`;
    const APISETTINGS = `?api_key=${APIKEY}&language=es-mx`;
    const movies = (async () => {
      const URL = `${BASEURL}/discover/movie${APISETTINGS}&sort_by=popularity.desc`;
      const response = await fetch(URL);
      return await response.json();
    })();
    let likedMovies = [];
    function toggleLike(event){
      const movie = event.detail;
          let index = likedMovies.findIndex(m => m.id === movie.id);
      if(index >= 0){
        likedMovies.splice(index, 1);
      }else{
        likedMovies.push(movie);
      }
      likedMovies = likedMovies;
    }
    
    $: isLike = (id) => {
      let index = likedMovies.findIndex(m => m.id === id);
      return index >= 0;
    };
  </script>
  
  <svelte:head>
    <title>Movies Svelte</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC"
      crossorigin="anonymous"
    />
  </svelte:head>
  
  <main>
    <div class="row">
      <div class="col-12 col-md-6 col-lg-8 border panel">
        <h2>Películas Populares</h2>
        <div class="row">
          {#await movies}
            <p>Cargando datos...</p>
          {:then data}
            {#each data.results as movie}
              <div class="col-12 col-md-6 col-lg-4 p-2">
                <MovieItem
                  like={isLike(movie.id)}
                  id={movie.id}
                  overview={movie.overview}
                  title={movie.title}
                  cover={movie.poster_path}
                  on:onToggleLike={toggleLike}
                />
              </div>
            {/each}
          {/await}
        </div>
      </div>
      <div class="col-12 col-md-6 col-lg-4 border panel">
        <h2>Películas Favoritas</h2>
        <div class="row">
          {#if likedMovies.length}
          {#each likedMovies as movie, i (movie.id)}
          <div in:fly="{{duration:2000, y: -20}}"
               out:fly="{{duration: 1000, y: -20}}"
            class="col-12 col-md-6 col-lg-4 p-2">
            <MovieItem
              like={isLike(movie.id)}
              id={movie.id}
              overview=""
              title={movie.title}
              cover={movie.cover}
              on:onToggleLike={toggleLike}
            />
          </div>
        {/each}
          {:else}
            <div class="col-12">
              <p>No tienes películas favoritas</p>
            </div>
          {/if}
  
          
        </div>
      </div>
    </div>
  </main>
  
  <style>
    .panel{
      height: 100vh;
      overflow: auto;
  }
  </style>