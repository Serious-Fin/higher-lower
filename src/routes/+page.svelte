<script>
  import { products } from "$lib/data";

  /** @type {number} current user score */
  let score = $state(0);
  /** @type {import('$lib/types').Product} */
  // @ts-ignore
  let previousProduct = $state({});
  /** @type {import('$lib/types').Product} */
  // @ts-ignore
  let currentProduct = $state({});

  function startGame() {
    previousProduct = getRandomElement(products);
    currentProduct = getRandomElement(products);
  }

  function getRandomElement(array) {
    return array[getRandomNumber(array.length)];
  }

  /**
   * Returns a random number in range [0, endIndex)
   * @param endIndex last index until which to get the number
   */
  function getRandomNumber(endIndex) {
    return Math.floor(Math.random() * endIndex);
  }

  startGame();
</script>

<div class="min-h-screen bg-gray-900 text-white p-4 grid grid-cols-1 md:grid-cols-2 gap-8 content-center">
  <!-- Previous product -->
  <div class="flex flex-col items-center text-center">
    <div class="w-64 h-64 mb-4 overflow-hidden rounded-lg">
      <img src={previousProduct.image} alt={previousProduct.productName} class="w-full h-full object-cover" />
    </div>
    <h2 class="text-2xl font-semibold text-cyan-300">{previousProduct.productName}</h2>
    <p class="text-sm">Kainuoja</p>
    <p class="text-3xl font-bold mt-2">{previousProduct.productCost}€</p>
  </div>

  <!-- Divider - Horizontal on mobile, Vertical on desktop -->
  <div class="block md:hidden absolute left-10 right-10 top-1/2 h-px bg-gray-600"></div>
  <div class="hidden md:block absolute top-10 bottom-10 left-1/2 w-px bg-gray-600"></div>

  <!-- Next Product -->
  <div class="flex flex-col items-center text-center">
    <div class="w-64 h-64 mb-4 overflow-hidden rounded-lg">
      <img src={currentProduct.image} alt={currentProduct.productName} class="w-full h-full object-cover" />
    </div>
    <h2 class="text-2xl font-semibold text-cyan-300">{currentProduct.productName}</h2>
    <p class="text-sm">Kainuoja</p>
    <div class="flex justify-center gap-4 mt-4 text-xl">
      <button class="border-4 border-green-600 hover:bg-green-600 text-white font-bold py-2 px-6 rounded-lg transition-colors">Daugiau</button>
      <button class="border-4 border-red-600 hover:bg-red-600 text-white font-bold py-2 px-6 rounded-lg transition-colors">Mažiau</button>
    </div>
  </div>
</div>
