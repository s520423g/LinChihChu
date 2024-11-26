<template>
    <div class="work  h-screen relative">
        <div class="title pl-5 sm:pl-16 absolute top-[20px]">  
            <div class="mt-3 md:text-xl text-base flex items-center">
                <div ref="sceneContainer" class="model md:w-[50px] md:h-[50px]  w-[40px] h-[40px]"></div> 
                本區域精選出林之助著名畫作共12幅，其中包含入選日本著名畫展:"奉祝展"的〈朝涼〉，供大家欣賞大師級的膠彩畫作品
            </div>
        </div>
        <swiper ref="swiper" :effect="'coverflow'" :grabCursor="true" :centeredSlides="true" :slidesPerView="'auto'" :initialSlide="currentSlide"
            :coverflowEffect="{
                rotate: 50,
                stretch: 0,
                depth: 100,
                modifier: 1,
                slideShadows: true,
            }" :pagination="{
            clickable: true,
          }"  :modules="modules" class="mySwiper absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2" @swiper="onSwiper">
            <swiper-slide class="select-none " v-for="(painting, index) in paintings" :key="painting.src"
                @click="selectPainting(painting, index)"><img class="rounded-md " :src="painting.src"
                    :alt="painting.title" /></swiper-slide>
        </swiper>

        <div id="selected-painting" v-if="selectedPainting"
            class=" z-20 w-full h-[600px] md:px-0 px-2 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 flex flex-col md:flex-row justify-center items-center"
            @click="deletePainting">

            <img class="w-full md:w-auto h-full" :src="selectedPainting.src" alt="選擇的畫作" />
            <div
                class="w-full md:w-[300px] h-full bg-[#DCCBC2] text-[#889481] flex flex-col justify-center items-center text-center">
                <h2 class="font-bold mb-3">{{ selectedPainting.title }}</h2>
                <p class="w-auto">{{ selectedPainting.description }}</p>
            </div>

        </div>
    </div>
</template>
<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue';

// Import Swiper styles
import 'swiper/css';

import 'swiper/css/effect-coverflow';
import 'swiper/css/pagination';
// import required modules
import { EffectCoverflow, Pagination} from 'swiper/modules';

//model
import * as THREE from 'three';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import pan from '@/assets/model/pan.glb';


import Img01 from '@/assets/img/painting/1936-梅花鹿-SpottedDeer.jpg';
import Img02 from '@/assets/img/painting/1937新宿所見ShinjukuJapan.jpg';
import Img03 from '@/assets/img/painting/1939-小閑-Leisure.jpg';
import Img04 from '@/assets/img/painting/1940-朝涼BathingintheMorning.jpg';
import Img05 from '@/assets/img/painting/1951-少女-YoungLady.jpg';
import Img06 from '@/assets/img/painting/1956-春意Spring.jpg';
import Img07 from '@/assets/img/painting/1958-彩塘幻影-IllusionsbythePond.jpg';
import Img08 from '@/assets/img/painting/1958-樹韻-TreeStyles.jpg';
import Img09 from '@/assets/img/painting/1963-暮紅Sunset.jpg';
import Img10 from '@/assets/img/painting/1966-春意Spring.jpg';
import Img11 from '@/assets/img/painting/1970-樹林-Forest.jpg';
import Img12 from '@/assets/img/painting/1973-秋柿FallPersimmon.jpg';

