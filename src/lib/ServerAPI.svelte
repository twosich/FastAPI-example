<script>
    import { onMount } from "svelte";

    const url = "https://fastapi-learning-yezd.onrender.com/";

    export async function usersList(){
        let response = await fetch('${url}/users');
        return await response.json;
    }

     export async function nameUsers(name){
        let response = await fetch('${url}/users/${name}')
        return await response.json();
    }

    let users = {};

    onMount(async()=> {
        users = usersList();
    });

</script>

<h2>
    <ul>
        {#each users.users as user }
            <li>{user.name} {user.age}</li>
        {/each}
    </ul>
</h2>