<script>
import * as THREE from 'three';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import colorWall from '@/assets/model/COLORSHELF2.glb';


gsap.registerPlugin(ScrollTrigger);

export default {
    data() {
        return {

        };
    },
    mounted() {
        this.initThree();
    },

    methods: {
        initThree() {
            const scene = new THREE.Scene();

            const camera = new THREE.PerspectiveCamera(75, this.$refs.threeCanvas.clientWidth / this.$refs.threeCanvas.clientHeight, 0.1, 1000);

            const renderer = new THREE.WebGLRenderer({ alpha: true });
            // const renderer = new THREE.WebGLRenderer();

            renderer.domElement.classList.add('pointer-events-none');

            renderer.setSize(this.$refs.threeCanvas.clientWidth, this.$refs.threeCanvas.clientHeight);
            this.$refs.threeCanvas.appendChild(renderer.domElement);

            //模型跟著rwd
            const resize = () => {
                renderer.setSize(this.$refs.threeCanvas.clientWidth, this.$refs.threeCanvas.clientHeight);
                camera.aspect = this.$refs.threeCanvas.clientWidth / this.$refs.threeCanvas.clientHeight;
                camera.updateProjectionMatrix();
            };
            window.addEventListener('resize', resize);
            resize(); // 初始调⽤

            // renderer.setPixelRatio(window.devicePixelRatio);

            const allLight = new THREE.AmbientLight(0x404040, 10);
            scene.add(allLight);

            const light = new THREE.HemisphereLight(0xffffbb, 0x080820, 2);
            scene.add(light);

            const bottle1 = new THREE.Object3D();
            bottle1.visible = false;
            const bottle2 = new THREE.Object3D();
            bottle2.visible = false;
            const bottle3 = new THREE.Object3D();
            bottle3.visible = false;
            const bottle4 = new THREE.Object3D();
            bottle4.visible = false;
            const bottle5 = new THREE.Object3D();
            bottle5.visible = false;
            const bottle6 = new THREE.Object3D();
            bottle6.visible = false;
            const bottle7 = new THREE.Object3D();
            bottle7.visible = false;
            const bottle8 = new THREE.Object3D();
            bottle8.visible = false;
            const bottle9 = new THREE.Object3D();
            bottle9.visible = false;
            const bottle10 = new THREE.Object3D();
            bottle10.visible = false;
            const bottle11 = new THREE.Object3D();
            bottle11.visible = false;
            const bottle12 = new THREE.Object3D();
            bottle12.visible = false;
            const bottle13 = new THREE.Object3D();
            bottle13.visible = false;
            const bottle14 = new THREE.Object3D();
            bottle14.visible = false;
            const bottle15 = new THREE.Object3D();
            bottle15.visible = false;
            const bottle16 = new THREE.Object3D();
            bottle16.visible = false;
            const bottle17 = new THREE.Object3D();
            bottle17.visible = false;
            const bottle18 = new THREE.Object3D();
            bottle18.visible = false;
            const bottle19 = new THREE.Object3D();
            bottle19.visible = false;
            const bottle20 = new THREE.Object3D();
            bottle20.visible = false;
            const bottle21 = new THREE.Object3D();
            bottle21.visible = false;
            const bottle22 = new THREE.Object3D();
            bottle22.visible = false;
            const bottle23 = new THREE.Object3D();
            bottle23.visible = false;
            const bottle24 = new THREE.Object3D();
            bottle24.visible = false;


            const loader = new GLTFLoader();
            loader.load(colorWall,
                (item) => {
                    console.log(item);
                    const box = new THREE.Box3().setFromObject(item.scene);
                    const center = box.getCenter(new THREE.Vector3());
                    item.scene.position.sub(center); //模型中心設為原點
                    let shelf = item.scene;

                    bottle1.add(item.scene.children[25]);
                    bottle2.add(item.scene.children[63]);
                    bottle3.add(item.scene.children[104]);
                    bottle4.add(item.scene.children[147]);
                    bottle5.add(item.scene.children[178]);
                    bottle6.add(item.scene.children[207]);
                    bottle7.add(item.scene.children[251]);
                    bottle8.add(item.scene.children[279]);
                    bottle9.add(item.scene.children[287]);
                    bottle10.add(item.scene.children[77]);
                    bottle11.add(item.scene.children[151]);
                    bottle12.add(item.scene.children[222]);
                    bottle13.add(item.scene.children[6]);
                    bottle14.add(item.scene.children[129]);
                    bottle15.add(item.scene.children[192]);
                    bottle16.add(item.scene.children[108]);
                    bottle17.add(item.scene.children[244]);
                    bottle18.add(item.scene.children[74]);
                    bottle19.add(item.scene.children[166]);
                    bottle20.add(item.scene.children[269]);
                    bottle21.add(item.scene.children[51]);
                    bottle22.add(item.scene.children[135]);
                    bottle23.add(item.scene.children[230]);
                    bottle24.add(item.scene.children[14]);

                    // 初始化滾動觸發

                    // 配置瓶子的位置和缩放
                    this.setBottlePositionAndScale([bottle1, bottle2, bottle3, bottle4, bottle5, bottle6, bottle7, bottle8, bottle9, bottle10, bottle11, bottle12, bottle13, bottle14, bottle15, bottle16, bottle17, bottle18, bottle19, bottle20, bottle21, bottle22, bottle23, bottle24,]);

                    shelf.position.set(0, 30, 0); // 初始位置
                    shelf.scale.set(50, 50, 50);
                    shelf.rotation.x = Math.PI / 2; // 俯视角度
                    scene.add(shelf);
                    scene.add(bottle1, bottle2, bottle3, bottle4, bottle5, bottle6, bottle7, bottle8, bottle9, bottle10, bottle11, bottle12, bottle13, bottle14, bottle15, bottle16, bottle17, bottle18, bottle19, bottle20, bottle21, bottle22, bottle23, bottle24,);

                    // 初始化滚动触发器
                    this.initScrollTrigger(shelf);

                    // 给不同的瓶子组设置不同的动画延迟
                    this.animateBottles([bottle1, bottle4, bottle9], "45% center", "60% center", 0);
                    this.animateBottles([bottle3, bottle5, bottle8], "50% center", "65% center", 0.1); // 延遲0.1s
                    this.animateBottles([bottle2, bottle6, bottle7], "55% center", "70% center", 0.2); // 延遲0.2s
                    this.animateBottles([bottle10, bottle11, bottle12], "60% center", "75% center", 0.3); // 延遲0.3s
                    this.animateBottles([bottle13, bottle14, bottle15], "65% center", "80% center", 0.4); // 延遲0.4s
                    this.animateBottles([bottle16, bottle17, bottle18], "70% center", "85% center", 0.5); // 延遲0.5s
                    this.animateBottles([bottle19, bottle20, bottle21], "75% center", "90% center", 0.6); // 延遲0.6s
                    this.animateBottles([bottle22, bottle23, bottle24], "80% center", "95% center", 0.7); // 延遲0.7s

                }, undefined, function (error) {
                    console.error('模型載入錯誤', error);
                });


            camera.position.set(0, 0, 100);


            // 4. 動畫循環
            const animate = () => {
                requestAnimationFrame(animate);
                renderer.render(scene, camera);
            };

            animate();
        },

        setBottlePositionAndScale(bottles) {
            bottles.forEach((bottle, index) => {
                bottle.position.set(10, -5, 0);
                bottle.scale.set(80, 80, 80);
            });
        },


        initScrollTrigger(shelf) {
            ScrollTrigger.create({
                trigger: "#shelf",
                start: "top 20%",
                end: "center center",
                scrub: 0.5, //調整scrub值可使滾動更滑順
                // markers: true,
                // pin:true,
                onUpdate: (self) => {

                    const progress = self.progress;

                    // 控制 shelf 的旋轉
                    if (shelf) {
                        shelf.rotation.x = Math.min(Math.PI / 2 - (progress * Math.PI / 2), Math.PI / 2);
                        // shelf.rotation.x = Math.PI / 2 - (progress * Math.PI / 2);
                        shelf.position.y = 30 - (progress * 35); // shelf 往下移動
                    };
                },

            });
        },

        // 用於瓶子
        animateBottles(bottles, start, end, delay) {
            ScrollTrigger.create({
                trigger: "#shelf",
                start: start,
                end: end,
                scrub: 0.5,
                // markers: true,
                onUpdate: (self) => {
                    const btProgress = self.progress;

                    if (btProgress > delay) {
                        bottles.forEach((bottle) => {
                            bottle.visible = true;
                            const scale = 80 - (btProgress * 30); // 缩小瓶子
                            bottle.scale.set(scale, scale, scale);
                            const newX = 10 - (btProgress * 10); // X軸移動
                            bottle.position.set(newX, -5, 0);
                        });
                    } else {
                        bottles.forEach((bottle) => {
                            bottle.visible = false;
                        });
                    }
                }
            });
        }

    },
}
</script>

<template>
    <div id="shelf" ref="threeCanvas" class="absolute w-full h-dvh top-0 z-1"></div>
</template>

<style scope>
.pointer-events-none {
    pointer-events: none !important;
}

#shelf,
#shelf * {
    pointer-events: none;
}
</style>
