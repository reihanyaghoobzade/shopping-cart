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
          <div
            class="flex flex-col gap-2 items-center justify-center"
            @click="showAuth = true"
          >
            <img src="~/assets/images/profile.png" alt="" />
            <span v-if="!isLogin" class="text-purple-700 font-semibold"
              >Login / Sign Up</span
            >
            <span v-if="isLogin" class="text-purple-700 font-semibold"
              >Profile</span
            >
          </div>
          <Auth v-if="showAuth" @close="showAuth = false" />
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
      <hr />
      <div
        class="flex gap-4 items-center py-4 w-1/4 relative"
        @mouseover="showCategories = true"
        @mouseleave="showCategories = false"
      >
        <span class="font-bold text-2xl">Categories</span>
        <img
          src="~/assets/images/arrow.png"
          alt=""
          class="transition-all duration-200"
          :class="{ 'rotate-180': showCategories }"
        />
        <div
          class="absolute top-full -left-4 flex flex-col gap-4 px-4 text-lg font-bold bg-white h-0 w-full overflow-hidden transition-all z-20 rounded-b-lg"
          :class="{ 'h-56': showCategories }"
          @mouseover="showCategories = true"
          @mouseleave="showCategories = false"
        >
          <nuxt-link
            to="/category/electronics"
            class="w-full hover:text-purple-700 transition"
            >Electronics</nuxt-link
          >
          <hr />
          <nuxt-link
            to="/category/jewelery"
            class="w-full hover:text-purple-700 transition"
            >Jewelery</nuxt-link
          >
          <hr />
          <nuxt-link
            to="/category/men's clothing"
            class="w-full hover:text-purple-700 transition"
            >Men's clothing</nuxt-link
          >
          <hr />
          <nuxt-link
            to="/category/women's clothing"
            class="w-full hover:text-purple-700 transition"
            >Women's clothing</nuxt-link
          >
          <hr />
        </div>
      </div>
    </section>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
    return {
      showCategories: false,
      showAuth: false,
    }
  },
  computed: {
    cartNumber() {
      if (this.$route && process.client) {
        const number = JSON.parse(localStorage.carts).length
        if (number !== 0) {
          return true
        } else {
          return false
        }
      } else {
        return false
      }
    },
    isLogin() {
      if (process.client) {
        return localStorage.Login || false
      } else {
        return false
      }
    },
  },
  methods: {},
}
</script>
