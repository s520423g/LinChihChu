<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import wallTest from "@/components/WallTest.vue";
import { nextTick } from 'vue';

gsap.registerPlugin(ScrollTrigger);

export default {

    components: {
        wallTest,
    },

    data() {
        return {
            resizeTimeout: null,
            currentWidth: window.innerWidth, // 初始化當前寬度
        };
    },

    mounted() {
        window.addEventListener("resize", this.handleResize);
        nextTick(() => {
            this.updateAnimation();
        });
        window.addEventListener("resize", this.updateSVGForMediaQuery);
        this.updateSVGForMediaQuery();
    },

    beforeDestroy() {
        window.removeEventListener("resize", this.handleResize);
        clearTimeout(this.resizeTimeout);
    },

    methods: {
        handleResize() {
            clearTimeout(this.resizeTimeout);

            this.resizeTimeout = setTimeout(() => {
                const newWidth = window.innerWidth;

                if (newWidth !== this.currentWidth) {
                    this.currentWidth = newWidth;
                    this.updateAnimation();
                    location.reload();
                }
            }, 0);
        },

        updateAnimation() {
            const wallTestElement = this.$refs.wallTestRef.$el;
            const theLine = document.querySelector("#theline");

            const pathLength = theLine.getTotalLength();
            theLine.style.strokeDasharray = pathLength;
            theLine.style.strokeDashoffset = pathLength;

            // 滾動放大動畫
            gsap.from("#wallSection", {
                scrollTrigger: {
                    trigger: "#wallSection",
                    start: "top 80%",
                    end: "+=500",
                    scrub: 1,
                },
                scaleX: 0.7,
            });

            let cardtl = gsap.timeline({
                scrollTrigger: {
                    trigger: "#wallSection",
                    start: "bottom bottom",
                    end: "+=5500",
                    scrub: 1,
                    pin: true,
                    anticipatePin: 1,
                },
            });

            cardtl
                .from(".section-title-1", { yPercent: 30, scale: 1.2, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch1")
                .from(".con-1", { yPercent: 30, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch1")
                .to(".con-1", { yPercent: -30, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch2")
                .from(".con-2", { opacity: 0, yPercent: 30, duration: 2, ease: "power2.inOut" }, "switch2")
                .to(".con-2", { opacity: 0, yPercent: -30, duration: 2, ease: "power2.inOut" }, "switch3")
                .from(".con-3", { opacity: 0, yPercent: 30, duration: 2, ease: "power2.inOut" }, "switch3")
                .to(".section-title-1", { yPercent: -30, scale: 0.8, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch4")
                .from(".section-title-2", { yPercent: 30, scale: 1.2, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch4+=0.5")
                .from(".col-1", { yPercent: 30, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch4+=0.5")
                .to(".col-1", { yPercent: -30, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch5")
                .from(".col-2", { opacity: 0, yPercent: 30, duration: 2, ease: "power2.inOut" }, "switch5")
                .to(".section-title-2", { yPercent: -30, scale: 0.8, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch6+=1")
                .from(".section-title-3", { yPercent: 30, scale: 1.2, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch6+=1")
                .from(".tip-1", { yPercent: 30, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch6+=1")
                .to(".tip-1", { yPercent: -30, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch7")
                .from(".tip-2", { opacity: 0, yPercent: 30, duration: 2, ease: "power2.inOut" }, "switch7")
                .to(wallTestElement, { opacity: 0, duration: 4, ease: "power2.inOut" }, "switch7")
                .to(".section-title-3", { yPercent: -30, scale: 0.8, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch8")
                .from(".section-title-4", { yPercent: 30, scale: 1.2, opacity: 0, duration: 2, ease: "power2.inOut" }, "switch8+=0.5")
                .fromTo("#theline", { strokeDashoffset: pathLength }, { strokeDashoffset: 0, duration: 4, ease: "power1.inOut" }, "switch9");

            ScrollTrigger.refresh();  // 放在最後
        },

        updateSVGForMediaQuery() {
            const line = document.getElementById('theline');
            const balls = document.querySelectorAll('.ball');

            if (window.innerWidth <= 1200) {
                // 更新曲線為直線
                line.setAttribute('d', 'M 40 3 L 40 97');

                // 更新每個圓點的位置
                const positions = [
                    { cx: 40, cy: 3 },
                    { cx: 40, cy: 11 },
                    { cx: 40, cy: 19 },
                    { cx: 40, cy: 27 },
                    { cx: 40, cy: 35 },
                    { cx: 40, cy: 43 },
                    { cx: 40, cy: 51 },
                    { cx: 40, cy: 59 },
                    { cx: 40, cy: 67 },
                    { cx: 40, cy: 75 },
                    { cx: 40, cy: 83 },
                    { cx: 40, cy: 90 },
                    { cx: 40, cy: 97 },
                ];

                balls.forEach((ball, index) => {
                    if (positions[index]) {
                        ball.setAttribute('cx', positions[index].cx);
                        ball.setAttribute('cy', positions[index].cy);
                    }
                });
            }

            if (window.innerWidth <= 699) {
                // 更新曲線為直線
                line.setAttribute('d', 'M 10 11 L 10 95');

                // 更新每個圓點的位置
                const positions = [
                    { cx: 10, cy: 11 },
                    { cx: 10, cy: 18 },
                    { cx: 10, cy: 25 },
                    { cx: 10, cy: 32 },
                    { cx: 10, cy: 39 },
                    { cx: 10, cy: 46 },
                    { cx: 10, cy: 53 },
                    { cx: 10, cy: 60 },
                    { cx: 10, cy: 67 },
                    { cx: 10, cy: 74 },
                    { cx: 10, cy: 81 },
                    { cx: 10, cy: 88 },
                    { cx: 10, cy: 95 },
                ];

                balls.forEach((ball, index) => {
                    if (positions[index]) {
                        ball.setAttribute('cx', positions[index].cx);
                        ball.setAttribute('cy', positions[index].cy);
                    }
                });
            }
        },
    },
}
</script>

<template>
    <div id="wallSection" class="relative w-full h-[100dvh] mb-5 overflow-hidden">
        <div class="w-full h-full absolute top-0 flex-row content-center z-50">
            <div class="w-1/2 flex-row p-[15px] section-title-1 absolute top-[10%] right-[10px] ">
                <div
                    class="title-all bg-[#DCCBC2]/75 rounded-t-3xl p-[15px] text-4xl font-extrabold mb-2 text-[#6c7865]">
                    何謂膠彩
                </div>
                <div class="text-lg gouache-content relative text-[#556069]">
                    <div class="bg-[#DCCBC2]/75 rounded-b-3xl p-[15px] con-1 absolute top-0">
                        林之助於1977年提出膠彩畫正名：指凡用膠水（鹿膠、牛膠、魚膠等）作媒劑，調入磺物質顏料、水干顏料、植物性顏料或金屬性顏料（金、銀、鋁等），在紙、絹、麻或木板上所畫出來的畫都稱為「膠彩畫」；其中，並不限定哪一種風格、技法、地域。
                    </div>
                    <div class="bg-[#DCCBC2]/75 rounded-b-3xl p-[15px] con-2 absolute top-0">
                        以天然膠料調製大自然的色料描繪形體，是人類最古老的繪畫形式。此種以膠兌彩的繪畫，在中國唐宋發展成熟，出現金碧、青綠及重彩畫風格，並東傳朝鮮、日本，流行於亞洲地區。此外，西藏的唐卡、印度的細密畫都是以膠兌彩的繪畫類型。
                    </div>
                    <div class="bg-[#DCCBC2]/75 rounded-b-3xl p-[15px] con-3 absolute top-0">
                        唐宋繪畫傳入日本，發展成日本畫。<br>
                        1895年臺灣隨著日本殖民文化政策，「日本畫」傳入臺灣，改稱為「東洋畫」，取代水墨畫，成為畫壇的新主流。<br>
                        1945年再次的政權轉換，東洋畫改稱國畫納入美展部門。<br>
                        1950年代與水墨畫產生正統國畫論爭。中原水墨又取代了東洋畫，東洋畫沒落幾近消失。<br>
                        1977年，膠彩畫家林之助提倡以國際慣用媒劑素材命名，提出「膠彩畫」取代「東洋畫」的正名呼籲，逐漸獲得認同開始再興。正名後的臺灣膠彩畫，以礦物顏料及動物膠為理論、創作核心，不斷強調礦物顏料的材質美感及保存性，在臺灣畫壇形塑了獨特的繪畫風格特色，引起廣大的興趣與學習，近20年快速發展。
                    </div>
                </div>
            </div>
            <div class="w-1/2 flex-row p-[15px] section-title-2 absolute top-[30%] left-[10px]">
                <div
                    class="title-all bg-[#DCCBC2]/75 rounded-t-3xl p-[15px] text-4xl font-extrabold mb-2 text-[#6c7865]">
                    天然礦物顏料
                </div>
                <div class="text-lg aboutColor-content h-fit w-auto relative text-[#556069]">
                    <div class="col-1 bg-[#DCCBC2]/75 rounded-b-3xl p-[15px] absolute top-0">
                        一、礦物顆粒結構可分為結晶體與非結晶體，其中因為礦物顏料 的結構在放大鏡下是多塊面的晶體顆粒結構，有不同角度的斷面，礦物顏料層受光後，會產生獨特的發光效果，具高雅微妙色彩質感。
                    </div>
                    <div class="col-2 bg-[#DCCBC2]/75 rounded-b-3xl p-[15px] absolute top-0">
                        二、礦物顏料的顏色深淺，由顆粒的粗細決定，顆粒粗者顏色深，顆粒細者顏色較淺。而顆粒粗細由號數來表示，號數越小，顆粒越粗；反之，號數越大，顆粒越細。
                    </div>
                </div>
            </div>
            <div class=" w-1/2 flex-row p-[15px] section-title-3 absolute top-[55%] right-[10px]">
                <div
                    class="title-all bg-[#DCCBC2]/75 rounded-t-3xl p-[15px] text-4xl font-extrabold mb-2 text-[#6c7865]">
                    礦物顏料製作步驟
                </div>
                <div class="text-lg colorTips-content h-fit w-auto relative text-[#556069]">
                    <div class="tip-1 bg-[#DCCBC2]/75 rounded-b-3xl p-[15px] absolute top-0">
                        步驟因原石成分、品質的不同，而以不同的程序操作，甚至有時刻意忽略其中某些步驟，裂作出豐富的中灰色階泌礦物顏料質感高雅，且永不退色，自古以來一直是最佳的繪畫顏料。
                    </div>
                    <div class="tip-2 bg-[#DCCBC2]/75 rounded-b-3xl p-[15px] absolute top-0">
                        礦物顏料的製作過程相當複雜繁瑣，步驟有洗、挑、搗、籮、淘、研、煮、漂、水磨、過磁、水飛、水漂、乾燥等過程。 </div>
                </div>
            </div>
            <div class="w-full h-full section-title-4 text-[#556069] text-xl relative">
                <div class="text-con text-con-1 flex absolute left-[15%] top-[5%]">
                    1.
                    製作各種礦物顏料礦石
                </div>
                <div class="text-con text-con-2 flex absolute left-[30%] top-[20%]">
                    2.
                    礦石的條痕決定了製成顏料的色彩
                </div>
                <div class="text-con text-con-3 flex absolute left-[20%] top-[35%]">
                    3. 清洗礦石
                </div>
                <div class="text-con text-con-4 flex absolute left-[5%] top-[55%]">
                    4. 篩選礦物依成色分類
                </div>
                <div class="text-con text-con-5 flex absolute left-[15%] top-[65%]">
                    5. 敲碎礦物去除不純物
                </div>
                <div class="text-con text-con-6 flex absolute left-[15%] top-[90%]">
                    6. 以粉碎機粉碎礦石
                </div>
                <div class="text-con text-con-7 flex absolute left-[35%] top-[75%]">
                    7. 以球磨機進行細磨
                </div>
                <div class="text-con text-con-8 flex absolute left-[55%] top-[60%]">
                    8. 以金屬篩網篩分粗細
                </div>
                <div class="text-con text-con-9 flex absolute left-[35%] top-[45%]">
                    9. 依礦石比重顆粒不同，以水飛法分粗細
                </div>
                <div class="text-con text-con-10 flex absolute left-[70%] top-[30%]">
                    10. 以水飛水漂分出粗細不同號數顏料
                </div>
                <div class="text-con text-con-11 flex absolute left-[65%] top-[40%]">
                    11.
                    以人工掏洗雜質，獲得乾淨純度礦物顏料
                </div>
                <div class="text-con text-con-12 flex absolute left-[80%] top-[70%]">
                    12.
                    乾燥完成礦物顏料
                </div>
                <div class="text-con text-con-13 flex absolute left-[65%] top-[95%]">
                    13.
                    不同礦石製成礦物顏料
                </div>

                <svg id="svg" viewBox="0 0 100 100" preserveAspectRatio="none" width="100%" height="100%">
                    <!-- 使用 Q 命令繪製曲線，起點、控制點和終點改為相對百分比 -->
                    <path id="theline" d="
                    M 13 7 
                    Q 14 14 20 15 
                    T 28 22
                    T 18 37
                    Q 13 43 8 48
                    T 2.5 57
                    Q 3 65 8 62
                    T 13 67
                    Q 13 70 10 75
                    T 17 87
                    T 33 77
                    Q 35 70 48 72
                    T 53 62
                    Q 48 55 38 60
                    T 33 47
                    Q 36 35 55 25
                    T 68 32
                    Q 67 36 65 38
                    T 63 42
                    Q 63 48 69 52
                    T 78 72
                    Q 80 83 70 80
                    T 63 97" stroke="#556069" stroke-width="0.3" fill="none" />

                    <!-- 圓形的位置也用百分比來處理，讓它跟著變化 -->


                    <circle class="ball" cx="13" cy="7" r="0.5" fill="#556069" />
                    <circle class="ball" cx="28" cy="22" r="0.5" fill="#556069" />
                    <circle class="ball" cx="18" cy="37" r="0.5" fill="#556069" />
                    <circle class="ball" cx="2.5" cy="57" r="0.5" fill="#556069" />
                    <circle class="ball" cx="13" cy="67" r="0.5" fill="#556069" />
                    <circle class="ball" cx="17" cy="87" r="0.5" fill="#556069" />
                    <circle class="ball" cx="33" cy="77" r="0.5" fill="#556069" />
                    <circle class="ball" cx="53" cy="62" r="0.5" fill="#556069" />
                    <circle class="ball" cx="33" cy="47" r="0.5" fill="#556069" />
                    <circle class="ball" cx="68" cy="32" r="0.5" fill="#556069" />
                    <circle class="ball" cx="63" cy="42" r="0.5" fill="#556069" />
                    <circle class="ball" cx="78" cy="72" r="0.5" fill="#556069" />
                    <circle class="ball" cx="63" cy="97" r="0.5" fill="#556069" />
                </svg>
            </div>
        </div>
        <wallTest ref="wallTestRef" />
    </div>
</template>

<style scoped>
@media (max-width:899px) {

    .section-title-1,
    .section-title-3 {
        width: 80%;
        right: 50%;
        transform: translateX(50%);
    }

    /* .section-title-3{
        top:30%;
    } */

    .section-title-2 {
        width: 80%;
        left: 50%;
        transform: translateX(-50%);
    }
}

@media (max-width:699px) {
    .title-all {
        font-size: 24px;
    }

    .gouache-content,
    .aboutColor-content,
    .colorTips-content {
        font-size: 16px;
    }
}


.theline {
    transition: d 0.5s ease;
}

.ball {
    transition: cx 0.5s ease, cy 0.5s ease;
}


@media (max-width:1300px) {
    .text-con {
        font-size: 18px;
    }
}

/* 當螢幕寬度為 1200px 或更大時，將曲線改為直線，並調整圓點位置 */
@media (max-width: 1200px) {

    /* 將曲線變成簡單直線 */
    /* .theline {
        d: path("M 40 3 L 40 97");
    } */

    /* 調整每個圓點的位置 */
    /* .ball:nth-child(2) {
        cx: 40;
        cy: 3;
    }

    .ball:nth-child(3) {
        cx: 40;
        cy: 11;
    }

    .ball:nth-child(4) {
        cx: 40;
        cy: 19;
    }

    .ball:nth-child(5) {
        cx: 40;
        cy: 27;
    }

    .ball:nth-child(6) {
        cx: 40;
        cy: 35;
    }

    .ball:nth-child(7) {
        cx: 40;
        cy: 43;
    }

    .ball:nth-child(8) {
        cx: 40;
        cy: 51;
    }

    .ball:nth-child(9) {
        cx: 40;
        cy: 59;
    }

    .ball:nth-child(10) {
        cx: 40;
        cy: 67;
    }

    .ball:nth-child(11) {
        cx: 40;
        cy: 75;
    }

    .ball:nth-child(12) {
        cx: 40;
        cy: 83;
    }

    .ball:nth-child(13) {
        cx: 40;
        cy: 90;
    }

    .ball:nth-child(14) {
        cx: 40;
        cy: 97;
    } */

    /* .text-con{
            position:unset;
            padding:12px;
        }

        .section-title-4{
            margin-left:30px;
        } */

    .text-con {
        left: 43%;
    }

    .text-con-1 {
        top: 1.5%;
    }

    .text-con-2 {
        top: 9.5%;
    }

    .text-con-3 {
        top: 17.5%;
    }

    .text-con-4 {
        top: 25.5%;
    }

    .text-con-5 {
        top: 33.5%;
    }

    .text-con-6 {
        top: 41.5%;
    }

    .text-con-7 {
        top: 49.5%;
    }

    .text-con-8 {
        top: 57.5%;
    }

    .text-con-9 {
        top: 65.5%;
    }

    .text-con-10 {
        top: 73.5%;
    }

    .text-con-11 {
        top: 81.5%;
    }

    .text-con-12 {
        top: 88.5%;
    }

    .text-con-13 {
        top: 95.5%;
    }

    /* .ball, .theline{
            display: none;
        } */

}

@media (max-width: 699px) {

    /* 將曲線變成簡單直線
    .theline {
        d: path("M 10 11 L 10 95");
    }

    /* 調整每個圓點的位置 */
    /* .ball:nth-child(2) {
        cx: 10;
        cy: 11;
    }

    .ball:nth-child(3) {
        cx: 10;
        cy: 18;
    }

    .ball:nth-child(4) {
        cx: 10;
        cy: 25;
    }

    .ball:nth-child(5) {
        cx: 10;
        cy: 32;
    }

    .ball:nth-child(6) {
        cx: 10;
        cy: 39;
    }

    .ball:nth-child(7) {
        cx: 10;
        cy: 46;
    }

    .ball:nth-child(8) {
        cx: 10;
        cy: 53;
    }

    .ball:nth-child(9) {
        cx: 10;
        cy: 60;
    }

    .ball:nth-child(10) {
        cx: 10;
        cy: 67;
    }

    .ball:nth-child(11) {
        cx: 10;
        cy: 74;
    }

    .ball:nth-child(12) {
        cx: 10;
        cy: 81;
    }

    .ball:nth-child(13) {
        cx: 10;
        cy: 88;
    }

    .ball:nth-child(14) {
        cx: 10;
        cy: 95;
    } */


    /* .section-title-4{
            margin-top:70px;
        } */

    .text-con {
        left: 15%;
    }

    .text-con-1 {
        top: 9.5%;
    }

    .text-con-2 {
        top: 16.5%;
    }

    .text-con-3 {
        top: 23.5%;
    }

    .text-con-4 {
        top: 30.5%;
    }

    .text-con-5 {
        top: 37.5%;
    }

    .text-con-6 {
        top: 44.5%;
    }

    .text-con-7 {
        top: 51.5%;
    }

    .text-con-8 {
        top: 58.5%;
    }

    .text-con-9 {
        top: 65.5%;
    }

    .text-con-10 {
        top: 72.5%;
    }

    .text-con-11 {
        top: 79.5%;
    }

    .text-con-12 {
        top: 86.5%;
    }

    .text-con-13 {
        top: 93%;
    }
}
</style>