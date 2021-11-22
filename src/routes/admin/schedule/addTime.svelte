<script>
    import supabase from '$lib/db';
    import moment from 'moment';
    
    let startDate = new Date("2021-10-01");
    let endDate =  new Date("2021-10-07");
    
    let time = "test";
    
    //get dates inbetween start and end time
    var getDates = function(startDate, endDate) {
      var dates = [],
          currentDate = startDate,
          addDays = function(days) {
            var date = new Date(this.valueOf());
            date.setDate(date.getDate() + days);
            return date;
          };
      while (currentDate <= endDate) {
        dates.push(currentDate);
        currentDate = addDays.call(currentDate, 1);
      }
    
      return dates;
    };
    
    let dateRange = getDates(startDate, endDate);
    //let dateRange = ["12/01/2021", "12/02/2021", "12/03/2021", "12/04/2021"];
    
    
    async function insertTime(){
    
    const { data, error } = await supabase
      .from('test')
      .insert([
     
       {date: "12/03/76"},
      ])
    
    }
    
    
    </script>
    
    
    <form on:submit|preventDefault={insertTime} method="post">
      {#each dateRange as dr}
    <input type="text" bind:value={dr}/>
    {/each}
    <input bind:value={time}>
    <button type="submit"> Add Time</button>
    </form>