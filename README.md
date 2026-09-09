<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Portfolio - กัญญาภัค เจตนาภิวัฒน์</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Kanit', sans-serif;
        }

        body {
            overflow: hidden;
            background-color: #fce4ec;
            color: #5d4037;
        }

        #canvas-container {
            width: 100vw;
            height: 100vh;
            position: absolute;
            top: 0;
            left: 0;
            z-index: 1;
        }

        /* Profile Card Overlay */
        .profile-card {
            position: absolute;
            top: 30px;
            left: 30px;
            z-index: 10;
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            padding: 25px 30px;
            border-radius: 24px;
            box-shadow: 0 8px 32px 0 rgba(225, 190, 231, 0.37);
            border: 2px solid rgba(255, 255, 255, 0.8);
            max-width: 380px;
            pointer-events: auto;
        }

        h1 {
            font-size: 24px;
            color: #8e24aa;
            margin-bottom: 5px;
            font-weight: 600;
        }

        h2 {
            font-size: 16px;
            color: #ec407a;
            margin-bottom: 15px;
            font-weight: 400;
        }

        .info-group {
            margin-bottom: 12px;
            font-size: 14px;
            line-height: 1.6;
            color: #4a148c;
        }

        .skills-tag {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 15px;
        }

        .tag {
            background-color: #f3e5f5;
            color: #ab47bc;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 12px;
            font-weight: 600;
            border: 1px solid #e1bee7;
        }

        .hint {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 10;
            background: rgba(255, 255, 255, 0.8);
            padding: 10px 20px;
            border-radius: 20px;
            font-size: 14px;
            color: #d81b60;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            pointer-events: none;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {transform: translateX(-50%) translateY(0);}
            40% {transform: translateX(-50%) translateY(-10px);}
            60% {transform: translateX(-50%) translateY(-5px);}
        }
    </style>
