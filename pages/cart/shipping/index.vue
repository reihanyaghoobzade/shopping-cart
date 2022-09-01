<template>
  <section class="container mx-auto">
    <div class="flex flex-col gap-4">
      <div class="flex items-center gap-4 p-4 bg-white rounded-lg">
        <nuxt-link to="/cart">
          <img src="~/assets/images/left-arrow.png" alt="" />
        </nuxt-link>
        <span class="font-bold text-xl">Choose Adderess</span>
      </div>
      <div
        v-if="!form.name"
        class="flex flex-col gap-4 justify-center bg-white p-4 rounded-lg"
      >
        <div class="flex gap-4 items-center">
          <img class="w-4 h-4" src="~/assets/images/location.png" alt="" />
          <span class="text-gray-500">Receiver address</span>
        </div>
        <div class="flex items-center justify-between">
          <div class="px-8 text-semibold text-lg">
            You have not entered an address yet!
          </div>
          <div
            class="mx-8 px-16 py-2 font-bold border border-purple-500 text-purple-700 hover:bg-[#C084FC30] rounded transition-all cursor-pointer"
            @click="showAddressGetter = true"
          >
            Add address &nbsp; &nbsp;+
          </div>
        </div>
      </div>
      <div
        v-else
        class="flex flex-col gap-4 justify-center bg-white p-4 rounded-lg"
      >
        <div class="flex gap-4 items-center">
          <img class="w-4 h-4" src="~/assets/images/location.png" alt="" />
          <span class="text-gray-500">Receiver address</span>
        </div>
        <div>{{ form.name }}</div>
        <div>{{ form.address }}</div>
        <div class="flex gap-8">
          <div>Postal number: {{ form.postalCode }}</div>
          <div>Phone number: {{ form.phoneNumber }}</div>
        </div>
      </div>
      <AddressGetter
        v-if="showAddressGetter"
        @close="showAddressGetter = false"
        @sendAddress="sendAddress($event)"
      />
    </div>
  </section>
</template>

<script>
export default {
  name: 'AddressPage',
  head() {
    return {
      title: 'Cart | Address',
    }
  },
  data() {
    return {
      showAddressGetter: true,
      form: {},
    }
  },
  methods: {
    sendAddress(event) {
      console.log(event)
      this.form = { ...event }
      this.showAddressGetter = false
    },
  },
}
</script>
