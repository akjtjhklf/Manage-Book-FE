<template>
  <div class="flex min-h-full flex-1 flex-col justify-center items-center py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <h2 class="mt-12 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Đăng nhập với tài khoản
        của bạn
      </h2>
    </div>

    <div class="my-8 lg:w-2/5 md:w-1/2 sm:w-full w-full px-5 py-10 rounded-md  shadow-2xl">
      <form class="space-y-6" @submit.prevent="signIn">
        <div>
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Tên người dùng</label>
          <div class="mt-2">
            <input v-model="username" id="email" name="email" type="text"
              class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Mật khẩu</label>
          </div>
          <div class="mt-2">
            <input v-model="password" id="password" name="password" type="password" autocomplete="current-password"
              class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
          </div>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-1 lg:grid-cols-2 justify-between">
          <div class="text-sm">
            <a href="#" class="font-semibold text-rose-600 hover:text-black">Quên mật khẩu?</a>
          </div>

          <div class="text-sm">
            <div class="flex items-center">
              <input type="checkbox" id="agree" name="agree"
                class="lg:ml-auto h-3 w-3 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded-full">
              <label for="agree" class="ml-2 font-semibold text-rose-600 hover:text-black">Tôi đồng ý với các điều khoản
                dịch vụ</label>
            </div>
          </div>

        </div>
        <div class="grid grid-cols-1 gap-4 sm:grid-cols-1 md:grid-cols-1 lg:grid-cols-2 justify-between">
          <div>
            <button type="submit"
              class="flex w-1/2 mx-auto justify-center rounded-md bg-rose-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-gray-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Đăng
              nhập</button>
          </div>
          <div>
            <button type="button" @click="handleSignUp"
              class="flex w-1/2 mx-auto justify-center rounded-md bg-black px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-gray-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Đăng
              ký</button>
          </div>
        </div>

      </form>
    </div>
  </div>
</template>

<script setup>
import { useStore } from 'vuex';
import ReadersService from '@/services/reader.service';
import { message } from 'antd';
import { useRouter } from 'vue-router';
import { getCurrentInstance, ref } from 'vue';
const instance = getCurrentInstance();
const store = useStore();
const router = useRouter();
const username = ref('');
const password = ref('');

const signIn = async () => {
  try {
    if (!username.value || !password.value) {
      message.error('Vui lòng điền đầy đủ thông tin.');
      return;
    }

    const token = await ReadersService.signIn({ username: username.value, password: password.value });
    localStorage.setItem('token', token.token.token);

    if (token.token.isSuccess == true) {
      message.success(token.token.message)
      await store.dispatch('fetchUser');
      router.push("/")
    }
    else {
      message.error(token.token.message)
    }
  } catch (error) {
    message.error('Đăng nhập không thành công.');
  }
}
const handleSignUp = () => {
  instance.emit('signUp'); // Emit the signUp event to the parent component
}
</script>
