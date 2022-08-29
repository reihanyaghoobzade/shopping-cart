<template>
  <main class="px-2 w-full">
    <div class="container mx-auto">
      <div class="grid grid-cols-12 gap-12 justify-center items-center">
        <div class="col-span-6">
          <img class="w-[36rem] h-[44rem]" :src="item.image" alt="" />
        </div>
        <div class="col-span-6 flex flex-col gap-8 text-justify">
          <div class="text-4xl font-bold">{{ item.title }}</div>
          <div class="text-lg text-gray-700">{{ item.description }}</div>
          <div class="flex justify-between items-center">
            <span class="text-lg font-semibold">{{ item.price }} $</span>
            <div
              class="px-4 py-2 border-2 border-purple-400 text-purple-400 font-semibold hover:text-white hover:bg-purple-400 transition rounded-lg cursor-pointer"
              @click="addToCart"
            >
              Add to cart
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'SingleProductPage',
  async asyncData(context) {
    const response = await context.$axios.$get(`/products/${context.params.id}`)
    response.quantity = 0
    return { item: { ...response } }
  },
  methods: {
    addToCart() {
      const carts = JSON.parse(localStorage.getItem('carts')) || []

      if (carts.some((item) => item.id === this.item.id)) {
        const cart = carts.find((item) => item.id === this.item.id)
        carts.pop(cart)
        this.item.quantity = cart.quantity + 1
      } else {
        this.item.quantity = 1
      }

      carts.push(this.item)
      localStorage.setItem('carts', JSON.stringify(carts))
    },
  },
}
</script>

<style></style>
