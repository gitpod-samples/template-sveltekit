<script>
    import supabase from "$lib/db";

async function getData(){
  
const { data, error } = await supabase
  .from('activities')
  .select(`
  id,
    name,
    previewLine

  `)
  if (error) throw new Error(error.message)
  
  return data
}
</script>
<h1>Test get data</h1>

{#await getData()}
  <p>Fetching data...</p>
{:then data}
  {#each data as activity}
  <div class="card" style="width: 18rem;">
  <div class="card-body">
    <h5 class="card-title">{activity.name}</h5>
    <h6 class="card-subtitle mb-2 text-muted">{activity.previewLine}</h6>
    <!-- <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p> -->
    <p>Price: </p>
    <a href="/activity/times/{activity.id}" class="card-link">Details</a>
  </div>
</div>

  {/each}
{:catch error}
  <p>Something went wrong while fetching the data:</p>
  <pre>{error}</pre>
{/await}

