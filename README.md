<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portfolio - กัญญาภัค เจตนาภิวัฒน์</title>
    
    <!-- Google Fonts (Prompt) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;600;700&display=swap" rel="stylesheet">

    <!-- Three.js CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <style>
        :root {
            --bg-color: #e8f5e9;
            --card-bg: rgba(255, 255, 255, 0.75);
            --primary: #81c784;
            --dark-green: #2e7d32;
            --text-main: #2c3e50;
            --text-sub: #546e7a;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Prompt', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            overflow-x: hidden;
        }

        /* Canvas สำหรับ Three.js ฉากหลัง */
        #webgl-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
        }

        /* Layout หลัก */
        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 2rem;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        /* การ์ดข้อมูลโปรไฟล์ */
        .profile-card {
            background: var(--card-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.8);
            border-radius: 24px;
            padding: 3rem 2.5rem;
            box-shadow: 0 20px 40px rgba(46, 125, 50, 0.08);
            max-width: 650px;
            animation: fadeIn 1.2s ease-out;
        }

        .badge {
            display: inline-block;
            background-color: #a5d6a7;
            color: var(--dark-green);
            padding: 6px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
            letter-spacing: 0.5px;
        }

        h1 {
            font-size: 2.8rem;
            font-weight: 700;
            color: #1b5e20;
            margin-bottom: 0.5rem;
            line-height: 1.2;
        }

        .subtitle {
            font-size: 1.25rem;
            color: var(--text-sub);
            margin-bottom: 1.8rem;
            font-weight: 400;
        }

        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.2rem;
            margin-top: 1.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid rgba(0, 0, 0, 0.08);
        }

        .info-item {
            display: flex;
            flex-direction: column;
        }

        .info-label {
            font-size: 0.85rem;
            color: var(--text-sub);
            margin-bottom: 4px;
        }

        .info-value {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--text-main);
        }

        .cta-btn {
            display: inline-block;
            margin-top: 2rem;
            padding: 12px 32px;
            background-color: var(--dark-green);
            color: #fff;
            text-decoration: none;
            border-radius: 12px;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(46, 125, 50, 0.2);
        }

        .cta-btn:hover {
            background-color: #1b5e20;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(46, 125, 50, 0.3);
        }

        /* Animation */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            h1 { font-size: 2.2rem; }
            .profile-card { padding: 2rem 1.5rem; }
        }
    </style>
