<script>
    import { supabase } from './_client.js';

    let roomName;

    async function createNewRoom() {
        if (!roomName) {
            alert("Enter a valid room name first.");
            return
        }

        const { data, error } = await supabase
            .from('rooms')
            .insert([
                { room_name: roomName, room_owner: supabase.auth.user().id }
            ]);

        await supabase
            .from('room_users')
            .insert([
                { room_id: data[0].room_id, user_id: supabase.auth.user().id }
            ]);
    }
</script>

<main>
    <h1>{supabase.auth.user().email}: Create a new chatroom</h1>

    <input bind:value={roomName} placeholder="Room Name">
    <button on:click={createNewRoom}>Make new room</button>
</main>