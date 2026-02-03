<template>
  <div class="min-h-screen bg-slate-50 py-12 px-4 sm:px-6 lg:px-8 font-prompt">
    <div class="max-w-2xl mx-auto">
      
      <div class="bg-white rounded-3xl shadow-sm border border-slate-100 p-6 mb-8 flex items-center justify-between">
        <div class="flex items-center space-x-5">
          <div class="relative">
            <div class="absolute -inset-0.5 bg-gradient-to-r from-orange-400 to-red-500 rounded-full blur opacity-30"></div>
            <img :src="getAvatar(user.avatar)" alt="Avatar" class="relative w-16 h-16 rounded-full object-cover border-2 border-white shadow-sm" />
          </div>
          <div>
            <h1 class="text-xl font-bold text-gray-800">{{ user.name }}</h1>
            <p class="text-sm text-orange-500 font-medium bg-orange-50 px-2 py-0.5 rounded-md inline-block">
              {{ user.role }}
            </p>
          </div>
        </div>
        <div class="hidden sm:block text-right">
          <p class="text-xs text-gray-400 uppercase tracking-widest">สถานะปัจจุบัน</p>
          <p class="text-sm font-semibold text-green-500">Online</p>
        </div>
      </div>

      <div class="bg-white rounded-3xl shadow-sm border border-slate-100 overflow-hidden">
        <div class="p-8">
          <h2 class="text-lg font-bold text-gray-800 mb-6 flex items-center">
            <span class="w-1.5 h-6 bg-orange-500 rounded-full mr-3"></span>
            รายการงานที่ต้องทำ
          </h2>

          <div class="relative mb-8 group">
            <input 
              v-model="newTaskTitle" 
              @keyup.enter="addTask"
              placeholder="พิมพ์ชื่อรายงานหรืองานที่ต้องการเพิ่ม..." 
              class="w-full pl-5 pr-32 py-4 bg-slate-50 border-none rounded-2xl focus:ring-2 focus:ring-orange-500/20 transition-all outline-none text-gray-700 placeholder:text-gray-400"
            />
            <button 
              @click="addTask" 
              class="absolute right-2 top-2 bottom-2 bg-gray-900 hover:bg-orange-600 text-white px-6 rounded-xl text-sm font-medium transition-all shadow-lg active:scale-95"
            >
              เพิ่มงาน
            </button>
          </div>

          <div class="space-y-3">
            <div 
              v-for="task in tasks" 
              :key="task.id" 
              class="group flex items-center justify-between p-4 rounded-2xl border border-transparent hover:border-slate-100 hover:bg-slate-50/50 transition-all"
              :class="{ 'opacity-75': task.completed }"
            >
              <div class="flex items-center space-x-4">
                <label class="relative flex items-center cursor-pointer">
                  <input 
                    type="checkbox" 
                    v-model="task.completed" 
                    @change="updateTaskStatus(task)"
                    class="peer h-6 w-6 cursor-pointer appearance-none rounded-lg border-2 border-slate-200 checked:bg-orange-500 checked:border-orange-500 transition-all"
                  />
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 absolute text-white opacity-0 peer-checked:opacity-100 top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 transition-opacity" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
                  </svg>
                </label>
                <span 
                  class="text-gray-700 transition-all"
                  :class="{ 'line-through text-gray-400': task.completed }"
                >
                  {{ task.title }}
                </span>
              </div>
              
              <button 
                @click="deleteTask(task.id)" 
                class="p-2 text-gray-300 hover:text-red-500 hover:bg-red-50 rounded-xl transition-all opacity-0 group-hover:opacity-100"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                </svg>
              </button>
            </div>

            <div v-if="tasks.length === 0" class="text-center py-10">
              <p class="text-gray-400 italic">ไม่มีงานค้างในรายการ</p>
            </div>
          </div>
        </div>
        
        <div class="bg-slate-50/50 px-8 py-4 border-t border-slate-100 flex justify-between items-center text-sm">
          <span class="text-gray-500">ทั้งหมด {{ tasks.length }} รายการ</span>
          <span class="text-gray-500">เสร็จสิ้นแล้ว {{ tasks.filter(t => t.completed).length }} รายการ</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap');
.font-prompt { font-family: 'Prompt', sans-serif; }
</style>

<script>
export default {
  data() {
    return {
      user: {
        name: 'Thapnawat panvijit',
        role: 'เจ้าหน้าที่บริหารงานทั่วไป',
        avatar: '37887487-businessman-profile-icon-male-portrait-flat.jpg' 
      },
      newTaskTitle: '',
      tasks: [
        { id: 1, title: 'จัดทำสรุปรายงานประจำเดือนมกราคม', completed: false},
        { id: 2, title: 'เตรียมเอกสารประกอบการประชุมวิชาการ', completed: true },
        { id: 3, title: 'ส่งแบบฟอร์มประเมินบุคลากรดีเด่น', completed: false},
      ],
    }
  },
  methods: {
    getAvatar(filename) { 
      // ในระบบจริงอาจจะใช้ https://ui-avatars.com ถ้าไม่มีรูป
      return filename ? `/uploads/${filename}` : `https://ui-avatars.com/api/?name=${this.user.name}&background=f97316&color=fff`;
    },
    addTask() {
      if (this.newTaskTitle.trim() === '') return;
      this.tasks.unshift({ // ใช้ unshift เพื่อให้งานใหม่อยู่บนสุด
        id: Date.now(),
        title: this.newTaskTitle,
        completed: false
      });
      this.newTaskTitle = '';
    },
    updateTaskStatus(task) {
      console.log(`Task ${task.id} updated to: ${task.completed}`);
    },
    deleteTask(taskId) {
      if(confirm('คุณแน่ใจหรือไม่ว่าต้องการลบงานนี้?')) {
        this.tasks = this.tasks.filter(t => t.id !== taskId);
      }
    }
  }
}
</script>