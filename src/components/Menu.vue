<script>

import * as THREE from 'three';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import panModel from '@/assets/model/brush.glb';

// ---------------------------------
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue';

// Import Swiper styles
import 'swiper/css';

import 'swiper/css/pagination';
// import required modules
import { Mousewheel, Pagination ,Autoplay} from 'swiper/modules';

// ----------------------------------


export default {
  components: {
      Swiper,
      SwiperSlide,
    },
    setup() {
      return {
        modules: [Mousewheel, Pagination ,Autoplay],
      };
    },
  data() {
    return {
      menuVisible: false, // 控制選單的顯示狀態
      topimgVisible: true,
      top2imgVisible: false,
      resizeObserver: null,

      mouseX: 0, // 儲存滑鼠的X位置
      mouseY: 0,  // 儲存滑鼠的Y位置
      menupanX: 0,
      menupanY: 0,
      lerpFactor: 0.05 // 控制延遲

    };
  },
  methods: {
    scrollToSection(sectionId) {
      const section = document.getElementById(sectionId);
      if (section) {
        section.scrollIntoView({ behavior: 'smooth' }); // 平滑滾動
      }
      this.menuVisible = false;
      this.topimgVisible = true;
      this.top2imgVisible = false;
    },
    open() {
      this.menuVisible = !this.menuVisible; // 切換選單的顯示狀態
      this.topimgVisible = !this.topimgVisible;
      this.top2imgVisible = !this.top2imgVisible;
    },
    back(){
      this.menuVisible = false;
      this.topimgVisible = true;
      this.top2imgVisible = false;
     
    },
    Model() {
      const scene = new THREE.Scene();
      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      camera.position.set(0, 0, 5); // 設定攝影機的位置

      //渲染
      const model = document.querySelector('#menupan');
      const renderer = new THREE.WebGLRenderer({ alpha: true });  //渲染透明色
      renderer.setSize(model.clientWidth, model.clientHeight);
      this.$refs.sceneContainer.appendChild(renderer.domElement);

      function resize() {
        renderer.setSize(model.clientWidth, model.clientHeight);
        camera.aspect = model.clientWidth / model.clientHeight;
        camera.updateProjectionMatrix();
      }
      this.resizeObserver = new ResizeObserver(resize);
      this.resizeObserver.observe(model);
      window.addEventListener('resize', resize);
      resize();
      //-----------------------------------------------
      scene.background = null;   //背景空白
      const light = new THREE.AmbientLight(0xFFFFFF, 3); // 環境光
      scene.add(light);
      //----------------------------------------------
      const object = new THREE.Object3D();
      const loader = new GLTFLoader();

      loader.load(panModel, function (gltf) {

        // console.log(gltf);
        object.add(gltf.scene);
        object.position.set(0, 0, 0);
        object.scale.set(1, 1, 1);

        scene.add(object);
        camera.lookAt(object.position)
      }, undefined, function (error) {

        console.error(error);

      });
      //-----------------------------------------------------------
      function animate() {

        camera.lookAt(object.position);
        renderer.render(scene, camera);

      }
      renderer.setAnimationLoop(animate);
    },

    updateMenupanPosition(event) {
      // 更新 mouseX 和 mouseY 的位置
      this.mouseX = event.clientX;
      this.mouseY = event.clientY;
    },
    animateMenupan() {
      // 每一幀讓模型的位置慢慢靠近滑鼠的位置
      this.menupanX += (this.mouseX - this.menupanX) * this.lerpFactor;
      this.menupanY += (this.mouseY - this.menupanY) * this.lerpFactor;

      // 更新 #menupan 的位置
      const menupan = this.$refs.sceneContainer;
      if (menupan) {
        menupan.style.left = `${this.menupanX}px`;
        menupan.style.top = `${this.menupanY + 5}px`;
      }
      requestAnimationFrame(this.animateMenupan);
    }
  },

  mounted() {
    this.Model()

    window.addEventListener('mousemove', this.updateMenupanPosition);
    this.animateMenupan();

  },
}


</script>

