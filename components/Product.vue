<template>
  <nuxt-link
    :to="`/${item.id}`"
    class="col-span-1 flex flex-col gap-8 justify-center items-center rounded shadow-xl hover:shadow-2xl transition duration-300 py-8 bg-white"
  >
    <img class="w-44 h-44" :src="item.image" alt="" />
    <div class="flex flex-col gap-4 items-center">
      <div
        class="text-center truncate w-60 hover:text-purple-500 transition text-xl font-bold"
      >
        {{ item.title }}
      </div>
      <div class="flex jutify-center items-center gap-4">
        <div class="text-lg font-bold">{{ item.price }} $</div>
      </div>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: 'ProductComponent',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style></style>
