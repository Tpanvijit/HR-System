<template>
  <div class="min-h-screen flex flex-col bg-slate-50 font-prompt">
    <main class="flex-grow flex items-center justify-center p-6">
      <div class="w-full max-w-5xl">
        
        <div class="bg-red/80 backdrop-blur-md rounded-3xl shadow-xl overflow-hidden border border-white">
          <div class="md:flex">
            
            <div class="p-8 md:p-12 md:w-3/5">
              <div class="inline-block px-3 py-1 rounded-full bg-Red-100 text-orange-600 text-xs font-bold mb-4 tracking-wider uppercase">
                Personnel Assessment System
              </div>
              <h1 class="text-4xl font-extrabold text-gray-900 mb-4 leading-tight">
                ยินดีต้อนรับเข้าสู่ระบบ <br/>
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-orange-500 to-red-600">
                  ประเมินบุคลากร
                </span>
              </h1>
              <p class="text-gray-500 text-lg mb-8 leading-relaxed">
                ยกระดับการบริหารจัดการองค์กรด้วยระบบประเมินผลอัจฉริยะ 
                ช่วยให้คุณบันทึกข้อมูล ดูรายงาน และสรุปผลคะแนนได้อย่างรวดเร็ว แม่นยำ และโปร่งใส
              </p>
              
              <div class="flex flex-wrap gap-4">
                <button class="px-8 py-3 bg-orange-500 hover:bg-orange-600 text-white rounded-xl font-medium transition-all transform hover:scale-105 shadow-lg shadow-orange-200">
                  เริ่มต้นใช้งาน
                </button>
                <button class="px-8 py-3 bg-white border border-gray-200 hover:bg-gray-50 text-gray-700 rounded-xl font-medium transition-all">
                  คู่มือการใช้งาน
                </button>
              </div>
            </div>

            <div class="bg-gradient-to-br from-orange-400 to-orange-600 md:w-2/5 p-8 text-white flex flex-col justify-center">
              <div class="space-y-6">
                <div class="flex items-start space-x-4">
                  <div class="bg-white/20 p-2 rounded-lg">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor font-bold">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                  </div>
                  <div>
                    <h4 class="font-bold">ใช้งานง่าย</h4>
                    <p class="text-orange-100 text-sm">แบบฟอร์มประเมินที่ออกแบบมาเพื่อลดความซับซ้อน</p>
                  </div>
                </div>

                <div class="flex items-start space-x-4">
                  <div class="bg-white/20 p-2 rounded-lg">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor font-bold">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                    </svg>
                  </div>
                  <div>
                    <h4 class="font-bold">สรุปผลทันที</h4>
                    <p class="text-orange-100 text-sm">ดูรายงานและกราฟสรุปผลได้แบบ Real-time</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>

    <footer class="py-6 text-center text-gray-400 text-sm border-t border-gray-100 bg-white">
      <div class="flex justify-center items-center space-x-2">
        <span class="w-2 h-2 bg-orange-400 rounded-full animate-pulse"></span>
        <p>© 2026 วิทยาลัยเทคนิคขอนแก่น — ระบบประเมินบุคลากรสมัยใหม่</p>
      </div>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap');

.font-prompt {
  font-family: 'Prompt', sans-serif;
}
</style>

<script>
export default {
  name: "MainView",
};
</script>