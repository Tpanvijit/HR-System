<template>
  <div class="min-h-screen bg-slate-50 font-prompt pb-12">
    <header class="sticky top-0 z-30 bg-white/80 backdrop-blur-md border-b border-slate-200 px-6 md:px-10 py-4 flex justify-between items-center">
      <div class="flex items-center space-x-3">
        <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center shadow-lg shadow-blue-200">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
          </svg>
        </div>
        <h1 class="text-xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-blue-700 to-indigo-600 hidden sm:block">
          ระบบประเมินบุคลากร
        </h1>
      </div>
      
      <div class="flex items-center space-x-3">
        <button class="px-4 py-2 text-sm font-medium text-gray-600 hover:text-blue-600 transition">เข้าสู่ระบบ</button>
        <button class="px-5 py-2.5 bg-gray-900 hover:bg-blue-600 text-white text-sm font-semibold rounded-xl transition-all shadow-md">
          สมัครใช้งาน
        </button>
      </div>
    </header>

    <section class="max-w-7xl mx-auto px-6 mt-8">
      <div class="bg-white p-4 rounded-3xl shadow-sm border border-slate-100 flex flex-col md:flex-row gap-4 items-center">
        <div class="relative flex-1 w-full">
          <span class="absolute inset-y-0 left-0 pl-4 flex items-center text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </span>
          <input
            v-model="search"
            type="text"
            placeholder="ค้นหาชื่อบุคลากรที่ต้องการประเมิน..."
            class="w-full pl-12 pr-4 py-3 bg-slate-50 border-none rounded-2xl focus:ring-2 focus:ring-blue-500/20 outline-none text-gray-700"
          />
        </div>

        <div class="flex flex-wrap md:flex-nowrap gap-3 w-full md:w-auto">
          <select v-model="selectedPeriod" class="flex-1 md:w-48 px-4 py-3 bg-slate-50 border-none rounded-2xl focus:ring-2 focus:ring-blue-500/20 outline-none text-gray-600 text-sm appearance-none">
            <option value="">ทุกรอบการประเมิน</option>
            <option value="รอบที่ 1/2568">รอบที่ 1/2568</option>
            <option value="รอบที่ 2/2568">รอบที่ 2/2568</option>
          </select>

          <select v-model="selectedDept" class="flex-1 md:w-48 px-4 py-3 bg-slate-50 border-none rounded-2xl focus:ring-2 focus:ring-blue-500/20 outline-none text-gray-600 text-sm appearance-none">
            <option value="">ทุกภาควิชา</option>
            <option v-for="d in departments" :key="d" :value="d">{{ d }}</option>
          </select>
        </div>
      </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 py-10 grid sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
      <div
        v-for="u in filteredUsers"
        :key="u.id"
        class="group bg-white rounded-3xl p-6 border border-slate-100 shadow-sm hover:shadow-xl hover:shadow-blue-500/5 hover:-translate-y-1 transition-all duration-300"
      >
        <div class="flex flex-col items-center text-center">
          <div class="relative mb-4">
            <div class="absolute -inset-1 bg-gradient-to-tr from-blue-500 to-indigo-400 rounded-full opacity-0 group-hover:opacity-100 transition-opacity blur-sm"></div>
            <img :src="u.image" alt="User" class="relative w-20 h-20 rounded-2xl object-cover bg-slate-100 border-2 border-white shadow-md" />
          </div>

          <h3 class="text-lg font-bold text-gray-800 group-hover:text-blue-600 transition-colors">{{ u.name }}</h3>
          <p class="text-blue-500 text-xs font-semibold bg-blue-50 px-3 py-1 rounded-full mt-2 uppercase tracking-wide">
            {{ u.department }}
          </p>
          
          <div class="mt-4 w-full pt-4 border-t border-slate-50 flex items-center justify-between">
            <div class="text-left">
              <p class="text-[10px] text-gray-400 uppercase tracking-tighter">รอบปัจจุบัน</p>
              <p class="text-xs font-medium text-gray-600">{{ u.period }}</p>
            </div>
            <router-link
              :to="`/evaluator/assignments/${u.id}`"
              class="bg-gray-50 hover:bg-blue-600 text-gray-700 hover:text-white p-2 rounded-xl transition-all"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
              </svg>
            </router-link>
          </div>
        </div>
      </div>
    </section>

    <div v-if="filteredUsers.length === 0" class="text-center py-20">
      <div class="bg-slate-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
        </svg>
      </div>
      <p class="text-gray-500">ไม่พบข้อมูลบุคลากรที่ตรงตามเงื่อนไข</p>
    </div>

    <footer class="text-center py-10 text-gray-400 text-sm border-t border-slate-100 mx-10 mt-10">
      © 2026 วิทยาลัยเทคนิคขอนแก่น — ความภาคภูมิใจในความเป็นเลิศด้านอาชีวศึกษา
    </footer>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";

const users = ref([]);
const search = ref("");
const selectedPeriod = ref("");
const selectedDept = ref("");

onMounted(async () => {
  const res = await fetch("https://dummyjson.com/users?limit=12");
  const data = await res.json();

  users.value = data.users.map(u => ({
    id: u.id,
    name: `${u.firstName} ${u.lastName}`,
    image: u.image, // ใช้รูปจาก API จริง
    department: u.company?.department || "General",
    period: u.id % 2 === 0 ? "รอบที่ 1/2568" : "รอบที่ 2/2568"
  }));
});

const departments = computed(() => {
  return [...new Set(users.value.map(u => u.department))].sort();
});

const filteredUsers = computed(() => {
  return users.value.filter(u => {
    const matchPeriod = !selectedPeriod.value || u.period === selectedPeriod.value;
    const matchDept = !selectedDept.value || u.department === selectedDept.value;
    const matchSearch = !search.value || u.name.toLowerCase().includes(search.value.toLowerCase());
    return matchPeriod && matchDept && matchSearch;
  });
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap');
.font-prompt { font-family: 'Prompt', sans-serif; }
</style>