</head>
<body>

    <!-- Canvas สำหรับ Three.js -->
    <canvas id="webgl-bg"></canvas>

    <!-- Content ส่วนหน้าเว็บ -->
    <div class="container">
        <div class="profile-card">
            <span class="badge">3D & Game Artist Portfolio</span>
            <h1>กัญญาภัค เจตนาภิวัฒน์</h1>
            <p class="subtitle">สถาปัตยกรรมศาสตร์ • สาขาเกมและอนิเมชั่น</p>
            
            <div class="info-grid">
                <div class="info-item">
                    <span class="info-label">สถานะปัจจุบัน</span>
                    <span class="info-value">นักศึกษาชั้นปีที่ 4</span>
                </div>
                <div class="info-item">
                    <span class="info-label">อายุ</span>
                    <span class="info-value">21 ปี</span>
                </div>
            </div>

            <a href="#works" class="cta-btn">รับชมผลงาน (View Works)</a>
        </div>
    </div>

    <!-- Script สำหรับสร้าง 3D Scene ด้วย Three.js -->
    <script>
        // 1. Scene, Camera, Renderer Setup
        const scene = new THREE.Scene();
        
        // หมอกสีเขียวพาสเทลเพื่อกลมกลืนกับ Background
        scene.background = new THREE.Color(0xe8f5e9);
        scene.fog = new THREE.FogExp2(0xe8f5e9, 0.03);

        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.z = 15;

        const renderer = new THREE.WebGLRenderer({
            canvas: document.querySelector('#webgl-bg'),
            antialias: true
        });
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.setSize(window.innerWidth, window.innerHeight);

        // 2. Lighting (แสง)
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.7);
        scene.add(ambientLight);

        const dirLight1 = new THREE.DirectionalLight(0xa5d6a7, 0.8);
        dirLight1.position.set(5, 10, 7);
        scene.add(dirLight1);

        const dirLight2 = new THREE.DirectionalLight(0x81c784, 0.5);
        dirLight2.position.set(-5, -5, -5);
        scene.add(dirLight2);

        // 3. Create Pastel Floating Objects (สร้างโมเดลเรขาคณิตลอยได้)
        const materials = [
            new THREE.MeshStandardMaterial({ color: 0xc8e6c9, roughness: 0.3, metalness: 0.1 }), // Mint Light
            new THREE.MeshStandardMaterial({ color: 0xa5d6a7, roughness: 0.4, metalness: 0.1 }), // Pastel Green
            new THREE.MeshStandardMaterial({ color: 0x81c784, roughness: 0.2, metalness: 0.2 }), // Medium Pastel
            new THREE.MeshStandardMaterial({ color: 0xe8f5e9, roughness: 0.5, metalness: 0.0 })  // Very Soft Green
        ];

        const geometries = [
            new THREE.IcosahedronGeometry(1.2, 0),
            new THREE.TorusGeometry(1, 0.35, 16, 100),
            new THREE.OctahedronGeometry(1.5, 0),
            new THREE.TetrahedronGeometry(1.3, 0)
        ];

        const objects = [];
        const count = 25; // จำนวนชิ้นงาน 3D ในฉาก

        for (let i = 0; i < count; i++) {
            const geometry = geometries[Math.floor(Math.random() * geometries.length)];
            const material = materials[Math.floor(Math.random() * materials.length)];
            const mesh = new THREE.Mesh(geometry, material);

            // สุ่มตำแหน่ง
            mesh.position.x = (Math.random() - 0.5) * 30;
            mesh.position.y = (Math.random() - 0.5) * 30;
            mesh.position.z = (Math.random() - 0.5) * 20;

            // สุ่มขนาด
            const scale = Math.random() * 0.8 + 0.5;
            mesh.scale.set(scale, scale, scale);

            // สุ่มมุมหมุนเริ่มต้น
            mesh.rotation.x = Math.random() * Math.PI;
            mesh.rotation.y = Math.random() * Math.PI;

            // ค่าความเร็วการหมุนและการลอย
            mesh.userData = {
                rotSpeedX: (Math.random() - 0.5) * 0.01,
                rotSpeedY: (Math.random() - 0.5) * 0.01,
                floatSpeed: Math.random() * 0.01 + 0.005,
                floatOffset: Math.random() * Math.PI * 2
            };

            scene.add(mesh);
            objects.push(mesh);
        }

        // 4. Mouse Interaction (ตอบสนองตามการขยับ เมาส์)
        let mouseX = 0;
        let mouseY = 0;

        window.addEventListener('mousemove', (event) => {
            mouseX = (event.clientX / window.innerWidth - 0.5) * 2;
            mouseY = (event.clientY / window.innerHeight - 0.5) * 2;
        });

        // 5. Animation Loop
        let clock = new THREE.Clock();

        function animate() {
            requestAnimationFrame(animate);

            const elapsedTime = clock.getElapsedTime();

            // เคลื่อนที่วัตถุแต่ละชิ้น
            objects.forEach((obj) => {
                obj.rotation.x += obj.userData.rotSpeedX;
                obj.rotation.y += obj.userData.rotSpeedY;

                // เอฟเฟกต์ลอยขึ้นลงแบบนุ่มนวล
                obj.position.y += Math.sin(elapsedTime * 2 + obj.userData.floatOffset) * 0.003;
            });

            // หมุนมุมกล้องเล็กน้อยตามการเคลื่อนที่ของเมาส์
            camera.position.x += (mouseX * 2 - camera.position.x) * 0.03;
            camera.position.y += (-mouseY * 2 - camera.position.y) * 0.03;
            camera.lookAt(scene.position);

            renderer.render(scene, camera);
        }

        animate();

        // 6. Responsive Window Resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
