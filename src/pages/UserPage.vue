<template>
    <div class="mt-12 mx-auto max-w-2xl px-4 sm:px-6 lg:px-8 px-15 my-16">
        <div class="px-4 sm:px-0 text-center">
            <h3 class="text-2xl mt-4 font-semibold leading-7 text-gray-900">Thông tin cá nhân</h3>
            <p class="mt-4 text-lg leading-6 text-gray-500">Thông tin cá nhân chi tiết.</p>
            <button @click="openUpdateModal" class="border-black border w-10 h-10 rounded-xl mt-4 hover:bg-teal-200"><i class="fa-solid fa-pencil text-lg m-auto"></i></button>
        </div>
        <div class="mt-6 border-t border-gray-300" v-if="store.state.user != null">
            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0 border-t-2 border-gray-300">
                <dt class="text-base font-medium leading-6 text-gray-900">Họ
                </dt>
                <dd class="mt-1 text-base leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{
                    store.state.user.data.firstName }}
                </dd>
            </div>
            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0 border-t-2 border-gray-300">
                <dt class="text-base font-medium leading-6 text-gray-900">Tên
                </dt>
                <dd class="mt-1 text-base leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{
                    store.state.user.data.lastName }}
                </dd>
            </div>
            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0 border-t-2 border-gray-300">
                <dt class="text-base font-medium leading-6 text-gray-900">Giới tính
                </dt>
                <dd class="mt-1 text-base leading-6 text-gray-700 sm:col-span-2 sm:mt-0">
                    {{ store.state.user.data.gender }}
                </dd>
            </div>
            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0 border-t-2 border-gray-300">
                <dt class="text-base font-medium leading-6 text-gray-900">Số điện thoại </dt>
                <dd class="mt-1 text-base leading-6 text-gray-700 sm:col-span-2 sm:mt-0">
                    {{ store.state.user.data.phone }}</dd>
            </div>
            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0 border-t-2 border-gray-300">
                <dt class="text-base font-medium leading-6 text-gray-900">Ngày sinh </dt>
                <dd class="mt-1 text-base leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ store.state.user.data.dob
                    }}</dd>
            </div>
            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-0 border-y-2 border-gray-300">
                <dt class="text-base font-medium leading-6 text-gray-900">Địa chỉ
                </dt>
                <dd class="mt-1 text-base leading-6 text-gray-700 sm:col-span-2 sm:mt-0">{{ store.state.user.data.address }}</dd>
            </div>
        </div>
    </div>
    <TransitionRoot as="template" :show="isUpdateModalOpen">
        <Dialog as="div" class="fixed z-20 inset-0 overflow-y-auto" @close="closeUpdateModal">
            <div class="flex items-center justify-center min-h-screen">
                <DialogOverlay class="fixed inset-0 bg-black opacity-30" />
                <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 scale-95"
                    enter-to="opacity-100 scale-100" leave="ease-in duration-200" leave-from="opacity-100 scale-100"
                    leave-to="opacity-0 scale-95">
                    <DialogPanel class="bg-white rounded-lg p-6 max-w-md mx-auto z-10 w-96">
                        <form class="space-y-6" @submit.prevent="updateReader">
                            <div>
                                <label for="firstName" class="block text-base font-medium text-gray-700">Họ</label>
                                <input id="firstName" type="text" v-model="store.state.user.data.firstName"
                                    class="mt-1 block w-full border-gray-300 rounded-md shadow-sm p-2">
                            </div>
                            <div>
                                <label for="lastName" class="block text-base font-medium text-gray-700">Tên</label>
                                <input id="lastName" type="text" v-model="store.state.user.data.lastName"
                                    class="mt-1 block w-full border-gray-300 rounded-md shadow-sm p-2">
                            </div>
                            <div>
                                <label for="gender" class="block text-base font-medium text-gray-700">Giới tính</label>
                                <input id="gender" type="text" v-model="store.state.user.data.gender"
                                    class="mt-1 block w-full border-gray-300 rounded-md shadow-sm p-2">
                            </div>
                            <div>
                                <label for="phone" class="block text-base font-medium text-gray-700">Số điện thoại</label>
                                <input id="phone" type="text" v-model="store.state.user.data.phone"
                                    class="mt-1 block w-full border-gray-300 rounded-md shadow-sm p-2">
                            </div>
                            <div>
                                <label for="dob" class="block text-base font-medium text-gray-700">Ngày sinh</label>
                                <input id="dob" type="date" v-model="store.state.user.data.dob"
                                    class="mt-1 block w-full border-gray-300 rounded-md shadow-sm p-2">
                            </div>
                            <div>
                                <label for="address" class="block text-base font-medium text-gray-700">Địa chỉ</label>
                                <input id="address" type="text" v-model="store.state.user.data.address"
                                    class="mt-1 block w-full border-gray-300 rounded-md shadow-sm p-2">
                            </div>
                            <div class="flex justify-end space-x-2">
                                <button type="submit"
                                    class="px-4 py-2 bg-blue-600 text-white rounded-md">Cập nhật</button>
                                <button type="button" class="px-4 py-2 bg-gray-200 rounded-md"
                                    @click="closeUpdateModal">Hủy</button>
                            </div>
                        </form>
                    </DialogPanel>
                </TransitionChild>
            </div>
        </Dialog>
    </TransitionRoot>
</template>
<script setup>
import { ref, watchEffect } from 'vue';
import { useStore } from 'vuex';
import ReaderService from '@/services/reader.service';
import {
    Dialog,
    DialogPanel,
    TransitionChild,
    TransitionRoot,
} from '@headlessui/vue'
import { XMarkIcon } from '@heroicons/vue/24/outline'
import { FunnelIcon, MinusIcon, PlusIcon, Squares2X2Icon } from '@heroicons/vue/20/solid'
import { message } from 'antd';
const store = useStore();

watchEffect(async () => {
    await store.dispatch('fetchUser');
    console.log(store.state.user)
});
const isUpdateModalOpen = ref(false);

function openUpdateModal() {
    isUpdateModalOpen.value = true;
}

function closeUpdateModal() {
    isUpdateModalOpen.value = false;
}

const updateReader = async () => {
    try {
        await ReaderService.update(store.state.user.data._id, store.state.user.data);
        // Refresh the user data
        await store.dispatch('fetchUser');
        message.success("Cập nhật thành công")
        closeUpdateModal();
    } catch (error) {
        console.error('Failed to update the reader:', error);
    }
};
</script>