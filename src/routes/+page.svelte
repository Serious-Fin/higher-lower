<script>
    // Game state
    let score = 0;
    let currentProduct = {
      name: "Wireless Headphones",
      price: 89.99,
      image: "/api/placeholder/300/300"
    };
    
    // Next product (hidden from user until they guess)
    let nextProduct = {
      name: "Smart Watch",
      price: 149.99,
      image: "/api/placeholder/300/300"
    };
    
    // Sample products database
    const products = [
      { name: "Wireless Headphones", price: 89.99, image: "/api/placeholder/300/300" },
      { name: "Smart Watch", price: 149.99, image: "/api/placeholder/300/300" },
      { name: "Bluetooth Speaker", price: 59.99, image: "/api/placeholder/300/300" },
      { name: "Gaming Mouse", price: 45.99, image: "/api/placeholder/300/300" },
      { name: "Mechanical Keyboard", price: 129.99, image: "/api/placeholder/300/300" },
      { name: "External SSD 1TB", price: 99.99, image: "/api/placeholder/300/300" },
      { name: "Wireless Charger", price: 29.99, image: "/api/placeholder/300/300" },
      { name: "Noise Cancelling Earbuds", price: 199.99, image: "/api/placeholder/300/300" }
    ];
    
    // Game messages
    let message = "Will the next product cost higher or lower?";
    let showNextRound = false;
    
    // Get a random product that's different from the current one
    function getRandomProduct() {
      let availableProducts = products.filter(p => p.name !== currentProduct.name);
      return availableProducts[Math.floor(Math.random() * availableProducts.length)];
    }
    
    // Handle user guess
    function makeGuess(isHigher) {
      const actuallyHigher = nextProduct.price > currentProduct.price;
      
      if ((isHigher && actuallyHigher) || (!isHigher && !actuallyHigher)) {
        score++;
        message = `Correct! ${nextProduct.name} costs ${nextProduct.price > currentProduct.price ? 'more' : 'less'}.`;
      } else {
        message = `Wrong! ${nextProduct.name} costs ${nextProduct.price > currentProduct.price ? 'more' : 'less'}.`;
      }
      
      showNextRound = true;
    }
    
    // Continue to next round
    function nextRound() {
      currentProduct = nextProduct;
      nextProduct = getRandomProduct();
      message = "Will the next product cost higher or lower?";
      showNextRound = false;
    }
  </script>
  
  <div class="min-h-screen bg-gray-900 text-white flex flex-col items-center justify-center p-4">
    <!-- Header -->
    <header class="mb-8 text-center">
      <h1 class="text-3xl font-bold text-purple-400">Price Guesser</h1>
      <p class="text-xl mt-2">Pick if the next product costs higher or lower</p>
      <p class="text-lg mt-2">Score: {score}</p>
    </header>
    
    <!-- Game Container -->
    <div class="bg-gray-800 p-6 rounded-xl shadow-lg max-w-md w-full">
      <!-- Product Display -->
      <div class="flex flex-col items-center mb-6">
        <div class="w-64 h-64 mb-4 overflow-hidden rounded-lg">
          <img src={currentProduct.image} alt={currentProduct.name} class="w-full h-full object-cover" />
        </div>
        <h2 class="text-2xl font-semibold text-cyan-300">{currentProduct.name}</h2>
        <p class="text-3xl font-bold mt-2">${currentProduct.price.toFixed(2)}</p>
      </div>
      
      <!-- Game Message -->
      <p class="text-center mb-6 text-lg text-amber-300">{message}</p>
      
      <!-- Game Controls -->
      {#if !showNextRound}
        <div class="flex justify-center gap-4">
          <button 
            on:click={() => makeGuess(true)} 
            class="bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-6 rounded-lg transition-colors">
            HIGHER
          </button>
          <button 
            on:click={() => makeGuess(false)} 
            class="bg-red-600 hover:bg-red-700 text-white font-bold py-3 px-6 rounded-lg transition-colors">
            LOWER
          </button>
        </div>
      {:else}
        <div class="flex justify-center">
          <button 
            on:click={nextRound} 
            class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-lg transition-colors">
            NEXT PRODUCT
          </button>
        </div>
      {/if}
    </div>
  </div>