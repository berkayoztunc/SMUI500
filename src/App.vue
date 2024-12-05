<template>
  <div class="grid grid-cols-2 md:grid-cols-4 items-center justify-center  max-w-3xl mx-auto gap-2">
    <div class="text-center rounded overflow-hidden shadow-lg p-2 rounded-xl">
      <a href="/">
        <img src="/smui500_x.png" alt="" class="">
      </a>
    </div>
    <div class="hidden md:flex">
      
    </div>
    <div class="hidden md:flex">
     
    </div>
    <div class="text-center rounded overflow-hidden shadow-lg p-10 rounded-xl">
      <ul>
        <li><a href="/meme.html">Memes (soon)</a></li>
        <li><a href="https://t.me/smux500">Telegram </a></li>
        <li><a href="/merch.html">Merch (soon)</a></li>
        <li><a href="/merch.html">Dexscreener (soon)</a></li>
      </ul>
    </div>
  </div>
  <div class="text-center rounded overflow-hidden shadow-lg p-10 rounded-xl">
    <!-- Görseller -->
    <div class="text-center rounded overflow-hidden shadow-lg p-10 rounded">

      <h1 class="text-3xl">Solana Men's Underwaer Index = SMUX500</h1>
      <p>CA : 69FSWQK2bY6aqP8bTVErEMwwh7g5fC5Pve7JTxGbpump</p>
      <div class=" text-center">
          {{  price }}$
        </div>
      <div class="flex justify-around w-full mb-8  gap-1 md:gap-4">
        <div
          v-for="(image, index) in images"
          :key="index"
          class="w-24 h-24 rounded-md  flex items-center justify-center p-0 md:p-4"
        
        >
          <img :src="(index) + '.png'" alt="">
        </div>
      </div>

      <!-- Progress Bar -->
      <div class="relative w-full ">
        <div class="h-8 bg-gray-300 rounded-full flex">
          <div
            class="h-full bg-green-500 rounded-full transition-all"
            :style="{ width: progressPercentage + '%' }"
          ></div>
        </div>

        <!-- Fiyat Etiketleri -->
        <div class="flex justify-between mt-2 text-sm text-gray-600">
          <span v-for="label in labels" :key="label">{{ label }}$</span>
        </div>
      </div>
      <p class="p-6 text-justify	">

        The Men's Underwear Index (SMUX) is an economic indicator that purportedly signals the onset of recovery during economic downturns. The concept is based on the idea that men's underwear is a basic necessity, with sales typically stable during normal times. However, during severe economic slumps, purchases may be delayed, reflecting shifts in discretionary spending.

        SMUX is considered a potential measure of broader consumption trends, particularly during periods of economic recovery. This indicator gained attention for being monitored by former Federal Reserve Chairman Alan Greenspan.
      </p>
      <h1 class="text-xl">Why SMUX500 ?</h1>
      <p class="text-justify	">The Men’s Underwear Index is an unconventional yet surprisingly insightful economic indicator, reflecting broader consumption trends during recovery periods. Owning the SMUI500 token makes you part of a community that values   understanding the economy.</p>
      

    </div>
    
    <ul class="pt-10">
        <li><a href="https://glenmont.co/the-mens-underwear-index-as-an-economic-indicator">https://glenmont.co/the-mens-underwear-index-as-an-economic-indicator</a></li>
        <li><a href="https://en.wikipedia.org/wiki/Men%27s_underwear_index">https://en.wikipedia.org/wiki/Men%27s_underwear_index</a></li>
        <li><a href="https://fred.stlouisfed.org/series/WPUSI094011#0">https://fred.stlouisfed.org/series/WPUSI094011#0</a></li>
        <li><a href="https://fortune.com/2023/02/15/alan-greenspan-mens-underwear-index-us-economy-inflation/">https://fortune.com/2023/02/15/alan-greenspan-mens-underwear-index-us-economy-inflation/</a></li>
      </ul>
 
    
  </div>
  
</template>

<script>
export default {
  data() {
    return {
      price: 0, // API'den gelen fiyat
      progressPercentage: 0, // Progress bar yüzdesi
      labels: [0, 0.1, 0.2, 0.3, 1], // Progress bar etiketleri
      images: [1, 2, 3, 4, 5], // Görsel yer tutucular
    };
  },
  computed: {
    currentRange() {
      // Fiyatın hangi aralıkta olduğunu hesapla
      const step = 0.1;
      return Math.min(Math.floor(this.price / step), this.images.length - 1);
    },
  },
  methods: {
    async fetchPrice() {
      try {
        const response = await fetch(
          "https://api.jup.ag/price/v2?ids=69FSWQK2bY6aqP8bTVErEMwwh7g5fC5Pve7JTxGbpump,So11111111111111111111111111111111111111112"
        );
        const data = await response.json();
        this.price = parseFloat(
          data.data["69FSWQK2bY6aqP8bTVErEMwwh7g5fC5Pve7JTxGbpump"].price
        );

        // Progress yüzdesini hesapla (0 ile 1 arasında)
        const maxPrice = 1;
        this.progressPercentage = Math.min(
          (this.price / maxPrice) * 100,
          100
        );
      } catch (error) {
        console.error("API'den fiyat alınamadı:", error);
      }
    },
  },
  mounted() {
    this.fetchPrice();
    setInterval(this.fetchPrice, 10000); // Fiyatı her 10 saniyede bir güncelle
  },
};
</script>

<style>
/* Tailwind CSS zaten projede */
</style>
