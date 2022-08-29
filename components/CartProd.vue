<template>
  <div
    class="w-full grid grid-cols-4 gap-12 items-start bg-white shadow-lg hover:shadow-xl p-8 rounded-lg transition duration-300"
  >
    <div class="col-span-1 justify-self-center self-center">
      <img class="w-40 h-40 rounded" :src="item.image" alt="" />
    </div>
    <div
      class="col-span-3 flex flex-col gap-8 justify-between items-start text-justify"
    >
      <nuxt-link
        class="font-bold text-xl hover:text-purple-400 transition"
        :to="`/${item.id}`"
      >
        {{ item.title }}
      </nuxt-link>
      <div class="w-full truncate">{{ item.description }}</div>
      <div class="w-full flex justify-between items-center">
        <div class="flex items-center gap-4">
          <img
            class="w-6 h-6 cursor-pointer"
            src="~/assets/images/plus.png"
            alt=""
            @click="$emit('addOne', item)"
          />
          <div
            class="bg-gradient-to-br from-[#6F00B7] via-[#3B82F6] to-[#E200F1] rounded"
          >
            <span class="block h-5 leading-6 text-center w-12 m-0.5 bg-white">{{ item.quantity }}</span>
        </div>
          <img
            class="w-6 h-6 cursor-pointer"
            src="~/assets/images/minus.png"
            alt=""
            @click="$emit('removeOne', item)"
          />
          <img
            class="w-6 h-6 cursor-pointer"
            src="~/assets/images/bin.png"
            alt=""
            @click="$emit('removeCart', item)"
          />
        </div>
        <span class="font-bold">{{ totalPrice }} $</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShowCartComponent',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  emits: ['removeOne', 'removeCart'],
  computed: {
    totalPrice() {
      return (this.item.price * this.item.quantity).toFixed(2)
    },
  },
}
</script>
