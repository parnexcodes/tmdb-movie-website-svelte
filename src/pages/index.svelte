<script>
    import { onMount } from 'svelte';
    import { element } from 'svelte/internal';
    let api_key = '4c1c4651b470f738873f80310325d848'
    let result = []
  
    const apiReq = async () => {
      const response = await fetch(`https://api.themoviedb.org/3/movie/now_playing?api_key=${api_key}&language=en-US`)
      result = await response.json()
      result = result['results']
      console.log(result)
    }
  
    onMount(() => {
          apiReq();
      });
  
  </script>
  <section>
    <div class="text-center text-white text-5xl my-8">
      <h1>Trending Movies</h1>
    </div>
  
    <div class="mx-24 grid gap-4 lg:grid-cols-5">
      {#each result as element}
      <div class="rounded-md overflow-hidden">
        <a href="/movie/{element.id}" title="{element.title}">
          <img class="w-11/12 hover:opacity-70" title="{element.title}" src="https://image.tmdb.org/t/p/original{element.poster_path}" alt="{element.title}" width="1500px" height="2250px"/>
      </a>
      </div>
      {/each}
      </div>
  
  </section>
<br>
<div class="text-center py-4 text-white" style="background-color: rgba(0, 0, 0, 0.5)">
    <p>Made with ❤️ by parnex</p>
    <p>Powered by Svelte</p>
</div>
  
  <style>
    :root{
      background-color: #181818;
    }
    .text-center{
      color: whitesmoke;
    }
  </style>