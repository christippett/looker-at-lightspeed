<script>
	import { onMount } from 'svelte';
	import {
		AddOperation,
		Fog,
		Mesh,
		MeshBasicMaterial,
		PerspectiveCamera,
		PlaneGeometry,
		Scene,
		SphereBufferGeometry,
		WebGLRenderer
	} from 'three';

	//1. Call for Three.js libraries
	let camera, scene, renderer;
	//2. Create an array to store stars
	let stars = [];
	//3 Asd a filter
	let planeMesh;
	//4.Speed of the stars

	const colors = ['#FFFFFF', '#DA77F2', '#4DABF7', '#FFFCDF', '#845EF7'];
	const normalSpeed = 0.05;
	const lightSpeed = 0.26;

	let speed = normalSpeed;
	export let activated = false;

	/*---------------------
      Implementation
  ---------------------*/

	function init() {
		//Set up the scene
		scene = new Scene();
		scene.fog = new Fog(0x000000, 0.015, 72);
		//Set up the camera
		camera = new PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
		renderer = new WebGLRenderer({ preserveDrawingBuffer: true, alpha: true });
		renderer.sortObjects = false;
		renderer.autoClearColor = false;

		//Camera initialisation
		camera.position.z = 55;

		//Add the background
		renderer.setClearColor('#000', 1);
		renderer.setSize(window.innerWidth, window.innerHeight);
		renderer.setPixelRatio(window.devicePixelRatio);

		//Add the scene
		document.body.appendChild(renderer.domElement);

		//Create stars in random locations within a cube
		//Store the stars in an array to be moved within render
		for (let i = 0; i < 3000; i++) {
			let geometry = new SphereBufferGeometry(0.08 * Math.random(), 10, 10);
			let material = new MeshBasicMaterial({
				color: colors[Math.floor(Math.random() * colors.length)],
				envMap: null,
				combine: AddOperation
				//shading: FlatShading
			});
			let star = new Mesh(geometry, material);

			star.position.x = Math.random() * 140 - 70;
			star.position.y = Math.random() * 140 - 70;
			star.position.z = Math.random() * 50 - 25;

			scene.add(star);
			stars.push(star);
		}

		let planeGeometry = new PlaneGeometry(1000, 500, 1, 1);
		let planeMaterial = new MeshBasicMaterial({ color: 0x000000, transparent: true, opacity: 1 });

		planeMesh = new Mesh(planeGeometry, planeMaterial);
		scene.add(planeMesh);
	}

	/*-------------------------
         Render
  --------------------------*/
	function render() {
		//Animation loop
		requestAnimationFrame(render);
		//Add the scene cube plus the camera
		renderer.render(scene, camera);

		//Move stars within a cube and
		//reinitialise the position when the stars go out of the cube
		for (let i = 0; i < stars.length; i++) {
			stars[i].position.z += speed;

			if (stars[i].position.z >= 60) {
				stars[i].position.x = Math.random() * 140 - 70;
				stars[i].position.y = Math.random() * 140 - 70;
				stars[i].position.z = 5;
			}
		}
		//When the mouse is pressed, light effect is activated
		if (activated) {
			speed = lightSpeed;
			planeMesh.material.opacity = 0.001;
		} else {
			if (planeMesh.material.opacity < 1) {
				planeMesh.material.opacity += 0.005;
				speed = normalSpeed;
			}
		}
	}

	export function activateLightspeed() {
		activated = true;
	}

	onMount(async () => {
		window.addEventListener('mousedown', (event) => {
			activated = true;
		});
		window.addEventListener('mouseup', (event) => {
			activated = false;
		});

		addEventListener('resize', () => {
			camera.aspect = window.innerWidth / window.innerHeight;
			camera.updateProjectionMatrix();
			renderer.setSize(window.innerWidth, window.innerHeight);
		});

		init();
		render();
	});
</script>
