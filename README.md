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
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Prompt', sans-serif;
        }

        body {
            overflow-x: hidden;
            background-color: #0d0e15;
            color: #ffffff;
        }

        /* Canvas สำหรับ Three.js ฉากหลัง */
        #webgl-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 1;
            pointer-events: none; /* เพื่อให้คลิกทะลุไปกดปุ่มด้านหลังได้ */
        }

        /* Overlay Layout */
        .content-container {
            position: relative;
            z-index: 2;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 2rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        /* Header / Navbar */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
            backdrop-filter: blur(10px);
        }

        .logo {
            font-size: 1.2rem;
            font-weight: 700;
            letter-spacing: 2px;
            color: #00f0ff;
            text-transform: uppercase;
        }

        .nav-links a {
            color: #a0a5c0;
            text-decoration: none;
            margin-left: 2rem;
            transition: color 0.3s;
        }

        .nav-links a:hover {
            color: #00f0ff;
        }

        /* Hero Section */
        .hero {
            margin: auto 0;
            max-width: 650px;
            background: rgba(13, 14, 21, 0.6);
            padding: 2.5rem;
            border-radius: 16px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(12px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
        }

        .tag {
            display: inline-block;
            padding: 0.3rem 0.8rem;
            background: rgba(0, 240, 255, 0.1);
            color: #00f0ff;
            border: 1px solid rgba(0, 240, 255, 0.3);
            border-radius: 20px;
            font-size: 0.85rem;
            margin-bottom: 1rem;
        }

        h1 {
            font-size: 3rem;
            font-weight: 700;
            line-height: 1.2;
            margin-bottom: 1rem;
            background: linear-gradient(45deg, #ffffff, #8a99ad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p.subtitle {
            font-size: 1.1rem;
            color: #a0a5c0;
            margin-bottom: 1.5rem;
            line-height: 1.6;
        }

        .details-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1rem;
            margin-top: 1.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .detail-item h4 {
            font-size: 0.85rem;
            color: #707590;
            text-transform: uppercase;
        }

        .detail-item p {
            font-size: 1rem;
            font-weight: 600;
            color: #e2e8f0;
        }

        .btn-group {
            margin-top: 2rem;
            display: flex;
            gap: 1rem;
        }

        .btn {
            padding: 0.8rem 1.8rem;
            border-radius: 8px;
            font-weight: 600;
            text-decoration: none;
            transition: all 0.3s;
            cursor: pointer;
        }

        .btn-primary {
            background: #00f0ff;
            color: #0d0e15;
            border: none;
        }

        .btn-primary:hover {
            background: #00b8c4;
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.4);
        }

        .btn-outline {
            background: transparent;
            color: #fff;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .btn-outline:hover {
            border-color: #00f0ff;
            color: #00f0ff;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 1rem 0;
            color: #606580;
            font-size: 0.85rem;
        }

        /* Responsive */
        @media (max-width: 768px) {
            h1 { font-size: 2.2rem; }
            .details-grid { grid-template-columns: 1fr; }
            .hero { padding: 1.5rem; }
        }
    </style>
</head>
<body>

    <!-- Three.js Canvas Background -->
    <canvas id="webgl-bg"></canvas>

    <!-- Overlay UI Content -->
    <div class="content-container">
        <nav>
            <div class="logo">KANYAPAK.3D</div>
            <div class="nav-links">
                <a href="#about">เกี่ยวกับ</a>
                <a href="#works">ผลงาน</a>
                <a href="#contact">ติดต่อ</a>
            </div>
        </nav>

        <main class="hero">
            <span class="tag">3D & Game Animation Student</span>
            <h1>กัญญาภัค เจตนาภิวัฒน์</h1>
            <p class="subtitle">
                นักศึกษาชั้นปีที่ 4 ผู้มีความหลงใหลในการออกแบบมิติ空間 (Spatial Design) การสร้างโมเดล 3D และงานอนิเมชั่นสำหรับเกม ผสมผสานศาสตร์แห่งสถาปัตยกรรมเข้ากับโลกดิจิทัล
            </p>
            
            <div class="details-grid">
                <div class="detail-item">
                    <h4>คณะ</h4>
                    <p>สถาปัตยกรรมศาสตร์</p>
                </div>
                <div class="detail-item">
                    <h4>สาขาวิชา</h4>
                    <p>เกมและอนิเมชั่น</p>
                </div>
                <div class="detail-item">
                    <h4>อายุ</h4>
                    <p>21 ปี</p>
                </div>
                <div class="detail-item">
                    <h4>ระดับการศึกษา</h4>
                    <p>ชั้นปีที่ 4 (Senior Year)</p>
                </div>
            </div>

            <div class="btn-group">
                <a href="#works" class="btn btn-primary">ชมผลงาน 3D</a>
                <a href="#contact" class="btn btn-outline">ติดต่อเรา</a>
            </div>
        </main>

        <footer>
            <p>&copy; 2026 Kanyapak Jetanapiwat. Portfolio Built with Three.js</p>
        </footer>
    </div>

    <!-- Import Three.js Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <script>
        // --- THREE.JS SETUP ---
        const canvas = document.querySelector('#webgl-bg');
        const scene = new THREE.Scene();
        
        // เพิ่มหมอก (Fog) ให้ฉากลึกและเนียนขึ้น
        scene.fog = new THREE.FogExp2(0x0d0e15, 0.03);

        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.z = 15;
        camera.position.y = 3;

        const renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true });
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.setSize(window.innerWidth, window.innerHeight);

        // --- OBJECTS (3D World) ---
        
        // 1. Grid (สื่อถึงโครงสร้างสถาปัตยกรรมและพื้นที่ 3D)
        const gridHelper = new THREE.GridHelper(60, 40, 0x00f0ff, 0x1f293d);
        gridHelper.position.y = -4;
        scene.add(gridHelper);

        // 2. Floating Architectural / Game Geometries (วัตถุ 3D ลอยได้)
        const geometries = [
            new THREE.BoxGeometry(2, 2, 2),
            new THREE.IcosahedronGeometry(1.5, 0),
            new THREE.TorusGeometry(1.2, 0.4, 16, 100),
            new THREE.OctahedronGeometry(1.5)
        ];

        const material = new THREE.MeshStandardMaterial({
            color: 0xffffff,
            wireframe: true,
            transparent: true,
            opacity: 0.4
        });

        const objects = [];
        for (let i = 0; i < 25; i++) {
            const randomGeo = geometries[Math.floor(Math.random() * geometries.length)];
            const mesh = new THREE.Mesh(randomGeo, material.clone());
            
            // สุ่มตำแหน่ง
            mesh.position.x = (Math.random() - 0.5) * 40;
            mesh.position.y = (Math.random() - 0.5) * 20;
            mesh.position.z = (Math.random() - 0.5) * 30;

            // สุ่มการหมุน
            mesh.rotation.x = Math.random() * Math.PI;
            mesh.rotation.y = Math.random() * Math.PI;

            // สุ่มขนาด
            const scale = Math.random() * 0.8 + 0.4;
            mesh.scale.set(scale, scale, scale);

            // เปลี่ยนสีขอบเป็นโทน Neon Cyan / Purple
            mesh.material.color.setHex(Math.random() > 0.5 ? 0x00f0ff : 0x7000ff);

            scene.add(mesh);
            objects.push(mesh);
        }

        // --- LIGHTS (แสงสว่าง) ---
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
        scene.add(ambientLight);

        const pointLight = new THREE.PointLight(0x00f0ff, 2, 50);
        pointLight.position.set(5, 5, 5);
        scene.add(pointLight);

        // --- MOUSE PARALLAX EFFECT ---
        let mouseX = 0;
        let mouseY = 0;

        document.addEventListener('mousemove', (e) => {
            mouseX = (e.clientX / window.innerWidth - 0.5) * 2;
            mouseY = (e.clientY / window.innerHeight - 0.5) * 2;
        });

        // --- ANIMATION LOOP ---
        function animate() {
            requestAnimationFrame(animate);

            // หมุนและขยับ Object 3D แต่ละชิ้น
            objects.forEach((obj, index) => {
                obj.rotation.x += 0.005;
                obj.rotation.y += 0.008;
                obj.position.y += Math.sin(Date.now() * 0.001 + index) * 0.005;
            });

            // ขยับมุมกล้องตามพฤติกรรมการขยับเมาส์ (Smooth Parallax)
            camera.position.x += (mouseX * 2 - camera.position.x) * 0.05;
            camera.position.y += (-mouseY * 2 + 3 - camera.position.y) * 0.05;
            camera.lookAt(scene.position);

            renderer.render(scene, camera);
        }

        animate();

        // --- RESIZE HANDLER ---
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