<template>
  <div class="menu bg-[#99a8b4] md:text-3xl text-2xl font-bold z-50 top-0 right-0 fixed rounded-full mt-3 hidden sm:block"
    :class="{ expanded: menuVisible }">
    <!-- 按鈕區塊 -->
    <div class="menu-image flex justify-center items-center ">
      
      <!-- 按鈕圖片 -->
      <img src="../assets/img/bird3.PNG" alt="" class="md:w-[100px] md:h-[100px] w-[80px] h-[80px] cursor-pointer " @click="open"
        :class="{ 'hidden': !topimgVisible }">
        <!-- 點擊後出現的LOGO -->
      <img src="../assets/img/logo-white.PNG" alt="" class="top2img w-[242px] h-[80px] opacity-0"
        :class="{ 'hidden': !top2imgVisible }">
    </div>
    <!-- ---------------------------------------------------------------- -->
    <div class="btn flex justify-center items-center realtive" :class="{ 'hidden': !menuVisible }">
      <div class="back p-1 border-2 absolute md:left-10 left-2 top-5 md:ml-0 ml-2" :class="{ openback: menuVisible }"><img src="../assets/img/back.png" alt="" class="backimage md:w-[50px] md:h-[50px] w-[40px] h-[40px]" @click="back"></div>
      <img src="../assets/img/bird2.PNG" alt="" class="w-1/6 absolute -left-5 bottom-0">
      <div class="btn-right md:w-1/3 w-auto flex flex-col p-10 ">
        <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('banner')">1. HOME</a>
        <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('artist')">2. 林之助</a>
        <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('gluepainting')">3. 關於膠彩畫</a>
        <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('work')">4. 數位典藏</a>
        <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('curator')">5. 紀念館資訊</a>
        <a class="btn-right text-[#faf8f1] cursor-pointer mb-5" @click="scrollToSection('info')">6. 聯絡及交通資訊</a>
      </div>
      <!-- swiper放這邊 w-1/3 -->
       <div class="advertisement w-1/3 h-screen hidden md:block">
        <swiper
          :direction="'vertical'"
          :slidesPerView="1"
          :spaceBetween="0"
          :autoplay="{
            delay: 3000,
            disableOnInteraction: false,
          }"
          :mousewheel="true"
          :pagination="{
            clickable: true,
          }"
          :modules="modules"
          class="mySwiper">
          <swiper-slide><img src="../assets/img/ad1.jpg" alt="" ></swiper-slide>
          <swiper-slide><img src="../assets/img/ad2.jpg" alt="" ></swiper-slide>
        </swiper>
       </div>
       <!-- ================ -->
      <img src="../assets/img/bird1.PNG" alt="" class="w-1/6 absolute right-0 top-0">
      <div id="menupan" ref="sceneContainer" class="absolute z-50 hidden md:block"></div>
    </div>
  </div>
  <div
    class="tooltip fixed hidden md:block md:top-[65px] top-[50px] right-0 transform -translate-x-1/2 -translate-y-1/2 bg-[#DCCBC2] text-[#000000] p-5 rounded-lg shadow-lg z-50 border-dotted border-2 md:text-base text-sm">
    <p>此區可點選快速移動到相應頁面 &#9658</p>
  </div>

</template>

<style scoped>
.menu {
  max-height: 100px;
  max-width: 100px;
  overflow: hidden;
}

.menu.expanded {
  /* animation: name duration timing-function delay iteration-count direction fill-mode; */
  animation: menu-expand 1s ease 0s forwards;
}

@keyframes menu-expand {
  0% {
    width: 100px;
    height: 100px;
  }

  10% {
    border-radius: unset;
    margin-top: 0px;
  }

  100% {
    min-height: 100dvh;
    min-width: 100vw;
    border-radius: unset;
    top: 0;
    margin-top: 0px;
  }
}

#menupan {
  width: 100px;
  height: 100px;
}

.tooltip {
  animation: tool 1.5s ease 0s forwards;
}

@keyframes tool {
  0% {
    opacity: 1;
    display: block;
  }

  70% {
    opacity: 1;
    display: block;
  }

  90% {
    opacity: 0;
    display: block;
  }

  100% {
    opacity: 0;
    display: none;
  }
}
.back{
  opacity: 0;
}
.back.openback {
  animation: back 0.7s ease 0.3s forwards;
}
.backimage {
  transition: transform 0.3s ease; 
}

.backimage:hover {
  transform: rotate(-30deg); 
}
@keyframes back{
  0%{
    opacity: 0;
  }
  100%{
    opacity: 1;
  }
}

.btn {
  height: calc(100% - 100px);
}

.swiper {
  width: 100%;
  height: 100%;
}

.swiper-slide {
  text-align: center;
  font-size: 18px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.swiper-slide img {
  display: block;
  width: 100%;
  /* height: 60%; */
  object-fit: cover;
}
.top2img{
  opacity: 0;
  animation: back 0.7s ease 0.3s forwards;
}
.btn-right ,.advertisement{
  opacity: 0;
  animation: back 0.7s ease 0.3s forwards;

}
a {
  text-decoration: none;
  transition: 0.4s;
  padding: .75rem;
}

@media (hover: hover) {
  a:hover {
    border-radius: 5px;
    background-color: #8b6c6f;
  }
}

</style>
