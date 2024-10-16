<script>
    let batteryLevel = 100; // Start with a full battery
    let isCharging = false;
  
    // Simulate a decrease in battery level
    function decreaseBattery() {
      // Simulate battery drain
      if (batteryLevel > 0) {
        batteryLevel -= Math.floor(Math.random() * 10) + 1; // Decrease by 1-10%
        if (batteryLevel < 0) {
          batteryLevel = 0; // Don't let it go below 0%
        }
      }
    }
  
    // Simulate charging
    function chargeBattery() {
      if (batteryLevel < 100) {
        batteryLevel += Math.floor(Math.random() * 10) + 1; // Increase by 1-10%
        if (batteryLevel > 100) {
          batteryLevel = 100; // Don't let it go above 100%
        }
      }
    }
  
    // Toggle between charging and not charging
    function toggleCharging() {
      isCharging = !isCharging;
      if (isCharging) {
        chargeBattery();
      } else {
        decreaseBattery();
      }
    }
  </script>
  
  <!-- UI to Display Battery Level -->
  <div>
    <h2>Smart Bag Battery Level</h2>
    <p>Battery Level: {batteryLevel}%</p>
    <p>{isCharging ? "Charging" : "Not Charging"}</p>
  
    <!-- Button to simulate charging/discharging -->
    <button on:click={toggleCharging}>
      {isCharging ? "Stop Charging" : "Start Charging"}
    </button>
  
    <!-- Button to manually decrease the battery -->
    <button on:click={decreaseBattery}>
      Decrease Battery
    </button>
  </div>
  
  <style>
    h2 {
      font-size: 1.5em;
      margin-bottom: 10px;
    }
    p {
      font-size: 1.2em;
    }
    button {
      margin-top: 10px;
      margin-right: 10px;
      padding: 10px 20px;
      font-size: 1em;
    }
  </style>
  