<template>
  <header class="px-2 w-full bg-white">
    <section class="container mx-auto">
      <div class="flex justify-between items-center">
        <div>
          <nuxt-link to="/">
            <img class="w-24" src="~/assets/images/logo.png" alt="logo" />
          </nuxt-link>
        </div>
        <div class="flex gap-8">
          <div class="flex flex-col gap-2 items-center justify-center">
            <img src="~/assets/images/profile.png" alt="" />
            <span class="text-purple-700 font-semibold">Login / Sign Up</span>
            <!-- <span>پروفایل</span> -->
          </div>
          <nuxt-link
            to="/cart"
            class="flex flex-col gap-2 items-center justify-center relative"
          >
            <div
              v-if="cartNumber"
              class="block absolute bottom-11 right-2 animate-ping w-3 h-3 text-center text-white text-sm bg-purple-400 rounded-full"
            >
              &nbsp;
            </div>
            <img src="~/assets/images/shopping-cart.png" alt="shopping-cart" />
            <span class="text-purple-700 font-semibold">Cart</span>
          </nuxt-link>
        </div>
      </div>
    </section>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  computed: {
    cartNumber() {
      let number = false
      if (this.$route && process.client) {
        JSON.parse(localStorage.getItem('carts')).length === 0
          ? (number = false)
          : (number = true)
      }
      return number
    },
  },
}
</script>

<style></style>
