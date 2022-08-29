<template>
  <main class="px-2 py-10 w-full">
    <div class="container mx-auto">
      <div class="grid grid-cols-4 gap-12 items-center justify-center">
        <Product v-for="item in items" :key="item.id" :item="item" />
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'IndexPage',
  async asyncData(context) {
    const response = await context.$axios.$get('/products')
    return { items: { ...response } }
  },
}
</script>