export default {
    components: {
        Swiper,
        SwiperSlide,
    },
    setup() {
        return {
            modules: [EffectCoverflow, Pagination ],
        };
    },
    data() {
        return {
            paintings: [
                { src: Img01, title: '梅花鹿 Spotted Deer 1936', description: '紙本．膠彩 Gouache on paper｜80×116cm (30F)｜本作品於1999年8月遭竊' },
                { src: Img02, title: '新宿所見 Shinjuku, Japan 1937', description: '紙本．膠彩 Gouache on paper｜80×177cm (50P)｜本作品於1999年8月遭竊' },
                { src: Img03, title: '小閑 Leisure 1939', description: '紙本．膠彩 Gouache on paper｜195×150cm (130變)｜臺北市立美術館典藏' },
                { src:Img04, title: '朝涼 Bathing in the Morning 1940', description: '紙本．膠彩 Gouache on paper｜245.3×184.5cm (180F)｜國立臺灣美術館典藏' },
                { src: Img05, title: '少女 Young Lady 1951', description: '紙本．膠彩 Gouache on paper｜43×46cm(8變)｜私人收藏' },
                { src: Img06, title: '春意 Spring 1956', description: '紙本．膠彩 Gouache on paper｜22×27cm(3F)｜私人收藏' },
                { src: Img07, title: '彩塘幻影 Illusions by the Pond 1958', description: '紙本．膠彩 Gouache on paper｜118×78cm(50P)｜私人收藏' },
                { src: Img08, title: '樹韻 Tree Styles 1958', description: '絹本．膠彩 Gouache on silk｜33×52cm(10M)｜私人收藏' },
                { src: Img09, title: '暮紅 Sunset 1963', description: '紙本．膠彩 Gouache on paper｜45×49cm(10變)｜國立台灣美術館典藏' },
                { src: Img10, title: '春意 Spring 1966', description: '紙本．膠彩 Gouache on paper｜24×27cm(3變)｜私人收藏' },
                { src: Img11, title: '樹林 Forest 1970', description: '紙本．膠彩 Gouache on paper｜50.5X60.5cm(12F)｜國立台灣美術館典藏' },
                { src: Img12, title: '秋柿 Fall Persimmon 1973', description: '紙本．膠彩 Gouache on paper｜27 X24cm｜私人收藏' },

            ],
            selectedPainting: null,
            currentSlide:6,
            swiperInstance: null,
        };
    },
    methods: {
        onSwiper(swiperInstance) {
        this.swiperInstance = swiperInstance;  // 保存 swiper 實例
        },
        selectPainting(painting, index) {
            this.selectedPainting = painting;
            this.currentSlide = index;
            if (this.swiperInstance) {  // 確認 swiper 實例是否已初始化
            this.swiperInstance.slideTo(index);
        }
        },
        deletePainting() {
            this.selectedPainting = null;
        },
        Model() {
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            camera.position.set(0, 0, 5); // 設定攝影機的位置


            //渲染
            const model = document.querySelector('.model');
            const renderer = new THREE.WebGLRenderer({ alpha: true });  //渲染透明色
            renderer.setSize(model.clientWidth, model.clientHeight);
            this.$refs.sceneContainer.appendChild(renderer.domElement);

            function resize() {
                renderer.setSize(model.clientWidth, model.clientHeight);
                camera.aspect = model.clientWidth / model.clientHeight;
                camera.updateProjectionMatrix();
            }
            window.addEventListener('resize', resize);
            resize(); // 初始調用
            //-----------------------------------------------
            scene.background = null;   //背景空白
            const light = new THREE.AmbientLight(0xFFFFFF, 3); // 環境光
            scene.add(light);
            //----------------------------------------------

            const object = new THREE.Object3D();
            const loader = new GLTFLoader();

            loader.load(pan, function (gltf) {

                // console.log(gltf);
                object.add(gltf.scene);
                object.position.set(0, 0, 0);
                object.scale.set(1, 1, 1);

                scene.add(object);


            }, undefined, function (error) {

                console.error(error);

            });
            //-----------------------------------------------------------
            function animate() {
                object.rotation.y += 0.001;
                object.rotation.z += 0.001;

                camera.lookAt(object.position);
                renderer.render(scene, camera);

            }
            renderer.setAnimationLoop(animate);

        }
    },
    mounted() {
        this.Model()

    },

};
</script>
<style scoped>
.swiper {
    width: 100%;
    padding-top: 50px;
    padding-bottom: 50px;

}

.swiper-slide {
    background-position: center;
    background-size: cover;
    width: 300px;
    height: 300px;
    border-radius: 50%;
}

.swiper-slide img {
    display: block;
    width: 100%;
    height: 300px;
}

.swiper-pagination-bullet {
    background-color: #f0f0f0; 
    opacity: 1; 
}

</style>
<style type="text/css">

  .swiper{
    --swiper-theme-color: #546165;/* 设置Swiper风格 */
  }
</style>