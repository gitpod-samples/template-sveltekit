<script context="module">
    export async function load(ctx) {
      let slug = ctx.page.params.slug;
      return { props: { slug } };
    }
  </script>
  
  <script>
  import { time_ranges_to_array } from "svelte/internal";
  import supabase from "$lib/db";
  export let slug;
  
  async function getTimes(){
  
  const { data, error } = await supabase
    .from('activity_schedule')
    .select(`
      activity_id,
      activity_times (time)
    `)
    .match({activity_id:slug})
  
    if (error) throw new Error(error.message)
    return data
  }
  
  </script>
  
  {#await getTimes()}
    {:then data}  
  
  {#each data as { activity_id, time}}
    <li>{ activity_id } </li> <a href="/activity/times/booking/" class="btn btn-primary">Book</a>
  {:else}
    <li>No available times</li>
  {/each}
      
  {:catch error}
    <p>Something went wrong while fetching the data:</p>
    <pre>{error}</pre>
  {/await}
  