<script>
  import { onMount } from "svelte";

  const url = "https://fastapi-learning-yezd.onrender.com";

  export async function usersList(){
      let response = await fetch('${url}/users/');
      return await response.json;
  }

  export async function getUserByName(userName) {
  const response = await fetch(`${url}/users/${userName}`);
  return await response.json();
}

  let users = {};
  let searchName = '';
  let foundUser = null;

  onMount(async()=> {
      users = usersList();
  });

  async function handleSearchUser() {
    foundUser = await getUserByName(searchName);
  }

</script>

<h2>
  <ul>
      {#each users.users as user }
          <li>{user.name} {user.age}</li>
      {/each}
  </ul>
</h2>

<h2>Buscar Usuario por Nombre</h2>
<input type="text" bind:value={searchName} placeholder="Nombre" />
<button on:click={handleSearchUser}>Buscar</button>
{#if foundUser}
  <p>{foundUser.user ? `${foundUser.user.name} - ${foundUser.user.age}` : "Usuario no encontrado"}</p>
{/if}