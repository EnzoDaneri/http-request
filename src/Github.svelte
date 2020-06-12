<!-- <script>
import { onMount } from 'svelte';

let users = [];
let loading = true;

onMount(async () => {
   let userData = await fetch('https://api.github.com/users');
   let githubUsers = await userData.json();
   users = githubUsers;
   loading = false;   
});

</script>   

<style>
h2 {
    text-align: center;
}

</style>

{#if loading}
 <h2>Loading...</h2>
 {:else}
 <section>
 {#each users as user}
 <article class="user">
 <img src={user.avatar_url} alt={user.login}>
 <div class="user-info">
 <h3>User: {user.login}</h3>
 <a href={user.html_url} class="btn-primary" target="blank">Github url</a>
 </div>
 </article>
 {/each}
 
 </section>
{/if} -->

<!-- /////////////////////////FORMA PROPIA DE SVELTE/////////////////////////////////////////// -->
- <script>

async function  getUsers() { 
 let userData = await fetch('https://api.github.com/users');
   let githubUsers = await userData.json();
   return githubUsers;
}

</script>  

<style>
.userGithub {
    font-size:15px;
    text-align: center;
    margin-top: 10px;
}
.credits {
    text-align: center;
}
</style>


<section>
{#await getUsers()}
<!-- promise is pending -->
<h1>Loading...</h1>
{:then users}
 {#each users as user}
 <article class="user">
 <img src={user.avatar_url} alt={user.login}>
 <div class="userGithub">
 <h3>{user.login}</h3>
 <a href={user.html_url} class="btn-primary" target="blank">Github url</a>
 </div>
 </article>
 {/each}
 {:catch error}
 <!-- promise was rejected -->
<p>Something went wrong : {error.message}</p>
{/await}

</section> 
<div class="credits"><a href="https://www.youtube.com/watch?v=uk1eM0Yn0UQ">Credits</a></div>