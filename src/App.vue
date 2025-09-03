<script setup lang="ts">
import { ref } from "vue";

const showModal = ref(false);

function OpenModal() {
  showModal.value = true;
}

function closeModal() {
  showModal.value = false;
}
</script>

<template>
  <div class="bg-[#F7F7F7] min-h-screen">
    <div class="w-[52%] pt-10 mx-auto flex flex-col gap-[30px] h-screen relative">
      <div class="flex flex-col gap-[18px]">
        <h1 class="text-center font-kanit font-medium text-[26px] leading-[100%] text-[#252525]">TODO LIST</h1>
        <div class="flex items-center justify-between">
          <div class="py-2 px-4 rounded-[5px] border border-[#6C63FF] w-[79.3%] flex items-center justify-between">
            <input type="text" placeholder="Search note" class="font-inter font-medium text-base leading-[100%] text-[#C3C1E5] placeholder-[#C3C1E5]" />
            <img src="/search icon.png" alt="search icon" class="w-[21px] h-[21px]" />
          </div>
          <div class="p-[10px] rounded-[5px] bg-[#6C63FF]">
            <div class="flex items-center w-[65px] justify-between">
              <p class="font-kanit font-medium text-lg leading-[100%] text-[#F7F7F7]">ALL</p>
              <img src="/chevron-top.png" alt="select icon" class="w-[6px] h-[3px]" />
            </div>
          </div>
          <div class="p-2 rounded-[5px] bg-[#6C63FF]">
            <img src="/moon.png" alt="moon icon" class="w-[22px] h-[22px]" />
          </div>
        </div>
      </div>
      <div class="w-[69.3%] flex flex-col gap-5 mx-auto items-center">
        <img src="/detective.png" alt="detective icon" class="w-[221px] h-[174px]" />
        <p class="font-kanit font-normal text-xl leading-[100%] text-[#252525]">Empty...</p>
      </div>
      <div class="w-[50px] h-[50px] absolute bottom-8 right-1" @click="OpenModal">
        <img src="/Add button.png" alt="add button" class="w-full h-full" />
      </div>
    </div>
    <div class="fixed inset-0 bg-[#252525B2]/70 flex w-full h-screen items-center justify-center" v-if="showModal">
      <div class="w-[500px] py-[18px] px-[30px] h-[289px] flex flex-col justify-between border border-[#6C63FF] bg-white rounded-2xl">
        <div class="flex flex-col gap-[25px]">
          <h1 class="text-center font-kanit font-medium text-2xl leading-[100% text-[#252525]]">NEW NOTE</h1>
          <input
            type="text"
            placeholder="Input your note"
            class="w-full py-2 px-4 border border-[#6C63FF] rounded-[5px] outline-0 font-kanit font-medium text-base leading-[100%] text-[#C3C1E5] placeholder-[#C3C1E5]" />
        </div>
        <div class="flex items-center justify-between">
          <button class="py-[10px] px-[22px] border border-[#6C63FF] rounded-[5px] font-kanit font-medium text-lg leading-[100%] text-[#6C63FF]" @click="closeModal">Cancel</button>
          <button class="py-[10px] px-[22px] bg-[#6C63FF] font-kanit font-medium text-lg leading-[100%] text-[#F7F7F7] rounded-[5px]">Apply</button>
        </div>
      </div>
    </div>
  </div>
</template>

https://jsonplaceholder.typicode.com/todos https://jsonplaceholder.typicode.com/