</head>
<body>

    <!-- UI Overlay -->
    <div class="profile-card">
        <h1>กัญญาภัค เจตนาภิวัฒน์</h1>
        <h2>Portfolio & 3D Showcase</h2>
        
        <div class="info-group">
            <p><strong>อายุ:</strong> 21 ปี</p>
            <p><strong>การศึกษา:</strong> นิสิตชั้นปีที่ 4</p>
            <p>คณะสถาปัตยกรรมศาสตร์ สาขาเกมและอนิเมชัน</p>
        </div>

        <div class="skills-tag">
            <span class="tag">🎨 2D/3D Drawing</span>
            <span class="tag">🗿 3D Modeling</span>
            <span class="tag">🏞️ Environment Design</span>
        </div>
    </div>

    <div class="hint">🌸 คลิกที่ดอกไม้เพื่อปล่อยผึ้งตัวน้อย! 🐝</div>

    <div id="canvas-container"></div>

    <!-- Import Three.js and OrbitControls -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>

    <script>
        // --- 1. SET UP SCENE, CAMERA, RENDERER ---
        const container = document.getElementById('canvas-container');
        const scene = new THREE.Scene();
        
        // Soft Pastel Fog & Background
        scene.background = new THREE.Color(0xfce4ec); 
        scene.fog = new THREE.FogExp2(0xfce4ec, 0.03);

        const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 8, 18);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.shadowMap.enabled = true;
        renderer.shadowMap.type = THREE.PCFSoftShadowMap;
        container.appendChild(renderer.domElement);

        const controls = new THREE.OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;
        controls.maxPolarAngle = Math.PI / 2 - 0.05; // ไม่ให้มุมกล้องมุดลงใต้พื้น
        controls.minDistance = 5;
        controls.maxDistance = 30;

        // --- 2. LIGHTS ---
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.7);
        scene.add(ambientLight);

        const dirLight = new THREE.DirectionalLight(0xfff5e6, 0.8);
        dirLight.position.set(10, 20, 10);
        dirLight.castShadow = true;
        dirLight.shadow.mapSize.width = 2048;
        dirLight.shadow.mapSize.height = 2048;
        scene.add(dirLight);

        // --- 3. ENVIRONMENT (PASTEL GARDEN) ---
        // Ground (Soft Green Island)
        const groundGeo = new THREE.CylinderGeometry(10, 10, 1, 64);
        const groundMat = new THREE.MeshStandardMaterial({ color: 0xc8e6c9, roughness: 0.8 });
        const ground = new THREE.Mesh(groundGeo, groundMat);
        ground.position.y = -0.5;
        ground.receiveShadow = true;
        scene.add(ground);

        // Flowers & Bees Container
        const flowers = [];
        const bees = [];

        // Helper: Create Simple Pastel Flower
        function createFlower(x, z, petalColor) {
            const flowerGroup = new THREE.Group();

            // Stem
            const stemGeo = new THREE.CylinderGeometry(0.05, 0.05, 1.5);
            const stemMat = new THREE.MeshStandardMaterial({ color: 0xa5d6a7 });
            const stem = new THREE.Mesh(stemGeo, stemMat);
            stem.position.y = 0.75;
            stem.castShadow = true;
            flowerGroup.add(stem);

            // Center
            const centerGeo = new THREE.SphereGeometry(0.2, 16, 16);
            const centerMat = new THREE.MeshStandardMaterial({ color: 0xffe082 });
            const center = new THREE.Mesh(centerGeo, centerMat);
            center.position.y = 1.5;
            center.castShadow = true;
            flowerGroup.add(center);

            // Petals
            const petalCount = 5;
            const petalGeo = new THREE.SphereGeometry(0.25, 16, 16);
            petalGeo.scale(1, 0.3, 1.8);
            const petalMat = new THREE.MeshStandardMaterial({ color: petalColor, roughness: 0.5 });

            for (let i = 0; i < petalCount; i++) {
                const petal = new THREE.Mesh(petalGeo, petalMat);
                const angle = (i / petalCount) * Math.PI * 2;
                petal.position.set(
                    Math.sin(angle) * 0.35,
                    1.5,
                    Math.cos(angle) * 0.35
                );
                petal.rotation.y = angle;
                petal.rotation.x = 0.2;
                petal.castShadow = true;
                flowerGroup.add(petal);
            }

            flowerGroup.position.set(x, 0, z);
            
            // Random Scale & Rotation for natural look
            const scale = 0.8 + Math.random() * 0.5;
            flowerGroup.scale.set(scale, scale, scale);
            flowerGroup.rotation.y = Math.random() * Math.PI;

            scene.add(flowerGroup);
            
            // Store reference for Raycasting
            center.userData = { parentGroup: flowerGroup };
            flowers.push(center);
        }

        // Generate Flowers Array with Pastel Colors
        const pastelColors = [0xf48fb1, 0xce93d8, 0xb39ddb, 0x90caf9, 0xffab91];
        for (let i = 0; i < 25; i++) {
            const angle = Math.random() * Math.PI * 2;
            const radius = Math.random() * 8; // Keep within island
            const x = Math.sin(angle) * radius;
            const z = Math.cos(angle) * radius;
            const color = pastelColors[Math.floor(Math.random() * pastelColors.length)];
            createFlower(x, z, color);
        }

        // --- 4. BEE CREATION (SPAWN ON CLICK) ---
        function createBee(position) {
            const beeGroup = new THREE.Group();

            // Body
            const bodyGeo = new THREE.SphereGeometry(0.2, 16, 16);
            bodyGeo.scale(1, 1, 1.3);
            const bodyMat = new THREE.MeshStandardMaterial({ color: 0xffd54f, roughness: 0.4 });
            const body = new THREE.Mesh(bodyGeo, bodyMat);
            beeGroup.add(body);

            // Stripes
            const stripeGeo = new THREE.CylinderGeometry(0.205, 0.205, 0.1, 16);
            const stripeMat = new THREE.MeshStandardMaterial({ color: 0x4e342e });
            const stripe1 = new THREE.Mesh(stripeGeo, stripeMat);
            stripe1.rotation.x = Math.PI / 2;
            stripe1.position.z = 0.05;
            beeGroup.add(stripe1);

            // Wings
            const wingGeo = new THREE.SphereGeometry(0.15, 16, 16);
            wingGeo.scale(1, 0.1, 0.5);
            const wingMat = new THREE.MeshStandardMaterial({ color: 0xffffff, transparent: true, opacity: 0.7 });
            
            const wingL = new THREE.Mesh(wingGeo, wingMat);
            wingL.position.set(0.15, 0.15, 0);
            wingL.rotation.z = 0.3;
            beeGroup.add(wingL);

            const wingR = new THREE.Mesh(wingGeo, wingMat);
            wingR.position.set(-0.15, 0.15, 0);
            wingR.rotation.z = -0.3;
            beeGroup.add(wingR);

            // Position & Setup Fly Animation Data
            beeGroup.position.copy(position);
            beeGroup.position.y += 0.5; // Spawn slightly above flower
            beeGroup.scale.set(0.1, 0.1, 0.1); // Start small for pop effect

            scene.add(beeGroup);

            bees.push({
                mesh: beeGroup,
                wingL: wingL,
                wingR: wingR,
                targetY: beeGroup.position.y + 1.5 + Math.random(),
                speed: 0.02 + Math.random() * 0.02,
                angle: Math.random() * Math.PI * 2,
                radius: 0.5 + Math.random() * 1.5,
                centerPos: beeGroup.position.clone()
            });
        }

        // --- 5. RAYCASTING (INTERACTION) ---
        const raycaster = new THREE.Raycaster();
        const mouse = new THREE.Vector2();

        window.addEventListener('pointerdown', (event) => {
            // Prevent triggering when clicking on UI
            if (event.clientX < 400 && event.clientY < 300) return;

            mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
            mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

            raycaster.setFromCamera(mouse, camera);
            const intersects = raycaster.intersectObjects(flowers);

            if (intersects.length > 0) {
                const flowerCenter = intersects[0].object;
                
                // Animate Flower Bounce
                const parent = flowerCenter.userData.parentGroup;
                let scaleProgress = 0;
                const animateFlower = () => {
                    scaleProgress += 0.1;
                    const scaleEffect = 1 + Math.sin(scaleProgress) * 0.2;
                    parent.scale.set(scaleEffect, scaleEffect, scaleEffect);
                    if (scaleProgress < Math.PI) {
                        requestAnimationFrame(animateFlower);
                    } else {
                        parent.scale.set(1, 1, 1);
                    }
                };
                animateFlower();

                // Spawn Bee
                const worldPos = new THREE.Vector3();
                flowerCenter.getWorldPosition(worldPos);
                createBee(worldPos);
            }
        });

        // --- 6. ANIMATION LOOP ---
        let clock = new THREE.Clock();

        function animate() {
            requestAnimationFrame(animate);

            const elapsedTime = clock.getElapsedTime();

            // Update Bees Animation
            bees.forEach((bee) => {
                // Scale up when spawned
                if (bee.mesh.scale.x < 1) {
                    bee.mesh.scale.addScalar(0.05);
                }

                // Flap wings fast
                bee.wingL.rotation.z = 0.3 + Math.sin(elapsedTime * 30) * 0.3;
                bee.wingR.rotation.z = -0.3 - Math.sin(elapsedTime * 30) * 0.3;

                // Fly in small circles around spawning flower
                bee.angle += bee.speed;
                bee.mesh.position.x = bee.centerPos.x + Math.cos(bee.angle) * bee.radius;
                bee.mesh.position.z = bee.centerPos.z + Math.sin(bee.angle) * bee.radius;
                
                // Floating Up and Down
                bee.mesh.position.y = bee.targetY + Math.sin(elapsedTime * 3 + bee.angle) * 0.3;

                // Rotate bee towards movement direction
                bee.mesh.rotation.y = -bee.angle + Math.PI / 2;
            });

            controls.update();
            renderer.render(scene, camera);
        }

        animate();

        // --- 7. RESPONSIVE RESIZE ---
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
