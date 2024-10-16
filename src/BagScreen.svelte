<script>
    import BoopAction from './BoopAction.svelte';
  
    let screen = "main";
    let isLocked = true;
    let isConnected = true;
    let isPhoneRinging = false;
    let batteryPercentage = 75; // Example battery percentage
    let notification = "Do not forget your phone!";
  
    function toggleLock() {
      isLocked = !isLocked;
    }
  
    function ringPhone() {
      isPhoneRinging = true;
      setTimeout(() => isPhoneRinging = false, 5000); // Reset after 5 seconds
    }
  
    function showBattery() {
      screen = "battery";
    }
  
    function showNotification() {
      screen = "notification";
    }
  
    function goBack() {
      screen = "main";
    }
  </script>
  
  <style>
    .bag-screen {
      width: 500px;
      height: 50px;
      border: 10px solid black;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background-color: black;
      margin-left: 20px;
      margin-top: 50px;
    }
  
    .buttons {
      display: flex;
      justify-content: space-around;
      width: 100%;
    }
  
    .button, .indicator {
      width: 40px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 5px;
      margin: 5px;
      cursor: pointer;
    }
  
    .battery-screen, .notification-screen {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      color: white;
    }
  
    .return-button {
      cursor: pointer;
    }
  
    .connected {
      background-color: green;
    }
  
    .disconnected {
      background-color: red;
    }
  
    i {
      font-size: 24px;
    }
  </style>
  
  <div class="bag-screen">
    {#if screen === "main"}
      <div class="buttons">
        <!-- Battery Button -->
        <div class="button" on:click={showBattery}>
          <i class="fa fa-battery-4" style="font-size:48px;color:white"></i>
        </div>
  
        <!-- Lock Button -->
        <div class="button" on:click={toggleLock}>
          {#if isLocked}
            <i class='fas fa-lock' style='font-size:48px;color:white'></i> <!-- Closed lock icon -->
          {:else}
            <i class='fas fa-lock-open' style='font-size:48px;color:white'></i> <!-- Open lock icon -->
          {/if}
        </div>
  
        <!-- Connection Status Indicator -->
        <div class="indicator {isConnected ? 'connected' : 'disconnected'}">
          {isConnected ? "🟢" : "🔴"}
        </div>
  
        <!-- Find My Phone Button -->
        <div class="button" on:click={ringPhone}>
          {#if isPhoneRinging}
            <BoopAction animationType="wiggle">
              <i class='fas fa-mobile' style='font-size:48px;color:red'></i>
            </BoopAction>
          {:else}
            <i class='fas fa-mobile' style='font-size:48px;color:white'></i>
          {/if}
        </div>
  
        <!-- Notification Button -->
        <div class="button" on:click={showNotification}>
            <i class='fas fa-exclamation-triangle' style='font-size:48px;color:red'></i>
        </div>
      </div>
  
    {:else if screen === "battery"}
      <div class="battery-screen">
        <span class="return-button" on:click={goBack}><i class="fa fa-caret-left" style="font-size:48px;color:white"></i></span>
        <span>Battery: {batteryPercentage}%</span>
      </div>
  
    {:else if screen === "notification"}
      <div class="notification-screen">
        <span class="return-button" on:click={goBack}><i class="fa fa-caret-left" style="font-size:48px;color:white"></i></span>
        <span>{notification}</span>
      </div>
    {/if}
  </div>
  