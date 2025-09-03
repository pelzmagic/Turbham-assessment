<script setup lang="ts">
import { ref, computed } from "vue";

const showModal = ref(false);

const newNote = ref("");
const notes = ref<any[]>([]);
const searchQuery = ref("");

function OpenModal() {
  showModal.value = true;
}

function closeModal() {
  showModal.value = false;
}

async function submitNote() {
  if (!newNote.value.trim()) {
    alert("Please enter a note.");
    return;
  }

  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/todos", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        title: newNote.value,
        completed: false,
        userId: 1,
      }),
    });

    const data = await res.json();
    console.log("Note created:", data);
    notes.value.unshift(data);
    newNote.value = "";
    showModal.value = false;
  } catch (error) {
    console.error("Error creating note:", error);
  }
}

async function deleteNote(id: number) {
  try {
    await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
      method: "DELETE",
    });
    notes.value = notes.value.filter((note) => note.id !== id);
    console.log(`Note ${id} deleted`);
  } catch (error) {
    console.error("Error deleting note:", error);
  }
}

const filteredNotes = computed(() => {
  if (!searchQuery.value.trim()) return notes.value;
  return notes.value.filter((note) => note.title.toLowerCase().includes(searchQuery.value.toLowerCase()));
});
</script>

<template>
  <div class="bg-[#F7F7F7] min-h-screen">
    <div class="w-[52%] pt-10 mx-auto flex flex-col gap-[30px] h-screen relative">
      <div class="flex flex-col gap-[18px]">
        <h1 class="text-center font-kanit font-medium text-[26px] leading-[100%] text-[#252525]">TODO LIST</h1>
        <div class="flex items-center justify-between">
          <div class="py-2 px-4 rounded-[5px] border border-[#6C63FF] w-[79.3%] flex items-center justify-between">
            <input type="text" placeholder="Search note" v-model="searchQuery" class="font-inter font-medium text-base leading-[100%] text-[#C3C1E5] placeholder-[#C3C1E5] outline-0" />
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
        <template v-if="filteredNotes.length">
          <ul class="w-full space-y-2">
            <li v-for="note in filteredNotes" :key="note.id" class="p-3 border rounded bg-white flex items-center justify-between">
              <span>{{ note.title }}</span>
              <button class="text-red-500 font-bold" @click="deleteNote(note.id)">Delete</button>
            </li>
          </ul>
        </template>
        <template v-else>
          <img src="/detective.png" alt="detective icon" class="w-[221px] h-[174px]" />
          <p class="font-kanit font-normal text-xl leading-[100%] text-[#252525]">Empty...</p>
        </template>
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
            class="w-full py-2 px-4 border border-[#6C63FF] rounded-[5px] outline-0 font-kanit font-medium text-base leading-[100%] text-[#C3C1E5] placeholder-[#C3C1E5]"
            v-model="newNote" />
        </div>
        <div class="flex items-center justify-between">
          <button class="py-[10px] px-[22px] border border-[#6C63FF] rounded-[5px] font-kanit font-medium text-lg leading-[100%] text-[#6C63FF]" @click="closeModal">Cancel</button>
          <button class="py-[10px] px-[22px] bg-[#6C63FF] font-kanit font-medium text-lg leading-[100%] text-[#F7F7F7] rounded-[5px]" @click="submitNote">Apply</button>
        </div>
      </div>
    </div>
  </div>
</template>

https://jsonplaceholder.typicode.com/todos https://jsonplaceholder.typicode.com/
