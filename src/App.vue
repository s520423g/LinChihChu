<script setup>
import { RouterLink, RouterView } from 'vue-router';
import { ref } from 'vue';

const menuVisible = ref(false);

const scrollToSection = (sectionId) => {
  const section = document.getElementById(sectionId);
  if (section) {
    section.scrollIntoView({ behavior: 'smooth' });
  }
  menuVisible.value = false;
};

const opennavarea = () => {
  menuVisible.value = !menuVisible.value;
};

const clickCount = ref(0);
const showImage = ref(false);
const showup = () => {
  clickCount.value += 1;
  if (clickCount.value === 5) {
    showImage.value = true;
    setTimeout(() => {
      showImage.value = false;
      clickCount.value = 0; // Reset the counter if you want it to repeat every 20 clicks
    }, 100); // 1000ms = 1 second
  }
}


</script>

<template>
  <nav class="nav fixed w-full h-[70px] flex justify-center p-3 z-20 sm:hidden bg-[#99a8b4]/90">
    <!-- 點擊這裡開啟/關閉選單 -->
    <div class="navmenu absolute top-1/2 -translate-y-1/2 left-0 ml-5">
      <!-- 切換圖示 -->
      <svg v-if="!menuVisible" class="w-8 h-8 text-white cursor-pointer" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" @click="opennavarea">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
      </svg>
      <svg v-else class="w-8 h-8 text-white cursor-pointer" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" @click="opennavarea">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
      </svg>
    </div>
    <div 
      class="navarea absolute bg-[#99a8b4]/90 md:text-3xl text-2xl font-bold z-50 top-[70px] left-0  w-full h-screen"
      :class="{ hidden: !menuVisible }" 
    >
      <div class="btn flex justify-center items-center relative">
        <img src="../src/assets/img/bird2.PNG" alt="" class="w-1/6 absolute -left-5 bottom-0">
        <div class="btn-right md:w-1/3 w-auto flex flex-col p-10">
          <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('banner')">1. HOME</a>
          <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('artist')">2. 林之助</a>
          <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('gluepainting')">3. 關於膠彩畫</a>
          <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('work')">4. 數位典藏</a>
          <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('curator')">5. 紀念館資訊</a>
          <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('info')">6. 聯絡及交通資訊</a>
        </div>
        <img src="../src/assets/img/bird1.PNG" alt="" class="w-1/6 absolute right-0 top-0">
      </div>
    </div>
    
    <!-- Logo -->
    <img src="../src/assets/img/logo-white.PNG" alt="" class="w-[151px] h-[50px] shrink-0 z-20" @click="showup">
    <div v-if="showImage" class="fixed top-0 left-0 w-screen h-screen flex items-center justify-center z-50 bg-black/50">
      <img src="../src/assets/img/lcc.PNG" alt="放大圖片" class="w-full h-screen transition-transform duration-1000">
    </div>
    
  </nav>
  <RouterView />
</template>

<style scoped>
nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  nav {
    text-align: left;
    font-size: 1rem;
  }
}

.btn {
  height: calc(100% - 100px);
}
</style>
