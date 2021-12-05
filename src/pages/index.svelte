<script>
    import { onMount } from 'svelte';
    import { element } from 'svelte/internal';
    import Footer from '../../components/Footer.svelte'
    import Header from '../../components/Header.svelte'
    let api_key = '4c1c4651b470f738873f80310325d848'
    let result = []
    let page = ''
    let pageNum = [1,2,3,4,5,6,7,8,9,10]
  
    const apiReq = async () => {
      const response = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${api_key}&language=en-US&page=${page}`)
      result = await response.json()
      result = result['results']
      console.log(result)
    }
  
    onMount(() => {
          apiReq();
      });
  
  </script>
  <Header />
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

      <div class="flex justify-center">
        <li class="flex-row list-none my-8 space-x-4">
          <a href="/" class="rounded-md px-4 py-2 mr-4  text-gray-300 hover:opacity-70">Previous Page</a>
        </li>
      <li class="flex-row list-none my-8 space-x-4">
        {#each pageNum as pages}
      <a href="/page/{pages}" class="rounded-md px-4 py-2  text-gray-300 hover:opacity-70">{pages}</a>
      {/each}
    </li>
    <li class="flex-row list-none my-8 space-x-4">
      <a href="/" class="rounded-md px-4 py-2 ml-4 text-gray-300 hover:opacity-70">Next Page</a>
    </li>
  </div>

  </section>
<br>

<Footer />
  
  <style>
    :root{
      background-color: #181818;
    }
    .text-center{
      color: whitesmoke;
    }
  </style>