<script>
  import { Router, Route, link } from 'svelte-routing';
  import bagImage from './lib/Shoulder-Bag-PNG-Isolated-HD.png';
  import { onMount } from 'svelte';
  import Battery from './Battery.svelte';
    import BagItems from './BagItems.svelte';
    import BagScreen from './BagScreen.svelte';

  //let batteryLevel = 100; // Start at 100%
  //let batteryIcon = "fas fa-battery-full"; // Default icon

  // Function to update battery level
  // function updateBatteryLevel() {
  //   if (batteryLevel > 0) {
  //     batteryLevel -= 10; // Decrease by 10%
  //     // Update the icon based on battery level
  //     if (batteryLevel > 50) {
  //       batteryIcon = "fas fa-battery-full";
  //     } else if (batteryLevel > 20) {
  //       batteryIcon = "fas fa-battery-half";
  //     } else {
  //       batteryIcon = "fas fa-battery-empty";
  //     }
  //   }
  // }

  // Simulate battery drain every second
  // onMount(() => {
  //   const interval = setInterval(() => {
  //     updateBatteryLevel();
  //     if (batteryLevel <= 0) {
  //       clearInterval(interval); // Stop when battery is empty
  //     }
  //   }, 1000); // Update every second

  //   return () => clearInterval(interval); // Cleanup interval on component destroy
  // });
  let showTeam = false;
  let name = "pranathi";
  let cScreen = false;
  let mScreen = false;
  let isHomeDisabled = false;
  let bag_num =''
  let showBatteryLevel = false;
  let c1Screen = true;
  let optionSelected ="Bag 01";
  function team() {
    showTeam = !showTeam;
  }
  function connectScreen(){
  mScreen = true;
  c1Screen = false;
  }
 
  function home(){
      bag_num = "";
      isHomeDisabled = false;
      c1Screen = true;
      mScreen = false;
  }
  function batteryLevel(){
    mScreen= false;
    isHomeDisabled = false;
    showBatteryLevel = true;
    c1Screen = false;
    cScreen= false;
  }

</script>

<main>
  <header><h1>Smart Bag</h1></header>
  
  <div>
    <button class="normalButton" on:click={team}>Team Members</button>
    {#if showTeam}
      <ul>
        <li>Ana</li>
        <li>Harshini</li>
        <li>Pranathi</li>
        <li>Seethala</li>
      </ul>
    {/if}
  </div>

  <br>
  <button class="normalButton"><a use:link href="link" target="_blank" class="doc">Documentation</a></button>
  <br><br>
  <button class="normalButton">Tutorial</button>
  <br><br>
  <select bind:value={optionSelected}>
    <option value='Bag 01'>Bag 01</option>
    <option value ='Bag 02'>Bag 02</option>
  </select>
  <div class="container">
    <div class="bag-screen">
        <BagScreen />
    </div>
 <BagItems></BagItems>
    
    <div class="bag-container">
      <img src={bagImage} alt="Bag" class="bag" />
    
    </div>

    <div class="phone">
      <div class="screen-content">
        <p class="heading">Smart Bag App</p>
        {#if c1Screen===true} <button class="normalButton1 connectButton"on:click={connectScreen}>Connect</button>{/if}
        <!-- {#if cScreen ===true && mScreen ===false }
        <div class="bag-buttons">
        <p>Bag 01 <button class="normalButton1 connectButton" on:click={() => mainScreen("bag01")}>Connect</button></p>
        <br>
        <p>Bag 02 <button class="normalButton1 connectButton" on:click={() => mainScreen("bag02")}>Connect</button></p>
        </div>
        {/if} -->
        {#if mScreen}
        <p>Connected to {optionSelected} <button on:click={connectScreen}>Disconnect</button> </p>
        <div class="button-container">
        <button class="normalButton" on:click={batteryLevel}>Battery Level</button>
        <button>Lock/Unlock</button>
        <br>
        <button>Find my bag</button>
        <button>New Add on</button>
        </div>
        {/if}
        {#if showBatteryLevel}
        <Battery></Battery>
        {/if}
        <div class="phone-buttons">
          <nav>
            <button class="nav-btn" on:click={home} disabled={isHomeDisabled}>
              <i class="fa fa-home"></i>
            </button>
            <button class="nav-btn">
              <i class="fa fa-line-chart"></i>
            </button>
            <button class="nav-btn">
              <i class="fas fa-bell"></i>
            </button>
            <button class="nav-btn">
              <i class="fas fa-cog"></i>
            </button>
          </nav>
        </div>
      </div>
    </div>
  </div>
  
  
    
  
</main>

<style>
    h1 {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.5;
    font-weight: bold;
    text-align: center;
  }
  .connectButton{
    position:relative;
    bottom: 30%;
  }
  .normalButton {
    background-color: black;
    color: white;
    cursor: pointer;
    font-weight: 100;
    border-radius: 20px;
    font-size: 20px;
    margin: 5px;
  }
  .normalButton1 {
    background-color: white;
    color: black;
    cursor: pointer;
    font-weight: 100;
    border-radius: 20px;
    font-size: 20px;
  }

  nav {
    position: absolute;
    width: 290px;
    display: flex;
    justify-content: space-around;
    padding: 10px;
    margin-top: 0px;
    margin-bottom: 30px;
    border-radius: 20px;
  }

  .nav-btn {
    color: white;
    background-color: transparent;
    border: none;
    font-size: 24px;
    cursor: pointer;
  }

  .nav-btn:hover {
    color: #aaa;
  }
  .nav-btn[disabled] {
    opacity: 0.5; /* Make the button appear faded */
    cursor: not-allowed; /* Change the cursor to indicate it's disabled */
  }
  
 
  button:hover {
    background-color: gray;
  }
  
  .doc {
    text-decoration: none;
    color: white;
  }
  
  .container {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-top: 20px; /* Spacing above the container */
  }
  i{
    font-size: 24px;
  }
  
  .bag-container {
    position: relative;
    width: 300px;
    height: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    right:10%;
  }
  
  .bag {
    width: 100%; /* Automatically fits within the bag-container */
    height: auto;
  
  }

  .phone {
    width: 320px;
    height: 540px;
    border-radius: 40px;
    border: 3px solid rgba(0, 0, 0, 0.3); /* Thin bezel */
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(145deg, #e0e0e0, #ffffff);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15); /* Subtle shadow for depth */
    margin-right: 100px; /* Space between phone and bag */
    position: relative;
    overflow: hidden;
   /* Space between phone and bag */
  }

  .screen-content {
    width: 300px;
    height: 520px;
    background-color: black;
    color: white;
    border-radius: 35px; /* Internal rounded screen */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  /* Button container inside phone screen */
  .phone-buttons {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    width: 100%;
    padding: 10px;
    margin-top:30px;
  }
  .bag-buttons{
    margin-bottom:30px;
  }
  .heading{
    font-size: 30px;
    bottom:40%;
  }
  .button-container{
    display: flex; /* Use flexbox for layout */
    justify-content: space-between; /* Space between buttons */
    margin-top: 10px;
  }
  #map {
        height:100%;
        width: 100%;
    }

</style>
