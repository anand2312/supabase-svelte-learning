<script>
    import { supabase } from './_client.js';

    async function getUserRooms() {
        const { data, error } = await supabase
            .from('rooms')
            .select('room_name, room_id');

        if (error) {
            console.log(error);
        }

        return data;
    }
</script>

<main>
    <h1>{supabase.auth.user().email}: Your chatrooms</h1>
    {#await getUserRooms()}
        <center><p>Loading your chatrooms...</p></center>
    {:then rooms}
        {#each rooms as { room_name, room_id }}
            <a href="/chat/{room_id}">{room_name}</a>
        {/each}
    {/await}
</main>