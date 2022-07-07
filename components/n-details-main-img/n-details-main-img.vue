<template>
	<view class="collection-bg">
	    <view id="threeView" class="media-wrap"></view>
	</view>
</template>

<script module="test" lang="renderjs">
	// import THREE from 'three/build/three.min.js'
	const THREE = require('three')
    import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
    
    	// 导入 glb 格式模型，若要导入其他格式模型，可尝试在 loaders 目录下加载其他文件
    import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
	let renderer;
	let scene;
	let camera;
	let controls;
	export default {
		name:"n-des-main",
		props:{
			url: String,
		},
		data() {
			return {
				isImg: true,
			};
		},
		mounted() {
			this.initThree();
		},
		methods:{
			// 导入模型
			leadModel() {
				let loader = new GLTFLoader();
				// 导入本地或者服务器上的模型都可以
				loader.load('https://threejs.org/examples/models/gltf/RobotExpressive/RobotExpressive.glb', function(gltf) {
					// loader.load('https://threejs.org/examples/models/gltf/RobotExpressive/RobotExpressive.glb', function(gltf) {
					scene.add(gltf.scene);
				});
			},
			initThree(){
				scene = new THREE.Scene();
				
				// var ambient = new THREE.AmbientLight(0xffffff,2);
				// scene.add(ambient);
				//设置了六个平行光 
				const directionLight1 = new THREE.DirectionalLight(0xffffff, 1);
				directionLight1.position.set(-300,0,0)
				scene.add(directionLight1);
		
				const directionLight2 = new THREE.DirectionalLight(0xffffff, 1);
				directionLight2.position.set(300,0,0)
				scene.add(directionLight2);
				
				const directionLight3 = new THREE.DirectionalLight(0xffffff, 1);
				directionLight3.position.set(0,300,0)
				scene.add(directionLight3);
				
				const directionLight4 = new THREE.DirectionalLight(0xffffff, 1);
				directionLight4.position.set(0,300,0)
				scene.add(directionLight4);
		
				const directionLight5 = new THREE.DirectionalLight(0xffffff, 1);
				directionLight5.position.set(0,0,-300)
				scene.add(directionLight5);
		
				const directionLight6 = new THREE.DirectionalLight(0xffffff, 1);
				directionLight6.position.set(0,0,300)
				scene.add(directionLight6);

				scene.position.y=-3
				
				const element = document.getElementById('threeView');
				const rect = element.getBoundingClientRect();


				let width = rect.width; // 窗口宽度
				let height = rect.height; // 高度
				var k = width / height; // 窗口宽高比
				var s = 1000; // 三维场景显示范围控制系数，系数越大，显示的范围越大
				
				camera = new THREE.PerspectiveCamera(30, k, 1, 10000);
				
				camera.position.set(0, 0, 20); //设置相机的摆放位置
				camera.lookAt(new THREE.Vector3(0, 0, 0)); // 控制相机的焦点(镜头)位置，决定相机的朝向（取值为3维坐标对象-THREE.Vector3(x,y,z)）
			
			
				renderer = new THREE.WebGLRenderer({
					antialias: true,
					// alpha: true //设置透明，为true时，背景颜色需要注释掉
				});
				
				//设置设备像素比。通常用于避免HiDPI设备上绘图模糊
				renderer.setPixelRatio( window.devicePixelRatio );
				renderer.setSize(width, height);
				renderer.setClearColor(0xffffff,0);
				renderer.outputEncoding = THREE.sRGBEncoding;
				renderer.toneMapping = THREE.ACESFilmicToneMapping;
				renderer.toneMappingExposure = 1;
				renderer.outputEncoding = THREE.sRGBEncoding;
				
				element.appendChild(renderer.domElement);
				renderer.render(scene,camera);
				//创建控制器
				controls = new OrbitControls(camera, renderer.domElement);
				controls.enabled = false;
				controls.enableRotate =false;
				controls.enableZoom = false;
				controls.autoRotate = true;
				
				this.leadModel();
				this.render();
			},
			render() {
				requestAnimationFrame(() => {
					this.render();
				});
				controls.update();
				renderer.render(scene,camera); //执行渲染操作
			},
		}
	}
</script>

<style lang="scss" scoped>
.collection-bg{
    width: 100%;
    height: 760rpx;
    background: url('../../static/energy/collection-bg.png') left 0 top 0 no-repeat;
    background-size: 100% 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    .collection{
        width: 450rpx;
        height: 450rpx;
        position: relative;
        margin-bottom: 60rpx;
        &.collection-video-wrap{
            width: 660rpx;
        }
        image{
            width: 100%;
            height: 100%;
            border-radius: 30rpx;
        }
        .collection-border{
            --border-radius: 30rpx;
            --border-width: 4rpx;
            appearance: none;
            position: relative;
            padding: 14rpx 6rpx 6rpx 14rpx;
            border: 0;
            font-weight: 500;
            color: #fff;
            z-index: 2;
            width: 100%;
            height: 100%;
            box-sizing: border-box;
            &.collection-video{
                --border-width: 0rpx;
            }
            image{
                padding: 4rpx 0 0 4rpx;
            }
            &::after{
                --m-i: linear-gradient(#000, #000);
                --m-o: content-box, padding-box;
                content: "";
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                height: 100%;
                z-index: -1;
                padding: var(--border-width);
                border-radius: var(--border-radius);
                background-image: conic-gradient(#F59EAA, #7FDEFF, #F59EAA);
                -webkit-mask-image: var(--m-i), var(--m-i);
                mask-image: var(--m-i), var(--m-i);
                -webkit-mask-origin: var(--m-o);
                mask-origin: var(--m-o);
                mask-clip: var(--m-o);
                mask-composite: exclude;
                -webkit-mask-composite: destination-out;
            }
        }
    }
    .rarity{
        width: 116rpx;
        height: 116rpx;
        position: absolute;
        right: 36rpx;
        bottom: 0;
        image{
            width: 100%;
            height: 100%;
        }
    }
}

.media-wrap{
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.details-img{
		width: 100%;
		height: 100%;
		border-radius: 30rpx;
	}
	.details-video{
		width: 100%;
		height: 100%;
		padding: 6rpx 0 0 6rpx;
		border: 4px solid;
    	border-image:  linear-gradient(90deg, rgba(247, 157, 168, 1) 0%, rgba(148, 226, 252, 1) 100%)30 30;;
	}
</style>