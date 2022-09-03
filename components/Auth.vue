<template>
  <div
    class="absolute flex flex-col justify-center items-center top-0 left-0 min-h-screen w-screen bg-[#00000070] z-20"
  >
    <div class="flex flex-col gap-4 w-1/5 p-8 bg-white rounded-lg">
      <div class="flex flex-col gap-2">
        <label for="email"
          >E-Mail Address
          <span class="text-red-400">*</span>
        </label>
        <input
          id="email"
          v-model.lazy="user.email"
          type="email"
          placeholder="E-Mail "
          class="p-2 border-2 border-black outline-none rounded"
        />
      </div>
      <div class="flex flex-col gap-2">
        <label for="password"
          >Password
          <span class="text-red-400">*</span>
        </label>
        <input
          id="password"
          v-model.lazy="user.password"
          type="password"
          placeholder="Paswword"
          class="w-full p-2 border-2 border-black outline-none rounded"
        />
      </div>
      <div
        class="text-red-500"
        :class="{ block: showError, hidden: !showError }"
      >
        Email or Password is incorrect!
      </div>
      <div class="flex gap-4 mt-4">
        <div
          class="w-full text-center bg-purple-400 font-bold text-white py-2 transition ring-offset-2 ring-purple-400 hover:ring-2 rounded-lg cursor-pointer"
          @click="submitForm"
        >
          {{ isLogin ? 'Login' : 'Sign up' }}
        </div>
        <div
          class="w-full text-center py-2 border-2 border-purple-400 text-purple-400 font-bold transition hover:bg-[#C084FC40] rounded-lg cursor-pointer"
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
  name: 'AuthComponent',
  emits: ['close'],
  data() {
    return {
      showError: false,
      user: {
        email: this.email,
        password: this.password,
      },
    }
  },
  computed: {
    isLogin() {
      let isLogin
      localStorage.Login ? (isLogin = true) : (isLogin = false)
      return isLogin
    },
  },
  methods: {
    submitForm() {
      if (this.isLogin) {
        const user = JSON.parse(localStorage.Login)
        user.email === this.user.email && user.password === this.user.password
          ? this.$emit('close')
          : (this.showError = true)
      } else {
        localStorage.Login = JSON.stringify(this.user)
        this.$emit('close')
      }
    },
  },
}
</script>

<style></style>
