<script>
    export let slug;
    import { onMount } from 'svelte';
    import { element } from 'svelte/internal';
    import {isActive, url} from '@roxi/routify'
    import Footer from '../../../components/Footer.svelte'
    let api_key = '4c1c4651b470f738873f80310325d848'
    let result = []
    let poster = ''
    let title = ''
    let overview = ''
    let runtime = ''
    let release_date = ''
    let imdb_id = ''
    let backdrop_path = ''
    let genres = ''
    let vote_average = ''
  
    const apiReq = async () => {
      const response = await fetch(`https://api.themoviedb.org/3/movie/${slug}?api_key=${api_key}&language=en-US`)
      result = await response.json()
    //   result = result['results']
      console.log(result)
      poster = `https://image.tmdb.org/t/p/original${result['poster_path']}`
      title = result['title']
      overview = result['overview']
      runtime = result['runtime']
      release_date = result['release_date']
      imdb_id = result['imdb_id']
      backdrop_path = `https://image.tmdb.org/t/p/original${result['backdrop_path']}`
      genres = result['genres']
      vote_average = result['vote_average']
    }
  
    onMount(() => {
          apiReq();
      });

</script>
<div class="movie-info">
  <div class="container mx-auto px-4 py-16 flex flex-col md:flex-row">
      <div class="flex-none">
          <img src="{poster}" alt="poster" class="w-64 lg:w-96">
      </div>
      <div class="md:ml-24">
          <h2 class="text-4xl mt-4 md:mt-0 font-semibold text-gray-300">{title}</h2>
          <div class="flex flex-wrap items-center text-gray-300 text-sm my-4">
              <svg class="fill-current text-orange-500 w-4" viewBox="0 0 24 24"><g data-name="Layer 2"><path d="M17.56 21a1 1 0 01-.46-.11L12 18.22l-5.1 2.67a1 1 0 01-1.45-1.06l1-5.63-4.12-4a1 1 0 01-.25-1 1 1 0 01.81-.68l5.7-.83 2.51-5.13a1 1 0 011.8 0l2.54 5.12 5.7.83a1 1 0 01.81.68 1 1 0 01-.25 1l-4.12 4 1 5.63a1 1 0 01-.4 1 1 1 0 01-.62.18z" data-name="star"/></g></svg>
              <span class="ml-1">{vote_average}</span>
              <span class="mx-2">|</span>
              <span>{release_date}</span>
              <span class="mx-2">|</span>
              <span>{runtime} minutes.</span>
              <span class="mx-2">|</span>
              {#each genres as genre}
              <span>{genre.name}, &nbsp;</span>
              {/each}
          </div>

          <p class="text-gray-300 mt-8">
              {overview}
          </p>

          <div class="mt-12">
            <a href="/play/{slug}">
            <button 
                class="flex inline-flex items-center bg-gray-500 text-gray-300 rounded font-semibold px-5 py-4 hover:bg-gray-600 transition ease-in-out duration-150"
            >
                <svg class="w-6 fill-current" viewBox="0 0 24 24"><path d="M0 0h24v24H0z" fill="none"/><path d="M10 16.5l6-4.5-6-4.5v9zM12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8z"/></svg>
                <span class="ml-2">Play Movie</span>
            </button>
          </a>
        </div>
    </div>
</div>
</div>
<Footer />

  <style>
    :root{
      background-color: #181818;
      overflow: hidden;
    }
</style>