<template>
  <div class="flex flex-col items-center justify-center min-h-screen max-w-3xl mx-auto scale-150	">
    <!-- Görseller -->
    <h1 class="text-3xl">Solana Men's underwaer index = SMUI500</h1>
    <p>CA : FYZJXcT6XPPfPDVg9L1vjwTxMAFLLWcQe5aFvpchpump</p>

    <div class="flex justify-around w-full mb-8 gap-4">
      <div
        v-for="(image, index) in images"
        :key="index"
        class="w-24 h-24 rounded-md  flex items-center justify-center p-4"
       
      >
        <img :src="(index) + '.png'" alt="">
      </div>
    </div>

    <!-- Progress Bar -->
    <div class="relative w-full max-w-3xl">
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
      <div class="flex justify-between mt-2 text-sm  text-center">
        {{  price }}$
      </div>
    </div>
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
          "https://api.jup.ag/price/v2?ids=8x5VqbHA8D7NkD52uNuS5nnt3PwA8pLD34ymskeSo2Wn,So11111111111111111111111111111111111111112"
        );
        const data = await response.json();
        this.price = parseFloat(
          data.data["8x5VqbHA8D7NkD52uNuS5nnt3PwA8pLD34ymskeSo2Wn"].price
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
