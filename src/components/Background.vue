<script>
import * as THREE from 'three';
import { MarchingCubes } from 'three/addons/objects/MarchingCubes.js';


export default {
    mounted() {
        // 第一版 球
        this.initOne();
    },
    methods: {
        initOne() {
            let camera, scene, renderer;

            let materials;

            let light, pointLight, ambientLight;

            let effect, resolution;

            let effectController;

            let time = 0;

            const clock = new THREE.Clock();

            init();

            function init() {
                // 找 DOM
                const backgroundArea = document.getElementById('backgroundArea');

                // CAMERA

                camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 10000);
                camera.position.set(0, 0, 1000);
                camera.lookAt(0, 0, 0);

                // SCENE

                scene = new THREE.Scene();
                scene.background = new THREE.Color(0xD0C9BC); // 背景顏色

                // LIGHTS

                light = new THREE.DirectionalLight(0x767F86, 0.6);
                light.position.set(0.5, 0.5, 1);
                scene.add(light);

                pointLight = new THREE.PointLight(0x767F86, 3, 0, 0);
                pointLight.position.set(0, 0, 100);
                scene.add(pointLight);

                ambientLight = new THREE.AmbientLight(0xF7F3EA, 3); // 會反射成球體顏色
                scene.add(ambientLight);

                // MATERIALS

                materials = new THREE.MeshPhongMaterial();

                // MARCHING CUBES

                resolution = 28;

                effect = new MarchingCubes(resolution, materials, true, true, 100000);
                effect.position.set(0, 0, 0);
                effect.scale.set(1000, 1000, 100);
                effectController = {
                    speed: 0.1,
                    numBlobs: 20,
                    resolution: 60,
                    isolation: 20,

                    dummy: function () { }

                };

                scene.add(effect);

                // ----------------------------------------------------------------------
                // noise plane
                // 建立平面幾何
                const geometry = new THREE.PlaneGeometry(1500, 1500);

                // 高斯噪點的片段shader
                const fragmentShader = `
                    precision mediump float;

                    // GLSL偽隨機數生成器
                    float random(vec2 st) {
                        return fract(sin(dot(st.xy, vec2(12.9898, 78.233))) * 43758.5453123);
                    }

                    // 生成高斯噪點
                    float gaussianNoise(vec2 st) {
                        float r1 = random(st);
                        float r2 = random(st * 0.9); //噪點尺寸
                        return sqrt(-2.0 * log(r1)) * cos(2.0 * 3.14159265 * r2);
                    }

                    void main() {
                        vec2 st = gl_FragCoord.xy / vec2(500.0, 500.0); // 坐標標準化
                        float noise = gaussianNoise(st);  // 生成噪點

                        // 调整噪點强度，增加對比度，使其更锐利
                        noise = step(1.0, noise);  // 使用step函数二值化噪點(域值, noise)

                        // 背景色為黑色
                        vec3 backgroundColor = vec3(0.0, 0.0, 0.0); 

                        // 噪點的颜色為淺白色, 使用噪點的值作為透明度
                        float alpha = noise; // 使用二值化的噪點控制透明度
                        vec3 noiseColor = vec3(0.9, 0.9, 0.9);  // 噪點為淺白色

                        // 最终颜色：背景色 + 噪點的透明度控制
                        vec3 finalColor = mix(backgroundColor, noiseColor, alpha);
                        gl_FragColor = vec4(finalColor, alpha);  // 應用噪點作為透明度
                    }
                    `;

                // 使用ShaderMaterial
                const material = new THREE.ShaderMaterial({
                    fragmentShader: fragmentShader,
                    transparent: true // 允許透明度
                });

                // 創建平面放到場景
                const plane = new THREE.Mesh(geometry, material);
                scene.add(plane);
                plane.position.set(0, 0, 300)
                // --------------------------------------------------------------------

                // RENDERER

                renderer = new THREE.WebGLRenderer();
                renderer.setPixelRatio(window.devicePixelRatio);
                renderer.setSize(window.innerWidth, window.innerHeight);
                renderer.setAnimationLoop(animate);
                backgroundArea.appendChild(renderer.domElement);

                // EVENTS

                window.addEventListener('resize', onWindowResize);

            }

            // 函式區

            function onWindowResize() {

                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();

                renderer.setSize(window.innerWidth, window.innerHeight);

            }

            // this controls content of marching cubes voxel field

            function updateCubes(object, time, numblobs) {

                object.reset();

                // 生成球體
                const subtract = 12;
                const strength = 1.2 / ((Math.sqrt(numblobs) - 1) / 4 + 1);

                for (let i = 0; i < numblobs; i++) {

                    const ballx = Math.sin(i + 1.26 * time * (1.03 + 0.5 * Math.cos(0.21 * i))) * 0.27 + 0.5;
                    const bally = Math.abs(Math.cos(i + 1.12 * time * Math.cos(1.22 + 0.1424 * i))) * 0.77; // dip into the floor
                    const ballz = Math.cos(i + 1.32 * time * 0.1 * Math.sin((0.92 + 0.53 * i))) * 0.27 + 0.5;
                    
                    object.addBall(ballx, bally, ballz, strength, subtract);

                }

                object.update();

            }

            // 渲染回圈

            function animate() {

                render();

            }

            function render() {

                const delta = clock.getDelta();

                time += delta * effectController.speed * 0.5;

                // marching cubes

                if (effectController.resolution !== resolution) {

                    resolution = effectController.resolution;
                    effect.init(Math.floor(resolution));

                }

                if (effectController.isolation !== effect.isolation) {

                    effect.isolation = effectController.isolation;

                }

                updateCubes(effect, time, effectController.numBlobs);

                // render

                renderer.render(scene, camera);

            }
        },
    },
};
</script>

<template>
    <div id="backgroundArea" class="background w-full h-dvh fixed top-0 left-0 -z-10">
    </div>
</template>