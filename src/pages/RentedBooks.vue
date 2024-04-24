<template>
  <div class="mt-12 mx-auto max-w-10xl px-4 sm:px-6 lg:px-8">
    <div class="px-4 sm:px-0 text-center">
      <h3 class="text-2xl font-semibold leading-7 text-gray-900 text-center">THÔNG TIN THUÊ SÁCH</h3>
      <p class="mt-1 text-lg leading-6 text-gray-500 text-center">Thông tin thuê sách chi tiết.</p>
    </div>
    <div class="mt-6 border-t border-gray-300">
      <ul role="list">
        <li v-for="track in tracks" :key="track._id"
          class="flex flex-col gap-x-6 py-5 px-12 my-10 bg-gray-200 shadow-2xl rounded-xl">
          <div class="flex justify-between mb-4">
            <div class="flex min-w-0 gap-x-4 my-3">
              <img class="h-full w-full max-w-32 flex-none bg-gray-50 rounded-xl" :src="track.book.bookPicture" alt="" />
              <div class="min-w-0 flex-auto">
                <p class="text-lg font-semibold leading-6 text-gray-900 mt-3">{{ track.book.name }}</p>
                <p class="text-lg font-semibold leading-6 text-gray-500 mt-3">{{ track.book.author.name }}</p>
              </div>
            </div>
            <div class="shrink-0 sm:flex sm:flex-col sm:items-end my-3 hidden lg:flex">
              <p class="text-lg font-semibold leading-6 text-gray-900 mt-3">{{ track.book.price }} VNĐ/Ngày</p>
              <p v-if="track.borroweddate" class="mt-1 text-md leading-5 text-gray-500">
                Rent at: <time :datetime="track.borroweddate">{{ track.borroweddate }}</time>
              </p>
            </div>
          </div>
          <div class="border-t-2 border-gray-400 text-right">
            <p v-if="track.borroweddate" class="mt-1 text-md leading-5 text-gray-500">
              Total: {{ totalPay(track) }} VND
            </p>
            <button type="button" class="mt-3 px-5 py-3 rounded-md border-black border-2 ease-in-out duration-300 hover:border-rose-600 hover:bg-red-300" @click="openModal(track)">Trả
              sách</button>
          </div>
        </li>
      </ul>
    </div>
  </div>
  <div v-if="showModal" class="fixed z-10 inset-0 overflow-y-auto">
    <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
      <div class="fixed inset-0 transition-opacity" aria-hidden="true">
        <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
      </div>
      <div
        class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full">
        <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
          <div class="sm:flex sm:items-start">
            <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
              <h3 class="text-lg leading-6 font-medium text-gray-900">
                Trả Sách
              </h3>
              <div class="mt-2">
                <p class="text-md text-gray-700">
                  Bạn có chắc chắn muốn trả lại sách "{{ selectedTrack.book.name }}" không? Tổng số tiền cần phải thanh
                  toán là {{
                    totalPay(selectedTrack) }} VND.
                </p>
              </div>
            </div>
          </div>
        </div>
        <div class="bg-gray-50 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
          <button type="button"
            class="w-full inline-flex justify-center rounded-md border border-transparent shadow-sm px-4 py-2 bg-blue-600 text-base font-medium text-white hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 sm:ml-3 sm:w-auto sm:text-sm"
            @click="confirmReturn">
            Confirm
          </button>
          <button type="button"
            class="mt-3 w-full inline-flex justify-center rounded-md border border-gray-300 shadow-sm px-4 py-2 bg-white text-base font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 sm:mt-0 sm:w-auto sm:text-sm"
            @click="closeModal">
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import tracksService from '@/services/tracks.service';
import { ref, watchEffect } from 'vue';
import { useStore } from 'vuex';
const tracks = ref([]);
const store = useStore();
const now = ref(new Date());
const showModal = ref(false);
const selectedTrack = ref(null);

watchEffect(async () => {
  await store.dispatch('fetchUser');
  if (store.state.user.data && store.state.user.data._id) {
    const allTracks = await tracksService.getFiltered({ userId: store.state.user.data._id });
    tracks.value = allTracks.data.map(track => {
      const date = new Date(track.borroweddate);
      const formattedDate = date.getFullYear() + '-' + (date.getMonth() + 1).toString().padStart(2, '0') + '-' + date.getDate().toString().padStart(2, '0');
      return {
        id: track._id,
        readerid: track.readerid,
        book: track.book,
        borroweddate: formattedDate,
      }
    });
  }
});

const totalPay = (track) => {
  const borrowedDate = new Date(track.borroweddate);
  if (isNaN(borrowedDate)) {
    return 'Invalid date';
  }
  const diffTime = Math.abs(now.value.getTime() - borrowedDate.getTime());
  const diffDays = Math.floor(diffTime / (1000 * 60 * 60 * 24));
  return diffDays * track.book.price;
};

const openModal = (track) => {
  selectedTrack.value = track;
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
};

const confirmReturn = async () => {
  await returnBook(selectedTrack.value);
  closeModal();
};

const returnBook = async (track) => {
  try {
    await tracksService.delete(track.id);
    tracks.value = tracks.value.filter(t => t.id !== track.id);
  } catch (error) {
    console.error('Failed to return the book:', error);
  }
};
</script>
