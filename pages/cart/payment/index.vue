<template>
  <main class="container mx-auto">
    <section class="flex flex-col gap-4">
      <div class="flex items-center gap-4 p-4 bg-white rounded-lg">
        <nuxt-link to="/cart/shipping">
          <img src="~/assets/images/left-arrow.png" alt="" />
        </nuxt-link>
        <span class="font-bold text-xl">Payment</span>
      </div>
      <div class="flex gap-4 items-center p-4 bg-white rounded-lg">
        <div class="flex items-center gap-4">
          <label class="text-lg font-semibold" for="discount-code"
            >Discount code:
          </label>
          <input
            id="discount-code"
            v-model.lazy="discountCode"
            type="text"
            placeholder="Enter here"
            class="border-2 border-black p-2 rounded"
          />
        </div>
        <div
          class="px-12 py-2 text-white font-bold bg-purple-500 rounded border-2 border-purple-500 cursor-pointer"
          @click="applyDiscountCode"
        >
          Apply
        </div>
      </div>
      <div class="flex flex-col gap-4 bg-white p-4 rounded-lg">
        <div class="text-xl font-bold">
          Price of products:
          <span>{{ totalPrice }} $</span>
        </div>
        <div class="text-xl font-bold text-purple-500">
          Shipping discount:
          <span>{{ shippingDiscount }} $</span>
        </div>
        <div class="text-xl font-bold">
          Payable: <span>{{ payable }} $</span>
        </div>
        <div
          class="self-end py-2 px-12 bg-purple-500 text-white font-bold rounded-lg transition ring-offset-2 ring-purple-500 hover:ring-2 cursor-pointer"
        >
          Payment
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'PaymentPage',
  data() {
    return {
      discountCode: '',
      discountPercent: 0,
      shippingDiscount: 0,
      totalPrice: 0,
      payable: 0,
    }
  },
  head() {
    return {
      title: 'Cart | Payment',
    }
  },
  mounted() {
    JSON.parse(localStorage.carts).forEach((cart) => {
      this.payable = this.totalPrice += cart.price * cart.quantity
    })
  },
  methods: {
    applyDiscountCode() {
      if (this.discountCode) {
        this.discountPercent = Math.floor(Math.random() * 16) + 5
        this.shippingDiscount = (
          this.discountPercent *
          (this.totalPrice / 100)
        ).toFixed(2)
        this.payable = (
          this.totalPrice -
          this.totalPrice * (this.discountPercent / 100)
        ).toFixed(2)
      }
    },
  },
}
</script>

<style></style>
