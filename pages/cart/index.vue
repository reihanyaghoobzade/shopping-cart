<template>
  <main class="px-2 py-10 w-full">
    <div class="container mx-auto">
      <div
        class="flex justify-between items-center w-full bg-white rounded-lg cursor-pointer relative active"
        :class="{
          'after:left-[calc(10%/2)]': left,
          'after:right-[calc(10%/2)]': right,
        }"
      >
        <div
          class="w-full text-center text-lg font-semibold py-4"
          :class="{ 'text-purple-400': left }"
          @click=";(left = true) && (right = false)"
        >
          Shopping Cart
        </div>
        <span class="block h-10 w-[2px] bg-gray-200"></span>
        <div
          class="w-full text-center text-lg font-semibold py-4"
          :class="{ 'text-purple-400': right }"
          @click=";(right = true) && (left = false)"
        >
          Next Shopping Cart
        </div>
      </div>
      <div
        v-if="carts.length === 0"
        class="flex flex-col gap-8 justify-center items-center mt-40 w-full"
      >
        <img src="~/assets/images/empty-cart.png" alt="" />
        <div class="flex flex-col justify-center items-center">
          <span class="text-gray-700">Your shopping cart is empty!</span>
          <span class="text-gray-500"
            >It looks like you haven't added anything to your cart yet.</span
          >
        </div>
      </div>
      <div v-else class="grid grid-cols-5 justify-start items-start gap-8 mt-4">
        <div class="col-span-3 flex flex-col justify-center items-center gap-4">
          <CartProd
            v-for="cart in carts"
            :key="cart.title"
            :item="cart"
            @addOne="addOne"
            @removeOne="removeOne"
            @removeCart="removeCart"
          />
        </div>
        <div
          class="col-span-2 w-full p-8 flex flex-col gap-6 justify-self-center bg-white rounded-lg shadow-lg"
        >
          <div class="flex justify-between text-xl font-semibold">
            <span>Number of orders:</span>
            <span>{{ carts.length }}</span>
          </div>
          <hr class="mx-10" />
          <div class="flex justify-between text-xl font-semibold">
            <span>The amount payable</span>
            <span>{{ totalPrice }} $</span>
          </div>
          <nuxt-link
            to="/cart/shipping"
            class="w-full bg-purple-400 text-white text-xl text-center py-2 mt-4 rounded-lg transition ring-offset-2 ring-purple-400 hover:ring-2"
          >
            Continue
          </nuxt-link>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'CartPage',
  head() {
    return {
      title: 'Cart',
    }
  },
  data() {
    return {
      carts: [],
      right: false,
      left: true,
    }
  },
  mounted() {
    this.carts = JSON.parse(localStorage.getItem('carts')) || []
  },
  computed: {
    totalPrice() {
      let total = 0
      this.carts.forEach((cart) => {
        total += cart.price * cart.quantity
      })

      return total.toFixed(2)
    },
  },
  methods: {
    addOne(item) {
      const index = this.carts.findIndex((cart) => {
        return cart.id === item.id
      })

      item.quantity++
      this.carts.splice(index, 1, item)
      localStorage.setItem('carts', JSON.stringify(this.carts))
    },
    removeOne(item) {
      const index = this.carts.findIndex((cart) => {
        return cart.id === item.id
      })

      item.quantity--

      item.quantity === 0
        ? this.carts.splice(index, 1)
        : this.carts.splice(index, 1, item)

      localStorage.setItem('carts', JSON.stringify(this.carts))
    },
    removeCart(item) {
      const index = this.carts.findIndex((cart) => {
        return cart.id === item.id
      })
      this.carts.splice(index, 1)
      localStorage.setItem('carts', JSON.stringify(this.carts))
    },
  },
}
</script>

<style scoped>
.active::after {
  content: ' ';
  width: 40%;
  height: 3px;
  background-color: blueviolet;
  margin: 0 auto;
  position: absolute;
  display: block;
  bottom: 0px;
}
</style>
>
