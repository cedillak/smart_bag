<script>
    import { onMount } from 'svelte';
    import { navigate } from "svelte-routing"; // Assuming you are using svelte-routing

    let username = 'User Name';
    
    function authenticate() {
        // Logic for biometric authentication
        console.log('Authenticating...');
        // Once authenticated, navigate to the next screen
        navigate('/screen2');
    }
</script>

<div class="screen-container">
    <h2>{username}</h2>
    <p>Biometric Authentication</p>
    <button on:click={authenticate}>Authenticate</button>
</div>

<style>
    .screen-container {
        background-color: #f0f0f0;
        padding: 20px;
        border-radius: 10px;
        text-align: center;
        width: 200px;
        margin: 0 auto;
    }
    
    h2 {
        font-size: 1.5rem;
    }

    button {
        margin-top: 20px;
        padding: 10px 20px;
        font-size: 1rem;
        cursor: pointer;
    }
</style>
