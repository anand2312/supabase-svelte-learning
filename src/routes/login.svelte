<script>
    import { supabase } from './_client.js';

    let email;
    let password;

    async function signIn() {
        console.log(email);
        console.log(password);
        const { user, session, error} = await supabase.auth.signIn({email: email, password: password});
        
        if (error) {
            console.log(error);
        }

        await supabase
            .from('users')
            .insert([
                { id: user.id }
            ]);
    }

    async function signUp() {
        console.log(email);
        console.log(password);
        const { user, session, error} = await supabase.auth.signUp({email: email, password: password});

        if (error) {
            console.log(error);
        }
    }

</script>


<h1>Join us!</h1>

<p>Create an account on this app with an email and password, or log in.</p>

<div>
    <input bind:value={email} placeholder="Email">
    <br><br>
    <input type="password" placeholder="Password" bind:value={password}>
    <br><br>
    <button on:click={signUp}>Sign Up</button>
    <button on:click={signIn}>Sign In</button>
</div>