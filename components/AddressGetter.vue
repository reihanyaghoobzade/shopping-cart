<template>
  <div
    class="absolute flex flex-col justify-center items-center top-0 left-0 min-h-screen w-screen bg-[#00000070]"
  >
    <div class="flex flex-col gap-8 w-1/2 p-8 h-2/3 bg-white rounded-lg">
      <div class="flex flex-col gap-4">
        <label for="recipient-name"
          >The name of the recipient of the order
          <span class="text-red-400">*</span>
        </label>
        <input
          id="recipient-name"
          v-model.lazy="form.name"
          type="text"
          placeholder="Name"
          class="p-2 border-2 border-black outline-none rounded"
          :class="{ 'border-red-400': border.name }"
        />
      </div>
      <div class="flex flex-col gap-4">
        <label for="city"
          >Select your city and province of residence
          <span class="text-red-400">*</span>
        </label>
        <div class="w-full flex gap-4">
          <input
            id="city"
            v-model.lazy="form.city"
            type="text"
            placeholder="City"
            class="w-full p-2 border-2 border-black outline-none rounded"
            :class="{ 'border-red-400': border.city }"
          />
          <input
            id="city"
            v-model.lazy="form.province"
            type="text"
            placeholder="Province"
            class="w-full p-2 border-2 border-black outline-none rounded"
            :class="{ 'border-red-400': border.province }"
          />
        </div>
      </div>
      <div class="flex flex-col gap-4">
        <label for="address"
          >Exact mailing address
          <span class="text-red-400">*</span>
        </label>
        <input
          id="address"
          v-model.lazy="form.address"
          type="text"
          placeholder="Address"
          class="p-2 border-2 border-black outline-none rounded"
          :class="{ 'border-red-400': border.address }"
        />
      </div>
      <div class="flex gap-4">
        <div class="w-full flex flex-col gap-4">
          <label for="postal-code"
            >Postal code
            <span class="text-red-400">*</span>
          </label>
          <input
            id="postal-code"
            v-model.lazy="form.postalCode"
            type="text"
            placeholder="Example: 1234567890"
            class="w-full p-2 border-2 border-black outline-none rounded"
            :class="{ 'border-red-400': border.postalCode }"
          />
        </div>
        <div class="w-full flex flex-col gap-4">
          <label for="phone-number"
            >The phone number of the order recipient
            <span class="text-red-400">*</span></label
          >
          <input
            id="phone-number"
            v-model.lazy="form.phoneNumber"
            type="text"
            placeholder="Example: 0912*******"
            class="w-full p-2 border-2 border-black outline-none rounded"
            :class="{ 'border-red-400': border.phoneNumber }"
          />
        </div>
      </div>
      <div class="flex justify-end items-center gap-4">
        <div
          class="py-2 w-24 text-center bg-purple-500 font-bold text-white rounded-lg border-2 border-purple-500 transition ring-offset-2 ring-purple-400 hover:ring-2 cursor-pointer"
          @click="sendAddress"
        >
          Ok
        </div>
        <div
          class="py-2 w-24 text-center border-2 border-purple-500 font-bold text-purple-500 hover:bg-[#C084FC40] transition rounded-lg cursor-pointer"
          @click="$emit('close')"
        >
          Cancel
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddressGetterComponent',
  emits: ['sendAddress', 'close'],
  data() {
    return {
      form: {
        name: '',
        city: '',
        province: '',
        address: '',
        postalCode: '',
        phoneNumber: '',
      },
      border: {
        name: false,
        city: false,
        province: false,
        address: false,
        postalCode: false,
        phoneNumber: false,
      },
    }
  },
  methods: {
    sendAddress() {
      Object.keys(this.border).forEach((key) => {
        this.border[key] = false
      })

      if (
        this.form.name &&
        this.form.city &&
        this.form.province &&
        this.form.address &&
        this.form.phoneNumber &&
        this.form.postalCode
      )
        this.$emit('sendAddress', this.form)

      if (!this.form.name) this.border.name = true
      if (!this.form.city) this.border.city = true
      if (!this.form.province) this.border.province = true
      if (!this.form.address) this.border.address = true
      if (!this.form.phoneNumber) this.border.phoneNumber = true
      if (!this.form.postalCode) this.border.postalCode = true
    },
  },
}
</script>

<style></style>
