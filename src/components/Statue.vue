<script>
import * as THREE from 'three';
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader.js';
import { gsap } from "gsap";
import { ScrollTrigger, Observer } from "gsap/all";
import LCC from '@/assets/model/LCC.fbx';

export default {
    data() {
        return {

        }
    },
    methods: {
        model() {
            // 初始變數設定
            const scene = new THREE.Scene();
            const modelArea = document.querySelector('#statue-section');
            const camera = new THREE.OrthographicCamera(modelArea.clientWidth / - 2, modelArea.clientWidth / 2, modelArea.clientHeight / 2, modelArea.clientHeight / - 2, 0.0001, 1000);
            camera.position.set(modelArea.clientWidth / 3, 350, 250);
            let mouseX = 0, mouseY = 0;
            const maxRotation = 0.1; // 限制旋轉角度的範圍

            // 渲染器
            const renderer = new THREE.WebGLRenderer({ alpha: true });  //渲染透明色
            renderer.setSize(modelArea.clientWidth, modelArea.clientHeight);
            modelArea.appendChild(renderer.domElement);

            // RWD
            function resize() {
                renderer.setSize(modelArea.clientWidth, modelArea.clientHeight);
                camera.aspect = modelArea.clientWidth / modelArea.clientHeight;
                camera.updateProjectionMatrix();
            }
            window.addEventListener('resize', resize, false);
            resize();

            // 光線
            const AmbientLight = new THREE.AmbientLight(0xffffff, 10); // 環境光
            scene.add(AmbientLight);
            const light = new THREE.PointLight(0xffffff, 1000000, 1000);
            light.position.set(50, 500, 300);
            scene.add(light);
            const light2 = new THREE.PointLight(0xffffff, 1000000, 1000);
            light2.position.set(modelArea.clientWidth * 3 / 5, 500, 300);
            scene.add(light2);


            // 模型導入
            const statue = new THREE.Object3D();
            const loader = new FBXLoader();
            loader.load(LCC, (object) => {
                // 調整模型的位置和縮放
                object.position.set(0, 0, 0);
                object.scale.set(1.3, 1.3, 1.3);  // 根據需求調整
                object.rotation.y = Math.PI / 2
                statue.add(object);
            }, undefined, (error) => {
                console.error('載入模型時出錯：', error);
            });
            scene.add(statue);
            // statue.rotation.y = Math.PI / 2;

            // 監聽滑鼠移動事件
            document.addEventListener('mousemove', onMouseMove, false);

            function onMouseMove(event) {
                // 將滑鼠座標轉換為 [-0.5, 0.5] 的範圍
                mouseX = (event.clientX / window.innerWidth) - 0.5;
                mouseY = (event.clientY / window.innerHeight) - 0.5;
            }


            // 畫面更新
            function animate() {
                // 根據滑鼠位置來稍微旋轉攝像機
                camera.rotation.y = mouseX * maxRotation; // 控制水平旋轉
                camera.rotation.x = -mouseY * maxRotation; // 控制垂直旋轉

                requestAnimationFrame(animate);
                renderer.render(scene, camera);
            }
            animate();

            // 滾輪動畫

            gsap.registerPlugin(ScrollTrigger, Observer);

            // Timeline Animations 設定動畫細節
            let moveToRight = gsap.timeline();
            // moveToRight.to("#statue-section", { y: "30%", opacity: 0, duration: 0.3, ease: "power2.inOut" }, { y: "10%", opacity: 1, duration: 0.3, ease: "power2.inOut" }, 0);

            moveToRight.to("#statue-section", {
                scrollTrigger: {
                    scrub: 1,
                    trigger: "#statue-section",
                    start: "top top",
                    end: "160% top",
                    // pin: true,
                    // markers: true,
                    onUpdate: (self) => {
                        if (self.progress < 0.5) {
                            statue.rotation.y = Math.PI / - 1 * (self.progress / 0.5);
                            statue.position.x = modelArea.clientWidth * 2 / 3 * (self.progress / 0.5);
                            statue.scale.set(1, 1, 1);
                            // statue.position.y = -700 * self.progress;
                        } else {
                            statue.rotation.y = - 2 * Math.PI * (self.progress);
                            if (self.progress > 0.8) {
                                statue.scale.set(5 - 5 * self.progress, 5 - 5 * self.progress, 5 - 5 * self.progress);
                            }
                        }
                    },
                },
            }
            );
        },
        movement() {

        }
    },
    mounted() {
        this.model();
    }
};

</script>



<template>
    <div id="statue-section" class="fixed container h-dvh top-0 left-1/2 -translate-x-1/2"></div>
</template>