<script>
  import { onMount } from "svelte";

  let movies = [];
  let pagination = null;

  const getMovies = async () => {
    await fetch(`http://localhost:3000/movies`)
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        movies = data.data;
        pagination = data.pagination;
      })
      .catch((err) => console.log(err));
  };
  onMount(async () => getMovies());
</script>

<main class="text-center">
  <div class="container">
    <div class="row">
      {#each movies as movie}
        <div class="col">
          <div class="card" style="width: 18rem;">
            <img src={movie.poster} class="card-img-top" alt={movie.title} />
            <div class="card-body">
              <p class="card-text">
                {movie.title}
                <br />
                {#each movie.genres as genre}
                  <span>{genre}</span>,
                {/each}
                <br />
                Year: <span>{movie.year}</span>
              </p>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
