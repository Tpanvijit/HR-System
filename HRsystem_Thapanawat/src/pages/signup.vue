<template>
  <div class="min-h-screen flex items-center justify-center bg-slate-50 py-12 px-4 sm:px-6 lg:px-8 font-prompt">
    <div class="max-w-md w-full">
      <div class="bg-white rounded-3xl shadow-xl shadow-slate-200/50 overflow-hidden border border-slate-100">
        <div class="bg-gradient-to-r from-blue-600 to-indigo-700 pt-10 pb-12 px-8 text-center">
          <h1 class="text-3xl font-extrabold text-white mb-2">สร้างบัญชีใหม่</h1>
          <p class="text-blue-100 opacity-90 text-sm">กรอกข้อมูลด้านล่างเพื่อเข้าใช้งานระบบประเมิน</p>
        </div>

        <div class="px-8 pb-10 -mt-6">
          <form @submit.prevent="signup" class="bg-white rounded-2xl p-6 shadow-sm space-y-5 border border-slate-50">
            
            <div class="grid grid-cols-2 gap-4">
              <div class="space-y-1">
                <label class="text-sm font-semibold text-gray-700 ml-1">ชื่อจริง</label>
                <input v-model="form.fname" type="text"
                  class="w-full px-4 py-3 bg-slate-50 border border-transparent rounded-xl focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500 focus:bg-white transition-all outline-none text-gray-700"
                  placeholder="สมชาย" required />
              </div>
              <div class="space-y-1">
                <label class="text-sm font-semibold text-gray-700 ml-1">นามสกุล</label>
                <input v-model="form.lname" type="text"
                  class="w-full px-4 py-3 bg-slate-50 border border-transparent rounded-xl focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500 focus:bg-white transition-all outline-none text-gray-700"
                  placeholder="ใจดี" required />
              </div>
            </div>

            <div class="space-y-1">
              <label class="text-sm font-semibold text-gray-700 ml-1">ชื่อผู้ใช้งาน (Username)</label>
              <div class="relative">
                <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center text-gray-400">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                  </svg>
                </span>
                <input v-model="form.username" type="text"
                  class="w-full pl-11 pr-4 py-3 bg-slate-50 border border-transparent rounded-xl focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500 focus:bg-white transition-all outline-none text-gray-700"
                  placeholder="username123" required />
              </div>
            </div>

            <div class="space-y-1">
              <label class="text-sm font-semibold text-gray-700 ml-1">รหัสผ่าน</label>
              <input v-model="form.password" type="password"
                class="w-full px-4 py-3 bg-slate-50 border border-transparent rounded-xl focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500 focus:bg-white transition-all outline-none text-gray-700"
                placeholder="••••••••" required />
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <div class="space-y-1">
                <label class="text-sm font-semibold text-gray-700 ml-1">ตำแหน่ง</label>
                <select v-model="form.role"
                  class="w-full px-4 py-3 bg-slate-50 border border-transparent rounded-xl focus:ring-2 focus:ring-blue-500/20 focus:border-blue-500 focus:bg-white transition-all outline-none text-gray-700 appearance-none">
                  <option value="user">User</option>
                  <option value="admin">Admin</option>
                </select>
              </div>
              <div class="space-y-1">
                <label class="text-sm font-semibold text-gray-700 ml-1">รูปโปรไฟล์</label>
                <label class="cursor-pointer flex items-center justify-center w-full px-4 py-3 bg-blue-50 text-blue-600 border border-dashed border-blue-200 rounded-xl hover:bg-blue-100 transition-all text-sm font-medium">
                  {{ form.avatar ? 'เลือกไฟล์แล้ว' : 'อัปโหลดรูป' }}
                  <input type="file" @change="handleFile" class="hidden" />
                </label>
              </div>
            </div>

            <button type="submit"
              class="w-full py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-2xl transition-all transform active:scale-[0.98] shadow-lg shadow-blue-200 mt-2">
              สร้างบัญชีผู้ใช้งาน
            </button>

            <p class="text-sm text-gray-500 text-center pt-2">
              มีบัญชีอยู่แล้ว? 
              <router-link to="/login" class="text-blue-600 font-bold hover:underline decoration-2 underline-offset-4">เข้าสู่ระบบ</router-link>
            </p>
          </form>
        </div>
      </div>

      <footer class="text-center py-8 text-gray-400 text-xs">
        © 2026 วิทยาลัยเทคนิคขอนแก่น — ระบบประเมินบุคลากร
      </footer>
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap');
.font-prompt { font-family: 'Prompt', sans-serif; }
</style>

<script>
export default {
  name: "SignUp",
  data() {
    return {
      form: {
        fname: "",
        lname: "",
        username: "",
        password: "",
        avatar: null,
        role: "user",
      },
    };
  },
  methods: {
    handleFile(event) {
      this.form.avatar = event.target.files[0];
    },
    async signup() {
      // โค้ดส่วน Logic ของคุณเหมือนเดิมครับ...
      const formData = new FormData();
      formData.append("fname", this.form.fname);
      formData.append("lname", this.form.lname);
      formData.append("username", this.form.username);
      formData.append('password', this.form.password);
      if (this.form.avatar) {
        formData.append('avatar', this.form.avatar);
      }
      formData.append('role', this.form.role);

      try {
        const res = await fetch('http://localhost:3000/signup', {
          method: 'POST',
          body: formData,
        });

        if (res.ok) {
          alert('สมัครสมาชิกเรียบร้อยแล้ว!');
          this.$router.push('/login'); // แนะนำให้ redirect ไปหน้า login เลย
        } else {
          const error = await res.json();
          alert('ล้มเหลว: ' + (error.message || 'ข้อมูลไม่ถูกต้อง'));
        }
      } catch (err) {
        alert('ไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้');
      }
    },
  },
};
</script>