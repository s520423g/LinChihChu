<script>
import { gsap } from "gsap";
import { TextPlugin } from "gsap/TextPlugin";
import Img01 from '@/assets/img/banner/IMG_deer.PNG';
import Img02 from '@/assets/img/banner/IMG_dragonfly.PNG';
import Img03 from '@/assets/img/banner/IMG_hen.PNG';
import Img04 from '@/assets/img/banner/IMG_lady.PNG';
import Img05 from '@/assets/img/banner/IMG_lotus.PNG';
import Img06 from '@/assets/img/banner/IMG_seeds.PNG';
import Img07 from '@/assets/img/banner/IMG_vase.PNG';



export default {
    data() {
        return {
            title: '林之助紀念館',
            subTitle: '『每一畫作，應該沒有高低、優劣之分，　　　　　　　\n　　　　　　　因為每一幅畫都代表著作者自己的面目。』',
            img: [
                Img01,
                Img02,
                Img03,
                Img04,
                Img05,
                Img06,
                Img07,

            ],
            floatingImg: [
                { id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }, { id: 5 },
            ],
            showImg: '',
        }
    },
    methods: {
        // get random img src
        getImg() {
            let num = Math.floor(Math.random() * 7);
            let pickedImg = this.img.slice(num, num + 1);
            return pickedImg
        },
        // 選一張圖片顯示(給定時器用)
        updateImg() {
            this.showImg = this.getImg();
        },
        randomImg() {
            // 選一張圖片顯示
            this.showImg = this.getImg();
            // 定時重新選圖
            setInterval(this.updateImg, 8500)
        }
    },
    mounted() {
        // 註冊插件
        gsap.registerPlugin(TextPlugin);

        // 選圖並設定定時器
        this.randomImg();

        // 圖片上飄 gsap 動畫
        const banner = document.querySelector('#banner-section');
        let height = banner.clientHeight;
        gsap.fromTo('.banner-right img',
            {
                opacity: 1
            },
            {
                duration: 4,
                ease: "power2.inOut",
                repeat: -1,
                y: -height,
                opacity: 0,
                stagger: 0.5
            })

        // 字體 gsap 動畫
        gsap.fromTo('#banner-title',
            {
                yPercent: 10,
            }, {
            yPercent: -10,
            duration: 2,
            ease: 'linear',
            repeat: -1,
            yoyo: true
        })


        // 下滑提示消失
        gsap.to('.scroll-down',{
            scrollTrigger:{
                trigger: ".scroll-down",
                start: "top 80%",
                end: "+=100",
                scrub: 1,
            },opacity: 0}
        )
    }
}

</script>



<template>
    <div id="banner-section" class="container h-dvh flex mx-auto relative">
        <div class="scroll-down absolute bottom-8 left-1/2 -translate-x-full z-10 w-fit h-5 animate-bounce flex flex-col items-center select-none">
            <p class="text-center text-xl text-black">Scroll</p>
            <img src="../assets/img/down.png" alt="arrow" class="w-5">
        </div>
        <div class="banner-left w-0 sm:w-1/5"></div>
        <div class="banner-right w-full sm:w-4/5 content-center relative overflow-hidden">
            <h1 id="banner-title" class="mb-5 text-5xl md:text-6xl text-center font-bold p-5">{{ title }}</h1>
            <h3 id="banner-subtitle" class="text-sm md:text-md text-center whitespace-pre-wrap">{{ subTitle }}</h3>
            <!-- 漂浮的圖片 -->
            <img v-for=" n in 10 " :key="n" :src="this.showImg" :alt="n" class="absolute w-36 opacity-1 top-full"
                :style="{ left: (Math.floor(Math.random() * 70) + 10) + '%' }">
        </div>
    </div>
</template>

<style scoped></style>