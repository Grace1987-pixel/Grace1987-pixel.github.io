<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Portfolio - กัญญาภัค เจตนาภิวัฒน์</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Kanit', sans-serif;
        }

        body {
            overflow: hidden;
            background-color: #fce4ec;
            color: #2c1820;
        }

        #canvas-container {
            width: 100vw;
            height: 100vh;
            position: absolute;
            top: 0;
            left: 0;
            z-index: 1;
        }

        /* Prominent Profile Card Overlay */
        .profile-card {
            position: absolute;
            top: 30px;
            left: 30px;
            z-index: 10;
            background: rgba(255, 255, 255, 0.92);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            padding: 30px 35px;
            border-radius: 28px;
            box-shadow: 0 12px 40px rgba(142, 36, 170, 0.22), 0 2px 10px rgba(0, 0, 0, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.95);
            max-width: 420px;
            pointer-events: auto;
        }

        .profile-badge {
            display: inline-block;
            background: linear-gradient(135deg, #f06292, #ba68c8);
            color: #ffffff;
            font-size: 13px;
            font-weight: 600;
            padding: 4px 14px;
            border-radius: 20px;
            margin-bottom: 12px;
            letter-spacing: 0.5px;
            box-shadow: 0 4px 10px rgba(240, 98, 146, 0.3);
        }

        h1 {
            font-size: 28px;
            color: #4a148c;
            margin-bottom: 4px;
            font-weight: 700;
            letter-spacing: -0.3px;
            line-height: 1.2;
        }

        h2 {
            font-size: 16px;
            color: #d81b60;
            margin-bottom: 18px;
            font-weight: 500;
        }

        .info-group {
            margin-bottom: 20px;
            font-size: 15px;
            line-height: 1.8;
            color: #3e2723;
            background: rgba(243, 229, 245, 0.5);
            padding: 16px;
            border-radius: 18px;
            border: 1px solid rgba(225, 190, 231, 0.6);
        }

        .info-group p strong {
            color: #7b1fa2;
        }

        .skills-title {
            font-size: 14px;
            font-weight: 600;
            color: #6a1b9a;
            margin-bottom: 8px;
        }

        .skills-tag {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }

        .tag {
            background: #ffffff;
            color: #8e24aa;
            padding: 7px 14px;
            border-radius: 16px;
            font-size: 13px;
            font-weight: 600;
            border: 1.5px solid #e1bee7;
            box-shadow: 0 2px 6px rgba(142, 36, 170, 0.08);
            transition: transform 0.2s;
        }

        .tag:hover {
            transform: translateY(-2px);
        }

        /* Hint Notification */
        .hint {
            position: absolute;
            bottom: 25px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 10;
            background: rgba(255, 255, 255, 0.92);
            padding: 12px 26px;
            border-radius: 30px;
            font-size: 15px;
            font-weight: 600;
            color: #c2185b;
            box-shadow: 0 8px 24px rgba(216, 27, 96, 0.18);
            border: 2px solid rgba(255, 255, 255, 0.9);
            pointer-events: none;
            animation: float 3s ease-in-out infinite;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        @keyframes float {
            0%, 100% { transform: translateX(-50%) translateY(0); }
            50% { transform: translateX(-50%) translateY(-8px); }
        }

        /* Responsive UI */
        @media (max-width: 600px) {
            .profile-card {
                top: 15px;
                left: 15px;
                right: 15px;
                max-width: none;
                padding: 20px 22px;
            }
            h1 { font-size: 22px; }
            h2 { font-size: 14px; }
            .info-group { font-size: 13px; padding: 12px; }
        }
    </style>
</head>
<body>

    <!-- UI Overlay (Prominent Profile Card) -->
    <div class="profile-card">
        <span class="profile-badge">PORTFOLIO</span>
        <h1>กัญญาภัค เจตนาภิวัฒน์</h1>
        <h2>3D Artist & Environment Designer</h2>
        
        <div class="info-group">
            <p><strong>อายุ:</strong> 21 ปี</p>
            <p><strong>ระดับการศึกษา:</strong> ชั้นปีที่ 4</p>
            <p><strong>คณะ:</strong> สถาปัตยกรรมศาสตร์</p>
            <p><strong>สาขา:</strong> เกมและอนิเมชัน</p>
        </div>

        <div class="skills-title">ความสามารถหลัก (Key Skills)</div>
        <div class="skills-tag">
            <span class="tag">🎨 การวาดรูป (Drawing)</span>
            <span class="tag">🗿 ปั้น 3D โมเดล (Modeling)</span>
            <span class="tag">🏞️ ออกแบบฉาก (Environment Design)</span>
        </div>
    </div>

    <div class="hint">🌻 ตามหาดอกไม้สีเหลืองเพื่อปล่อยผึ้งตัวน้อย! 🐝</div>

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
        scene.fog = new THREE.FogExp2(0xfce4ec, 0.025);

        const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 10, 22);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.shadowMap.enabled = true;
        renderer.shadowMap.type = THREE.PCFSoftShadowMap;
        container.appendChild(renderer.domElement);

        const controls = new THREE.OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;
        controls.maxPolarAngle = Math.PI / 2 - 0.05;
        controls.minDistance = 6;
        controls.maxDistance = 35;

        // --- 2. LIGHTS ---
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.75);
        scene.add(ambientLight);

        const dirLight = new THREE.DirectionalLight(0xfff5e6, 0.85);
        dirLight.position.set(12, 22, 12);
        dirLight.castShadow = true;
        dirLight.shadow.mapSize.width = 2048;
        dirLight.shadow.mapSize.height = 2048;
        scene.add(dirLight);

        // --- 3. ENVIRONMENT (PASTEL GARDEN) ---
        // Expanded Ground Island
        const groundGeo = new THREE.CylinderGeometry(14, 14, 1.2, 64);
        const groundMat = new THREE.MeshStandardMaterial({ color: 0xc8e6c9, roughness: 0.8 });
        const ground = new THREE.Mesh(groundGeo, groundMat);
        ground.position.y = -0.6;
        ground.receiveShadow = true;
        scene.add(ground);

        // Containers
        const allFlowers = [];
        const yellowFlowers = [];
        const bees = [];

        // Helper: Create Flower
        function createFlower(x, z, petalColor, isYellow = false) {
            const flowerGroup = new THREE.Group();

            // Stem
            const stemGeo = new THREE.CylinderGeometry(0.05, 0.05, 1.5);
            const stemMat = new THREE.MeshStandardMaterial({ color: 0xa5d6a7 });
            const stem = new THREE.Mesh(stemGeo, stemMat);
            stem.position.y = 0.75;
            stem.castShadow = true;
            flowerGroup.add(stem);

            // Center
            const centerGeo = new THREE.SphereGeometry(0.22, 16, 16);
            const centerMat = new THREE.MeshStandardMaterial({ 
                color: isYellow ? 0xffb300 : 0xffe082,
                roughness: 0.4
            });
            const center = new THREE.Mesh(centerGeo, centerMat);
            center.position.y = 1.5;
            center.castShadow = true;
            flowerGroup.add(center);

            // Petals
            const petalCount = 6;
            const petalGeo = new THREE.SphereGeometry(0.26, 16, 16);
            petalGeo.scale(1, 0.3, 1.8);
            const petalMat = new THREE.MeshStandardMaterial({ 
                color: petalColor, 
                roughness: 0.5,
                metalness: isYellow ? 0.1 : 0.0
            });

            for (let i = 0; i < petalCount; i++) {
                const petal = new THREE.Mesh(petalGeo, petalMat);
                const angle = (i / petalCount) * Math.PI * 2;
                petal.position.set(
                    Math.sin(angle) * 0.38,
                    1.5,
                    Math.cos(angle) * 0.38
                );
                petal.rotation.y = angle;
                petal.rotation.x = 0.2;
                petal.castShadow = true;
                flowerGroup.add(petal);
            }

            flowerGroup.position.set(x, 0, z);
            
            const scale = 0.8 + Math.random() * 0.5;
            flowerGroup.scale.set(scale, scale, scale);
            flowerGroup.rotation.y = Math.random() * Math.PI;

            scene.add(flowerGroup);
            
            // Interaction Data
            center.userData = { parentGroup: flowerGroup, isYellow: isYellow };
            
            // Save references
            allFlowers.push(center);
            if (isYellow) {
                yellowFlowers.push(center);
            }
        }

        // Generate Dense Garden (80 Flowers)
        const pastelColors = [0xf48fb1, 0xce93d8, 0xb39ddb, 0x90caf9, 0x80deea, 0xffab91];
        
        // Pick 1 random spot for the single Yellow Flower
        const yellowIndex = Math.floor(Math.random() * 80);

        for (let i = 0; i < 80; i++) {
            const angle = Math.random() * Math.PI * 2;
            const radius = Math.random() * 12.5; // Spread across island
            const x = Math.sin(angle) * radius;
            const z = Math.cos(angle) * radius;

            if (i === yellowIndex) {
                // The ONLY Yellow Flower (Special Interactive)
                createFlower(x, z, 0xffeb3b, true);
            } else {
                // Regular Pastel Flowers
                const color = pastelColors[Math.floor(Math.random() * pastelColors.length)];
                createFlower(x, z, color, false);
            }
        }

        // --- 4. BEE CREATION (WITH FADE OUT EFFECT) ---
        function createBee(position) {
            const beeGroup = new THREE.Group();

            // Materials with transparency enabled for smooth fading
            const bodyMat = new THREE.MeshStandardMaterial({ color: 0xffd54f, roughness: 0.4, transparent: true, opacity: 1 });
            const stripeMat = new THREE.MeshStandardMaterial({ color: 0x3e2723, transparent: true, opacity: 1 });
            const wingMat = new THREE.MeshStandardMaterial({ color: 0xffffff, transparent: true, opacity: 0.75 });

            // Body
            const bodyGeo = new THREE.SphereGeometry(0.22, 16, 16);
            bodyGeo.scale(1, 1, 1.3);
            const body = new THREE.Mesh(bodyGeo, bodyMat);
            beeGroup.add(body);

            // Stripes
            const stripeGeo = new THREE.CylinderGeometry(0.225, 0.225, 0.1, 16);
            const stripe1 = new THREE.Mesh(stripeGeo, stripeMat);
            stripe1.rotation.x = Math.PI / 2;
            stripe1.position.z = 0.05;
            beeGroup.add(stripe1);

            // Wings
            const wingGeo = new THREE.SphereGeometry(0.16, 16, 16);
            wingGeo.scale(1, 0.1, 0.5);
            
            const wingL = new THREE.Mesh(wingGeo, wingMat);
            wingL.position.set(0.16, 0.16, 0);
            wingL.rotation.z = 0.3;
            beeGroup.add(wingL);

            const wingR = new THREE.Mesh(wingGeo, wingMat);
            wingR.position.set(-0.16, 0.16, 0);
            wingR.rotation.z = -0.3;
            beeGroup.add(wingR);

            // Spawn Position & Animation Parameters
            beeGroup.position.copy(position);
            beeGroup.position.y += 0.6;
            beeGroup.scale.set(0.1, 0.1, 0.1);

            scene.add(beeGroup);

            bees.push({
                mesh: beeGroup,
                wingL: wingL,
                wingR: wingR,
                materials: [bodyMat, stripeMat, wingMat],
                targetY: beeGroup.position.y + 1.8 + Math.random() * 0.5,
                speed: 0.02 + Math.random() * 0.02,
                angle: Math.random() * Math.PI * 2,
                radius: 0.8 + Math.random() * 1.5,
                centerPos: beeGroup.position.clone(),
                createdAt: performance.now(),
                lifespan: 30000 // 30 Seconds Total
            });
        }

        // --- 5. RAYCASTING & CLICK EVENTS ---
        const raycaster = new THREE.Raycaster();
        const mouse = new THREE.Vector2();

        window.addEventListener('pointerdown', (event) => {
            // Ignore click if over profile UI
            if (event.clientX < 450 && event.clientY < 380) return;

            mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
            mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

            raycaster.setFromCamera(mouse, camera);
            const intersects = raycaster.intersectObjects(allFlowers);

            if (intersects.length > 0) {
                const flowerCenter = intersects[0].object;
                const parent = flowerCenter.userData.parentGroup;

                // Bounce animation for clicked flower
                let scaleProgress = 0;
                const animateFlower = () => {
                    scaleProgress += 0.12;
                    const scaleEffect = 1 + Math.sin(scaleProgress) * 0.25;
                    parent.scale.set(scaleEffect, scaleEffect, scaleEffect);
                    if (scaleProgress < Math.PI) {
                        requestAnimationFrame(animateFlower);
                    } else {
                        parent.scale.set(1, 1, 1);
                    }
                };
                animateFlower();

                // Check if it's the YELLOW flower!
                if (flowerCenter.userData.isYellow) {
                    const worldPos = new THREE.Vector3();
                    flowerCenter.getWorldPosition(worldPos);
                    createBee(worldPos);
                }
            }
        });

        // --- 6. ANIMATION & FADE OUT LOOP ---
        let clock = new THREE.Clock();

        function animate() {
            requestAnimationFrame(animate);

            const elapsedTime = clock.getElapsedTime();
            const now = performance.now();

            // Loop backwards to remove faded bees
            for (let i = bees.length - 1; i >= 0; i--) {
                const bee = bees[i];
                const age = now - bee.createdAt;

                // 30-Second Lifetime Logic
                if (age >= bee.lifespan) {
                    // Remove bee from scene
                    scene.remove(bee.mesh);
                    bee.mesh.traverse((child) => {
                        if (child.geometry) child.geometry.dispose();
                    });
                    bees.splice(i, 1);
                    continue;
                }

                // Scale up when spawned
                if (bee.mesh.scale.x < 1) {
                    bee.mesh.scale.addScalar(0.06);
                }

                // Smooth Fade Out towards the end of lifespan (Fade during last 10 seconds or gradually)
                // Linear fade across the 30 seconds for gradual effect
                const remainingRatio = 1 - (age / bee.lifespan); // 1.0 down to 0.0
                const alpha = Math.max(0, remainingRatio);

                bee.materials[0].opacity = alpha; // Body
                bee.materials[1].opacity = alpha; // Stripe
                bee.materials[2].opacity = alpha * 0.75; // Wing

                // Flap wings fast
                bee.wingL.rotation.z = 0.3 + Math.sin(elapsedTime * 35) * 0.35;
                bee.wingR.rotation.z = -0.3 - Math.sin(elapsedTime * 35) * 0.35;

                // Orbit around spawn area
                bee.angle += bee.speed;
                bee.mesh.position.x = bee.centerPos.x + Math.cos(bee.angle) * bee.radius;
                bee.mesh.position.z = bee.centerPos.z + Math.sin(bee.angle) * bee.radius;
                
                // Gentle Bobbing
                bee.mesh.position.y = bee.targetY + Math.sin(elapsedTime * 2.5 + bee.angle) * 0.35;

                // Face movement direction
                bee.mesh.rotation.y = -bee.angle + Math.PI / 2;
            }

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
