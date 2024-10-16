<script>
    // Array of bag items
    let items = [
      { name: "Laptop", checked: false },
      { name: "Water Bottle", checked: false },
      { name: "Notebook", checked: false },
      { name: "Headphones", checked: false }
    ];
  
    // Function to calculate the fullness of the bag (based on checked items)
    function getBagGraphic() {
      const checkedItems = items.filter(item => item.checked).length;
      if (checkedItems === 0) return 'empty-bag.png';
      if (checkedItems === 1) return 'half-full-bag.png';
      if (checkedItems === 2 || checkedItems === 3) return 'full-bag.png';
      return 'overflowing-bag.png';  // if all items are checked
    }
  </script>
  
  <style>
    .bag-image {
      width: 200px;
      height: 200px;
      object-fit: cover;
    }
  </style>
  
  <!-- Display checklist for bag items -->
  <ul>
    {#each items as item}
      <li>
        <label>
          <input type="checkbox" bind:checked={item.checked}>
          {item.name}
        </label>
      </li>
    {/each}
  </ul>
  
  <!-- Bag graphic updates dynamically based on selected items -->
  <div>
    <img src={getBagGraphic()} alt="Bag graphic" class="bag-image">
  </div>
  