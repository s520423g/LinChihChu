<script>
import { gsap } from "gsap";
import { ScrollTrigger, Observer } from "gsap/all";
import Img01 from '@/assets/img/artist/lcc02.jpg';
import Img02 from '@/assets/img/artist/lcc01.png';


export default {
    data() {
        return {
            artistDescribe: [
                {
                    id: 'describe-1',
                    content: '　　出生於臺中大雅，12歲赴日本東京留學，中學畢業後考進日本帝國美術學校（今武藏野美術大學）日本畫科就讀，受教於奧村土牛、山口逢春、川崎小虎及小林巢居。畢業後進入兒玉希望日本畫塾，深入學習當時日本畫官展繪畫風格，並在年僅24歲時以〈朝涼〉入選紀元二六○○年奉祝美術展。林之助返臺後參加臺灣官辦府展，1942年以〈母子〉獲第五屆府展特選，1943年〈好日〉再獲第六屆府展特選第一名，奠定在臺灣畫壇的地位。'
                },
                {
                    id: 'describe-2',
                    content: '　　1945 年第二次世界大戰結束，臺灣經歷政權轉換，以膠為媒劑的東洋畫在戰後的臺灣日漸式微、幾近失傳。林之助有感於「東洋畫」名稱帶日本風，難容於當時的官方意識形態，於1977年提出「膠彩畫正名」，改用繪畫材料命名，以「膠彩畫」取代「東洋畫」，避免多餘的誤解與爭議，其後更組織膠彩畫協會、舉辦膠彩畫展，使膠彩畫在臺灣美術中得以保留並延續發展。'
                },
                {
                    id: 'describe-3',
                    content: '　　林之助於1946年進入臺中師範學校（今國立臺中教育大學）執教，同時遷入位於柳川西路的學校附屬宿舍，自此展開長達一甲子、他與住家兼畫室的不解之緣。\n　　由於當時學校裡只能教授素描、水彩及色彩學課程，面對膠彩畫即將失傳的窘境，林之助採用傳統畫塾的方式，從每屆學生中挑選出優秀學生，非但不收學費且免費提供顏料繪具，課後於住處教導傳授，以此培養膠彩畫的新一代。也因林之助所住宿舍外圍為竹籬笆圍牆，學生們便將之暱稱為「竹籬笆畫室」。這些竹籬笆畫室的學生，成了膠彩畫沒落、艱困時期中的少數捍衛者，也是往後臺灣省膠彩畫協會成立主要的中堅會員及推動執行者。'
                }
            ],
            artistImg: [
                {
                    id: 'img-1',
                    src: Img01,
                },
                {
                    id: 'img-2',
                    src: Img02,
                },
            ]
        }
    },
    mounted() {
        // Register GSAP Plugins 將要用的套件加進來
        gsap.registerPlugin(ScrollTrigger, Observer);


        let cardtl = gsap.timeline({
            scrollTrigger: {
                trigger: "#artist-section",
                // 開始碰撞 trigger的哪邊 碰到 螢幕的哪邊 開始動畫
                start: "bottom bottom",
                end: "+=1000",
                scrub: 1,
                pin: true,
                anticipatePin: 1,
                // markers: true,
            },
        });

        cardtl
            // switch1---------------------
            // card-1 disappear
            .to(
                "#describe-1",
                {
                    yPercent: -30,
                    scale: 0.8,
                    opacity: 0,
                    duration: 2,
                    ease: "power2.inOut",
                },
                "switch1"
            )
            // card-2 appear
            .from(
                "#describe-2",
                {
                    yPercent: 30,
                    scale: 1.2,
                    opacity: 0,
                    duration: 2,
                    ease: "power2.inOut",
                },
                "switch1"
            )
            // img-1 appear
            .from(
                "#img-area",
                {
                    // backgroundColor: "#e5dcd1",
                    scale: 0.8,
                    opacity: 0,
                    duration: 2,
                    ease: "power2.inOut",
                },
                "switch1"
            )
            // switch2---------------------
            // card-2 disappear
            .to(
                "#describe-2",
                {
                    yPercent: -30,
                    scale: 0.8,
                    opacity: 0,
                    duration: 2,
                    ease: "power2.inOut",
                },
                "switch2"
            )
            // img-1 disappear
            .to(
                "#img-1",
                {
                    scale: 0.8,
                    opacity: 0,
                    duration: 2,
                    ease: "power2.inOut",
                },
                "switch2"
            )
            // card-3 appear
            .from(
                "#describe-3",
                {
                    yPercent: 30,
                    scale: 1.2,
                    opacity: 0,
                    duration: 2,
                    ease: "power2.inOut",
                },
                "switch2"
            )
            // img-2 appear
            .from(
                "#img-2",
                {
                    scale: 0.8,
                    opacity: 0,
                    duration: 2,
                    ease: "power2.inOut",
                },
                "switch2"
            );
    },
    methods: {
    }
};

</script>



<template>
    <!-- 把區塊切成左右兩格，右邊留給雕像 -->
    <div id="artist-section" class="w-full h-dvh mx-auto grid grid-cols-5 gap-0 mb-5">
        <!-- 左側文字區 -->
        <div class="h-dvh col-span-5 md:col-span-3 flex flex-col items-center bg-white/70 md:bg-transparent">
            <!-- 標題 -->
            <h2 class="w-full h-1/3 pl-3 sm:pl-16 text-3xl md:text-5xl font-bold content-center">林之助</h2>
            <div class="w-5/6 md:w-4/5 lg:w-3/5 text-justify relative">
                <div class="w-100 absolute top-0 left-0 text-md sm:text-lg font-medium whitespace-pre-line"
                    v-for="text in artistDescribe" :key="text.id" :id="text.id">
                    {{ text.content }}
                </div>
            </div>
        </div>
        <!-- 右側圖片區 -->
        <div id="img-area" class="w-0 md:w-auto md:col-span-2 flex flex-col justify-center items-center overflow-hidden opacity-1">
            <img class="img w-full absolute rounded-md" v-for="img in artistImg" :key="img.id" :id="img.id"
                :src="img.src" :alt="img.src">
        </div>
    </div>
</template>