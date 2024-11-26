<script>
// import { gsap } from "gsap";
// import Img01 from '@/assets/img/banner/IMG_deer.PNG';
// import Img02 from '@/assets/img/banner/IMG_dragonfly.PNG';
// import Img03 from '@/assets/img/banner/IMG_hen.PNG';
// import Img04 from '@/assets/img/banner/IMG_lady.PNG';
// import Img05 from '@/assets/img/banner/IMG_lotus.PNG';
// import Img06 from '@/assets/img/banner/IMG_seeds.PNG';
// import Img07 from '@/assets/img/banner/IMG_vase.PNG';

export default {
    // data() {
    //     return {
    //         img: [
    //             Img01,
    //             Img02,
    //             Img03,
    //             Img04,
    //             Img05,
    //             Img06,
    //             Img07,
    //         ],
    //         floatingImg: [
    //             { id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }, { id: 5 },
    //         ],
    //         showImg: '',
    //     }
    // },
    methods: {
        // 禁用滾輪和鍵盤滾動
        disableScroll() {
            window.addEventListener('wheel', this.preventScroll, { passive: false }); // 禁用滾輪滾動
            window.addEventListener('keydown', this.preventKeyScroll); // 禁用鍵盤滾動
        },
        // 恢復滾輪和鍵盤滾動
        enableScroll() {
            window.removeEventListener('wheel', this.preventScroll); // 恢復滾輪滾動
            window.removeEventListener('keydown', this.preventKeyScroll); // 恢復鍵盤滾動
        },
        preventScroll(e) {
            e.preventDefault(); // 阻止滾動事件
        },
        preventKeyScroll(e) {
            // 禁用特定鍵盤按鍵的滾動功能
            if (['ArrowUp', 'ArrowDown', 'PageUp', 'PageDown', 'Space'].includes(e.code)) {
                e.preventDefault();
            }
        },
        
        // getImg() {
        //     let num = Math.floor(Math.random() * 7);
        //     let pickedImg = this.img.slice(num, num + 1);
        //     return pickedImg
        // },
        
        // updateImg() {
        //     this.showImg = this.getImg();
        // },
        // randomImg() {          
        //     this.showImg = this.getImg();
        //     setInterval(this.updateImg, 8500)
        // },
        
        startAni() {
            const section = document.getElementById('banner');
            if (section) {
                section.scrollIntoView({ behavior: 'smooth' }); 
            }
            const loadingSection = document.querySelector('#loading-section');
            loadingSection.style.animationPlayState = 'running'; // 設置 animation-play-state 為 running

            const loading2Section = document.querySelector('#loading2-section');
            loading2Section.style.animationPlayState = 'running';
            // 監聽動畫結束
            loadingSection.addEventListener('animationend', () => {
                this.animationCompleted = true; // 標記動畫完成
                this.finishAnimation(); // 動畫完成後觸發
            });
        },
        finishAnimation() {
            if (this.animationCompleted) {
                this.enableScroll(); // 動畫完成後啟用滾動
                this.$emit('animation-done'); // 通知父組件動畫完成
            }
        }
    },
    mounted() {
        this.disableScroll(); // 頁面加載時禁用滾動
        
        // this.randomImg();        
        //  const loading = document.querySelector('#loading-section');
        // let height = loading.clientHeight;
        // gsap.fromTo('#loading-section img',
        //     {
        //         opacity: 1
        //     },
        //     {
        //         duration: 4,
        //         ease: "power2.inOut",
        //         repeat: -1,
        //         y: -height,
        //         opacity: 0,
        //         stagger: 0.5
        //     });
    

    },
    beforeDestroy() {
        this.enableScroll(); // 組件銷毀前恢復滾動
    }
}
</script>

<template>
    <div id="loading-section"
        class="loading z-[100] h-screen w-full bg-[#8b6c6f] bg-blend-screen bg-[url('../assets/img/2.jpg')] bg-cover bg-center flex flex-col justify-center items-center fixed">
        <div id="loading2-section" class="loading2 flex flex-col justify-center items-center w-full h-full">
            <div class="bg-[url('../assets/img/logo.png')] w-[193px] h-[40px] bg-contain mb-8"></div>
            <button type="button"
                class="start py-2 px-8 rounded-full ring-1 ring-[#231815] text-[#231815] hover:text-[#a01628] text-xl content-center cursor-pointer relative"
                @click="startAni">開始</button>
            <!-- <img v-for=" n in 10 " :key="n" :src="this.showImg" :alt="n" class="absolute w-36 opacity-1 top-full"
                :style="{ left: (Math.floor(Math.random() * 70) + 10) + '%' }"> -->
        </div>
    </div>

</template>

<style scope>
.loading {
    transform-origin: bottom left;
    /* animation: name duration timing-function delay iteration-count direction fill-mode; */
    animation: loadingup 2s linear 0.5s forwards;
    animation-play-state: paused;
    overflow: hidden;
}
@keyframes loadingup {
    0% {
        opacity: 1;
        rotate: 0deg;
    }
    50%{
        opacity: 1;
    }
    100% {
        transform: scaleX(1.5);
        rotate: -90deg;
        opacity: 0;
    }
}

.loading2 {
    /* animation: name duration timing-function delay iteration-count direction fill-mode; */
    animation: loadingrota 0.5s linear 0s forwards;
    animation-play-state: paused;
    overflow: hidden;
}

@keyframes loadingrota {
    0% {
        opacity: 1;
    }

    100% {
        opacity: 0;
    }
}

.start::before {
    content: '';
    display: block;
    position: absolute;
    top: -8px;
    left: -8px;
    background-color: rgba(180, 170, 160, 0.7);
    width: 110px;
    height: 50px;
    z-index: -1;
    border-radius: 50px;
    filter: blur(1px);
}
</style>
