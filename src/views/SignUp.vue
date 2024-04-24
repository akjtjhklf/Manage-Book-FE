<template>
    <div class="flex min-h-full flex-1 flex-col justify-center items-center py-10 lg:px-8">
        <div class="sm:mx-auto sm:w-full sm:max-w-sm">
            <h2 class="mt-0 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Đăng ký tài khoản
                của bạn</h2>
        </div>
        <div class="my-6 lg:w-1/2 md:w-1/2 sm:w-full w-full px-5 py-10 rounded-md  shadow-2xl">
            <form class="space-y-6" method="POST">
                <div class="grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-2">
                    <div>
                        <label for="userName" class="block text-sm font-medium leading-6 text-gray-900">Tên người
                            dùng</label>
                        <div class="mt-2">
                            <input id="userName" name="username" type="text" v-model="username"
                                class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
                        </div>
                    </div>

                    <div>
                        <label for="phone" class="block text-sm font-medium leading-6 text-gray-900">Số điện
                            thoại</label>
                        <div class="mt-2">
                            <input id="phone" name="phone" type="text" v-model="phone"
                                class="appearance-none block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
                        </div>
                    </div>

                    <div>
                        <div class="flex items-center justify-between">
                            <label for="firstName" class="block text-sm font-medium leading-6 text-gray-900">Họ </label>
                        </div>
                        <div class="mt-2">
                            <input id="firstName" name="firstName" type="text" v-model="firstName"
                                class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
                        </div>
                    </div>

                    <div>
                        <div class="flex items-center justify-between">
                            <label for="lastName" class="block text-sm font-medium leading-6 text-gray-900">Tên</label>
                        </div>
                        <div class="mt-2">
                            <input id="lastName" name="lastName" type="text" v-model="lastName"
                                class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
                        </div>
                    </div>

                    <div>
                        <div class="flex items-center justify-between">
                            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Mật
                                khẩu</label>
                        </div>
                        <div class="mt-2">
                            <input id="password" name="password" type="password" v-model="password"
                                class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
                        </div>
                    </div>

                    <div>
                        <div class="flex items-center justify-between">
                            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Nhập lại mật
                                khẩu
                            </label>
                        </div>
                        <div class="mt-2">
                            <input id="confirmpassword" name="confirmpassword" type="password" v-model="confirmPassword"
                                class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
                        </div>
                    </div>

                    <div>
                        <div class="flex items-center justify-between">
                            <label for="gender" class="block text-sm font-medium leading-6 text-gray-900">Giới
                                tính</label>
                        </div>

                        <select id="gender" name="gender" v-model="gender"
                            class="mt-2 py-2 block w-full rounded-md border-0 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6">
                            <option class="rounded-md">Male</option>
                            <option class="rounded-md">Female</option>
                        </select>

                    </div>

                    <div>
                        <div class="flex items-center justify-between">
                            <label for="dob" class="block text-sm font-medium leading-6 text-gray-900">Ngày sinh</label>
                        </div>
                        <div class="mt-2">
                            <input id="dob" name="dob" type="date" v-model="dob"
                                class="block w-full rounded-md border-0 py-1.5 px-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 sm:text-sm sm:leading-6" />
                        </div>
                    </div>
                </div>
                <div>
                    <div class="flex items-center justify-between">
                        <label for="address" class="block text-sm font-medium leading-6 text-gray-900">Địa chỉ</label>
                    </div>
                    <div class="mt-2">
                        <input id="address" name="address" type="text" v-model="address"
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
                            <label for="agree" class="ml-2 font-semibold text-rose-600 hover:text-black">Tôi đồng ý với
                                các điều khoản dịch vụ</label>
                        </div>
                    </div>

                </div>
                <div class="grid grid-cols-1 gap-4 sm:grid-cols-1 md:grid-cols-1 lg:grid-cols-2 justify-between">
                    <div>
                        <button type="submit" @click.prevent="signUp"
                            class="flex w-1/2 mx-auto justify-center rounded-md bg-rose-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-gray-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Đăng
                            ký</button>
                    </div>
                    <div>
                        <button type="button" @click.prevent="handleSignIn"
                            class="flex w-1/2 mx-auto justify-center rounded-md bg-gray-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-gray-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Đăng
                            nhập</button>
                    </div>
                </div>

            </form>
        </div>

    </div>
</template>

<script setup>
import { getCurrentInstance, ref } from 'vue';
import ReadersService from '@/services/reader.service'; // Đảm bảo import đúng đường dẫn đến ReadersService
import { message } from 'antd';

const instance = getCurrentInstance();
const username = ref('');
const phone = ref('');
const firstName = ref('');
const lastName = ref('');
const password = ref('');
const confirmPassword = ref('');
const gender = ref('');
const dob = ref('');
const address = ref('');


const signUp = async () => {
    try {
        if (!username.value || !password.value || !confirmPassword.value || !firstName.value || !lastName.value || !phone.value || !gender.value || !dob.value || !address.value) {
            message.error('Vui lòng điền đày đủ thông tin!');
            return;
        }
        const userData = {
            username: username.value,
            phone: phone.value,
            firstName: firstName.value,
            lastName: lastName.value,
            password: password.value,
            confirmPassword: confirmPassword.value,
            gender: gender.value,
            dob: dob.value,
            address: address.value
        };

        // Gọi hàm signUp từ ReadersService
        const response = await ReadersService.signUp(userData);

        if (response.isSuccess == true) {
            message.success(response.message)
            handleSignIn()
        }
        else {
            message.error(response.message)
        }
    } catch (error) {
        // Xử lý lỗi nếu đăng ký không thành công
        message.error('Đăng ký không thành công!');
    }
}
const handleSignIn = () => {
    instance.emit('signIn'); // Emit the signIn event to the parent component
}
</script>